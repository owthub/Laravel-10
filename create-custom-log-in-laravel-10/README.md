
## How To Create Custom Log File in Laravel 10 Tutorial


__Open logging.php file from /config folder. Inside logging.php search for channels.__

```swift
'channels' => [

    ...       

    'webtutorlog' => [
        'driver' => 'single',
        'path' => storage_path('logs/applicationlog.log'),
        'level' => 'info',
    ],

],
```

webtutorlog is channel name. applicationlog.log is custom log file name where we will store our custom log messages.

__Open web.php from /routes folder. Add this route into it.__

```swift
//...

use Illuminate\Support\Facades\Log;

Route::get('create-log', function () {
  
    Log::channel('webtutorlog')->info('This is info log level for testing');
    Log::channel('webtutorlog')->warning('This is warning log level for testing');
    Log::channel('webtutorlog')->error('This is error log level for testing');
    Log::channel('webtutorlog')->alert('This is alert log level for testing');
    Log::channel('webtutorlog')->emergency('This is emergency log level for testing');
    Log::channel('webtutorlog')->notice('This is notice log level for testing');
    
    dd('done');
     
});

//...
```


__Start Development Server__

```swift
$ php artisan serve
```

URL: http://127.0.0.1:8000/create-log

You will get applicationlog.log file inside /storage/logs folder. When you open, you should see these lines added into it.

```swift
[2023-04-08 10:48:06] local.INFO: This is info log level for testing  
[2023-04-08 10:48:06] local.WARNING: This is warning log level for testing  
[2023-04-08 10:48:06] local.ERROR: This is error log level for testing  
[2023-04-08 10:48:06] local.ALERT: This is alert log level for testing  
[2023-04-08 10:48:06] local.EMERGENCY: This is emergency log level for testing  
[2023-04-08 10:48:06] local.NOTICE: This is notice log level for testing 
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/how-to-create-custom-log-file-in-laravel-10-tutorial/)