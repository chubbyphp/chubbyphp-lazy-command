# chubbyphp-lazy-command

[![Build Status](https://api.travis-ci.org/chubbyphp/chubbyphp-lazy-command.png?branch=master)](https://travis-ci.org/chubbyphp/chubbyphp-lazy-command)
[![Coverage Status](https://coveralls.io/repos/github/chubbyphp/chubbyphp-lazy-command/badge.svg?branch=master)](https://coveralls.io/github/chubbyphp/chubbyphp-lazy-command?branch=master)
[![Latest Stable Version](https://poser.pugx.org/chubbyphp/chubbyphp-lazy-command/v/stable.png)](https://packagist.org/packages/chubbyphp/chubbyphp-lazy-command)
[![Total Downloads](https://poser.pugx.org/chubbyphp/chubbyphp-lazy-command/downloads.png)](https://packagist.org/packages/chubbyphp/chubbyphp-lazy-command)
[![Monthly Downloads](https://poser.pugx.org/chubbyphp/chubbyphp-lazy-command/d/monthly)](https://packagist.org/packages/chubbyphp/chubbyphp-lazy-command)
[![Daily Downloads](https://poser.pugx.org/chubbyphp/chubbyphp-lazy-command/d/daily)](https://packagist.org/packages/chubbyphp/chubbyphp-lazy-command)

## Description

Allow to lazyload commands.

## Requirements

 * php: ^7.2
 * psr/container: ^1.0
 * symfony/console: ^3.4.43|^4.4.11|^5.0

## Installation

Through [Composer](http://getcomposer.org) as [chubbyphp/chubbyphp-lazy-command][1].

```sh
composer require chubbyphp/chubbyphp-lazy-command "^1.4"
```

## Usage

### For callables

```php
<?php

use Chubbyphp\Lazy\LazyCommand;
use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Input\InputArgument;
use Symfony\Component\Console\Output\OutputInterface;

$container['service'] = function () {
    return function (InputInterface $input, OutputInterface $output) {
        // run some lazy logic
    };
};

$command = new LazyCommand(
   $container,
   'service',
   'name',
   [
       new InputArgument('argument'),
   ],
   'description',
   'help'
);

$command->run();
```

### For existing commands extending Command

```php
<?php

use Chubbyphp\Lazy\CommandAdapter;
use Chubbyphp\Lazy\LazyCommand;
use Symfony\Component\Console\Input\InputArgument;

$container['service'] = function () {
    return new CommandAdapter(new ExistingCommand());
};

$command = new LazyCommand(
   $container,
   'service',
   'name',
   [
       new InputArgument('argument'),
   ],
   'description',
   'help'
);

$command->run();
```

[1]: https://packagist.org/packages/chubbyphp/chubbyphp-lazy-command

## Copyright

Dominik Zogg 2020
