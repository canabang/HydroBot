# 🤖 HydroBot (ESP32 Indoor Garden)

Un système de jardinage d'intérieur intelligent et hackable, basé sur un kit hydroponique standard modifié avec un ESP32 pour une intégration complète dans Home Assistant (ESPHome).

## 🎯 Objectifs du Projet
Transformer un kit hydroponique "bête" en un robot jardinier autonome et connecté.

### 👁️ Ce qu'il surveille :
*   **💧 Eau (Niveau) :** Jauge du réservoir (0-100%) via le capteur capacitif + Alerte critique via un Flotteur physique (pour stopper et ne pas griller la pompe si le bac est vide).
*   **🌡️ Eau (Température) :** Température de la solution nutritive (DS18B20) pour éviter la prolifération de bactéries (Pythium).
*   **🌡️ Air :** Température, Humidité et Pression atmosphérique de la pièce (BME280).
*   **☀️ Lumière :** Intensité lumineuse ambiante (BH1750) pour adapter automatiquement la puissance de l'éclairage.

### 🤖 Ce qu'il gère :
*   **💡 Soleil Artificiel (2 Canaux) :** Gestion indépendante de la Croissance (Blanc/Bleu) et Floraison (Rouge) via 2 MOSFETs. Allumage progressif (PWM 30s).
*   **🌊 Arrosage :** Pilotage de la pompe de circulation d'eau (Cycle 30min ON / 30min OFF par défaut).
*   **🏠 Home Assistant (Le Cerveau) :**
    *   **Contrôle Total des Lumières :** Pilotage séparé ou combiné des canaux Blanc/Bleu et Rouge. Tu as des boutons ON/OFF dédiés et des curseurs pour régler l'intensité de 0% à 100% pour chaque canal.
    *   **Pilotage Pompe :** Bouton pour forcer l'allumage manuel ou l'arrêt de la pompe hors cycle.
    *   **📱 Télécommande Tactile Dédiée :** Un écran déporté autonome de 4.3" (ESP32-S3) s'intègre au système pour le pilotage et l'affichage des graphiques (niveau d'eau, température).

---

## 🛒 Liste des Courses & Coûts Estimés
Voici le matériel nécessaire (liens validés).

## 💰 Budget Comparatif

Tu as le choix entre la rapidité (Amazon) ou l'économie (AliExpress pour l'électronique).
**La base reste la même (Amazon) pour la qualité/SAV.**

| Composant & Rôle | Option A : Tout Amazon (Rapide) | Option B : Mixte (Éco) |
| :--- | :--- | :--- |
| **Kit Base Yoocaa**<br>*Bac, pompe intégrée, et rampe LED d'origine.* | [Yoocaa (12 Capsules)](https://www.amazon.fr/dp/B092D7L1Y8) : **69,98 €** | [Yoocaa (12 Capsules)](https: //www.amazon.fr/dp/B092D7L1Y8) : **69,98 €** |
| **ESP32 (Modèle WROOM-32 ou WROVER)**<br>*Le cerveau avec Wi-Fi pour Home Assistant.* | [Amazon](https://www.amazon.fr/dp/B071P98VTG) : 8,49 € | [AliExpress](https://fr.aliexpress.com/item/1005007820190456.html) : 4.29 € |
| **Carte d'Extension ESP32 (38 Pins)**<br>*Borniers à vis pour tout brancher proprement sans soudures "en l'air".* | [Amazon (Similaire)](https://www.amazon.fr/s?k=esp32+38+pin+expansion+board) : ~ 8,99 € | [AliExpress](https://fr.aliexpress.com/item/1005007840748529.html) : 2,59 € |
| **Buck Converter (LM2596)**<br>*Abaisse le 24V du potager en 5V pour alimenter l'ESP32.* | [Amazon (Lot)](https://www.amazon.fr/dp/B0D5QZ16MR) : 9,66 € | [AliExpress](https://fr.aliexpress.com/item/1005007053,695625007.html) : 1,49 € |
| **Module MOSFET (D4184 ou LR7843) x2**<br>*Interrupteurs avec borniers pour régler l'intensité des LEDs sans soudure complexe.* | [Amazon (Lot de 5)](https://www.amazon.fr/dp/B0DG8KH7HQ) : 7,85 € | [AliExpress](https://fr.aliexpress.com/item/4000532890256.html) : 2x 0,77 € |
| **Module Relais 5V (1 Canal)**<br>*Interrupteur "ON/OFF" brut pour allumer/éteindre la pompe à eau.* | [Amazon](https://www.amazon.fr/dp/B07DJ4NRC1) : 4,99 € | [AliExpress](https://fr.aliexpress.com/item/1005006280813881.html) : 1,12 € |
| **Capteur Capacitif (v1.2 / v2.0)**<br>*Détourné de son usage : Mesure le niveau d'eau (0-100%) dans le bac.* | [Amazon (Lot)](https://www.amazon.fr/dp/B07HJ6N1S4) : 5,99 € | [AliExpress](https://fr.aliexpress.com/item/1005005973892592.html) : 1,16 € |
| **Interrupteur à Flotteur**<br>*Sécurité: Coupe la pompe physiquement si le bac est vide.* | [Amazon](https://www.amazon.fr/s?k=sourcing+map+interrupteur+flotteur+vertical) : 8,99 € | [AliExpress](https://fr.aliexpress.com/item/33054312857.html) : 1,47 € |
| **BME280**<br>*Capteur de climat (Temp/Hum/Pression) autour des feuilles.* | [Amazon](https://www.amazon.fr/dp/B07PAB23G3) : 4,99 € | [AliExpress](https://fr.aliexpress.com/item/1005008728942141.html) : 4,29 € |
| **BH1750**<br>*Capteur de luminosité (Lux) pour baisser/monter les LEDs selon le soleil.* | [Amazon (Lot de 3)](https://www.amazon.fr/ICQUANZX-BH1750FVI-DIntensit%C3%A9-Num%C3%A9rique-Alimentation/dp/B07VF15XJJ) : 7,49 € | [AliExpress](https://fr.aliexpress.com/item/1005009671465215.html) : 0,99 € |
| **DS18B20**<br>*Sonde étanche pour l'alerte température d'eau.* | [Amazon (Lot de 3)](https://www.amazon.fr/OUDQFCJ-capteur-temp%C3%A9rature-num%C3%A9rique-inoxydable/dp/B0D1G5BVGV) : 7,49 € | [AliExpress](https://fr.aliexpress.com/item/1005004899620913.html) : 1,26 € |
| **Écran Tactile 4.3"**<br>*Télécommande déportée indépendante (ESP32-S3).* | [Amazon (Waveshare)](https://www.amazon.fr/dp/B0CNZ6CHR7) : 41,79 € | [AliExpress (SpotPear)](https://fr.aliexpress.com/item/1005009526082638.html) : 37.39 € |
| **TOTAL** | **~ 186,70 €** | **~ 127,57 €** |
| **Gain** | - | **59,13 €** |

*Note : Les prix AliExpress incluent la livraison standard (souvent gratuite ou faible), mais compte 10-15 jours de délai.*

---

## 🔌 Plan de Câblage (ESP32 38-pin)

| Composant | Pin ESP32 | Type | Notes |
| :--- | :--- | :--- | :--- |
| **I2C SDA** | GPIO **21** | Data | Pour BME280 & BH1750 (En parallèle) |
| **I2C SCL** | GPIO **22** | Clock | Pour BME280 & BH1750 (En parallèle) |
| **Lumière Croissance**| GPIO **16** | PWM Output | Via MOSFET 1 (LEDs Blanches/Bleues). |
| **Lumière Floraison** | GPIO **17** | PWM Output | Via MOSFET 2 (LEDs Rouges). |
| **Pompe Eau** | GPIO **4** | Switch | Via Relais (IN). |
| **Jauge (Capacitif)** | GPIO **34** | Analog Input | Pin "Input Only", parfait pour l'ADC. |
| **Flotteur (Alerte)** | GPIO **25** | Binary Input | Mode `INPUT_PULLUP`. Circuit fermé = Eau OK. |
| **Température Eau** | GPIO **26** | 1-Wire | Capteur DS18B20 étanche. Besoin résistance 4.7k entre Data et 3.3V. |

*Note : Alimenter l'ESP32 via le pin 5V (VIN) sortie du Buck Converter.*

## ⚡ Monitoring Énergie
La gestion de l'énergie et la remontée de consommation se feront via une **prise connectée Zigbee** (ex: NOUS A1Z ou Sonoff S26).

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

---

## 🌱 Guide Pas-à-Pas : Le Démarrage des Semis

L'erreur numéro 1 des débutants est de mettre de l'engrais dès le premier jour. Les graines ont leur propre réserve d'énergie, l'engrais va les brûler ! Voici la méthode infaillible pour démarrer à partir de zéro :

### Étape 1 : Le Semis (Jour 1)
1.  **Préparation de l'eau :** Remplis le bac de ton potager jusqu'à la ligne "Max" avec de l'eau claire du robinet. **Aucun engrais pour l'instant !**
2.  **Préparation de l'éponge :** Mouille complètement tes éponges (substrat) sous le robinet pour bien les hydrater avant de les utiliser.
3.  **Les graines :** Place 2 à 3 graines maximum dans le petit trou au centre de chaque éponge (si tu mets trop de graines, elles vont s'étouffer entre elles plus tard).
4.  **Mise en place :** Insère l'éponge dans le panier en plastique, puis place le panier dans un des trous du bac.
5.  **L'effet Serre :** Recouvre chaque panier avec le petit dôme transparent en plastique (fourni avec le kit). Cela garde l'humidité à 100% pour réveiller la graine.
6.  **Lumière & Pompe :** Allume la pompe (cycle de base, ex: 15min on / 45min off). Allume la lumière (12h à 14h par jour).

### Étape 2 : La Germination (Jour 3 à Jour 14)
*   Surveille tous les jours à travers les dômes.
*   Dès que tu vois une plante sortir et que ses petites feuilles commencent à toucher le haut du dôme transparent, **retire le dôme définitivement**. Si tu le laisses, la plante va moisir.
*   L'eau baisse un peu à cause de l'évaporation ? Rajoute juste de l'eau claire.

### Étape 3 : Le Repas (Quand 2 vraies feuilles apparaissent)
Au bout de 2 à 3 semaines, tes plantes feront entre 3 et 5 cm de haut et auront développé leurs "vraies feuilles" (pas les deux premières petites feuilles rondes de naissance). C'est le moment de les nourrir !
1.  Vérifie que ton bac est rempli d'eau jusqu'au repère.
2.  Prépare ton **engrais liquide A et B** en respectant les doses indiquées sur les bouteilles (généralement autour de 2 à 3 ml de chaque par litre d'eau).
3.  *Astuce : verse bien le produit A, mélange l'eau, puis verse le produit B, ne mélange jamais les produits purs ensemble.*
4.  Optionnel : C'est ici que tu peux ajuster le pH de ton eau (idéal 6.0) si tu as un testeur.

### Étape 4 : L'Entretien (Chaque Semaine)
*   Vérifie le niveau d'eau. Les grands plants de menthe ou basilic boivent énormément en été (plus d'un litre tous les 3 jours !).
*   Rajoute de l'eau mélangée à de l'engrais (ne rajoute pas que de l'eau claire avec le temps, sinon l'eau va devenir pauvre en nutriments).
*   **Taille tes plantes :** N'hésite pas à couper les têtes de ton basilic pour le forcer à faire des branches sur le côté, sinon il va pousser tout droit, toucher la lampe et brûler.

---

## 💰 Dépenses Réelles (Historique d'Achat)
Afin de garder une trace du coût effectif du projet (qui diffère du budget théorique grâce à la récupération de matériel et aux promotions) :

| Date | Composants | Fournisseur | Coût Réel |
| :--- | :--- | :--- | :--- |
| **Fév. 2026** | Lot Électronique (2x ESP32, LM2596, 2x LR7843, Relais 5v, CapteurCapacitif, Flotteur, BME280)<br>*Équivalent Amazon : ~ 59,45 €* | AliExpress | **13,69 €** |
| **Déjà Acquis** | Carte d'Extension 38 pins, Capteur BH1750, Sonde étanche DS18B20 | N/A | **0,00 €** |
| *À venir* | *Écran Tactile 4.3" Waveshare* | *Amazon* | *-* |
| *À venir* | *Potager de base (Option : Yoocaa 12 Capsules)* | *Amazon* | *-* |
| **TOTAL ACTUEL** | | | **13,69 €** |
