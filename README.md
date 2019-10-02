# Nova Filepond

[![Latest Version on Packagist](https://img.shields.io/packagist/v/digital-creative/nova-filepond)](https://packagist.org/packages/digital-creative/nova-filepond)
[![Total Downloads](https://img.shields.io/packagist/dt/digital-creative/nova-filepond)](https://packagist.org/packages/digital-creative/nova-filepond)
[![License](https://img.shields.io/packagist/l/digital-creative/nova-filepond)](https://github.com/dcasia/nova-filepond/blob/master/LICENSE)

![Laravel Nova Filepond in action](https://raw.githubusercontent.com/dcasia/nova-filepond/master/screenshots/demo-1.gif)

A Nova field for uploading File, Image and Video using Upload File, Image and Video using [Filepond](https://github.com/pqina/filepond).

# Installation

You can install the package via composer:

```
composer require digital-creative/nova-filepond
```

# Usage

```php
use DigitalCreative\Filepond\Filepond;

class Post extends Resource
{
    public function fields(Request $request)
    {
        return [
            // ...
            Filepond::make('Audio Example')
                    ->multiple() // the default is single upload, use this method to allow multiple uploads
                    ->limit(4) // limit the number of attached files
                    ->rules('required') // every validation rule works!!
                    ->mimesTypes([ 'audio/mp3', 'audio/ogg', 'audio/vnd.wav' ]) // if opmited, accepts anything
                    ->disk('public', '/optional/location') // the second argument instruct the file to be stored into a subfolder
                    ->storeAs(function (Illuminate\Http\File $file) { // this is optional, use in case you need generate custom file names
                        return Str::random(20) . '.' . $file->getExtension();
                    })

        ];

    }
}
```

When uploading multiple files you will need to cast the attribute to an array in your model class

```php
class Post extends Model {
    
    /**
     * The attributes that should be cast to native types.
     *
     * @var array
     */
    protected $casts = [
        'images' => 'array'
    ];

}
```

## License

The MIT License (MIT). Please see [License File](https://raw.githubusercontent.com/dcasia/nova-filepond/master/LICENSE) for more information.
