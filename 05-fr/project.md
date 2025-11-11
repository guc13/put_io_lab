# System aukcyjny

## Wprowadzenie

Specyfikacja wymagań funkcjonalnych w ramach informatyzacji procesu sprzedaży produktów w oparciu o mechanizm aukcyjny. 

## Procesy biznesowe

---
<a id="bc1"></a>
### BC1: Sprzedaż aukcyjna 

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Opis:** Proces biznesowy opisujący sprzedaż za pomocą mechanizmu aukcyjnego.

**Scenariusz główny:**
1. [Sprzedający](#ac1) wystawia produkt na aukcję. ([UC1](#uc1))
2. [Kupujący](#ac2) oferuje kwotę za produkt wyższą od aktualnie najwyższej oferty. ([UC2](#uc2))
3. [Kupujący](#ac2) wygrywa aukcję ([UC3](#uc3))
4. [Kupujący](#ac2) przekazuje należność Sprzedającemu. ([UC4](#uc4))
5. [Sprzedający](#ac1) wystawia fakturę i przekazuje produkt Kupującemu. ([UC5](#uc5))

**Scenariusze alternatywne:** 

2.A. Oferta Kupującego została przebita, a [Kupujący](#ac2) pragnie przebić aktualnie najwyższą ofertę.
* 2.A.1. Przejdź do kroku 2.

3.A. Czas aukcji upłynął i [Kupujący](#ac2) przegrał aukcję.
* 3.A.1. Koniec przypadku użycia.

---

## Aktorzy

<a id="ac1"></a>
### AC1: Sprzedający

Osoba oferująca towar na aukcji.

<a id="ac2"></a>
### AC2: Kupujący

Osoba chcąca zakupić produkt na aukcji.


## Przypadki użycia poziomu użytkownika

### Aktorzy i ich cele

[Sprzedający](#ac1):
* [UC1](#uc1): Wystawienie produktu na aukcję
* [UC5](#uc5): Wystawienie faktury i przekazanie produktu
* [UC6](#uc6): Anulowanie aukcji


[Kupujący](#ac2):
* [UC2](#uc2): Złożenie oferty
* [UC3](#uc3): Wygranie aukcji
* [UC4](#uc4): Przekazanie należności Sprzedającemu
* [UC7](#uc7): Przegląd aktywnych aukcji
* [UC8](#uc8): Wycofanie oferty


---
<a id="uc1"></a>
### UC1: Wystawienie produktu na aukcję

**Aktorzy:** [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Sprzedający](#ac1) zgłasza do systemu chęć wystawienia produktu na aukcję.
2. System prosi o podanie danych produktu i ceny wywoławczej.
3. [Sprzedający](#ac1) podaje dane produktu oraz cenę wywoławczą.
4. System weryfikuje poprawność danych.
5. System informuje o pomyślnym wystawieniu produktu na aukcję.

**Scenariusze alternatywne:** 

4.A. Podano niepoprawne lub niekompletne dane produktu.
* 4.A.1. System informuje o błędnie podanych danych.
* 4.A.2. Przejdź do kroku 2.

---
<a id="uc2"></a>
### UC2: Złożenie oferty

**Aktorzy:** [Kupujący](#ac2)

**Scenariusz główny:**
1. [Kupujący](#ac2) wybiera aktywną aukcję.
2. System prezentuje aktualną najwyższą ofertę i czas pozostały do zakończenia.
3. [Kupujący](#ac2) wprowadza kwotę oferty wyższą od aktualnej.
4. System weryfikuje poprawność oferty zgodnie z [BR1](#br1).
5. System zapisuje ofertę i aktualizuje najwyższą kwotę.
6. System informuje o pomyślnym złożeniu oferty.

**Scenariusze alternatywne:**

4.A. Oferta jest niższa niż wymagana.
* 4.A.1. System informuje Kupującego o konieczności zwiększenia oferty.
* 4.A.2. Przejdź do kroku 3.

---
<a id="uc3"></a>
### UC3: Wygranie aukcji

**Aktorzy:** [Kupujący](#ac2)

**Scenariusz główny:**
1. System monitoruje czas trwania aukcji.
2. Po upływie czasu system ustala najwyższą ofertę zgodnie z [BR2](#br2).
3. System informuje zwycięskiego [Kupującego](#ac2) o wygraniu aukcji.
4. System udostępnia dane płatności [Sprzedającego](#ac1).
5. Aukcja zostaje oznaczona jako zakończona.

**Scenariusze alternatywne:**

2.A. Brak ofert złożonych przez Kupujących.
* 2.A.1. System oznacza aukcję jako zakończoną bez sprzedaży.
* 2.A.2. Informuje [Sprzedającego](#ac1).

---
<a id="uc4"></a>
### UC4: Przekazanie należności Sprzedającemu

**Aktorzy:** [Kupujący](#ac2), [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Kupujący](#ac2) wybiera opcję zapłaty za wygraną aukcję.
2. System prezentuje dane płatności i kwotę należności.
3. [Kupujący](#ac2) dokonuje płatności za pomocą wybranej metody.
4. System potwierdza otrzymanie płatności.
5. System informuje [Sprzedającego](#ac1) o zaksięgowaniu należności.

**Scenariusze alternatywne:**

3.A. Płatność nieudana.
* 3.A.1. System informuje Kupującego o błędzie transakcji.
* 3.A.2. Kupujący może ponowić próbę zapłaty.

---
<a id="uc5"></a>
### UC5: Wystawienie faktury i przekazanie produktu

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Scenariusz główny:**
1. [Sprzedający](#ac1) potwierdza otrzymanie płatności.
2. System umożliwia wygenerowanie faktury sprzedaży.
3. [Sprzedający](#ac1) uzupełnia dane do faktury.
4. System generuje fakturę w formacie PDF i zapisuje ją w systemie.
5. [Sprzedający](#ac1) oznacza produkt jako wysłany.
6. System powiadamia [Kupującego](#ac2) o wysyłce i udostępnia fakturę.

**Scenariusze alternatywne:**

3.A. Brak wymaganych danych do faktury.
* 3.A.1. System informuje Sprzedającego o brakach.
* 3.A.2. Przejdź do kroku 3.s
---
<a id="uc6"></a>
### UC6: Anulowanie aukcji
**Aktorzy:** [Sprzedający](#ac1)

<a id="uc7"></a>
### UC7: Przegląd aktywnych aukcji
**Aktorzy:** [Kupujący](#ac2)

<a id="uc8"></a>
### UC8: Wycofanie oferty
**Aktorzy:** [Kupujący](#ac2)

---

## Obiekty biznesowe

### BO1: Aukcja

Aukcja jest formą zawierania transakcji kupna-sprzedaży, w której Sprzedający określa cenę wywoławczą produktu, natomiast Kupujący mogą oferować własną ofertę zakupu każdorazowo proponując kwotę wyższą od aktualnie oferowanej kwoty. Aukcja kończy się po upływie określonego czasu. Jeśli złożona została co najmniej jedna oferta zakupu, produkt nabywa ten Kupujący, który zaproponował najwyższą kwotę. 

### BO2: Produkt

Fizyczny lub cyfrowy obiekt, który ma zostać sprzedany w ramach aukcji.

### BO3: Oferta

Propozycja zakupu produktu w określonej aukcji, zawierająca kwotę zaproponowaną przez Kupującego.

## Reguły biznesowe

<a id="br1"></a>
### BR1: Złożenie oferty

Złożenie oferty wymaga zaproponowania kwoty wyższej niż aktualnie oferowana o minimum 1,00 PLN.

<a id="br2"></a>
### BR2: Rozstrzygnięcie aukcji

Aukcję wygrywa ten z [Kupujący](#ac2)ch, który w momencie jej zakończenia (upłynięcia czasu) złożył najwyższą ofertę.

## Macierz CRUDL

| Przypadek użycia                                   | Aukcja | Produkt | Oferta |
| -------------------------------------------------- | ------ | ------- | ------ |
| UC1: Wystawienie produktu na aukcję                | C      | C       |        |
| UC2: Złożenie oferty                               | R      | R       | C      |
| UC3: Wygranie aukcji                               | U      |         | R      |
| UC4: Przekazanie należności Sprzedającemu          | R      |         | R      |
| UC5: Wystawienie faktury i przekazanie produktu    | R      | U       |        |
|                                                    |        |         |        |
| UC6: Anulowanie aukcji                             | D      | D       | D      |
| UC7: Przegląd aktywnych aukcji                     | L      | L       | L      |
| UC8: Wycofanie oferty                              |        |         | D      |