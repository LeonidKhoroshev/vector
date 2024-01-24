Vector
=========

Комбайн для обработки данных из баз данных, позволяющий преобразовывать их журналы и метрики для удобного отображения в тексте, либо в графическом виде.

Требования
------------

На настраиваемых хостах должна быть уствновлена ОС Linux (RPM линейка), так как установка производится пакетным менеджером yum. Поскольку Vector крайне требователен к системным ресурсам, рекомендуется его установка на хосты с ек менее 4 Гб оперативной памяти и 2 Гб места на жестком диске (указаны минимальные параметры, оптимальные параметры зависят от объема обрабатываемых данных).

Переменные
--------------

Данная роль доступна к использованию без переменных, так как все значения прописаны в коде. При необходимости можно изменить отдельные настройки, такие как версия ПО (по умолчанию доступна версия "0.35.0") и имя пользователя. В шаблоне конфигурационного файла `templates/vector.j2` задаются источники данных (в указанной роли указан  dummy_logs, позволяющий генерировать данные в учебных и исследовательских целях), endpoint (ip адрес и порт) и таблицы для хранение сгенерированных данных.


Зависимости
------------

Для корректной работы понядорбится также установить СУБД Clickhouse (роль доступна по [ссылке](https://github.com/LeonidKhoroshev/clickhouse-role)) и графический интерфейл Lighthouse (роль доступна по [ссылке](https://github.com/LeonidKhoroshev/lighthouse) ). В сулчае, если базы данных, Vector и Lighthouse предполагается устанавливать на разных хостах, также потребуется веб-сервер (роль для установки Nginx доступна по [ссылке](https://github.com/LeonidKhoroshev/nginx)).

Пример плейбука
----------------

Установить роль можно через ansible-galaxy:
```
ansible-galaxy install -r requirements.yml
```

указав в файле requirements.yml cледующее содержание:
```
  - src: https://github.com/LeonidKhoroshev/vector
    scm: git
    name: lighthouse
```

Далее вписываем роль в плейбук:
```
- name: Install Vector
  hosts: vector
  remote_user: leo
  become: true
  roles:
    - vector-role
```


Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

