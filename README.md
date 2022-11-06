# **Performance Test Report**

**Ссылка на задание/требования:** https://github.com/netology-code/loadqa-homeworks/blob/main/5.Metrics/homework_lecture5.md

## **Ссылки на предыдущие работы:**

- Сбор информации и создание профиля нагрузки: https://docs.google.com/document/d/1J9hF8j1L7bee_kPHq0cSPWPLLIPMpg83siPEZ1CK8OE/edit?usp=sharing
- Мониторинг:

https://github.com/Vavlauz/TelegrafGrafana

https://github.com/Vavlauz/PrometheusNode

- Проведение нагрузочного тестирования WEB: https://github.com/Vavlauz/LoadTestWeb
- Проведение тестирования БД: https://github.com/Vavlauz/LoadDB

## **Содержание**

1. [Краткое описание](#краткое-описание)
2. [Задачи](#задачи)
3. [Используемые инструменты (ПО)](<#используемые-инструменты-(ПО)>)
4. [Ожидаемое количество посетителей сервиса бронирования билетов](#ожидаемое-количество-посетителей-сервиса-бронирования-билетов)
5. [Тестовая среда](#тестовая-среда)
6. [Результаты профиля нагрузочного тестирования сервиса бронирования билетов](#результаты-профиля-нагрузочного-тестирования-сервиса-бронирования-билетов)
7. [Результаты нагрузочного тестирования сервиса бронирования билетов](#результаты-нагрузочного-тестирования-сервиса-бронирования-билетов)
8. [Результаты объемного тестирования СУБД сервиса WordPress c постами и комментариями](#результаты-объемного-тестирования-СУБД-сервиса-WordPress-c-постами-и-комментариями)
9. [Результаты параллельного объемного и нагрузочного тестирования сервиса WordPress с постами и комментариями](#результаты-параллельного-объемного-и-нагрузочного-тестирования-сервиса-WordPress-с-постами-и-комментариями)
10. [Рекомендации для оптимизации сервиса бронирования билетов](#рекомендации-для-оптимизации-сервиса-бронирования-билетов)
11. [Рекомендации для оптимизации сервиса WordPress](#рекомендации-для-оптимизации-сервиса-WordPress)

## **Краткое описание**

Данный отчет представляет итоги проведения тестирования производительности сервиса бронирования билетов (нагрузочное тестирование), а также сервиса WordPress c постами и комментариями (объемное тестирование).

## **Задачи**

В рамках тетстирования производительности было несколько задач:

- Провести прогноз количества посетителей сервиса бронирования билетов при увеличении количества кинотеатров в разных городах;

- Создать профиль нагрузочного тестирования

- Определить параметры тестовой среды исходя из среды, на которой расположен сервис бронирования билетов;

- Провести нагрузочное тестирование сервиса бронирования билетов;

- Провести объемное тестирование СУБД сервиса WordPress c постами и комментариями;

- Провести параллельное объемное и нагрузочное тестирование сервиса WordPress с постами и комментариями;

- Оценить состояние базовых параметров оборудования/ОС при проведении нагрузочного тетстирования.

## **Используемые инструменты (ПО)**

- Для нагрузочного тетсирования: JMeter и BlazeMeter.

- Для объемного тестирования: JMeter.

- Для мониторинга системы: Telegraph + InfluxDB + Grafana (докер - контейнер) и node-exporter + prometheu + Grafana (докер - контейнер).

## **Ожидаемое количество посетителей сервиса бронирования билетов**

| Параметры                                                   | Результаты                                                                                                                             |
| ----------------------------------------------------------- |----------------------------------------------------------------------------------------------------------------------------------------|
| Количество посетителей в сутки во всех кинотеатрах          | Ожидается 10 млн посетителей в сутки во все кинотеатры сети, если предположить, что в будние и в выходные дни посещаемость одинаковая. |
| Влияение того, что города находятся в разных часовых поясах | В выходные дни с 16 до 20 по московскому времени совпадают пики посещаемости в Москве и во Владивостоке!!!                             |
| Ожидаемое количество посетителей на сайте в выходной день   | Гостей - 5 000 000, Пользователь - 4 000 000, Кинокритик - 999 999, Администратор - 1000                                               |

## **Тестовая среда**

| Параметры               | Значения          |
| ----------------------- |-------------------|
| Особенности сервера     | Выделенный сервер |
| Количество серверов     | 3                 |
| CPU - количество ядер   | 8 ядер            |
| RAM                     | 32 Гб             |
| Disk SSD                | 512 Гб            |
| Поправочный коэффициент | 2                 |

**Примечание:** тестирование выполнялось на ПК (процессор - Intel Pentium G 4620 with GeForce 1060 GTX), оперативная память - 16,00 ГБ (доступно: 12,00 ГБ). OS Windows 10.

## **Результаты профиля нагрузочного тестирования сервиса бронирования билетов**

| Параметры                                                                                        | Значения                                                                                           |
| ------------------------------------------------------------------------------------------------ |----------------------------------------------------------------------------------------------------|
| Роли                                                                                             | Гость (1 сценарий), Пользователь (2 сценария), Кинокритик (1 сценарий), Администратор (1 сценарий) |
| Общее количество сценариев                                                                       | 5                                                                                                  |
| Интервал, сек                                                                                    | 3600                                                                                               |                                                                                           |
| RPS                                                                                              | 460 040                                                                                            |
| RPS с учетом поправочного коэффициента                                                           | 230 020                                                                                            |

## **Результаты нагрузочного тестирования сервиса бронирования билетов**

**Примечание:** упрощение в том, что выполнялся один сценарий (покупка билета в кинотеатре и получение QR кода).

**Результаты при заданной (оптимальной) нагрузке с учетом рассчитанного количества посетителей сервиса**

RPS c учетом поправочного коэффициента: 230 020.

Схема достижения необходимого RPS: количество тредов - 50, количество повторений - 10.

Тест выполнялся в течение 5 минут.

[TestWeb](https://github.com/Vavlauz/TestReport/blob/master/TestWeb/HitPerSecond.png)

**Выводы:**

- Сервис эффективно работает при достижении заданного RPS.



## **Результаты объемного тестирования СУБД сервиса WordPress c постами и комментариями**

Сценарий: SQL запрос создания строки в таблице.

**Выводы:**

- Подтверждено, что в СУБД может быть создано больше 500 000 записей с комментариями

- Количество строк в таблице wp_comments не влияет на время отклика

## **Результаты параллельного объемного и нагрузочного тестирования сервиса WordPress с постами и комментариями**





**Выводы:**

- Если в таблице появляется около 10 000 записей, то пользователи будут ожидать загрузку страницы с комментариями более/равно 20 сек;

- Если в таблице появляется больше 21 500 записей, то пользователи не смогут добавить комментарий в графическом интерфейсе.

## **Рекомендации для оптимизации сервиса бронирования билетов**

- Сервис хорошо функционирует при заданных условиях нагрузки. Ресурсов системы достаточно для обеспечения бесперебойной работы.

- Явная оптимизация сервиса не требуется.

## **Рекомендации для оптимизации сервиса WordPress**

- Рекомендуется контролировать количество комментариев к одному посту. Не более 10 000 комментариев. Возможно переодическое удаление старых комментариев, если общее количество комментариев приближается к 9000. Также возможно оптимизация взаимодействия ПО бэкенда с СУБД. После оптимизации необходимо повторно провести параллельное объемное и WEB тестирование.

- При текущем состоянии строго не рекомендуется хранить более 11 000 комментариев к посту, поскольку это приведет к невозможности добавлять новые комментарии.
