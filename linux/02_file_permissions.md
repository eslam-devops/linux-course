# 🔐 File Permissions & Ownership

محتوى الدرس...
جميل جدًا يا نجم 👌
يلا بينا ندخل على تاني قسم وده من أهم وأخطر الحاجات في لينكس
لإن موضوع الـ Users والصلاحيات هو قلب أي سيستم شغال، سواء شغال DevOps أو System Admin أو حتى SecOps 🔐

---

## 🔐 2. المستخدمين والصلاحيات

### 🎯 هدفك هنا:

* تبقى فاهم إزاي تضيف مستخدمين وتتحكم فيهم
* تمنع أي حد يبوظ السيستم
* تدي صلاحيات بالراحة وبحذر

---

### 👤 `whoami` – بيقولك إنت مين

```bash
whoami
```

✅ لو مش فاكر إنت داخل بأي يوزر، ده بيفكرك
📌 مفيد لو بتتنقل بين users في الشغل

---

### 👥 `id` – بيعرض معلومات اليوزر

```bash
id
```

✅ بيجيبلك UID و GID والمجموعات اللي إنت فيها

---

### 👤 `sudo` – استخدم صلاحيات الأدمن مؤقتًا

```bash
sudo ls /root
```

✅ بتستخدمه في أي أمر محتاج صلاحيات Root
💡 تقدر تضيف يوزر لقائمة الـ sudoers

---

### 👷‍♂️ `useradd` – لإنشاء يوزر جديد

```bash
sudo useradd -m yahia
```

✅ بيعمل يوزر جديد اسمه yahia ومعاه home folder

💡 لو عايز تحدد الشيل بتاعه:

```bash
sudo useradd -m -s /usr/bin/python yahia
```

⚠️ لو محددتش `-m` مش هيعمله home folder

---

### 🔐 `passwd` – لتغيير باسورد يوزر

```bash
sudo passwd yahia
```

هيطلب منك تدخل الباسورد مرتين
💡 أو بطريقة أسرع في بيئة Red Hat:

```bash
echo "redhat55" | sudo passwd --stdin yahia
```

✅ أمر محترف جدًا وبيستخدم في سكريبتات Ansible ومهام الـ automation

---

### ❌ `userdel` – حذف يوزر

```bash
sudo userdel yahia
```

💡 لو عايز تحذف الهوم فولدر كمان:

```bash
sudo userdel -r yahia
```

---

### 👨‍👩‍👧‍👦 `groupadd` – إنشاء جروب جديد

```bash
sudo groupadd devops
```

### ➕ إضافة يوزر لجروب

```bash
sudo usermod -aG devops yahia
```

💡 خد بالك من الـ `-aG` دي مهمة عشان ميتمسحش من باقي الجروبات

---

### 📄 صلاحيات الملفات: `chmod` و `chown`

#### 🛡️ `chmod` – تعديل صلاحيات الملف

```bash
chmod 755 script.sh
```

✅ 7 = read + write + execute
✅ 5 = read + execute
📌 هنتكلم بتفصيل أكتر قدام في Permissions

#### 🧑‍🏭 `chown` – تغيير صاحب الملف

```bash
sudo chown yahia file.txt
```

---

### ✅ خطواتك المنفذة لحد دلوقتي:

* [x] whoami
* [x] id
* [x] sudo
* [x] useradd
* [x] passwd
* [x] userdel
* [x] groupadd
* [x] usermod
* [x] chmod
* [x] chown

---

### 🧠 مراجعة سريعة:

1. إزاي تعمل يوزر جديد وتحددله الشيل بتاعه؟
2. يعني إيه `--stdin` في أمر `passwd`؟
3. إزاي تضيف يوزر لجروب موجود؟
4. لو عايز تمنح صلاحيات تنفيذ لملف سكريبت، تستخدم إيه؟
5. الفرق بين `userdel` و `userdel -r`؟
تعالى نجاوب واحدة واحدة وباللهجة المصرية 👇

---

👤 **إزاي تعمل يوزر جديد وتحددله الشيل بتاعه؟**

```bash
sudo useradd -s /bin/bash eslam
```

✅ `-s` معناها تختار الشيل (shell) اللي هيشتغل بيه اليوزر
🧠 مثال تاني لو عايز yahiya يستخدم Python كـ shell:

```bash
sudo useradd -s /usr/bin/python yahiya
```

---

🔐 **يعني إيه `--stdin` في أمر `passwd`؟**

`--stdin` بتخلي الأمر `passwd` ياخد الباسورد من الـ input بدل ما يطلبه منك

يعني لو عايز تعمل سكريبت يحط باسورد من غير تدخل يدوي:

```bash
echo "mypassword" | sudo passwd --stdin eslam
```

📌 المفيد في السكريبتات أو الـ automation
لكن خلي بالك مش كل توزيعة بتدعم `--stdin`

---

👥 **إزاي تضيف يوزر لجروب موجود؟**

```bash
sudo usermod -aG groupname username
```

✅ `-aG` معناها append to group
🧠 مثال:

```bash
sudo usermod -aG docker eslam
```

يعني بتخلي eslam يشتغل مع مجموعة docker

---

⚙️ **لو عايز تمنح صلاحيات تنفيذ لملف سكريبت، تستخدم إيه؟**

```bash
chmod +x script.sh
```

✅ `+x` معناها "خلي الملف executable"
🧠 بعد كده تقدر تشغله كده:

```bash
./script.sh
```

---

❌ **الفرق بين `userdel` و `userdel -r`؟**

* `userdel eslam`:
  بيمسح اليوزر من السيستم بس **بيسيب الهوم فولدر وملفاته**

* `userdel -r eslam`:
  بيمسح اليوزر **وكمان** بيمسح الهوم فولدر بتاعه وكل ملفاته

📌 دا مهم لو بتنضف السيرفر من ناس مش محتاجة تفضل فيه

---

---
