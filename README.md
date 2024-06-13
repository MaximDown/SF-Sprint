# SkillFactory
Итоговый проект - Виртуальная стажировка

<b>Профессия Python-разработчик<b><br>
<i><b>PDEV-43, m.maslennikov</b></i>

В рамках итоговой аттестации был разработан проект REST API для Федерации Спортивного Туризма России (ФСТР).

# Были созданы

	•	БД
 	•	Классы по работе с БД
 	•	REST API

# REST API

## 1) POST/pereval/ - Ввод информации о туристе и перевале

	•	ФИО, эл. почта, телефон
 	•	Название перевала
	•	Координаты перевала и его высоту
 	•	Несколько фотографий перевала  

Результат POST-запроса:

	•	status — код HTTP, целое число:
    - 500 — ошибка при выполнении операции
    - 400 — Bad Request (не все поля заполнены)
    - 200 — успех
       
	•	message — строка:
    - Причина ошибки (если она была)
    - Отправлено успешно
    - Если отправка успешна, дополнительно возвращается id вставленной записи
     
_Пример запроса:_

{
  "beauty_title": "string",
  "title": "string",
  "other_titles": "string",
  "connect": "string",
  "user": {
    "email": "string",
    "last_name": "string",
    "first_name": "string",
    "patronymic": "string",
    "phone": "string"
  },
  "coords": {
    "latitude": "19.",
    "longitude": "79.84803",
    "elevation": 2147483647
  },
  "level": {
    "winter": "1A",
    "spring": "1A",
    "summer": "1A",
    "autumn": "1A"
  },
  "images": [
    {
      "images": "string",
      "title": "string"
    }
  ]
}

_Примеры ответа:_

{ "status": 500, "message": "Ошибка подключения к базе данных","id": null}

{ "status": 200, "message": null, "id": 42 }


## 2) GET/pereval/\<id> - Метод позволяет получить всю информацию о перевале по её id, в том числе статус модерации

## 3) PATCH/pereval/\<id> - Метод позволяет частично отредактировать существующую запись, если она в статусе <i>new</i>


После того, как турист добавит в БД информацию о новом перевале, сотрудники ФСТР проведут модерацию для каждого нового объекта и поменяют поле status. Допустимые значения: new, pending, accepted, rejected.

# Что может пользователь с помощью этого REST API

	•	Создавать новые объекты перевала со своими данными, загружать фотографии (в текущей реализации они сохраняются в виде ссылок)
 
 	•	Просматривать статус модерации для объекта
  
  	•	Просматривать все объекты, когда-либо отправленные на сервер самим пользователем, а также их статусы
   
   	•	Редактировать отправленные на сервер данные об объекте, если они в статусе new. 
    	При этом пользователь может редактировать все поля, кроме тех, что содержат в себе ФИО, адрес почты и номер телефона
    
JSON-схема API будет генерироваться по адресу: http://127.0.0.1:8000/api/schema/, по ней будет строиться Swagger-UI документация по адресу: http://127.0.0.1:8000/api/docs/

Код покрыт тестами, отчет находится в [файле](https://github.com/MaximDown/SF-Sprint/blob/main/FSTR/htmlcov/index.html)

