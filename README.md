## Laboratory work IV

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```ShellSession
$ open https://travis-ci.org
```

## Tasks

- [x] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
- [x] 2. Создать публичный репозиторий с названием **lab05** на сервисе **GitHub**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
- [x] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
- [x] 6. Получить фрагмент вставки значка сервиса **Travis CI** в формате **Markdown**
- [x] 7. Выполнить инструкцию учебного материала
- [x] 8. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
Установка переменных
```ShellSession
$ export GITHUB_USERNAME=CrazyOverdose
$ export GITHUB_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
Подготовка рабочего пространства
```ShellSession
$ cd ${GITHUB_USERNAME}/workspace   # Переход в папку workspace
$ pushd .                        # Сохранение текущей директории
~/CrazyOverdose/workspace ~/CrazyOverdose/workspace
$ source scripts/activate   # Выполнение скрипта подготовки
```
Установка инструментов для работы с Travis CI
```ShellSession
$ \curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles # Получение и установка bash-файла
Turning on ignore dotfiles mode.
Downloading https://github.com/rvm/rvm/archive/master.tar.gz
Installing RVM to /home/overdose/.rvm/
Installation of RVM in /home/overdose/.rvm/ is almost complete:
* To start using RVM you need to run `source /home/overdose/.rvm/scripts/rvm`
in all your open shell windows, in rare cases you need to reopen all shell windows.
Thanks for installing RVM 🙏
Please consider donating to our open collective to help us maintain RVM.

👉  Donate: https://opencollective.com/rvm/donate
$ echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate 
                                        # Дописывание команды запуска rvm в скрипт
$ . scripts/activate                    # Активация скрипта
$ rvm autolibs disable                  # Диактивация зависимостей
$ rvm install ruby-2.4.2            #Установление ruby
Warning, new version of rvm available '1.29.8', you are using older version '1.29.8-next'.
You can disable this warning with:   echo rvm_autoupdate_flag=0 >> ~/.rvmrc
You can enable auto-update with:     echo rvm_autoupdate_flag=2 >> ~/.rvmrc
You can update manually with:        rvm get VERSION                         (e.g. 'rvm get stable')

Searching for binary rubies, this might take some time.
No binary rubies available for: manjaro/18.0.4/x86_64/ruby-2.4.2.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Installing Ruby from source to: /home/absinthetoxin/.rvm/rubies/ruby-2.4.2, this may take a while depending on your cpu(s)...
ruby-2.4.2 - #downloading ruby-2.4.2, this may take a while depending on your connection...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 12.0M  100 12.0M    0     0  85192      0  0:02:27  0:02:27 --:--:-- 89798
No checksum for downloaded archive, recording checksum in user configuration.
ruby-2.4.2 - #extracting ruby-2.4.2 to /home/absinthetoxin/.rvm/src/ruby-2.4.2.|
ruby-2.4.2 - #configuring......................................................-
ruby-2.4.2 - #post-configuration..
ruby-2.4.2 - #compiling.........................................................
ruby-2.4.2 - #installing.............
ruby-2.4.2 - #making binaries executable..
ruby-2.4.2 - #downloading rubygems-3.0.3
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  882k  100  882k    0     0   113k      0  0:00:07  0:00:07 --:--:--  133k
No checksum for downloaded archive, recording checksum in user configuration.
ruby-2.4.2 - #extracting rubygems-3.0.3.....
ruby-2.4.2 - #removing old rubygems........
ruby-2.4.2 - #installing rubygems-3.0.3...................................
ruby-2.4.2 - #gemset created /home/absinthetoxin/.rvm/gems/ruby-2.4.2@global
ruby-2.4.2 - #importing gemset /home/absinthetoxin/.rvm/gemsets/global.gems....-
ruby-2.4.2 - #generating global wrappers.......
ruby-2.4.2 - #gemset created /home/absinthetoxin/.rvm/gems/ruby-2.4.2
ruby-2.4.2 - #importing gemsetfile /home/absinthetoxin/.rvm/gemsets/default.gems evaluated to empty gem list
ruby-2.4.2 - #generating default wrappers.......
ruby-2.4.2 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
Install of ruby-2.4.2 - #complete 
Ruby was built without documentation, to build it run: rvm docs generate-ri
$ rvm use 2.4.2 --default  # Установка установленной версии как основной
Using /home/absinthetoxin/.rvm/gems/ruby-2.4.2
$ gem install travis      # Установка travis
Fetching faraday-0.15.4.gem
Fetching highline-1.7.10.gem
Fetching multipart-post-2.1.1.gem
Fetching multi_json-1.13.1.gem
Fetching addressable-2.4.0.gem
Fetching net-http-persistent-2.9.4.gem
Fetching launchy-2.4.3.gem
Fetching net-http-pipeline-1.0.1.gem
Fetching backports-3.15.0.gem
Fetching gh-0.15.1.gem
Fetching typhoeus-0.8.0.gem
Fetching websocket-1.2.8.gem
Fetching travis-1.8.10.gem
Fetching ffi-1.11.1.gem
Fetching ethon-0.12.0.gem
Fetching faraday_middleware-0.13.1.gem
Fetching pusher-client-0.6.2.gem
Successfully installed multipart-post-2.1.1
Successfully installed faraday-0.15.4
Successfully installed faraday_middleware-0.13.1
Successfully installed highline-1.7.10
Successfully installed backports-3.15.0
Successfully installed multi_json-1.13.1
Successfully installed addressable-2.4.0
Successfully installed net-http-persistent-2.9.4
Successfully installed net-http-pipeline-1.0.1
Successfully installed gh-0.15.1
Successfully installed launchy-2.4.3
Building native extensions. This could take a while...
Successfully installed ffi-1.11.1
Successfully installed ethon-0.12.0
Successfully installed typhoeus-0.8.0
Successfully installed websocket-1.2.8
Successfully installed pusher-client-0.6.2
Successfully installed travis-1.8.10
Parsing documentation for multipart-post-2.1.1
Installing ri documentation for multipart-post-2.1.1
Parsing documentation for faraday-0.15.4
Installing ri documentation for faraday-0.15.4
Parsing documentation for faraday_middleware-0.13.1
Installing ri documentation for faraday_middleware-0.13.1
Parsing documentation for highline-1.7.10
Installing ri documentation for highline-1.7.10
Parsing documentation for backports-3.15.0
Installing ri documentation for backports-3.15.0
Parsing documentation for multi_json-1.13.1
Installing ri documentation for multi_json-1.13.1
Parsing documentation for addressable-2.4.0
Installing ri documentation for addressable-2.4.0
Parsing documentation for net-http-persistent-2.9.4
Installing ri documentation for net-http-persistent-2.9.4
Parsing documentation for net-http-pipeline-1.0.1
Installing ri documentation for net-http-pipeline-1.0.1
Parsing documentation for gh-0.15.1
Installing ri documentation for gh-0.15.1
Parsing documentation for launchy-2.4.3
Installing ri documentation for launchy-2.4.3
Parsing documentation for ffi-1.11.1
Installing ri documentation for ffi-1.11.1
Parsing documentation for ethon-0.12.0
Installing ri documentation for ethon-0.12.0
Parsing documentation for typhoeus-0.8.0
Installing ri documentation for typhoeus-0.8.0
Parsing documentation for websocket-1.2.8
Installing ri documentation for websocket-1.2.8
Parsing documentation for pusher-client-0.6.2
Installing ri documentation for pusher-client-0.6.2
Parsing documentation for travis-1.8.10
Installing ri documentation for travis-1.8.10
Done installing documentation for multipart-post, faraday, faraday_middleware, highline, backports, multi_json, addressable, net-http-persistent, net-http-pipeline, gh, launchy, ffi, ethon, typhoeus, websocket, pusher-client, travis after 36 seconds
17 gems installed

```
Клонирование репозитория ЛР3 в ЛР4
```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab03 projects/lab05 # Клонирование репозитория
Клонирование в «projects/lab05»…
remote: Enumerating objects: 27, done.
remote: Counting objects: 100% (27/27), done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 27 (delta 4), reused 23 (delta 3), pack-reused 0
Распаковка объектов: 100% (27/27), готово.
$ cd projects/lab05  # Переход в директорию
$ git remote remove origin # Удаление связки с репозиторием
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab05 # Добавление связки
```
Записывание в .travis.yml информации о языке
```ShellSession
$ cat > .travis.yml <<EOF      # Запись в .travis.yml
language: cpp
EOF
```
Дописывание в .travis.yml команд, выполняющихся при интеграции
```ShellSession
$ cat >> .travis.yml <<EOF  # Дозапись в .travis.yml

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```
Добавление в .travis.yml информации об устанавливаемых пакетах
```ShellSession
$ cat >> .travis.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```
Авторизация в сервисе Travis CI по токену
```ShellSession
$ travis login --github-token ${GITHUB_TOKEN}  # Авторизация 
Successfully logged in as CrazyOverdose!
```
Проверка
```ShellSession
$ travis lint
Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping
```
Добавление в начало файла строки с фрагментом вставки значка сервиса Travis CI в формате Markdown
```ShellSession
$ sed -i '1i|[![Build Status](https://travis-ci.org/CrazyOverdose/lab05.svg?branch=master)](https://travis-ci.org/CrazyOverdose/lab05)' README.md   # Команда изменена

```
Отправка изменений
```ShellSession
$ git add .travis.yml   # Фиксирование 
$ git add README.md      # Фиксирование 
$ git commit -m"added CI"  # Добавление коммита  
[master da3553a] added CI
 2 files changed, 14 insertions(+)
 create mode 100644 .travis.yml
$ git push origin master   # Отправка изменений
Username for 'https://github.comCrazyOverdose
Password for 'https://CrazyOverdose@github.com': 
Перечисление объектов: 31, готово.
Подсчет объектов: 100% (31/31), готово.
Сжатие объектов: 100% (26/26), готово.
Запись объектов: 100% (31/31), 14.38 KiB | 3.59 MiB/s, готово.
Всего 31 (изменения 6), повторно использовано 0 (изменения 0)
remote: Resolving deltas: 100% (6/6), done.
To https://github.com/CrazyOverdose/lab05
 * [new branch]      master -> master
```
Работа с Travis CI
```ShellSession
$ travis lint   # Проверка конфига
Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping
$ travis accounts    #Информация об аккаунте 
CrazyOverdose (Crazyoverdose): subscribed, 13 repositories
$ travis sync       # Синхронизация
synchronizing: .. done
$ travis repos          #Список репозиториев 
CrazyOverdose/lab00 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем обмена данными

CrazyOverdose/lab003 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем автоматизации сборки проекта на примере CMake

CrazyOverdose/lab006 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение средств пакетирования на примере CPack

CrazyOverdose/lab01 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение утилит для разработки проектов

CrazyOverdose/lab02 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

CrazyOverdose/lab03 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

CrazyOverdose/lab05 (active: yes, admin: yes, push: yes, pull: yes)
Description: ???

CrazyOverdose/lab05 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

CrazyOverdose/lab06 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

CrazyOverdose/lab07 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем управления пакетами на примере Hunter

CrazyOverdose/laba04 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем непрерывной интеграции на примере сервиса Travis CI

CrazyOverdose/laba05 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение фреймворков для тестирования на примере GTest

CrazyOverdose/labaa02 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем контроля версий на примере Git

$ travis enable   # Активация проекта
Detected repository as CrazyOverdose/lab05, is this correct? |yes| yes
CrazyOverdose/lab05: enabled :)
$ travis whatsup   # Список последних сборок
CrazyOverdose/lab05 passed: #1
$ travis branches    # Список последних сборок по веткам проекта
master:  #1    passed     added CI
$ travis history  # История сборок для проекта
#1 passed:       master added CI
$ travis show   # Основная информация о последней сборке
Job #1.1:  added CI
State:         passed
Type:          push
Branch:        master
Compare URL:   https://github.com/CrazyOverdose/lab05/compare/89df61653546^...da3553aea864
Duration:      28 sec
Started:       2019-06-09 19:09:31
Finished:      2019-06-09 19:09:59
Allow Failure: false
Config:        os: linux

```

## Report

```ShellSession
$ popd
$ export LAB_NUMBER=04
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Homework

Вы продолжаете проходить стажировку в "Formatter Inc." (см [подробности](https://github.com/tp-labs/lab03#Homework)).

В прошлый раз ваше задание заключалось в настройке автоматизированной системы **CMake**.

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в [прошлый раз](https://github.com/tp-labs/lab03#Homework). Настройте сборочные процедуры на различных платформах:
* используйте [TravisCI](https://travis-ci.com/) для сборки на операционной системе **Linux** с использованием компиляторов **gcc** и **clang**;
* используйте [AppVeyor](https://www.appveyor.com/) для сборки на операционной системе **Windows**.

## Links

- [Travis Client](https://github.com/travis-ci/travis.rb)
- [AppVeyour](https://www.appveyor.com/)
- [GitLab CI](https://about.gitlab.com/gitlab-ci/)

```
Copyright (c) 2015-2019 The ISC Authors
```
