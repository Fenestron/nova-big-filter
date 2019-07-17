## Laravel Nova Big Filter
[![Latest Version on Github](https://img.shields.io/packagist/v/nrml-co/nova-big-filter.svg?style=flat)](https://packagist.org/packages/nrml-co/nova-big-filter)
[![Total Downloads](https://img.shields.io/packagist/dt/nrml-co/nova-big-filter.svg?style=flat)](https://packagist.org/packages/nrml-co/nova-big-filter)


A nice looking filter menu that's always open **(in one line)**.

![Nova Big Filter Screenshot](resources/img/screenshot.png)

## Install

Install the package in to a [Laravel Nova](https://nova.laravel.com) project via composer:

```bash
composer require nrml-co/nova-big-filter
```

## Usage

Add the class to the card array of a resource with filters. The default 'Per Page' filter is not included.  If you add the card but don't have any filters, you wont see anything.  Add some filters and it will show up.  

This package makes life easy by eliminating the tiresome click and scroll of the default filter. You may have to play with the order of your filters to get things looking great.  For instance, Date Filters look best on the bottom.  


```php

use NrmlCo\NovaBigFilter\NovaBigFilter;
use App\Nova\Filters\YourFilter;
use App\Nova\Filters\YourOtherFilter;

public function filters()
{
    return [
        new YourFilter,
        new YourOtherFilter,
    ];
}

public function cards()
{
    return [        
        new NovaBigFilter,
    ];
}
```

## Customization
Adding customization functions as needed, and by request.  :)

### setTitle($title)

Use setTitle to change the card title.  The default is 'Filter Menu'.

```php

public function cards()
{
    return [        
        (new NovaBigFilter)->setTitle('Big Filter'),
    ];
}

```

### setMaxHeight($height)

Use setMaxHeight to change the max height of the filter block.  The default is 350.

```php

public function cards()
{
    return [        
        (new NovaBigFilter)->setMaxHeight(400),
    ];
}

```

### hideFilterTitle()

Use hideFilterTitle to hide a title of the filter block, if you don't need it.

```php

public function cards()
{
    return [        
        (new NovaBigFilter)->hideFilterTitle(),
    ];
}

```
