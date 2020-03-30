+++
author = "Martin Weber"
categories = ["Design Tools"]
date = 2020-03-30T04:00:00Z
description = "This is meta description"
image = "/images/photo-1528501905679-0eb90962e249.jfif"
title = "Shelly 2.5 als Jalousiensteuerung"
type = "post"

+++
Ich verwende einen Shelly 2.5 um meine Jalousien welche über einen propritären Controller angesteuert werden in mein SmartHome einzubinden. Da der propritäre Controller keine Möglichkeit bietet ihn über LAN/USB/Wifi/Zigbee anzusteueren, simuliere ich das Drücken eines Wandschalters mit einen Shelly 2.5. Die regulärenen an den Wänden verbauten Doppelschalter werden bei meiner Installation mit zwei Anoden und einer Kathode versorgt. Da der Shelly 2.5 im Gegensatz zu seinem älteren Bruder, dem Shelly 1 nicht potentialfrei schaltet muss der Shelly 2.5 hiermit mit den gleichen 12V versorgt werden mit denen auch der Controller arbeitet. Der propritärer Controller besitzt neben den Sensor-Eingängen und Schalt-Ausgängen auch einen 12V Anschluss. Daher habe ich mich entschlossen den Shelly 2.5 direkt im Schaltkasten neben dem Controller zu platzieren. An meinem Controller sind 4 Jalousien mit jeweils separaten Wandschaltern angeschlossen. Zusätzlich gibt es einen Schalter der alle 4 Jalousien gemeinsam steuert. Da ich meistens alle Jalousien nach oben oder unten fahre, wird nur dieser Zentralscalter in mit einem Shelly 2.5 ausgestattet und so ins SmartHome zu integrieren. Es wäre natürlich auch möglich jede Jalousie einzeln zu integrieren. Hierbei muss jedoch ein Shelly 2.5 pro Jalousie verwendet werden, da ja pro Jalsousie ein nach oben und ein nach unten Schalter zu simulieren ist.

![Shelly 2.5](https://shelly.cloud/wp-content/uploads/2019/01/shelly-25.png "Shelly 2.5 (source: shelly.cloud)")

Ist der Shelly 2.5 erst mal verkabelt ist das nach oben und nach unten fahren schnell über die Shelly App oder den im Shelly integrierten Webserver auszuprobieren. Auch die erste Anbindung an Home Assistant über MQTT ist schnell erledigt und unterscheidet sich nicht von der Einbindung eines Shellys als Smarten Lichtschalter (siehe mein erster Shelly Blogpost). Um die Jalousien nun aber auch als solche in Home Assistant abzubilden müssen wir noch ein paar Dinge konfigurieren. 

    light:
      - platform: mqtt
        name: shadesdown
        state_topic: "shellies/shellyswitch25-68F9FD/relay/0"
        command_topic: "shellies/shellyswitch25-68F9FD/relay/0/command"
        qos: 2
        payload_on: "on"
        payload_off: "off"
        retain: false
        optimistic: false
      - platform: mqtt
        name: shadesup
        state_topic: "shellies/shellyswitch25-68F9FD/relay/1"
        command_topic: "shellies/shellyswitch25-68F9FD/relay/1/command"
        qos: 2
        payload_on: "on"
        payload_off: "off"
        retain: false
        optimistic: false

Zuerst erstellen wir unsere Jalousien Objekt. Wir nutzen hier keine Home Assistant Logik oder Funktionalität sondern lediglich das User Interface. Ziel ist es das Öffnen, Schließen und Kippen zu ermöglichen. Wir verwenden stop für die Kipp Funktion. open und close blieben bei ihrer ursprünglichen Funktionalität.

    cover:
      - platform: template
        covers:
          shades:
            device_class: blind
            friendly_name: "Shades"
            position_template: 50
            icon_template: mdi:window-shutter
            open_cover:
              service: input_boolean.turn_on
              data:
                entity_id: input_boolean.open_shades
            stop_cover:
              service: input_boolean.turn_on
              data:
                entity_id: input_boolean.tilt_shades
            close_cover:
              service: input_boolean.turn_on
              data:
                entity_id: input_boolean.close_shades

 Um den Status der User Interface Tasten im System verfügbar zu haben schreiben wir diesen in die 3 input_boolean variablen welche wir im nächsten Konfigurationsblock nun definieren.

    input_boolean:
      close_shades:
        name: "Close Shades"
        initial: off
        icon: mdi:window-shutter
      open_shades:
        name: "Open Shades"
        initial: off
        icon: mdi:window-shutter-open
      tilt_shades:
        name: "Tilt Shades"
        initial: off
        icon: mdi:window-shutter-alert

Somit haben wir die Konfiguration in Home Assistant selbst abgeschlossen. Die Logik zur Steuerung der Jalousien selbst bilde ich in NodeRed ab.

In NodeRed können wir an die drei input_booleans trigger hängen welche dann die Prozesskette anstoßen. Das Öffnen und Schließen ist hierbei denkbar einfach. wir sezten einfach den entsprechenden Schalter für ca. 1 Sekunde auf on und schalten ihn danach wieder aus. Zusätzlich schalten wir auch das input boolean feld wieder auf aus.

Das Kippen der Jalousien erfordert auch bei manueller Bedienung schon etwas Timing. Hier kommen in meinem Setup einige Probleme zusammen. Meine Jalousien Controller reagiert mit abweichender Verzögerung auf den Zentralschalter, auch bei manueller Bedienung. Bei den Einzelschaltern ist diese (gefühlt) konstanter. Zusätlich entstehen durch WIFI, MQTT, HomeAssistant, NodeRed (auch stark schwankende) Verzögerungen. Im Gegensatz zur manuellen Bedienung habe ich hier auch kein Feedback ob die Jalousien sich bereits bewegen oder nicht. Um das Kippen dennoch möglichst zuverlässig zu implementieren bediene ich mich einiger Tricks.

Bevor ich die Jalousien durch das Einschalten eines Schalters in Bewegung versetzte, schalte ich diesen (ausgeschalteten) Schalter nochmal aus. Damit ist die Verbindung zwischen NodeRed, HomeAssistant, MQTT-Server und Shelly schon aufgewärmt. 200ms später setzte ich den Schalter auf on. Bei meinen Tests hat sich herausgestellt, dass die Verzögerung beim vom Shelly gesendeten Events etwas konstanter ist, als die bei der Umsetzung von Schaltbefehlen die an den Shelly gesendet werden. Daher warte ich auf die Bestätigung des Shellies, dass dieser geschaltet hat, bevor ich den Timer für das Ausschalten des Shellies ( Loslassen des virtuellen Tasters) sende. Die Jalousien sind nun immer noch in Bewegung zur Kipp-Position. Es muss nu so lange (bei mir zusätzliche 300ms) gewartet werden wie es dauert bis die Jalousien diese Position (fast) erreicht haben. Stoppen lassen sich die Jaslousien in meinem Fall durch das kurze Betätigen des jeweils anderen Schalters. Da auch diese Reaktion etwas verzögert erfolgt muss sie etwas vor dem Erreichen der Endposition ausgelöst werden.