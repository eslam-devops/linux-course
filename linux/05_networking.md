# 🌐 Networking Basics in Linux

محتوى الدرس...
تمام يا نجم
ندخل على درس مهم لأي DevOps أو Admin:

---

## 📄 `05_networking.md`

````markdown
# 🌐 Networking Basics in Linux

في الشغل الحقيقي، مشاكل النت بتظهر كتير
لازم تبقى عارف تتصرف بسرعة
تشيّك البورتات، تتأكد من الاتصال، تبعت ريكوستات، تحل DNS، تفهم مين واصل لمين

---

## 🧠 أهم أوامر الشبكة في لينوكس

### 🔹 عنوان الجهاز:

```bash
hostname              # اسم الجهاز
hostname -I           # العنوان الداخلي (IP)
ip a                  # كل الكروت والـ IPs
````

### 🔹 الإتصال بالنت:

```bash
ping google.com              # تتأكد إن فيه إنترنت
ping 8.8.8.8                 # لو الشك في DNS
curl -I https://google.com   # يشوف الـ Headers
```

---

## 📌 أوامر فحص الشبكة:

### 🔹 مين شغال على أنهى بورتات:

```bash
ss -tuln                  # أسرع من netstat
netstat -tulnp            # لو موجود (apt install net-tools)
```

معاني الخيارات:

* `t`: TCP
* `u`: UDP
* `l`: listening
* `n`: أرقام بدل أسماء
* `p`: يجيب اسم البروسيس

---

### 🔍 مثال:

```bash
ss -tuln | grep 80
```

➜ هل فيه سيرفر Web شغال على بورت 80؟

---

### 🔹 معرفة حالة الاتصال:

```bash
ip r                     # الراوتينج
traceroute google.com   # خطوات التوصيل (apt install traceroute)
mtr google.com          # دمج بين ping + traceroute (رهيب)
```

---

## 🧪 أوامر بتستخدم في CI/CD والشغل:

### 🔹 تحميل ملفات:

```bash
wget https://example.com/file.zip
curl -O https://example.com/file.zip
```

### 🔹 إرسال ريكوست:

```bash
curl https://api.example.com/data
curl -X POST -d '{"name":"eslam"}' -H "Content-Type: application/json" https://api.site.com
```

---

## 🔒 فحص بورتات:

```bash
nc -zv localhost 22       # فحص بورت SSH
```

لو مش عندك `nc`:

```bash
sudo apt install netcat
```

---

## 🧠 مثال عملي:

#### سكربت يشوف لو بورت معين مفتوح:

```bash
#!/bin/bash

host="localhost"
port=22

nc -z $host $port
if [ $? -eq 0 ]; then
  echo "✅ البورت $port مفتوح"
else
  echo "❌ البورت $port مقفول"
fi
```

---

## ⚠️ أخطاء شائعة:

* ping شغال لكن curl لأ ➜ DNS شغال بس السيرفر مش بيرد
* curl بيشتكي من SSL ➜ ممكن تستخدم `-k` لتخطي التحقق (خطر في الإنتاج)
* ما تشوفش البورت في `ss` ➜ السيرفر مش شغال، أو مش بـ listen على كل الـ IPs

---

## 🧪 تمرين عملي ليك:

1. شوف عنوان IP بتاع جهازك
2. Ping على أي موقع خارجي
3. شوف كل البورتات المفتوحة
4. curl على موقع وهمي وجيب الـ status code
5. اعمل سكربت يشيك على بورتات 80 و443 و22

---

لو تمام كده
اللي بعده ممكن يكون:

* SSH & Passwordless Login
* Cron Jobs & Scheduling
* Monitoring & Logs

اختار اللي تحب نكمل بيه
وقولي كمان لو تحب أبدأ أجهزلك فولدر `.zip` بكل الملفات اللي عملناها لحد دلوقتي ترفعه على GitHub

