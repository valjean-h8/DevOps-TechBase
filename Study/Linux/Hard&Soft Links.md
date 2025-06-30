`hardlink` (жесткие ссылки)
```bash
touch file.txt
echo "Hardlink" > file.txt

ln file.txt hardlink.txt

ls -li *.txt # одинаковые `inodes`
1309381 -rw-rw-r-- 2 valjean valjean 9 Jun 30 08:56 file.txt
1309381 -rw-rw-r-- 2 valjean valjean 9 Jun 30 08:56 hardlink.txt

rm file.txt 

ls -li *.txt
1309381 -rw-rw-r-- 1 valjean valjean 9 Jun 30 08:56 hardlink.txt

cat hardlink.txt 
Hardlink

```

Жесткая ссылка копирует `inode` файла и даже при удалении оригинала, содержимое останется.

**Поправочка!**
>`rm` удаляет имя файла, но не само содержимое на диске.
>Только когда счётчик ссылок `inode` становится нулём И ни один процесс не держит файл открытым, тогда ядро освобождает блоки данных и сам `inode`. ==> Пока хотя бы одна жесткая ссылка указывает на тот же **`inode`** - **данные продолжают существовать.**

---

`softlink` (мягкие/символические ссылки)
```bash
touch file.txt
echo "Softlink" > file.txt

ln -s file.txt softlink.txt

ls -li *.txt # разные `inodes`
1309381 -rw-rw-r-- 1 valjean valjean 9 Jun 30 09:01 file.txt
1327650 lrwxrwxrwx 1 valjean valjean 8 Jun 30 09:01 softlink.txt -> file.txt


rm file.txt

ls -li *.txt
1327650 lrwxrwxrwx 1 valjean valjean 8 Jun 30 09:01 softlink.txt -> file.txt

cat softlink.txt 
cat: softlink.txt: No such file or directory

```

Мягкая ссылка создаёт ярлык на оригинал, и при удалении оригинала она не работает, становится "битой" (broken).

> К тому же мягкая ссылка может ссылаться и на каталоги, а жесткая нет!

```bash
mkdir CheckLinks

ln CheckLinks/ hardlink
ln: CheckLinks/: hard link not allowed for directory

ln -s CheckLinks/ softlink

ls -li
total 4
2105469 drwxrwxr-x 2 valjean valjean 4096 Jun 30 09:15 CheckLinks
2109602 lrwxrwxrwx 1 valjean valjean   11 Jun 30 09:16 softlink -> CheckLinks/
```

# Когда что использовать?
- `Hardlink` - отличный способ "переименовать" файл без дублирования данных;
- `Softlink` - удобна когда нужно сделать ссылку на директорию.