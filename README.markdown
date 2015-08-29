# Liberta-Logger: Simple Logging for PHP

A project written by [Paul Coifier](http://www.mobissime.com) .

## About

Liberta-Logger is an easy-to-use [PSR-3](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md)
compliant logging class for PHP. It isn't naive about
file permissions (which is expected). It was meant to be a class that you could
quickly include into a project and have working right away.

If you need a logger that supports PHP < 5.3.

## Installation

### Composer

From the Command Line:

```
composer require liberta\logger:dev-master
```

In your `composer.json`:

``` json
{
    "require": {
        "liberta\logger": "dev-master"
    }
}
```

## Basic Usage

``` php
<?php

require 'vendor/autoload.php';

$users = [
    [
        'name' => 'Paul Coiffier',
        'username' => 'pcoiffier',
    ],
    [
        'name' => 'Audrey Dupont',
        'username' => 'adupont',
    ],
];

$logger = new Liberta\Logger\Logger(__DIR__.'/logs');
$logger->info('Returned a million search results');
$logger->error('Oh dear.');
$logger->debug('Got these users from the Database.', $users);
```

### Output

```
[2014-03-20 3:35:43.762437] [INFO] Returned a million search results
[2014-03-20 3:35:43.762578] [ERROR] Oh dear.
[2014-03-20 3:35:43.762795] [DEBUG] Got these users from the Database.
    0: array(
        'name' => 'Paul Coiffier',
        'username' => 'coiffierp',
    )
    1: array(
        'name' => 'Michel Dupont',
        'username' => 'mdup',
    )
```

## PSR-3 Compliant

Liberta-Logger is [PSR-3](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md)
compliant. This means it implements the `Psr\Log\LoggerInterface`.

[See Here for the interface definition.](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md#3-psrlogloggerinterface)

## Setting the Log Level Threshold

You can use the `Psr\Log\LogLevel` constants to set Log Level Threshold, so that
any messages below that level, will not be logged.

### Default Level

The default level is `DEBUG`, which means everything will be logged.

### Available Levels

``` php
<?php
use Psr\Log\LogLevel;

// These are in order of highest priority to lowest.
LogLevel::EMERGENCY;
LogLevel::ALERT;
LogLevel::CRITICAL;
LogLevel::ERROR;
LogLevel::WARNING;
LogLevel::NOTICE;
LogLevel::INFO;
LogLevel::DEBUG;
```

### Example

``` php
<?php
// The 
$logger = new Liberta\Logger\Logger('/var/log/', Psr\Log\LogLevel::WARNING);
$logger->error('Uh Oh!'); // Will be logged
$logger->info('Something Happened Here'); // Will be NOT logged
```

### Additional Options

MLogger supports additional options via third parameter in the constructor:

``` php
<?php
// Example
$logger = new Liberta\Llogger\Logger('/var/log/', Psr\Log\LogLevel::WARNING, array (
    'extension' => 'log', // changes the log file extension
));
```

Here's the full list:

| Option | Default | Description |
| ------ | ------- | ----------- |
| dateFormat | 'Y-m-d G:i:s.u' | The format of the date in the start of the log lone (php formatted) |
| extension | 'txt' | The log file extension |
| filename | [prefix][date].[extension] | Set the filename for the log file. **This overrides the prefix and extention options.** |
| flushFrequency | `false` (disabled) | How many lines to flush the output buffer after |
| prefix  | 'log_' | The log file prefix |



## License

The MIT License

Copyright (c) 2015 Paul Coiffier <coiffier.paul@gmail.com>
Copyright (c) 2008-2014 Kenny Katzgrau <katzgrau@gmail.com>


Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
