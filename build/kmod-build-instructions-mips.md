
# Инструкция по сборке драйверов

Сборка драйверов осуществляется с использованием предоставленной структуры
каталогов и файлов, которая существует в директории **angtel-projects**. Ниже
приводится описание организации этой директории, а также последовательность
шагов, выполнение которых необходимо для корректной сборки драйверов.

## Подготовительные операции

Прежде чем приступить к сборке драйверов необходимо скопировать директорию
**angtel-projects** в свой домашний каталог. Для этого необходимо,
прежде всего, определить где находится директория **netprog2** относительно
корневого каталога (**/**). В директории **netprog2** содержатся исходные файлы
проекта. Определив указанный путь (назовем его path_to_netprog2),
выполните приведенные ниже команды:

```console
$ cp -R /path_to_netprog2/build/angtel-projects ~/
$ cd ~/angtel-projects
```

После выполнения указанных команд Вы окажетесь в директории
**angtel-projects**, расположенной в домашнем каталоге.

## Структура каталогов

В директории **angtel-projects** содержится каталог с названием
**kmod-hello-world**. Также в директории **angtel-projects** находится общий
makefile, который называется **kmod-common&#46;mk**.

Рассмотрим структуру каталога **kmod-hello-world**. Исходные файлы
располагаются в самом каталоге **kmod-hello-world**. Помимо этого, в каталоге
**kmod-hello-world** имеется частный makefile с именем **Makefile**.
Частный makefile содержит следующую информацию:

```make
DRV_NAME ::= hello_world

MAIN_MAKEFILE ::= ../kmod-common.mk

ifneq ($(KERNELRELEASE),)
MAIN_MAKEFILE ::= $(M)/$(MAIN_MAKEFILE)
endif

include $(MAIN_MAKEFILE)
```

Здесь **DRV_NAME** это имя файла драйвера, получающегося в результате
сборки драйвера, **MAIN_MAKEFILE** - путь к общему makefile относительно
каталога **kmod-hello-world**.

## Алгоритм сборки

1. Перейти в каталог **kmod-hello-world**.

    ```console
    $ cd ~/angtel-projects/kmod-hello-world
    ```

2. Поместить файлы с исходным кодом (*.c) в каталог **kmod-hello-world**.

3. Задать в частном makefile с именем **Makefile**, который находится в текущем
   каталоге, желаемое имя файла драйвера. Для этого необходимо установить
   для переменной **DRV_NAME** соответствующее значение.

4. Собрать драйвер.

    ```console
    $ make
    ```

5. Записать драйвер на плату.

    ```console
    $ make install
    ```

## Дополнительные действия

1. Очистка директории от файлов, появившихся во время сборки.

    ```console
    $ make clean
    ```

2. Удаление файла драйвера с платы.

    ```console
    $ make uninstall
    ```

3. Вывод списка доступных действий.

    ```console
    $ make help
    ```