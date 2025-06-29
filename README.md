# Classificació Automàtica de Sentiment en Crítiques de Pel·lícules

Aquest projecte implementa diversos enfocaments per determinar si una crítica de pel·lícula expressa una opinió positiva o negativa. S'hi integren tècniques d’aprenentatge supervisat i no supervisat, amb una anàlisi detallada de la precisió i dels errors dels models.

## Objectius

- Preparar i netejar un corpus de ressenyes de pel·lícules (Movie Reviews).
- Comparar models supervisats (Naive Bayes, Random Forest, Regressió Logística, SVM).
- Implementar un enfocament no supervisat amb SentiWordNet i Lesk.
- Analitzar el rendiment i les limitacions de cada aproximació.

## Conjunt de Dades

S’ha utilitzat el corpus **Movie Reviews** de NLTK, format per 2000 ressenyes (50% positives i 50% negatives).

### Preprocessament aplicat:

- Tokenització i POS tagging.
- Lematització amb WordNetLemmatizer.
- Eliminació de dígits, signes de puntuació i stopwords.
- Vectorització del text amb **CountVectorizer** (unigrams i bigrams, `max_features=2000`, `min_df=10`, `binary=True`).

## Models Supervisats

Es van entrenar quatre models:

- **Multinomial Naive Bayes**  
- **Random Forest**  
- **Regressió Logística** (millor resultat global)  
- **SVM**  

La regressió logística, amb un paràmetre `C=0.01`, va obtenir una *accuracy* del **86.5%** i un AUC de **0.95**.

Tots els models es van validar amb **GridSearchCV** i validació creuada (10 folds).

## Enfocament No Supervisat

Es va implementar un classificador basat en:

- **Lesk** per a desambiguació semàntica.
- **SentiWordNet** per obtenir la polaritat de cada paraula.

Es van provar diferents configuracions de ponderació per adjectius, verbs, noms i adverbis. La millor versió va assolir una *accuracy* del **62.5%**, destacant pel seu alt *recall* en la classe positiva.

## Comparació de Models

| Model                    | Accuracy Test | AUC   |
|--------------------------|---------------|-------|
| Regressió Logística      | 86.5%         | 0.95  |
| SVM                      | lleugerament inferior |
| Multinomial Naive Bayes  | lleugerament inferior |
| Random Forest            | menor rendiment, tendència a sobreajustament |
| Model no supervisat      | 62.5%         | 0.62  |

Els models supervisats han demostrat una capacitat superior per capturar patrons específics del conjunt d’entrenament, mentre que l’enfocament no supervisat ha funcionat raonablement bé sense dades etiquetades.

## Anàlisi dels Errors

Es van analitzar les prediccions incorrectes per identificar:

- Llenguatge ambigu, irònic o neutre.
- Construccions llargues i complexes.
- Diferències de comportament entre models supervisats i no supervisats.

Aquesta anàlisi ha permès evidenciar les limitacions de cada enfocament i identificar possibles millores, com la integració d’informació contextual.

## Conclusions

- La regressió logística va ser el model més fiable i estable.
- El model no supervisat pot ser útil quan no es disposa d’exemples etiquetats, tot i la seva menor precisió.
- L’estudi ha posat de manifest la importància del preprocessament i de l’ajust dels hiperparàmetres.
- Es planteja com a línia futura la combinació d’ambdós enfocaments per millorar la robustesa del sistema.

## Llibreries i Eines

- Python
- NLTK
- scikit-learn
- SentiWordNet
- NumPy
- pandas

## Llicència

Aquest projecte s’ha desenvolupat amb finalitats acadèmiques. L’ús en entorns productius requereix una revisió addicional i proves de robustesa.
