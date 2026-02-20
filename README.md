# 🤖 HydroBot (ESP32 Indoor Garden)

Un système de jardinage d'intérieur intelligent et hackable, basé sur un kit hydroponique standard modifié avec un ESP32 pour une intégration complète dans Home Assistant (ESPHome).

## 🎯 Objectifs du Projet
Transformer un kit hydroponique "bête" en un robot jardinier autonome et connecté.

### 👁️ Ce qu'il surveille :
*   **🌱 Sol :** Humidité de la terre (Capacitif) pour savoir quand les racines ont soif.
*   **💧 Eau :** Niveau du réservoir (0-100%) + Alerte critique (Flotteur) pour ne pas griller la pompe.
*   **🌡️ Air :** Température, Humidité et Pression atmosphérique (BME280).
*   **☀️ Lumière :** Intensité lumineuse ambiante (BH1750) pour adapter l'éclairage.

### 🤖 Ce qu'il gère :
*   **💡 Soleil Artificiel :** Cycle Jour/Nuit automatique avec allumage progressif (PWM 30s) pour respecter le rythme des plantes.
*   **🌊 Arrosage :** Pilotage de la pompe (Cycles ON/OFF programmables, ex: 15min/h).
*   **🏠 Home Assistant :** Remontée de toutes les stats et pilotage manuel via WiFi (ESPHome).

---

## 🛒 Liste des Courses & Coûts Estimés
Voici le matériel nécessaire (liens validés).

## 💰 Budget Comparatif

Tu as le choix entre la rapidité (Amazon) ou l'économie (AliExpress pour l'électronique).
**La base reste la même (Amazon) pour la qualité/SAV.**

| Composant | Option A : Tout Amazon (Rapide) | Option B : Mixte (Éco) |
| :--- | :--- | :--- |
| **Kit Base** | [Amazon (12 Capsules)](https://www.amazon.fr/dp/B0D83Q2BG6) : **69,98 €** | [Amazon (12 Capsules)](https://www.amazon.fr/dp/B0D83Q2BG6) : **69,98 €** |
| **ESP32** | [Amazon](https://www.amazon.fr/dp/B071P98VTG) : 8,49 € | [AliExpress](https://fr.aliexpress.com/item/1005007820190456.html) : 3,69 € |
| **Buck Conv.** | [Amazon (Lot)](https://www.amazon.fr/dp/B0D5QZ16MR) : 9,66 € | [AliExpress](https://fr.aliexpress.com/item/1005007055625007.html) : 1,48 € |
| **MOSFET** | [Amazon (Lot)](https://www.amazon.fr/dp/B0CBKH4XGL) : 11,99 € | [AliExpress](https://fr.aliexpress.com/item/1005009242758699.html) : 2,11 € |
| **Relais 5V** | [Amazon](https://www.amazon.fr/dp/B07DJ4NRC1) : 4,99 € | [AliExpress](https://fr.aliexpress.com/item/1005005319972049.html) : 1,99 € |
| **Capa. Soil** | [Amazon (Lot)](https://www.amazon.fr/dp/B07HJ6N1S4) : 5,99 € | [AliExpress](https://fr.aliexpress.com/item/1005005973892592.html) : 1,16 € |
| **Flotteur** | [Amazon](https://www.amazon.fr/s?k=sourcing+map+interrupteur+flotteur+vertical) : 8,99 € | [AliExpress](https://fr.aliexpress.com/item/1005003292793524.html) : 1,82 € |
| **BME280** | [Amazon](https://www.amazon.fr/dp/B07PAB23G3) : 4,99 € | [AliExpress](https://fr.aliexpress.com/item/1005008728942141.html) : 0,98 € |
| **TOTAL** | **~ 125,08 €** | **~ 83,21 €** |
| **Gain** | - | **41,87 €** (et du rab !) |

*Note : Les prix AliExpress incluent la livraison standard (souvent gratuite ou faible), mais compte 10-15 jours de délai.*

---

## 🤔 Dilemme : DIY vs LetPot ?

Tu hésites à "te faire chier" avec le DIY ? Voici le comparatif honnête pour t'aider à trancher.

| Critère | 🤖 HydroBot (DIY) | 📦 LetPot (Commercial) |
| :--- | :--- | :--- |
| **Prix** | **~ 83 €** (Mixte) à **125 €** (Amazon) | **~ 100-150 €** (Selon promo) |
| **Effort** | 🛠️ **Moyen** (Soudure, Flash, Montage) | 🟢 **Nul** (Plug & Play) |
| **Home Assistant** | ✅ **100% Local** (ESPHome) <br> *Zéro Latence, Zéro Cloud.* | ☁️ **Cloud** (Intégration Tuya/LetPot) <br> *Dépend d'internet + Compte chinois.* |
| **Réparabilité** | ⭐⭐⭐⭐⭐ (Tout se change pour <5€) | ⭐⭐ (Si l'électronique lâche, c'est poubelle) |
| **Satisfaction** | 🏆 "C'est moi qui l'ai fait !" | 😐 "J'ai acheté un truc." |

**Verdict :**
*   Choisis **LetPot** si tu veux **juste des plantes** sans bricoler et que le Cloud ne te gêne pas.
*   Garde **HydroBot** si tu veux un **objet unique**, durable, et totalement privé pour ton Home Assistant.

## 🔌 Plan de Câblage (ESP32 38-pin)

| Composant | Pin ESP32 | Type | Notes |
| :--- | :--- | :--- | :--- |
| **I2C SDA** | GPIO **21** | Data | Pour BME280 & BH1750 (En parallèle) |
| **I2C SCL** | GPIO **22** | Clock | Pour BME280 & BH1750 (En parallèle) |
| **Lumière LED** | GPIO **16** | PWM Output | Via MOSFET (Gate). Résistance 10k recommandée. |
| **Pompe Eau** | GPIO **4** | Switch | Via Relais (IN). |
| **Jauge (Capacitif)** | GPIO **34** | Analog Input | Pin "Input Only", parfait pour l'ADC. |
| **Flotteur (Alerte)** | GPIO **25** | Binary Input | Mode `INPUT_PULLUP`. Circuit fermé = Eau OK. |
| **INA226 (Option)** | I2C (21/22) | Power Monitor | *Adresse 0x40. Monitorer conso 24V.* |

*Note : Alimenter l'ESP32 via le pin 5V (VIN) sortie du Buck Converter.*

## ⚡ Monitoring Énergie (Optionnel)
Tu veux savoir combien ça consomme ? Deux options :

1.  **La Prise Connectée (Recommandé)** :
    *   Branche tout le système sur une prise Zigbee (ex: **[NOUS A1Z](https://www.amazon.fr/dp/B0054PSKYW)** ou **Sonoff S26**).
    *   ✅ **Avantages** : Précis, Sécurisé, "Kill-Switch" d'urgence, Zéro câblage.
2.  **Le Capteur Intégré (DIY)** :
    *   Ajoute un module **[INA226 (AliExpress)](https://fr.aliexpress.com/item/1005003292793524.html)** sur le bus I2C.
    *   ⚠️ **Attention** : Prends bien un **INA226** (Max 36V) et PAS un INA219 (Max 26V), car le kit est en 24V (trop risqué pour le 219).
    *   *Câblage* : VIN+ sur le 24V, VIN- vers le kit. I2C sur GPIO 21/22.

---

## 🛠️ Instructions de Montage Rapide
1.  **Démonter** la base du potager pour accéder au contrôleur d'origine.
2.  **Couper** les fils des LEDs et de la Pompe.
3.  **Régler** le Buck Converter : Brancher au 24V du potager et tourner la vis jusqu'à avoir **5.0V** pile en sortie.
4.  **Câbler** selon le tableau ci-dessus.
5.  **Protéger** le capteur capacitif (vernis) avant immersion.
6.  **Flasher** le code ESPHome.

---

## 🥬 Consommables & Semis
Pour démarrer tes cultures, il te faudra :

### 🌟 Option Tout-en-un (Recommandé)
*   **[Kit de Recharge Yoocaa (Amazon)](https://www.amazon.fr/dp/B09L17SJJ4)** : Contient **Éponges + Engrais A&B Solide**.
    *   *Note : Les paniers ne s'achètent pas en recharge, tu réutiliseras ceux fournis avec le bac.*

### 🛠️ Option au Détail
1.  **Les Éponges (Substrat)** : Cherche **"Éponges de culture hydroponique"** sur Amazon/AliExpress.
    *   *Astuce* : Prends les "compatibles AeroGarden/iDOO", c'est le standard qui rentre partout.
2.  **Les Paniers** : Normalement fournis avec le kit, mais si besoin cherche **"Paniers culture hydroponique"**.
3.  **La Nourriture (Engrais)** : Cherche **"Engrais Hydroponique A+B"**.
    *   *Important* : Il faut un engrais LIQUIDE spécial hydro (souvent vendu en 2 bouteilles A et B à mélanger). N'utilise pas d'engrais terreau classique !
4.  **Les Graines** : N'importe quelles graines de commerce (Basilic, Laitue, Tomates Cerises...).

