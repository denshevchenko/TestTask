# Public.DevopsTest

В этом репозитории содержится простое приложение `.NET Core` которое используется для проверки базовых знаний DevOps кандидатов.
Задания со звездочкой - не обязательные, но чем больше будет сделано, тем лучше.

## About Application
Данное приложение читает и записывает данные в/из  Redis. В приложении есть простой unit test. На нужно использовать этот тест в нашем CI.
Так же необходимо свормировать и предоставить приложению connection string до Redis. У приложения есть эндпоинт `http(s)://url:port/WeatherForecast`. Он принимает `POST` и `GET`. POST отправляет рандомный прогноз в Redis, GET - показывает все результаты из Redis. Никакие дополнительные параметры не требуются

## Test Tasks
1. Dockerfile
2*. docker-compose.yaml
3*. CI spec file

Обратите внимание, создание Dockerfile будет необходимо в любом случае.  Вы можете сделать часть заданий или даже написать часть кода и затем его объяснить на интервью

### 1. Dockerfile
Необходимо контейнеризовать наше приложение с мульти-сейдж сборкой для оптимизации полученного образа. Полученный образ не должен содержать никакого исходного кода. Только исполняемые артефакты.
*В докер-орбазе должна быть метка: environment со значением, которое предается при сборке докер-образа

### 2. Docker compose
Docker-compose должен быть основан на Dockerfile из предыдущего шага.  `docker-compose up` должна разворачивать и запускать все контейнры, включая приложение и Redis.
Приложение должно быть сконфигурировано для работы с запускаемым Redis и доступно на порту 80 за перемиетром контейнера(на localhost)

### 3. CI spec
Предпочтительно использовать синтаксис .gitlab-ci.yml, но не обязательно. CI должна выполнять следующие простые шаги:

1. Компиляция и контейнеризация
2. После создания контейнера, необходимо кастомизировать его(без пересборки), добавив файл changed.txt с текущем временем
3. push artifact
 
4* первым шагом можно добавить запуск юнит-теста. Это может быть либо отдельный шаг CI, либо запуск с помощью команды RUN в Dockerfile на Ваш выбор
