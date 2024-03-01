# Registrace Domény

Počítače jsou v síti identifikované pomocí IP adresy, například: 147.229.2.90 (IPv4), nebo novější 2001:718:1:1::1 (IPv6).
Protože pamatovat si IP adresy je pro lidi nepřirozené, vznikla potřeba nějakého lidsky čitelného způsobu, jak se k počítači dostat.
Řešením, které vzniklo a dodnes se používá je protokol DNS (domain name system).
Jde o federativní protokol, který umožňuje překlad doménových jmen na IP adresy.

## Úvod
### Jak to funguje
Když zadáme do prohlížeče nějakou doménu, například favu.vut.cz, prohlížeč se zeptá na DNS server, který je zodpovědný za doménu vut.cz, na jakou IP adresu má odkazovat doména favu.vut.cz.
Tento server mu odpoví, že má odkazovat na IP adresu 147.229.2.90 a prohlížeč se potom připojí na tuto IP adresu a požádá o obsah stránky.
Právo na změnu IP adresy, na kterou doména odkazuje, má vlastník domény, který si platí registraci domény u registrátora.

### Jak zjistit IP adresu
Zjistit IP adresu můžeme například na Linuxu/Macu: `dig +short favu.vut.cz`, nebo na Windowsu: `nslookup favu.vut.cz`.

### Hack - vlastní DNS server
Pokud si chceme vyzkoušet, jak DNS funguje, můžeme si na svém počítači nastavit vlastní DNS server, který bude odpovídat na dotazy o domény.
Případně nastavit DNS v síti, kterou ovládáme, tak, aby místo pravdivých odpovědí poskytovala naše vlastní odpovědi.
Jde o jednoduchý způsob, jak si vyzkoušet, jak DNS funguje, a také jak se dá DNS zneužít k uměleckým intervencím na síť.

## Prakticky


# Web 
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

### 2. vyžádání adresy IP skrze DNS

Prohlížeč se dotáže DNS serveru, na jakou adresu odkazuje doména favu.vut.cz, získá IP adresu a může jít na další krok.

### 3. vyžádání obsahu

1. Prohlížeč vytvoří HTTP request na adresu, kterou zjistil, a požádá o obsah stránky.

Typy requestů:
- GET - požaduje obsah stránky
- POST - požaduje změnu stavu na serveru
- PUT - požaduje vložení nového obsahu
- DELETE - požaduje smazání obsahu
- PATCH - požaduje změnu části obsahu
- a další

2. webový server vrátí odpověď, součástí odpovědi je i HTTP status code, který říká, jak se serverovi podařilo požadavek zpracovat.

Status kódy:
- 1xx - informační
- 2xx - úspěšný požadavek - 200 OK, 201 Created, 204 No Content
- 3xx - přesměrování - 301 Moved Permanently, 302 Found, 307 Temporary Redirect
- 4xx - chyba na straně klienta - 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found (často chyba uživatele, například chce URL, která (už) neexistuje)
- 5xx - chyba na straně serveru - 500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable (pokud vyvíjíme server my, toto je většinou naše chyba)
- a další

Server může vrátit odpověď jako HTML, ale také jako JSON, XML, nebo jiný formát, který klient požaduje.
Klasicky se vrací HTML, ale například při požadavcích na API se často vrací JSON, který poté zpracuje JavaScript v prohlížeči a zobrazí uživateli.

### 4. dynamické dovyžádání obsahu
V bodě 3 končí klasický statický web.
Server vrátil HTML, konec.
V dnešní době ale často takto načtená HTML stránka obsahuje i JavaScript, který může dodatečně načítat další obsah, nebo měnit obsah stránky.
V takové případě dělá v pozadí JavaScript další HTTP requesty na server, který mu vrátí obsah, který potom JavaScript zpracuje a zobrazí uživateli změnou HTML elementů.

## URI
```
          userinfo       host      port
          ┌──┴───┐ ┌──────┴──────┐ ┌┴┐
  https://john.doe@www.example.com:123/forum/questions/?tag=networking&order=newest#top
  └─┬─┘   └─────────────┬────────────┘└───────┬───────┘ └────────────┬────────────┘ └┬┘
  scheme          authority                  path                  query           fragment
```