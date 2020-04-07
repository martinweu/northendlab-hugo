+++
author = "Martin Weber"
categories = ["Hugo"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-3.jpg"
title = "Shelly 1 Relay"
type = "post"

+++
I use the shellys to integrate my regular electricity installation to my smart home.
Home Assistant is working together perfectly. Although shellys are able to run tasmoto. The stock firmware is handling MQTT perfectly. Via the Mosquitto MQTT Broker which I run via Home Assistant on my Raspberry Pi 4 (4GB).

In meinem SmartHome verwendet ich mehrere Shelly 1 und Shelly 2.5. Alle davon sind hinter herkömmlichen Lichtschalter verbaut. Den ursprünglichen Plan auf die Shellies Tasmoto aufzuspielen habe ich angesichts der einfach funktionierenden MQTT Einbindung und der guten Weboberfläche verworfen. 2 Shellies 2.5 sind direkt im Schaltschrank an 4 Relais angeschlossen. Die Relais werden für die Schaltkreise benötigt welche mittels Taster geschaltet werden. Für den Shelly ist das Relais und die vielen Taster also nichts anderes als ein einfacher Schalter.

Die meisten meiner Shellie betreibe ich so das der Physikalische-Schalter seine normale Funktion behält und der Shelly nur eine zusätzliche Schaltmöglichkeit bietet. Dadurch ist die normale Schaltfunktion auch bei einem Netzwerkausfall gewährleistet. Einige wenige Schalter habe ich jedoch virtuell vom Schaltkreis entkoppelt. Die physische Verkabelung des Shellies bleibt hier ident. Das Signal was durch Drücken des Schalters erzeugt wird, wird nun nicht mehr direkt vom Shelly als Aufforderung zum Umschalten seines Ausgangs interpretiert, sondern lediglich als Event an Home Assistant gesendet. Dort wird dann ein Ablauf in NodeRed gestartet der die entsprechenden Schaltbefehle ausführt. Ich habe so zum Beispiel zusätzlich zum regulären Küchenlicht einen Wifi-RGB-LED Controller eingebunden. Das wäre ansich auch noch ohne die Entkopplung, und der damit einhergehenden Funktionsuntüchtigkeit der Beleuchtung im Falle eines Ausfalls des Home Assistants oder WLANs, möglich. Je doch kann es in meinem Fall sein, dass das reguläre Küchenlicht aus ist, aber der LED-Streifen an ist. Dann soll der Schalter beim ersten Drücken den LED-Streifen ausschalten und eben nicht das reguläre Küchenlicht einschalten.