
## How To Generate Unique Slug in Laravel 10 Tutorial

Create Model & Migration

```swift
$ php artisan make:model Product -m
```

This command create two different files – a Model file and a Migration file. -m is for migration file.

1. Proudct.php model file inside /app/Models folder.
2. 2023_03_15_030914_create_products_table.php Migration file inside /database/migrations.

Open __{timestamp}_create_products_table.php__ migration file and write this update code.

```swift
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('products', function (Blueprint $table) {
            $table->id();
            $table->string("name", 70);
            $table->string("slug", 100)->nullable();
            $table->text("description")->nullable();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('products');
    }
};
```

Run Migration

```swift
$ php artisan migrate
```

Open __Product.php__ from __/app/Models__ folder and write this following code into it.

```swift
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Support\Str;

class Product extends Model
{
    use HasFactory;

    protected $fillable = [
        'name', 'slug', 'description'
    ];

    public $timestamps = false;

    /**

     * Boot the model.

     */

    protected static function boot()
    {
        parent::boot();

        static::created(function ($product) {

            $product->slug = $product->createSlug($product->name);

            $product->save();
        });
    }

    /** 
     * Write code on Method
     *
     * @return response()
     */
    private function createSlug($name)
    {
        if (static::whereSlug($slug = Str::slug($name))->exists()) {

            $max = static::whereName($name)->latest('id')->skip(1)->value('slug');

            if (isset($max[-1]) && is_numeric($max[-1])) {

                return preg_replace_callback('/(\d+)$/', function ($mathces) {

                    return $mathces[1] + 1;
                }, $max);
            }
            return "{$slug}-2";
        }
        return $slug;
    }
}
```

__whereSlug__ is dynamic method created from the name of column. where{ColumnName}. whereName() is for name column.

### Create Application Controller

```swift
$ php artisan make:controller ProductController
```

It will create a file __ProductController.php__ inside __/app/Http/Controllers__ folder.

Open this controller file and write this code into it.

```swift
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Product;

class ProductController extends Controller
{
    public function addProduct()
    {
        $product = Product::create([
            "name" => "Laravel 10 Sample Product",
            "description" => "Sample data"
        ]);

        dd($product);
    }
}
```

### Add Route

Open __web.php__ from __/routes__ folder. Add this route into it.

```swift
//...
use App\Http\Controllers\ProductController;

Route::get('product', [ProductController::class, 'addProduct']);

//...
```


### Application Testing

```swift
$ php artisan serve
```

__URL__ – http://127.0.0.1:8000/product

### See Complete Article, [Click here](https://onlinewebtutorblog.com/how-to-generate-unique-slug-in-laravel-10-tutorial/)