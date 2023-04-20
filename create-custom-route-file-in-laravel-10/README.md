
## How To Create Custom Route File in Laravel 10 Tutorial

### Custom Route Files (Module wise Separation)

Create files as __admin.php__ and __customer.php__ as per requirement into /routes folder.

Open __admin.php__ file from __/routes__ folder. Inside this file we will place all admin related routes.

```swift
<?php

use Illuminate\Support\Facades\Route;

// Admin Routes
Route::prefix("admin")->group(function(){
   Route::get("create-user", [AdminController::class, "createUser"]);
   Route::get("list-users", [AdminController::class, "listUsers"]);
   Route::get("edit-user", [AdminController::class, "editUser"]);
});
```

Open __customer.php__ from __/routes__ folder. Inside this file we will place all customer related routes.

```swift
<?php

use Illuminate\Support\Facades\Route;

// Customer Routes
Route::prefix("customer")->group(function(){
   Route::get("list-purchase", [CustomerController::class, "listPurchase"]); 
   Route::get("list-blogs", [CustomerController::class, "listBlogs"]);
   Route::get("create-blog", [CustomerController::class, "createBlog"]);
});
```

### How To Register Custom Route Files?

Open __RouteServiceProvider.php__ file from __/app/Providers__ folder. Next, you can add your custom route files here.

```swift
<?php

namespace App\Providers;

use Illuminate\Cache\RateLimiting\Limit;
use Illuminate\Foundation\Support\Providers\RouteServiceProvider as ServiceProvider;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\RateLimiter;
use Illuminate\Support\Facades\Route;

class RouteServiceProvider extends ServiceProvider
{
    /**
     * The path to the "home" route for your application.
     *
     * This is used by Laravel authentication to redirect users after login.
     *
     * @var string
     */
    public const HOME = '/home';

    /**
     * Define your route model bindings, pattern filters, etc.
     *
     * @return void
     */
    public function boot()
    {
        $this->configureRateLimiting();

        $this->routes(function () {
            Route::middleware('api')
                ->prefix('api')
                ->group(base_path('routes/api.php'));

            Route::middleware('web')
                ->group(base_path('routes/web.php'));

            // Admin Route file 
            Route::middleware('web')
                ->namespace($this->namespace)
                ->group(base_path('routes/admin.php'));

            // Customer Route file
            Route::middleware('web')
                ->namespace($this->namespace)
                ->group(base_path('routes/customer.php'));
        });
    }

    /**
     * Configure the rate limiters for the application.
     *
     * @return void
     */
    protected function configureRateLimiting()
    {
        RateLimiter::for('api', function (Request $request) {
            return Limit::perMinute(60)->by($request->user()?->id ?: $request->ip());
        });
    }
}
```

### Application Testing

```swift
$ php artisan serve
```

__Admin URLs:__

__URL:__ http://127.0.0.1:8000/admin/create-user and all.

__Customer URLs:__

__URL:__ http://127.0.0.1:8000/customer/list-purchase and all.

### See Complete Article, [Click here](https://onlinewebtutorblog.com/how-to-create-custom-route-file-in-laravel-10-tutorial/)