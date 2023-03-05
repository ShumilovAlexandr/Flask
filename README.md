**Суть работы**<br>
Необходимо написать бекенд для работы с приложением React, которое позволяет  пользователю зарегистрироваться и загрузить файл на сервер для обработки. После асинхронной обработки пользователь сможет посмотреть информацию о своем файле. Непринципиально какая именно обработка файла: сервер может посчитать количество строк в файле, обрезать видео файл и т.д.

Приложение React общается с бекендом по GraphQL. Соответственно нужны методы для регистрации, логина, логаута пользователей, аплоада файла и просмотра информации о нем. 

**Как запустить**
1. Копируйте проект по команду git clone 'https://github.com/ShumilovAlexandr/Flask'
2. Создайте виртуальное окружение команой python -m venv venv
3. Установите зависимости из файла requirements.py
4. Запускаете его в любом текстовом редакторе в папке api/ командой ****flask run****.
5. Далее - можете тестировать приложение в Postmane, или в браузере по ссылке [localhost](http://127.0.0.1:5000/graphql).

**Пример запроса через Postman**
Когда запустите сервис, на запрос 
   POST http://127.0.0.1:5000/login

осуществляется регистрация нового пользователя в базу данных Postgres.
По данному же маршруту, но с заменой login на signup происходит добавление уже зарегистрированного пользователя из базы данных в сессию.

Далее, по запросу
   POST http://127.0.0.1:5000/process

и указанием в body -> form-data в VALUE названия и пути для файла, а в KEY типа файла, можно выполнить его обработку с последующей выдачей результата. **ВНИМАНИЕ!** Приложение обрабатывает только текстовые файла формата .txt. Обработку файла может выполнить только залогиненый пользователь

Когда пользователь закончит работу, выход активного пользователя можно выполнить следующим образом по маршруту: 
   POST http://127.0.0.1:5000/logout

Полный список пользователей из базы данных можно получить следующим образом по маршруту: 
   GET http://127.0.0.1:5000/users

Данные конкретного пользователя можно получить по следующему маршруту:
   GET http://127.0.0.1:5000/users/<id>/
   
где id - это айди конкретного пользователя.

**Тестирование через GraphQL**
Запрос через (http://127.0.0.1:5000/graphql) выглядит следующим образом:
```
    mutation {
      usermutation(username: username, email: email, password: password) {
      users{
            username
            email
            password
          }
        }
    }
```
По ссылке (http://127.0.0.1:5000/graphql) указана подобная схема с возможными запросами.

**Используемые технологии** <br>
![PyPI - GraphQl-core Version](https://img.shields.io/badge/GraphQl-3.2.3-green)
![PyPI - Flask Version](https://img.shields.io/badge/Flask-2.2.2-blue)
![PyPI - Python Version](https://img.shields.io/badge/Python-3.10.8-blue)
