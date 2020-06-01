+++
author = "Martin Weber"
categories = ["Light"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/rgbw-controller-both.jpg"
title = "RGB(W)-LED WIFI-Controller"
type = "post"

+++
RGB-LED Streifen waren aber das mein erster Schritt in Richtung Homeautomation. Das Philips Hue System kam erst wesentlich später dazu. Ich verwende mehrere Meter RGB(W)-LED Strips zur indirekten Beleuchtung. 
Dafür verwende ich bisher zwei unterschiedliche Modelle welche sich aber alle durch die MagicHome-App konfigurieren lassen. Beide Controller bauen ein eigenes WLAN-Netzwerk auf in durch welches die Controller dann erstmalig konfiguriert werden können. Dabei ist natürlich auch die Einbindung in ein schon existierendes WLAN möglich.
## Netzwerkkonfiguration
Dem RGB-Modell kann hierbei auch eine statische IP-Adresse zugewiesen werden. Das ist beim meinem RGBW-Modell nicht möglich. Ich würde aber eher davon abraten die IP-Adresse auf den Geräten direkt zu vergeben. Die Zuteilung einer fixen IP-Adresse anhand der jeweiligen MAC-Adresse durch den DHCP-Server ist hier die elegantere Lösung. Für die spätere Konfiguration im Home Assistant ist nämlich eine gleichbleibende IP-Adresse oder ein DNS-Name nötig. Unter FHEM hatte ich mit dem RGBW-Modell öfters mal Probleme (Verbindungsabrisse, ignorierte Kommandos), seit ich mit Home Assistant arbeite funktionieren aber beide Modelle anstandslos.

## Hardware
### RGB-Controller

![RGB Controller](/images/post/rgb-controller.jpg "RGB Controller")

### RGBW-Controller

![RGBW Controller](/images/post/rgbw-controller.jpg "RGBW Controller")

## Links
* [RGB Wifi Controller für MagicHome App auf Amazon](https://www.amazon.de/s?k=rgb+wifi+led+magic+home&__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&ref=nb_sb_noss)