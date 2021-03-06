#Car

Car is a PHP implementation of the Command Bus pattern for DDD.

[![Build Status](https://travis-ci.org/maximecolin/car.svg)](https://travis-ci.org/maximecolin/car)

##Disclaimer

This is a very basic and simple implementation. It has to grow up :)

##Installation

```
composer require maximecolin/car
```

##Purpose

The aim of the command bus pattern is to isolate your domain code in atomic, testable and reusable classes and to execute them through a dedicated service.

##Usage

A command is an order. It can contains data you need. Attributes can be set on construct, fill through a form, set by other services, ...

```php
class CreateArticleCommand implements CommandInterface
{
	public $title;
	public $content;
	
	public function __construct($title, $content)
	{
		$this->title   = $title;
		$this->content = $content;
	}
}
```

Create an handler which will process your command.

```php
class CreateCommandHandler implements CommandHandlerInterface
{
	public function handle(CommandInterface $command)
	{
		// Place here you domain code which create an article ...
	}
}
```



```php
// Usually, have a service to get the bus
$bus = new CommandBus();
$bus->addResolver(new ClassNameResolver());

$command = new CreateArticleCommand('My article name', 'My article content');

$bus->execute($command);
```

##Comming soon

Event sourcing integration.

