Запуск WSGI приложений
1) Разверните репозиторий со своим проектом в директориию /home/box/web

2) Создайте WSGI приложение в файле /home/box/web/hello.py

WSGI приложение должно возвращать документ с MIME-типом text/plain, содержащий все GET параметры, по одному на каждую строку.

Например при запросе  /?a=1&a=2&b=3 приложение должно вернуть такой текст

a=1
a=2
b=3
3) Настройте Gunicorn таким образом, что бы он запускал приложение  /home/box/web/hello.py , и принимал соединения на IP адресе 0.0.0.0 на порту 8080 .  (Использования IP = 0.0.0.0 необходимо для тестирования). Конфиг разместить в файле /home/box/etc/hello.py и подключите его с помощью символической ссылки /etc/gunicorn.d/hello.py

4) Настройте nginx так что бы location /hello/ проксировался на cервер Guincorn

Таким образом, WSGI приложение должно быть доступно по URL

http://127.0.0.1/hello/
http://127.0.0.1:8080/
5) Не забудьте закомитить и сохранить на github полученную структуру директорий и конфиги.


1) git clone https://github.com/your_account/stepic_web_project.git /home/box/web
2) bash /home/box/web/init.sh
3) Вместо символических ссылок сделал так: 
    В файле--> sudo gedit /etc/nginx/nginx.conf
    захешировал(можно просто удалить) -->#include /etc/nginx/conf.d/*.conf;
                                                                   -->#include /etc/nginx/sites-enabled/*;
    добавил      --> include /home/box/web/etc/nginx.conf;