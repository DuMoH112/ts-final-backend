# Digital Assistant to Recruiting Officer
Реализация задачи для хакатона "Цифровой прорыв" в треке Газпромбанка: “Цифровой ассистент сотрудника по подбору персонала”

# Запросы к бэкенду

### Окружение
<table>
    <tr>
        <td>Token</td>
        <td>ImFkOGUwODA0MGQyNWMxY2E5ZTliMWEzZmQ2YzNjYzEwMTE3OThmYjIi.Xl9zsQ.sfwq6sx8a5FDqbc8_9Fg8CVEewY</td>
    </tr>
    <tr>
        <td>UserToken</td>
        <td>Токен, который приходит при авторизации</td>
    </tr>
    <tr>
        <td>url</td>
        <td>http://178.205.101.202:81</td>
    </tr>
</table>

Получить юзеров:

## Авторизация:

### {{url}}/auth

Тип: POST

Данные: JSON

Реквест:

```json
{
    "login": "username",
    "password": "password"
}
```

Результат:

```json
// Все ок
{
    "UserToken": "IJP98hbvVSAqDcGzWbhpCAPF-TaeI6_qjFldanPv-etW2tOUAfG3IFnJqwuTWIT6K8HQM0rjW14l28KewX3UfEGPWSDrZ9QwBzv-RgWLSn3RrLR47iOX6qh0zaf6ChF3X-h7DiB5tXZWi3cHfmGLGUVWE_2Paaoyvo-s9Tj8Nzelt82Fz37dPczruTYe873LrmMChM0qeDOM8mVosVSx06DZlyNKZ37oqEIbKKdxOZTd_aAiTHnU5PXbcBjNLImwdzW1x7U7mewSFzzpmuUKRBccJWxZsJywGatjT9DMHG_3OwTw2A-QkU-lNrk-SlTGKH8d9ehthOfGQJUWN7aEKg",
    "role": 2
}
// Ошибка пользователя
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

## Logout:

### {{url}}/logout

Тип: GET

Данные: JSON

Результат:

```json
// Все ок
{
	"message": "Пользователь вышел"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

## Получить справочники для составления вакансии:

### {{url}}/get_directories_for_vacancies

Тип: GET

Данные: JSON

Авторизация: да

Результат:

```json
// Все ок
{
    "grade": [
        [
            28,
            "Junior",
            "Младший разработчик"
        ],
        [
            29,
            "Middle",
            ""
        ]
    ],
    "job_responsibilities": [
        [
            26,
            "Сидеть",
            "Ты должен сидеть и ничего не делать"
        ]
    ],
    "professional_area": [
        {
            "id": 29,
            "specializations": [
                {
                    "description": "Разработка веб приложений",
                    "id": 29,
                    "title": "Веб-разработчик"
                }
            ],
            "title": "Разработка"
        },
        {
            "id": 30,
            "specializations": [
                {
                    "description": null,
                    "id": 30,
                    "title": "Инженер DevOps"
                }
            ],
            "title": "DevOps"
        },
        {
            "id": 31,
            "specializations": [
                {
                    "description": null,
                    "id": 31,
                    "title": "Главный инженер по тестированию (автоматизация)"
                }
            ],
            "title": "Тестирование"
        }
    ],
    "skills": [
        [
            30,
            "python"
        ],
        [
            31,
            "JavaScript"
        ]
    ],
    "soft_requirements": [
        [
            1,
            "Flask"
        ]
    ],
    "special_advantages": [
        [
            19,
            "Cookies",
            "Печеееееньки"
        ]
    ],
    "technologies_and_tools": [
        [
            1,
            "Курить бамбук вверх ногами"
        ]
    ],
    "type_employment": [
        [
            28,
            "Удалёнка"
        ]
    ],
    "work_address": [
        [
            28,
            "г. Москва, ул.Коровий вал, 5"
        ]
    ],
    "working_conditions": [
        [
            26,
            "График работы с 9:00 до 18:00",
            "График работы"
        ]
    ]
}
// Ошибка
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

## Создать вакансию:

### {{url}}/create_new_vacancy

Тип: POST

Данные: JSON

Авторизация: да

### Headers
<table>
    <tr>
        <td>Token</td>
        <td>{{Token}}</td>
    </tr>
    <tr>
        <td>UserToken</td>
        <td>{{UserToken}}</td>
    </tr>
</table>

Реквест:

Если значение есть в словаре, то вставляется id, иначе:

Подставляется для соответствующих полей структуры:

- title
- [title, description]

```json
{
    "grade": [["Junior", "Младший разработчик"]],
    "skills": ["python", "JavaScript"],
    "work_address": ["г. Москва, ул.Коровий вал, 5"],
    "type_employment": ["Удалёнка"],
    "professional_area": ["Разработка"],
    "specializations": [["Веб-разработчик", "Разработка веб приложений"]],
    "working_conditions": [["График работы с 9:00 до 18:00", "График работы"]],
    "job_responsibilities": [["Сидеть", "Ты должен сидеть и ничего не делать"]],
    "special_advantages": [["Cookies", "Печеееееньки"]],
    "soft_requirements": ["Flask"],
    "technologies_and_tools": ["Курить бамбук вверх ногами"],
    "is_testing": true
}
```

Результат:

```json
// Все ок
true
// Ошибка
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

## Получить все вакансии(вариант для смертных пользователей):

### {{url}}/get_all_vacancy

Тип: GET

Данные: JSON

Авторизация: необязательно

Результат для не авторизованного пользователя:

```json
// Все ок
[
    {
        "dt": 1606435200.0,
        "id": 20,
        "professional_area": "Разработка",
        "specialization": "Веб-разработчик"
    }
]
// Ошибка
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

Результат для HR:

```json
// Все ок
[
    {
        "dt": 1606521600.0,
        "id": 24,
        "professional_area": "Разработка",
        "specialization": "Веб-разработчик",
        "status": "Публикация"
    },
    {
        "dt": 1606521600.0,
        "id": 23,
        "professional_area": "Разработка",
        "specialization": "Веб-разработчик",
        "status": "Согласование на вакансию"
    }
]
// Ошибка
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

## Получить вакансию(вариант для смертных пользователей):

### {{url}}/get_vacancy/<int:vacancy_id>

Тип: GET

Данные: JSON

Авторизация: нет

Результат:

```json
// Все ок
{
    "dt": 1606521600.0,
    "grade": {
        "description": "Младший разработчик",
        "title": "Junior"
    },
    "job_responsibilities": [
        {
            "description": "Ты должен сидеть и ничего не делать",
            "title": "Сидеть"
        }
    ],
    "professional_area": "Разработка",
    "skills": [
        "python",
        "JavaScript"
    ],
    "soft_requirements": [
        "Flask"
    ],
    "special_advantages": [
        {
            "description": "Печеееееньки",
            "title": "Cookies"
        }
    ],
    "specialization": {
        "description": "Разработка веб приложений",
        "title": "Веб-разработчик"
    },
    "technologies_and_tools": [
        "Курить бамбук вверх ногами"
    ],
    "type_employment": [
        "Удалёнка"
    ],
    "work_address": "г. Москва, ул.Коровий вал, 5",
    "working_conditions": [
        {
            "description": "График работы",
            "title": "График работы с 9:00 до 18:00"
        }
    ]
}
// Ошибка
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

## Получить справочники для отклика на вакансию:

### {{url}}/get_directories_for_response_vacancy

Тип: GET

Данные: JSON

Авторизация: нет

Результат:

```json
// Все ок
{
    "skills": [
        [
            30,
            "python"
        ],
        [
            31,
            "JavaScript"
        ]
    ],
    "technologies_and_tools": [
        [
            1,
            "Курить бамбук вверх ногами"
        ]
    ]
}
// Ошибка
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

## Получить список статусов:

### {{url}}/get_directories_for_response_vacancy

Тип: GET

Данные: JSON

Авторизация: да

### Headers
<table>
    <tr>
        <td>Token</td>
        <td>{{Token}}</td>
    </tr>
    <tr>
        <td>UserToken</td>
        <td>{{UserToken}}</td>
    </tr>
</table>

Результат:

```json
// Все ок
[
    {
        "id": 1,
        "title": "Согласование на вакансию"
    },
    {
        "id": 2,
        "title": "Публикация"
    },
    {
        "id": 3,
        "title": "Приостановлено"
    }
]
// Ошибка
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

## Изменение статуса вакансии:

### {{url}}/change_status_vacancy

Тип: POST

Данные: JSON

Авторизация: да

### Headers
<table>
    <tr>
        <td>Token</td>
        <td>{{Token}}</td>
    </tr>
    <tr>
        <td>UserToken</td>
        <td>{{UserToken}}</td>
    </tr>
</table>

Реквест:

```json
{
    "status_id": 2, 
    "vacancy_id": 23
}
```

Результат:

```json
// Все ок
true
// Ошибка пользователя
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```

## Отклик на вакансию:

### {{url}}/response_vacancy

Тип: POST

Данные: JSON

Авторизация: нет

Реквест:

```json
{
    "firstname": "Петр",
    "lastname": "Петечник",
    "number_phone": "+7-777-777-77-77",
    "link_social_network": "my-soc-set.com",
    "resume": "binary",
    "skills": [30,31],
    "technologies_and_tools": [1],
    "answers": [[3,2]],
    "vacancy_id": 24
}
```

Результат:

```json
// Все ок
true
// Ошибка пользователя
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```


## Анализ кандидатов:

### {{url}}/analiz_all_candidates

Тип: GET

Данные: JSON

Авторизация: да

### Headers
<table>
    <tr>
        <td>Token</td>
        <td>{{Token}}</td>
    </tr>
    <tr>
        <td>UserToken</td>
        <td>{{UserToken}}</td>
    </tr>
</table>

Результат:

```json
// Все ок
[
    {
        "candidates_firstname": "Вася",
        "candidates_id": 8,
        "candidates_lastname": "Петечник",
        "score": 87,
        "specializations_title": "Веб-разработчик",
        "status_title": "Приглашён на собеседование",
        "vacancy_id": 24
    },
    {
        "candidates_firstname": "Петр",
        "candidates_id": 9,
        "candidates_lastname": "Петечник",
        "score": 82,
        "specializations_title": "Веб-разработчик",
        "status_title": "Выдан оффер",
        "vacancy_id": 24
    }
]
// Ошибка
{
	"message": "text"
}
// Ошибка сервера
{
	"messageError": "text"
}
```
