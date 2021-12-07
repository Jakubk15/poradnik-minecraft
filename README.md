### 1. Podstawy



### 1.1 Instalacja serwera Minecraft na VPS.

> Na współdzielonych hostingach serwerów Minecraft wszystko masz gotowe do gry, jednak na serwerze VPS lub DEDYKU musisz wszystko przygotować sam. I co wtedy?

> Pierwszym krokiem jest zainstalowanie programów [WinSCP](https://winscp.net/eng/download.php) lub [Bitvise](https://www.bitvise.com/download-arealub) oraz [PuTTY](https://www.putty.org/).

> Następnie aby połączyć się z konsolą przez PuTTY, połącz się adresem IP twojego VPSa i zaloguj danymi:

 - `Nazwa użytkownika` - zazwyczaj root
 - `hasło` - znajdziesz je w panelu lub na skrzynce mailowej (zależnie od dostawcy VPS)

> Do WinSCP łączysz się podobnie, pamiętaj o protokole SFTP i porcie 22 przykład znajdziesz poniżej
> 
> <img src = "https://i.imgur.com/zOOoVMt.png">

> W przypadku macOS zalecamy program [FileZilla](https://filezilla-project.org) do połączeń FTP, oraz wbudowanego klienta SSH do łączenia się z serwerem VPS.
> Aby połączyć się wystarczy wpisać komendę `ssh root@<IP_TWOJEGO_VPS>`, następnie system poprosi nas o hasło.


> Następnie musimy stworzyć miejsce, w którym będzie znajdował się nasz serwer MC. Wpisujemy komendy:


```linux
cd /home
mkdir mc 
```

> Aby zainstalować silnik, najpierw należy go pobrać.
> Dla przykładu paper, pobieramy go ze strony [PaperMC](https://papermc.io/downloads). Zainstalowany silnik wrzuć do folderu `home/mc`.


> Zmieniamy nazwę silnika serwera na jakąś prostą, pamiętajmy jednak, że musimy zachować format .jar, np. server.jar
> Musimy najpierw zainstalować Javę oraz aplikację `screen`. Jeżeli już ją masz pomiń ten krok.

Aby to zrobić użyj następujących komend

#### Dla Javy 8
```linux
sudo apt-get install openjdk-8-jdk -y
```

#### Dla Javy 11
```linux
sudo apt-get install openjdk-11-jdk -y
```

####  Dla Javy 16
```linux
sudo add-apt-repository ppa:linuxuprising/java -y
sudo apt update
sudo apt-get install oracle-java16-installer
```

#### Dla Javy 17
```linux
sudo add-apt-repository ppa:linuxuprising/java -y
sudo apt update
sudo apt-get install oracle-java16-installer
```

#### Następnie sprawdzamy wersje Javy
```linux
java -version
```

#### Jeżeli wersja javy nam nie odpowiada możemy ją ustawić pod komendą 
```linux 
sudo update-alternatives --config java
```

#### Oraz instalujemy screena
```linux
sudo apt-get install screen -y
```
- ### Przykładowa ścieżka screena ```screen -S NAZWA java -Xmx2048m -jar silnik.jar```

> Jeżeli wyświetli nam się komunikat informujący o obecności Javy, to już prawie gotowe.
> Musimy teraz stworzyć plik uruchamiający serwer. W przypadku Linuxa będzie to start.sh.
> Wrzucamy go do folderu `home/mc` oraz wpisujemy tam następujący kod: **(Są to tylko przykładowe flagi zaczęrpnięte z strony [mcflags](https://mcflags.emc.gs/))**

```
screen -S mc java -Xms10G -Xmx10G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true -jar server.jar nogui -o false
```

**UWAGA!** Wartość `10G` to liczba twojego RAMU serwera! Np. jeżeli chcesz przydzielić 4GB ram, wpisujesz `4G`.

Teraz wpisujemy komendę:
```linux
chmod +x start.sh
```

#### 1.2 Uruchamianie serwera.

W tym celu wpisujemy komendę:
```linux
sh start.sh
```

Teraz powinna nam się ukazać konsola serwera. Jeżeli to nie nastąpi, wpisujemy `screen -ls`. Teraz wyświetli nam się lista naszych screenów wraz z ich nazwami. Następnie wpisujemy:

```linux
screen -d -r NAZWA
```

W razie dodatkowych pytań skontaktuj się z supportem.

### 2. Optymalizacja

Support Team zaleca zapoznanie się z tym poradnikiem odnośnie optymalizacji:
*https://github.com/Helios3991/minecraft-optimization*


### 3. Zabezpieczenia:

#### 3.1 Ochrona Anti-Crash

**UWAGA! Jeżeli masz serwer na najnowszej wersji, to nie będziesz potrzebował zabezpieczenia typu Anti-Crash. Paper naprawia w większości znane błędy pozwalające crashować serwer, a każdy nowy naprawia w chwilę.**

> Jeśli korzystasz ze starszej wersji, zainteresuj się pluginem [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-the-ultimate-antiexploit-plugin.62842/).
> Z płatnych AntiCrash polecamy SafeMC który można zakupić na [discordzie](https://discord.gg/vSxAYAtzqv)


#### 3.2 Ochrona Anti-Bot

> Support Team zaleca następujące zabezpieczenia Anti-Bot:

**DARMOWE:**

[2LS AntiBot](https://www.spigotmc.org/resources/2ls-antibot-the-ultimate-antibot-plugin.62847/) (Kompatybilny tylko z bungeecordem)

[EpicGuard](https://www.spigotmc.org/resources/%E2%AD%90-epicguard-protect-your-server-from-bots-more-%E2%AD%90.72369/) (Kompatybilny z bukkitem, bungeecordem i velocity, lecz blokuje o wiele gorzej niż 2ls AntiBot)

[nAntiBot](https://www.nickuc.com/en/details/nantibot) (Kompatybilny z bungeecordem i velocity)

**PŁATNE:**

[BotSentry](https://www.spigotmc.org/resources/%E2%9A%A1-botsentry-%E2%9A%A1-the-only-antibot-resisting-30k-bots-per-second-bungee-spigot-sponge-velocity.55924/) (Kompatybilny z bukkitem, bungeecordem i velocity. Bardzo intuicyjny, z zaawansowanym podglądem na ataki i zarządzaniem)

> Z płatnych AntiBotów polecamy silnik proxy EyfenCord który można zakupić na ich [discordzie](https://discord.gg/d2r9NhwuMf)


### 4. Wybór silników i ich cechy.



Support Team, w celu uzyskania najlepszej wydajności oraz bezpieczeństwa serwera, zaleca użycie następujących silników:

> Silniki na serwery główne:

[PaperMC](https://papermc.io/downloads) - Fork Spigota w celu poprawienia bezpieczeństwa oraz wydajności. (rekomendowany na wersje 1.9-1.14.x)

[Airplane](https://dl.airplane.gg) - Fork Papera w celu uzyskania jeszcze lepszej wydajności. (rekomendowany na wersję 1.16.x)

[Purpur](https://purpur.pl3x.net) - Fork Airplane (a dokładniej fork Papera z patchami Airplane'a) mający na celu umożliwieniu administratorom serwera swobodnej i prostej konfiguracji (rekomendowany na wersje 1.15-1.16.x)

[SportPaper](https://github.com/Electroid/SportPaper) - Fork Papera na wersję 1.8.8 zwiększający wydajność i naprawiający niektóre błędy. (rekomendowany na wersję 1.8.8) 

> Z płatnych wyróżniamy:

[ImanitySpigot](https://www.mc-market.org/resources/10770/)

> Silniki na serwery Proxy:
[Waterfall](https://papermc.io/downloads#Waterfall) - Ulepszony fork Bungeecorda pod wieloma względami

[Velocity](https://velocitypowered.com) - Oddzielny silnik proxy stworzony przez twórcę waterfalla, dwukrotnie od waterfalla wydajniejszy i dużo bezpieczniejszy.

> Z płatnych silników proxy polecamy:

[EyfenCord](https://discord.gg/d2r9NhwuMf)


**UWAGA!
Nigdy, ale to nigdy nie kupuj płatnych silników ze strony Mc-Market! Nie wprowadzają one nic więcej niż darmowe silniki, nie daj się nabrać na ładne gui!
Kilka takich silników:**

SSSpigot - Kod skradziony w 100% z darmowego, szybkiego, ale bardzo niestabilnego silnika Yatopia. W skrócie: płacisz za zniszczenie swojego świata.

MSpigot, FoxSpigot, SternalSpigot i ogólnie wszystkie silniki sprzedawane przez jedną tą samą osobę o nicku Scalebound - Niczym się nie różnią, specjalnie udostępnił aż 8 takich z różną nazwą i róznymi opisami żeby po rozczarowaniu na jednym ofiara zakupiła drugi, zwykłe oszustwo. 

### 5. Konfiguracja Chatu, prefixów.

Aby skonfigurować chat, potrzebujesz pluginu Vault, pluginu z permisjami (najlepiej [LuckPerms](https://luckperms.net) oraz pluginu EssentialsXChat wraz z [EssentialsX](https://essentialsx.net).
Aby zmienić format chatu, musimy wejść w config.yml EssentialsX i poszukać sekcji odpowiadającej za chat. Mamy tam opcję `formats`, w której możemy
zmienić wygląd czatu. Pamiętajmy, aby stworzyć grupę oraz nadać ją sobie w celu sprawdzenia!
`(/lp creategroup <ranga> <waga>, /lp user <nick> parent set <ranga>), /lp group <ranga> meta setprefix "<prefix> "`
W razie dodatkowych pytań skontaktuj się z Support Teamem. 

### 6. Uprawnienia.

Aby dodać/usunąć uprawnienie dla danej rangi, należy użyć następujących komend (plugin LuckPerms):

`/lp group <ranga> permission set <uprawnienie>` (dodawanie)

`/lp group <ranga> permission unset <uprawnienie>` (usuwanie)

Więcej informacji o pluginie LuckPerms znajdziecie pod: https://luckperms.net/wiki/Home

### 7. Spawn

Aby ustawić spawn, potrzebujesz pluginu EssentialsX z dodatkiem EssentialsXSpawn. Możesz go pobrać tutaj: https://essentialsx.net
Następnie, stajemy w miejscu w którym chcemy ustawić spawn i wpisujemy /setspawn [ranga] / *


#### 7.1 Zabezpieczanie spawnu


W tym celu potrzebujesz pluginów [WorldEdit](https://dev.bukkit.org/projects/worldedit) oraz [WorldGuard](https://dev.bukkit.org/projects/worldguard).
Wpisujemy komendę `//wand` i zaznaczamy teren. Następnie wpisujemy komendę `//expand vert`
Potem zostało nam tylko stworzenie regionu komendą `/rg create <nazwa_regionu>`
Nasz region jest już zabezpieczony, jednak z pewnością chcielibyśmy modyfikować jego ustawienia, wystarczy wpisać komendę `/rg flags <region>` i wyświetli nam się interaktywna wiadomość na czacie, w której możemy ustawiać tzw. flagi dla naszego regionu.


### 8. Serwer proxy

#### 8.1 Omówienie.

Serwer proxy pozwala nam na szybkie przełączanie się pomiędzy serwerami. Można to wykorzystać np. do zrobienia wielu trybów na serwerze.

#### 8.2 Instalacja serwera proxy (Velocity).

Jako silnika proxy użyjemy [Velocity](https://velocitypowered.com/downloads). Jest to najlepszy silnik proxy, który jest w stanie zapewnić nam wysoki poziom wydajności oraz bezpieczeństwa. 

Tworzymy nowy folder, przeznaczony na serwer Proxy. 

`cd /home/`

`mkdir proxy`

Teraz pobieramy nasz silnik do stworzonego wcześniej folderu z [oficjalnej strony Velocity](https://velocitypowered.com/downloads).

Zmieniamy nazwę pliku na bardziej przyjazną, np. `velocity.jar`

#### 8.3 Utworzenie skryptu startowego

W przypadku proxy skrypt wygląda podobnie jak w przypadku innych silników. Po prostu tworzymy plik, np. proxy.sh

Wpisujemy poniższy kod:

```
screen -dmS proxy java -Xms512M -Xmx512M -XX:+UseG1GC -XX:G1HeapRegionSize=4M -XX:+UnlockExperimentalVMOptions -XX:+ParallelRefProcEnabled -XX:+AlwaysPreTouch -XX:MaxInlineLevel=15 -jar velocity.jar
```

I zapisujemy skrótem `CTRL+X`, następnie klikamy `ENTER`.

Następnie odpalamy serwer proxy poprzez wpisanie komendy `./proxy.sh`, `screen -r proxy` (lub inną, zależy od nazwy waszego pliku)

Dajemy teraz Velocity czas na przygotowanie wszystkich plików, następnie wyłączamy serwer komendą `shutdown`.

#### 8.4 Konfiguracja 

Jeżeli wolisz bardziej rozwiniętą dokumentację, zapraszam do [oficjalnej dokumentacji Velocity](https://velocitypowered.com/wiki/).

`bind` - Możesz tutaj zmienić port swojego serwera proxy.

`online-mode`- Tryb online, zabezpieczenie Mojanga. Gdy ta opcja jest ustawiona na true, na serwer dołączać mogą jedynie osoby, które legalnie pozyskały grę.

`player-info-forwarding-mode` - Tryb przekazywania informacji z serwera proxy do serwerów Minecraft. Ustaw na "MODERN" jeśli chcesz uniknąć włamań.

`forwarding-secret` - Hasło do wpisania w paper.yml.

`[servers]` - Tutaj możesz dodać swoje serwery.


#### 8.5 Konfiguracja plików serwera Minecraft


To jeszcze nie wszystko. W naszym serwerze podrzędnym musimy jeszcze zmienić parę rzeczy.

Przechodzimy do katalogu serwera podrzędnego np. `cd/home/minecraft`, w zależności od ustawionej nazwy folderu.

Przechodzimy do pliku `paper.yml`

Ustawiamy wartości `velocity-support.enabled` na `true` oraz `velocity-support.secret` na hasło ustawione w configu Velocity (forwarding-secret).

Zapisujemy i przechodzimy do pliku `server.properties`

Ustawiamy wartość `online-mode` na false.

Uruchamiamy serwer Minecraft oraz serwer proxy, łączymy się z serwerem proxy i... gotowe!!! Powinniśmy być w tym momencie na wybranym przez nas serwerze podrzędnym. Możemy się przełączyć na inny serwer (o ile taki dodaliśmy) komendą `/server`


### 9. Certyfikat SSL.

Certyfikat SSL to certyfikat nadawany przez odpowiednie urzędy, tzw. rooty, aby uruchomić połączenia HTTPS dla serwera dla domeny. Jednym z takich rootów, jest [LetsEncrypt](https://letsencrypt.org), który pozwala nam na nadanie takiego certyfikatu dla naszej domeny zupełnie za darmo, przy użyciu klienta ACME. Jednym z takich klientów jest [CertBot](https://certbot.eff.org), którego użyjemy.


### 9.1 Instalacja CertBota


Instrukcje dotyczące instalacji można znaleźć [tutaj](https://certbot.eff.org/instructions)
Do instalacji wymagany jest tzw. shell access, czyli dostęp SSH do VPSA.
W zależności od tego, jaki system posiadamy, instrukcje są podane na powyższej stronie. W pewnym momencie może wyskoczyć pole do wprowadzenia e-maila, wtedy go więc wpisujemy. Jeżeli podczas wpisania komendy `certbot --nginx` lub `certbot --apache`, w zależności od oprogramowania wyskoczy wam, że konfiguracja nieznaleziona, podajcie domenę oraz potem powinno wyskoczyć wam pole tekstowe, aby wpisać adres e-mail. 


**UWAGA! Domena musi być podpięta do serwera WWW, który jest na waszym serwerze VPS, w celu weryfikacji domeny**

### 9.2 Usuwanie certyfikatu

Usuwanie certyfikatu jest proste.

Wpisujemy komendę `certbot revoke --cert-name example.com`

Aby przywrócić certyfikat ponownie, po prostu uruchamiamy CertBota ponownie.





### 10. Instalacja bazy danych + PHP + PHPmyAdmin + Apache2

Na początku zainstalujmy dodatki:

`apt install zip sudo nano wget software-properties-common`
`apt install zip sudo nano wget lsb-release apt-transport-https ca-certificates`

### 10.1 Apache2

Aby zainstalować Apache2, wystarczy wpisać komendy: 

`apt install apache2`
`apt update`


### 10.2 Instalacja MariaDB (szybszy MYSQL)

MariaDB to szybszy MySQL z pełną kompatybilnością. Aby go zainstalować, wpisujemy:

`apt install mariadb-server`

Aby przejść do dalszej instalacji, wpisujemy:

`mysql_secure_installation`


1. Klikamy Enter

2. Klikamy Y i Enter

3. Wpisujemy nasze hasło do bazy danych

4. Potwierdzamy nasze hasło do MariaDB wpisując dokładnie to samo co poprzednio.

5. Klikamy Y i Enter

6. Klikamy Y i Enter

7. Klikamy Y i Enter

8. Klikamy Y i Enter


Tworzenie użytkownika:

Aby stworzyć użytkownika wpisujemy:


`sudo mysql` - Otwieramy konsolę MariaDB



`CREATE USER 'nazwa_użytkownika'@'%' IDENTIFIED BY 'hasło';`


`GRANT ALL PRIVILEGES ON * . * TO 'nazwa_użytkownika'@'%';`


I spłukujemy permisje komendą:


`FLUSH PRIVILEGES;`


oraz wychodzimy z konsoli - `quit`

Teraz wpisujemy komendę:

`sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf`

W linijce `bind-address`, przed nią dajemy znak `#`.

Teraz zapisujemy; CTRL+X i 2x ENTER.

I restartujemy MariaDB.

`sudo systemctl restart mariadb`


### 10.3 PHP

Aby zainstalować repozytoria PHP, wpisujemy te komendy:

```
Dla ubuntu
LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php

Dla Debiana: 
sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/php.list
```

I dodatkowo:

`apt install php7.4 php7.4-cli php7.4-common libapache2-mod-php7.4 php7.4-mysql php7.4-mysql php7.4-dom php7.4-simplexml php7.4-ssh2 php7.4-xml php7.4-xmlreader php7.4-curl php7.4-exif php7.4-ftp php7.4-gd php7.4-iconv php7.4-imagick php7.4-json php7.4-mbstring php7.4-posix php7.4-sockets php7.4-tokenizer php7.4-pdo php7.4-bcmath php7.4-fpm php7.4-zip`

`apt update`

Teraz sprawdzamy czy mamy wersję PHP 7.4: `php -v`

Jeżeli tak, to baza danych już działa.
