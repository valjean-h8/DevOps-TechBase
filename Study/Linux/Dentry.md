# Что такое dentry?
`dentry (directory entry)` - это **структура в памяти ядра**, которая представляет **одну связь между именем файла и его `inode`**.(`kernelnamespace`)

Проще говоря:
> `dentry` = file_name --> `inode`

```C
struct dentry {
  struct qstr d_name;           // имя
  struct inode *d_inode;        // указатель на inode
  struct dentry *d_parent;      // ссылка на родителя
  ...
};
```

Служит для **быстрого резолвинга путей** и **кеширования** имя → `inode`.