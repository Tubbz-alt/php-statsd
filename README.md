# php-statsd
Simple PHP library to send stats to statsd.

Installation
------------
Add the dependency to your composer.json.

```javascript
{
    "require": {
        "shazam/php-statsd": "2.*"
    }
}
```

Usage
-----
An example of how to send metrics of how long it takes to load a page.

```php
<?php

use Statsd;

// $config = array(...);
// $path = ...

// initialize client
$configuration = new Statsd\Client\Configuration();
$configuration->setHost($config['host'])
    ->setNamespace($config['namespace']);

$statsClient = new Statsd\Client($configuration);

// add stats (you can also add an array of stats with addStats())
$statsClient->addStat(
    array(
        'namespace' => 'endpoints.' . $path, // that will be your stat namespace
        'value' => $executionTime, // calculate it in microseconds
        'type' => 'ms'
    )
);

// send them
$statsClient->sendStats();

```

You can use TIME_MS, COUNT, GAUGE or SET (ms, c, g, s) as type of stats.

Configuration
-------------
 * A host to push metrics (use 127.0.0.1 if you have netpipes installed in your box).
 * A port (by default, 8126).
 * A namespace (where all your metrics will be added. Use "." to separate folders.
 * Optionally, a Monolog\Logger object, to log the metrics.

An example of a config file for that client could be:

```yaml
stats:
  enable: true
  client:
    host: 127.0.0.1
    namespace: shazam.twitterhose
```
