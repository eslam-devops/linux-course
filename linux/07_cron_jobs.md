# ⏰ Cron Jobs & Scheduling in Linux

محتوى الدرس...
تمام يا ملك
نخش دلوقتي على:

---

## 📄 `07_cron_jobs.md`

````markdown
# 🧠 Cron Jobs & Scheduling in Linux

الكرون هو السيستم اللي بيخلّي اللينكس يشغل سكريبت أو أمر في وقت معين أو بشكل دوري
زي مثلًا:
- باك آب كل يوم
- مسح لوجات قديمة
- تشغيل سكريبت كل ساعة

---

## ✅ إيه هو الـ `cron`؟

- cron: الخدمة اللي بتشغل المهام
- crontab: الملف اللي بتحط فيه المهام بتاعتك

---

## 🔍 عرض الكرون بتاعك

```bash
crontab -l
````

➜ يعرض المهام المجدولة لليوزر الحالي

---

## ✍️ تعديل الكرون:

```bash
crontab -e
```

➜ هيفتحلك محرر النصوص (عادة nano)

---

## ⏰ شكل الجملة في الكرون:

```
* * * * * command
| | | | |
| | | | └──── يوم الأسبوع (0 = الأحد)
| | | └────── الشهر (1 - 12)
| | └──────── اليوم (1 - 31)
| └────────── الساعة (0 - 23)
└──────────── الدقيقة (0 - 59)
```

---

### 🎯 أمثلة حقيقية:

| الوقت                   | الأمر                  |
| ----------------------- | ---------------------- |
| كل دقيقة                | `* * * * * command`    |
| كل يوم 5 صباحًا         | `0 5 * * * command`    |
| كل يوم أحد الساعة 2     | `0 2 * * 0 command`    |
| كل 15 دقيقة             | `*/15 * * * * command` |
| كل ساعة في أول 10 دقايق | `0-10 * * * * command` |

---

### 👨‍💻 مثال عملي:

شغل سكريبت كل يوم الساعة 1 الظهر:

```bash
0 13 * * * /home/eslam/scripts/backup.sh
```

---

## 📂 ملاحظة:

كل أوامر الكرون لازم تبقى فيها المسارات كاملة
يعني بدل `myscript.sh` ➜ استخدم `/home/eslam/myscript.sh`

---

## 🔁 تشغيل كذا كماند في نفس الوقت:

```bash
0 0 * * * command1 && command2
```

---

## 📦 كرون للـ Root:

لو عايز تضيف لـ root:

```bash
sudo crontab -e
```

---

## 📁 ملفات الكرون موجودة في:

```bash
/var/spool/cron/crontabs
/etc/crontab
/etc/cron.d/
/etc/cron.daily/
/etc/cron.hourly/
```

---

## 🛠️ Debug & Logging:

عايز تتأكد إن السكريبت اشتغل؟
ضيف Log زي ده:

```bash
0 6 * * * /home/eslam/clean.sh >> /var/log/clean.log 2>&1
```

---

## ❗ أخطاء بتحصل:

* نسيان المسار الكامل للسكريبت ➜ مش هيشتغل
* السكريبت مش قابل للتنفيذ ➜ لازم `chmod +x`
* نسيت تضيف `SHELL` ➜ ممكن تضيفه في أول ملف الكرون:

```bash
SHELL=/bin/bash
```

---

## 🧪 تمرين عملي ليك:

1. اعمل سكريبت بيطبع التاريخ في ملف
2. خليه يتشغل كل دقيقة
3. شوف اللوج وتأكد إنه بيزيد
4. عدّل الوقت ليشتغل كل 5 دقايق
5. وقف الكرون وشوف بيوقف ولا لأ

---

## 🔁 أمر مفيد عالسريع:

```bash
watch -n 60 tail -n 5 /var/log/syslog
```

➜ يراقب آخر لوجات الكرون كل دقيقة

---

كده خلصنا أهم أدوات الجدولة التلقائية في Linux

اللي جاي:

* 📊 Monitoring & Logs (نراقب السيستم من غير أدوات)
* أو تبدأ نبص على Ansible

قولي نروح على انهي اتجاه
وجاهز أجهزلك `.zip` بكل الملفات دي وREADME مرتب ترفعه على GitHub؟

