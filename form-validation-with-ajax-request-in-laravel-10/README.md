
## Form Validation with Ajax Request in Laravel 10 Tutorial

In web application, form must have validation rules. Validation rules can be from any end. Form validation using Client side library. Form validations handled by server side. Means we have several options to do this. The main reason is to protect input fields from invalid entries and restrict user.

We will implement form validation using server side. Form data we will post via Ajax. In the request from client side, we will do request to server and validate form from server.

### Create Controller

Open project into terminal and type these artisan command into it to create controllers.

```swift
$ php artisan make:controller HomeController
$ php artisan make:controller AjaxController
```

These commands will create __HomeController.php__ and __AjaxController.php__ files inside __/app/Http/Controllers__ folder.

Open __HomeController.php__ and write this code into it.

```swift
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class HomeController extends Controller
{
    public function addForm()
    {
        return view('add-form');
    }
}

```

Open __AjaxController.php__ and write this code into it.

```swift
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Validator;

class AjaxController extends Controller
{
    public function submitForm(Request $request)
    {
        $validator = Validator::make($request->all(), [
            'first_name' => 'required',
            'last_name' => 'required',
            'email' => 'required|email'
        ]);

        if ($validator->passes()) {
            return response()->json(['success' => 'Added new records.']);
        }

        return response()->json(['error' => $validator->errors()->all()]);
    }
}

```

### Create Template File with Ajax Code

Create a file with name __add-form.blade.php__ inside __/resources/views__ folder.

```swift
<!DOCTYPE html>
<html>
<head>
    <title>Laravel 10 Ajax Validation Tutorial - Online Web Tutor</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.js"></script>
</head>
<body>
       
<div class="container">
    <h3 style="text-align: center;">Laravel 10 Ajax Validation Tutorial - Online Web Tutor</h3>
       
    <div class="alert alert-danger print-error-msg" style="display:none">
        <ul></ul>
    </div>
       
    <form method="post" action="javascript:void(0);">

        {{ csrf_field() }}
        
        <div class="form-group">
            <label>First Name:</label>
            <input type="text" name="first_name" class="form-control" placeholder="First Name">
        </div>
       
        <div class="form-group">
            <label>Last Name:</label>
            <input type="text" name="last_name" class="form-control" placeholder="Last Name">
        </div>
       
        <div class="form-group">
            <strong>Email:</strong>
            <input type="text" name="email" class="form-control" placeholder="Email">
        </div>
       
        <div class="form-group">
            <button class="btn btn-success btn-submit">Submit</button>
        </div>
    </form>
</div>
       
<script type="text/javascript">
       
    $(document).ready(function() {

        $(".btn-submit").click(function(e){
          
            e.preventDefault();
       
            // prepare form data
            var _token = $("input[name='_token']").val();
            var first_name = $("input[name='first_name']").val();
            var last_name = $("input[name='last_name']").val();
            var email = $("input[name='email']").val();
       
            // ajax request
            $.ajax({
                url: "{{ route('add.form') }}",
                type:'POST',
                data: {_token:_token, first_name:first_name, last_name:last_name, email:email},
                success: function(data) {
                    if($.isEmptyObject(data.error)){
                        alert(data.success);
                        $(".print-error-msg").css({
                            display:"none"
                        });
                    }else{
                        printErrorMsg(data.error);
                    }
                }
            });
       
        }); 
       
        function printErrorMsg (msg) {
            $(".print-error-msg").find("ul").html('');
            $(".print-error-msg").css('display','block');
            $.each( msg, function( key, value ) {
                $(".print-error-msg").find("ul").append('<li>'+value+'</li>');
            });
        }
    });


</script>


</body>
</html>
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/form-validation-with-ajax-request-in-laravel-10-tutorial/)