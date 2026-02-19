# 🤖 HydroBot (ESP32 Indoor Garden)

Un système de jardinage d'intérieur intelligent et hackable, basé sur un kit hydroponique standard modifié avec un ESP32 pour une intégration complète dans Home Assistant (ESPHome).

## 💡 Idées de Noms pour le Projet
Si ce nom ne te plaît pas, voici d'autres suggestions :
1.  `smart-grow-box`
2.  `esphome-hydroponics`
3.  `ha-indoor-garden`
4.  `green-esp32`

---

## 🛒 Liste des Courses & Coûts Estimés
Voici le matériel nécessaire (liens validés).

| Composant | Modèle & Lien | Prix Approx. |
| :--- | :--- | :--- |
| **Le Kit de Base** | [Kit Hydroponique 12 Capsules (Amazon)](https://www.amazon.fr/dp/B0D83Q2BG6) <br> *Base "bête" à hacker (Bac + Pompe + LED).* | ~ 50,00 € |
| **Cerveau** | **ESP32 WROOM-32** (38 pins) | ~ 6,00 € |
| **Alimentation** | [Buck Converter VISSQH](https://www.amazon.fr/dp/B0D5QZ16MR) <br> *Pour passer du 24V du kit au 5V de l'ESP.* | ~ 10,00 € (lot) |
| **Lumière (PWM)** | [MOSFET IRLZ44N](https://www.amazon.fr/dp/B0CBKH4XGL) <br> *Lot de 10. Logic Level (3.3V) pour le dimming LED.* | ~ 7,00 € (lot) |
| **Pompe (ON/OFF)** | [Relais 5V Optocouplé (DollaTek)](https://www.amazon.fr/dp/B07DJ4NRC1) <br> *Pour piloter la pompe.* | ~ 6,00 € |
| **Niveau (Jauge)** | [Capteur Capacitif v1.2 (AZDelivery)](https://www.amazon.fr/dp/B07HJ6N1S4) <br> *⚠️ À vernir/siliconer en haut ! Sert de jauge 0-100%.* | ~ 2,00 € |
| **Niveau (Alerte)** | [Flotteur Vertical (Sourcingmap)](https://www.amazon.fr/s?k=sourcing+map+interrupteur+flotteur+vertical) <br> *Sécurité coupure pompe si vide.* | ~ 6,00 € |
| **Air** | **BME280** (Temp/Hum/Pression) | ~ 4,00 € |
| **Lumière Ambiante** | **BH1750** (Stock) | - |
| **Total Estimé** | | **~ 91,00 €** |

---

## 🔌 Plan de Câblage (ESP32 38-pin)

| Composant | Pin ESP32 | Type | Notes |
| :--- | :--- | :--- | :--- |
| **I2C SDA** | GPIO **21** | Data | Pour BME280 & BH1750 (En parallèle) |
| **I2C SCL** | GPIO **22** | Clock | Pour BME280 & BH1750 (En parallèle) |
| **Lumière LED** | GPIO **16** | PWM Output | Via MOSFET (Gate). Résistance 10k recommandée. |
| **Pompe Eau** | GPIO **4** | Switch | Via Relais (IN). |
| **Jauge (Capacitif)** | GPIO **34** | Analog Input | Pin "Input Only", parfait pour l'ADC. |
| **Flotteur (Alerte)** | GPIO **25** | Binary Input | Mode `INPUT_PULLUP`. Circuit fermé = Eau OK. |

*Note : Alimenter l'ESP32 via le pin 5V (VIN) sortie du Buck Converter.*

---

## 🛠️ Instructions de Montage Rapide
1.  **Démonter** la base du potager pour accéder au contrôleur d'origine.
2.  **Couper** les fils des LEDs et de la Pompe.
3.  **Régler** le Buck Converter : Brancher au 24V du potager et tourner la vis jusqu'à avoir **5.0V** pile en sortie.
4.  **Câbler** selon le tableau ci-dessus.
5.  **Protéger** le capteur capacitif (vernis) avant immersion.
6.  **Flasher** le code ESPHome.

