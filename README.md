Phantom PDF
===========

A Package for generating PDF files using PhantomJS. The package is framework agnostic, but provides integration with Laravel.

Notice: This package only ships with the 64-bit Linux version of PhantomJS. If you want to use it with another version you can reference it in the configuration.

## Installation
Run `composer require vikki-user/phantom-pdf`

### Usage

```php
$pdf = new PdfGenerator;

// Set a writable path for temporary files
$pdf->setStoragePath('storage/path');

// Saves the PDF as a file (optional)
$pdf->saveFromView($html, 'filename.pdf');

// Returns a Symfony\Component\HttpFoundation\BinaryFileResponse
return $pdf->createFromView($html, 'filename.pdf');

```

### PhantomJS Version
This package uses PhantomJS 1.9.8 x64 which is included in the package. If you want to use another version it's easy.
```php
$pdf->setBinaryPath('/some/path/phantomjs');
```

### Customizing the conversion script
If you want to use another script to execute with PhantomJS, this it how you do it.
```php
$pdf->useScript('`/path/to/script');
```

## Laravel integration

### Installation

#### For Laravel 5.5 the package supports auto discovery and don't need any configuration.

For Laravel 4, use the 0.10.0 branch.

Add `LaravelServiceProvider` in the `providers` array in `config/app.php`
```php
'providers' => [
  PhantomPdf\Laravel\LaravelServiceProvider::class,
]
```

#### Facades (optional)

Add the facade to the `aliases` array in `app/config/app.php` (optional)
```php
'aliases' => [
  'PDF' => PhantomPdf\Laravel\PDFFacade::class,
]
```

### Usage
```php
class SampleController extends Controller
{
  public function index()
  {
    return PDF::createFromView(view('index'), 'filename.pdf');
  }

  // Save the pdf to disk
  public function save()
  {
      PDF::saveFromView(view('index'), 'path/filename.pdf');
  }

  // Usa via injection
  public function foo(PdfGenerator $pdf)
  {
    return $pdf->createFromView(view('path'), 'filename.pdf');
  }
}
```
