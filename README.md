💻 **| INSTALACJA SILNIKA**

Większość hostingów preinstaluje silniki, jednak może nadejść moment, gdy musisz wgrać własny. I co wtedy?

Aby zainstalować silnik, najpierw należy go pobrać.
Dla przykładu PaperMC, pobieramy go ze strony papermc.io/downloads. Ja pobiorę Build #
Następnie tworzymy folder, w którym ma znajdować się nasz serwer i przenosimy do niego plik silnika serwera.
Zmieniamy nazwę silnika serwera na jakąś prostą, pamiętajmy jednak, że musimy zachować format .jar, np. server.jar
Jeżeli jesteśmy na VPS/Dedyku musimy najpierw zainstalować Javę oraz aplikację `screen`. Jeżeli już ją masz pomiń ten krok.
Wpisujemy komendy:
`apt-get install openjdk-11-jre`
`apt-get install screen`
`java -version`
Jeżeli wyświetli nam się komunikat informujący o obecności Javy, to już prawie gotowe.
Musimy teraz stworzyć plik uruchamiający serwer. W przypadku Linuxa będzie to start.sh

Wpisujemy tam następujący kod:
screen -dmS java -Xms10G -Xmx10G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true -jar server.jar nogui

I zapisujemy plik jako start.sh w folderze z serwerem.
Teraz wpisujemy komendę:
`chmod +x server.jar`
oraz
`./start.sh`

Teraz powinna nam się ukazać konsola serwera. Jeżeli to nie nastąpi, wpisujemy `screen -ls`. Teraz wyświetli nam się lista naszych screenów wraz z ich nazwami. Następnie wpisujemy:
`screen -S "<nazwa_screena>"`

W razie dodatkowych pytań skontaktuj się z supportem

:hammer_and_wrench:  **| OPTYMALIZACJE**

Support Team zaleca zapoznanie się z tym poradnikiem odnośnie optymalizacji:
*https://github.com/YouHaveTrouble/minecraft-optimization*


:shield: **| OCHRONA ANTYCRASH**

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




:robot:  **| OCHRONA ANTI-BOT**

Support Team zaleca następujące zabezpieczenia Anti-Bot:

:white_check_mark:  **| DARMOWE**

[2LS] AntiBot (Bungee, dostępny na SpigotMC)

**:moneybag:  | PŁATNE**

EyfenCord (Bungee, pełni też funkcję AntiCrash)

BotSentry (Bungee, bardzo intuicyjny, z zaawansowanym podglądem na ataki i zarządzaniem)




----------------------------------------------





:robot: **| Silniki**

Support Team, w celu uzyskania najlepszej wydajności oraz bezpieczeństwa serwera, zaleca użycie następujących silników:

Silniki na serwery główne:

PaperMC - Fork Spigota w celu poprawienia bezpieczeństwa oraz wydajności. // https://papermc.io/downloads (rekomendowany na wszystkie wersje)

Tuinity - Fork Papera w celu uzyskania lepszej wydajności. // https://github.com/Spottedleaf/Tuinity (rekomendowany na wyższe wersje)

Airplane - Fork Tuinity w celu uzyskania jeszcze lepszej wydajności. // https://dl.airplane.gg (rekomendowany na wyższe wersje)

**Purpur - Fork Airplane mający na celu umożliwieniu administratorom serwera swobodnej i prostej konfiguracji.** // https://purpur.pl3x.net (rekomendowany na wyższe wersje)

💰  GuardSpigot - fork Spigota mający na celu dodatkowe zabezpieczenia przed crashami. (rekomendowany na niższe wersje, lub jeżeli posiadasz na serwerze multiwersję)

Silniki na serwery Proxy:
Waterfall - Ulepszony fork Bungeecorda pod wieloma względami
Velocity - Ulepszony fork Bungeecorda pod względem wydajności oraz bezpieczeństwa.




----------------------------------------------




:speech_balloon: **| CHAT**

Aby skonfigurować chat, potrzebujesz pluginu Vault, pluginu z permisjami (np. LuckPerms) oraz pluginu EssentialsXChat wraz z EssentialsX.
Aby zmienić format chatu, musimy wejść w config.yml EssentialsX i poszukać sekcji odpowiadającej za chat. Mamy tam wartość `group-formats`, w której możemy
nadawać formaty czatu dla rang. Pamiętajmy, aby stworzyć grupę oraz nadać ją sobie w celu sprawdzenia!
`(/lp creategroup <nazwa>, /lp user <nick> parent add <ranga>)`
W razie dodatkowych pytań skontaktuj się z Support Teamem. 




----------------------------------------------



:crown: **| PERMISJE**

Aby dodać/usunąć permisje dla danej rangi, należy użyć następujących komend (plugin LuckPerms):

`/lp group <nazwa_rangi> permission set <permisja>` (dodawanie)

`/lp group <nazwa_rangi> permission unset <permisja>` (usuwanie)

W przypadku pluginu PermissionsEx zamiast `permission set/unset` należy wpisać po prostu `add/remove`
W razie dodatkowych pytań skontaktuj się z Support Teamem.





----------------------------------------------





:earth_africa:  **| SPAWN**

Aby ustawić spawn, potrzebujesz pluginu EssentialsX z dodatkiem EssentialsXSpawn. Możesz go pobrać tutaj: https://essentialsx.net
Następnie, stajemy w miejscu w którym chcemy ustawić spawn i wpisujemy /setspawn <ranga> / *

:lock: **| ZABEZPIECZANIE SPAWNU**

W tym celu potrzebujesz pluginów WorldEdit oraz WorldGuard.
Wpisujemy komendę `//wand` i zaznaczamy teren. Następnie patrzymy się w dół i wpisujemy komendę `//expand 100 100`
Potem zostało nam tylko zdefiniowanie regionu komendą `/rg define <nazwa_regionu>`
Nasz region jest już zabezpieczony, jednak z pewnością chcielibyśmy modyfikować jego ustawienia, wystarczy wpisać komendę `/rg flags <region>` i wyświetli nam się interaktywna wiadomość na czacie, w której możemy ustawiać tzw. flagi dla naszego regionu.
