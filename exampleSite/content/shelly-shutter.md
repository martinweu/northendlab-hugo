+++
author = "Martin Weber"
categories = ["Home Automation"]
date = 2020-03-30T04:00:00Z
description = "This is meta description"
image = "/images/photo-1528501905679-0eb90962e249.jfif"
title = "Shelly 2.5 als Jalousiensteuerung"
type = "post"

+++

## Shelly Installation

Ich verwende einen Shelly 2.5 um meine Jalousien welche über einen propritären Controller angesteuert werden in mein SmartHome einzubinden. Da der propritäre Controller keine Möglichkeit bietet ihn über LAN/USB/Wifi/Zigbee anzusteueren, simuliere ich das Drücken eines Wandschalters mit einen Shelly 2.5. Die regulärenen an den Wänden verbauten Doppelschalter werden bei meiner Installation mit zwei Anoden und einer Kathode versorgt. Da der Shelly 2.5 im Gegensatz zu seinem älteren Bruder, dem Shelly 1 nicht potentialfrei schaltet muss der Shelly 2.5 hiermit mit den gleichen 12V versorgt werden mit denen auch der Controller arbeitet. Der propritärer Controller besitzt neben den Sensor-Eingängen und Schalt-Ausgängen auch einen 12V Anschluss. Daher habe ich mich entschlossen den Shelly 2.5 direkt im Schaltkasten neben dem Controller zu platzieren. An meinem Controller sind 4 Jalousien mit jeweils separaten Wandschaltern angeschlossen. Zusätzlich gibt es einen Schalter der alle 4 Jalousien gemeinsam steuert. Da ich meistens alle Jalousien nach oben oder unten fahre, wird nur dieser Zentralscalter in mit einem Shelly 2.5 ausgestattet und so ins SmartHome zu integrieren. Es wäre natürlich auch möglich jede Jalousie einzeln zu integrieren. Hierbei muss jedoch ein Shelly 2.5 pro Jalousie verwendet werden, da ja pro Jalsousie ein nach oben und ein nach unten Schalter zu simulieren ist.

![Shelly 2.5](/images/post/shelly-25.jpg "Shelly 2.5 (source: shelly.cloud)")

Ist der Shelly 2.5 erst mal verkabelt, ist das nach oben und nach unten Fahren schnell über die Shelly App oder den im Shelly integrierten Webserver auszuprobieren. Auch die Anbindung an Home Assistant über MQTT ist schnell erledigt und unterscheidet sich nicht von der Einbindung eines Shellys als Smarten Lichtschalter ([siehe mein erster Shelly Blogpost](../shelly-switches/)).

### Home Assistant MQTT Switches

    switch:
      - platform: mqtt
        name: shadesdown
        state_topic: "shellies/shellyswitch25-11F9FD/relay/0"
        command_topic: "shellies/shellyswitch25-11F9FD/relay/0/command"
        qos: 2
        payload_on: "on"
        payload_off: "off"
        retain: false
        optimistic: false
      - platform: mqtt
        name: shadesup
        state_topic: "shellies/shellyswitch25-11F9FD/relay/1"
        command_topic: "shellies/shellyswitch25-11F9FD/relay/1/command"
        qos: 2
        payload_on: "on"
        payload_off: "off"
        retain: false
        optimistic: false

## Jalousien in Home Assistant

Um die Jalousien nun aber auch als solche in Home Assistant abzubilden müssen wir noch ein paar Dinge konfigurieren.
Zuerst erstellen wir unsere Jalousien Objekt. Wir nutzen hier keine Home Assistant Logik oder Funktionalität sondern lediglich das User Interface. Ziel ist es das Öffnen, Schließen und Kippen zu ermöglichen. Wir verwenden stop für die Kipp Funktion. open und close blieben bei ihrer ursprünglichen Funktionalität.

### Jalousien Objekt konfigurieren

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

Um den Status im System verfügbar zu haben schreiben wir diesen in die 3 input_boolean variablen welche wir im nächsten Konfigurationsblock nun definieren.
Auf Änderungen dieser 3 boolschen variablen können wir dann aus NodeRed reagieren.

### Konfiguration der 3 input_booleans

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

## NodeRed für die Ablaufsteuerung

In NodeRed können wir an die drei input_booleans trigger hängen welche dann die Prozesskette anstoßen. Das Öffnen und Schließen ist hierbei denkbar einfach. wir sezten den entsprechenden Schalter für ca. 1 Sekunde auf on und schalten ihn danach wieder aus. Zusätzlich schalten wir auch das input boolean Feld wieder auf aus.

### Kippen und Timing
Das Kippen der Jalousien erfordert auch bei manueller Bedienung schon etwas Timing. Hier kommen in meinem Setup einige Probleme zusammen. Mein Jalousien Controller reagiert mit abweichender Verzögerung auf den Zentralschalter. Bei den Einzelschaltern ist diese (gefühlt) konstanter. Zusätlich entstehen durch WIFI, MQTT, HomeAssistant, NodeRed stark schwankende Verzögerungen. Im Gegensatz zur manuellen Bedienung habe ich hier auch kein Feedback ob die Jalousien sich bereits bewegen oder nicht. Um das Kippen dennoch möglichst zuverlässig zu implementieren bediene ich mich einiger Tricks.

Bevor ich die Jalousien durch das Einschalten eines Schalters in Bewegung versetzte, schalte ich diesen ausgeschalteten Schalter nochmal aus. Damit ist die Verbindung zwischen NodeRed, HomeAssistant, MQTT-Server und Shelly schon mal aufgewärmt. 200ms später setzte ich den Schalter auf on. Bei meinen Tests hat sich herausgestellt, dass die Verzögerung beim vom Shelly gesendeten Events etwas konstanter ist, als die bei der Umsetzung von Schaltbefehlen die an den Shelly gesendet werden. Daher warte ich auf die Bestätigung des Shellies, dass dieser geschaltet hat, bevor ich den Timer für das Ausschalten des Shellies (Loslassen des virtuellen Tasters) sende. Die Jalousien sind nun immer noch in Bewegung zur Kipp-Position. Es muss nun so lange (bei mir zusätzliche 300ms) gewartet werden wie es dauert bis die Jalousien diese Position (fast) erreicht haben. Stoppen lassen sich die Jaslousien in meinem Fall durch das kurze Betätigen des jeweils anderen Schalters. Da auch diese Reaktion etwas verzögert erfolgt, muss sie etwas vor dem Erreichen der Endposition ausgelöst werden.

![NodeRed Jalousiensteuerung](/images/post/node-red-shades.png "NodeRed Jalousiensteuerung")


## Links
* [Shelly](https://shelly.cloud)
* [Shelly 2.5 auf Amazon](https://www.amazon.de/Shelly-Dual-WLAN-Schalter-Messfunktion/dp/B07Q9M2Y1S/ref=pd_sbs_60_1/259-7694751-8299156?_encoding=UTF8&pd_rd_i=B07Q9M2Y1S&pd_rd_r=333081d1-3415-404a-8de4-b34b3cfadf5a&pd_rd_w=1xh0j&pd_rd_wg=TtJJz&pf_rd_p=42bf0ad8-ce6f-4127-a2f0-106727020a41&pf_rd_r=5CBB398VN4NCJ48XKJRB&psc=1&refRID=5CBB398VN4NCJ48XKJRB&tag=napster220203-21)