Poniżej znajduje się dokumentacja przeznaczona na Discord z Tworzenia Serwerów.

Playlista z tworzenia serwerów: https://www.youtube.com/playlist?list=PL_BBuK-pXvpXsYuKQg3JMghpAHg2td5WL



Playlista z tworzenia serwerów PLUS: https://www.youtube.com/playlist?list=PL_BBuK-pXvpUzafMeyIOwj1ppaHY3LkQZ


**1. Podstawy**



1.1 Instalacja silnika gry oraz organizacja miejsca.

Większość hostingów preinstaluje silniki, jednak może nadejść moment, gdy musisz wgrać własny. I co wtedy?


Musimy stworzyć miejsce w którym będzie znajdował się nasz serwer MC. Wpisujemy komendy:


`cd /home/`


oraz


`mkdir <nazwa_folderu>`




Aby zainstalować silnik, najpierw należy go pobrać.
Dla przykładu PaperMC, pobieramy go ze strony papermc.io/downloads. Ja pobiorę Build #645. W tym celu wpisuję komendę:

`wget https://papermc.io/api/v2/projects/paper/versions/1.16.5/builds/645/downloads/paper-1.16.5-645.jar`


Następnie do naszego, stworzonego wcześniej przez nas folderu, przenosimy plik silnika serwera.



Zmieniamy nazwę silnika serwera na jakąś prostą, pamiętajmy jednak, że musimy zachować format .jar, np. server.jar
Jeżeli jesteśmy na VPS/Dedyku musimy najpierw zainstalować Javę oraz aplikację `screen`. Jeżeli już ją masz pomiń ten krok.
Wpisujemy komendy:

`apt-get install openjdk-11-jre`


`apt-get install screen`


`java -version`


Jeżeli wyświetli nam się komunikat informujący o obecności Javy, to już prawie gotowe.
Musimy teraz stworzyć plik uruchamiający serwer. W przypadku Linuxa będzie to start.sh

Wpisujemy tam następujący kod:



```
screen -dmS java -Xms10G -Xmx10G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true -jar server.jar nogui
```


UWAGA! Wartość `10G` to liczba twojego RAMU serwera! Np. jeżeli chcesz przydzielić 3500MB ram, wpisujesz `3500M`.


I zapisujemy plik jako start.sh w folderze z serwerem.
Teraz wpisujemy komendę:
`chmod +x server.jar`

1.2 Uruchamianie serwera.

W tym celu wpisujemy komendę:

`./start.sh`

Teraz powinna nam się ukazać konsola serwera. Jeżeli to nie nastąpi, wpisujemy `screen -ls`. Teraz wyświetli nam się lista naszych screenów wraz z ich nazwami. Następnie wpisujemy:

`screen -S "<nazwa_screena>"`


W razie dodatkowych pytań skontaktuj się z supportem.

2. Optymalizacja

Support Team zaleca zapoznanie się z tym poradnikiem odnośnie optymalizacji:
*https://github.com/YouHaveTrouble/minecraft-optimization*


3. Zabezpieczenia:

3.1 Ochrona Anti-Crash

**UWAGA! Jeżeli masz serwer na wersji 1.16.x, to prawdopodobnie nie będziesz potrzebował zabezpieczenia typu Anti-Crash**

Support Team zaleca następujące zabezpieczenia Anti-Crash:

**DARMOWE:**

EpicGuard (Spigot)

ExploitFixer (Spigot)

SafeMC-AntiCrash-Free (Spigot)

**PŁATNE:**

SafeMC Premium (Spigot)

EyfenCord (Bungee)

GuardSpigot (Silnik zabezpieczający Spigota)



----------------------------------------------




3.2 Ochrona Anti-Bot

Support Team zaleca następujące zabezpieczenia Anti-Bot:

**DARMOWE:**

[2LS] AntiBot (Bungee, dostępny na SpigotMC)

**PŁATNE:**

EyfenCord (Bungee, pełni też funkcję AntiCrash)

BotSentry (Bungee, bardzo intuicyjny, z zaawansowanym podglądem na ataki i zarządzaniem)




----------------------------------------------





4. Wybór silników i ich cechy.



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




5. Konfiguracja Chatu, prefixów.

Aby skonfigurować chat, potrzebujesz pluginu Vault, pluginu z permisjami (np. LuckPerms) oraz pluginu EssentialsXChat wraz z EssentialsX.
Aby zmienić format chatu, musimy wejść w config.yml EssentialsX i poszukać sekcji odpowiadającej za chat. Mamy tam wartość `group-formats`, w której możemy
nadawać formaty czatu dla rang. Pamiętajmy, aby stworzyć grupę oraz nadać ją sobie w celu sprawdzenia!
`(/lp creategroup <nazwa>, /lp user <nick> parent add <ranga>)`
W razie dodatkowych pytań skontaktuj się z Support Teamem. 




----------------------------------------------



6. Permisje.

Aby dodać/usunąć permisje dla danej rangi, należy użyć następujących komend (plugin LuckPerms):

`/lp group <nazwa_rangi> permission set <permisja>` (dodawanie)

`/lp group <nazwa_rangi> permission unset <permisja>` (usuwanie)

W przypadku pluginu PermissionsEx zamiast `permission set/unset` należy wpisać po prostu `add/remove`
W razie dodatkowych pytań skontaktuj się z Support Teamem.

Więcej informacji o pluginie LuckPerms znajdziecie pod: https://luckperms.net/wiki/Home





----------------------------------------------




7. Spawn

Aby ustawić spawn, potrzebujesz pluginu EssentialsX z dodatkiem EssentialsXSpawn. Możesz go pobrać tutaj: https://essentialsx.net
Następnie, stajemy w miejscu w którym chcemy ustawić spawn i wpisujemy /setspawn [ranga] / *


7.1 Zabezpieczanie spawnu


W tym celu potrzebujesz pluginów WorldEdit oraz WorldGuard.
Wpisujemy komendę `//wand` i zaznaczamy teren. Następnie patrzymy się w dół i wpisujemy komendę `//expand 100 100`
Potem zostało nam tylko zdefiniowanie regionu komendą `/rg define <nazwa_regionu>`
Nasz region jest już zabezpieczony, jednak z pewnością chcielibyśmy modyfikować jego ustawienia, wystarczy wpisać komendę `/rg flags <region>` i wyświetli nam się interaktywna wiadomość na czacie, w której możemy ustawiać tzw. flagi dla naszego regionu.
