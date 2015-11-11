# Pipeline

Pipeline allows to easily chain/sequence operations / tasks on the fly or create a reusable chain of commands.

## Installation

```
composer require stomp/pipeline
```

## Basic usage

Example.

```php
class ConvertToCaps implements TaskInterface {
    public function run($data) {
        return mb_strtoupper($data);
    }
}

class DeleteSpaces implements TaskInterface {
    public function run($data) {
        return str_replace(' ', '', $data);
    }
}

$pipeline = new Pipeline(
    new ConvertToCaps(),
    new DeleteSpaces()
);
$pipeline->execute("Hello, my name is Steve"); // HELLO,MYNAMEISSTEVE
```


```

You don't have to pass all of your tasks at initialisation time. ``Pipeline`` provides an ``add`` method to add steps
 to an existing object:

```php
$pipeline = new Pipeline(new ConvertToCaps());
$pipeline->add(new DeleteSpaces());
$pipeline->execute("Hello, world!"); // HELLO,WORLD!
```
