
## How To Create Custom Artisan Command in Laravel 10

The __make:command__ is used to create artisan command.

When we create custom artisan command, then command files will be stored inside __/app/Console/Commands__ folder.

### Create Basic Artisan Command

Run this command to create command file.

```swift
$ php artisan make:command UserInfo
```

Command file __UserInfo.php__ will be created inside __/app/Console/Commands__ folder.

Open __UserInfo.php__ and write this code into it.

```swift
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;

class UserInfo extends Command
{
    /**
     * The name and signature of the console command.
     *
     * @var string
     */
    protected $signature = 'user:info';

    /**
     * The console command description.
     *
     * @var string
     */
    protected $description = 'This is the command asks for user information and display';

    /**
     * Execute the console command.
     *
     * @return int
     */
    public function handle()
    {
        $name = $this->ask('What is your name?');

        $email = $this->ask('What is your email address?');

        $this->info('User Informations: Name - ' . $name . " and Email - " . $email);
    }
}
```

### Usage of Command

Back to terminal and run this command

```swift
$ php artisan user:info
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/how-to-create-custom-artisan-command-in-laravel-10/)