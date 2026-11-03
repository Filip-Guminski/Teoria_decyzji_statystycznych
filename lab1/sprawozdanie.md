# LINK DO REPOZYTORIUM: https://github.com/Filip-Guminski/Teoria_decyzji_statystycznych/tree/main

**LINK DO RAPORTU KOŃCOWEGO:** https://github.com/Filip-Guminski/Teoria_decyzji_statystycznych/blob/main/lab1/exercise-summary.json

> **Antigravity · Gemini 4 Argon · Medium**

---

## Pytania:

### 1. Jaki wynik zlecono, jakie zmiany były dozwolone i o jakie informacje do odbioru poproszono agenta?

Agent AI najwidoczniej z pliku `Zadanie.md` sam odczytał pożądany wynik, dopuszczalne zmiany, i informacje które powinienem otrzymać, na dole treść tego co zaproponował, co było zgodne z zadaniem, co zaakceptowałem.

* **Wynik:** Wygenerowanie raportu dla pliku `data/exercise.csv` i zapisanie go w `results/exercise-summary.json` (wewnątrz folderu `project/`).
* **Granice:** W Etapie 1 nie wprowadzamy żadnych zmian w kodzie (`describe_data.py`), danych (`data/exercise.csv`) ani w testach (`tests/test_report.py`). Dopiero w Etapie 2 zmienimy jedną etykietę w `data/exercise.csv` i odświeżymy raport.
* **Odbiór:** Po wykonaniu mam:
  * Wskazać miejsce zapisu raportu i odczytać jego pełną treść.
  * Pokazać użyte dane wejściowe, dokładne wykonane polecenie, narzędzie oraz wynik procesu (wraz z kodem wyjścia i środowiskiem uruchomienia).
  * Uruchomić gotowy test (`python -m unittest discover -s tests -v`), wyjaśnić używane przez niego dane i oczekiwania oraz podać jego wynik.
  * Zgłosić ewentualne niewykonane kroki lub błędy.

---

### 2. Jak powstał raport? Wskaż wejście, polecenie, narzędzie, środowisko wykonania i wynik procesu. Dodaj link do końcowego raportu i wyjaśnij jego liczebności.

* **Użyte narzędzie i podział ról:** Model wybrał polecenie i wywołał narzędzie terminalowe (`run_command`) → aplikacja Antigravity uruchomiła proces w lokalnej powłoce PowerShell → Twój komputer wykonał skrypt za pomocą lokalnego interpretera Pythona → kod wyjścia (`0`) i strumień wyjścia wróciły do modelu.
* **Środowisko wykonania:** Twój lokalny komputer, katalog roboczy `C:\Filip\CLC\lab-1-project\project`, interpreter `C:\Users\arekg\AppData\Local\Programs\Python\Python313\python.exe` (Python 3.13.9).
* **Użyte dane wejściowe:** `data/exercise.csv`
* **Wykonane polecenie:**
```powershell
python describe_data.py --data data/exercise.csv --out results/exercise-summary.json
```
* **Kod wyjścia:** `0`

**Wynik procesu (stdout) (za pierwszym razem):**
```text
Report saved: C:\Filip\CLC\lab-1-project\project\results\exercise-summary.json
Messages: 8; labels: {'ham': 5, 'spam': 3}
```

**Wynik procesu (stdout) (za drugim razem):**
```text
Report saved: C:\Filip\CLC\lab-1-project\project\results\exercise-summary.json
Messages: 8; labels: {'ham': 4, 'spam': 4}
```

* `Messages: 8` - 8 wiadomości/maili
* `ham: 4` - 4 wiadomości zaklasyfikowane pozytywnie
* `spam: 4` - 4 wiadomości zaklasyfikowane jako spam

Zmieniło się z `ham` 5 na 4 oraz z `spam` z 3 na 4, ponieważ zmieniliśmy etykietę pierwszej wiadomości z `ham` na `spam`

**LINK DO RAPORTU KOŃCOWEGO:** https://github.com/Filip-Guminski/Teoria_decyzji_statystycznych/blob/main/lab1/exercise-summary.json

---

### 3. Który fragment dokumentacji lub kodu wyjaśniłeś? Podaj plik i miejsce, własne wyjaśnienie oraz mały przypadek: przewidywanie, sposób sprawdzenia i wniosek.

**Wyjaśniany fragment dokumentacji `README.md`:**
> One CSV record represents one email. The text field contains its subject and full body, which can span multiple lines. Counting physical lines in the CSV does not count messages. spam means unwanted email; ham means legitimate email according to the dataset label. The identifier links a record to its original message.
>
> Inspect one message to understand the fields. You do not need to understand the technical discussions inside the emails or decide whether their labels are correct. Manually counting all labels is optional; the main task is to run the program and trace the saved result to its execution.

**Moje wyjaśnienie:**
instrukcja mówiąca o tym jak wygląda struktura danych, które będziemy klasyfikować, jest tam między innymi informacja że jeden mail to jeden rekord, jeden mail może mieć wiele linijek, istnieją tam tagi takie jak `spam` i `ham`. Nie muszę rozumieć jaka jest zawartośc maili bo to nie jest celem ćwiczenia

**Mały przypadek zadania (przykładowy plik CSV):**
```csv
message_id,text,label
msg-01,"Subject: Spotkanie
Czesc,
widzimy sie jutro o 10:00.",ham
msg-02,"Subject: Wygrana!
Kliknij tutaj, aby odebrac nagrode.",spam
```

**Przewidywanie:**
```text
Messages: 2; labels: {'ham': 1, 'spam': 1}
```

**Sposób sprawdzenia:**
Przeczytanie części i zrozumienie skryptu `describe_data.py`, dodatkowo wyjaśnienie działania poprzez Agenta AI.

**Wnioski:**
Skrypt zlicza wiadomości oraz ilość wystąpień danego labela.

---

### 4. Jak uruchomiono gotowy test, jaki był wynik i czego dotyczyło sprawdzenie?

**Wykonane polecenie:**
```powershell
python -m unittest discover -s tests -v
```

**Kod wyjścia:** `0`

**Wynik procesu:**
```text
test_cli_writes_expected_counts (test_report.ReportTest.test_cli_writes_expected_counts)
The CLI saves a report for the intended input with counts 3 / 2 / 1. ... ok

---

Ran 1 test in 0.115s
OK
```

Test dotyczył wykonania na małym zbiorze (`messages.csv`) skrypt `describe_data.py`.
Sprawdzane dotyczy tego czy proces kończy się kodem `0`, czy plik raportu zostaje utworzony, czy ścieżka `input_file` się zgadza, czy wyniki skryptu są prawidłowe.

---

### 5. Jaką etykietę zmieniono w etapie 2? Jakiej zmiany liczebności oczekiwałeś, jakie operacje wybrałeś i dlaczego? Porównaj wynik przed zmianą i po nowym wykonaniu.

Zmieniono etykietę `ham` na `spam` w pierwszej wiadomości, spodziewałem się zmiany z `ham` 5 na 4 oraz z `spam` z 3 na 4.
Operacje to uruchomienie jeszcze raz skryptu, aby nadpisał się raport.

**Wynik procesu (stdout) (za pierwszym razem):**
```text
Report saved: C:\Filip\CLC\lab-1-project\project\results\exercise-summary.json
Messages: 8; labels: {'ham': 5, 'spam': 3}
```

**Wynik procesu (stdout) (za drugim razem):**
```text
Report saved: C:\Filip\CLC\lab-1-project\project\results\exercise-summary.json
Messages: 8; labels: {'ham': 4, 'spam': 4}
```

* `Messages: 8` - 8 wiadomości/maili
* `ham: 4` - 4 wiadomości zaklasyfikowane pozytywnie
* `spam: 4` - 4 wiadomości zaklasyfikowane jako spam

Zmieniło się z `ham` 5 na 4 oraz z `spam` z 3 na 4, ponieważ zmieniliśmy etykietę pierwszej wiadomości z `ham` na `spam`
