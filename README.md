# Модуль модификации управляемы форм

При доработке типовых конфигураций, для уменьшения измержек на сопровождение конфигурации при ее обновлении, доработка форм должна производиться с максимальным приоритетом программной доработки.

Целью модуля является упрощенное добавление реквизитов формы, добавление их на форму (в том числе и таблиц), так же добавление групп, команд формы и кнопок к ним.

## Установка

Уставновка производится через сравнение/объединения конфигурации с файлом поставки, с установкой на поддержку.

##№ Предварительные требования

Модуль распространяется поставкой. 
Зависимостей не имеет.

### Обновление

Обновление производится через обновление с сохранением конфигурации поставщика
Для проверки корректности совместимистои версий необходимо открыть обработку тестирования обновляемой версии(которая входит в поставку) на версии, на которую будет обновлен модуль.

## Предварительная подготовка

Каждая форма, в которой используется модуль должна быть предварительно подготовлена.
Предварительная подготовка заключается в добавлении вызова одной 

Необходимо добавить вызов процедуры, содержащей код программного добавления в самое начало следующих процедур:
 * ПриСозданииНаСервере()
 * ПриЧтенииНаСервер() - если форма имеет возможность открытия существующего объекта
  
 <details>
  <summary>Пример кода подготовки</summary>
	
 ``` bsl
 &НаСервере
Процедура ПриСозданииНаСервере(Отказ, СтандартнаяОбработка)
	ПрефиксПодготовитьФорму();
	//Текст процедуры	
КонецПроцедуры 
	
&НаСервере
Процедура ПриЧтенииНаСервере(ТекущийОбъект)
	ПрефиксПодготовитьФорму();
	//Текст процедуры	
КонецПроцедуры 	

&НаСервере	
Процедура ПрефиксПодготовитьФорму()
	Если РедакторФорм.ФормаПодготовлена(ЭтаФорма) Тогда
		Возврат;
	КонецЕсли;
	//Код изменения формы
КонецПроцедуры 
```
</details>

## Начало работы

Все вызовы модуля должны производиться из модуля формы при выполнении процедур ПриСозданииНаСервере и ПриЧтенииНаСервер.


## Использование

<details>
 <summary>Вариант заполнение свойств элемента после инициализации контекста.</summary>
	
``` bsl
КонтекстФормы = РедакторФорм.СоздатьКонтекстЭлемента(ЭтотОбъект);	
КонтекстФормы.Свойства.Вставить("Вид", ВидГруппыФормы.ОбычнаяГруппа);
КонтекстФормы.Свойства.Вставить("Группировка", ГруппировкаПодчиненныхЭлементовФормы.ГоризонтальнаяЕслиВозможно);
КонтекстФормы.Свойства.Вставить("ОтображатьЗаголовок", Ложь);
ЭлементГруппаШапка = РедакторФорм.ДобавитьГруппуНаФорму(КонтекстФормы, "ГруппаШапка"); 
```
</details>

<details>
 <summary>Вариант определение свойств до создания контекста.</summary>
	
``` bsl
Свойства = Новый Структура("Вид, ОтображатьЗаголовок", ВидГруппыФормы.ОбычнаяГруппа, Ложь);
КонтекстФормы = РедакторФорм.СоздатьКонтекстЭлемента(ЭтотОбъект, , , Свойства);	
ЭлементГруппаШапка = РедакторФорм.ДобавитьГруппуНаФорму(КонтекстФормы, "ГруппаШапка"); 
```
</details>

## Запуск тестов

Тесты запускаются через vanessa runner: файл run_vanessa.bat.

## Authors

See the list of [contributors](https://github.com/huxuxuya/FormModificator/contributors) who participated in this project.

