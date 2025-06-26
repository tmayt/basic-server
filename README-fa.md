# 🐳 مدیر سرور داکریزه شده

این مخزن شامل فایل `docker-compose.yml` است که راه‌اندازی می‌کند:

- [سرور DNS تکنیتیوم (Technitium DNS Server)](https://github.com/TechnitiumSoftware/DnsServer)
- [مدیر معکوس‌پراکسی Nginx (Nginx Proxy Manager)](https://github.com/NginxProxyManager/nginx-proxy-manager)

ابزاری مفید برای رزولوشن محلی DNS و مدیریت آسان پراکسی معکوس با پشتیبانی از Let's Encrypt.

---

## 🚀 شروع سریع

### ۱. کلون کردن مخزن

```bash
git clone https://github.com/your-username/your-repo.git
cd basic-server
```

### ۲. راه‌اندازی سرویس‌ها

```bash
docker compose up -d
```

این دستور سرویس‌های زیر را راه‌اندازی می‌کند:

* سرور DNS تکنیتیوم روی پورت `5380`
* مدیر معکوس‌پراکسی Nginx روی پورت‌های `80`، `81` و `443`
* MariaDB به عنوان پایگاه داده برای NPM

---

## 🌐 دسترسی به برنامه‌ها

### 🧠 سرور DNS تکنیتیوم

* **آدرس:** [http://localhost:5380](http://localhost:5380)

### 🛠️ مدیر معکوس‌پراکسی Nginx (NPM)

* **آدرس:** [http://localhost:81](http://localhost:81)
* نام کاربری و رمز عبور پیش‌فرض:

  * **ایمیل:** `admin@example.com`
  * **رمز عبور:** `changeme`

> ⚠️ حتماً بعد از اولین ورود، این اطلاعات را تغییر دهید.

---

## ⚙️ اجرای برنامه وب خودتان

شما می‌توانید برنامه وب خود را روی **هر پورتی** اجرا کنید، مثلاً:

```bash
docker run -d -p 3000:3000 your-app-image
```

سپس:

1. وارد **مدیر معکوس‌پراکسی Nginx** شوید ([http://localhost:81](http://localhost:81))
2. **یک هاست پراکسی جدید اضافه کنید**:

   * دامنه: your-domain.com
   * میزبان/آی‌پی مقصد: `host.docker.internal` (برای برنامه‌های محلی)
   * پورت مقصد: `3000` (یا پورتی که برنامه شما استفاده می‌کند)
3. در صورت تمایل، SSL را با Let's Encrypt فعال کنید

---

## 🌍 اتصال دامنه به جهان از طریق DNS

1. وارد **سرور DNS تکنیتیوم** شوید ([http://localhost:5380](http://localhost:5380))
2. **یک زون جدید** برای دامنه خود بسازید (مثلاً `your-domain.com`)
3. رکوردهای A را برای دامنه یا زیر دامنه‌های خود به آی‌پی عمومی خود تنظیم کنید
4. (اختیاری) رکوردهای CNAME، TXT یا MX مورد نیاز را اضافه کنید

پس از پیکربندی و در صورتی که دامنه شما از سرور DNS تکنیتیوم به عنوان DNS معتبر استفاده کند (یا آن را به عنوان رزولور محلی تنظیم کنید)، ترافیک به درستی به سرویس‌های محلی شما از طریق مدیر معکوس‌پراکسی Nginx هدایت خواهد شد.

---

## 🛑 متوقف کردن سرویس‌ها

```bash
docker compose down
```

---

## 🗂️ حجم‌های ذخیره‌سازی استفاده شده

* `dns_data`: داده‌های پایدار سرور DNS
* `app_data`: تنظیمات و داده‌های SSL برای NPM
* `npm_db_data`: ذخیره‌سازی پایگاه داده MariaDB

---

## 📝 پیش‌نیازها

* [داکر (Docker)](https://docs.docker.com/get-docker/)
* [داکر کامپوز (Docker Compose)](https://docs.docker.com/compose/)

