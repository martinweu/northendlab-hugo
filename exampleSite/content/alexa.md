+++
author = "Martin Weber"
categories = ["Hugo"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-3.jpg"
title = "Alexa"
type = "post"

+++
Gleich mal vorweg ich verwende Alexa (Amazon Echo Geräte) mit drei unterschiedlichen Anbindungen in meinem SmartHome.

1. via Spotify
2. Alexa Media Player (Community Paket)
3. NodeRed - Virtual Hue Bridge

Über die Spotify-HomeAssistant-Integration kann ich die Echo-Geräte wie auch andere mit Spotify verbunden Geräte als Wiedergabegeräte anwählen. Dies ist sowohl im UserInterface aber auch über verschiedene Abläufe welche ich in NodeRed erstellt habe möglich.

Die zweite Integration erfolgt über das Community Paket Alexa Media Player welches ich über HACS installiert habe. Damit habe ich die Möglichkeit Sprachausgaben an die jeweiligen Echo Geräte zu senden bzw. die für die einzelnen Geräte programmieren Wecker oder Timer auszulesen. 

Die dritte Integration erfolgt über ein NodeRed-Paket welches eine HUE-Bridge simuliert. Alle Amazon Echo-Devices (auch die ohne SmartHome-Hub, also auch Dots) können über das lokale Netzwerk mit einer Philips-Hue Bridge kommunizieren. Soweit mir bekannt, ist das die einzige Integration die direkt imlokalen Netzwerk erfolgt.