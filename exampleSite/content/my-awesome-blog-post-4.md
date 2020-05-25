+++
author = "Martin Weber"
categories = ["Hugo"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-3.jpg"
title = "Shelly 1 und Shelly 2.5 Relay"
type = "post"

+++
In meinem SmartHome verwendet ich mehrere Shelly 1 und Shelly 2.5. Alle davon sind hinter herkömmlichen Lichtschalter verbaut. Den ursprünglichen Plan auf die Shellies Tasmoto aufzuspielen habe ich angesichts der einfach funktionierenden MQTT Einbindung und der guten Weboberfläche verworfen. 2 Shellies 2.5 sind direkt im Schaltschrank an 4 Relais angeschlossen. Die Relais werden für die Schaltkreise benötigt welche mittels Taster geschaltet werden. Für den Shelly ist das Relais und die vielen Taster also nichts anderes als ein einfacher Schalter.

## Home Assistant

Die Shellies werden bei mir über MQTT in das Smart Home eingebunden. Home Assistant kann dann darüber den Status auslesen und die Schaltbefehle aus dem Webinterface auf die Shellies übertragen. Am Shelly muss man dazu den MQTT Server konfigurieren und im Home Assistant die Shellys als MQTT Devices eintragen.

### Konfiguration in Home Assistant

Die nachfolgenden Konfigurationen hab ich im Block _light_ erstellt. Hier müsst ihr natürlich den Namen des Shelly anpassen. Die Shelly 2.5 heißen shellyswitch25-Seriennummer die Shelly 1 nur shelly1-Seriennummer. Für den zweiten Kanal des Shelly 2.5 einfach die beiden 0 in state_topic und command_topic durch zwei 1 ersetzen.

* Für den Shelly 1:

      - platform: mqtt
        name: kitchenspot
        state_topic: "shellies/shelly1-67DC99/relay/0"
        command_topic: "shellies/shelly1-67DC99/relay/0/command"
        qos: 2
        payload_on: "on"
        payload_off: "off"
        retain: false
        optimistic: false
* Für den ersten Kanal des Shelly 2.5:

      - platform: mqtt
        name: hall
        state_topic: "shellies/shellyswitch25-6926D6/relay/0"
        command_topic: "shellies/shellyswitch25-6926D6/relay/0/command"
        qos: 2
        payload_on: "on"
        payload_off: "off"
        retain: false
        optimistic: false

## Schalter entkoppeln

Die meisten meiner Shellies betreibe ich so das der physikalische Schalter seine normale Funktion behält und der Shelly nur eine zusätzliche Schaltmöglichkeit bietet. Dadurch ist die normale Schaltfunktion auch bei einem Netzwerkausfall gewährleistet. Einige wenige Schalter habe ich jedoch durch den Shelly virtuell vom Schaltkreis entkoppelt. Die physische Verkabelung des Shellies bleibt hier ident. Der Kontakt welcher durch Drücken des Schalters erzeugt wird, wird nun nicht mehr direkt vom angebundenen Shelly als Aufforderung zum Umschalten seines Ausgangs interpretiert, sondern lediglich als MQTT-Event an Home Assistant gesendet. Dort kann dann entschieden werden was mit dem Umlegen des Schalters ausgelöst werden soll.

### Mehrere Geräte mit einen Schalter steuern

Neben den Reaktionsmöglichkeiten die Home Assistant bietet kann das Event aber auch in NodeRed verarbeitet werden. Ich habe so zum Beispiel zusätzlich zum regulären Küchenlicht einen Wifi-RGB-LED Controller eingebunden. Das wäre ansich auch noch ohne die Entkopplung und der damit einhergehenden Funktionsuntüchtigkeit der Beleuchtung im Falle eines Ausfalls des Home Assistants oder WLANs möglich. In diesem Fall kann es aber sein, dass das reguläre Küchenlicht aus und der LED-Streifen an ist. Dann soll der Schalter beim ersten Drücken den LED-Streifen ausschalten und nicht das reguläre Küchenlicht einschalten. Somit kann der Shelly die Entscheidung über den Schaltvorgang nicht selbst treffen sondern muss diesen an den Home Assistant delegieren.

### Smarte Lampen

Ein anderes Beispiel wo es Sinn mach über die Entscheidung über das Schaltverhalten nicht am Shelly sonderen am Home Assistant zu treffen, ist bei der Verwendung von smarten Lampen (z.B.: Philips Hue, ...). Diese können zwar mit dem Wegfallen der Spannung umgehen und auch deren Verhalten kann entsprechend konfiguriert werden, jedoch können sie natürlich ohne Strom nicht eingeschaltet werden. Das bedeutet dass Home Assistant zuerst mit dem Shelly die Stromversorgung der smarten Lampe herstellen muss bevor er eine entsprechende Lichteinstellung übertragen kann. Möchte ich zum Beispiel das Schlafzimmerlicht in der Nach nur auf 10% schalten, wird es bevor Home Assistant die Dimmung senden kann auf die Helligkeitsstufe schalten die beim Wegfall der Stromversorgung aktiv war. Man könnte natürlich die smarten Lampe auch so einstellen dass diese beim erneuten Herstellen der Stromversorgung erstmal dunkel bleibt, dann funktioniert der physikalische Schalter alleine aber auch nicht mehr.

## Web Interface

Auf allen Shellies läuft auch ein eigenes Webinterface welches durch Benutzername und Passwort geschütz wird. Dies ermöglicht die einfache Konfiguration und auch das aktualisierter der Firmware. Einige meiner Shelly 1 kamen noch mit einer Firmware welche noch keine MQTT Unterstützung bot. Dies wurde aber durch die schon bereit liegene neue Softwareversion behoben. Das Aktualisieren der Firmware funktioniert mit einem Click und dauert in etwa 1-2 Minuten. In meinem Fall hat auch noch kein Shelly dabei seine Einstellungen verlohren.

## Fazit

Nach nun mittlerweile 7 Monaten im Einsatz kann ich von keinem einzigen Verbindungsabriss oder anderen Funktionsstörung berichten. Ich muss sagen, dass ich damit nicht gerechnet hatte. Mir sind bisher keine so zuverlässigen Geräte aus dem Home Automation Sektor bekannt.