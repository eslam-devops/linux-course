جميل جدًّا يا إسلام
دلوقتي نخش على:

---

## 📄 `04_process_service.md`

````markdown
# ⚙️ Process & Service Management

في الدرس ده هنتعلم إزاي نراقب ونسيطر على العمليات (processes) والخدمات (services) في السيستم  
مفيش DevOps ولا Admin محترف ميعرفش يـ manage البروسيس والسيرفيسز  

---

## 🧠 يعني إيه Process؟

هي أي حاجة شغالة في السيستم:  
سكريبت – برنامج – سيرفيس

---

## 📌 أهم أوامر مراقبة العمليات

```bash
ps aux                # يعرض كل العمليات
ps -ef                # عرض تفصيلي برضو

top                   # مراقبة لحظية (real-time)
htop                  # نسخة متطورة (لو مش عندك: sudo apt install htop)

kill <PID>            # وقف عملية
kill -9 <PID>         # قتل إجباري
````

### مثال:

```bash
ps aux | grep nginx
kill 1234
```

---

## 🔥 أوامر مفيدة جدًّا:

```bash
pidof nginx           # يطبع رقم العملية بتاعة nginx
pgrep nginx           # زي pidof لكن تقدر تستخدمه في سكربت
pkill nginx           # يقتل كل عمليات nginx
```

---

## 🔄 Background & Foreground

```bash
command &             # يشغل حاجة في الخلفية
jobs                  # يعرض الحاجات اللي في الخلفية
fg %1                 # يرجع أول مهمة تشتغل في الواجهة
```

---

## 🧩 مراقبة موارد السيستم

```bash
uptime                # السيستم شغال بقاله قد إيه
free -h               # الذاكرة (RAM)
df -h                 # الديسك
du -sh *              # استهلاك فولدرات
iostat                # إحصائيات I/O (sudo apt install sysstat)
```

---

## 🧭 إدارة الخدمات (Services)

### النظام الحديث: `systemd`

```bash
systemctl status nginx       # حالة الخدمة
systemctl start nginx        # تشغيل
systemctl stop nginx         # وقف
systemctl restart nginx      # إعادة تشغيل
systemctl enable nginx       # يبدأ مع البوت
systemctl disable nginx      # متبدأش مع البوت
```

---

### الأنظمة القديمة:

```bash
service nginx status
```

---

## 🧠 تاسك عملي من الشغل:

1. شوف لو الخدمة `ssh` شغالة
2. وقفها وشغّلها تاني
3. شوف البروسيس اللي واخدة أكتر RAM
4. اقتل عملية معينة واكتبها في Log

---

## ⚠️ أخطاء بتحصل:

* استخدام `kill` على PID غلط ➜ ممكن تقفل حاجة مش بتاعتك
* نسيان `sudo` في `systemctl` ➜ “Access denied”
* استخدام `kill -9` بدون داعي ➜ يبوظ الترتيب في بعض السيستمز
* نسيان `enable` ➜ الخدمة متشتغلش مع البوت

---

## 🎯 تطبيق بسيط:

### سكربت يطمن على شوية خدمات أساسية:

```bash
#!/bin/bash

services=("ssh" "nginx" "cron")

for srv in "${services[@]}"
do
  systemctl is-active --quiet $srv
  if [ $? -eq 0 ]; then
    echo "$srv شغالة ✅"
  else
    echo "$srv واقفة ❌"
  fi
done
```

---

كده تمام معلم
لو جاهز نكمل
اللي بعده هيكون Networking Basics 🧠

ولا تحب تروح لـ SSH أو Cron؟
قول وأنا أظبطه ليك فورًا
# 🧰 Bash Scripting Basics

محتوى الدرس...
