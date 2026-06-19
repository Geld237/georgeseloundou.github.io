# Site personnel — Georges Ngnouwal Eloundou

Site académique bilingue (FR/EN) construit avec [Quarto](https://quarto.org), déployé automatiquement sur GitHub Pages.

## Structure du projet

```
.
├── _quarto.yml              # Configuration globale
├── index.qmd                # Accueil (FR)
├── research.qmd             # Recherche (FR)
├── teaching.qmd             # Enseignement (FR)
├── talks.qmd                # Communications (FR)
├── cv.qmd                   # CV (FR)
├── en/                      # Version anglaise
│   ├── index.qmd
│   ├── research.qmd
│   ├── teaching.qmd
│   ├── talks.qmd
│   └── cv.qmd
├── styles.css               # CSS personnalisé
├── assets/
│   ├── profile.jpg          ← À AJOUTER (placeholder SVG en attendant)
│   ├── cv-eloundou-fr.pdf   ← À AJOUTER (CV français)
│   ├── cv-eloundou-en.pdf   ← À AJOUTER (CV anglais)
│   ├── lang-switcher.html   # Script de bascule de langue (ne pas modifier)
│   └── profile.jpg.svg      # Placeholder de la photo
├── .github/workflows/
│   └── publish.yml          # Déploiement automatique
└── README.md
```

## Comment fonctionne le bilingue

- **URL** : `/` pour la version française (par défaut), `/en/...` pour l'anglais.
- **Bouton FR | EN** dans la navbar : bascule entre les deux versions de la **même page** (si tu es sur `research.html` en FR et tu cliques EN, tu arrives sur `en/research.html`).
- **Labels de navbar** traduits automatiquement par JavaScript selon la langue de la page.
- **CV** : la page CV (FR ou EN) propose les deux PDFs au téléchargement — le bouton principal correspond à la langue de la page.

---

## Mise en route (10 minutes)

### 1. Prérequis

- **[Quarto](https://quarto.org/docs/get-started/)** (gratuit, < 5 min à installer)
- **[Git](https://git-scm.com/)**
- **Un compte [GitHub](https://github.com)**

### 2. Personnaliser le contenu

a. **Place ta photo** : `assets/profile.jpg` (carrée, 600×600 px minimum, fond uni de préférence).
   Puis dans `index.qmd` ET `en/index.qmd`, remplace `profile.jpg.svg` par `profile.jpg`.

b. **Place les deux CV PDF** :
   - `assets/cv-eloundou-fr.pdf` (compile depuis ton fichier `.qmd` existant)
   - `assets/cv-eloundou-en.pdf` (à traduire)

c. **Mets à jour la section *Actualités*** (`index.qmd` et `en/index.qmd`) selon les besoins.

### 3. Prévisualiser en local

```bash
cd georges-eloundou-site
quarto preview
```

Le site s'ouvre automatiquement (par défaut sur `http://localhost:4444`) avec rechargement à chaque modification.

### 4. Publier sur GitHub Pages

**a. Créer le dépôt GitHub.** Pour une URL propre type `https://georgeseloundou.github.io`, le nom du dépôt doit être exactement `georgeseloundou.github.io` (= ton username GitHub + `.github.io`).

**b. Pousser le code :**

```bash
cd georges-eloundou-site
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<ton-username>/<nom-du-repo>.git
git push -u origin main
```

**c. Activer GitHub Pages :**

1. Va dans **Settings → Pages** du dépôt.
2. Sous **Build and deployment → Source**, choisis **GitHub Actions**.
3. Le workflow `.github/workflows/publish.yml` va compiler le site et le publier (1–2 min).

**d. Pour chaque mise à jour future :**

```bash
git add .
git commit -m "Mise à jour"
git push
```

Le site se redéploie automatiquement à chaque `push` sur `main`.

---

## Ajouter une page bilingue

Pour chaque nouveau contenu : crée le fichier en français (`mapage.qmd`) à la racine, et son équivalent anglais (`en/mapage.qmd`). Ajoute le lien dans `_quarto.yml` sous `navbar > left`. Le sélecteur FR/EN gérera automatiquement la bascule.

## Personnalisations courantes

### Changer la couleur d'accentuation

Dans `styles.css`, modifie la variable `--ge-accent` (actuellement un vert académique `#1e4d3a`). Alternatives sobres :

- Bleu marine : `#1e3a5f`
- Bordeaux : `#7a1e3a`
- Anthracite : `#2c3e50`

### Modifier la navigation

Édite la section `navbar:` dans `_quarto.yml`. Si tu ajoutes un nouveau lien, pense à l'ajouter aussi dans le tableau `labelMap` de `assets/lang-switcher.html` pour la traduction automatique.

### Désactiver une langue temporairement

Pour cacher le bouton EN : commente la ligne `- text: "EN"` dans `_quarto.yml`.

---

## Dépannage rapide

- **`quarto preview` ne fonctionne pas** → vérifie l'installation : `quarto --version` doit renvoyer ≥ 1.4.
- **GitHub Pages affiche une page blanche** → onglet **Actions**, vérifie que le workflow a réussi (✅). Sinon, lis les logs.
- **L'URL retourne 404** → vérifie que dans **Settings → Pages**, la source est bien **GitHub Actions** (pas "Deploy from a branch").
- **Le bouton FR/EN ne marche pas** → ouvre la console du navigateur (F12), regarde s'il y a une erreur JS. Vérifie que `assets/lang-switcher.html` est bien présent.
- **Les labels de navbar ne se traduisent pas en anglais** → tu as probablement renommé un item dans `_quarto.yml` sans mettre à jour `labelMap` dans `assets/lang-switcher.html`.

---

## Ressources

- [Documentation Quarto Websites](https://quarto.org/docs/websites/)
- [Galerie de sites Quarto académiques](https://quarto.org/docs/gallery/#websites)
