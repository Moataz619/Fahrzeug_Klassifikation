# 🚗 Fahrzeug-Klassifikation (Silhouette-Analyse)

Ein end-to-end Machine-Learning-Projekt zur automatisierten Klassifikation von Fahrzeugsilhouetten in die Kategorien **Car**, **Bus** und **Van** basierend auf geometrischen und statistischen Bildmerkmalen.

---

## 📌 Projektübersicht

Die automatisierte Erkennung und Kategorisierung von Fahrzeugtypen spielt eine zentrale Rolle in modernen Transportsystemen, Mauterfassung und autonomen Fahrsystemen. In diesem Projekt analysieren und klassifizieren wir silhouettesbasierte Messwerte von Fahrzeugen mithilfe verschiedener Machine-Learning-Algorithmen.

### 🎯 Hauptziele
* **Data Cleaning & Imputation:** Behandlung fehlender Messwerte mittels Median-Imputation.
* **Explorative Datenanalyse (EDA):** Identifikation von Korrelationen, Ausreißern und Merkmalsverteilungen.
* **Modellierung & Vergleich:** Evaluation von Logistic Regression, Decision Tree, Random Forest und Support Vector Machine (SVM).
* **Preprocessing:** Z-Standardisierung und stratifizierter Train-Test-Split.

---

## 📁 Projektstruktur

```text
Fahrzeug_Klassifikation/
│
├── data/
│   ├── raw/                    # Ursprünglicher Datensatz (vehicle.csv)
│   └── processed/              # Bereinigte Daten (vehicle_clean.csv)
│
├── notebooks/
│   └── code.ipynb              # Haupt-Jupyter-Notebook mit der Analyse
│
├── reports/
│   ├── figures/                # Gespeicherte Diagramme (Confusion Matrix, Plots)
│   └── final_report.md         # Ausführlicher wissenschaftlicher Projektbericht
│
├── .gitignore                  # Git-Ignore Konfiguration
├── README.md                   # Projekt-Dokumentation
