## Содержание
[Основы](#Основы)

## Основы

### Первоночальная настройка

Все настройки  
git config --list --show-origin

Установка пользователя  
git config --global user.name "user name"  
git config --global user.email user@example.com

Инициализация  
git intit

Клонирование  
git clone https://github.com/address

### Запись имзенений

Отслеживание изменений  
git add filename

Оменить изменения сделанные до staged  
git restore

Добавить в staged  
git add filename

Удалить файл и перестать отслеживать  
git rm

Игнорировать файлы  
.gitignore  
ignore all .a files  
`*.a`  
but do track lib.a, even though you're ignoring .a files above  
`!lib.a`  
only ignore the TODO file in the current directory, not subdir/TODO  
`/TODO`  
ignore all files in any directory named build  
`build/`  
ignore doc/notes.txt, but not doc/server/arch.txt  
`doc/*.txt`  
ignore all .pdf files in the doc/ directory and any of its subdirectories  
`doc/**/*.pdf`  

Посмотреть статус  
git status

### История коммитов
git log

### Отмена изменений
Изменить комментарий к последнему коммиту и добавить в него новые изменения. Например если сделал коммит, и понял что нужно добавить что-то еще в него же.
git commit --amend
