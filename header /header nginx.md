# header nginx


    # اجبار استفاده از HTTPS و جلوگیری از حملات Man-in-the-Middle
```bash
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
```
    # جلوگیری از تغییر نوع محتوای فایل‌ها توسط مرورگر (MIME sniffing)
```bash 
add_header X-Content-Type-Options "nosniff" always;
```
    # جلوگیری از بارگذاری سایت در iframe سایت‌های دیگر (Clickjacking)
```bash
add_header X-Frame-Options "SAMEORIGIN" always;
```
    # فعال‌سازی فیلتر محافظت در برابر XSS در مرورگرهای قدیمی‌تر
```bash
add_header X-XSS-Protection "1; mode=block" always;
```
    # تعیین سیاست ارسال referrer برای جلوگیری از افشای اطلاعات
```bash
add_header Referrer-Policy "no-referrer" always;
```
    # محدود کردن دسترسی به قابلیت‌های مرورگر مانند موقعیت مکانی و میکروفون
```bash
add_header Permissions-Policy "geolocation=(), microphone=()" always;
```
    # تعیین سیاست امنیت محتوا (CSP) برای محدود کردن منابع بارگذاری شده
```bash
add_header Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self'; object-src 'none'; base-uri 'self'; frame-ancestors 'none';" always;
```
    # جلوگیری از کش شدن صفحات حساس (اختیاری، برای صفحات خاص)
```bash
add_header Cache-Control "no-store, no-cache, must-revalidate, max-age=0" always;
add_header Pragma "no-cache" always;
```
  

### نمونه کامل برای nginx (در فایل کانفیگ سرور):

```bash

add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
add_header Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self'; object-src 'none'; base-uri 'self'; frame-ancestors 'none';" always;
add_header X-Frame-Options "DENY" always;
add_header X-Content-Type-Options "nosniff" always;
add_header Referrer-Policy "no-referrer" always;
add_header Permissions-Policy "geolocation=(), microphone=(), camera=()" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Cache-Control "no-store, no-cache, must-revalidate, max-age=0" always;
add_header Pragma "no-cache" always;

```

نکات تکمیلی
حتماً از HTTPS استفاده کن.

ورودی‌های کاربر را اعتبارسنجی و فیلتر کن.

محدودیت تعداد تلاش ورود (Rate Limiting) را فعال کن.

در صورت امکان احراز هویت دومرحله‌ای (2FA) فعال کن.

در صورت استفاده از فریم‌ورک یا CMS، افزونه‌های امنیتی را فعال نگه دار

server {
    # سایر تنظیمات سرور ...

    # اجبار استفاده از HTTPS و جلوگیری از حملات Man-in-the-Middle
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;

    # جلوگیری از تغییر نوع محتوای فایل‌ها توسط مرورگر (MIME sniffing)
    add_header X-Content-Type-Options "nosniff" always;

    # جلوگیری از بارگذاری سایت در iframe سایت‌های دیگر (Clickjacking)
    add_header X-Frame-Options "SAMEORIGIN" always;

    # فعال‌سازی فیلتر محافظت در برابر XSS در مرورگرهای قدیمی‌تر
    add_header X-XSS-Protection "1; mode=block" always;

    # تعیین سیاست ارسال referrer برای جلوگیری از افشای اطلاعات
    add_header Referrer-Policy "no-referrer" always;

    # محدود کردن دسترسی به قابلیت‌های مرورگر مانند موقعیت مکانی و میکروفون
    add_header Permissions-Policy "geolocation=(), microphone=()" always;

    # تعیین سیاست امنیت محتوا (CSP) برای محدود کردن منابع بارگذاری شده
    add_header Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self'; object-src 'none'; base-uri 'self'; frame-ancestors 'none';" always;

    # جلوگیری از کش شدن صفحات حساس (اختیاری، برای صفحات خاص)
    add_header Cache-Control "no-store, no-cache, must-revalidate, max-age=0" always;
    add_header Pragma "no-cache" always;

    # سایر تنظیمات سرور ...
}
