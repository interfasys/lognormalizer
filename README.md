## Log Normalizer
Parses variables and converts them to string so that they can be logged

Based on the [Monolog](https://github.com/Seldaek/monolog) normalizer.

## How to use

### Initialisation in your class

```
use InterfaSys\LogNormalizer\Normalizer;

$normalizer = new Normalizer();
```

The constructor supports the following optional arguments

* `int $maxObjectDepth`: How deep do you want to go when inspecting objects
* `int $maxArrayItems`: The maximum number of Array elements you want to show, when parsing an array
* `string $dateFormat`: The format to apply to dates

### Normalize a log entry

This is what your logging function could look like

```
/**
 * Converts the variables in the received log message to string before
 * sending everything to the real logger
 *
 * @param string $level
 * @param string $message
 * @param array $variables
 *
 * @return mixed
 */
public function log($level, $message, array $variables= []) {
	array_walk($variables, [$this->normalizer, 'format']);
	
	// Then use your current PSR-3 compatible logging system
	$this->logger->log($level, $message, $variables);
}
```	

And you would call it like this from another class

```
$myLogger->log('debug',
	'Logger test {var1}, {var2}',
	[
		'var1' => $var1,
		'var2' => $var2
		]
);
```

### Normalize a single variable

```
$normalizedVariable = $this->normalizer->format($variable);
```
