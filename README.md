# # recaptcha

สิ่งที่ต้องมี

1. คีย์ฝั่ง client
2. คีย์ฝั่ง Server

สมัครได้ที่

https://www.google.com/recaptcha/admin/create | https://www.google.com/recaptcha/admin/ | https://www.google.com/recaptcha/

โค้ดฝั่ง client (HTML)

Javascript ใส่ในแท็ก head
```html
<script async defer src="https://www.google.com/recaptcha/api.js"></script>
```

โค้ดกล่องให้ติ้กยืนยันวางในตำแหน่งที่ต้องการ
```html
<div class="g-recaptcha" data-sitekey="คีย์ฝั่ง client"></div>
```

โค้ดฝั่ง Server (PHP)

```php
<?php
define('secretkey', 'คีย์ฝั่ง Server');
$options = [
	'secret' => secretkey,
	'response' => filter_input(INPUT_POST, 'g-recaptcha-response'),
	'remoteip' => $_SERVER['REMOTE_ADDR']
];
$url = 'https://www.google.com/recaptcha/api/siteverify?'.http_build_query($options);
$result = json_decode(file_get_contents($url), true);
if ($result['success']) {
	//เพิ่มสิ่งที่จะทำเมื่อยืนยันตนถูก
}else{
	//เพิ่มสิ่งที่จะทำเมื่อยืนยันตนผิด
}
?>
```
