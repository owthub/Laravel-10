
## Laravel 10 How To Add Image Into PDF Using DomPDF Library

DomPDF is a well-known PHP package that generates PDF documents from HTML and CSS. It is simple to integrate in Laravel by utilising the __“barryvdh/laravel-dompdf”__ package.

### How To Install “dompdf” Package

```swift
$ composer require barryvdh/laravel-dompdf
```

### Create Application Controller

```swift
$ php artisan make:controller SiteController
```

It will create SiteController.php file inside /app/Http/Controllers folder. Open controller file and write this code into it.

```swift
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Barryvdh\DomPDF\Facade\Pdf;

class SiteController extends Controller
{
    public function generatePDF()
    {
        $data = [
            'title' => 'Welcome to OnlineWebTutorBlog.com',
            'author' => "Sanjay"
        ];
          
        $pdf = PDF::loadView('my-pdf-file', $data);
    
        return $pdf->download('onlinewebtutorblog.pdf');
    }
}
```

### Create Blade Template (PDF Layout)

Create a file named as my-pdf-file.blade.php inside __/resources/views__ folder. This template file will be the layout for pdf file.

First let’s place __logo__ file into __/public__ folder which is at application root. This logo file we will add into pdf.

Placing a image file with name __“image.png”__ inside __/public__ folder.
Open file __my-pdf-file.blade.php__ and write this code into it.

```swift
<!DOCTYPE html>
<html>
<head>
    <title>Title From OnlineWebTutorBlog</title>
</head>
<body>
    <div style="text-align: center;">
        <img src="{{ public_path('image.png') }}" style="width: 100px; height: 100px">
    </div>
    <h1>Title: {{ $title }}</h1>
    <h3>Author: {{ $author }}</h3>
    <p>ut aliquip ex ea commodoconsequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
    cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidata.</p>
</body>
</html>
```

### Add Route

Open __web.php__ from __/routes__ folder. Add this route into it.

```swift
//...

use App\Http\Controllers\SiteController;

Route::get('generate-pdf', [SiteController::class, 'generatePDF']);

//...
```

### Application Testing

```swift
$ php artisan serve
```
__URL:__ http://127.0.0.1:8000/generate-pdf

### See Complete Article, [Click here](https://onlinewebtutorblog.com/laravel-10-how-to-add-image-into-pdf-using-dompdf-library/)