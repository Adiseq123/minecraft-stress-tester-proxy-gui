# 🌐 Minecraft Server Stress Tester GUI (Proxy Support)

<img width="1919" height="1034" alt="image" src="https://github.com/user-attachments/assets/16409741-9221-4f79-b6b0-b5f1f176953a" />

Zaawansowana aplikacja desktopowa zbudowana na bazie **Electron** oraz **Mineflayer**, przeznaczona do testowania wydajności, obciążenia (**stress-test**) oraz stabilności serwerów Minecraft z obsługą połączeń przez **SOCKS5 Proxy**.

![Electron](https://img.shields.io/badge/Electron-30.x-4B8BF5?style=flat&logo=electron)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?style=flat&logo=node.js)
![Mineflayer](https://img.shields.io/badge/Mineflayer-4.20.0-green)
![SOCKS5](https://img.shields.io/badge/Proxy-SOCKS5-orange)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux-blue)

---

## 🖥️ Interfejs GUI

Aplikacja posiada nowoczesny interfejs w ciemnym motywie, który pozwala na wygodne zarządzanie botami oraz konfiguracją testu bez konieczności edytowania plików `.js`.

### Najważniejsze funkcje

- 🌑 **Nowoczesny Dark Theme** — czytelny panel sterowania.
- ⚙️ **Konfiguracja w czasie rzeczywistym** — zmiana:
  - adresu IP serwera,
  - portu,
  - wersji Minecraft,
  - liczby botów,
  - haseł,
  - opóźnień,
  - ustawień proxy.
- 📋 **Kolorowana konsola logów** — podgląd wydarzeń w czasie rzeczywistym:
  - 🟢 `[+]` — pomyślne zalogowanie,
  - 🔵 `[i]` — działania autoryzacyjne,
  - 🟡 `[!]` — wyrzucenie z serwera / AntiBot,
  - 🟠 `[-]` — rozłączenie i oczekiwanie na reconnect,
  - 🔴 `[X]` — błędy połączenia lub proxy.
- 💬 **Customowe wiadomości i komendy** — możliwość definiowania wiadomości oraz komend wysyłanych przez boty.

---

## 🌟 Obsługa SOCKS5 Proxy

Najważniejszym dodatkiem tej wersji jest możliwość nawiązywania połączeń z serwerem Minecraft za pośrednictwem serwerów **SOCKS5 Proxy**.

### 📥 Automatyczne pobieranie proxy

Jeżeli w katalogu aplikacji nie znajduje się plik `proxies.txt`, program może automatycznie pobrać listę publicznych serwerów SOCKS5 z **ProxyScrape**.

Pozwala to rozpocząć test bez konieczności ręcznego przygotowywania listy proxy.

### 📄 Własny plik `proxies.txt`

Program obsługuje również własną listę serwerów proxy.

Plik:

```text
proxies.txt
```

powinien znajdować się w tym samym katalogu co aplikacja.

Obsługiwane formaty:

```text
IP:PORT
```

lub:

```text
IP:PORT:USER:PASS
```

Przykład:

```text
123.45.67.89:1080
98.76.54.32:1080:login:haslo
```

Dzięki temu możliwe jest korzystanie zarówno z proxy bez autoryzacji, jak i serwerów wymagających loginu oraz hasła.

### 🔄 Automatyczna rotacja proxy

W przypadku problemów z połączeniem program może automatycznie przejść do kolejnego serwera proxy z listy.

Jeżeli wybrane proxy nie odpowiada w określonym czasie, zostaje uznane za niedostępne, a bot próbuje nawiązać połączenie przy użyciu kolejnego adresu.

---

## 🤖 Funkcje Botów — Mineflayer

### Masowe testowanie

Obsługa wielu botów jednocześnie z możliwością stopniowego dołączania do serwera poprzez parametr:

```text
spawnDelayMs
```

Pozwala to kontrolować tempo nawiązywania kolejnych połączeń.

### 🎮 Emulacja zachowania gracza

Boty mogą wykonywać podstawowe czynności imitujące zachowanie prawdziwych graczy:

- chodzenie,
- kucanie,
- skakanie,
- sprint,
- machanie ręką,
- losowe rozglądanie się w przestrzeni 3D,
- losowe aktywności,
- opóźnienia podczas wykonywania określonych czynności.

Parametr:

```text
humanTypingDelay
```

umożliwia dodanie opóźnienia podczas symulowania wpisywania tekstu.

### 🔐 Automatyczna autoryzacja

Boty mogą automatycznie reagować na komunikaty serwera związane z rejestracją i logowaniem.

Po wykryciu odpowiednich komunikatów mogą zostać wysłane komendy:

```text
/register
/login
```

z wykorzystaniem skonfigurowanego hasła oraz opóźnienia imitującego wpisywanie tekstu.

### 💬 Aktywność na czacie

Boty mogą okresowo wysyłać skonfigurowane wiadomości lub wykonywać komendy, np.:

```text
/help
/ping
```

Wiadomości mogą zawierać losowy identyfikator pozwalający odróżnić aktywność poszczególnych botów.

### 🔄 Smart Auto-Reconnect

W przypadku rozłączenia bot automatycznie próbuje ponownie połączyć się z serwerem.

Jeżeli problem wynika z rate-limitów lub ograniczeń połączeń, program może odpowiednio wydłużyć czas oczekiwania przed kolejną próbą.

---

## ⚠️ Ważne informacje dotyczące proxy

> **UWAGA:** Korzystanie z publicznych serwerów SOCKS5 nie gwarantuje stabilnego ani szybkiego połączenia.

Darmowe proxy są często:

- przeciążone,
- niestabilne,
- wolne,
- niedostępne,
- niekompatybilne z połączeniami Minecraft.

W rezultacie część proxy może nie przejść handshake'u z serwerem lub może rozłączać boty z powodu timeoutów.

Serwery Minecraft mogą również posiadać zabezpieczenia takie jak **AntiBot, Anti-VPN, rate-limit** oraz inne mechanizmy ograniczające nietypowy ruch.

### Zalecane zastosowanie

Program jest przeznaczony do testowania:

- własnych serwerów Minecraft,
- środowisk lokalnych,
- serwerów testowych,
- infrastruktury, do której użytkownik posiada odpowiednie uprawnienia.

> **Nie używaj programu do obciążania lub zakłócania działania serwerów osób trzecich bez ich zgody.**

---

## 📥 Pobieranie

Gotową wersję programu dla systemu Windows (`.exe`) można pobrać z zakładki **[Releases](../../releases)**.

---

## 🛠️ Instrukcja dla deweloperów

### Wymagania

- [Node.js](https://nodejs.org/) **18 lub nowszy**

### Uruchomienie z kodu źródłowego

#### 1. Sklonuj repozytorium

```bash
git clone https://github.com/TWOJ_NICK/minecraft-stress-tester-proxy.git
cd minecraft-stress-tester-proxy
```

#### 2. Zainstaluj zależności

```bash
npm install
```

#### 3. Uruchom aplikację

```bash
npm start
```

---

## 📦 Budowanie aplikacji

Gotowe pliki zostaną wygenerowane w folderze:

```text
dist/
```

### Windows — `.exe`

```bash
npm run dist:win
```

### Linux — `.AppImage` / archiwum

```bash
npm run dist:linux
```

---

## 🧩 Technologie

- **Electron** — aplikacja desktopowa i interfejs GUI,
- **Node.js** — środowisko uruchomieniowe,
- **Mineflayer** — obsługa botów Minecraft,
- **SOCKS5** — obsługa połączeń przez serwery proxy,
- **ProxyScrape** — źródło publicznych serwerów SOCKS5.

---

## ⚖️ Licencja i zastrzeżenie

Projekt został stworzony **wyłącznie w celach edukacyjnych oraz do autoryzowanych testów wydajnościowych, obciążeniowych i stabilności własnych serwerów Minecraft**.

Użytkownik jest odpowiedzialny za sposób wykorzystania programu oraz za posiadanie odpowiednich uprawnień do przeprowadzania testów.

Autor nie ponosi odpowiedzialności za niewłaściwe wykorzystanie programu.
