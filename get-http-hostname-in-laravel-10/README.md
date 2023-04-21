
## How To Get HTTP Hostname In Laravel 10 Tutorial

The hostname of the web server to which the HTTP request is being made is specified by the HTTP Hostname, often known as the HTTP Host header or simply the Host header.

### Get HTTP Hostname Using Request Helper

Get HTTP Hostname in views or in controllers using request helper function –

```swift
$host = request()->getHttpHost();
```

### Get HTTP Host Using Request Helper

```swift
$host = request()->getHost();
```

### Get HTTP Hostname Using Request Object

```swift
//...

public function anyControllerMethod(Request $request) { 
    
     $hostname = $request->getHttpHost(); 

     $host = $request->getHost(); 
 
     print_r($hostname); 

     print_r($host); 
}
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/how-to-get-http-hostname-in-laravel-10-tutorial/)