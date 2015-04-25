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

```
public function log($level, $message, array $context = []) {
	array_walk($context, [$this->normalizer, 'format']);
	
	// Then use your current logging system
	$this->logger->log($level, $message, $context);
}
```	

### Normalize a single variable

```
$normalizedVariable = $this->normalizer->format($variable);
```
