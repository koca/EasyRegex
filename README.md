## Easy Regex
- ported from [VerbalExpressions](https://github.com/VerbalExpressions/PHPVerbalExpressions)

EasyRegex is a PHP library that helps to construct hard regular expressions.  

## Install

```
$ composer require koca/easyregex
```

## Usage

```php
// some tests
use Koca\EasyRegex\EasyRegex;

$regex = new EasyRegex;

$regex  ->startOfLine()
        ->then("http")
        ->maybe("s")
        ->then("://")
        ->maybe("www.")
        ->anythingBut(" ")
        ->endOfLine();


if($regex->test("https://github.com/"))
    echo "valid url";
else
    echo "invalid url";

if (preg_match($regex, 'http://github.com')) {
    echo 'valid url';
} else {
    echo 'invalid url';
}


echo "<pre>". $regex->getRegex() ."</pre>";



echo $regex ->clean(array("modifiers" => "m", "replaceLimit" => 4))
            ->find(' ')
            ->replace("This is a small test http://somesite.com and some more text.", "-");

```

### Regex Capturing

```php

$regex->find("You have ")
    ->beginCapture("count")
    ->word()
    ->endCapture();

$contributions = $regex->match("You have 258 contributions in the last year");

echo $contributions["count"];

// Output: 258

``` 

##Methods list

Name|Description|Usage
:---|:---|:---
add| add values to the expression| add('abc')
startOfLine| mark expression with ^| startOfLine(false)
endoOfLine| mark the expression with $|endOfLine()
then|add a string to the expression| add('foo')
find| alias for then| find('foo')
maybe| define a string that might appear once or not| maybe('.com')
anything| accept any string| anything()
anythingUntil | Anything up until given sequence of characters| anythingUntil('.com')
anythingBut| accept any string but the specified char| anythingBut(',')
something| accept any non-empty string| something()
somethingBut| anything non-empty except for these chars| somethingBut('a')
replace| shorthand for preg_replace()| replace($source, $val)
lineBreak| match \r \n|lineBreak()
br|shorthand for lineBreak| br()
tab|match tabs \t |tab()
word|match \w+|word()
anyOf| any of the listed chars| anyOf('abc')
any| shorthand for anyOf| any('abc')
range| adds a range to the expression|range(a,z,0,9)
withAnyCase| match case default case sensitive|withAnyCase()
beginCapture| Capture groups (can optionally name)| beginCapture("bar")
endCapture| Stop capture| endCapture()
match| Shorthand method for preg_match| match("long string")
matchAll| Shorthand method for preg_match_all| matchAll("long string")
stopAtFirst|toggles the g modifiers|stopAtFirst()
addModifier| add a modifier|addModifier('g')
removeModifier| remove a mofier|removeModifier('g')
searchOneLine| Toggles m modifier|searchOneLine()
multiple|adds the multiple modifier| multiple('*')
_or|wraps the expression in an `or` with the provided value|_or('bar')
limit|adds char limit|limit(1,3)
test| performs a preg_match| test('valid@email.com')


## Building the project and running the tests
The project supports Composer so you have to install [Composer](https://getcomposer.org/doc/00-intro.md#installation-nix) first before project setup.

    curl -sS https://getcomposer.org/installer | php
    php composer.phar install --dev
    ln -s vendor/phpunit/phpunit/phpunit.php phpunit
    ./phpunit
    

## License

This project is free and open source software, distributed under the [MIT License](/LICENSE) 
