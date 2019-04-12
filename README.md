# Автозагрузчик классов

Данные правила являются переводом на русский язык правил [PSR-4] от компании PHP Framework Interop Group.

Ключевые слова «ОБЯЗАН», «ОБЯЗАН НЕ», «ТРЕБУЕТСЯ», «ДОЛЖЕН», «ДОЛЖЕН НЕ», «СЛЕДУЕТ»,
«СЛЕДУЕТ НЕ», «РЕКОМЕНДУЕТСЯ», «МОЖЕТ» и «ПО ЖЕЛАНИЮ» в этом документе нужно
интерпретировать, как описано в стандарте [RFC 2119].

## 1. Обзор

Данный набор правил PSR описывает спецификацию для [автозагрузки][] классов из файловых путей. 
Он полностью совместимый, и может быть использован в дополнение к любой другой спецификации автозагрузки классов, включая [PSR-0][]. Данный PSR также описывает где размещать файлы, которые будут автозагружены согласно спецификации.

## 2. Спецификация

1. Термин "класс" относится к классам, интерфейсам, трейтам, и к другим похожим структурам.

2. A fully qualified class name has the following form:

        \<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>

    1. The fully qualified class name MUST have a top-level namespace name,
       also known as a "vendor namespace".

    2. The fully qualified class name MAY have one or more sub-namespace
       names.

    3. The fully qualified class name MUST have a terminating class name.

    4. Underscores have no special meaning in any portion of the fully
       qualified class name.

    5. Alphabetic characters in the fully qualified class name MAY be any
       combination of lower case and upper case.

    6. All class names MUST be referenced in a case-sensitive fashion.

3. When loading a file that corresponds to a fully qualified class name ...

    1. A contiguous series of one or more leading namespace and sub-namespace
       names, not including the leading namespace separator, in the fully
       qualified class name (a "namespace prefix") corresponds to at least one
       "base directory".

    2. The contiguous sub-namespace names after the "namespace prefix"
       correspond to a subdirectory within a "base directory", in which the
       namespace separators represent directory separators. The subdirectory
       name MUST match the case of the sub-namespace names.

    3. The terminating class name corresponds to a file name ending in `.php`.
       The file name MUST match the case of the terminating class name.

4. Autoloader implementations MUST NOT throw exceptions, MUST NOT raise errors
   of any level, and SHOULD NOT return a value.

## 3. Примеры

The table below shows the corresponding file path for a given fully qualified
class name, namespace prefix, and base directory.

| Fully Qualified Class Name    | Namespace Prefix   | Base Directory           | Resulting File Path
| ----------------------------- |--------------------|--------------------------|-------------------------------------------
| \Acme\Log\Writer\File_Writer  | Acme\Log\Writer    | ./acme-log-writer/lib/   | ./acme-log-writer/lib/File_Writer.php
| \Aura\Web\Response\Status     | Aura\Web           | /path/to/aura-web/src/   | /path/to/aura-web/src/Response/Status.php
| \Symfony\Core\Request         | Symfony\Core       | ./vendor/Symfony/Core/   | ./vendor/Symfony/Core/Request.php
| \Zend\Acl                     | Zend               | /usr/includes/Zend/      | /usr/includes/Zend/Acl.php

For example implementations of autoloaders conforming to the specification,
please see the [примеры файлов][]. Example implementations MUST NOT be regarded
as part of the specification and MAY change at any time.

[автозагрузки]: http://php.net/autoload
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[примеры файлов]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md
[PSR-4]: https://github.com/php-fig/fig-standards/edit/master/accepted/PSR-4-autoloader.md
[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
