# 📄 Projektbericht: Fahrzeug-Klassifikation basierend auf Silhouetten-Merkmalen

**Autor:** Moataz  
**Datum:** September 2026  
**Repository:** Fahrzeug_Klassifikation

---

## 1. Einleitung & Problemstellung
Die automatische Erkennung und Kategorisierung von Fahrzeugtypen ist eine Kernkomponente moderner intelligenter Transportsysteme (ITS) und Mauterfassungssysteme. Ziel dieses Projekts ist die Entwicklung eines Machine-Learning-Modells zur präzisen Klassifikation von Fahrzeugsilhouetten in die Kategorien **Car**, **Bus** und **Van**.

---

## 2. Datenbasis & Explorative Datenanalyse (EDA)

### 2.1 Datensatz-Charakteristika
* **Gesamtumfang:** 846 Zeilen und 19 Spalten.
* **Features:** 18 numerische Messwerte (z. B. `compactness`, `circularity`, `radius_ratio`, `scatter_ratio`, `elongatedness`).
* **Zielvariable (`class`):** Ursprünglich 5 Ausprägungen (`saab900`, `opel`, `bus`, `van`, `car`).

### 2.2 Data Cleaning & Target Mapping
* **Zielvariablen-Konsolidierung:** Die spezifischen Pkw-Modelle `saab900` und `opel` wurden mit der Kategorie `car` zusammengefasst.
* **Exakte Klassenverteilung:**
  * `car`: 429 Fahrzeuge (50,7 %)
  * `bus`: 218 Fahrzeuge (25,8 %)
  * `van`: 199 Fahrzeuge (23,5 %)

### 2.3 Imputation fehlender Werte
Insgesamt wurden 36 fehlende Werte über 14 Merkmale hinweg identifiziert (u. a. `radius_ratio`: 6, `circularity`: 5, `distance_circularity`: 4). Diese wurden mittels **Median-Imputation** (`SimpleImputer(strategy='median')`) auf Basis des Training-Sets aufgefüllt.

---

## 3. Preprocessing & Skalierung

1. **Train-Test-Split:** Stratifizierter Split im Verhältnis 80:20 (Train: 676 Instanzen, Test: 170 Instanzen).
2. **Feature-Skalierung:** Alle 18 Merkmale wurden mittels `StandardScaler` z-standardisiert ($\mu = 0, \sigma = 1$).

---

## 4. Modellierung & Exakte Ergebnisse

Die Modelle wurden auf den skalierten Trainingsdaten trainiert und auf den 170 ungesehenen Testdaten evaluiert:

| Modell | Accuracy (Test) | F1-Score (Macro) | Leistungsbeurteilung |
| :--- | :---: | :---: | :--- |
| **Decision Tree** | 87,65 % | 0.8732 | Leicht überangepasst ohne Hyperparameter-Tuning |
| **Logistic Regression** | 93,53 % | 0.9342 | Sehr starke lineare Trennbarkeit nach Skalierung |
| **Random Forest** | 95,88 % | 0.9587 | Hervorragendes Ensemble-Ergebnis |
| **SVM (RBF Kernel)** | **97,06 %** | **0.9701** | **Top-Performer mit minimaler Fehlerrate** |

---

## 5. Detaillierte Evaluation des Siegermodells (SVM)

Das SVM-Modell erzielte eine Test-Genauigkeit von **97,06 %** (165 von 170 Testbeispielen korrekt klassifiziert).

### 5.1 Classification Report (SVM)
* **Bus:** Precision = 97,78 %, Recall = 100,00 %, F1-Score = 0.9888 (44/44 korrekt)
* **Car:** Precision = 98,80 %, Recall = 95,35 %, F1-Score = 0.9704 (82/86 korrekt)
* **Van:** Precision = 92,86 %, Recall = 97,50 %, F1-Score = 0.9512 (39/40 korrekt)

### 5.2 Confusion Matrix (SVM)
* **Tatsächlich Car (86):** 82 als `car`, 1 als `bus`, 3 als `van` klassifiziert.
* **Tatsächlich Bus (44):** 44 als `bus` klassifiziert (100 % Trefferquote).
* **Tatsächlich Van (40):** 39 als `van`, 1 als `car` klassifiziert.

---

## 6. Fazit & Ausblick

Das Support Vector Machine (SVM) Modell erwies sich für diesen 18-dimensionalen, kontinuierlichen Merkmalsraum als die optimale Wahl. Die z-Standardisierung spielte hierbei eine entscheidende Rolle für die Performance der SVM. Bussen wurden fehlerfrei erkannt, während minimale Überschneidungen nur zwischen Vans und Pkws auftraten.
