🛠️  ** | OPTYMALIZACJE**

Support Team zaleca zapoznanie się z tym poradnikiem odnośnie optymalizacji:
*https://github.com/YouHaveTrouble/minecraft-optimization*


:shield: ** | OCHRONA ANTYCRASH**

Support Team zaleca następujące zabezpieczenia Anti-Crash:

:white_check_mark:  **| DARMOWE**

EpicGuard (Spigot)

ExploitFixer (Spigot)

SafeMC-AntiCrash-Free (Spigot)

:moneybag:  **| PŁATNE**

SafeMC Premium (Spigot)

EyfenCord (Bungee)

GuardSpigot (Silnik zabezpieczający Spigota)



----------------------------------------------




:robot:  ** | OCHRONA ANTI-BOT**

Support Team zaleca następujące zabezpieczenia Anti-Bot:

:white_check_mark:  **| DARMOWE**

[2LS] AntiBot (Bungee, dostępny na SpigotMC)

**:moneybag:  | PŁATNE**

EyfenCord (Bungee, pełni też funkcję AntiCrash)

BotSentry (Bungee, bardzo intuicyjny, z zaawansowanym podglądem na ataki i zarządzaniem)




----------------------------------------------





:robot: ** | Silniki**

Support Team, w celu uzyskania najlepszej wydajności oraz bezpieczeństwa serwera, zaleca użycie następujących silników:

Silniki na serwery główne:

PaperMC - Fork Spigota w celu poprawienia bezpieczeństwa oraz wydajności. // https://papermc.io/downloads (rekomendowany na wszystkie wersje)

Tuinity - Fork Papera w celu uzyskania lepszej wydajności. // https://github.com/Spottedleaf/Tuinity (rekomendowany na wyższe wersje)

Airplane - Fork Tuinity w celu uzyskania jeszcze lepszej wydajności. // https://dl.airplane.gg (rekomendowany na wyższe wersje)

**Purpur - Fork Airplane mający na celu umożliwieniu administratorom serwera swobodnej i prostej konfiguracji.** // https://purpur.pl3x.net (rekomendowany na wyższe wersje)

💰 GuardSpigot - fork Spigota mający na celu dodatkowe zabezpieczenia przed crashami. (rekomendowany na niższe wersje, lub jeżeli posiadasz na serwerze multiwersję)

Silniki na serwery Proxy:
Waterfall - Ulepszony fork Bungeecorda pod wieloma względami
Velocity - Ulepszony fork Bungeecorda pod względem wydajności oraz bezpieczeństwa.




----------------------------------------------




:speech_balloon: ** | CHAT**

Aby skonfigurować chat, potrzebujesz pluginu Vault, pluginu z permisjami (np. LuckPerms) oraz pluginu EssentialsXChat wraz z EssentialsX.
Aby zmienić format chatu, musimy wejść w config.yml EssentialsX i poszukać sekcji odpowiadającej za chat. Mamy tam wartość `group-formats`, w której możemy
nadawać formaty czatu dla rang. Pamiętajmy, aby stworzyć grupę oraz nadać ją sobie w celu sprawdzenia!
`(/lp creategroup <nazwa>, /lp user <nick> parent add <ranga>)`
W razie dodatkowych pytań skontaktuj się z Support Teamem. 




----------------------------------------------



:crown: ** | PERMISJE**

Aby dodać/usunąć permisje dla danej rangi, należy użyć następujących komend (plugin LuckPerms):

`/lp group <nazwa_rangi> permission set <permisja>` (dodawanie)

`/lp group <nazwa_rangi> permission unset <permisja>` (usuwanie)

W przypadku pluginu PermissionsEx zamiast `permission set/unset` należy wpisać po prostu `add/remove`
W razie dodatkowych pytań skontaktuj się z Support Teamem.





----------------------------------------------





:earth_africa:  ** | SPAWN**

Aby ustawić spawn, potrzebujesz pluginu EssentialsX z dodatkiem EssentialsXSpawn. Możesz go pobrać tutaj: https://essentialsx.net
Następnie, stajemy w miejscu w którym chcemy ustawić spawn i wpisujemy /setspawn <ranga> / *

:lock: ** | ZABEZPIECZANIE SPAWNU**

W tym celu potrzebujesz pluginów WorldEdit oraz WorldGuard.
Wpisujemy komendę `//wand` i zaznaczamy teren. Następnie patrzymy się w dół i wpisujemy komendę `//expand 100 100`
Potem zostało nam tylko zdefiniowanie regionu komendą `/rg define <nazwa_regionu>`
Nasz region jest już zabezpieczony, jednak z pewnością chcielibyśmy modyfikować jego ustawienia, wystarczy wpisać komendę `/rg flags <region>` i wyświetli nam się interaktywna wiadomość na czacie, w której możemy ustawiać tzw. flagi dla naszego regionu.
