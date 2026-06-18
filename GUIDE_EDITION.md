# Guide d'édition — ajouter ou retirer une ressource

Ce site lit le fichier **`resources.json`** à chaque chargement de page.
Pour ajouter, modifier ou retirer une ressource, il suffit de modifier ce fichier
directement sur GitHub (bouton crayon ✏️ en haut à droite du fichier sur github.com),
puis de valider ("Commit changes"). Pas besoin de toucher au fichier `index.html`.

⚠️ Le JSON est strict sur la syntaxe : une virgule oubliée ou en trop casse tout le site.
Suivez les exemples ci-dessous au pied de la lettre. En cas de doute, utilisez un
validateur en ligne (ex. jsonlint.com) avant de valider sur GitHub.

---

## 1. Ajouter une ressource dans un bloc (contenus pédagogiques ou capsules)

Repérez le bloc concerné (ex. `"id": "aes-bloc-2"`), puis la catégorie
(`contenus_pedagogiques` ou `capsules_pedagogiques`), puis son tableau `"ressources": [ ]`.

Ajoutez un objet de ce type **à l'intérieur des crochets** :

```json
{
  "titre": "Les transmissions en équipe pluriprofessionnelle",
  "type": "lien",
  "url": "https://moncompte.github.io/transmissions-bloc2/",
  "note": "Capsule interactive avec quiz de révision"
}
```

### Champs disponibles

| Champ   | Obligatoire | Valeurs possibles                          | Exemple |
|---------|-------------|---------------------------------------------|---------|
| `titre` | oui         | texte libre                                  | `"Les transmissions en équipe"` |
| `type`  | oui         | `"lien"` (site web) · `"pdf"` · `"doc"` · `"video"` | `"pdf"` |
| `url`   | oui         | adresse complète, commence par `https://`   | `"https://moncompte.github.io/site/fichier.pdf"` |
| `note`  | non         | texte libre, courte description affichée sous le titre | `"Mis à jour en mai 2026"` |

➡️ Si vous n'avez pas de note à ajouter, supprimez simplement la ligne `"note": "..."`
(et la virgule juste avant si c'est la dernière ligne de l'objet).

### S'il y a déjà des ressources dans la liste

Pensez à la **virgule** entre chaque objet :

```json
"ressources": [
  {
    "titre": "Ressource déjà existante",
    "type": "lien",
    "url": "https://exemple.github.io/site-existant/"
  },
  {
    "titre": "Nouvelle ressource ajoutée",
    "type": "pdf",
    "url": "https://exemple.github.io/docs/nouveau.pdf",
    "note": "Support de cours"
  }
]
```

---

## 2. Ajouter une ressource dans l'épreuve certificative

C'est la même chose, mais il y a un niveau en plus : les **sous-groupes**
(Méthodologie écrite / Méthodologie orale / Fiche de notation orale).
Trouvez le bon sous-groupe par son `"nom"`, puis ajoutez dans son `"ressources": [ ]`
exactement comme au point 1.

```json
"sous_groupes": [
  {
    "nom": "Méthodologie écrite",
    "ressources": [
      {
        "titre": "Méthodologie de l'écrit Bloc 1",
        "type": "pdf",
        "url": "https://exemple.github.io/docs/methodo-ecrit-bloc1.pdf"
      }
    ]
  },
  ...
]
```

---

## 3. Ajouter une ressource dans "Contenus transversaux"

Tout en bas du fichier, dans `"contenus_transversaux"`, même principe, directement
dans `"ressources": [ ]` :

```json
"contenus_transversaux": {
  ...
  "ressources": [
    {
      "titre": "Charte des droits de la personne accompagnée",
      "type": "pdf",
      "url": "https://exemple.github.io/docs/charte.pdf"
    }
  ]
}
```

---

## 4. Retirer une ressource

Supprimez tout le bloc `{ ... }` correspondant à la ressource, **y compris la
virgule qui le sépare des objets voisins**. Si c'était le seul élément du tableau,
remettez simplement `"ressources": []`.

---

## 5. Ajouter ou retirer un bloc / une filière entière

C'est plus rare, mais possible : un bloc est un objet avec `id`, `numero`,
`intitule` et `categories`. Le plus sûr est de copier un bloc existant en entier
(par exemple `aes-bloc-5`), de le coller juste après, puis de changer son `id`,
son `numero` et son `intitule`. Pensez à vider les `ressources` du bloc copié si
elles ne s'appliquent pas au nouveau bloc.

---

## Erreurs fréquentes

- **Oubli d'une virgule** entre deux objets `{ }` d'un même tableau → le site ne s'affiche plus du tout.
- **Virgule en trop** après le dernier élément d'un tableau ou d'un objet → même problème.
- **Guillemets droits uniquement** : `"texte"`, jamais `“texte”` (guillemets "intelligents" de Word).
- **URL incomplète** : toujours commencer par `https://`.

En cas de doute, copiez tout le contenu du fichier dans [jsonlint.com](https://jsonlint.com)
avant de valider — il vous dira immédiatement où est l'erreur.
