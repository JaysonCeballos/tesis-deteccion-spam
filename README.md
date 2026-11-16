# Detección de spam con machine learning

**Proyecto de tesis · Ingeniería en Ciberseguridad · Universidad de las Ciencias Informáticas (UCI), 2026**

**Autores:** Jayson Ceballos Hernández y Alejandro Vázquez Marrero

Comparación de cinco enfoques de clasificación supervisada —Naive Bayes, SVM con kernel RBF, Random Forest, Soft Voting y Stacking— para la detección de spam en SMS, correo electrónico y comentarios, sobre cinco conjuntos de datos heterogéneos en inglés y turco, evaluados con F1-score mediante validación cruzada.

`Python` · `scikit-learn` · `pandas` · `machine learning` · `seguridad`

---

## Resultados

F1-score de la clase spam, media ± desviación típica entre particiones (`—` = no aplicable: el conjunto es numérico y Naive Bayes no se evaluó sobre él).

| Modelo | sms_spam | spambase | youtube_shakira | trspam | spam_ham_email |
|---|---:|---:|---:|---:|---:|
| Naive Bayes | 0,951 ± 0,013 | — | 0,904 ± 0,024 | 0,935 ± 0,010 | 0,972 ± 0,006 |
| SVM (RBF) | 0,945 ± 0,012 | 0,933 ± 0,005 | 0,916 ± 0,043 | 0,929 ± 0,021 | **0,986 ± 0,003** |
| Random Forest | 0,924 ± 0,021 | 0,951 ± 0,008 | 0,915 ± 0,028 | 0,894 ± 0,027 | 0,968 ± 0,006 |
| Soft Voting | 0,956 ± 0,014 | 0,947 ± 0,008 | 0,920 ± 0,031 | **0,942 ± 0,013** | 0,983 ± 0,004 |
| Stacking | **0,959 ± 0,003** | **0,954 ± 0,006** | **0,927 ± 0,028** | 0,934 ± 0,014 | 0,985 ± 0,003 |

**Hallazgos principales**

- **Stacking** obtuvo el mejor F1 medio (0,952) y ganó en tres de los cinco conjuntos.
- **SVM** fue el mejor en `spam_ham_email` (0,986) y **Soft Voting** en `trspam` (0,942): no hay un modelo que gane siempre.
- La dispersión **entre conjuntos** (de 0,894 a 0,986) es mayor que la **entre modelos** (medias entre 0,930 y 0,952). El corpus influye más que el algoritmo.
- Los corpus desbalanceados y cortos (`youtube_shakira`, 331 comentarios, 45 % de spam) concentran los peores resultados y la mayor varianza entre particiones.

## Conjuntos de datos

| Conjunto | Dominio | Idioma | Mensajes | % spam | Entrada | Origen |
|---|---|---|---:|---:|---|---|
| `sms_spam` | SMS | EN | 5.169 | 12,63 % | Texto crudo | UCI SMS Spam Collection |
| `spambase` | Correo | — | 4.601 | 39,40 % | Numérico (57 rasgos) | UCI Spambase |
| `youtube_shakira` | Comentarios | EN | 331 | 45,32 % | Texto crudo | Kaggle |
| `trspam` | Correo | TR | 634 | 35,17 % | Texto crudo | TurkishSpam (Kaggle) |
| `spam_ham_email` | Correo | EN | 4.993 | 29,28 % | Texto crudo | Kaggle |

En total, **15.728 mensajes**. Los cinco ficheros están en `data/` y proceden de repositorios públicos.

## Metodología

1. **Limpieza y normalización** de cada corpus, con tratamiento específico para el conjunto numérico (`spambase`).
2. **Vectorización del texto** en los cuatro corpus de texto; los detalles de configuración están en los notebooks.
3. **Validación cruzada**: cada celda de la tabla es la media ± desviación típica entre particiones, no un único resultado.
4. **Modelos comparados**: `MultinomialNB`, `SVC` con kernel RBF, `RandomForestClassifier`, `VotingClassifier` (soft) y `StackingClassifier`.
5. **Métrica principal**: F1-score de la **clase spam**, no la exactitud, porque los corpus están desbalanceados (del 12,6 % al 45,3 % de spam). Un modelo que ignore el spam puede exhibir una exactitud alta y ser inútil en producción.

## Estructura del repositorio

```
.
├── notebooks/
│   ├── 01_codigo_tesis.ipynb                  # pipeline completo
│   ├── anexos_tesis.ipynb                     # análisis descriptivo de los corpus
│   └── COMPARACIONES_GLOBALES_notebook.ipynb  # comparativas y figuras
├── data/                                      # los cinco conjuntos (públicos)
├── results/
│   ├── f1_modelo_dataset.csv                  # tabla de resultados en formato largo
│   └── datasets_resumen.csv                   # características de los corpus
├── requirements.txt
├── CITATION.cff
├── LICENSE
└── README.md
```

## Reproducir

```bash
git clone https://github.com/JaysonCeballos/tesis-deteccion-spam.git
cd tesis-deteccion-spam
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/
```

> **Nota sobre Google Colab.** Los notebooks se desarrollaron en Colab y leen y escriben en `/content/drive/MyDrive/spam_tesis`. Para ejecutarlos en local basta con cambiar esa ruta base por la carpeta del repositorio: los cinco conjuntos ya están incluidos en `data/` y las salidas se generan en `results/`.

## Autores

Trabajo de diploma realizado por los dos autores principales del proyecto, en la Facultad de Ciberseguridad de la Universidad de las Ciencias Informáticas (UCI).

**Jayson Ceballos Hernández** — Ingeniero en Ciberseguridad (UCI, 2026)

- LinkedIn: [linkedin.com/in/jayson-ceballos03](https://linkedin.com/in/jayson-ceballos03)
- Correo: jaysoncybersecurity@gmail.com

**Alejandro Vázquez Marrero** — Ingeniero en Ciberseguridad (UCI, 2026)

- LinkedIn: [linkedin.com/in/alejandro-vázquez-a75b1a432](https://www.linkedin.com/in/alejandro-v%C3%A1zquez-a75b1a432/)
- Correo: alejandrociberedit@gmail.com

## Cómo citar

```
Ceballos Hernández, J. y Vázquez Marrero, A. (2026). Detección de spam con machine learning:
comparación de modelos sobre cinco conjuntos de datos. Universidad de las Ciencias Informáticas (UCI).
https://github.com/JaysonCeballos/tesis-deteccion-spam
```

## Licencia

Código bajo licencia MIT (ver [LICENSE](LICENSE)). Cada conjunto de datos conserva la licencia de su origen.

---

## English summary

BSc thesis by **Jayson Ceballos Hernández** and **Alejandro Vázquez Marrero** comparing five supervised classifiers —Naive Bayes, SVM with RBF kernel, Random Forest, soft voting and stacking— for spam detection across five heterogeneous public datasets (SMS, email and comment corpora in English and Turkish). Every cell is a cross-validated F1 mean ± standard deviation on the spam class, chosen over accuracy because of class imbalance. Stacking gave the best average F1 (0.952); the spread across corpora (0.894–0.986) was larger than the spread across models, showing that the dataset matters more than the algorithm.
