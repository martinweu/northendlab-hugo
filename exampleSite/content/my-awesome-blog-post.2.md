+++
author = "Martin Weber"
categories = ["Meta Data"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-2.jpg"
title = "AdGuard und Pi-hole"
type = "post"

+++
Es ist natürlich eine gewissens Frage ob man Werbeblocker verwenden möchte oder nicht. Natürlich sie nervt, benötigt Bandbreite, erzeugt Spuren und belastet den Akku unseres Endgeräts. Sie finanziert aber auch die Inhalte die wir konsumieren. Das mal vorab gesagt habe ich mich entschlossen die Werbeinnahmen der Contentbranche nicht zu schmälern. Dennoch betreibe ich einen DNS basierten Content und Tracking Blocker auf meinem Homeassistant. Von Endgeräten mit denen ich Inhalte konsumiere wird dieser jedoch nicht verwendet, er dient ausschließlich dazu die Erzähllaune meiner SmartHome Geräte etwas im Blick zu behalten bzw. einzuschränken. Bis vor kurzem nutzte ich dafür hauptsächlich Pi-hole, da die Entwicklung an der Integration mit HomeAssistant aber eingestellt wurde bin ich nun zu AdGuard gewechselt. Beide sind als Erweiterung direkt in HomeAssistant über den Add-On Store installierbar und benötigen für den standard Anwenungsfall keine zusätzliche Konfiguration. Natürlich müssen beide als DNS-Server bei den entsprechenden Endgeräten eingetragen werden. Dies kann man natürlich für jedes Geräte manuell einstellen oder (wie ich) die Einstellungen über den DHCP-Server verteilen lassen. Alles wichtige funktioniert wie gehabt. Die top-Listen der geblockten Domains beinhalten im wesentlichen das was ich von Pihole schon kannte. Auch das Verhältnis aus geblockten zu zugelassen DNS-Abfragen hat sich gegenüber Pihole nicht geändert. In der Funktion lässt sich für mich absolut kein Unterschied feststellen.  Die Auswertungs-und Analyse-Dashboards bei Pihole boten aber mehr Funktionalität.