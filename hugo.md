# Hugo

Hugo je generátor statického webu.
Hodí se v situaci, kdy chceme zveřejnit větší web, ale třeba nemáme moc prostředků - proto zvolíme statický web namísto WordPressu či něčeho podobného.
Nevýhodou je absence online administrace.
Výhodou je téměř nulová cena za hosting (když použijeme třeba Github Pages pro hosting).

Ve stručnosti řečeno Hugo dělá toto:
markdown + templates + static files -> prolinkované HTML soubory

## Prerekvizity: Instalace Hugo příkazu
https://gohugo.io/installation/

Ověříme tím, že v terminálu spustíme:
`hugo version`

## Ukázkový projekt

1. `hugo new site mujweb` - vytvori slozku mujweb, ve ktere vyplni kostru Hugo projektu
```
$ hugo new site mujweb
Congratulations! Your new Hugo site was created in /Users/ag/devel/teachings/kreap3/hugo-sample/lol.

Just a few more steps...

1. Change the current directory to /Users/ag/devel/teachings/kreap3/hugo-sample/lol.
2. Create or install a theme:
   - Create a new theme with the command "hugo new theme <THEMENAME>"
   - Install a theme from https://themes.gohugo.io/
3. Edit hugo.toml, setting the "theme" property to the theme name.
4. Create new content with the command "hugo new content <SECTIONNAME>/<FILENAME>.<FORMAT>".
5. Start the embedded web server with the command "hugo server --buildDrafts".
```

2. `cd mujweb` - vejdeme do slozky, abysme byli v projektu

3. `hugo new theme mujtheme` - vytvori kostru theme/sablony v `mujweb/themes/mujtheme` - ta je zodpovedna za to, jak se content zobrazuje, bez ni to nejde
```
$ hugo new theme mujtheme
Creating new theme in /Users/ag/devel/teachings/kreap3/hugo-sample/themes/mujtheme
```

4. `hugo new content mujprvnipost.md` - vytvori prvni content (stranku jinou nez index.html) - v tomto pripade je to markdown soubor, ktery se nachazi v `mujweb/content/mujprvnipost.md` nebo pozdeji na serveru: `http://localhost:1313/myfirstpost/`
```
$ hugo new content mujprvnipost.md
Content "/Users/ag/devel/teachings/kreap3/hugo-sample/content/mujprvnipost.md" created
```

5. Otevreme soubor `mujweb/hugo.toml` - tohle je konfigurace Hugo projektu. Musime zde pridat `theme = "mujtheme"`, aby Hugo vedelo, ze ma pouzit nas novy theme, jinak to nejspis nepojede.
Kdyz jsme u toho, muzeme udelat i par dalsich editu, z tohoto pocatecniho stavu:
```
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
```

Treba na:

```
baseURL = 'https://mujenejakadomena.cz/'
languageCode = 'en-us'
title = 'Muj Web'
theme = 'mujtheme'
```

5. `hugo server` - prikaz, aby se hugo choval jako lokalni webserver - to je super, protoze automaticky nacita zmenene soubory a reloduje stranky, web je dostupny na: http://localhost:1313

### volitelne: Init git repository
V tento moment muzeme iniciovat git repo a napojit si to na GitHub:
1. `git init` - inicializuje git repo
2. `git remote add origin https://github.com/<username>/<mujweb>.git` - doporucuji drzet stejny nazev repa jako je nazev slozky lokalne, lepe se v tom pak vyzna
3. `git add .` - přidani vsech souboru do gitu
4. `git commit -m "Initial commit Hugo projektu mujweb"` - udelame prvni commit
5. `git push --set-upstream origin main` - nastavime upstream - vicemene jen rekneme, ze nase lokalni branch ma jit na remote origin a taky na branch main

### Struktura skeletonu Hugo projektu

```
$ tree
.
├── archetypes                    # templates pro novy content, nemusi nas moc zajimat
│   └── default.md
├── assets                        # The assets directory contains global resources typically passed through an asset pipeline. This includes resources such as images, CSS, Sass, JavaScript, and TypeScript. 
├── content                       # zde definujeme samotny obsah webu skrze Markdown soubory a strukturu skrze cleneni slozek
│   └── mujprvnipost.md
├── data
├── hugo.toml                     # konfiguracni soubor Hugo projektu - nadpis webu, domena atd.
├── i18n                          # internationalization - preklady pokud chceme mit vice jazykovych variant
├── layouts                      
├── public                        # vlastne vysledny build nasi stranky
│   ├── categories
│   │   ├── index.html
│   │   └── index.xml
│   ├── css
│   │   └── main.css
│   ├── favicon.ico
│   ├── index.html
│   ├── index.xml
│   ├── js
│   │   └── main.js
│   ├── posts
│   │   ├── index.html
│   │   ├── index.xml
│   │   ├── post-1
│   │   │   └── index.html
│   │   ├── post-2
│   │   │   └── index.html
│   │   └── post-3
│   │       ├── bryce-canyon.jpg
│   │       └── index.html
│   ├── sitemap.xml
│   └── tags
│       ├── blue
│       │   ├── index.html
│       │   └── index.xml
│       ├── green
│       │   ├── index.html
│       │   └── index.xml
│       ├── index.html
│       ├── index.xml
│       └── red
│           ├── index.html
│           └── index.xml
├── resources                      # The resources directory contains cached output from Hugo’s asset pipelines, generated when you run the hugo or hugo server commands. By default this cache directory includes CSS and images.
├── static                         # Staticke soubory jako favicon.ico, robots.txt, driv zde byly i CSS a JavaScript, ale ted se doporucuje ./assets
└── themes                         # zde se instaluji/vytvareji themes, muzeme jich mit vice a zkouset je
    └── mujtheme
        ├── LICENSE
        ├── README.md
        ├── archetypes
        │   └── default.md
        ├── assets
        │   ├── css
        │   │   └── main.css
        │   └── js
        │       └── main.js
        ├── content
        │   ├── _index.md
        │   └── posts                     # skeleton theme pridava vlastni obsah pro ukazkove ucely, idealne muzeme casem smazat
        │       ├── _index.md
        │       ├── post-1.md
        │       ├── post-2.md
        │       └── post-3
        │           ├── bryce-canyon.jpg   # ale aspon vidime strukturu - dobre porovnat s tim, jak se to reflektuje v URL
        │           └── index.md
        ├── data
        ├── hugo.toml
        ├── i18n
        ├── layouts                        # tohle nas zajima nejvic, protoze je to struktura, ktera se pouziva pro vytvareni stranky
        │   ├── _default                   # default layout, ktery se pouziva pro vsechny stranky
        │   │   ├── baseof.html
        │   │   ├── home.html
        │   │   ├── list.html
        │   │   └── single.html
        │   └── partials                    # partials jsou kousky HTML, ktere muzeme pouzit v jinych layoutech, treba header pouzijeme v home.html, list.html atd. abysme se neopakovali
        │       ├── footer.html
        │       ├── head
        │       │   ├── css.html
        │       │   └── js.html
        │       ├── head.html
        │       ├── header.html
        │       ├── menu.html
        │       └── terms.html
        ├── static
        │   └── favicon.ico
        └── theme.toml                    # metadata o tvurcich themu, kdybysme jej chteli zverejnit, meli bysme vyplnit

37 directories, 50 files
```

Kompletni a nejcerstvejsi informace na: https://gohugo.io/getting-started/directory-structure/

