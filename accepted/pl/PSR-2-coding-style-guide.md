Przewodnik po stylu zapisu kodu
==================

Ten przewodnik rozszerza i uzupełnia [PSR-1], podstawowy standard zapisu kodu.

Zamiarem tego przewodnika jest zredukowanie problemów poznawczych podczas
skanowania kodu przez różnych autorów. Robi to poprzez znalezienie wspólnego
zbioru reguł i oczekiwań na temat tego jak formatować kod PHP.

Reguły odnośnie stylu zostały wyprowadzone z elementów wspólnych dla różnych
projektów członkowskich. Jeden zestaw wskazówek jest pomocny kiedy różni autorzy
współpracują nad wieloma projektami. Dlatego korzyści ze stosowania tych
wskazówek nie wynikają z samych reguł, a z ich współdzielenia.


Słowa kluczowe "MUSI" (ang. MUST), "NIE MOŻNA" (ang. MUST NOT), "WYMAGANE"
(ang. REQUIRED), "BĘDZIE" (ang. SHALL), "NIE BĘDZIE" (ang. SHALL NOT), "POWINNO"
(ang. SHOULD), "NIE POWINNO" (ang. SHOULD NOT), "REKOMENDOWANE" (ang. RECOMMENDED),
"MOŻNA" (ang. MAY) i "OPCJONALNE" (ang. OPTIONAL) w tym dokumencie będą
interpretowane jak opisano w [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md


1. Informacje ogólne
-----------

- Kod MUSI przestrzegać "podstawowy standard zapisu kodu" PSR [[PSR-1]].

- Kod MUSI wykorzystywać 4 spacje jako wcięcia, a nie tabulacje.

- NIE MOŻE być twardego limitu długości linii; miękki limit MUSI wynosić 120
  znaków; linia POWINNA składać się z nie więcej niż 80 znaków.

- Po deklaracji `namespace` MUSI nastąpić jedna pusta linia, również po
  deklaracji bloku `use` MUSI nastąpić jedna pusta linia.

- Klamry otwierające dla klas MUSZĄ być zapisane w linii następującej, również
  klamry zamykające muszą być zapisane w linii następującej po zawartości.

- Klamry otwierające dla metod MUSZĄ być zapisane w linii następującej, również
  klamry zamykające muszą być zapisane w lini następującej po zawartości.

- Widoczność MUSI być zdeklarowana dla wszystkich właściwości i metod;
  `abstract` oraz `final` MUSZĄ być zdeklarowane przed widocznością; `static`
  MUSI być zdeklarowany po widoczności.

- Instrukcje sterujące MUSZĄ kończyć się jedną spacją; metody i wywołania
  funkcji NIE MOGĄ kończyć się spacją.

- Klamry otwierające dla instrukcji sterujących MUSZĄ być w tej samej linii,
  klamry zamykające muszą być zapisane w linii następującej po zawartości.

- Nawiasy otwierające dla instrukcji sterujących NIE MOGĄ mieć spacji po sobie,
  również nawiasy zamykające dla instrukcji sterujących NIE MOGĄ mieć spacji
  przed.

### 1.1. Przykład

Niniejszy przykład zbiera niektóre z reguł dla szybkiego przeglądu:

```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

2. Generalnie
----------

### 2.1 Podstawowy standard zapisu kodu

Kod MUSI przestrzegać wszystkie reguły zawarte w [PSR-1].

### 2.2 Pliki

Wszystkie pliki PHP MUSZĄ używać uniksowej karotki LF jako znak końca linii.

Wszystkie pliki PHP MUSZĄ kończyć się jedną pustą linią.

Tag zamykający `?>` MUSI być pominięty w plikach zawierających tylko kod PHP.

### 2.3. Linie

NIE MOŻE być twardego limitu długości linii.

Miękki limit MUSI wynosić 120 znaków; automatyczne korektory kodu MUSZĄ
ostrzegać przy przekroczeniu miękkiego limitu, ale NIE MOGĄ zwracać błędu.

Linie NIE POWINNY być dłuższe niż 80 znaków; linie dłuższe POWINNY być
podzielone na linie nie dłuższe niż 80 znaków każda.

NIE MOŻE być białej spacji na końcu niepustych linii.

Puste linie MOGĄ zostać dodane aby poprawić czytelność i aby wskazywać powiązane
fragmenty kodu.

NIE MOŻE być więcej niż jednej instrukcji w jednej linii.

### 2.4. Wcięcia

Kod MUSI wykorzystywać 4 spacje jako wcięcia, oraz NIE MOŻE wykorzystywać do
tego tabulacji.
> N.b.:  Korzystanie tylko ze spacji, i nie mieszanie spacji z tabulacją pomaga
> unikać problemów z diffami, łatkami, historią i adnotacjami. Wykorzystanie
> spacji czyni łatwiejszym wstawienie dobrze dopasowanych sub-wcięć do
> wyrównania między liniami.

### 2.5. Słowa kluczowe i True/False/Null

[Słowa kluczowe] MUSZĄ być zapisane małymi literami.

Stałe PHP takie jak `true`, `false` oraz `null` MUSZĄ być zapisane małymi
literami.

[Słowa kluczowe]: http://php.net/manual/en/reserved.keywords.php



3. Przestrzenie nazw i deklaracja Use
---------------------------------

Jeśli `namespace` zostało zdeklarowane, po deklaracji MUSI znaleźć się pusta
linia.

Jeśli deklaracje `use` są obecne MUSZĄ nastąpić po zdeklarowaniu `namespace`.

Na jedną deklarację MUSI przypadać jedno słowo kluczowe `use`.

Po bloku `use` MUSI nastąpić jedna pusta linia.

Na przykład:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...

```


4. Klasy właściwości i metody
-----------------------------------

Określenia "klasa" odnosi się do wszystkich klas, interfejsów oraz traitsów.

### 4.1. Extends oraz Implements

Słowa kluczowe `extends` oraz `implements` MUSZĄ zostać zdeklarowane w tej samej
linii co nazwa klasy.

Klamra otwierająca dla klasy musi być w oddzielnej linii; klamra zamykająca musi
nastąpić w osobnej linii po zawartości klasy.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

Lista `implements` MOŻE być rozdzielona na wiele odpowiednio wciętych linii tzn.
pierwszy element w liście MUSI być w linii następującej po `implements` oraz na
jedną linię MUSI przypadać tylko jeden interfejs.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

### 4.2. Właściwości

Widoczność MUSI być zdeklarowana dla wszystkich właściwości.

Słowo kluczowe `var` NIE MOŻE być używane do deklarowania właściwości.

NIE MOŻNA deklarować więcej niż jednej właściwości na instrukcję.

Właściwości NIE POWINNY być poprzedzone przedrostkiem znaku podkreślenia dla
wskazania zakresu widoczności prywatnej, bądź chronionej.

Deklaracja właściwości wygląda następująco:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
```

### 4.3. Metody

Widoczność MUSI być zdeklarowana dla wszystkich metod.

Nazwy metod NIE POWINNY być poprzedzone przedrostkiem znaku podkreślenia dla
wskazania zakresu widoczności prywatnej, bądź chronionej.

Nazwa metody NIE MOŻE być zdeklarowana ze spacją po nazwie metody. Klamra
otwierająca MUSI być zapisana w oddzielnej linii, również klamra zamykająca MUSI
nastąpić w oddzielnej linii po zawartości. Nawiasy otwierające NIE MOGĄ mieć
spacji po sobie, również nawiasy zamykające NIE MOGĄ mieć spacji przed.

Deklaracja metody wygląda następująco. Zauważ rozmieszczenie nawiasów,
przecinków, spacji oraz klamer:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

### 4.4. Argumenty metody

NIE MOŻE być spacji przed każdym przecinkiem w liście argumentów, MUSI BYĆ za to
jedna spacja po każdym przecinku.

Argumenty z wartościami domyślnymi MUSZĄ znaleźć się na końcu listy argumentów.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Lista argumentów MOŻE być rozdzielona pomiędzy odpowiednio wcięte, oddzielne
linie. Pierwszy element w liście MUSI być w linii następującej oraz na
jedną linię MUSI przypadać tylko jeden argument.

Kiedy lista argumentów zostaje rozdzielona pomiędzy oddzielne linie, nawias
zamykający MUSI być umieszczony wraz z klamrą otwierającą w tej samej linii z
jedną spacją pomiędzy.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

### 4.5. `abstract`, `final`, oraz `static`

Jeśli deklaracje `abstract` oraz `final` są obecne MUSZĄ poprzedzać deklaracje
zakresu widoczności.

Jeśli deklaracja `static` jest obecna MUSI nastąpić po deklaracji zakresu
widoczności.

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

### 4.6. Wywoływanie metod i funkcji

W wywołaniu metody lub funkcji, NIE MOŻE być spacji pomiędzy nazwą funkcji lub
metody, a nawiasem otwierającym, NIE MOŻE być spacji również po nawiasie
otwierającym czy przed nawiasem zamykającym. W liście argumentów NIE MOŻE być
spacji przed przecinkami, ale po każdym przecinku MUSI być jedna spacja.

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```
Lista argumentów MOŻE być rozdzielona pomiędzy odpowiednio wcięte, oddzielne
linie. Pierwszy element w liście MUSI być w linii następującej oraz na
jedną linię MUSI przypadać tylko jeden argument.

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

5. Instrukcje
---------------------

Generalne zasady zapisu dla instrukcji są następujące:

- Po słowie kluczowym instrukcji MUSI być jedna spacja
- Przed nawiasem otwierającym NIE MOŻE być spacji
- Przed nawiasem zamykającym NIE MOŻE być spacji
- Pomiędzy nawiasem zamykającym a klamrą otwierającą MUSI być jedna spacja
- Zawartość instrukcji MUSI być wcięta raz
- Klamra zamykająca MUSI być w oddzielnej lini po zawartości.

Zawartość każdej struktury MUSI być zawarta w klamrach. To standaryzuje wygląd
instrukcji oraz redukuje szanse na wprowadzenie błędu poprzez dodawanie nowych
lini do zawartości.


### 5.1. `if`, `elseif`, `else`

Instrukcja `if` wygląda następująco. Zauważ rozmieszczenie nawiasów, spacji oraz
klamer. Zwróć również uwagę na fakt, że `else` i `elseif` znajdują się w tej
samej linii co klamra zamykająca z poprzedniej zawartości.

```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```
Słowo kluczowe `elseif` POWINNO być używane zamiast `elseif` tak aby wszystkie
instrukcje wyglądały jak pojedyncze słowa.


### 5.2. `switch`, `case`

Instrukcja `switch` wygląda następująco. Zauważ rozmieszczenie nawiasów, spacji
oraz klamer. Instrukcja `case` MUSI być wcięta raz od instrukcji `switch`.
Zawartość instrukcji `case` wraz ze słowem kluczowym `brake` (albo innym
kończącym słowem kluczowym) MUSI być wcięta raz od instrukcji `case`. Jeśli
przejście w niepustej zawartości `case` jest intencjonalne MUSI być dodany
komentarz typu `// no break`.

```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```


### 5.3. `while`, `do while`

Instrukcja `while` wygląda następująco. Zauważ rozmieszczenie nawiasów, spacji
oraz klamer.

```php
<?php
while ($expr) {
    // structure body
}
```

Podobnie do poprzedniej instrukcja `do while` wygląda następująco. Zauważ
rozmieszczenie nawiasów, spacji oraz klamer.

```php
<?php
do {
    // structure body;
} while ($expr);
```

### 5.4. `for`

Instrukcja `for` wygląda następująco. Zauważ rozmieszczenie nawiasów, spacji
oraz klamer.

```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

### 5.5. `foreach`

Instrukcja `foreach` wygląda następująco. Zauważ rozmieszczenie nawiasów, spacji
oraz klamer.

```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

### 5.6. `try`, `catch`

Blok `try catch` wygląda następująco. Zauważ rozmieszczenie nawiasów, spacji
oraz klamer.

```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

6. Dommknięcia
-----------

Domknięcia MUSZĄ być deklarowane wraz ze spacją po słowie kluczowym `function`
oraz ze spacją przed i po słowie kluczowym `use`.

Klamra otwierająca MUSI być w tej samej linii, a klamra zamykająca MUSI być w
linii następującej po zawartości.

NIE MOŻE być spacji po nawiasie otwierającym listę argumentów lub listę
zmiennych oraz NIE MOŻE być spacji przed nawiasem zamykającym listę argumentów
lub listę zmiennych.

W liście argumentów oraz liście zmiennych NIE MOŻE być spacji przed przecinkami,
ale MUSI być jedna spacja po każdym przecinku.

Argumenty domknięcia ze zdeklarowanymi wartościami domyślnymi MUSZĄ się znaleźć
na końcu listy.

Deklaracja domknięcia wygląda następująco. Zwróć uwagę na rozmieszczenie
nawiasów, przecinków, spacji oraz klamer:


```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```
Lista argumentów MOŻE być rozdzielona pomiędzy odpowiednio wcięte, oddzielne
linie. Pierwszy element w liście MUSI być w linii następującej oraz na
jedną linię MUSI przypadać tylko jeden argument albo jedna zmienna.

Kiedy lista (argumentów lub zmiennych) zostaje rozdzielona pomiędzy oddzielne
linie, nawias zamykający MUSI być umieszczony wraz z klamrą otwierającą w tej
samej linii z jedną spacją pomiędzy.

Poniżej przedstawiono przykłady domknięć z rozdzielonymi lub nie rozdzielonymi
listami argumentów, tudzież listami zmiennych na wiele linii.

```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```
Zauważ, że te zasady również mają zastosowanie kiedy domknięcie jest
wykorzystane bezpośrednio w funkcji albo w wywołaniu metody jako argument.

```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```


7. Wnionski
--------------

Wiele elementów zapisu kodu zostało intencjonalnie pominięte w tym przewodniku.
Do pominiętych zaliczają się między innymi:

- Deklaracje zmiennych globalnych i stałych globalnych

- Deklaracje funkcji

- Operatory i przypisania

- Wyrównanie między liniami

- Sekcje komentarzy i dokumentacji

- Przedrostki i przyrostki w nazwach klas

- Najlepsze praktyki

Przyszłe rekomendacje MOGĄ zrewidować bądź rozszerzyć ten przewodnik aby
zaadresować te lub inne elementy zapisu kodu.


Dodatek A. Przegląd
------------------

W pisaniu tego przewodnika grupa zrobiła przegląd praktyk projektów
członkowskich aby dobrać wspólne praktyki. Przegląd został niniejszym zachowany
dla potomnych.

### A.1. Survey Data

    url,http://www.horde.org/apps/horde/docs/CODING_STANDARDS,http://pear.php.net/manual/en/standards.php,http://solarphp.com/manual/appendix-standards.style,http://framework.zend.com/manual/en/coding-standard.html,http://symfony.com/doc/2.0/contributing/code/standards.html,http://www.ppi.io/docs/coding-standards.html,https://github.com/ezsystems/ezp-next/wiki/codingstandards,http://book.cakephp.org/2.0/en/contributing/cakephp-coding-conventions.html,https://github.com/UnionOfRAD/lithium/wiki/Spec%3A-Coding,http://drupal.org/coding-standards,http://code.google.com/p/sabredav/,http://area51.phpbb.com/docs/31x/coding-guidelines.html,https://docs.google.com/a/zikula.org/document/edit?authkey=CPCU0Us&hgd=1&id=1fcqb93Sn-hR9c0mkN6m_tyWnmEvoswKBtSc0tKkZmJA,http://www.chisimba.com,n/a,https://github.com/Respect/project-info/blob/master/coding-standards-sample.php,n/a,Object Calisthenics for PHP,http://doc.nette.org/en/coding-standard,http://flow3.typo3.org,https://github.com/propelorm/Propel2/wiki/Coding-Standards,http://developer.joomla.org/coding-standards.html
    voting,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,no,no,no,?,yes,no,yes
    indent_type,4,4,4,4,4,tab,4,tab,tab,2,4,tab,4,4,4,4,4,4,tab,tab,4,tab
    line_length_limit_soft,75,75,75,75,no,85,120,120,80,80,80,no,100,80,80,?,?,120,80,120,no,150
    line_length_limit_hard,85,85,85,85,no,no,no,no,100,?,no,no,no,100,100,?,120,120,no,no,no,no
    class_names,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,lower_under,studly,lower,studly,studly,studly,studly,?,studly,studly,studly
    class_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,next,next,next,next,next,next,same,next,next
    constant_names,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper
    true_false_null,lower,lower,lower,lower,lower,lower,lower,lower,lower,upper,lower,lower,lower,upper,lower,lower,lower,lower,lower,upper,lower,lower
    method_names,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,lower_under,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel
    method_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,same,next,next,next,next,next,same,next,next
    control_brace_line,same,same,same,same,same,same,next,same,same,same,same,next,same,same,next,same,same,same,same,same,same,next
    control_space_after,yes,yes,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes
    always_use_control_braces,yes,yes,yes,yes,yes,yes,no,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes
    else_elseif_line,same,same,same,same,same,same,next,same,same,next,same,next,same,next,next,same,same,same,same,same,same,next
    case_break_indent_from_switch,0/1,0/1,0/1,1/2,1/2,1/2,1/2,1/1,1/1,1/2,1/2,1/1,1/2,1/2,1/2,1/2,1/2,1/2,0/1,1/1,1/2,1/2
    function_space_after,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no
    closing_php_tag_required,no,no,no,no,no,no,no,no,yes,no,no,no,no,yes,no,no,no,no,no,yes,no,no
    line_endings,LF,LF,LF,LF,LF,LF,LF,LF,?,LF,?,LF,LF,LF,LF,?,,LF,?,LF,LF,LF
    static_or_visibility_first,static,?,static,either,either,either,visibility,visibility,visibility,either,static,either,?,visibility,?,?,either,either,visibility,visibility,static,?
    control_space_parens,no,no,no,no,no,no,yes,no,no,no,no,no,no,yes,?,no,no,no,no,no,no,no
    blank_line_after_php,no,no,no,no,yes,no,no,no,no,yes,yes,no,no,yes,?,yes,yes,no,yes,no,yes,no
    class_method_control_brace,next/next/same,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/next,same/same/same,same/same/same,same/same/same,same/same/same,next/next/next,next/next/same,next/same/same,next/next/next,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/same,next/next/next

### A.2. Survey Legend

`indent_type`:
The type of indenting. `tab` = "Use a tab", `2` or `4` = "number of spaces"

`line_length_limit_soft`:
The "soft" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`line_length_limit_hard`:
The "hard" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`class_names`:
How classes are named. `lower` = lowercase only, `lower_under` = lowercase with underscore separators, `studly` = StudlyCase.

`class_brace_line`:
Does the opening brace for a class go on the `same` line as the class keyword, or on the `next` line after it?

`constant_names`:
How are class constants named? `upper` = Uppercase with underscore separators.

`true_false_null`:
Are the `true`, `false`, and `null` keywords spelled as all `lower` case, or all `upper` case?

`method_names`:
How are methods named? `camel` = `camelCase`, `lower_under` = lowercase with underscore separators.

`method_brace_line`:
Does the opening brace for a method go on the `same` line as the method name, or on the `next` line?

`control_brace_line`:
Does the opening brace for a control structure go on the `same` line, or on the `next` line?

`control_space_after`:
Is there a space after the control structure keyword?

`always_use_control_braces`:
Do control structures always use braces?

`else_elseif_line`:
When using `else` or `elseif`, does it go on the `same` line as the previous closing brace, or does it go on the `next` line?

`case_break_indent_from_switch`:
How many times are `case` and `break` indented from an opening `switch` statement?

`function_space_after`:
Do function calls have a space after the function name and before the opening parenthesis?

`closing_php_tag_required`:
In files containing only PHP, is the closing `?>` tag required?

`line_endings`:
What type of line ending is used?

`static_or_visibility_first`:
When declaring a method, does `static` come first, or does the visibility come first?

`control_space_parens`:
In a control structure expression, is there a space after the opening parenthesis and a space before the closing parenthesis? `yes` = `if ( $expr )`, `no` = `if ($expr)`.

`blank_line_after_php`:
Is there a blank line after the opening PHP tag?

`class_method_control_brace`:
A summary of what line the opening braces go on for classes, methods, and control structures.

### A.3. Survey Results

    indent_type:
        tab: 7
        2: 1
        4: 14
    line_length_limit_soft:
        ?: 2
        no: 3
        75: 4
        80: 6
        85: 1
        100: 1
        120: 4
        150: 1
    line_length_limit_hard:
        ?: 2
        no: 11
        85: 4
        100: 3
        120: 2
    class_names:
        ?: 1
        lower: 1
        lower_under: 1
        studly: 19
    class_brace_line:
        next: 16
        same: 6
    constant_names:
        upper: 22
    true_false_null:
        lower: 19
        upper: 3
    method_names:
        camel: 21
        lower_under: 1
    method_brace_line:
        next: 15
        same: 7
    control_brace_line:
        next: 4
        same: 18
    control_space_after:
        no: 2
        yes: 20
    always_use_control_braces:
        no: 3
        yes: 19
    else_elseif_line:
        next: 6
        same: 16
    case_break_indent_from_switch:
        0/1: 4
        1/1: 4
        1/2: 14
    function_space_after:
        no: 22
    closing_php_tag_required:
        no: 19
        yes: 3
    line_endings:
        ?: 5
        LF: 17
    static_or_visibility_first:
        ?: 5
        either: 7
        static: 4
        visibility: 6
    control_space_parens:
        ?: 1
        no: 19
        yes: 2
    blank_line_after_php:
        ?: 1
        no: 13
        yes: 8
    class_method_control_brace:
        next/next/next: 4
        next/next/same: 11
        next/same/same: 1
        same/same/same: 6
