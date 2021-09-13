## ДЗ "4.3. Языки разметки JSON и YAML"
___
Обязательные задания

**1. Мы выгрузили JSON, который получили через API запрос к нашему сервису:**
 ```
        { "info" : "Sample JSON output from our service\t",
            "elements" :[
                { "name" : "first",
                "type" : "server",
                "ip" : 7175 
                },
                { "name" : "second",
                "type" : "proxy",
                "ip : 71.78.22.43
                }
            ]
        }
 ```
Нужно найти и исправить все ошибки, которые допускает наш сервис

**Исправлено:**
 ```
    { "info" : "Sample JSON output from our service\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : 7175 
            },
            { "name" : "second",
            "type" : "proxy",
            "ip" : "71.78.22.43"  
            }
        ]
    }
 ```
**Ошибка в последней строчке массива: ip" и "71.78.22.43"**

**2. В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. 
   Формат записи JSON по одному сервису: { "имя сервиса" : "его IP"}. Формат записи YAML по одному сервису: - имя сервиса: его IP. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.**

Результат:
 ```	
	import socket
    import time
    import json
    import yaml
	
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
				#добавляем в условия создания json и yaml файлов ->
				with open("my_services.json", 'w') as js_f, open("my_services.yml", 'w') as ym_f:
                    js_f.write(json.dumps(my_service, indent=2)) 
                    ym_f.write(yaml.dump(my_service)) 
                print(f'[ERROR] {service_name} IP mismatch: {current_ip} New IP: {check_ip}')
            else:
                print(f'{service_name} - {current_ip}')
 ```
 


