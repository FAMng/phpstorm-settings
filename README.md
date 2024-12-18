# Пример настроек phpstorm

## Ftp/sftp
**settings > Build, Execution... > Deployment > Options**

![SFTP/ftp](https://github.com/FAMng/phpstrom-settings/images/sftp.png)

1. Не использовать автозагрузку (исключение - это сильно ускорит работу, при условии что разработчик полностью понимает как работает механизм автозагрузки на сервер)
2. Сравнивать файлы перед отправкой на сервер по контенту
3. Уведомлять если файлы на сервере отличаются

## Минификация/транспиляция

Большинство преобразований происходят через вотчеры (**settings > tools > file watchers**)
Одна из самых полезных настроек в вотчере - ``` scope ```, ее лучше установить в ``` current file ``` чтобы не задевать какие-либо файлы кроме тех которые редактируются.
Не забывайте указать результирующий файл в ``` Output paths to refresh ```, это влияет на то будет ли **ide** что-то делать с результирующим файлом (отправка на сервер, дальнейшие преобразования и т.д.)

Основные необходимые переменные:

* ``` $FileName$ ``` - полное имя файла (script.js)

* ``` $FileNameWithoutExtension$ ``` - имя без расширения (script)

### JS

Для минфикации использовать ``` terser ``` (устанавливается через npm в нужную версию node)

без доп флагов результирующая команда должна выглядеть так

    terser file.js -o file.min.js

Пример конфига:

![JS Минификация](https://github.com/FAMng/phpstrom-settings/images/js.png)

### CSS

Устанавливаем [csso](https://github.com/css/csso-cli) 

    npm install -g csso-cli

В поле arguments добавляем флаг ``` --no-restructure ```.

Результирующая команда должна выглядеть так:

    csso -i file.css -o file.min.css --no-restructure

![css Минификация](https://github.com/FAMng/phpstrom-settings/images/css.png)

### PHP

Встроенный форматтер (**settings > editor > code style > php**) справляется с форматированием (необходимо корректно выставить значение версии php в проекте)

![php](https://github.com/FAMng/phpstrom-settings/images/php1.png)

Для корректного линтинга необходимо подключить ```PHP_CodeSniffer```
Для .deb дистрибутивов linux можно установить глобально пакет php-codesniffer

    sudo apt install php-codesniffer

Настройка производится следующим образом:

* В ```Settings > PHP``` необходимо указать путь к интерпретатору

![php](https://github.com/FAMng/phpstrom-settings/images/php2.png)

* В ```Settings > PHP > Quality Tools``` указать корректные пути к снифферу и включить соответствующие валидации. При необходимости можно настроить индивидуально для проекта

![php](https://github.com/FAMng/phpstrom-settings/images/php3.png)
