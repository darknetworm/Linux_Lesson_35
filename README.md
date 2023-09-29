# Linux_Lesson_35
## DNS
### Описание репозитория

Лабораторный стенд для тестирования технологии split-DNS, настраиваемые с использованием Vagrant и Ansible. Все файлы и структуру директорий temрlates и client необходимо скопировать в общую директорию.

- **Vagrantfile** - создаёт два DNS-сервера (master и slave) и два клиентских хоста, подключенных к сети серверов.  
- Директория **/ansible** содержит файлы для настройки виртуальных машин с помощью Ansible, в этой директории расположены основные файлы:  
- **playbook.yml** - основной файл Ansible playbook для установки и настройки сетевых устройств стенда.  
- **hosts** - файл с настройками компьютеров для быстрого доступа к ним из playbook.


На серверах настроены зоны: dns.lab, ddns.lab, newdns.lab, обратный dns.lab.rev.  
Настройка split-DNS заключается в том, что клиентские хосты видят различные зоны DNS:  
*client* - видит dns.lab и newdns.lab, но в зоне dns.lab только web1;  
*client2* - видит только dns.lab.

---

 ### Проверка работоспособности стенда

 Для проверки правильности настройки split-DNS использовалась утилита ping на каждом из клиентских хостов.  
 ![client](https://github.com/darknetworm/Linux_Lesson_35/assets/82410807/d4383a59-38ba-474e-bae5-ee9b616dc7b5)
 
Хост client имеет доступ к зоне newdns.lab и к хосту web1.dns.lab, при этом доступ к хосту web2.dns.lab отсутствует.

![client2](https://github.com/darknetworm/Linux_Lesson_35/assets/82410807/20356c40-8c9f-47f0-9106-4cc4642e0498)  

Хост client2 не имеет доступ к зоне newdns.lab, при этом имеет к хостам web1.dns.lab и web2.dns.lab.
