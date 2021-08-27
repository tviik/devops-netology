# IB_DEVSYS9
Для ДЗ Нетологии (Богатырчук И.В.)

#ДЗ_1_2
- Описание жизненного цикла задачи (разработки нового функционала) /n
- 1.Определение функциональных требований и тз - менеджер /n
- 2.Постановка новых задач разработчикам - менеджер
- 3.Создание системы управления версиями - devops
- 4.Разворачивание стендов тестирования с разбивкой на версионность ПО (функционального/нагрузочного/a:b) - devops
- 5.Тестирование полученных бандлов от разработчика - тестирование
- 6.Внесение правок в ФТ/ТЗ после тестирования - менеджер по результатам тестирования
- 7.Если тестирование и клиент одобряет, установка версии в пром - devops
- 8.Разработка новой версии и повтор цикла

ДЗ_2_1
-----------
п.1 Модификация ридмихи через vim
-----------
ДЗ_2_2
https://github.com/tviik/devops-netology -- origin
https://gitlab.com/tviik/devops-netology -- gitlab
https://bitbucket.org/tviik/devops-netology -- bitbucket

------------

--------------------------------------------------------
# Домашнее задание к занятию «2.4. Инструменты Git»

- 1.commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Jun 18 10:29:58 2020 -0400
    Update CHANGELOG.md

- 2.(tag: v0.12.23)

- 3. 56cd7859e Merge pull request #23857 from hashicorp/cgriggs01-stable

- 4.commit 33ff1c03bb960b332be3af2e333462dde88b279e (tag: v0.12.24)
    v0.12.24
commit b14b74c4939dcab573326f4e3ee2a62e23e12f89
    [Website] vmc provider links

commit 3f235065b9347a758efadc92295b540ee0a5e26e
    Update CHANGELOG.md

commit 6ae64e247b332925b872447e9ce869657281c2bf
    registry: Fix panic when server is unreachable
    Non-HTTP errors previously resulted in a panic due to dereferencing the
    resp pointer while it was nil, as part of rendering the error message.
    This commit changes the error message formatting to cope with a nil
    response, and extends test coverage.
    Fixes #24384

commit 5c619ca1baf2e21a155fcdb4c264cc9e24a2a353
    website: Remove links to the getting started guide's old location

    Since these links were in the soon-to-be-deprecated 0.11 language section, I
    think we can just remove them without needing to find an equivalent link.

commit 06275647e2b53d97d4f0a19a0fec11f6d69820b5
    Update CHANGELOG.md

commit d5f9411f5108260320064349b757f55c09bc4b80
    command: Fix bug when using terraform login on Windows

commit 4b6d06cc5dcb78af637bbb19c198faff37a066ed
    Update CHANGELOG.md

commit dd01a35078f040ca984cdd349f18d0b67e486c35
    Update CHANGELOG.md

commit 225466bc3e5f35baa5d07197bbc079345b77525e
    Cleanup after v0.12.23 release

- 5. 
commit 8c928e83589d90a031f811fae52a81be7153e82f
тут не уверен, искал так:
git grep -p 'func providerSource('
provider_source.go:func providerSource(configs []*cliconfig.ProviderInstallation, services *disco.Disco) (getproviders.Source, tfdiags.Diagnostics) {
-> git log -S'func providerSource('

- 6. 
смотрим либы:
git grep -p 'globalPluginDirs'
commands.go=func initCommands(
commands.go:            GlobalPluginDirs: globalPluginDirs(),
commands.go=func credentialsSource(config *cliconfig.Config) (auth.CredentialsSource, error) {
commands.go:    helperPlugins := pluginDiscovery.FindPlugins("credentials", globalPluginDirs())
internal/command/cliconfig/config_unix.go=func homeDir() (string, error) {
internal/command/cliconfig/config_unix.go:              // FIXME: homeDir gets called from globalPluginDirs during init, before
plugins.go=import (
plugins.go:// globalPluginDirs returns directories that should be searched for
plugins.go:func globalPluginDirs() []string {

смотрим по либам:
git log -L :globalPluginDirs:config_unix.go
fatal: There is no path config_unix.go in the commit

git log -L :globalPluginDirs:internal/command/cliconfig/config_unix.go
fatal: -L parameter 'globalPluginDirs' starting at line 1: no match

git log -L :globalPluginDirs:plugins.go
commit 78b12205587fe839f10d946ea3fdc06719decb05
commit 52dbf94834cb970b510f2fba853a5b49ad9b1a46
commit 41ab0aef7a0fe030e84018973a64135b11abcd70
commit 66ebff90cdfaa6938f26f908c7ebad8d547fea17
commit 8364383c359a6b738a436d1b7745ccdce178df47

- 7. Author: Martin Atkins <mart@degeneration.co.uk>
(commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5)


-------------------------------
# Домашнее задание к занятию "3.1. Работа в терминале, лекция 1"

-п.5 --
- озу - 1024
- видюха = 8мб
- п.6 --
- config.vm.provider "virtualbox" do |v|
-   v.memory = 1024
- v.cpus = 2
- end
- п.7 - запустил из PS, работает root
- п.8 - строка 2940 HISTSIZE by default = 500 commands, set by histfilesize
- 	- что делает директива ignoreboth в bash - не записывать команду, которая начинается с пробела, либо команду, которая дублирует предыдущую. # export HISTCONTROL=ignoreboth.
- п.9 - игурные скобки {} для выражения переменнй. line 508
------------
- п.10 - можно циклом for i in {list}; do touch $i; done; 
- исправляюсь: п.10 touch file{1..10000} ; touch file{1..300000} -> argument too long -> ulimit -s = max_size(ulimt -a)->(65536)
------------
- п.11 - что делает конструкция [[ -d /tmp ]] - условие true если файл экзист и это директория
- п.12 Не смог через переменную создавал эту переменную окружения и под рутом и так.. через экспорт, максимум что получилось, это сделать alias в "etc/bash.bashrc" или "~/.bashrc". 
- Вывод был таким: 
---------
- "root@vagrant:/home/vagrant# type -a bash
-    bash is aliased to `/tmp/new_path_derictory/bash'
-    bash is /usr/bin/bash
-    bash is /bin/bash"
--------
- п.13 - Чем отличается планирование команд с помощью batch и at? - приоритетом, у at будет выше приоритет
- п.13 
- batch - многократные команы, последовательные,  чтение команд требует аргументы, логи уходят в syslog.  
- at - однократные, парралельные, чтение из stdin, логи алертят в почту. 
---------

# Домашнее задание к занятию "3.2. Работа в терминале, лекция 2"
---------------
- 1. "cd is a shell builtin" встроенная команда оболочки, мне сложно объяснить почему может или не может другого типа (не builtin), но в моем понимании как для того чтобы приготовить салат, необходим базовый наобор инструментов, в данном случае нож, достка и тара. (from google: cd has to be a builtin because the shell itself needs to change its "cwd" - current working directory - not a sub-process.)
- 2. something | grep -c ; man grep: -c, --count (Suppress normal output; instead print a count of matching lines for each  input  file.)
- 3. systemd
- 4. ls 2>/dev/pts/1 - по идее так, но у меня permisson denied даже под рутом, значит не так (трудность)
- 5. find / -name core > /tmp/testfile 2> /dev/null
- 6. Если правильно понял вопрос, то открыл две консоли (vagrant ssh (/dev/pts/0) и virtual box (/dev/tty1)) echo 'bonjour epta' > /dev/tty1. результат команды перенаправился в другой терминал.
- 7. bash 5>&1 - инициализируем новый файловый дескриптор и перенаправляем его в stdout. теперь 5 = &1 и echo netology > /proc/$$/fd/5 юудет выводить echo в stdout  
- 8. Очень сложно. Попробовал вывести так: bash 7>&2 | cat /tmp/dirnotexist | /proc/$$/fd/7 > /tmp/1.txt или bash 7>&2 | /tmp/1.txt <7 | cat /tmp/dirnotexist
- 10. cat /proc/$$/environ: "Этот файл содержит окружение процесса." Как еще можно получить аналогичный по содержанию вывод? - максимум что смог сообразить, это выдом через эхо указанных в предыдущем выводе переменных, импа echo $PATH, $HOME, $PWD etc.
* /proc/<PID>/cmdline: "Этот файл содержит полную командную строку запуска процесса, кроме тех процессов, что полностью ушли в своппинг, а также тех, что превратились в зомби. В этих двух случаях в файле ничего нет, то есть чтение этого файла вернет 0 символов. Аргументы командной строки в этом файле указаны как список строк, каждая из которых завешается нулевым символом, с добавочным нулевым байтом после последней строки." *
* /proc/<PID>/exe: "является символьной ссылкой, содержащей фактическое полное имя выполняемого файла" *
- 11. sse4_2 
- 12. ssh localhost 'tty' - not a tty - это удаленное исполнение "вне терминала". как изменить поведение - ввести в терминале.
- 13. тут воодще беда:
----------------------------
* kernel.yama.ptrace_scope = 0 *
* root@vagrant:/home/vagrant# reptyr -h *
* bash: reptyr: command not found *
* root@vagrant:/home/vagrant# sudo apt install reptyr *
* Reading package lists... Done *
* Building dependency tree *
* Reading state information... Done *
* The following NEW packages will be installed: *
*  reptyr *
* 0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded. *
* Need to get 22.5 kB of archives. *
* After this operation, 67.6 kB of additional disk space will be used. *
* Err:1 http://archive.ubuntu.com/ubuntu focal/universe amd64 reptyr amd64 0.6.2-1.3 *
*  Temporary failure resolving 'archive.ubuntu.com' *
* E: Failed to fetch http://archive.ubuntu.com/ubuntu/pool/universe/r/reptyr/reptyr_0.6.2-1.3_amd64.deb  Temporary failure resolving 'archive.ubuntu.com' *
* E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing? *
* root@vagrant:/home/vagrant# reptyr -h *
* bash: reptyr: command not found *
* root@vagrant:/home/vagrant#  *
-----------------------------
* в идеале думал так reptyr -l PID tty2 *
- 14. "Команда tee читает из стандартного ввода и записывает как в стандартный вывод, в один или несколько файлов одновременно" ; sudo не выполняет перенаправление вывода, но  sudo tee - команда для записи в файлы, принадлежащие другим пользователям. tee получит вывод команды echo, повысит права на sudo и запишет в файл.

    
    
---------------------------------   
# ДЗ Командная оболочка Bash: практические навыки
###### п.1 
```bash
c = a+b -- стринговое значение, нет пересменных
d = 1+2 -- стринговое значение неявнозаданных переменных без декларирования типа
e = 3 -- вызов арифметической функции внутри скобок
```
    
###### п.2
Что необходимо сделать, чтобы его исправить:
Необходимо из него выйти, при доступности, например:
```
#!/bin/bash
while ((1==1))
do curl https://localhost:4757
if (($? != 0))
then date > curl.log
sleep 60
elif
break
fi
done
```

###### п.3 тут у меня на виртуалке не настроена внешняя сеть и курл на внешние айпи не давал, а надо срочно сдать дз..
```
#!/bin/bash
array_ip=(192.168.0.1 173.194.222.113 87.250.250.242) #массив переменных
port=80
a=0
while (($a<=5))
	do
		for i in ${array_ip[@]}
		do 
		curl https://$i:$port
		if (($? != 0))
			then date >> file.log
			curl https://$i:$port  >> file.log
			sleep 3
		else
			date >> file.log
			echo evrything is ok! >> file.log
		fi
done
let "a += 1"
done
```

###### п.4 -- тут тоже не было возможности проверить (вообще пропустил блок с сетями, буду наверстывать), но посути логика скрипта понятна и проста
```
#!/bin/bash
array_ip=(192.168.0.1 173.194.222.113 87.250.250.242) #массив переменных
port=80
a=0
while ((1==1))
do
	for i in ${array_ip[@]}
		do 
		curl https://$i:$port
		if (($? != 0))
			then date >> error.log
			curl -I https://$i:$port  >> error.log
			break # прерываем скрипт на первом упавшем узле
		else
			date >> file.log
			echo evrything is ok! >> file.log
		fi
done
done
```

###### п.5  
```
#!/bin/bash
maxlength=30
mylenngth=$(cat $1|wc -m)
if [[ $mylenngth -gt $maxlength ]]
  then
  echo "your commit longer then 30"
  exit 1
elif ! grep -qE '^([0-9][0-9]-script-[0-9][0-9]-[a-z])' $1;
  then
  echo "your commit should be like [XX-script-XX-XX]"
  exit 1
fi  
```  
