# 📘 Template LaTeX : Rapport d'Ingénierie Moderne (Base IEEE)

TEST SEB - Ce projet est un template LaTeX modulaire, professionnel et moderne, spécialement conçu pour les rapports d'ingénierie, de recherche ou de fin d'études. Il utilise la rigueur de la structure IEEE (double colonne) tout en y ajoutant une esthétique moderne (page de garde, couleurs, sommaire simple colonne).

---

## 📂 1. Architecture du Projet (Recommandée)

Pour garder un projet lisible, organisez vos fichiers ainsi :

* `main.tex` : Le chef d'orchestre. Il charge les packages, la page de garde, et appelle les autres fichiers.
* `sections/` : Dossier contenant vos parties (ex: `01_intro.tex`, `02_methodo.tex`).
* `images/` : Dossier où placer toutes vos images, schémas et logos (PNG, JPG, PDF).
* `biblio.bib` : Votre base de données bibliographique (pour les références).
* `README.md` : Ce mode d'emploi.

---

## 🚀 2. Comment Compiler le Rapport (Mac/Terminal)

Pour transformer le code en fichier PDF, ouvrez votre terminal, naviguez dans le dossier du projet, et tapez :

```bash
pdflatex main.tex
```

**⚠️ Règle d'or du Sommaire :**
Si vous ajoutez de nouvelles sections (`\section{}`), de nouvelles images ou de nouveaux tableaux, LaTeX a besoin de lire le fichier deux fois pour calculer les numéros de page. Vous devez donc taper la commande deux fois de suite :

```bash
pdflatex main.tex
pdflatex main.tex
```

*(Si vous avez une erreur de package manquant, rappelez-vous la commande magique : `sudo tlmgr install nom_du_package`)*

---

## 🧩 3. Modularité : Travailler avec des fichiers séparés

Ne rédigez pas tout dans `main.tex` ! Créez des fichiers dans le dossier `sections/` (par exemple `sections/01_introduction.tex`) et insérez-les dans `main.tex` (après le sommaire) avec cette commande :

```latex
\input{sections/01_introduction.tex}
```

Cela permet de réorganiser le rapport facilement et de travailler à plusieurs sans conflits.

---

## 🛠️ 4. Boîte à Outils : Ajouter des Blocs (Cheat Sheet)

Voici les codes à copier-coller pour insérer n'importe quel élément dans votre rapport.

### ✍️ A. Titres et Structure

```latex
\section{Titre Principal}
\subsection{Sous-titre}
\subsubsection{Sous-sous-titre}
```

### 📏 B. Nombres et Unités (Package `siunitx`)

En ingénierie, n'écrivez jamais `10 kg` à la main. Utilisez `\SI{}{}` pour respecter les normes ISO.

```latex
Une force de \SI{50}{\newton} 
Une vitesse de \SI{130}{\kilo\meter\per\hour}
Une fréquence de \SI{50}{\hertz}
```

### 🧮 C. Équations Mathématiques

Pour une équation numérotée et centrée :

```latex
\begin{equation} \label{eq:loi_ohm}
    U = R \times I
\end{equation}
Comme le montre l'équation \ref{eq:loi_ohm}...
```

### 🖼️ D. Insérer une Image

Placez d'abord votre image (ex: `schema.png`) dans le dossier `images/`.

```latex
\begin{figure}[h]
    \centering
    \includegraphics[width=0.8\linewidth]{schema.png}
    \caption{Description claire de l'image}
    \label{fig:mon_schema}
\end{figure}
```

*Astuce : Le `[h]` demande à LaTeX de placer l'image "Here" (Ici).*

### 📊 E. Tableau Moderne (Package `booktabs`)

Fini les vieux tableaux quadrillés. Utilisez `\toprule`, `\midrule` et `\bottomrule`.

```latex
\begin{table}[h]
    \centering
    \caption{Titre du tableau}
    \label{tab:mesures}
    \begin{tabular}{lcc} % l=gauche, c=centre, r=droite
        \toprule
        \textbf{Paramètre} & \textbf{Test 1} & \textbf{Test 2} \\
        \midrule
        Température        & \SI{20}{\celsius} & \SI{25}{\celsius} \\
        Pression           & \SI{1}{\bar}      & \SI{1.2}{\bar} \\
        \bottomrule
    \end{tabular}
\end{table}
```

### 💻 F. Insérer du Code Source (Package `listings`)

```latex
\begin{lstlisting}[language=Python, caption=Calcul de la moyenne]
def calculer_moyenne(liste):
    somme = sum(liste)
    return somme / len(liste)
\end{lstlisting}
```

---

## 🎨 5. Personnalisation des Couleurs

Les couleurs du rapport sont définies tout en haut de `main.tex`. Vous pouvez modifier les valeurs RGB pour correspondre à la charte graphique de votre école ou de votre entreprise :

```latex
\definecolor{ModernBlue}{RGB}{0, 82, 155} 
\definecolor{AccentColor}{RGB}{220, 53, 69}
```

---

## 📚 6. Bibliographie

1. Créez un fichier `biblio.bib` et mettez-y vos références au format BibTeX.
2. À la toute fin de `main.tex` (juste avant `\end{document}`), décommentez ou ajoutez ces lignes :

```latex
\bibliographystyle{IEEEtran}
\bibliography{biblio}
```

3. Dans le texte, citez une source avec `\cite{cle_de_la_source}`.