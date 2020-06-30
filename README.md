
# VitaliyStrashnenko_microservices
VitaliyStrashnenko microservices repository

# CI/CD в Kubernetes

    Установлен helm версии 2 и 3.
    Создан манифест Tiller и применен к инфраструктуре kubernetes.
    Созданы Chart'ы для компонентов приложения.
    Проинсталлировано приложение и все его компоненты с использованием helm.
    Настроено взаимодействие между компонентами через общий Chart.
    Установлен gitlab с omnibus с помощью Helm. (нужно не забывать ставить галочку про устаревшие права в GCE).
    Созданы проекты UI, Comment и Post для создания через pipeline gitlab контейнеров этих приложний и заливка их в dockerhub.
    Создан центральный проект reddit-deploy для автоматического развертывания инфраструктуры в разных environment'ах.
    Для каждого приложения создан свой .gitlab-ci.yml конфиг для разных pipeline.
    Модернизированы .gitlab-ci.yml конфиги всех приложений для развертывания с разных версий helm.

# Kubernetes: Networks, Storages

    Детально изучили абстракцию Service
    Изучили тип подключения ClusterIP
    Изучили тип подключения NodePort
    Изучили тип подключения LoadBalancer
    Изучили тип подключения Ingress
    Изучили конфигурацию Secret
    Настроили TLS Termination
    Настроили Network Policy для нашего приложения в GKE
    Изучили механизмы хранения данных (Volume): emptyDir, gcePersistentDisk
    Изучили механизм выделения и нахначения ресурсов хранения для K8s: PersistentVolume, PersistentVolumeClaim


# Основные модели безопасности и контроллеры в Kubernetes

    Установили локально cubectl , minicube
    Ознакомились со конфигурацией и структурой комманд Kubectl
    Изменили созданные ранее Deployment-ы приложения reddit
    Задеплоили их на кластер и сконфигурровали для работы готового приложения
    Создали ресурсы с типом Services - для сетевого взапимодействия Pod-ов
    Создали свой Namespaces dev - и развернули там отдельную версию
    Развернули кластер Kubernetes в GKE
    Создали проект для создания клатсера из terraform


# Введение в Kubernetes

    Установили Kubernetes . В связи с лимитам GCE (4 публичных IP адреса) - пришлось сократить до 4 нод. 
    Создали конфиги деплоя микросервисов приложения reddit
    Протестировали что все конфиги успешно деплоятся на созданный кластер


#  Логирование и распределенная трассировка
 Установлен код измененного приложения
 Создан и настроен контейнер fluentd для сбора лог сообщений и пересылки их в контейнер с Elasticsearch
 Настроено развертывания контейнера Elasticsearch и Kibana для сбора логов и отображения в графическом виде
 Настроен сбор лог сообщений с сервисов post и ui с использованием fluentd
 Рассмотрено отображение лог сообщений в elasticsearch и kibana
 Настроен парсинг лог сообщений с использованием конфигурации fluentd при помощи json формата отображения логов, grok патернов и регулярных выражений
 Рассмотрен вариант отслеживания проблем и задержек в web приложении с использование zipkin.

#  Мониторинг приложенияи инфраструктурыи инфраструктуры

    Создали отдельный docker-compose конфигурацию для сервисов мониторинга
    Подключили сервис cAdvisor - и посмотриели на его работу
    Подключили сервис Grafana, настроили источник данных Prometheus, импортировали дашборд
    Создали свой дашборд и добавили туда несколько панелей с Графиками, Гистограммами, Перцнетилями
    Построили панель с бизнес метриками
    Добавили сервис с алертами, проверили его работспособность


# Введение в мониторинг. Системы мониторинга

    Развернули контейнер с Prometheus - посмотрели его встроенные метрики
    В ранее созадную конфигурацию микросервисов внесли сервис по мониторингу, и проверили что они выключились в endpoint
    Поигрались с health-checks для нашей конфигурации микросервисов
    Добавили NodeExporter в конфигурацию. проверили ее работу
    Добавили MongoExporter в конфигурацию. проверили ее работу
    Добавили BlackboxExporter в конфигурацию. проверили ее работу
    Написали Makefile для сборки и отправки образов на hub


# Устройство Gitlab CI. Построение процесса непрерывной интеграции

 Развернули Gitlab CI  через Docker образ в режиме Omnibus
 Зашли под пользователем  root и скофигурировали  безопасноть.
 Создали группу проектов homework и проект example
 Добавили наши исходники в проект и запушили его на CI
 Создали pipeline и поигрались с ним в  stag-и , job-ы, environment
 Создали и зарегистрировали runner
 Залили исходники  reddit. создали Job для  его сборки и деплоя
 Сконфигурировали создание динамических окружений

# Сетевое взаимодействие Docker контейнеров. Docker Compose. Тестирование образов 

Изучили различные виды сетей используемых в docker:
    
    Посомтрели на то как устроен сетевой стек сетей docker
    Изучили утилиту docker-compose и структуру docker-compose.yml
    Сконфигурировали приложение для использования сетей в compose-file и конфигурацию через env файлы
    Задать имя проекта можно через переменную среды COMPOSE_PROJECT_NAME или через параметр -p, --project-name NAME при запуске docker-compose

ДЗ*

    Исходники монтируются через volume
    Используется параметризиорванная комманда запуска


# Docker образы. Микросервисы
    1 VS-code установили линтер Hadolint
    2 Скачали исходники сайта и разместили их у себя в репозитории
    3 Создали на кадлый сервис по Dockerfile и создали из них образы
    4 На основе созданных образов запустили сайт
    5 Создали Docker Volume для MongoDb - для хранения состояния между перезапусками новых версий контейнеров
    
ДЗ*

    1 Создан файл с переменными.
    2 Образы оптимизированы путем частичного уменьшеиня слоев и удалением кешей закачки пакетного менеджера apk


# Docker контейнеры. Docker под капотом.
    - Установили docker и docker-machine
    - Bзучил основные комманды
    - Завели новый проект в GCP
    - Через docker-machine в GCE - подняли новую машину с установленным docker
    - Изучили примение Ansible как провижининг в Packer
    - Создали Dockerfile и сбилдили новый image
    - Через docker-machine развернули его в GCP
    - Не Затегировали образ, и залили его на docker hub

ДЗ* Не выполнял выполнял
