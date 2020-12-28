# taskForWebbylab
Test task for Webbylab

<h2>ИНСТРУКЦИЯ</h2>

1. Установить локальный сервер (XAMPP, OpenServer ...)
2. Создать БД
3. Перенести файлы веб приложения в папку htdocs в xampp
4. В папке config в файле db.php указать данные для входа в БД
5. Перейти по ссылке http://localhost/<имя папки>/
6. Миграция таблицы films происходит автоматически.

<h2>ОПИСАНИЕ АРХИТЕКТУРЫ</h2>

Это веб приложение для хранения, отображения и изменения фильмов.
Для реализации базового функционала приложения использовал MVC + ООП
В основе приложения был написан простой скелет фреймворка с механизмом маршутизации

Всякий раз, когда вы делаете запрос к приложению, он будет направлен на index.php внутри общей папки.
htaccess разбивает все, что идет после http: // localhost / <имя папки>, и добавляет его к URL-адресу в качестве аргумента строки запроса. 
Затем splitUrl () разделит строку запроса $ _GET ['url'] на контроллер, метод и любые переданные аргументы методу.
В классе приложения run () он создает экземпляр объекта из класса контроллера и вызывает метод, передавая любые аргументы, если они существуют.

Каждая модель внутри приложения должна наследоваться от родительского класса Model(которая наследуется от класа DB). 
Это позволяет масштабировать приложение и гибко взаимодействовать с базой данных (постарался приблизить к подходу используемому в Laravel)

Каждый контроллер должен наследоваться от родительского класса Controller, который при инициализации создаёт экземпляры классов Request и Response.

<b>Request</b> - формирует набор аргументов из суперглобальных переменных POST, GET, FILE

<b>Response</b> - используется в родительском <b>View</b> для указания заголовков и ответов сервера. 

В веб приложении реализована возможность загрузки файла формата docx(или doc) через веб интерфейс, чтения и записи в БД. Файл должен соответствовать шаблону предоставленному в "Дополнении к ТЗ.docx"
Для отображения данных использовалась DataTables и Bootstrap. Сортировка, поиск и пагинация реализованы serverside.

Все взаимодействия с таблицей films происходят посредством ajax.
