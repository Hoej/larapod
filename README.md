# Very short description of the package

This is where your description should go. Try and limit it to a paragraph or two, and maybe throw in a mention of what PSRs you support to avoid any confusion with users and contributors.

## Installation

You can install the package via composer:

```bash
composer require hoej/larapod --dev
```

## Usage

```php
# Start containers
./vendor/bin/pod start

# Stop containers
./vendor/bin/pod stop
```

## Extend

Sometime you will need to extend the runtime image, this could be needed if you need a specfic package or php-ext installed. To extend the runtime image, simply create a ```docker/Dockerfile``` in the root of your project.
```dockerfile
FROM hoej/pod:RUNTIME

# DO YOUR STUFF HERE

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
```

### Testing

```bash
composer test
```

### Security

If you discover any security related issues, please email nb@hoej.dk instead of using the issue tracker.

## Credits

-   [Nicolas Buch](https://github.com/hoej)
-   [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
