## Содержание
[Настройка](#Настройка)

## Настройка

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

Оменить изменения до staged  
git restore

Добавить в staged  
git add filename

Удалить файл из отслеживания  
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
