## ДЗ "4.2. Использование Python для решения типовых DevOps задач"

**1. Есть скрипт:**
    ```
        #!/usr/bin/env python3
        a = 1
        b = '2'
        c = a + b`
	```	
**Какое значение будет присвоено переменной c?**

Ошибка приведения типов :TypeError: unsupported operand type(s) for +: 'int' and 'str'. Нельзя складывать разные типы данных.

**Как получить для переменной c значение 12?**

Необходимо переменную a изменить на строковый тип str и сделать конкатинацию строк. Например: a=str(1), или a='1'.

**Как получить для переменной c значение 3?**

Необходимо переменную b изменить на числовой тип int, т провести операцию сложения. b=int('2'), или b=2.

**2. Мы устроились на работу в компанию, где раньше уже был DevOps Engineer. Он написал скрипт, позволяющий узнать, какие файлы модифицированы в репозитории, относительно локальных изменений. 
Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории, где они находятся.
Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?**
```
    #!/usr/bin/env python3

    import os

    bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
    result_os = os.popen(' && '.join(bash_command)).read()
    is_change = False
    for result in result_os.split('\n'):
        if result.find('modified') != -1:
            prepare_result = result.replace('\tmodified:   ', '')
            print(prepare_result)
            break
```

**Результат:
Пишем абсолютный путь и убирайем break (и is_change, т.к. она нигде более не фигурирует)**

```
  #!/usr/bin/env python3
    
    import os
    
    bash_command = ["cd /home/vagrant/netology/sysadm-homeworks", "git status"]
    result_os = os.popen(' && '.join(bash_command)).read()
    for result in result_os.split('\n'):
        if result.find('modified') != -1:
            prepare_result = result.replace('\tmodified:   ', '')
            print(prepare_result)
```

__
**3. Доработать скрипт выше так, чтобы он мог проверять не только локальный репозиторий в текущей директории, а также умел воспринимать путь к репозиторию, который мы передаём как входной параметр. 
Мы точно знаем, что начальство коварное и будет проверять работу этого скрипта в директориях, которые не являются локальными репозиториями.**

```
#!/usr/bin/env python3

    import os
    import sys

    r_path = sys.argv[1]
    c_path = os.path.exists(f'{r_path}.git')
    if c_path != True:
        print('directory not a repo')
        exit()
    bash_command = [f'cd {r_path}', "git status"]
    result_os = os.popen(' && '.join(bash_command)).read()
    for result in result_os.split('\n'):
        if result.find('modified') != -1:
            prepare_result = result.replace('\tmodified:   ', '')
            print(prepare_result)
```
Добавлен входной параметр и проверка на репозиторий

**4. Наша команда разрабатывает несколько веб-сервисов, доступных по http. 
Мы точно знаем, что на их стенде нет никакой балансировки, кластеризации, за DNS прячется конкретный IP сервера, где установлен сервис. 
Проблема в том, что отдел, занимающийся нашей инфраструктурой очень часто меняет нам сервера, поэтому IP меняются примерно раз в неделю, при этом сервисы сохраняют за собой DNS имена. 
Это бы совсем никого не беспокоило, если бы несколько раз сервера не уезжали в такой сегмент сети нашей компании, который недоступен для разработчиков. 
Мы хотим написать скрипт, который опрашивает веб-сервисы, получает их IP, выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. 
Также, должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена - оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. 
Будем считать, что наша разработка реализовала сервисы: drive.google.com, mail.google.com, google.com.**

```
	import socket
    import time
    
    my_service = {
        "drive.google.com": '',
        'mail.google.com': '',
        'google.com': ''
        }
    while True:
        for service_name, current_ip in my_service.items():
            check_ip = socket.gethostbyname(service_name)
            time.sleep(2)
            if check_ip != current_ip:
                my_service[service_name] = check_ip
                print(f'[ERROR] {service_name} IP mismatch: {current_ip} New IP: {check_ip}')
            else:
                print(f'{service_name} - {current_ip}')
```
