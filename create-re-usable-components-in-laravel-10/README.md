
## How To Create Re-Usable Components in Laravel 10
 
Components in Laravel are reusable and modular pieces of code that may be merged to build larger and more complicated apps. Tutorial is super easy to understand and easy to follow to implement it.

### How To Create a Reusable Component File

Create __components__ folder inside __/resources/views__ folder.

Create a file with name __message.blade.php__ inside __/components__ folder.

```swift
<div class="panel {{ $class }}">
    <div class="panel-heading">{{ $title }}</div>
    <div class="panel-body">{{ $slot }}</div>
</div>
```

Here, you can see we have 3 placeholders as __$class__, __$title__ and __$slot__.

### Create a Layout File

Create a __my-template.blade.php__ blade layout file inside __/resources/views__ folder.

Open __my-template.blade.php__ and write this code into it.

```swift
<!DOCTYPE html>
<html>
<head>
    <title>How To Create Re-Usable Components in Laravel 10</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css" />
</head>
<body>
  
<div class="container">
    <h3>How To Create Re-Usable Components in Laravel 10</h3>
   
    <div style="margin-top:20px;">
        <!-- For General info -->
        @component('components.message')    
    
            @slot('class')
                panel-primary
            @endslot

            @slot('title')
                This is from Online Web Tutor
            @endslot

            Custom components with primary class
        @endcomponent

        <br/>

        <!-- For Error -->
        @component('components.message')    

            @slot('class')
                panel-danger
            @endslot

            @slot('title')
                This is from Online Web Tutor
            @endslot

            Custom components with danger class
        @endcomponent

    <br/>

    <!-- For Success -->
    @component('components.message')    

        @slot('class')
            panel-success
        @endslot

        @slot('title')
            This is from Online Web Tutor
        @endslot

        Custom components with success class
    @endcomponent
    </div>
  
</div>
  
</body>
</html>
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/how-to-create-re-usable-components-in-laravel-10/)