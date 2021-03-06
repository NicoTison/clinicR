---
layout: lesson
root: ..
---



# Markdown et R Markdown pour des documents "dynamiques"

## Qu'est-ce qu'un  document "dynamique"?

Imaginons que vous avez besoin d'exporter vos résultats pour pouvoir les
intégrer dans un document que vous pourrez faire circuler  parmi vos
collaborateurs. Classiquement, vous allez copier vos tableaux à partir de votre
logiciel statistique pour ensuite les coller dans votre logiciel de traitement
de texte où vous ajouterez du contenu (vos notes, commentaires etc.). Même chose
pour vos figures, à moins que vous n'ayez pensé à les sauvegarder auparavant
dans un certain format (jpeg p.ex.). Et qu'arrivera-t-il si votre collaborateur
vous demande de corriger une petite erreur, de supprimer certaines observations
de votre base de données, d'ajouter une variable à votre modèle de régression?

Au lieu de découpler l'écriture du texte et les résultats de votre analyse, vaous
pourriez combiner l'écriture de votre contenu textuel et vos sorties
statistiques. Ce document "tout-en-un" est un document dynamique (permettant
aussi la
[recherche reproductible](http://aje.oxfordjournals.org/content/163/9/783)).

>  code + description =  rapport
>
>  langage informatique + langage de rédaction = rapport

Un tel document peut être créé avec R et RStudio grâce au package
[`knitr`](http://yihui.name/knitr). Le code `R` peut être combiné à différents
langages de rédaction tels que Markdown ou LaTeX.

## Qu'est-ce que Markdown?

[Markdown](http://fr.wikipedia.org/wiki/Markdown) est un langage de balisage
léger créé par [John Gruber](https://fr.wikipedia.org/wiki/John_Gruber) et
[Aaron Swartz](https://fr.wikipedia.org/wiki/Aaron_Swartz) en 2004. Avec un
logiciel de traitement de texte comme MS Word ou LibreOffice Writer, seul le
résultat final est visible mais pas les commandes de mise en forme (WYSIWYG ---
What You See Is What You Get, ou What You see Is _only_ What You Get...). Avec un
langage à balises comme Markdown, LaTeX ou HTML, on écrit et voit les commandes
de mise en forme mais pas directement le résultat final.

Markdown est simple, simple, simple:

* Installation très simple;

* Langage très simple, s'apprenant rapidement;

* Export très simple vers d'autres formats (HTML, pdf, docx).

Est-ce trop simple? Tout dépend du degré de complexité que l'on veut. LaTeX est
particulièrement approprié pour _l'impression_ de documents, avec un magnifique
rendu, et la possibilité d'éditer des éléments compliqués, tels que des
formules mathématiques. Mais au prix d'une syntaxe demandant une certaine
expérience. Markdown est particulièrement dédié au HTML, avec des possibilités
de composition plus limitée que LaTeX mais permettant une interaction avec le
document.

### HTML? Mais mon superviseur veut un document .doc!

C'est ici qu'intervient [Pandoc](http://johnmacfarlane.net/pandoc). Pandoc est
un convertisseur universel de documents. Pandoc peut convertir Markdown dans de
nombreux autres formats tels que LaTeX, HTML, Rich Text Format (*.rtf*), E-Book
(*.epub*), Microsoft Word (*.docx*), OpenDocument Text (*.odt*), etc. Pandoc est
un outil en ligne de commande. Une fois un terminal ouvert, on peut écrire des
commandes telles que celles-ci pour convertir un fichier Markdown test.md dans
d'autres formats: `pandoc test.md -o test.html`, `pandoc test.md -o test.odt`,
`pandoc test.md -o test.rtf`, `pandoc test.md -o test.docx`, or `pandoc test.md
-o test.pdf`.

### Ligne de commande? Je pensais que c'était simple!

La ligne de commande, c'est simple... Mais on peut se faciliter la vie en
utilisant le package `rmarkdown` gérant les 73 arguments de ligne de commande de
Pandoc (et les 49 options de `knitr`). Le tout directement à partir de RStudio!

### Syntaxe

Les titres de sections sont indiqués par un ou plusieurs #, selon le niveau de
profondeur du titre. La mise en gras se fait en encadrant le texte par deux
étoiles et la mise en italique par une étoile. Pour un espacement fixe
(monospace), on entoure le texte avec deux guillemets obliques (\`). Les
instructions pour `R` sont encadrées par \`\`\``{r}` et \`\`\` (appelé "chunk").

## Comment ça marche?

Un ficher `R` markdown avec l'extension .Rmd (ou .rmd) contient du texte et des
"chunks" contenant le code `R` à interpréter. Ce fichier est compilé, le code `R` est
évalué, son résultat obtenu et le tout est rendu dans un fichier markdown .md.
Ce fichier est alors rendu dans le format voulu (pdf, doc etc.).

> **Note:** [LaTeX](http://www.latex-project.org/) doit être installé pour
> pouvoir produire un fichier pdf.

## Comment faire?

  * Dans RStudio, installer les packages `knitr` et `rmarkdown`:


<pre class='in'><code>install.packages('knitr', dependencies = TRUE)
install.packages("rmarkdown")</code></pre>

  * Puis choisir l'option `Weave Rnw files using knitr` (Tools > Global Options >
Sweave)

<img src="figure/RStudio_option.png" width="50%" height="50%"/>

  * Créer un document vierge R markdown. Un document-type est déjà disponible.
Vous pouvez remplacer les parties correspondantes par les vôtres.

<img src="figure/RMarkdown_create.png" width="75%" height="75%"/>

  * Si vous avez besoin d'aide pour la syntaxe markdown, utiliser l'aide:

<img src="figure/RMarkdown_ref.png" width="75%" height="75%"/>

  * Ensuite il vous reste à "kniter" le document:

<img src="figure/RMarkdown_knit.png" width="75%" height="75%"/>

### Quand mettre en place la reproductibilité?

* N'importe quand mais c'est toujours mieux de le faire au début d'un projet.
* Toujours préférable d'êytre mis en place en même temps qu'un contrôle de
  version comme Git.
* En utilisant un logiciel comme R où les insructions sont données sous forme de
  code.
* Ne jamais sauver la sortie (seul le jeu de données brut avec le code de
  traitement. Même les jeux de données nettoyés peuvent être supprimés mais cela
  peut aider de les sauvegarder temporaireemnt lors des étapes intermédiaires).
* Finalement, enregistrer les données dans un format non-propriétaire (p.ex.
  `csv` plutôt que `xls`). Cela vous assure que vos données pourront être lues
  dans le futur. 

---
**Informations additionnelles**

[`knitr`](http://yihui.name/knitr)

[Original markdown reference](http://daringfireball.net/projects/markdown/basics)

[Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

[`R` Markdown cheatsheet](http://shiny.rstudio.com/articles/rm-cheatsheet.html)

[Dynamic Documents with `R` and `knitr`](http://www.crcpress.com/product/isbn/9781482203530)

[`R` markdown](http://rmarkdown.rstudio.com/)

[Markdown et Pandoc](http://enacit1.epfl.ch/markdown-pandoc/)

[`knitr` in a knutshell](http://kbroman.org/knitr_knutshell/)
