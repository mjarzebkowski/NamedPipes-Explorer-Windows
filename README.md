# NamedPipes-Explorer-Windows

Engish version [here](./README_EN.md)

# Co to za program ? 

To narzędzie ma za zadanie ułatwić prace z Named Pipes w systemie Windows. Jest to wrapper programu konsolowego [PipeList](https://learn.microsoft.com/en-us/sysinternals/downloads/pipelist), z pakietu [Sysinteranls](https://learn.microsoft.com/en-us/sysinternals/). Stworzonym w języku Julia. Wykorzystuje biblioteję Blink i Powershell.

# Jak uruchomić program ? 

Tu jest link do pobierania: [link]()

Dodatkowo będziesz potrzebować Powershell; Wersja dostarczana z systemem całkowicie wystarczy.

I oczywiście: [PipeList](https://learn.microsoft.com/en-us/sysinternals/downloads/pipelist)

Domyśnie zakładam, że jest w zarejestrowany jako ścieżka systemowa,, ale można też go dodać w pliku config.yaml

# Dlaczego powstało ?

Ponieważ nie znalazłem odpowiedniego narzędzia ułatwiającego pracę z named-pipes. Zależało mi na narzędziu graficznym i darmowym.

# Co to named pipes ? 

Named Pipes to jedna z technik komunikacji międzyprocesowej (IPC, Inter-Process Communication) dostępna w systemach operacyjnych Windows. Umożliwiają procesom (nawet na różnych maszynach) wymianę danych w sposób bezpieczny i wydajny. W odróżnieniu od Anonymous Pipes (nieskojarzonych z żadnym nazwanym obiektem), Named Pipes mają unikalne nazwy, które umożliwiają procesom łatwe odnajdywanie i łączenie się ze sobą.

Jak działają Named Pipes?

Named Pipes mogą być używane w scenariuszach komunikacji:

- lokalnej (między procesami działającymi na tym samym komputerze),
- sieciowej (między procesami działającymi na różnych komputerach w sieci).

Każdy Named Pipe jest reprezentowany jako zasób w systemie plików z unikalną nazwą, np.:

pwsh

    \\.\pipe\nazwa_pipe

Named Pipes działają na zasadzie mechanizmu klient-serwer, gdzie jeden proces pełni rolę serwera (tworzy i nasłuchuje na pipe), a drugi proces rolę klienta (łączy się i wysyła/odbiera dane).
Zasady działania:

- Tworzenie: Serwer tworzy Named Pipe i nadaje mu nazwę.
- Nasłuchiwanie: Serwer czeka, aż klient się połączy.
- Połączenie: Klient otwiera pipe i łączy się z serwerem.
- Komunikacja: Dane mogą być przesyłane w obu kierunkach – dwukierunkowo (Full Duplex) lub jednokierunkowo (Half Duplex).
- Zamknięcie: Gdy dane zostaną przetworzone, obie strony zamykają swoje połączenia.

### Zalety Named Pipes

- Wsparcie dwukierunkowej komunikacji: Umożliwiają wymianę danych w obu kierunkach (czyli zarówno serwer, jak i klient mogą wysyłać dane jednocześnie).
- Niezależność od procesów: Procesy, które komunikują się za pomocą Named Pipes, mogą być niezależne od siebie. Nie muszą być procesami rodzic-dziecko.
- Wielowątkowość: Named Pipes wspierają wiele równoczesnych połączeń, co pozwala na jednoczesną obsługę wielu klientów.
- Kompatybilność sieciowa: Umożliwiają łatwą komunikację między procesami działającymi na różnych komputerach w sieci, co jest istotne w aplikacjach rozproszonych.
- Bezpieczeństwo: Windows implementuje Named Pipes z wbudowanymi mechanizmami kontroli dostępu (ACL – Access Control List), co pozwala zabezpieczyć dostęp do nich i zdefiniować, które procesy mogą korzystać z danej rury.
- Obsługa strumieniowa: Named Pipes obsługują strumienie danych (tzw. byte stream), co pozwala na przesyłanie różnorodnych danych (w tym binarnych i tekstowych).

### Szybkość i wydajność Named Pipes

Named Pipes w systemie Windows są uznawane za jedną z najwydajniejszych form komunikacji międzyprocesowej. W kontekście komunikacji na tym samym komputerze działają bardzo szybko, ponieważ system operacyjny może zarządzać buforowaniem i przesyłaniem danych bez udziału sieci i dysków, co minimalizuje opóźnienia.
Czynniki wpływające na wydajność:

- Lokalizacja procesów: Jeśli oba procesy działają na tej samej maszynie, Named Pipes mają podobną wydajność jak pamięć współdzielona, ponieważ system operacyjny może buforować dane bez używania stosów sieciowych.
- Buforowanie: Windows automatycznie buforuje dane w Named Pipes, co minimalizuje opóźnienia w przesyłaniu małych fragmentów danych.
- Użycie sieci: Jeśli Named Pipes są używane w scenariuszach sieciowych, wydajność zależy od przepustowości i opóźnień sieci, choć nadal zapewniają one prostotę i łatwość konfiguracji.

W porównaniu z innymi metodami IPC, takimi jak gniazda (sockets), Named Pipes są zazwyczaj szybsze w scenariuszach lokalnych, ale w scenariuszach sieciowych mogą ustępować gniazdom TCP, które są bardziej zoptymalizowane do długodystansowej komunikacji.
Zastosowania Named Pipes

- Aplikacje serwer-klient: W scenariuszach, gdzie serwer musi obsługiwać wielu klientów jednocześnie (np. serwery plików, serwery baz danych).
- Komunikacja między usługami: W aplikacjach, gdzie różne usługi muszą ze sobą komunikować (np. usługi systemowe Windows).
- Aplikacje sieciowe: Named Pipes mogą być używane do wymiany danych między aplikacjami działającymi na różnych maszynach w sieci, co ułatwia tworzenie aplikacji rozproszonych.