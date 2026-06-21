# 🚨 Système de détection d'obstacle par ultrasons avec alarme sonore et visuelle

[![Arduino](https://img.shields.io/badge/Arduino-Uno-00979D?style=flat-square&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![Language](https://img.shields.io/badge/Language-C%2B%2B-blue?style=flat-square&logo=cplusplus)](https://github.com/SERGIO-OLIVIER-wink/ARDUINO-HC-SR04-ALARM)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()
[![Platform](https://img.shields.io/badge/Platform-Embedded%20Systems-orange?style=flat-square)]()

Système embarqué de détection d'obstacles en temps réel basé sur **Arduino Uno** et capteur ultrason **HC-SR04**, inspiré du principe des systèmes d'aide au stationnement automobile. Le système mesure en continu la distance à un objet et déclenche une alarme visuelle (LED rouge) et sonore (buzzer) lorsqu'un obstacle est détecté à moins de 20 cm.

> Projet réalisé dans le cadre de mon apprentissage autodidacte en électronique embarquée et systèmes microcontrôleurs — L2 Physique et Applications, Université d'Antananarivo.

---

## 📸 Aperçu

| Photo 1 | Photo 2 | Photo 3 |
|---|---|---|
| ![Montage 1](photo1.jpg) | ![Montage 2](photo2.jpg) | ![Montage 3](photo3.jpg) |

🎥 [Voir la démonstration vidéo](video.mp4)

---

## ⚙️ Fonctionnement

Le capteur **HC-SR04** émet une impulsion ultrasonique et mesure le temps de retour de l'écho pour calculer la distance, selon le principe du sonar :
**Logique du système :**

1. Le microcontrôleur déclenche une impulsion de 10 µs sur la broche `TRIG`.
2. Le capteur émet une salve ultrasonique à 40 kHz.
3. La broche `ECHO` passe à l'état haut pendant la durée de l'aller-retour de l'onde.
4. La durée mesurée par `pulseIn()` permet de calculer la distance.
5. Si la distance mesurée est **inférieure à 20 cm**, la LED s'allume et le buzzer s'active.
6. Sinon, le système reste au repos.
7. La distance est affichée en continu sur le port série (utile pour le débogage et le suivi en temps réel).

---

## 🔌 Schéma de câblage

| Composant | Broche du composant | Broche Arduino Uno |
|---|---|---|
| HC-SR04 | VCC | 5V |
| HC-SR04 | GND | GND |
| HC-SR04 | TRIG | D9 |
| HC-SR04 | ECHO | D10 |
| LED | Anode (+) | D11 |
| LED | Cathode (−) | GND (via résistance 220 Ω) |
| Buzzer | (+) | D13 |
| Buzzer | (−) | GND |

> ⚠️ Une résistance de protection (220 Ω – 330 Ω) est recommandée en série avec la LED pour limiter le courant.

---

## 🧰 Matériel requis

- 1 × Arduino Uno (ou compatible)
- 1 × Capteur ultrason HC-SR04
- 1 × LED (couleur libre)
- 1 × Buzzer actif 5V
- 1 × Résistance 220 Ω – 330 Ω
- Câbles de connexion (jumper wires)
- 1 × Breadboard

---

## 💻 Code source

Le programme complet se trouve dans [`ultrasonic_alarm.ino`](ultrasonic_alarm.ino).

**Extrait — configuration des broches :**

```cpp
#define TRIG    9
#define ECHO    10
#define BUZZER  13
#define LED     11
```

**Extrait — logique de déclenchement de l'alarme :**

```cpp
if (distance < 20) {
  digitalWrite(LED, HIGH);
  digitalWrite(BUZZER, HIGH);
} else {
  digitalWrite(LED, LOW);
  digitalWrite(BUZZER, LOW);
}
```

Un timeout de 30 ms est appliqué à `pulseIn()` afin d'éviter un blocage du programme en cas d'absence d'écho (objet hors de portée).

---

## 🚀 Installation et utilisation

1. **Câbler le circuit** selon le schéma ci-dessus.
2. **Cloner le dépôt :**
```bash
   git clone https://github.com/SERGIO-OLIVIER-wink/ARDUINO-HC-SR04-ALARM.git
```
3. **Ouvrir** `ultrasonic_alarm.ino` dans l'IDE Arduino.
4. **Sélectionner** la carte (Arduino Uno) et le port série correspondant.
5. **Téléverser** le programme sur la carte.
6. **Ouvrir le moniteur série** (9600 bauds) pour visualiser les mesures de distance en temps réel.

---

## 📁 Structure du dépôt
---

## 🔭 Améliorations possibles

Le système actuel utilise une logique binaire (alarme déclenchée / non déclenchée). Plusieurs pistes d'évolution ont été identifiées pour aller plus loin :

- [ ] **Détection par paliers** : ajouter deux LED supplémentaires (verte et jaune) pour signaler progressivement la proximité — vert (> 30 cm), jaune (10–30 cm), rouge + buzzer (< 10 cm)
- [ ] Affichage permanent de la distance sur un écran LCD 16×2 (sans dépendre du moniteur série)
- [ ] Réglage du seuil de détection via un potentiomètre
- [ ] Ajout d'un servo-moteur pour faire pivoter le capteur (balayage angulaire)
- [ ] Journalisation des détections avec horodatage

---

## 👤 Auteur

**Sergio Olivier Rakotondravao**
Étudiant en L2 Physique et Applications — Université d'Antananarivo, Madagascar
[GitHub](https://github.com/SERGIO-OLIVIER-wink)

---

## 📄 Licence

Ce projet est distribué sous licence [MIT](LICENSE).
