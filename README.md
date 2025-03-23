### Лекция 3: Создание моделей, контроллеров и представлений

#### Шаг 1: Включение Gii
1. Откройте файл `config/web.php` в вашем проекте.
2. Найдите раздел `modules` и добавьте следующий код:
   ```php
   'modules' => [
       'gii' => [
           'class' => 'yii\gii\Module',
           'allowedIPs' => ['127.0.0.1', '::1'], // Разрешить доступ только с localhost
       ],
   ],
   ```
3. Сохраните файл.


---


#### Шаг 2: Доступ к Gii
1. Откройте браузер и перейдите по адресу `http://cleaning_portal/web/index.php?r=gii` **ИЛИ** `http://xxxxxx-m1/web/index.php?r=gii`.
2. Вы увидите интерфейс Gii.

![image](https://github.com/user-attachments/assets/6d114b8a-5be2-45af-a65d-8c6dd70e0a30)


---


#### Шаг 3: Создание моделей
Модели в Yii2 представляют таблицы базы данных и используются для работы с данными.

##### Модель для таблицы `users`:
**ВАЖНО!** В архиве с проектом Yii2 по умолчанию уже есть модель `User`. Переименуйте ее, например в `User1` или `UserOld` 

1. В интерфейсе Gii выберите **Model Generator**.
2. Заполните поля:
   - Table Name: `users`
   - Model Class: `User`
3. Нажмите **Preview**, затем **Generate**.
4. Модель будет создана в папке `models/User.php`.

![image](https://github.com/user-attachments/assets/fea50e9b-3b1f-47b4-b5ab-849e0c66c829)


---


##### Модель для таблицы `requests`:
1. В интерфейсе Gii выберите **Model Generator**.
2. Заполните поля:
   - Table Name: `requests`
   - Model Class: `Request`
3. Нажмите **Preview**, затем **Generate**.
4. Модель будет создана в папке `models/Request.php`.

![image](https://github.com/user-attachments/assets/063e476e-1a12-4885-80e1-89588fc221e5)


---


#### Шаг 4: Создание CRUD для заявок
CRUD (Create, Read, Update, Delete) — это стандартные операции для работы с данными. Мы создадим CRUD для таблицы `requests`.

1. В интерфейсе Gii выберите **CRUD Generator**.
2. Заполните поля:
   - Model Class: `app\models\Request`
   - Search Model Class: `app\models\RequestSearch`
   - Controller Class: `app\controllers\RequestController`
   - View Path: `@app/views/request`
3. Нажмите **Preview**, затем **Generate**.
4. Gii создаст контроллер `RequestController` и представления для CRUD в папке `views/request/`.


![image](https://github.com/user-attachments/assets/f2745013-ecd9-4c6f-9ccf-44d40b14de19)


---


#### Шаг 5: Создание CRUD для пользователей
Теперь создадим CRUD для таблицы `users`. 

1. В интерфейсе Gii выберите **CRUD Generator**.
2. Заполните поля:
   - Model Class: `app\models\User`
   - Search Model Class: `app\models\UserSearch`
   - Controller Class: `app\controllers\UserController`
   - View Path: `@app/views/user`
3. Нажмите **Preview**, затем **Generate**.
4. Gii создаст контроллер `RequestController` и представления для CRUD в папке `views/user/`.


![image](https://github.com/user-attachments/assets/408b9676-302c-40b9-a93f-8c9059a39acc)


---


#### Шаг 6: Настройка маршрутов
1. Откройте файл `config/web.php`.
2. Раскоментируйте Url Manager:
   ```php
   'components' => [
       'urlManager' => [
           'enablePrettyUrl' => true,
           'showScriptName' => false,
           'rules' => [
               'user/register' => 'user/register',
               'request/create' => 'request/create',
           ],
       ],
   ],
   ```

![image](https://github.com/user-attachments/assets/c588ac77-2bc6-4c6e-952f-7b2d330678b3)

![image](https://github.com/user-attachments/assets/57390ea0-a3bc-42f2-a0e7-5ae816db84de)


---


#### Шаг 7: Проверьте работу CRUD
1. Откройте браузер и перейдите по следующим адресам:
   - `http://cleaning_portal/web/user/index`
   - `http://cleaning_portal/web/user/create`
   - `http://cleaning_portal/web/user/update` **Должна быть ошибка #400**
   - `http://cleaning_portal/web/user/delete` **Должна быть ошибка #405**
   - `http://cleaning_portal/web/request/index`
   - `http://cleaning_portal/web/request/create`
   - `http://cleaning_portal/web/request/update` **Должна быть ошибка #400**
   - `http://cleaning_portal/web/request/delete` **Должна быть ошибка #405**

2. Как вы видете, Yii2 создал формы добавления в базу данных. Далее, `user/create` мы будем использовать для регистрации


---

### Итог
Теперь у вас есть:
- Модели `User` и `Request` для работы с данными.
- Контроллеры `UserController` и `RequestController`.
- Представления для регистрации пользователей и работы с заявками.

В следующей лекции мы реализуем функционал регистрации, авторизации и создания заявок.
