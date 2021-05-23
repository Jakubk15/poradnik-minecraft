Poniżej znajduje się dokumentacja przeznaczona na [Discord z Tworzenia Serwerów.](https://discord.gg/RXkXWh6p4K)

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
Dla przykładu [PaperMC](https://papermc.io), pobieramy go ze strony https://papermc.io/downloads. Ja pobiorę Build #645. W tym celu wpisuję komendę:

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

`touch start.sh`

`nano start.sh`

**Jeżeli po wpisaniu powyższej komendy nie ujrzysz edytora tekstowego nano, musisz go zainstalować! Wpisz komendę:**

`apt-get install nano`

Wpisujemy tam następujący kod:



```
screen -dmS x java -Xms10G -Xmx10G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true -jar server.jar nogui
```


UWAGA! Wartość `10G` to liczba twojego RAMU serwera! Np. jeżeli chcesz przydzielić 3500MB ram, wpisujesz `3500M`.


I zapisujemy plik jako start.sh w folderze z serwerem.
Teraz wpisujemy komendę:
`chmod +x start.sh`

1.2 Uruchamianie serwera.

W tym celu wpisujemy komendę:

`./start.sh`

Teraz powinna nam się ukazać konsola serwera. Jeżeli to nie nastąpi, wpisujemy `screen -ls`. Teraz wyświetli nam się lista naszych screenów wraz z ich nazwami. Następnie wpisujemy:

`screen -r`


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

[PaperMC](https://papermc.io/downloads) - Fork Spigota w celu poprawienia bezpieczeństwa oraz wydajności. (rekomendowany na wszystkie wersje)

[Tuinity](https://github.com/Spottedleaf/Tuinity) - Fork Papera w celu uzyskania lepszej wydajności. rekomendowany na wyższe wersje)

[Airplane](https://dl.airplane.gg) - Fork Tuinity w celu uzyskania jeszcze lepszej wydajności. (rekomendowany na wyższe wersje)

**[Purpur](https://purpur.pl3x.net) - Fork Airplane mający na celu umożliwieniu administratorom serwera swobodnej i prostej konfiguracji.** (rekomendowany na wyższe wersje)

💰  [GuardSpigot](https://www.mc-market.org/resources/14497) - fork Spigota mający na celu dodatkowe zabezpieczenia przed crashami. (rekomendowany na niższe wersje, lub jeżeli posiadasz na serwerze multiwersję)

Silniki na serwery Proxy:
[Waterfall](https://papermc.io/downloads#Waterfall) - Ulepszony fork Bungeecorda pod wieloma względami


[Velocity](https://velocitypowered.com) - Ulepszony fork Bungeecorda pod względem wydajności oraz bezpieczeństwa.




----------------------------------------------




5. Konfiguracja Chatu, prefixów.

Aby skonfigurować chat, potrzebujesz pluginu Vault, pluginu z permisjami (np. [LuckPerms](https://luckperms.net) oraz pluginu EssentialsXChat wraz z [EssentialsX](https://essentialsx.net).
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


W tym celu potrzebujesz pluginów [WorldEdit](https://dev.bukkit.org/projects/worldedit) oraz [WorldGuard](https://dev.bukkit.org/projects/worldguard).
Wpisujemy komendę `//wand` i zaznaczamy teren. Następnie patrzymy się w dół i wpisujemy komendę `//expand 100 100`
Potem zostało nam tylko zdefiniowanie regionu komendą `/rg define <nazwa_regionu>`
Nasz region jest już zabezpieczony, jednak z pewnością chcielibyśmy modyfikować jego ustawienia, wystarczy wpisać komendę `/rg flags <region>` i wyświetli nam się interaktywna wiadomość na czacie, w której możemy ustawiać tzw. flagi dla naszego regionu.


8. BungeeCord

8.1 Omówienie.

BungeeCord to tzw. proxy, które pozwala nam na szybkie przełączanie się pomiędzy serwerami. Można to wykorzystać np. do zrobienia wielu trybów na serwerze.

8.2 Instalacja BungeeCorda.

Jako silnika proxy użyjemy [Velocity](https://velocitypowered.com/downloads). Jest to jeden z najlepszych darmowych silników proxy, który jest w stanie zapewnić nam wysoki poziom wydajności oraz bezpieczeństwa. 

Tworzymy nowy folder, przeznaczony na serwer Proxy. 

`cd /home/`

`mkdir bungeecord`

Teraz pobieramy nasz silnik do stworzonego wcześniej folderu.

`wget https://versions.velocitypowered.com/download/1.1.5.jar`

Zmieniamy nazwę pliku na bardziej przyjazną, np. `velocity.jar`

8.3 Utworzenie skryptu startowego

W przypadku proxy skrypt wygląda identycznie jak w przypadku innych silników. Po prostu tworzymy plik, np. bungeecord.sh

`touch bungeecord.sh`

`nano start.sh`

Wpisujemy poniższy kod:

```
screen -dmS s java -Xms512M -Xmx512M -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true -jar velocity.jar nogui
```

I zapisujemy skrótem `CTRL+X`, następnie klikamy `ENTER`.

Następnie odpalamy bungeecorda poprzez wpisanie komendy `./bungeecord.sh`, `screen -r s` (lub inną, zależy od nazwy waszego pliku)

Dajemy teraz Velocity czas na przygotowanie wszystkich plików, następnie wyłączamy serwer komendą `stop` lub `end` o ile się nie mylę.

8.4 Konfiguracja 

Jeżeli wolisz poradniki w formie filmu lub bardziej rozwiniętej dokumentacji, zapraszam do [tego](https://www.youtube.com/watch?v=frwNn1eVQtg) poradniku lub na [oficjalną wiki SpigotMC](https://www.spigotmc.org/wiki/bungeecord-configuration-guide/)


Otwieramy plik `config.yml`

Interesować będą nas tylko wartości:

`permissions` - miejsce w którym dodajemy permisje dla rang w BungeeCord. Domyślnie stworzone rangi to default oraz admin.

`query-port` - port naszego serwera Bungee. Domyślnie jest on ustawiony na 25577, jednak jeżeli masz inny serwer na tej samej maszynie pod tym portem, zmień to.

`host` - zostawiamy tą wartość na `0.0.0.0`, jednak port (cyfry po dwukropku) zmieniamy na taki sam jak w `query-port`

`player_limit` - liczba slotów serwera. Więcej graczy niż ustawiona wartość nie wejdzie. Jeżeli chcemy wyłączyć, wpisujemy `-1`

`motd` - wiadomość na liście serwerów MultiPlayer oraz query. Możemy używać [formatowania tekstu](https://htmlcolorcodes.com/minecraft-color-codes/) ze znakiem `&`

`max_players` - liczba slotów serwera wyświetlana na MOTD serwera bungee. Może się różnić od wartości `player_limit`

`online-mode` - taka sama funkcja jak w przypadku standardowych serwerów Spigot. Jeżeli jest to włączone, tylko gracze premium mogą wejść na serwer.

`priorities` - priorytet w wejściu na serwery podrzędne. Powiedzmy że mamy serwery Lobby oraz Survival. Po wejściu chcemy być przekierowani na Lobby, więc wpisujemy:


```
priorities:
- lobby
- survival
```

Takie ustawienie sprawi, że gdy serwer Lobby padnie z jakiejkolwiek przyczyny (np. z powodu crashu), BungeeCord przekierowuje graczy bezpośrednio na serwer Survival.

`servers` - najważniejsza część w konfiguracji. Dzieli się ona na zakładki:

```
nazwa_serwera:
  address: mojserwer.pl
  restricted: false
  motd: '&5Moje MOTD serwera`
```

Przypuśćmy, że chcę dodać serwer Lobby. W tej sytuacji wpisuję:

```
lobby:
  address: 127.0.0.1:25565 #Adres numeryczny mojego serwera Lobby. Jeżeli jest on na tej samej maszynie, możemy wpisać 127.0.0.1:PORT, lub localhost:PORT
  restricted: false #Tutaj ustawiamy, czy serwer ma być dla osób ze specjalnymi uprawnieniami. Jeżeli tak, ustawiamy wartość na true
  motd: '&5Moje MOTD serwera` #Tutaj wpisujemy MOTD serwera podrzędnego. Na 99% ta funkcja nie będzie nas interesować, ponieważ na liście serwerów widzimy MOTD Bungee, a nie MOTD Serwera podrzędnego.
  ```
  
  

8.5 Konfiguracja Spigota


To jeszcze nie wszystko. W naszym serwerze podrzędnym musimy jeszcze zmienić parę rzeczy.

Przechodzimy do katalogu serwera podrzędnego np. `cd/home/minecraft`, w zależności od ustawionej nazwy folderu.

Przechodzimy do pliku `spigot.yml`

Ustawiamy wartość `bungeecord` na `true`

Zapisujemy i przechodzimy do pliku `server.properties`

Ustawiamy wartość `online-mode` na false.

Uruchamiamy serwer Spigot oraz serwer bungee, łączymy się z serwerem Bungee i... gotowe!!! Powinniśmy być w tym momencie na wybranym przez nas serwerze podrzędnym. Możemy się przełączyć na inny serwer (o ile taki dodaliśmy) komendą `/server`


9. Certyfikat SSL.

Certyfikat SSL to certyfikat nadawany przez odpowiednie urzędy, tzw. rooty, aby uruchomić połączenia HTTPS dla serwera dla domeny. Jednym z takich rootów, jest [LetsEncrypt](https://letsencrypt.org), który pozwala nam na nadanie takiego certyfikatu dla naszej domeny zupełnie za darmo, przy użyciu klienta ACME. Jednym z takich klientów jest [CertBot](https://certbot.eff.org), którego użyjemy.


9.1 Instalacja CertBota


Instrukcje dotyczące instalacji można znaleźć [tutaj](https://certbot.eff.org/instructions)
Do instalacji wymagany jest tzw. shell access, czyli dostęp SSH do VPSA.
W zależności od tego, jaki system posiadamy, instrukcje są podane na powyższej stronie. W pewnym momencie może wyskoczyć pole do wprowadzenia e-maila, wtedy go więc wpisujemy. Jeżeli podczas wpisania komendy `certbot --nginx` lub `certbot --apache`, w zależności od oprogramowania wyskoczy wam, że konfiguracja nieznaleziona, podajcie domenę oraz potem powinno wyskoczyć wam pole tekstowe, aby wpisać adres e-mail. 


**UWAGA! Domena musi być podpięta do serwera WWW, który jest na waszym serwerze VPS, w celu weryfikacji domeny**

9.2 Usuwanie certyfikatu

Usuwanie certyfikatu jest proste.

Wpisujemy komendę `certbot revoke --cert-name example.com`

Aby przywrócić certyfikat ponownie, po prostu uruchamiamy CertBota ponownie.
