## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
Инициализация переменных
```ShellSession
$ export GITHUB_USERNAME=CrazyOverdose              #Инициализация переменной GITHUB_USERNAME
$ export GITHUB_EMAIL=alenkavh@yandex.ru            #Инициализация переменной GITHUB_EMAIL
$ export GITHUB_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxx #Инициализация переменной GITHUB_TOKEN
$ alias edit=nano                                   #Установка синонима команды edit
```
Подготовка рабочего пространства
```ShellSession
$ cd ${GITHUB_USERNAME}/workspace                      # Переход в папку workspace
$ source scripts/activate                              # Выполнение скрипта подготовки
```
Конфигурация hub
```ShellSession
$ mkdir ~/.config                           # Создание каталога с конфигурационными файлами
mkdir: невозможно создать каталог «/home/absinthetoxin/.config»: Файл существует
$ cat > ~/.config/hub <<EOF                 # Создание файла конфига hub и запись в него
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https            # Ининциализация переменной конфига git
```
Работа с git
```ShellSession
$ mkdir projects/lab02 && cd projects/lab02         # Создание каталога и переход в него
$ git init                                          # Инициальзация пустого репозитория
Инициализирован пустой репозиторий Git в
/home/absinthetoxin/CrazyOverdose/workspace/projects/lab02/.git/
$ git config --global user.name ${GITHUB_USERNAME}      
                                      # Инициальзация переменной конфига user.name для git
$ git config --global user.email ${GITHUB_EMAIL}                   
                                      # Инициальзация переменной конфига user.email для git
# check your git global settings
$ git config -e --global               # Вывод всего конфига из git

[hub]
        protocol = https
[user]
        name = CrazyOverdose
        email = alenkavh@yandex.ru
        
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git   
                                         # Добавление ссылки на репозиторий на GitHub
$ git pull origin master                 # Скачивание изменений с GitHub 
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (3/3), готово.
Из https://github.com/CrazyOverdose/lab02
 * branch            master     -> FETCH_HEAD
 * [новая ветка]     master     -> origin/master
$ touch README.md          # Создание README.md
$ git status               # Просмотр статуса репозитория

На ветке master
Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)

	README.md

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)

$ git add README.md                   # Добавление README.md в список фиксированных
$ git commit -m"added README.md"      # Добавление коммита фиксированных изменений

[master c9d334d] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md

$ git push origin master                 # Отправка изменений на GitHub 

Username for 'https://github.com': CrazyOverdose
Password for 'https://CrazyOverdose@github.com': 
Перечисление объектов: 4, готово.
Подсчет объектов: 100% (4/4), готово.
Сжатие объектов: 100% (2/2), готово.
Запись объектов: 100% (3/3), 284 bytes | 284.00 KiB/s, готово.
Всего 3 (изменения 0), повторно использовано 0 (изменения 0)
To https://github.com/CrazyOverdose/lab02.git
   c89adb6..7b17397  master -> master

```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```
Скачивание занесенных на GitHub изменений
```ShellSession
$ git pull origin master

remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (3/3), готово.
Из https://github.com/CrazyOverdose/lab02
 * branch            master     -> FETCH_HEAD
   7b17397..2acc764  master     -> origin/master
Обновление 7b17397..2acc764
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore


$ git log                                  # Просмотр коммитов

commit 2acc764fa34366a136cefb728fa6c8ac448fc49f (HEAD -> master, origin/master)
Author: CrazyOverdose <47750322+CrazyOverdose@users.noreply.github.com>
Date:   Sun Jun 9 16:24:55 2019 +0300

    Create .gitignore

commit 7b17397c4994ce38e16b22d3006ace21717f6923
Author: CrazyOverdose <alenkavh@yandex.ru>
Date:   Sun Jun 9 16:21:04 2019 +0300

    added README.md

commit c89adb6555a4f484937fc61ae6509cabe7e64d04
Author: CrazyOverdose <47750322+CrazyOverdose@users.noreply.github.com>
Date:   Sun Jun 9 16:14:40 2019 +0300

    Initial commit

```
Создание новых каталогов (один из них является файлом с кодом)
```ShellSession
$ mkdir sources                                       # Создание каталога
$ mkdir include
$ mkdir examples                                                                               
$ cat > sources/print.cpp <<EOF                       # Запись кода в файл
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```
Добавление файла с кодом в каталог
```ShellSession
$ cat > include/print.hpp <<EOF                   # Запись кода в файл
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```
Добавление файла с кодом в каталог
```ShellSession
$ cat > examples/example1.cpp <<EOF             # Запись кода в файл
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```
Добавление файла с кодом в каталог
```ShellSession
$ cat > examples/example2.cpp <<EOF              # Запись кода в файл
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```
Редактирование README.md
```ShellSession
$ edit README.md
```
Просмотр состояния репозитория и отправка изменений на GitHub
```ShellSession
$ git status

На ветке master
Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)

	examples/
	include/
	sources/

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)

$ git add .                      # Фиксирование всех изменений
$ git commit -m"added sources"   # Добавление коммита зафиксированных изменений

[master 67b30f3] added sources
 4 files changed, 32 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp

$ git push origin master           # Отправка изменений на GitHub 
Username for 'https://github.com': CrazyOverdose
Password for 'https://CrazyOverdose@github.com': 
Перечисление объектов: 10, готово.
Подсчет объектов: 100% (10/10), готово.
Сжатие объектов: 100% (7/7), готово.
Запись объектов: 100% (9/9), 968 bytes | 968.00 KiB/s, готово.
Всего 9 (изменения 0), повторно использовано 0 (изменения 0)
To https://github.com/CrazyOverdose/lab02.git
   2acc764..67b30f3  master -> master

```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=02
$ git clone 
https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```
