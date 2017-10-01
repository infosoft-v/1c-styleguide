# 1С: Руководство по стилю оформления

> Почти все убеждены, что любой стиль кроме их собственного ужасен и нечитаем. Уберите отсюда "кроме их собственного" — и они будут, наверное, правы... 
> 
> -- Джерри Коффин (Jerry Coffin) об отступах

## Соглашение о наименовании

- Используйте CAPS LOCK для обозначения переменных, которые будут выполнять роль констант. 
```bsl
СТАТУС_ОТПРАВКИ_OK  = 1;
СТАТУС_ОТПРАВКИ_ERR = 2;
``` 

- Используйте [венгерскую](https://ru.wikipedia.org/wiki/%D0%92%D0%B5%D0%BD%D0%B3%D0%B5%D1%80%D1%81%D0%BA%D0%B0%D1%8F_%D0%BD%D0%BE%D1%82%D0%B0%D1%86%D0%B8%D1%8F "wikipedia") нотацию в именах переменных.

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

- Ключи или поля коллекций рекомендуется именовать используя венгерскую нотацию.
```bsl
стАдресУчастника = Новый Структура("чРегионКод, сИндекс, сГород, сУлица");
```

- Переменные, в которых хранится элемент коллекции, допустимо начинать с префикса `элемент` или `строка`.
```bsl
Для каждого элементМассива Из мУчастникиСделки Цикл
    // код цикла
КонецЦикла;
```

- Для глобальных переменных модуля используйте префикс `м_`.
```bsl
Перем м_рефCOMобъект;
```

- Используйте стиль [CamelCase](https://ru.wikipedia.org/wiki/CamelCase) при именовании переменных и методов.
```bsl
Перем бВыполненоБезОшибок = Истина;
```

- В наименованиях переменных и методов допустимы суффиксы, указанные через `_`.
```bsl
Процедура УдалитьВременныеФайлы_УдСервер()
    // код метода
КонецПроцедуры
```

- Не используйте отрицание в именах переменных и методов.
```bsl
// Плохо:
Функция ПроверкаНеПройдена()
    Перем бНеУспешно;

    // код метода
    Возврат бНеУспешно;
КонецФункции    

// Хорошо:
Функция ПроверкаПройдена()
    Перем бУспешно;

    // код метода
    Возврат бУспешно;
КонецФункции    
```

## Оформление модулей

- Длина строки в общем случае не должна превышать 120 символов.
- Для отступов необходимо использовать символы **табуляции**.

- Одна строка кода - одна управляющая конструкция.
```bsl
// Плохо:
Если бЭтоБрак Тогда Продолжить; КонецЕсли;

// Хорошо:
Если бЭтоБрак Тогда
  Продолжить;
КонецЕсли;
```

- Следует отделять друг от друга пробелами ключевые слова, операторы, вызовы процедур и функций, параметры процедур и функций.
```bsl
// Плохо:
Сообщить(“Сумма: “+чСумма);

// Хорошо:
Сообщить(“Сумма: “ + чСумма);
```

- Для разделения кода на логические части внутри модуля следует использовать пустые строки.

- При определении или вызове функции с несколькими параметрами при переносе строк необходимо выравнивать параметры по ближайшему отступу.
```bsl
// Начальное состояние (строка слишком длинная):
НалоговыйУчет.ОстаткиВременныхРазниц(сВидАктиваОбязательства, мОрганизации, Реквизиты.дНачалоГода, Реквизиты.дКонДата);

// Хорошо:
НалоговыйУчет.ОстаткиВременныхРазниц(
    сВидАктиваОбязательства,
    мОрганизации,
    Реквизиты.дНачалоГода,
    Реквизиты.дКонДата);
```

- При следовании друг за другом нескольких однотипных операторов допускается их выравнивание. Выравнивание следует выполнять с помощью **пробелов**.
```bsl
// Хорошо:
НоваяСтрока = ВидыОпераций.Добавить();
НоваяСтрока.ВидОперации         = ВидОперации;
НоваяСтрока.НомерГруппы         = ГруппаПоВидуОперации(ВидОперации);
НоваяСтрока.ПоОрганизацииВЦелом = ГруппаПоОрганизации(НоваяСтрок);
```

### Методы (процедуры и функции)

- Метод должен иметь описание созданное с помощью команды "Создать описание процедуры" (щелчек правой кнопкой мыши на наименовании метода - Рефакторинг - Создать описание процедуры).

- Допустимо в имени метода использовать слова `Получить` (`Get`), `Установить` (`Set`).

- Допустимо, если параметр метода возвращает значение.
- Описание метода должно содержать указание вида параметра. `IN` для входящих, `OUT` для исходящих.
```bsl
//  Функция - Получить адрес участника как структура
//
//  Параметры:
//      рефКонтрагент - СправочникСсылка - IN. Ссылка на контрагента
//      стАдресУчастника - Структура - OUT. Адрес участника. Структура с ключами:
//          * чРегионКод - Число
//          * сИндекс - Строка
//          * сГород - Строка
//
//  Возвращаемое значение:
//      Булево - признак успешного выполнения
Функция ПолучитьАдресУчастника(рефКонтрагент, стАдресУчастника)
    Перем бВыполненоБезОшибок;

    // код метода
    Возврат бВыполненоБезОшибок;
КонецФункции
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
- Сложные условия (более трех конструкций) требуют рефакторинга.

### Переменные

- Явное определение переменных это хорошо.
```bsl
Функция УстановитьПризнакОнЛайн()
    Перем бВыполненоБезОшибок;
    
    // код метода
    Возврат бВыполненоБезОшибок;
КонецФункции
```

### Комментарии
- Если код требует комментария для пояснения работы - в первую очередь необходимо рассмотреть варианты рефакторинга, чтобы код не требовал комментария.
- К комментариям также относятся ограничения на длину строки в 120 символов.

## Обработка ошибок

### Проверка параметров метода
- Проверяйте параметры методов перед их использованием. Для некорректных параметров обработайте ошибку.
```bsl
Процедура РассчитатьПроцент(стКоллекцияСтрок)
    Если ТипЗнч(стКоллекцияСтрок)<>Тип("Структура") ИЛИ стКоллекцияСтрок.Количество()=0 Тогда
        // обработка ошибки
    КонецЕсли;
    // код метода    
КонецПроцедуры
```
- Инициализация некоректного параметра значением по умолчанием не всегда хорошая идеея. Это допустимо только в случае полной уверенности корректности этого значения с точки зрения бизнеса.
```bsl
// плохо:
Функция СтавкаНДСКакЧисло(сНДС)
    Перем чНДС;
    
    Если ТипЗнч(сНДС) <> Тип("Строка") ИЛИ ПустаяСтрока(сНДС) Тогда
        сНДС = "18%";    
    КонецЕсли;
    // код метода
    Возврат чНДС;
КонецФункции;

// хорошо:
Функция СтавкаНДСКакЧисло(сНДС)
    Перем чНДС;
    
    Если ТипЗнч(сНДС) <> Тип("Строка") ИЛИ ПустаяСтрока(сНДС) Тогда
        // обработка ошибки    
    КонецЕсли;
    // код метода
    Возврат чНДС;
КонецФункции;
```

### Использование TRY - CATCH
- Помните, что код заключенный в операторную скобку `Попытка - Исключение` (`TRY - CATCH`) выполняется медленнее
### Логирование ошибок
- Запись сообщения об ошибке в лог предпочтительнее сообщения пользователю
- Сообщение пользователю об ошибке должно быть ориентировано на пользователя
```bsl
// Плохо
сТекстСообщенияПользователю = "В методе РассчитатьПроцент() параметр стКоллекцияСтрок пуст или не является структурой.";

// Хорошо
сТекстСообщенияПользователю = "При расчете процентов произошла ошибка. Проценты не расчитаны. Продробнее см. Журнал регистрации."
```
## Создание, изменение объектов метаданных
- Если составной тип используется многократно, следует использовать объект конфигурации "Определяемый тип". Пример: "Документ резервирования", "Документ партии".