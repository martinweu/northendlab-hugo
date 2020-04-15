+++
author = "Martin Weber"
categories = ["Meta Data"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-1.jpg"
title = "RGB-LED WIFI-Controller"
type = "post"

+++
RGB-LED Streifen waren aber das mein erster Schritt in Richtung Homeautomation. Das Philips Hue System kam erst wesentlich später dazu. Ich verwende mehrere Meter RGB(W)-LED Strips zur indirekten Beleuchtung. 

## Netzwerkkonfiguration

Dafür verwende ich bisher zwei unterschiedliche Modelle welche sich aber alle durch die MagicHome-App konfigurieren lassen. Beide Controller bauen ein eigenes WLAN-Netzwerk auf in durch welches die Controller dann erstmalig konfiguriert werden können. Dabei ist natürlich auch die Einbindung in ein schon existierendes WLAN möglich. Dem RGB-Modell kann hierbei auch eine statische IP-Adresse zugewiesen werden. Das ist beim RGBW-Modell nicht möglich. Ich würde aber eher davon abraten die IP-Adresse auf den Geräten direkt zu vergeben. Die Zuteilung einer fixen IP-Adresse anhand der jeweiligen MAC-Adresse durch den DHCP-Server ist hier die elegantere Lösung. Für die spätere Konfiguration im Home Assistant ist nämlich eine gleichbleibende IP-Adresse oder ein DNS-Name nötig. Unter FHEM hatte ich mit dem RGBW-Modell öfters mal Probleme (Verbindungsabrisse, ignorierte Kommandos), seit ich mit Home Assistant arbeite funktionieren aber beide Modelle anstandslos.

## RGB-Controller

bild und link einfügen

## RGBW-Controller

bild und link einfügen