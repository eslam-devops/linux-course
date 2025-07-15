# 📁 File & Directory Commands

محتوى الدرس...

تمام يا نجم
نبدأ دلوقتي بملف:

---

## 📄 `01_file_directory_commands.md`

````markdown
# 📁 File & Directory Commands

الدرس ده بيغطي كل أوامر اللينكس الأساسية اللي بتستخدمها يوميًا في التنقل، إنشاء ملفات، تعديل، نقل، نسخ، مسح... إلخ
ركز في كل أمر لأنك هتحتاجه في أي شغل سواء Admin أو DevOps أو SecOps

---

## 🧭 التنقل جوه الفايل سيستم

```bash
pwd              # بتطبع المسار الحالي
cd /etc          # تدخل على فولدر معين
cd ~             # تدخل على الهوم
cd ..            # تطلع لفوق (الديركتوري الأب)
cd -             # ترجع للمكان اللي كنت فيه قبل كده
````

💡 لو عايز توصّل لمكان بسرعة:

```bash
cd /var/log/nginx/
```

---

## 📂 إنشاء ملفات وفولدرات

```bash
mkdir myfolder               # فولدر جديد
mkdir -p folder1/folder2     # يعمل الاتنين مرة واحدة
touch file.txt               # ملف فاضي جديد
```

---

## 📄 عرض الملفات والفولدرات

```bash
ls                        # يعرض اللي جوه
ls -l                     # عرض تفصيلي (permissions, size, date...)
ls -a                     # يعرض الملفات المخفية
ls -lh                    # human-readable size
ls -ltr                   # من الأقدم للأحدث
tree                      # عرض الشجرة (لو مش عندك نزله بـ apt install tree)
```

💡 alias مفيد:

```bash
alias ll='ls -alF'
```

---

## 📋 نسخ ونقل الملفات

```bash
cp file1.txt file2.txt        # نسخ
cp -r dir1 dir2               # نسخ فولدر بمحتواه
mv file.txt /tmp/             # نقل
mv old.txt new.txt            # إعادة تسمية
```

---

## ❌ مسح الملفات والفولدرات

```bash
rm file.txt                   # حذف ملف
rm -r myfolder/               # حذف فولدر بمحتواه
rm -rf *                      # حذف كل حاجة (خطر ⚠️)
```

🧠 مفيش سلة مهملات! لو مسحت حاجة خلاص راحت
اعمل نسخ احتياطي قبل ما تمسح حاجة مهمة

---

## 📌 قراءة محتوى الملفات

```bash
cat file.txt                  # يعرض الملف كله
less file.txt                 # يعرض بشكل page-by-page (q للخروج)
more file.txt                 # زيه تقريبًا
head -n 10 file.txt           # أول 10 سطور
tail -n 10 file.txt           # آخر 10 سطور
tail -f /var/log/syslog       # متابعة اللوج في الوقت الحقيقي
```

---

## 🔍 البحث عن الملفات

```bash
find . -name "*.log"              # كل ملفات اللوج في المسار الحالي
find /etc -type f -name "hosts"   # دور على ملف معين في /etc
locate nginx.conf                 # أسرع من find (بس لازم تعمل updatedb)
```

💡 قبل ما تستخدم `locate`:

```bash
sudo updatedb
```

---

## 🔀 إعادة توجيه وإخراج

```bash
echo "test" > file.txt         # يكتب جملة جوه ملف (يمسح القديم)
echo "line" >> file.txt        # يزود جملة جديدة في الآخر
cat file.txt | grep "ERROR"    # يفلتر سطور فيها ERROR
```

---

## 🧠 مثال عملي من الشغل:

#### سكريبت بسيط يشيك على ملفات مهمة:

```bash
#!/bin/bash

for file in /etc/hosts /etc/passwd /etc/resolv.conf
do
  if [ -f "$file" ]; then
    echo "✔️ $file موجود"
  else
    echo "❌ $file مش موجود"
  fi
done
```

اعمله:

```bash
chmod +x check_files.sh
./check_files.sh
```

---

## ❗ أخطاء شائعة:

* استخدام `rm -rf /` بالغلط ➜ بيبوظ السيستم
* نسيان المسار في `mv` ➜ ممكن تكتب فوق ملف تاني
* استخدام `cp` بدون `-r` مع فولدر ➜ مش هيشتغل
* نسيان `sudo` مع ملفات في `/etc`

---

## 🧪 تاسكات ليك:

* جرب تعمل فولدر فيه ملفات مختلفة
* انسخهم لفولدر تاني
* احذف ملف معين
* ابحث عن كل ملفات `.conf` في `/etc`
* اعمل ملف فيه لوج وجرب `tail -f`

---

كده خلصنا التوبيك التاني
لو جاهز أكتب لك التوبيك التالت:
`File Permissions & Ownership`؟
ولو تحب أجهزلك السكريبتات والملفات دي في فولدر جاهز ترفعه على GitHub قولي وأنا أظبطهولك على طول

