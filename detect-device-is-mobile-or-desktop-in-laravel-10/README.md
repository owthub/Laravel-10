
## How To Detect Device is Mobile or Desktop in Laravel 10

Device detection in application is process in which you will the device information, browser information etc where your application runs.

Always developer or designer wants to know that whenever they open application, which device is being to used for it. So for this device detection concept, we will use jessenger agent laravel package.

### Install jessenger/ajent Package

Open project into terminal and run this command to install this device detection package.


```swift
$ composer require jenssegers/agent
```

It will install __jessenger/ajent__ package inside application.

### Usage of Detection Package

Before use of jenssegers/agent package, we need to create an instance.

```swift
$agent = new \Jenssegers\Agent\Agent;
```

Detect Mobile

```swift
$agent->isMobile();
```

Detect Laptop/Desktop

```swift
$agent->isDesktop();
```

Detect Tablet

```swift
$agent->isTablet();
```

### See Complete Article, [Click here](https://onlinewebtutorblog.com/how-to-detect-device-is-mobile-or-desktop-in-laravel-10/)