+++
author = "Martin Weber"
categories = ["Hugo"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-3.jpg"
title = "Shelly 1 Relay"
type = "post"

+++
In meinem SmartHome verwendet ich mehrere Shelly 1 und Shelly 2.5. Alle davon sind hinter herkömmlichen Lichtschalter verbaut. Den ursprünglichen Plan auf die Shellies Tasmoto aufzuspielen habe ich angesichts der einfach funktionierenden MQTT Einbindung und der guten Weboberfläche verworfen. 2 Shellies 2.5 sind direkt im Schaltschrank an 4 Relais angeschlossen. Die Relais werden für die Schaltkreise benötigt welche mittels Taster geschaltet werden. Für den Shelly ist das Relais und die vielen Taster also nichts anderes als ein einfacher Schalter.

Die meisten meiner Shellie betreibe ich so das der Physikalische-Schalter seine normale Funktion behält und der Shelly nur eine zusätzliche Schaltmöglichkeit bietet. Dadurch ist die normale Schaltfunktion auch bei einem Netzwerkausfall gewährleistet. Einige wenige Schalter habe ich jedoch durch den Shelly virtuell vom Schaltkreis entkoppelt.

## Schalter entkoppeln

Die physische Verkabelung des Shellies bleibt hier ident. Der Kontakt welcher durch Drücken des Schalters erzeugt wird, wird nun nicht mehr direkt vom angebundenen Shelly als Aufforderung zum Umschalten seines Ausgangs interpretiert, sondern lediglich als MQTT-Event an Home Assistant gesendet. Dort kann dann entschieden werden was mit dem Umlegen des Schalters ausgelöst werden soll. 

### Mehrere Geräte mit einen Schalter steuern

Neben den Reaktionsmöglichkeiten die Home Assistant bietet kann das Event aber auch in NodeRed verarbeitet werden. Ich habe so zum Beispiel zusätzlich zum regulären Küchenlicht einen Wifi-RGB-LED Controller eingebunden. Das wäre ansich auch noch ohne die Entkopplung und der damit einhergehenden Funktionsuntüchtigkeit der Beleuchtung im Falle eines Ausfalls des Home Assistants oder WLANs möglich. In diesem Fall sein kann es aber sein, dass das reguläre Küchenlicht aus und der LED-Streifen an ist. Dann soll der Schalter beim ersten Drücken den LED-Streifen ausschalten und nicht das reguläre Küchenlicht einschalten. 

### Smarte Lampen

Ein anderes Beispiel wo es Sinn mach über die Entscheidung über das Schaltverhalten nicht am Shelly sonderen am Home Assistant zu treffen, ist bei der Verwendung von smarten Lampen (z.B.: Philips Hue, ...). Diese können zwar mit dem Wegfallen der Spannung umgehen und auch deren Verhalten kann entsprechend konfiguriert werden, jedoch können sie natürlich ohne Strom nicht eingeschaltet werden. Das bedeutet dass Home Assistant zuerst mit dem Shelly die Stromversorgung der smarten Lampe herstellen muss bevor er eine entsprechende Lichteinstellung übertragen kann. Möchte ich zum Beispiel das Schlafzimmerlicht in der Nach nur auf 10% schalten, wird es bevor Home Assistant die Dimmung senden kann auf die Helligkeitsstufe schalten die beim Wegfall der Stromversorgung aktiv war. Man könnte natürlich die smarten Lampe auch so einstellen dass diese beim erneuten Herstellen der Stromversorgung erstmal dunkel bleibt, dann funktioniert der physikalische Schalter alleine aber auch nicht mehr.