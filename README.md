# ForexService
Микросервисы для конвертации валют

1) Forex сервис (REST сервис на основе Spring Boot Starter Web, Spring Boot Started JPA, Hibernate для реализации JPA и подключения к базе данных H2).
Forex Service (FS) является поставщиком услуг. Он обеспечивает значения курсов обмена валюты для различных валют.
Сервис создан в плагине Spring Tool Suite, использованы следующие зависимости:

— Web
— DevTools
— Стартер JPA
— H2

2) Функция Spring Boot Dashboard,  запускает приложение в среде, когда приложение запущено, 
укажите в веб-браузере http://localhost:8080/h2-console (нажмите кнопку Глобус на панели Spring Boot Dashboard), автоматически активируется консоль H2 (база данных,
с которыми работает приложение). Исходные данные для таблицы exchange_value, находятся в файле data.sql(папка ресурсы).
Spring Boot выполнит этот скрипт после того, как таблицы будут созданы из сущностей.

3)Тестируем Forex микросервис. Вводим в браузере  http://localhost:8000/currency-exchange/from/EUR/to/INR
Получаем ответ в Json файле  - обменный курс EUR к INR равен 75
{
  id: 10002,
  from: "EUR",
  to: "INR",
  conversionMultiple: 75,
  port: 8000,
}

 4) Далее создаем второй микросервис - сервис конвертации валют (CCS), он конвертирует заданное количество валюты
 в другую валюту, по обменному курсу, полученному с Forex сервиса. Исходный код CCS  смотри в репо MicroserviceCurrencyConversion
 
 запуск (CCS) MicroserviceCurrencyConversion, аналогичен Forex сервису. Для тестерирования  вводим в браузере 
 http://localhost:8100/currency-converter/from/EUR/to/INR/quantity/10000
 получаем ответ в Json файле
 {
  id: 10002,
  from: "EUR",
  to: "INR",
  conversionMultiple: 75,
  quantity: 10000,
  totalCalculatedAmount: 750000,
  port: 8000,
}
Запрос выше позволяет определить стоимость 10000 евро в индийских рупиях.
TotalCalculatedAmount составляет 750000 INR, тестирование показывает, что связь между CCS и FS сервисами установлена.
