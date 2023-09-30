---
## Front matter
title: "Лабораторная работа №4"
subtitle: "Дискреционное разграничение прав в Linux. Расширенные атрибуты"
author: "Акопян Изабелла Арменовна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Получение практических навыков работы в консоли с расширенными атрибутами файлов.

# Задание

Проделать последовательность действий, описанных в задании к лабораторной работе: поработать на практике с расширенными атрибутами «а» и «i».


# Теоретическое введение

У каждого файла имеется определённый набор свойств в файловой системе. Например, это права доступа, владелец, имя, метки времени. В Linux каждый файл имеет довольно много свойств, например, права доступа устанавливаются трижды (для владельца, группы и всех прочих), метки времени также бывают трёх разных видов (время создание, доступа и изменения). 

chattr изменяет атрибуты файлов в файловой системе Linux.

Формат символьного режима: +-=[aAcCdDeFijmPsStTux].

Оператор «+» вызывает добавление выбранных атрибутов к существующим атрибутам файлов; «-» заставляет их удалить; и «=» делает их единственными атрибутами файлов. 

Атрибуты, с которыми предстоит работа:

a - Файл с установленным атрибутом «a» можно открыть только в режиме добавления для записи. Только суперпользователь или процесс, обладающий возможностью CAP_LINUX_IMMUTABLE, может установить или очистить этот атрибут.

i - Файл с атрибутом «i» не может быть изменён: его нельзя удалить или переименовать, нельзя создать ссылку на этот файл, большую часть метаданных файла нельзя изменить, и файл нельзя открыть в режиме записи. Только суперпользователь или процесс, обладающий возможностью CAP_LINUX_IMMUTABLE, может установить или очистить этот атрибут. 


# Выполнение лабораторной работы

От имени пользователя guest определите расширенные атрибуты файла file1 командой lsattr /home/guest/dir1/file1. Установите командой chmod 600 file1 на файл права, разрешающие чтение и запись для владельца файла. Попробовала установить на файл расширенный атрибут a от имени пользователя guest командой chattr.

В ответ получила отказ от выполнения операции (рис. @fig:001).    

![подготовка файла для работы и попытка добавления атрибута](image/1.png){#fig:001 width=70%}    

Повысила свои права с помощью команды su -. И через суперпользователя попробовала установить расширенный атрибут "a" на файл  командой chattr (рис. @fig:002).    

![суперпользователь](image/2.png){#fig:002 width=70%}    

От пользователя guest проверьте правильность установления атрибута:
lsattr  (рис. @fig:003).    

![проверка](image/3.png){#fig:003 width=70%}    

Выполнила дозапись в файл слова «test» командой echo  (рис. @fig:004).    

![запись в файл](image/4.png){#fig:004 width=70%}    

После этого выполнила чтение файла командой cat с суперпользователя. (рис. @fig:005).    

![чтение](image/5.png){#fig:005 width=70%}    


Попробовала стереть имеющуюся в нём информацию командой echo. Далее попробовала переименовать и удалить файл. Всё получилось. (рис. @fig:006).    

![работа с файлом](image/6.png){#fig:006 width=70%}    

Далее сняла расширенный атрибут "a" с файла от имени суперпользователя командой chattr. (рис. @fig:007).    

![удаление атрибута](image/7.png){#fig:007 width=70%}    

Добавила атрибут i. (рис. @fig:008).    

![добавление атрибута](image/8.png){#fig:008 width=70%}    

Проделала те же действия, что и ранее,но с новым атрибутом (рис. @fig:009).    

![Работа с файлом](image/9.png){#fig:009 width=70%}    

Ничего не смогла сделать с файлом. Как указано в теоретическом материале файл с атрибутом i не может быть изменен.

# Выводы

Получила практические навыки работы в консоли с расширенными атрибутами файлов. Опробовала действие на практике расширенных атрибутов «а» и «i». Только суперпользователь может установить или очистить этот атрибут.

# Список литературы{.unnumbered}

::: {#refs} 
:::

