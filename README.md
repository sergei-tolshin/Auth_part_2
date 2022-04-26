# Проектная работа 7 спринта

## Задание 1
Упростите регистрацию и аутентификацию пользователей в Auth-сервисе, добавив вход через социальные сервисы. Список сервисов выбирайте исходя из целевой аудитории онлайн-кинотеатра — подумайте, какими социальными сервисами они пользуются. Например, использовать [OAuth от Github](https://docs.github.com/en/free-pro-team@latest/developers/apps/authorizing-oauth-apps){target="_blank"} — не самая удачная идея. Ваши пользователи не разработчики и вряд ли имеют аккаунт на Github. А вот добавить Twitter, Facebook, VK, Google, Yandex или Mail будет хорошей идеей.

Вам не нужно делать фронтенд в этой задаче и реализовывать собственный сервер OAuth. Нужно реализовать протокол со стороны потребителя.

Информация по OAuth у разных поставщиков данных: 

- [Twitter](https://developer.twitter.com/en/docs/authentication/overview){target="_blank"},
- [Facebook](https://developers.facebook.com/docs/facebook-login/){target="_blank"},
- [VK](https://vk.com/dev/access_token){target="_blank"},
- [Google](https://developers.google.com/identity/protocols/oauth2){target="_blank"},
- [Yandex](https://yandex.ru/dev/oauth/?turbo=true){target="_blank"},
- [Mail](https://api.mail.ru/docs/guides/oauth/){target="_blank"}.

### Дополнительное задание

Реализуйте возможность открепить аккаунт в соцсети от личного кабинета. 
Решение залейте в репозиторий текущего спринта и отправьте на ревью.


## Задание 2
Подготовьте Auth сервис к интеграции с другими сервисами вашего сайта. Сгенерируйте схему взаимодействия с Auth сервисом в формате, который используется в вашем сервисе.

## Задание 3
Создайте интеграцию Auth-сервиса и AsyncAPI-сервиса, используя контракт, который вы сделали в прошлом задании.
При создании интеграции не забудьте учесть изящную деградацию Auth-сервиса. Как вы уже выяснили ранее, Auth сервис один из самых нагруженных, потому что в него ходят большинство сервисов сайта. И если он откажет, сайт отказать не должен. Обязательно учтите этот сценарий в интеграциях с Auth-сервисом.

## Задание 4
Добавьте в Auth трасировку и подключите к Jaeger. Для этого вам нужно добавить работу с заголовком x-request-id и отправку трасировок в Jaeger.


## Задание 5
Сейчас сервис Auth беззащитен перед DDOS-атаками. Чтобы сберечь важный элемент системы от чрезмерной нагрузки, которая может вывести его из строя, реализуйте алгоритм Leaky bucket или Token bucket, используя Redis для синхронизации реплик. Впоследствии вы можете делегировать эту обязанность сторонниму инструменту, например, Cloudflare.


## Задание 6
Партицируйте таблицу с пользователями. Подумайте, по каким критериям вы бы разделили её. Важно посмотреть на таблицу не только в текущем времени, но и заглядывая в некое будущее, когда в ней будут миллионы записей. Пользователи могут быть из одной страны, но из разных регионов. А еще пользователи могут использовать разные устройства для входа и иметь разные возрастные ограничения.

____

### Задание со звёздочкой 1
Реализуйте свой вариант фильтрации ботов для Smart TV. На Smart TV не будет работать noCaptcha, потому что в нём вряд ли есть история, а анализировать поведение пользователя очень сложно из-за механики работы умного телевизора. Вам придётся реализовать каптчу на математических примерах: генерировать простую задачку и отправлять её пользователю.
Подумайте, в какой из баз данных вы будете хранить правильный ответ. Дадите ли вы только один шанс ввести правильный ответ или позволите пользователю ошибаться несколько минут подряд? Станете ли с подозрением относиться к ответам, которые приходят слишком часто для человека?

### Задание со звездочкой 2
Из коробки библиотека `opentelemetry` предоставляет контекстный менеджер `tracer.start_as_current_span()`, но это не всегда удобно. Например, вы хотите пометить трасировкой не весь код, а отдельные функции.
Сделайте декоратор `@trace` для трассировок любых функций.
