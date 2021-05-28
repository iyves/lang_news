
_Слайды:_ https://docs.google.com/presentation/d/1tXr1Q1briB4v8z3TLkRxVDyND7uACYrHoFy8nfsYI8E/edit?usp=sharing

__Слайд 1__
Несколько месяцев назад я столкнулся трудностями, когда описывал русскоязычным коллегам события, произошедшие 6-го января в Капитолии. Помню разговор с репетитором за несколько дней до происшествий. В это время называли собрания массы людей, выступающие против инаугурации нового президента, протестом. Тем не менее, на протяжении 6-го января название постепенно изменилось. То, что было “митингом” или “протестом”, превратилось в “нападение, бунт, мятеж, внутренний терроризм или даже государственный переворот” [1]. 

__Слайд 2__
Интересно, какими словами разные новостные агентства называли события. Кажется, что названия зависят от политической пристрастности агентства. Если взять Associated Press как нейтральный источник [2], видим наличие темы “capitol siege (осада Капитолия)” [3]. 

__Слайд 3__
Fox News является правой новостной организацией, которая предпочитает термин 
“сapitol protest (протест в Капитолии)” [4] [5]. 

__Слайд 4 & 5__
Наоборот, левоцентристская организация NPR и левая организация CNN используют слова “capitol insurrection (мятеж в Капитолии)” и “capitol riot (бунт в Капитолии)” [6-9].

__Слайд 6__
Меня заинтриговало влияние языка СМИ в проявлении одного или другого политического взгляда на события. Для этого проекта я, будучи исследователем искусственного интеллекта, задал себе вопрос: Может ли машинное обучение обнаружить предвзятость средств массовой информации?

__Слайд 7__
Через интернет я нашёл программу, разработанную программистом со схожим интересом [10]. Допустим у нас огромная база данных, включающая статьи, которые ежедневно публикуют разные новостные агентства. Общий подход, чтобы обнаружить предвзятость каждого из агентств, имеет два этапа: кластеринг и сентимент-анализ. Первый этап состоит из обнаружения латентных тем в статьях для определенного дня или промежутка дней. К примеру ожидаем следующие темы для статей, опубликованных 6-ого января: “коронавирус”, “осада Капитолия”, “новый год”. 

__Слайд 8__
Второй этап включает в себя оценивание насколько позитивным, негативным или нейтральным является подача новостей, каков язык каждой статьи. Статья, в которой используется “протест в Капитолии”, может получить нейтральную оценку, а для использования “бунт в Капитолии” -- негативную оценку. В результате можем выбрать определённую тему и смотреть, как разные новостные организации описывают данную тему. Также можем узнать, насколько негативно, позитивно или нейтрально даны статьи в среднем.

__Слайд 9__
Мой проект соблюдает вышеупомянутый процесс. Анализирую данные из датасет Kaggle “Russian News 2020” [11]. В нём 21670 статьей из 4 новостных агентств: lenta.ru, ria.ru, meduza.io и tjournal.ru. Lenta.ru -- традиционный источник новостей, которым владеет Rambler Media Group. Ria.ru --  государственное новостное агенство. Meduza.io -- несколько оппозиционное агенство, основанное в 2014 бывшим редактором lenta.ru после его увольнения. tjournal -- более современная новостная организация, фокусирующая внимание на новостях и трендах интернета.

__Слайд 10__
После загрузки данных надо очистить и с обработать их для первого этапа, то есть для кластеринга. Сначала стандартизируется формат дат публикации, потом из текста удаляются пустые пространства, заголовки и сноски. Затем проводим лемматизацию текста и удаляем частотные стоп-слова. Выбираем все статьи за первое, десятое и двадцатое числа каждого месяца. Проводим кластеринг с 22 кластерами, что переводится как 22 темы, обсуждаемые четырьмя новостными организациями. Для каждого кластера сохраняем 10 ключевых слов, которые определяют кластер. 

Потом проводим сентимент-анализ. Используем модель, предварительно обученную blanchefort на четырёх датасетах из твитов, обзоров товаров, постов в соцсетях и отзывов о медицинских учреждениях [12]. Получаем оценку тональности для заголовка и текста каждой статьи. Негативная тональность определяется “-1”, позитивная -- “1”, нейтральная же “0”. Загружаем результаты в Power BI, чтобы анализировать их дальше.

__Слайд 11__
Вот результаты моего проекта. Видим ежемесячное распределение статьей для 2020. Большинство статей из ria.ru, что повлияет на кластеринг и среднюю оценку тональности. Неизвестно, почему объём статей резко снижается с сентября по декабрь. В это время статей из lenta.ru and tjournal.ru почти совсем нет, и объём статей ria.ru уменьшается на две трети. 

__Слайд 12__
Вот результаты кластеринга. Опираясь на 10 ключевых слов, придумываем название для каждого кластера. Получаем следующее распределение тем. Согласно нашему алгоритму кластеринга, топовые темы 2020 относятся к Трампу, Путину, убийству Касима Сулеймана. Следует отметить, если бы я объединил темы “вакцина” и “ковид”, тогда ковид занял бы 4-ое место. 

__Слад 13__
Что касается сентимент-анализа, обнаруживаем, что, в основном, заголовок и текст статей оба довольно негативны. По данным модели средняя тональность заголовков более нейтральна, чем тексты. Заголовки meduza.io горазно негативнее средней тоальности, но текст граздо нейтральнее. Наоборот, tjournal.ru имеет в основном нейтральные заголовки, а тексты гораздо негативнее. 

__Слайд 14__
Самые нейтральные кластеры -- “золотой глобус”, “футбол -- премьер лига” и “погода”, а самые негативные кластеры -- “ковид”, “трамп” и “бывший глава Nissan”. 

__Слайд 15__
Если посмотрим на некоторые кластеры, то видим, как четыре новостных агентства описывают ковид, Трампа и Путина. Все источники очень негативно описывают ковид. Более того, все агентства негативно описывают Трампа и Путина, однако эта тональность не ясна только из заголовков. Неожиданно, meduza.io найболее нейтрально описывает Трампа и Путина.

__Слайд 16__
В итоге, этот проект показывает некоторые неожиданные моменты русскоязычных СМИ. Хотя я ожидал, что тональность заголовков была бы гораздо негативнее, чем тексты, из-за сенсации и клик-бейта, наши данные показывает наоборот. Более того, я неправильно думал, что meduza.io и ria.ru имели бы самую большую предвзятость из личного наблюдения, но они уступали место tjournal.ru.

В будущем можно улучшить качество результатов этого проекта, используя самые новые модели машинного обучения для кластеринга и сентимент-анализа. Более того, надо выяснить причину резкого снижения объёма статей в сентябре. Было бы интересно сравнивать данные статей из разных стран и по разным языкам.

[1]    https://apnews.com/article/donald-trump-capitol-siege-riots-media-8000ce7db2b176c1be386d945be5fd6a

[2]    https://mediabiasfactcheck.com/associated-press/ 

[3]    https://apnews.com/hub/capitol-siege

[4]    https://mediabiasfactcheck.com/fox-news/ 

[5]    https://www.foxnews.com/category/us/capitol-protests

[6]    https://mediabiasfactcheck.com/cnn 

[7]    https://www.cnn.com/2021/03/12/politics/us-capitol-riot-investigation-plea-deal/index.html

[8]    https://mediabiasfactcheck.com/npr/ 

[9]    https://www.npr.org/sections/insurrection-at-the-capitol

[10]    https://towardsdatascience.com/machine-learning-versus-the-news-3b5b479d8e6a 

[11]    https://www.kaggle.com/vfomenko/russian-news-2020 

[12]    https://huggingface.co/blanchefort/rubert-base-cased-sentiment
