> В данном задании выполненно изучение структуры каталогов Linux и прав доступа.

- - -

## Шаг 1. Создание структуры каталогов

Для начала работы нам необходимо сменить директорию:

```bash
sudo su # переходим в режим суперпользователя root.
cd /opt # переходим в нужную нам дерикторию opt.
```

Далее нам необходимо создать сами папки:

```bash
mkdir -p scripts/logs/backup/configs # Команда mkdir  с ключом -p поможет нам создать последовательно все нужные нам каталоги в этой директории.
```

Проверим созздание директорий:

```bash
ls -r # Выдаст нам один каталог первый в нашем списке scripts а значит остальные либо не создались либо внутри нее, попробуем командой apt install tree, установить tree чтобы посмотреть все дерево файлов и увидим что каталоги создались последовательно внутри каждой из папок в каком порядке мы их и задали.
```

Вывод команды:

```plaintext

root@serv1:/opt# ls -r
scripts  logs  configs  backup

```

Исправляем ошибку и удаляем ошибочные директории:

```bash
rm -r scripts # удаляем все каталоги в том чиле котоорые вложены друг в друге и проверяем командой tree.
```

Снова пытаюсь создать дериктории правильно:

```bash
mkdir -p scripts,logs,backup,configs # попробывал слздать через запятую, но понял что это просто назавание одного каталога черерз запятую, снова удаляем.
```

Понял как правильно создовать директории:

```bash
mkdir scripts logs backup configs # и проверяем через tree видим что теперь у нас 5 дерикторий в одном каталоге opt.
```

Создаем файл README.md:

```bash
nano README.md # создаем файл с раширением мд с помощью команды nano и сохраняем ctrl+o, и выходим ctrl+x, проверяем через free видим что появился файл с нужным расширением.
```

Создаем файл notes.txt:

```bash
nano notes.txt # так же создаю файл с расширением txt.
```

Создаем файл scripts.sh и проверяем, смотрим что получилось:

```bash
nano scripts.sh # и с расширением sh и смотрю через tree что у нас получилось 3 файла с разными расширениями, есть еще команды echo которая записывает текст в файл при создании и touch которая создает пустой файл, а nano отличается тем что мы сразу редактируем текст внутри файла при создании.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# nano README.md
root@serv1:/opt/training# nano notes.txt
root@serv1:/opt/training# nano scripts.sh
root@serv1:/opt/training# tree
.
├── backup
├── configs
├── logs
├── notes.txt
├── README.md
├── scripts
└── scripts.sh

```


Создаем ссылку на определенный файл:

```bash
ln -s notes.txt. notes_link.txt # этой командой создаем ссылку и указываем где она будет, еще можно указать ей полный путь в дерикторию и нде она будет хрониться например /opt/notes.txt opt/notes_link.txt
```

Проверяем работоспособность ссылки:

```bash
ls -l notes_link.txt # проверяем создалась и работает ли ссылка.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# ln -s notes.txt notes_link.txt
root@serv1:/opt/training# ls -l
total 16
drwxr-xr-x 2 root root 4096 Jul 30 14:28 backup
drwxr-xr-x 2 root root 4096 Jul 30 14:28 configs
drwxr-xr-x 2 root root 4096 Jul 30 14:28 logs
lrwxrwxrwx 1 root root    9 Jul 30 14:44 notes_link.txt -> notes.txt
-rw-r--r-- 1 root root    0 Jul 30 14:40 notes.txt
-rw-r--r-- 1 root root    0 Jul 30 14:39 README.md
drwxr-xr-x 2 root root 4096 Jul 30 14:28 scripts
-rw-r--r-- 1 root root    0 Jul 30 14:41 scripts.sh
```


Заметил ошибку в директории:

```bash
mkdir training # я заметил что проебался и не создал каталог training  значит в него переносим все каталоги и файлы которые находяться в opt.
```
Исправляю ощибку переносом директорий и файлов:

```bash
mv /opt/backup /opt/training # начнем с первого каталога и выдает ошибку о том что он не нашел файлы в этой директрии которые надо перенести, но при этом перенес сам коттолог в training после проверки командой tree -a, 
```

```bash
mv /opt/configs /opt/training # так же перенесоим каталог и теперь все пернеосится без проблем видимо он обращал внимание что в директории не было файлов.
```

```bash
mv /opt/logs /opt/training # так же переносим
```

```bash
mv /opt/scripts /opt/training  
```

```bash
mv /opt/notes.txt /opt/training 
```

```bash
mv /opt/README.md /opt/training 
```

```bash
mv /opt/scripts.sh /opt/training >
```

Перенес ссылку:

```bash
mv /opt/notes_link.txt /opt/training # ссылку тоже надо перенести посокльку сам файл тоже перенесся, проверяем командой tree -a все файлы и дериктории лежат в дериктории training как и говорилось в задании.
```

Смотрим права README.md и какие мы должны получить:

```bash
ls -l /opt/training # покажет нам все права у всех файлов и декректорий в дериктории training, мы видим что по заданию у README.md 644 (4+2,4,4)права а это значит -rw-r--r-- тоесть файл уже с этими правами значит переназначаем остальные
```

Вывод команды:

```plaintext
root@serv1:/opt/training# ls -l
total 16
drwxr-xr-x 2 root root 4096 Jul 30 14:28 backup
drwxr-xr-x 2 root root 4096 Jul 30 14:28 configs
drwxr-xr-x 2 root root 4096 Jul 30 14:28 logs
lrwxrwxrwx 1 root root    9 Jul 30 14:44 notes_link.txt -> notes.txt
-rw-r--r-- 1 root root    0 Jul 30 14:40 notes.txt
-rw-r--r-- 1 root root    0 Jul 30 14:39 README.md
drwxr-xr-x 2 root root 4096 Jul 30 14:28 scripts
-rw-r--r-- 1 root root    0 Jul 30 14:41 scripts.sh
```

Разобрался почему не смог нормально переходить в директорию:


```bash
cd /training # попытался провалится в след дерикторию но сделал это через слэш поэтому не получилось, убираем его и попадаем в training.
```

Меняю права владельцу файла scripts.sh:

```bash
chmod u+x scripts.sh # добавили владедьцу файла выполнеение (1) получается 7.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# chmod u+x scripts.sh
root@serv1:/opt/training# ls -n
total 16
drwxr-xr-x 2 0 0 4096 Jul 30 14:28 backup
drwxr-xr-x 2 0 0 4096 Jul 30 14:28 configs
drwxr-xr-x 2 0 0 4096 Jul 30 14:28 logs
lrwxrwxrwx 1 0 0    9 Jul 30 14:44 notes_link.txt -> notes.txt
-rw-r--r-- 1 0 0    0 Jul 30 14:40 notes.txt
-rw-r--r-- 1 0 0    0 Jul 30 14:39 README.md
drwxr-xr-x 2 0 0 4096 Jul 30 14:28 scripts
-rwxr--r-- 1 0 0    0 Jul 30 14:41 scripts.sh
```

Меняю права группы файла и остальных:


```bash
chmod go+x scripts.sh # добавили группе и остальным пользователям выполнение получилась 5.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# chmod go+x scripts.sh
root@serv1:/opt/training# ls -n
total 16
drwxr-xr-x 2 0 0 4096 Jul 30 14:28 backup
drwxr-xr-x 2 0 0 4096 Jul 30 14:28 configs
drwxr-xr-x 2 0 0 4096 Jul 30 14:28 logs
lrwxrwxrwx 1 0 0    9 Jul 30 14:44 notes_link.txt -> notes.txt
-rw-r--r-- 1 0 0    0 Jul 30 14:40 notes.txt
-rw-r--r-- 1 0 0    0 Jul 30 14:39 README.md
drwxr-xr-x 2 0 0 4096 Jul 30 14:28 scripts
-rwxr-xr-x 1 0 0    0 Jul 30 14:41 scripts.sh
```

Проверяю правильно ли я сделал и поменял права:


```bash
ls -l /opt/training # проверили все совпадает -rwxr-xr-x 755.
```

Меняю тагже правила для файла backup:

```bash
chmod go-rx backup # поскольку у группы и остальных пользователей были права на чтение и выполнение убираем их и получаем 700 drwx------.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# chmod go-rx backup
root@serv1:/opt/training# ls -n
total 16
drwx------ 2 0 0 4096 Jul 30 14:28 backup
```

Смотрим кто владелец и какаие права у файлов:


```bash
ls -ld /opt/training # можем посмотреть кто владелец директории и группы и какие у него права в нашем случае владелец root.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# ls -ld /opt/training
drwxr-xr-x 6 root root 4096 Jul 30 14:44 /opt/training
```

Таже команда для просмотра прав но с большой информацией:

```bash
stat /opt/training # подробная информация об валдельце директории о правах и изминениях а так же UID.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# stat /opt/training
  File: /opt/training
  Size: 4096            Blocks: 8          IO Block: 4096   directory
Device: 8,2     Inode: 1310727     Links: 6
Access: (0755/drwxr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2026-07-30 14:44:26.943277035 +0000
Modify: 2026-07-30 14:44:19.470314285 +0000
Change: 2026-07-30 14:44:19.470314285 +0000
 Birth: 2026-07-30 14:32:40.437868284 +0000
```

- - -
## Шаг 2. Смена и создание пользователя, и группы.
- - -

Добавляем нового пользователя:

```bash
adduser student # добавляем пользователя студент и насколько я могу увидеть он добавляется сразу в новая группа студент.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# adduser student
info: Adding user `student' ...
info: Selecting UID/GID from range 1000 to 59999 ...
info: Adding new group `student' (1001) ...
info: Adding new user `student' (1001) with group `student (1001)' ...
info: Creating home directory `/home/student' ...
info: Copying files from `/etc/skel' ...
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for student
Enter the new value, or press ENTER for the default
        Full Name []:
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
Is the information correct? [Y/n]
info: Adding new user `student' to supplemental / extra groups `users' ...
info: Adding user `student' to group `users' ...
```

Добовляем новую группу:

```bash
addgroup devops #  создание группы, можно было сразу при создании пользователя добавить его в эту группу с помощью ключа -g.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# addgroup
fatal: Only one or two names allowed.
root@serv1:/opt/training# addgroup devops
info: Selecting GID from range 1000 to 59999 ...
info: Adding group `devops' (GID 1002) ...
```

Добовляем пользователя в новую группу devops:

```bash
usermod -g devops student # лобавляем пользователя не закрепляя его в старых группах.
```

Меняю владельца директории ивсех файлов в ней:

```bash
chown -R student:devops /opt/training # меняем владельца директории и всех каталогов с файлами на нового владельца student  и группу devops
```

Проверяю поменялся ли пользователь:

```bash
ls -ld /opt/training # провреяем и видим что новый пользователь студент с группой девопс.
```

Вывод команды:

```plaintext
root@serv1:/opt/training# chown -R student:devops /opt/training
root@serv1:/opt/training# ls -ld /opt/training
drwxr-xr-x 6 student devops 4096 Jul 30 14:44 /opt/training
```

Вывод команды:

```bash
ls -l
```


```plaintext
root@serv1:/opt/training# ls -l
total 16
drwx------ 2 student devops 4096 Jul 30 14:28 backup
drwxr-xr-x 2 student devops 4096 Jul 30 14:28 configs
drwxr-xr-x 2 student devops 4096 Jul 30 14:28 logs
lrwxrwxrwx 1 student devops    9 Jul 30 14:44 notes_link.txt -> notes.txt
-rw-r--r-- 1 student devops    0 Jul 30 14:40 notes.txt
-rw-r--r-- 1 student devops    0 Jul 30 14:39 README.md
drwxr-xr-x 2 student devops 4096 Jul 30 14:28 scripts
-rwxr-xr-x 1 student devops    0 Jul 30 14:41 scripts.sh
```

Вывод команды:

```bash
groups student
```

```plaintext
root@serv1:/opt/training# groups student
student : devops users
```

Вывод команды:

```bash
id student
```

```plaintext
root@serv1:/opt/training# id student
uid=1001(student) gid=1002(devops) groups=1002(devops),100(users)
```

```bash
/etc # каталог для системных файлов и служб.
```

```bash
/var # место для записи системных журналов и логов.
```

```bash
/opt # каталог для сторонних приложений и данных.
```

```bash
/user # пользовательские ффайлы и приложения 
```

```bash
/tmp # временные файлы после ребута удаляются.
```

```bash
/home # личные файлы пользователя а также учетка.
```

```bash
chmode # это изменение прав владельца, группы и остальных.
```

```bash
chown # это изменение самого владельца директории или группы всех файлов.
```

```bash
drwxr-xr-x # директория владелец обладает правами на чтение запись и выполенение, группа на чтение и выполнение остальные тоже самое.
```