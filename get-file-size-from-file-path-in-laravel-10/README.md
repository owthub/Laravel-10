
## How To Get File Size From File Path in Laravel 10 Tutorial

Laravel provides few options to get file size from path. In this tutorial, we will use the concept of getting file size using __Storage class__ and File __Facade classes__. We need to assume that we have few files inside __/public__ folder or __/storage/app/public__ folder.


### How To Get File Size: Using Storage Class

Assume we have a file named as __1.png__ inside __/storage/app/public/images__ folder.

```swift
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Storage;

class SampleController extends Controller
{
    public function index()
    {
        $fileSize = Storage::size('public/images/1.png');

        // File size in bytes
        dd($fileSize);
    }
}
```

Output

```swift
File size will be returned into bytes.
```

### How To Get File Size: Using File Class

Assume we have a file named as __1.png__ inside __/public/images__ folder.

```swift
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\File;

class SampleController extends Controller
{
    public function index()
    {
        $fileSize = File::size(public_path('images/1.png'));

        // File size in bytes
        dd($fileSize);
    }
}
```

Output

```swift
File size will be returned into bytes.
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/how-to-get-file-size-from-file-path-in-laravel-10-tutorial/)