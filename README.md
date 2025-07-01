# SocialCAPI – Laravel Facebook CAPI Integration

**SocialCAPI** is a Laravel 11+ compatible package that provides a wrapper for sending Facebook Conversions API (CAPI) events server-side using the official [`facebook/php-business-sdk`](https://github.com/facebook/facebook-php-business-sdk). It is ideal for tracking conversions and interactions directly from your backend with support for `test_event_code`, dynamic data, and Laravel configuration management.

---

## 🚀 Features

- Laravel 11 compatible  
- Built on top of Facebook's official Business SDK  
- Supports `test_event_code` for development and QA validation  
- Fully dynamic input mapping for user data  
- Easily configurable via Laravel config and `.env`  
- Composer-installable, auto-discovered Laravel service provider  

---

## 📦 Installation

Install via Composer:

```bash
composer require mtechraw/social-capi
```

---

## 🛠 Configuration

### Step 1: Publish Configuration File

```bash
php artisan vendor:publish --tag=config
```

This will publish `config/fb-capi.php`:

```php
return [
    'pixel_id' => env('FB_PIXEL_ID'),
    'access_token' => env('FB_ACCESS_TOKEN'),
];
```

### Step 2: Set Environment Variables

Update your `.env` file:

```env
FB_PIXEL_ID=your_facebook_pixel_id
FB_ACCESS_TOKEN=your_fb_access_token
```

---

## ✅ Usage Example

You can use the `FacebookChannel` class directly using Laravel's container:

```php
use SocialCAPI\Facebook\FacebookChannel;

$data = [
    'email' => 'john@example.com',
    'ip' => '127.0.0.1',
    'city' => 'local',
    'state' => 'Texas',
    'country' => 'US',
    'event_name' => 'Purchase',
    'test_event_code' => 'TEST1234ABC', // Optional: for Facebook Events Manager test tab
];

app(FacebookChannel::class)->send($data);
```

---

## ⚙️ Advanced

### Supported Event Types

You can send any standard Facebook CAPI event type including:

- `Purchase`
- `InitiateCheckout`
- `Lead`
- `AddToCart`
- etc.

You only need to specify the event name in the `event_name` key.

### Dynamic Data Input

The input array can contain any of the following fields (optional, only what's provided will be sent):

- `email`
- `country`
- `city`
- `state`
- `ip`
- `event_name`
- `test_event_code`

---

## 🧪 Using test_event_code

To send a test event (visible in Facebook Events Manager → Test Events):

1. Go to Events Manager → your Pixel → Test Events  
2. Copy the test event code (e.g. `TEST1234ABC`)  
3. Add it in the `$data` array like:

```php
'test_event_code' => 'TEST1234ABC'
```

This event will appear in the Test Events tab for validation.

---

## 🧩 Folder Structure

```txt
social-capi/
├── config/
│   └── fb-capi.php
└── src/
    └── Facebook/
        ├── FBServiceProvider.php
        ├── FacebookChannel.php
        └── FacebookMessage.php
```

## 📘 License

MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🙋 Author

Developed with ❤️ by [Mukesh Rawat](https://github.com/mtechraw)