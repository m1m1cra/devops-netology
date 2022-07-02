1. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?
- у меня уже установлен локально VMware Workstation, поэтому я использовал провайдер VMWare для Vagrant. Машине выделены процессорные мощности, ОЗУ и место на HDD. По умолчанию были выделены 2 ядра CPU, 1 GB ОЗУ и 64 GB HDD

2. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?
- Добавить оперативную память и число ядер можно через параметры memory и cpus. Если машина выключена - то сконфигурить и включить, а если включена - обязательно vagrant reload. Конфиг прикрепляю.

-  Vagrant.configure("2") do |config|
 	   config.vm.box = "bento/ubuntu-20.04"
     config.vm.provider "VMWare" do |vm|
	   vm.memory = 2048
	   vm.cpus = 4
   end

3. Ознакомиться с разделами man bash, почитать о настройках самого bash:
    какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?
    
    - задать можно переменной HISTSIZE в файле .bashrc, указано на 536 строке man'a

           HISTSIZE
              The number of commands to remember in the command history (see HISTORY below).  If the value is 0, commands are not saved in the history list.  Numeric values less than zero result in every command being saved on the history list (there is no limit).  The shell sets the default value to 500 af‐
              ter reading any startup files.
	      
    что делает директива ignoreboth в bash?
    
 - ignoreboth — не записывать команду, которая начинается с пробела, либо команду, которая дублирует предыдущую.
 Описано в man'e bash строке 436
 
 HISTCONTROL
              A  colon-separated  list  of  values controlling how commands are saved on the history list.  If the list of values includes ignorespace, lines which begin with a space character are not saved in the history list.  A value of ignoredups causes lines matching the previous history entry to not be
              saved.  A value of ignoreboth is shorthand for ignorespace and ignoredups.  A value of erasedups causes all previous lines matching the current line to be removed from the history list before that line is saved.  Any value not in the above list is ignored.  If HISTCONTROL is unset, or does  not
              include a valid value, all lines read by the shell parser are saved on the history list, subject to the value of HISTIGNORE.  The second and subsequent lines of a multi-line compound command are not tested, and are added to the history regardless of the value of HISTCONTROL.


В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?
- Данные скобки применяются в составных командах, описано на 174 строке man bash

  Compound Commands
       A compound command is one of the following.  In most cases a list in a command's description may be separated from the rest of the command by one or more newlines, and may be followed by a newline in place of a semicolon.

       { list; }
              list  is  simply executed in the current shell environment.  list must be terminated with a newline or semicolon.  This is known as a group command.  The return status is the exit status of list.  Note that unlike the metacharacters ( and ), { and } are reserved words and must occur where a re‐
              served word is permitted to be recognized.  Since they do not cause a word break, they must be separated from list by whitespace or another shell metacharacter.

С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?
- Создать 100000 файлов можно командой  touch {1..100000}
Если попытаться создать 300000 файлов, будет ошибка, так как превышено число аргументов для процессa


В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]
-
Данная конструкция возвращает 0 в случае наличия папки tmp в корне, и 1 - в случае отсутствия 

avdeevan@bhdevops:/scripts$  ([[ -d /tmp ]]) \n
avdeevan@bhdevops:/scripts$  echo $?  \n
0
avdeevan@bhdevops:/scripts$  ([[ -d /tmp2 ]])
avdeevan@bhdevops:/scripts$  echo $?
1



avdeevan@bhdevops:/scripts$ cat scr
if [[ -d /tmp ]]
then
    echo "/tmp существует"
else
    echo "/tmp не существует"
fi
avdeevan@bhdevops:/scripts$ ./scr
**/tmp существует**
avdeevan@bhdevops:~/scripts$

Данная команда [[ -d /tmp ]] возвращает истинну, так как папка tmp в корне есть

Также, сделал следующий скрипт и вывод для демонстрации понимания работы
avdeevan@bhdevops:~/scripts$ [[ -d /tmp ]] && echo true || echo false
true
avdeevan@bhdevops:~/scripts$ [[ -d /QQQ ]] && echo true || echo false
false
avdeevan@bhdevops:~/scripts$








Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:
-
bash is /tmp/new_path_directory/bash
bash is /usr/local/bin/bash
bash is /bin/bash

(прочие строки могут отличаться содержимым и порядком) В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.
-
cd /tmp;
mkdir new_path_directory;
cd new_path_directory;
sudo cp /usr/bin/bash /usr/local/bin;
sudo cp /bin/bash /tmp/new_path_directory;
PATH=/tmp/new_path_directory/:$PATH


Чем отличается планирование команд с помощью batch и at?
- Отличие данных команд в том, что команды, запланированные к выполнению через at, выполнятся в любом случае в указанное время, а batch выполняется при определенной загрузке операционной системы - по умолчанию - 1.5, значение можно сменить посредством вызова atd 


Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.

vagrant halt

