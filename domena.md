# Doména

To, co jako uživatelstvo považujeme za webovou stránku, není ve své podstatě nic jiného než HTML soubor (často doplněný o CSS a JavaScript), který našemu prohlížeči na dané URI (uniform resource identifier) adrese poskytuje vzdálený počítač.
Poskytnutý soubor HTML (+ CSS a JS) poté náš prohlížeč interpretuje a předkládá ve vizuální podobě.
Obecně se prohlížeče snaží dohodnout na jednotném stylu interpretace, ale z technických i jiných důvodů se výsledky mohou někdy lišit (a stejně tak můžeme my anebo náš software je záměrně modifikovat - viz. třeba adBlocker nebo režim čtení).

Množina prolinkovaných HTML souborů na různých URL, často vytváří dojem toho, čemu můžeme někdy říkat web, zkrátka jednoho často vizuálně uceleného zdroje informací, na kterém můžeme brouzdat a zobrazovat různé detaily, podstránky, vykonávat nějakou činnost.
 
Obecně můžeme říct, že HTML nese obsah, CSS se stará o vizualitu a JavaScript zařizuje interaktivitu, toto však není výlučné a jednoznačné, jak se dozvíme během semestru - JavaScript může načítat data a měnit elementy HTML, CSS může reagovat jinak při různých šířkách obrazovek, HTML samotné může nést CSS a JavaScript v sobě samém. 

## Jak to probíhá

### 1. Zadání adresy
Když zadáme URL adresu do prohlížeče (například favu.vut.cz/studenti), prohlížeč z ní vyvodí několik závěrů:

1. protokol - pokud nespecifikujeme, prohlížeče si dnes doplní https://, případně přečtou http:// nebo https://.
Protokol HTTP (hypertext transfer protocol) je jedním z protokolů aplikační vrstvy ISO/OSI (například vedle BitTorrent - peer2peer sdílení souborů, POP3 - email, SMTP - email, FTP - přenos souborů, IRC - chat a řady dalších) a je zodpovědný za komunikaci s web servery a přenos hypertextových souborů (HTML, XML a jiných).
Protokol HTTPS je jeho zabezpečenou novější variantou, která přidává kontrolu, zda server, se kterým komunikujeme, je důvěryhodný, a také přidává šifrování naší komunikace.
Tím nás chrání před odposlechy komunikace třetími stranami a podstrčením falešného obsahu (man in the middle attack).
2. doménu prvního řádu (cz ve favu.vut.cz), doménu (vut ve favu.vut.cz) a případně subdoménu (favu ve favu.vut.cz).
Doména prvního řádu definuje, kdo je zodpovědný za přidělování domén - cz domény přiděluje organizace NIC.cz pověřená Českou republikou, domény .org jiná organizace mající jiná pravidla (a ceny).
Doména druhého řádu je fakticky to, co vlastníme, pokud si zaregistrujeme nějakou doménu, například VUT vlastní doménu druhého řádu vut na doméně prvního řádu cz.
Na této doméně druhého řádu, si potom může její vlastnice či vlastník zřídit jaké jen chce subdomény - je to už jen jejich volba.
Vlastník domény skrze DNS určuje, na jakou IP adresu doména odkazuje - na této IP adrese by potom měl být dostupný web server, který poskytuje HTML obsah.
3. cestu k souboru specifikovanou za lomítkem za doménou prvního řádu, v našem příkladu /studenti, ale může jít o delší cestu, nebo naopak žádnou, potom se poskytne tzv. index file, de facto hlavní stránka (často pojmenovaná index.html).
4. z protokolu se často také odvodí port - pro HTTP standardně 80, pro HTTPS standardně 443, ale můžeme specifikovat i jiný port, například: www.favu.vut.cz:8080/studenti. Server nám ale pravděpodobně neodpoví, není to standard na tomto portu očekávat HTTP(S) provoz. Často ale podobné porty otevíráme při lokálním vývoji serveru - např. localhost:8080, http://localhost:62485/about a podobně.

###

## URI
```
          userinfo       host      port
          ┌──┴───┐ ┌──────┴──────┐ ┌┴┐
  https://john.doe@www.example.com:123/forum/questions/?tag=networking&order=newest#top
  └─┬─┘   └─────────────┬────────────┘└───────┬───────┘ └────────────┬────────────┘ └┬┘
  scheme          authority                  path                  query           fragment
```