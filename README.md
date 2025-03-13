# Проект: Построения рекомендаций  Popularity-based model в случае холодного старта пользователя.


## Оглавение
[1. Описание проекта](https://github.com/AMK01001/Recommender-Systems.-Part-I?tab=readme-ov-file#%D0%BE%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0)

[2. Какой кейс решаем?](https://github.com/AMK01001/Recommender-Systems.-Part-I?tab=readme-ov-file#%D0%BA%D0%B0%D0%BA%D0%BE%D0%B9-%D0%BA%D0%B5%D0%B9%D1%81-%D1%80%D0%B5%D1%88%D0%B0%D0%B5%D0%BC)

[3. Результаты](https://github.com/AMK01001/Recommender-Systems.-Part-I?tab=readme-ov-file#%D1%80%D0%B5%D0%B7%D1%83%D0%BB%D1%8C%D1%82%D0%B0%D1%82%D1%8B)

## Описание проекта 
DeskDrop — платформы для внутренних коммуникаций, разработанной CI&T и ориентированной на компании, использующие Google Workspace (Google G Suite). Среди прочего, эта платформа позволяет сотрудникам компаний делиться актуальными статьями со своими коллегами.

В датасете содержится около 73 тысяч записей о взаимодействии пользователей с более чем тремя тысячами публичных статей, размещённых на платформе.
:arrow up:[к оглавлению](https://github.com/AMK01001/Recommender-Systems.-Part-I?tab=readme-ov-file#%D0%BE%D0%B3%D0%BB%D0%B0%D0%B2%D0%B5%D0%BD%D0%B8%D0%B5)

## Какой кейс решаем?

### *ИССЛЕДОВАНИЕ ДАННЫХ*

Информация в наборе данных:
- Оригинальный URL, название и текст статьи.
- Контекст посещений пользователей, например дата/время, клиент (мобильное приложение/браузер) и геолокация.
- Различные типы взаимодействия, что позволяет сделать вывод об уровне заинтересованности пользователя в статьях, например комментарии → лайки → просмотры.

Данные включают в себя два файла:
- shared_articles.csv;
- users_interactions.csv.

Начнём работать с файлом shared_articles.csv. Он содержит информацию о статьях, опубликованных на платформе DeskDrop.

Для каждой статьи есть:
- дата публикации (временная метка),
- исходный URL-адрес,
- заголовок,
- содержание в виде обычного текста,
- язык статьи (португальский — pt или английский — en),
- информация о пользователе, который поделился статьёй (автор).

Для временной метки существует два возможных типа событий:
- CONTENT SHARED — статья была опубликована на платформе и доступна для пользователей;
- CONTENT REMOVED — статья была удалена с платформы и недоступна для дальнейших рекомендаций.

Для простоты мы рассматриваем здесь только тип события CONTENT SHARED.


**КРИТЕРИИ ОЦЕНИВАНИЯ**:

- Отфильтрирование данные так, чтобы остались только объекты с типом события CONTENT SHARED. Сколько таких объектов в получившейся таблице?
- Создание признак, который будет отражать числовой вес для взаимодействия со статьёй (в соответствии с приведёнными выше весами). Вычисление среднее значение для полученного признака. Округлите его до двух знаков после точки-разделителя.
- Чтобы получить хоть какую-то информацию, на которую можно будет опираться, оставь только тех пользователей, которые взаимодействовали хотя бы с пятью статьями. Сколько всего таких пользователей?
- Оставим только те взаимодействия, которые касаются только отфильтрованных пользователей (то есть тех, которые взаимодействовали как минимум с пятью статьями). Сколько всего таких взаимодействий?
- Разделим данные на обучающую и тестовую выборки, выбрав в качестве временной отсечки значение 1475519545. Сколько объектов попало в обучающую выборку?
- Посчитать популярность каждой статьи как сумму всех логарифмических «оценок» взаимодействий с ней (используя только обучающую выборку). Выберем ID самой популярной статьи:
- Постройть систему рекомендаций. Оценить качество с помощью precision@10 для каждого пользователя (доля угаданных рекомендаций). После этого усреднем результат по всем пользователям.


**Требования к оформлению ноутбука-решения**

- Оформите решение в Jupyter Notebook. После выполнения задания не забудьте сохранить результат в корректном формате .IPYNB.
- Возьмите за основу ноутбук-шаблон: не следует менять последовательность действий и уже заполненные ячейки (если прямо не указано иного). Вам необходимо только дополнить 
предложенный файл.
- Выполняйте каждое задание в отдельной ячейке, выделенной под него (в шаблоне они помечены как «ваш код здесь»). Не создавайте множество дополнительных ячеек — они делают 
ноутбук перегруженным и трудночитаемым.
- В решении должен быть использован только уже пройденный материал, кроме тех случаев, когда на использование дополнительного материала будет указано отдельно. 
Также в кейсе вам будет предложено творческое задание (доработка модели с использованием дополнительных инструментов). В нём вы сможете использовать любой доступный материал. 
Это будет указано в задании явным образом.
- Код должен быть читабельным и понятным: имена переменных и функций должны отражать их сущность, приветствуется отсутствие многострочных конструкций и условий. 
Любую задачу можно решить множеством вариантов: постарайтесь найти самый красивый и лаконичный. 
- Оформите код по стандартам PEP-8. Вы можете освежить в памяти требования стандарта в соответствующем руководстве. Также вы можете воспользоваться одним из онлайн-ресурсов, 
который проверяет код на соответствие стандартам (однако он зачастую бывает слишком строг).
- Все визуализации необходимо выполнять в соответствии с требованиями, которые вы изучали ранее. Все диаграммы и графики должны иметь содержательные названия и подписи осей.
 Помните, что любой человек должен без труда и дополнительных вопросов понять, что изображено на визуализации только по имеющейся на ней информации.
- Оформите выводы к графикам в формате Markdown под самим графиком в отдельной ячейке (в шаблоне они помечены как «ваши выводы здесь»). Если вы хотите красиво оформить 
текстовые вставки, можно воспользоваться следующим ресурсом.

**Что практикуем**
работу с данными и оформление отчетов с помощью средств python

## Результаты
Ноутбук с выполненными заданиями и выводами(https://github.com/AMK01001/Recommender-Systems.-Part-I/blob/main/Recommender%20Systems.%20Part%20.ipynb)

:arrow up:[к оглавлению](https://github.com/AMK01001/Recommender-Systems.-Part-I?tab=readme-ov-file#%D0%BE%D0%B3%D0%BB%D0%B0%D0%B2%D0%B5%D0%BD%D0%B8%D0%B5)
