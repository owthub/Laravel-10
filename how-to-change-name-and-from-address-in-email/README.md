
## Laravel 10 How To Change Name And From Address in Email

Sending an email in web application is very common. Laravel provides the predefined Mail class used to send mail. We only need to use & configure it. The content of this article is very useful to understand the things that Step-by-step guide to changing email sender details in Laravel 10.

### How To Configure SMTP in Laravel?

To configure SMTP details, open up the file __.env__ from application root.

```swift
//..

MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=465
MAIL_USERNAME="xxxyyyzzz@gmail.com"
MAIL_PASSWORD="your_password"
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="xxxyyyzzz@gmail.com"
MAIL_FROM_NAME="Online Web Tutor"

//...

```

### How To Create a Mail Class

```swift
$ php artisan make:mail MyTestMail
```

Application will create a folder with the name of Mail inside __/app__ folder. You should see a file __MyTestMail.php__ inside __/app/Mail__ folder.

```swift
<?php
  
namespace App\Mail;
  
use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;
  
class MyTestMail extends Mailable
{
    use Queueable, SerializesModels;
  
    public $details;
  
    /**
     * Create a new message instance.
     *
     * @return void
     */
    public function __construct($details)
    {
        $this->details = $details;
    }
  
    /**
     * Build the message.
     *
     * @return $this
     */
    public function build()
    {
        $address = config("mail.from.address");
        $name = config("mail.from.name");

        $this->subject('New Article Published in Laravel ')
            ->view('emails.custom_template')
            ->from($address, $name);
      
        return $this;
    }
}
```

### Concept to add from address and name in email

Chaining of methods to send email in laravel with all values like subject, email template and from email address.

```swift
$this->subject("...")->view("...")->from($address, $name);
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/laravel-10-how-to-change-name-and-from-address-in-email/)