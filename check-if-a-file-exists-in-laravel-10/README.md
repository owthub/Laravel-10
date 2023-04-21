
## How to Check If a File Exists in Laravel 10 Tutorial

Generally we store public accessible files in __/public__ folder or even in __/storage__ folder. So while accessing those files always need to add a checkpoint that they exists or not.

### Checking File Existence inside Public folder

```swift
public_path("FILE PATH")
```

Example:

```swift
if(File::exists(public_path('images/85214563.jpg'))){

    dd('File is exists.');
}else{
    dd('File is not exists.');
}
```

### Checking File Existence inside Storage folder

```swift
storage_path("FILE PATH")
```

Example:

```swift
if(file_exists(storage_path('images/85214563.jpg'))){

    dd('File exists.');
}else{
    dd('File not exists.');
}
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/how-to-check-if-a-file-exists-in-laravel-10-tutorial/)