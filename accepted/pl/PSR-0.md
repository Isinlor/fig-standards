Standard automatycznego ładowania
====================

Niniejszy dokument określa wymagania, które muszą być przestrzegane dla
zachowania współdziałania automatycznego ładowania klas.

Wymagane
---------

* W pełni poprawna przestrzeń nazw i klas musi mieć następującą strukturę `\<Vendor Name>\(<Namespace>\)*<Class Name>`
* Każda przestrzeń nazw musi mieć przestrzeń nadrzędną ("Vendor Name")
(pol. Nazwa Dostarczyciela).
* Każda przestrzeń nazw może mieć dowolnie wiele podprzestrzeni.
* Każdy separator przestrzeni nazw jest zamieniany na `DIRECTORY_SEPARATOR`
podczas ładowania z systemu plików.
* Każdy znak `_` w nazwie klasy zamieniany jest na
  `DIRECTORY_SEPARATOR`. Znak `_` nie ma specjalnego znaczenia w przestrzeni
  nazw.
* W pełni poprawna przestrzeń nazw i klas musi być zakończona końcówką `.php`
kiedy ładowana z systemu plików.
* Znaki alfabetyczne w nazwie dostarczyciela, przestrzeni nazw i nazwie klasy
  może być jakąkolwiek kombinacją dużych i małych liter.

Przykłady
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

Znak podkreślenia w przestrzeniach nazw i klas
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

Standard ustalony tutaj powinien być najmniejszym wspólnym mianownikiem dla
bezproblemowego współdzielenia automatycznego ładowania. Możesz sprawdzić czy
przestrzegasz te standardy wykorzystując ten prosty przykład implementacji
SplClassLoader, który umożliwia ładowanie klas PHP 5.3.

Przykładowa implementacja
----------------------

Poniżej jest funkcja która w prosty sposób demonstruje proponowany standard
automatycznego ładowania.

```php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
```

Implementacja SplClassLoader
-----------------------------

Poniższy gist jest przykładem implementacji SplClassLoader, który umożliwia
ładowanie klas, jeśli przestrzegasz powyżej zaproponowanego standardu
automatycznego ładowania klas. Jest to obecnie rekomendowana metoda ładowania
klas które przestrzegają powyższych standardów w PHP 5.3.

* [http://gist.github.com/221634](http://gist.github.com/221634)
