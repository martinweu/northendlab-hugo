+++
author = "Martin Weber"
categories = ["Networking"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/access-point.jpg"
title = "Networking"
type = "post"

+++
## Vorwort

Mit dem Smarthome holt man sich auch einige Geräte mit zumindest fragwürdiger Security ins Haus. Hier beschreibe ich meine Gedanken bei der Umsetztung eines möglichst funktionalen und sicheren Netzwerksetups. Die Umsetzung einiger meiner Überlegungen scheiterte oft an Limitierungen der verwendeten Smarthome Geräte. Was mir am öftesten in die Quere kam waren mit Abstand die zwanghafte Autodiscovery-Funktionen durch Broadcasting-Mechanismen. Ohne die Probleme dabei immer genau validiert zu haben bin ich mir aber relativ sicher, dass mit manueller Konfiguration vieles möglich gewesen wäre was sich so nicht umsetzten lies. Die stärkere Verbreitung von Smart Homes Komponenten macht es Bastlern wie mir natürlich oft deutlich einfacher an gewünsche Hardware zu kommen, sie führt aber auch dazu, dass der Konfigurationsumfang bedingt durch die Benutzerfreudlichkeit abstriche machen muss.

## Subnetzte
![Ubiquiti Edge Router X](/images/post/edge-router.jpg "Ubiquiti Edge Router X")

Ein erster Schritt für verbesserte Security ist einmal das trennen von vertraulichem und nicht vertraulichen Geräten. Der Computer mit aktuellen Sicherheitsupdates von dem aus ich Online-Banking betreibe sollte nicht im gleichen Netzwerk liegen wie der 5 Jahre alte LED Controller aus Fernost. Diese Trennung kann zum Beispiel durch Subnetzte und passend konfigurierte Firewall-Regeln erfolgen. Physischen RJ45 Steckplätzen an meinem Ubiquiti Edge Router X kann ich somit also ein bestimmtes Netzwerk zuweisen.

### Broadcasts

Ein so schön getrenntes Netz bringt aber auch seine Probleme mit sich. Aufpassen muss man mit Smart-Home Geräten welche Kommunikation über Broadcast vorraussetzten. Das kann die Alexa sein die eine Philips Hue bridge durch eine Suche im lokalen netzwerk finden möchte und keine Konfiguration der IP-Adresse erlaubt. Aber auch das TV-Gerät welches man über Wake-On-Lan (WOL) eingeschalten werden möchte.

## Mit VLANs zu WLANs

![Access Point](/images/post/access-point-angle.jpg "Access Point")

Wie sieht das ganze jetzt im WLAN aus? Natürlich könnte man für jedes Subnetz jetzt einen eigenen Access-Point betreiben und somit die Netztrennung auf für WLAN umsetzten. Einfacher geht das aber mit der Hilfe von VLANs und einem Access Point der mit VLANs umgehen kann. Die VLANs sind bei mir am Edge Router konfiguriert und werden auch an die einzelnen RJ45 Steckplätze verteilt. Meine Phlips Hue Bridge wird dem Home Automation VLAN und damit auch dem entsprechenden Subnet zugeordnet. Mein Desktop-PC kommt ins Management VLAN. Zum WLAN Access Point müssen wir mehrere VLANs weiterreichen. Der WLAN Access Point spannt dann mehrere WLANs mit unterschiedlichem Namen (SSID) und Passphrase auf, welche je einem VLAN zugeordnet werden. Es gibt dann also wieder das Home Automation WLAN und das Management WLAN. Beide mit unterschiedlicher Passphrase. Der WLAN Access Point stellt dabei sicher das die Trennung der VLANs auch über Funk eingehalten wird.

## Powerline
![Powerline](/images/post/powerline.jpg "Powerline")

Obwohl mein TV-Gerät WLAN-fähig ist verwende ich für die Anbindung ans Netzwerk die TP-Link Powerline Adapter. Durch die Anbindung via Powerline habe ich nämlich die Möglichkeit den TV mittels Wake on Lan einzuschalten. Mehr dazu ([hier](../samsung-tv/)).

## Links
* [Ubiquiti Edge Router X auf Amazon](https://www.amazon.de/ER-X-Ubiquiti-Network-Router/dp/B011N1IT2A/ref=sr_1_1?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=edgerouter+x&qid=1591035704&sr=8-1)
* [TP Link Access Points auf Amazon](https://www.amazon.de/s?k=tplink+accesspoint&__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&ref=nb_sb_noss)
* [TP-Link Powerline auf Amazon](https://www.amazon.de/TP-Link-TL-PA4010-s-Ethernet-Port-energiesparend-kompatibel/dp/B00A0VBPLM/ref=sr_1_19?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=powerline+tplink&qid=1591038717&sr=8-19)