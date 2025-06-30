# Что такое `dirent`?

`dirent` - это запись каталога в пользовательском пространстве. (`usernamespace`)
```C
struct dirent {
    ino_t          d_ino;    // номер inode
    off_t          d_off;    // смещение на следующую запись в каталоге
    unsigned short d_reclen; // длина этой записи
    unsigned char  d_type;   // тип объекта (DT_REG, DT_DIR, DT_LNK и т.д.)
    char           d_name[]; // имя (нуль-терминированная строка)
};

```