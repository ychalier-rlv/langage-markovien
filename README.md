# Modèles de langage d'après des chaînes de Markov

Interface web permettant l'exploration de [chaînes de Markov](https://fr.wikipedia.org/wiki/Cha%C3%AEne_de_Markov) pour la [génération de texte](https://fr.wikipedia.org/wiki/Mod%C3%A8le_de_langage). Les modèles donnent les mots apparaissant le plus fréquemment après un mot donné. Les modèles sont au format JSON, selon le schéma décrit ci-dessous. Plusieurs sont donnés en exemple, tirés du [premier tome de la saga Harry Potter](https://fr.wikipedia.org/wiki/Harry_Potter_%C3%A0_l%27%C3%A9cole_des_sorciers) en français, avec différents paramètres (longueur des N-grammes considérés, niveau d'élagage).

Accessible sur [https://ychalier-rlv.github.io/langage-markovien/](https://ychalier-rlv.github.io/langage-markovien/). Une démonstration de la génération de texte à partir d'une [grammaire formelle](https://fr.wikipedia.org/wiki/Grammaire_formelle) est également disponible sur [https://ychalier-rlv.github.io/langage-markovien/gabarit.html](https://ychalier-rlv.github.io/langage-markovien/gabarit.html).

## Schéma du modèle

Les modèles sont enregistrés au format JSON et encodés en UTF-8. Voici un exemple, à partir des phrase `il fait beau` et `il pleut`.

```json
{
    "tokens": ["il", "fait", "beau", "pleut"],
    "chain": {
        "il": {
            "score": 2,
            "children": {
                "fait": {
                    "score": 0.5,
                    "children": {
                        "beau" : {
                            "score": 1,
                            "children": {}
                        }
                    }
                },
                "pleut": {
                    "score": 0.5,
                    "children": {}
                }
            }
        }
    }
}
```

Le champ `tokens` contient la liste des différents tokens, sans répétition. Le champ `chain` possède une structure récursive. À chaque niveau, la clé est un token, et la valeur associée un nœud avec le `score` (le score de la chaîne de Markov, normalisé pour que la somme fasse 1 sur tous les enfants du nœud, sauf à la racine), et les `children`, qui sont tous les mots suivant le mot actuel, en reprenant la structure de `chain`.