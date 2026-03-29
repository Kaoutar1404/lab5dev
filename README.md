# 📱 Convertisseur — Application Android (Lab 5)

> Application mobile de conversion de températures et de distances, développée avec Java et Android Studio dans le cadre du Lab 5.

---

## 🎯 Ce que fait l'application

L'application propose **deux onglets glissables** :

- 🌡 **Température** — convertir entre °C et °F dans les deux sens
- 📍 **Distance** — convertir entre kilomètres et miles dans les deux sens

En plus des conversions, l'application demande confirmation avant de se fermer, que ce soit via le menu ou le bouton Retour.

---

## 🎬 Vidéo de démonstration

https://github.com/user-attachments/assets/lab5dev.mp4

---

## ✨ Design de l'interface

Le choix graphique repose sur une **palette rose/fuchsia** avec des **cartes arrondies** pour chaque section. Chaque onglet est divisé en trois zones :

```
┌─────────────────────────────┐
│   🌡  En-tête coloré        │  ← CardView rose avec icône + titre
├─────────────────────────────┤
│   ○ °C → °F   ○ °F → °C   │  ← RadioGroup horizontal
│   [ Entrez la valeur      ] │  ← TextInputLayout style OutlinedBox
│   [      Convertir        ] │  ← MaterialButton pleine largeur
├─────────────────────────────┤
│         Résultat            │  ← CardView rose clair
│          77.00 °F           │
└─────────────────────────────┘
```

---

## 🗂 Fichiers du projet

```
java/
├── MainActivity.java          → gère les onglets, le menu et le bouton Retour
├── FragmentPagerAdapter.java  → relie ViewPager2 aux deux fragments
├── TemperatureFragment.java   → logique de conversion température
└── DistanceFragment.java      → logique de conversion distance

res/layout/
├── activity_main.xml          → TabLayout + ViewPager2
├── fragment_temperature.xml   → interface onglet Température (cartes roses)
└── fragment_distance.xml      → interface onglet Distance (cartes fuchsia)

res/values/
├── colors.xml                 → palette rose personnalisée
├── strings.xml                → nom de l'app "Convertisseur"
└── themes.xml                 → thème MaterialComponents rose
```

---

## 🔢 Formules appliquées

```
°C vers °F  :  résultat = (valeur × 9 ÷ 5) + 32
°F vers °C  :  résultat = (valeur − 32) × 5 ÷ 9

KM vers Miles  :  résultat = valeur × 0.621371
Miles vers KM  :  résultat = valeur ÷ 0.621371
```

### Exemples de tests

| Saisie | Mode | Résultat attendu |
|--------|------|-----------------|
| 25 | °C → °F | **77.00 °F** |
| 77 | °F → °C | **25.00 °C** |
| 10 | KM → Miles | **6.21 miles** |
| 6.21 | Miles → KM | **10.00 km** |

---

## 🔙 Gestion du bouton Retour

Chaque appui sur **Retour** ou sélection de **Quitter** dans le menu déclenche cette boîte de dialogue :

```
┌──────────────────────────┐
│         Quitter          │
│  Voulez-vous vraiment    │
│       quitter ?          │
│                          │
│  [ Non ]      [ Oui ]   │
└──────────────────────────┘
```

---

## ⚙️ Configuration technique

```gradle
minSdk          : 24
targetSdk       : 34
Langage         : Java 1.8
Theme           : MaterialComponents.Light.DarkActionBar
Dépendances clés :
  - material:1.11.0
  - fragment:1.6.2
  - viewpager2:1.0.0
```

---

## 💡 Points retenus du laboratoire

- La navigation par onglets avec `ViewPager2` + `TabLayoutMediator` est plus flexible que les boutons manuels
- `TextInputLayout.OutlinedBox` donne un rendu plus soigné qu'un simple `EditText`
- `onBackPressed()` permet d'intercepter le retour système et d'afficher une confirmation
- Séparer chaque écran dans un fragment dédié rend le code plus lisible et maintenable
