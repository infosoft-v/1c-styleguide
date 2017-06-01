# 1С: Руководство по стилю оформления

> Почти все убеждены, что любой стиль кроме их собственного ужасен и нечитаем. Уберите отсюда "кроме их собственного" — и они будут, наверное, правы... 
> 
> -- Джерри Коффин (Jerry Coffin) об отступах

## Соглашение о наименовании

- Используйте CAPS LOCK для обозначения переменных, которые будут выполнять роль констант 
```bsl
СТАТУС_ОТПРАВКИ_OK  = 1;
СТАТУС_ОТПРАВКИ_ERR = 2;
``` 

- Используйте [венгерскую](https://ru.wikipedia.org/wiki/%D0%92%D0%B5%D0%BD%D0%B3%D0%B5%D1%80%D1%81%D0%BA%D0%B0%D1%8F_%D0%BD%D0%BE%D1%82%D0%B0%D1%86%D0%B8%D1%8F "wikipedia") нотацию в именах переменных

| Тип                         | Русское | Английское | Пример               |
| --------------------------- | ------- | ---------- | -------------------- |
| **Примитивные типы**                                                      |
| число                       | ч   | n   | `чКоличество; nNumber`          |
| строка                      | с   | s   | `сТекст; sError`                |
| дата                        | д   | d   | `дНачало; dBegin`               |
| булево                      | б   | b   | `бФлаг; bFlag`                  |
| **Универсальные коллекции**                                               |
| массив                      | м   | a   | `мДокументы; aDocs`             |
| структура                   | ст  | st  | `стПараметры; stParam`          |
| таблица значений            | тз  | vt  | `тзТовары; vtGoods`             |
| дерево значений             | дз  | tr  | `дзДокумент; trDoc`             |
| соответствие                | со  | mp  | `соАдреса; mpAddr`              |
| список значений             | сз  | vl  | `сзФорма; vlForm`               |
| **Типы прикладных объектов**                                              |
| ссылка на прикладной объект | реф | ref | `рефСпрНоменклатура; refCatGoods` |
| сам прикладной объект       | о   | obj | `оСпрНоменклатура; objCatGoods`   |
| справочник                  | Спр | Cat | `рефСпрНоменклатура; refCatGoods` |
| документ                    | Док | Doc | `рефДокАкт; refDocAct`          |
| регистры сведений           | РС  | IR  | `РСОстатки; IRRemain`           |
| регистры накоплений         | РН  | AR  | `РНОстатки; ARRemain`           |

- Для переменных модуля используйте префикс `м_`
```bsl
Перем м_рефCOMобъект;
```

- Используйте стиль [CamelCase](https://ru.wikipedia.org/wiki/CamelCase) при именовании переменных и методов. Так же в наименованиях допустимы суффиксы, указанные через `_`
```bsl
Перем бВыполненоБезОшибок = Истина;

Процедура УдалитьВременныеФайлы_Локально()
    // код метода
КонецПроцедуры

Процедура УдалитьВременныеФайлы_УдСервер()
    // код метода
КонецПроцедуры
```

- Не используйте отрицание в именах переменных и методов
```bsl
// Плохо:
Функция ПроверкаНеПройдена()

// Хорошо:
Функция ПроверкаПройдена()
```

## Оформление модулей

- Длина строки в общем случае не должна превышать 120 символов.
- Для отступов необходимо использовать символы табуляции.
- Одна строка кода - одна управляющая конструкция.
 
```bsl
// Плохо:
Если бЭтоБрак Тогда Продолжить; КонецЕсли;

// Хорошо:
Если бЭтоБрак Тогда
  Продолжить;
КонецЕсли;
```
- Следует отделять друг от друга пробелами ключевые слова, вызовы процедур и функций, параметры процедур и функций внутри скобок, операторы.

```bsl
// Плохо:
Сообщить(“Сумма: “+Сумма);

// Хорошо:
Сообщить(“Сумма: “ + Сумма);
```

- Для разделения на логические части внутри модуля следует использовать пустые строки
- При вызове функции с несколькими параметрами при переносе строк необходимо выравнивать параметры по первому

```bsl
// Начальное состояние (строка слишком длинная):
НалоговыйУчет.ОстаткиВременныхРазниц(СтрокаВидАктиваОбязательства, СписокОрганизаций, Реквизиты.НачалоГода, Реквизиты.КонДата);

// Плохо:
НалоговыйУчет.ОстаткиВременныхРазниц(
    СтрокаВидАктиваОбязательства, СписокОрганизаций, Реквизиты.НачалоГода, Реквизиты.КонДата);

// Лучше:
НалоговыйУчет.ОстаткиВременныхРазниц(СтрокаВидАктиваОбязательства,
                                     СписокОрганизаций,
                                     Реквизиты.НачалоГода,
                                     Реквизиты.КонДата);

// Хорошо:
НалоговыйУчет.ОстаткиВременныхРазниц(
    СтрокаВидАктиваОбязательства,
    СписокОрганизаций,
    Реквизиты.НачалоГода,
    Реквизиты.КонДата);
    
```

- Выравнивание однотипных операторов. При следовании друг за другом нескольких однотипных операторов допускается их выравнивание. Выравнивание следует выполнять с помощью пробелов

```bsl
// Хорошо:
НоваяСтрока = ВидыОпераций.Добавить();
НоваяСтрока.ВидОперации         = ВидОперации;
НоваяСтрока.НомерГруппы         = ГруппаПоВидуОперации(ВидОперации);
НоваяСтрока.ПоОрганизацииВЦелом = ГруппаПоОрганизации(НоваяСтрок);
```

### Методы

- Метод должен иметь описание созданное с помощью команды "Создать описание процедуры" (щелчек правой кнопкой мыши на наименовании метода - Рефакторинг - Создать описание процедуры)

- Параметр функции не должен возвращать значение. Иными словами не используйте входные параметры функций как дополнительный вывод. Весь вывод должен быть в возвращаемом значении. Если нужно возвращать несколько значений следует использовать такие типы как `Структура`, `Массив` и т.д.
```bsl
// Плохо:
URLСервиса = "";
ИмяПользователя = "";
ПарольПользователя = "";

ЗаполнитьПараметрыПодключения(URLСервиса, ИмяПользователя, Пароль);

// Хорошо:
ПараметрыПодключения = ПолучитьПараметрыПодключения();
// Возвращаемое значение - структура:
//     URLСервиса         - Строка
//     ИмяПользователя    - Строка
//     ПарольПользователя - Строка
```

### Условия
- Предпочтительней использовать тернарный оператор для простых конструкций.
```bsl
// Плохо:
Если НДС0 Тогда
    Возврат 0;
Иначе
    Возврат 18;
КонецЕсли;

// Хорошо:
Возврат ?(НДС0, 0, 18);
```

- Не допускайте использования вложенных тернарных операторов.
- Ключевое слово `Тогда` пишется на той же строке, что и последнее условие.
- Сложные условия (содержащие 3  конструкции и более) необходимо выносить в отдельные методы.

```bsl
// Плохо:
Если ИдентификаторОбъекта = "АнализСубконто"
    ИЛИ ИдентификаторОбъекта = "АнализСчета"
    ИЛИ ИдентификаторОбъекта = "ОборотноСальдоваяВедомость"
    ИЛИ ИдентификаторОбъекта = "ОборотноСальдоваяВедомостьПоСчету"
    ИЛИ ИдентификаторОбъекта = "ОборотыМеждуСубконто"
    ИЛИ ИдентификаторОбъекта = "ОборотыСчета"
    ИЛИ ИдентификаторОбъекта = "СводныеПроводки" 
    ИЛИ ИдентификаторОбъекта = "ГлавнаяКнига"
    ИЛИ ИдентификаторОбъекта = "ШахматнаяВедомость" Тогда
    ПараметрыРасшифровки.Вставить("ОткрытьОбъект", Ложь);
		
    ЕстьПоказатель  = Ложь;
    ЕстьКорЗначение = Ложь;
    ЕстьСчет        = Истина;
    Счет            = Неопределено;
    ПервыйЭлемент   = Неопределено;
КонецЕсли;

// Хорошо:
Если ОткрыватьОбъектПриИдентификаторе(ИдентификаторОбъекта) Тогда
    ПараметрыРасшифровки.Вставить("ОткрытьОбъект", Ложь);
		
    ЕстьПоказатель  = Ложь;
    ЕстьКорЗначение = Ложь;
    ЕстьСчет        = Истина;
    Счет            = Неопределено;
    ПервыйЭлемент   = Неопределено;
КонецЕсли;

Функция ОткрыватьОбъектПриИдентификаторе(ИдентификаторОбъекта)
	
    Возврат ИдентификаторОбъекта = "АнализСубконто"
        ИЛИ ИдентификаторОбъекта = "АнализСчета"
        ИЛИ ИдентификаторОбъекта = "ОборотноСальдоваяВедомость"
        ИЛИ ИдентификаторОбъекта = "ОборотноСальдоваяВедомостьПоСчету"
        ИЛИ ИдентификаторОбъекта = "ОборотыМеждуСубконто"
        ИЛИ ИдентификаторОбъекта = "ОборотыСчета"
        ИЛИ ИдентификаторОбъекта = "СводныеПроводки" 
        ИЛИ ИдентификаторОбъекта = "ГлавнаяКнига"
        ИЛИ ИдентификаторОбъекта = "ШахматнаяВедомость";

КонецФункции
```

- Избегайте использование Йода-синтаксиса.
```bsl
// Плохо:
Если 0 = Сумма Тогда

// Хорошо:
Если Сумма = 0 Тогда
```

### Переменные

- Избегайте неявного определения переменных
```bsl
// Плохо
Функция ИдентификаторОбъекта(Объект)
    // Ошибки не будет, даже если переменная не определена в области видимости.
    // В результате будет определена переменная со значением Неопределено.
    ВашаПеременная = ВашаПеременная;
    
    Если Не ЗначениеЗаполнено(ВашаПеременная) Тогда
        ...
    КонецЕсли;
КонецФункции

// Хорошо
Функция ИдентификаторОбъекта(Объект)
    Перем ВашаПеременная;
    ...
КонецФункции
```

### Комментарии
- Если код требует комментария для пояснения работы - в первую очередь необходимо рассмотреть варианты рефакторинга, чтобы код не требовал комментария.
- К комментариям также относятся ограничения на длину строки в 120 символов.

## Обработка ошибок

### Проверка параметров метода
- Проверяйте параметры методов на корректность перед использованием
```bsl
Процедура Рассчитатьпроцент(стКоллекцияСтрок)
    Если ТипЗнч(стКоллекцияСтрок)<>Тип("Структура") ИЛИ стКоллекцияСтрок.Количество()=0
        // обработка ошибки
    КонецЕсли;
    // код метода    
КонецПроцедуры
```
- При обнаружении некорректного параметра инициализируйте его значением по умолчанию или обработайте ошибку
- Инициализируйте параметры методов значениями по умолчанию только в случае полной уверенности корректности этого значения с точки зрения бизнеса
### Использование TRY - CATCH
- Помните, что код заключенный в операторную скобку ```TRY - CATCH``` выполняется медленнее
### Логирование ошибок
- Запись сообщения об ошибке в лог предпочтительнее сообщения пользователю
- Сообщение пользователю об ошибке должно быть ориентировано на пользователя
```bsl
// Плохо
сТекстСообщенияПользователю = "В методе РассчитатьПроцент() параметр стКоллекцияСтрок пуст или не является структурой.";

// Хорошо
сТекстСообщенияПользователю = "При расчете процентов произошла ошибка. Проценты не расчитаны. Продробнее в Журнале регистрации."
```
## Создание, изменение объектов метаданных
- Если составной тип используется многократно, следует использовать объект конфигурации "Определяемый тип". Пример: "Документ резервирования", "Документ партии".