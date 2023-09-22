# ВНИМАНИЕ!!!

Проект включен в состав основной поставки [Vanessa-Automation](https://github.com/Pr-Mex/vanessa-automation).</span>

Все Issues и Pull requests принимаются только для репозитория Vanessa-Automation. Проект в виде отдельной обработки развиваться и поддерживать не будет!

# Формирование дымовых тестов для фреймворка тестирования Vanessa-Automation

Точкой входа является обработка **"ФормированиеДымовыхТестовVA.epf"** которую необходимо запускать в клиенте 1С:Предприятие 8. 
Тестировалось на платформе 1С:Предприятие 8.3 (8.3.19.1723) и выше. Работает только на управляемых формах. От конфигурации не зависит. 

# Описание работы обработки:

Обработка анализирует метаданные конфигурации (в которой была запущена) и формирует пакет feature-файлов для дальнейшего их запуска в фреймворке тестирования [Vanessa-Automation](https://github.com/Pr-Mex/vanessa-automation).

![image](https://user-images.githubusercontent.com/25642145/233015973-84c507bb-6ee2-4508-bce9-0dc49fd57844.png)

## Настройки

**Каталог выходных файлов** - каталог, в котором будут созданы feature-файлы

**Каталог файлов исключений** - каталог, в котором хранятся текстовые файлы (*.txt) со списком объектов, которые будут исключены из тестирования.
Имена и количество файлов произвольные. Каждая строчка в файле - один исключаемый объект. Формат строки:

[ИмяОбъектаМетаданных].[ТипТеста].[Уточнение]

- [ИмяОбъектаМетаданных] - имя объекта конфигурации, как оно задано в конфигураторе 
- [ТипТеста] - тип теста, который требуется исключить, возможны варианты:
  - ФормаСписка - исключить открытие формы списка
  - ФормаОбъекта - исключить открытие формы объекта
  - Запись - исключить запись существующего элемента
  - Копирование - исключить копирование существующего элемента
  - ВводНаОсновании - исключить ввод на основании существующего элемента
  - Печать - исключить проверку печатных форм
- [Уточнение] - уточнение по типу теста, например:
  - Для записи - группа или элемент справочника. Если не указан, то и форма и элемент.
  - Для ввода на основании - тип документа, который необходимо исключить из ввода на основании. Если не указан, то все типы. 
  - Для печати - имя печатной формы, которую необходимо исключить из проверки. Если не указан, то все печатные формы.
  
*Примеры:*

> ТранспортноеСообщение

Полностью исключить из тестов объект с именем "ТранспортноеСообщение"

> ВерсииРасширений.Запись

Исключить из тестов запись объекта с именем "ВерсииРасширений"

> ГруппыДоступа.Запись.Группа

Исключить из тестов запись группы справочника с именем "ГруппыДоступа"

> ТребованиеНакладная.ВводНаОсновании

Исключить из тестов ввод объектов на основании документа с именем "ТребованиеНакладная"

> АвансовыйОтчет.ВводНаОсновании.СчетФактураПолученный

Исключить из тестов ввод объекта с именем "СчетФактураПолученный" на основании документа с именем "АвансовыйОтчет"

> СчетФактураВыданный.Копирование

Исключить из тестов копирование объекта с именем "СчетФактураВыданный"

> ПередачаОС.Печать

Исключить из тестов печать из объекта с именем "ПередачаОС"

> ПередачаОС.Печать.УниверсальныйПередаточныйДокумент

Исключить из тестов печать печатной формы "УниверсальныйПередаточныйДокумент" из объекта с именем "ПередачаОС"

Больше примеров можно посмотреть [здесь](https://github.com/Tavalik/VA-Tests-UH32-Smoke/tree/main/ОбъектыИсключения)

**Только измененные относительно конфигурации поставщика** - при включении данного флага будет выполнено сравнение текущей конфигурации с конфигурацией поставщика. В тесты войдут только объекты, которые отличаются относительно конфигурации поставщика. 

**Имя конфигурации поставщика** - Имя конфигурации поставщика, с которой будет проходить сравнение. Имеет смысл только при установке флага "Только измененные относительно конфигурации поставщика"

**Только введенные в информационную базу объекты для расширенных действий** - при включении данного флага для расширенных действий (записть, копирование, ввод на основании, печать) будут отбираться только те объекты, для которых существует хотя бы один элемент в информационной базе. 

На закладке **Настройка сценариев** можно настроить типы формируемых тестов по видам объектов метаданных

![image](https://user-images.githubusercontent.com/25642145/233015849-17609603-368d-431a-a278-3286ac180dcf.png)

# Параметры запуска

Возможен также автоматический режим работы обработки. Параметры запуска:

- КаталогВыходныхФайлов – каталог выходных файлов
- КаталогФайловИсключений – каталог файлов исключений
- ИмяКонфигурацииПоставщика – имя конфигурации поставщика
- ТолькоИзмененные – включение флага «Только измененные относительно конфигурации поставщика»
- Сформировать – формирование файла при запуске
- ЗавершитьРаботуСистемы – завершение работы системы после выполнения обработки


