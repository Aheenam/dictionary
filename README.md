*NOTE: This package is still in development and yet not ready for production*

---

A PHP Dictionary package
===

This package serves the functionality of a simple dictionary. Mainly created for an own use case, this package will be helpful if you have a single table of words that need to be translated.

Requirements
---

This package is build to be used with `php 7.2 or higher`.

Installation
---

You can install the package by simply pulling it from packagist:

```bash
composer require aheenam/dictionary
```

Usage
---

The main intention of this package is to browse and filter words and their translations in a given dataset. It does not provide any functionality to actually store it in a database.

The basic concept of this package is a dictionary as a collection of words in the base language of this dictionary. All those words have a list of translations which are basically also words, but with the difference that they are in a different language.

The word and its translations together form an entry of the dictionary. A entry must have exactly one word in the base language of the dictionary to be added to it.

Once you have a full dictionary of entries, you can use this package to search and filter in this dictionary.

### A dictionary

To use this package you need an instance of a dictionary first. The dictionary must be declared with a base language.

```php
<?php
use Aheenam\Dictionary\Dictionary;
use Aheenam\Dictionary\Language;

$baseLanguage = new Language('ta');
$dictionary = new Dictionary($baseLanguage);
```

### A Dictionary Entry

The dictionary is a collection of a lot of words that can be translated. Words in the base language of the dictionary and the translations of this word for an entry.

```php
<?php
use Aheenam\Dictionary\Word;
use Aheenam\Dictionary\Entry;

$language = new Language('ta');
$tamilWord = new Word('அம்மா', $language, [
    'grammatical_gender' => 'f'
]);

$language = new Language('de');
$germanWord = new Word('Mutter', $language, [
    'grammatical_gender' => 'f',
    'article' => 'die'
]);

// A entry accepts as many instances of word as needed
$entry = new Entry($tamilWord, $germanWord);
```

#### Add entry to dictionary

Once you have an entry you can add it to the dictionary using the `add()` method.

```php
<?php

$dictionary->add($entry);
```

Note that you have to make sure that the entry contains exactly one word in the base language. Otherwise a `Aheenam\Dictionary\MultipleBaseWordsException` exception will be thrown