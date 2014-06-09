Podstawowe standardy zapisu kodu
=====================

Ta sekcja standardu zawiera postanowienia, które powinny być uznane za
standardowe praktyki zapisu kodu wymagane do zapewnienia wysokiego technicznego
poziomu współdziałania pomiędzy współdzielonym kodem PHP.

Słowa kluczowe "MUSI" (ang. MUST), "NIE MOŻNA" (ang. MUST NOT), "WYMAGANE"
(ang. REQUIRED), "BĘDZIE" (ang. SHALL), "NIE BĘDZIE" (ang. SHALL NOT), "POWINNO"
(ang. SHOULD), "NIE POWINNO" (ang. SHOULD NOT), "REKOMENDOWANE" (ang. RECOMMENDED),
"MOŻNA" (ang. MAY) i "OPCJONALNE" (ang. OPTIONAL) w tym dokumencie będą
interpretowane jak opisano w [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md


1. Informacje ogólne
-----------

- Pliki MUSZĄ używać tylko tagów `<?php` oraz `<?=`.

- Pliki MUSZĄ używać tylko UTF-8 bez BOM dla kodu PHP.

- Pliki POWINNY *albo* deklarować symbole (klasy, funkcje, stałe itd.)
  *albo* powodować skutki uboczne (np. generować wynik, zmieniać ustawienia .ini
  itd.), ale NIE POWINNY spełniać dwóch funkcji jednocześnie.

- Przestrzenie nazw i klasy MUSZĄ przestrzegać standardów automatycznego
ładowania PSR: [[PSR-0], [PSR-4]].

- Nazwy klas MUSZĄ być zapisane w notacji `StudlyCaps`.

- Sałe w klasach MUSZĄ być zapisane w całości dużymi literami wykorzystując znaki
podkreślenia jako separatory.

- Nazwy metod muszą być zapisane w notacji `camelCase`.


2. Pliki
--------

### 2.1. Tagi PHP

Kod PHP MUSI wykorzystywać długie tagi `<?php ?>` albo skrócone tagi z instrukcją
echo `<?= ?>`. Kod NIE MOŻE wykorzystywać innych kombinacji tagów.

### 2.2. Kodowanie zapisu

Kod PHP MUSI używać tylko UTF-8 bez BOM.

### 2.3. Skutki uboczne

Plik POWINIEN deklarować nowe symbole (klasy, funkcje, stałe itd.) i nie
powodować żadnych innych skutków ubocznych, albo POWINIEN wykonywać instrukcje,
które powodują skutki uboczne, ale NIE POWINIEN spełniać dwóch funkcji
jednocześnie.

Fraza "skutki uboczne" oznacza wykonywanie instrukcji nie powiązanych
bezpośrednio z deklarowaniem klas, funkcji, stałych itd. *, poza powiązaniami
poprzez załadowanie pliku.*

"Skutki uboczne" to między innymi generowanie wyniku, bezpośrednie użycie
`require` bądź `include`, łączenie z zewnętrznymi usługami, modyfikowanie
ustawień ini, wyświetlanie błędów lub wyjątków, modyfikowanie globalnych tudzież
statycznych zmiennych, odczytanie z bądź zapisywanie do pliku itd.

Poniżej jest przykład pliku z deklaracjami i skutkami ubocznymi; przykład czego
należy unikać:

```php
<?php
// skutek uboczny: zmiana ustawień ini
ini_set('error_reporting', E_ALL);

// skutek uboczny: załadowanie pliku
include "file.php";

// skutek uboczny: wygenerowanie wyniku
echo "<html>\n";

// deklaracja
function foo()
{
    // zawartość funkcji
}
```

Poniżej jest przykład pliku który zawiera tylko deklaracje bez skutków ubocznych;
przykład który należy naśladować:

```php
<?php
// deklaracja
function foo()
{
    // zawartość funkcji
}

// deklaracja warunkowa *nie jest* skutkiem ubocznym
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```


3. Przestrzeń nazw i nazwy klas
----------------------------

Przestrzenie nazw i nazwy klas muszą przestrzegać [PSR-0].

Co znaczy, że każda klasa znajduje się w osobnym pliku, oraz że znajduje się w
co najmniej jednopoziomowej przestrzeni nazw głównego dostarczyciela.

Nazwa klasy MUSI być zdeklarowana w `StudlyCaps`.

Kod PHP 5.3 i późniejszy MUSI korzystać z formalnych przestrzeni nazw.

Na przykład:

```php
<?php
// PHP 5.3 i późniejszy:
namespace Vendor\Model;

class Foo
{
}
```

Kod napisany z myślą o wersji 5.2.x i wcześniejszych POWINIEN korzystać z pseudo
przestrzeni nazw w konwencji zawierającej nazwę dostarczyciela w formie
przedrostka `Vendor_` w nazwach klas.

```php
<?php
// PHP 5.2.x i wcześniejszy:
class Vendor_Model_Foo
{
}
```

4. Stałe, właściwości i metody klas
-------------------------------------------

Termin "klasa" odnosi się do wszystkich klas, interfejsów i traitsów (pol.
ścieżek).

### 4.1. Stałe

Nazwy klas MUSZĄ być zdeklarowane dużymi literami ze znakami podkreślenia jako
separatorami. Na przykład:

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. Właściwości

Ten standard intencjonalnie nie rekomenduje żadnej konwencji zapisu nazw
właściwość w formie `$StudlyCaps`, `$camelCase` czy `$under_score`.

Jakakolwiek konwencja nazywania zostanie użyta powinna być wykorzystywana
konsekwentnie w rozsądnym zakresie. Ten zakres może obejmować poziom
dostarczyciela, paczki, klasy bądź metody.


### 4.3. Metody

Nazwa metody musi być zdeklarowana w konwencji `camelCase()`.
