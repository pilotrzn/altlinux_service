# Установка barman 3.4.0 на Альт 10

Установка barman версии >3 возможна только из пакетов. Пакеты скачиваем с офф. репозитория sisyphus.


```
barman-3.4.0-alt1.noarch.rpm 
barman-cli-3.4.0-alt1.noarch.rpm 
python3-module-barman-3.4.0-alt1.noarch.rpm
```

При установке python3-module-barman требуется доустановка зависимых пакетов python:

```
$ sudo rpm -i python3-module-barman-3.4.0-alt1.noarch.rpm

ошибка: Неудовлетворенные зависимости:
        python3-module-setuptools нужен для python3-module-barman-3.4.0-alt1.noarch
        python3-module-psycopg2 >= 2.4.2 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3-module-argh >= 0.21.2 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3-module-argcomplete нужен для python3-module-barman-3.4.0-alt1.noarch
        python3-module-dateutil нужен для python3-module-barman-3.4.0-alt1.noarch
        python3(argcomplete) < 0 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3(dateutil) < 0 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3(dateutil.parser) < 0 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3(dateutil.tz) < 0 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3(psycopg2) < 0 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3(psycopg2.errorcodes) < 0 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3(psycopg2.extensions) < 0 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3(psycopg2.extras) < 0 нужен для python3-module-barman-3.4.0-alt1.noarch
        python3(requests) < 0 нужен для python3-module-barman-3.4.0-alt1.noarch
```

Процесс установки со списком устанавливаемых пакетов:

```
$ sudo apt-get install python3-module-setuptools python3-module-psycopg2 python3-module-argh python3-module-argcomplete python3-module-dateutil python3-module-requests

Обновление / установка...
 1: pkg-config-0.29.2-alt3                      
 2: libcrypt-devel-4.4.23-alt1                  
 3: libtinfo-devel-6.2.20210123-alt1            
 4: libncurses-devel-6.2.20210123-alt1          
 5: python3-module-pkg_resources-1:57.4.0-alt1  
 6: tests-for-installed-python3-pkgs-0.1.19-alt2
 7: rpm-macros-python3-0.1.19-alt2              
 8: rpm-build-python3-0.1.19-alt2               
 9: python3-dev-3.9.6-alt1                      
10: python3-module-setuptools-1:57.4.0-alt1   
11: python3-module-six-1.15.0-alt2             
12: libpq5-15.2-alt1                           
13: python3-module-psycopg2-2.9.1-alt1         
14: python3-module-dateutil-2.8.1-alt3         
15: python3-module-argh-0.26.2-alt1            
16: python3-module-argcomplete-1.12.2-alt1     
17: python3-module-ntlm-1.1.0-alt1.2                
18: python3-module-ndg-0.4.2-alt1.qa1               
19: python3-module-idna-3.2-alt1                    
20: python3-module-chardet-1:3.0.4-alt2             
21: python3-module-pycparser-2.20-alt2              
22: python3-module-cffi-1.14.5-alt2                 
23: python3-module-cryptography-3.4.7-alt1          
24: python3-module-openssl-20.0.1-alt1              
25: python3-module-ndg-httpsclient-0.4.2-alt1.qa1   
26: python3-module-urllib3-2:1.26.6-alt1            
27: python3-module-requests-2.25.1-alt2 
```


После установки зависимостей установка barman проходит без проблем:

```
$ sudo rpm -i python3-module-barman-3.4.0-alt1.noarch.rpm barman-3.4.0-alt1.noarch.rpm barman-cli-3.4.0-alt1.noarch.rpm
```




