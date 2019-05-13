## Laboratory work IV

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```ShellSession
$ open https://travis-ci.org
```

## Tasks

- [x] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
- [x] 2. Создать публичный репозиторий с названием **lab04** на сервисе **GitHub**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
- [ ] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
- [ ] 6. Получить фрагмент вставки значка сервиса **Travis CI** в формате **Markdown**
- [ ] 7. Выполнить инструкцию учебного материала
- [ ] 8. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_TOKEN=<полученный_токен>
```

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .

~/Mihailus2000/workspace ~/Mihailus2000/workspace

$ source scripts/activate
```

```ShellSession
$ \curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles

ignore-dotfiles
Turning on ignore dotfiles mode.
Downloading https://github.com/rvm/rvm/archive/master.tar.gz
Installing RVM to /home/mic/.rvm/
Installation of RVM in /home/mic/.rvm/ is almost complete:

  * To start using RVM you need to run `source /home/mic/.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.
Thanks for installing RVM 🙏
Please consider donating to our open collective to help us maintain RVM.

👉  Donate: https://opencollective.com/rvm/donate



$ echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate

echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate

$ . scripts/activate
$ rvm autolibs disable
$ rvm install ruby-2.4.2

# already unstall

$ rvm use 2.4.2 --default

$ gem install travis

Fetching: faraday_middleware-0.13.1.gem (100%)
Successfully installed faraday_middleware-0.13.1
Fetching: highline-1.7.10.gem (100%)
Successfully installed highline-1.7.10
Fetching: backports-3.14.0.gem (100%)
Successfully installed backports-3.14.0
Fetching: addressable-2.4.0.gem (100%)
Successfully installed addressable-2.4.0
Fetching: net-http-pipeline-1.0.1.gem (100%)
Successfully installed net-http-pipeline-1.0.1
Fetching: gh-0.15.1.gem (100%)
Successfully installed gh-0.15.1
Fetching: launchy-2.4.3.gem (100%)
Successfully installed launchy-2.4.3
Fetching: typhoeus-0.8.0.gem (100%)
Successfully installed typhoeus-0.8.0
Fetching: websocket-1.2.8.gem (100%)
Successfully installed websocket-1.2.8
Fetching: pusher-client-0.6.2.gem (100%)
Successfully installed pusher-client-0.6.2
Fetching: travis-1.8.10.gem (100%)
Successfully installed travis-1.8.10
Parsing documentation for faraday_middleware-0.13.1
Installing ri documentation for faraday_middleware-0.13.1
Parsing documentation for highline-1.7.10
Installing ri documentation for highline-1.7.10
Parsing documentation for backports-3.14.0
Installing ri documentation for backports-3.14.0
Parsing documentation for addressable-2.4.0
Installing ri documentation for addressable-2.4.0
Parsing documentation for net-http-pipeline-1.0.1
Installing ri documentation for net-http-pipeline-1.0.1
Parsing documentation for gh-0.15.1
Installing ri documentation for gh-0.15.1
Parsing documentation for launchy-2.4.3
Installing ri documentation for launchy-2.4.3
Parsing documentation for typhoeus-0.8.0
Installing ri documentation for typhoeus-0.8.0
Parsing documentation for websocket-1.2.8
Installing ri documentation for websocket-1.2.8
Parsing documentation for pusher-client-0.6.2
Installing ri documentation for pusher-client-0.6.2
Parsing documentation for travis-1.8.10
Installing ri documentation for travis-1.8.10
Done installing documentation for faraday_middleware, highline, backports, addressable, net-http-pipeline, gh, launchy, typhoeus, websocket, pusher-client, travis after 7 seconds
11 gems installed


```

```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab03 projects/lab04

Клонирование в «projects/lab04»…
remote: Enumerating objects: 33, done.
remote: Counting objects: 100% (33/33), done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 33 (delta 9), reused 33 (delta 9), pack-reused 0
Распаковка объектов: 100% (33/33), готово.

$ cd projects/lab04
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab04
```

```ShellSession
$ cat > .travis.yml <<EOF
language: cpp
EOF
```

```ShellSession
$ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```

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

```ShellSession
$ travis login --github-token ${GITHUB_TOKEN}

Successfully logged in as Mihailus2000!

```

```ShellSession
$ travis lint

Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping

```

```ShellSession
$ ex -sc '1i|[![Build Status](https://travis-ci.org/Mihailus2000/lab04F.svg?branch=master)](https://travis-ci.org/Mihailus2000/lab04F)' -cx README.md

```

```ShellSession
$ git add .travis.yml
$ git add README.md
$ git commit -m"added CI"

[master ff1af40] added CI
 1 file changed, 14 insertions(+)
 create mode 100644 .travis.yml

$ git push origin master

Username for 'https://github.com': Mihailus2000
Password for 'https://Mihailus2000@github.com': 
Перечисление объектов: 36, готово.
Подсчет объектов: 100% (36/36), готово.
При сжатии изменений используется до 4 потоков
Сжатие объектов: 100% (31/31), готово.
Запись объектов: 100% (36/36), 11.46 KiB | 2.87 MiB/s, готово.
Всего 36 (изменения 10), повторно использовано 0 (изменения 0)
remote: Resolving deltas: 100% (10/10), done.
To https://github.com/Mihailus2000/lab04
 * [new branch]      master -> master

```

```ShellSession
$ travis lint

Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping

$ travis accounts

Mihailus2000 (Mihailus2000): subscribed, 11 repositories

$ travis sync

synchronizing: .. done

$ travis repos

Mihailus2000/First (active: no, admin: yes, push: yes, pull: yes)
Description: Start

Mihailus2000/HW1-Sem2- (active: no, admin: yes, push: yes, pull: yes)
Description: ???

Mihailus2000/MGTU_BAIMANA_Mihail (active: no, admin: yes, push: yes, pull: yes)
Description: ???

Mihailus2000/lab00 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем обмена данными

Mihailus2000/lab01 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение утилит для разработки проектов

Mihailus2000/lab02 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

Mihailus2000/lab02-1 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем контроля версий на примере Git

Mihailus2000/lab03 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

Mihailus2000/lab03Forked (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем автоматизации сборки проекта на примере CMake

Mihailus2000/lab04 (active: yes, admin: yes, push: yes, pull: yes)
Description: ???

Mihailus2000/lab04F (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем непрерывной интеграции на примере сервиса Travis CI

$ travis enable

Detected repository as Mihailus2000/lab04, is this correct? |yes| yes
Mihailus2000/lab04: enabled :)

$ travis whatsup

Mihailus2000/lab04 passed: #1

$ travis branches

master:  #1    passed     added CI

$ travis history

#1 passed:       master added CI

$ travis show

Job #1.1:  added CI
State:         passed
Type:          push
Branch:        master
Compare URL:   https://github.com/Mihailus2000/lab04/compare/0697494e977f^...1e17cb84a967
Duration:      54 sec
Started:       2019-05-13 18:35:49
Finished:      2019-05-13 18:36:43
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
