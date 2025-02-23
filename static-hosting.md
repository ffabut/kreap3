# Statický hosting

Pro hosting statických stránek (které nepotřebují backend server) není potřeba kupovat žádný drahý hosting ani nic podobného.
Statické stránky lze hostovat zcela zdarma.
Nejjednodušší cesta je využít některého z poskytovatelů online repozitářů pro kód, např.:

- github.com
- gitlab.com
- codeberg.org
- code.nolog.cz

Postup se u každého poskytovatele drobně liší, je potřeba pročíst jejich dokumentaci.
Jedno však mají společné: na platformě musím založit repozitář pro náš kód a HTML soubory poté nahrát do repozitáře pomocí nástroje `.git`.

Ač se postup může zdát složitý - proč se učit novou technologii a instalovat nový software .git - kvůli hostingu webu?
Výhoda je v tom, že pokud se tímto způsobem naučíme `.git` budeme moci:
- efektivně kolaborovat s ostatními na daném projektu statického webu
- budeme mít přehled o historii změn na webu
- můžeme stejné výhody použít i pro jakýkoliv jiný než HTML/CSS/JS kód

Git je extrémně užitečný a populární pomocný nástroj pro vývoj softwaru - kolem 95% developerů*ek jej využívá.
Je tak dobré se ho naučit, byť je celkem strašidelný.


## Statický web na Githubu

### Prerekvizity

- nainstalovaný git, pro popis postupu viz: https://github.com/ffabut/kreap2/tree/master/git#instalace-gitu.
- vytvořený účet na github.com, registrace na: https://github.com/signup

### Vytvoření repozitáře

Náš HTML/CSS/JS kód pro webovou stránku musí existovat v rámci tzv. repozitáře. Jinými slovy bysme mohli říct složky anebo projektu.
Vytvořit nový repozitář můžeme na: https://github.com/new

1. Při vytváření pojmenuj repozitář (např. muj-staticky-web).
2. Zvol public (pokud nechceš, aby byl soukromý).
3. Zvol předvyplnit README.md - jde o soubor, který slouží jako manuál.

### Klonování (stažení) repozitáře do počítače

1. V nově vytvořeném repozitáři na GitHubu najdi zelené tlačítko **Code** (vpravo nahoře).
2. Vyber **HTTPS** variantu klonování (nebo SSH, pokud máš nastavené SSH klíče) a zkopíruj odkaz.
3. V terminálu / příkazové řádce přejdi do složky, kde chceš mít projekt uložen.
4. Zadej příkaz:
    ```
    git clone https://github.com/username/repository_name.git
    ```


## Zdroje

- **Oficiální dokumentace Gitu:**  
  <https://git-scm.com/>  
- **GitHub a GitHub Pages:**  
  <https://docs.github.com/> | <https://pages.github.com/>  
- **Olia Lialina – „Summer” (2013):**  
  <https://rhizome.org/editorial/2013/aug/8/olia-lialina-summer-2013/>  
