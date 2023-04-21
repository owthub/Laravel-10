
## Laravel 10 Export MySQL Table Data into CSV File Tutorial

If we have an application which basically built for reporting then you need some kind of function which export tabular data into CSV format. This function is for admin purpose.

### Create Migration

We will create a products table using migration and then we seed test data inside it.

```swift
$ php artisan make:migration create_products_table
```

It will create __2023_03_17_031027_create_products_table.php__ file inside __/database/migrations__ folder.

Open __xxx_create_products_table.php__ and write this code into it.

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
            $table->string("slug", 100);
            $table->text("description");
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

Back to terminal and run this command.

```swift
$ php artisan migrate
```

### Create Controller

Open project into terminal and run this command into it.

```swift
$ php artisan make:controller DataController
```

It will create __DataController.php__ file inside __/app/Http/Controllers__ folder. Open controller file and write this code into it.

```swift
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Product;

class DataController extends Controller
{
    public function downloadCSVReport()
    {
        header('Content-Type: text/csv; charset=utf-8');
        header('Content-Disposition: attachment; filename=product-' . date("Y-m-d-h-i-s") . '.csv');
        $output = fopen('php://output', 'w');
      
        fputcsv($output, array('Id', 'Name', 'Slug'));

        $products = Product::get();

        if (count($products) > 0) {

            foreach ($products as $product) {

                $product_row = [
                    $product['id'],
                    ucfirst($product['name']),
                    $product['slug']
                ];

                fputcsv($output, $product_row);
            }
        }
    }
}
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/laravel-10-export-mysql-table-data-into-csv-file-tutorial/)