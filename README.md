# Instagram
## Основная часть
## 1. Тема и целевая аудитория

**Instagram** - американская социальная сеть для обмена фотографиями и видео.
### Функционал MVP
1. Регистрация и авторизация пользователей
2. Возможность загрузки фотографий, а также применения к ним фильтров
3. Комментирование фотографий другими пользователями
4. Возможность оценки фотографий (лайки)
5. Поиск авторов/пользователей
6. Возможность сохранять понравившиеся посты
7. Лента с постами от подписанных пользователей
8. Подписки на пользователей

### Целевая аудитория

Метрики трафика и вовлеченности
1. MAU - **2B** [^3]
2. DAU - **500M** (по статистике за 2017 год) [^4]
3. Среднее время использования приложения в день - **34 минуты** [^4]
4. Каждый день на платформу загружается **100M** фотографий [^2]
5. Средняя вовлеченность для постов в Instagram - **0.71%** [^1]

### Распределение аудитории по странам [^9]
[![Распределение аудитории по странам](diagrams/ig-country-users-distribution.png)](https://www.statista.com/statistics/578364/countries-with-most-instagram-users/)

### Средний возраст аудитории [^1]
[![Средний возраст аудитории](diagrams/age-distribution.png)](https://datareportal.com/essential-instagram-stats)



## 2. Расчет нагрузки
### Предположения
Предположим, что средний пользователь Instagram видит примерно **150** постов в день, при нахождении в приложении 34 минуты [^4].

В таком случае, при вовлеченности для одного поста в **0.71%** [^1] мы можем посчитать, что в среднем пользователь взаимодействует с **1.07** постом за день.

Также, используя данные об усредненной статистике поста по окончании года, мы можем увидеть значения количества лайков, комментариев и сохранений[^6]:

| Лайки  | Комментарии | Сохранения |
|--------|-------------|------------|
| 513.37 | 15.66       | 19.79      |


Тогда, при MAU в **500M** человек, каждый день оставляется примерно **467.8M** лайков, **14.25M** комментариев, а также **18M** сохранений постов.

На основе абсолютных качений, рассчитаем отношение лайков к остальным показателям:

- Отношение лайков к комментариям - 33:1

- Отношение лайков к сохранениям - 26:1

### Расчеты

Из расчета, что Instagram приводит большинство фотографий к разрешению **1080p x 1080p** [^7], а также сжимает их в целях сохранения места получаем размер одной фотографии примерно в **500KB** [^8].
Тогда, при **100M** загруженных фотографий в день, общий размер хранилища составляет **50TB** в день или **100KB** на пользователя.

Пусть средняя длина комментария - **60** символов, тогда в кодировке UTF-8 (для поддержки большинства языков и emoji) они занимают **0.24KB**. Тогда, при среднем дневном количестве комментариев в **14.25M**,
всего нужно около **3.42GB** в день, или же **0.035KB** на пользователя в день.

Примем, что **1%** пользователей входят на сервис каждый день.

Из роста **MAU** с 1B до 2B с 2018 по 2022 год, мы можем рассчитать среднее количество регистраций в **700K** в день[^4].

Около **18%** постов в Instagram используют встроенный фильтр [^14], тогда примерно **1.8M** из **100M** фотографий каждый день загружается с фильтром.

### Действия пользователей

Используя данные по усредненной статистике поста, а также о взаимодействии с постами, можем рассчитать дневные действия пользователя:

| Действие пользователя            | Количество в день |
|----------------------------------|-------------------|
| Просмотр постов                  | 150               |
| Использование поиска             | 1(*)              |
| Загрузка фотографии              | 0.2               |
| Комментирование поста            | 0.03              |
| Отметка "нравится" для поста     | 0.94              |
| Сохранение поста в "избранное"   | 0.04              |
| Подписка на другого пользователя | 0.15(**)          |
| Вход                             | 0.01              |
| Регистрация                      | 0.0014            |
| Использование фильтров           | 0.036             |

(*) Приблизительно, на основе данных использования страницы **Explore**[^11].

(**) Приблизительно, на основе технического ограничения на дневное количество подписок[^12].


### Продуктовые метрики

| Метрика                                                        | Значение                                  | 
|----------------------------------------------------------------|-------------------------------------------|
| MAU                                                            | **2B** [^3]                               |
| DAU                                                            | **500M** (по статистике за 2017 год) [^4] |
| Среднее время использования приложения в день                  | **34 минуты** [^4]                        |
| Каждый день на платформу загружается                           | **>100M** фотографий [^2]                 |
| Посещений instagram.com                                        | **7.24B** [^5]                            |
| Средний размер хранилища для фотографий на пользователя в день | **100KB**                                 |
| Средний размер комментария на пользователя в день              | **0.035KB**                               |
| Среднее количество фотографий на пользователя в день           | **0.2шт**                                 |
| Среднее количество комментариев на пользователя в день         | **0.03шт**                                |

### Технические метрики

#### Хранилища

| Тип хранилища | Размер в день | Размер в месяц |
|---------------|---------------|----------------|
| Фотографии    | **50TB**      | **1.5PB**      |
| Комментарии   | **3.42GB**    | **1TB**        |

#### Сетевой трафик

На каждую фотографию кидается запрос на сервер. При примерном количестве постов, которые видит один человек за день в **150**, он в среднем делает 150 запросов.
Тогда, при DAU в **500M**, каждый день происходит **75B** запросов, или же **3.125B** в час, **52M** в минуту, **868K** в секунду.

Предположим, что к каждому **10-му посту** пользователь прочитает комментарии, и к одному его оставит, либо поставит лайк. При общем количестве этих действий в **15** запросов 
(один запрос на комментарий + **14** на просмотр, так как для нескольких постов пользователь пролистает их вниз, в связи с чем произойдет еще несколько запросов для загрузки 
последующих комментариев),
при DAU в **500M** можем рассчитать дополнительное количество запросов в **7.5B** в день, **87K** в секунду.

Также предположим, что один запрос на получение комментариев возвращает батч на **5 штук**, общим весом в **1KB**.

Из среднего количества загруженных фотографий в день получаем, что в день **100M** запросов на загрузку, **1.2K** в секунду.

Предположим, что при поиске выдается **JSON** с несколькими результатами выдачи, общим размером **1KB**. Также предположим, что при подписке, а так же сохранении поста происходит запрос с **JSON** размером **20B**[^13]. 

Все фильтры для постов в Instagram работают локально на устройстве и не потребляют сетевой трафик[^14].

Предположим, что для регистрации и авторизации используются **JSON** с размерами **40B** и **20B**, соответственно.

| Тип                           | Средний RPS | Пиковый RPS(*) | Сетевой трафик (средний) | Сетевой трафик (пиковый) |
|-------------------------------|-------------|----------------|--------------------------|--------------------------|
| Просмотр поста                | 868K        | 1.7M           | 3.4Тбит/с                | 6.8Тбит/с                |
| Загрузка поста                | 1.2K        | 2.4K           | 4.8Гбит/s                | 9.6Гбит/s                |
| Открытие секции комментариев  | 81K         | 162K           | 650Mбит/с                | 1.2Гбит/с                |
| Оставление комментария        | 0.8K        | 1.6K           | 2Мбит/с                  | 4Мбит/с                  |
| Оставление отметки "Нравится" | 5.4K        | 10.8K          | 22Кбит/c                 | 44Кбит/с                 |
| Использование поиска          | 5.7K        | 11.4K          | 45.6Мбит/с               | 91.2Мбит/с               |
| Подписка на пользователя      | 1K          | 2K             | 160Кбит/с                | 320Кбит/с                |
| Сохранение поста              | 1K          | 2K             | 160Кбит/с                | 320Кбит/с                |
| Авторизация                   | 60          | 120            | 10Кбит/с                 | 20Кбит/с                 |
| Регистрация                   | 8           | 16             | 5Кбит/с                  | 10Кбит/с                 |
| Итого                         | 964K        | 1.9M           | 3.41 ТБит/с              | 6.82ТБит/с               |


(*) Считаем, что пиковый RPS в 2 раза больше среднего.

## 3. Расчет нагрузки

### Разбиение по доменам

Instagram использует один домен для основных страниц - **instagram.com**, а также некоторые дополнительные, для различных вспомогательных страниц, не рассматриваемых в **MVP** (например, [**help.instagram.com**](https://help.instagram.com)).

### Расположение датацентров

Исходя из данных о странах с самым большим количеством пользователей можем рассчитать следующее расположение датацентров:

1. Азия
   - Индия
     - Мумбаи - Будучи одним из самых населенных городов в Индии, находится рядом с Аравийским морем, что позволит обслуживать не только пользователей из Индии, а также из других ближневосточных стран из-за большого количества оптоволоконных кабелей, подведенных к городу[^10].
     - Нью-Дели - Столица Индии, размещение датацентра здесь позволит обслужить весь северо-восток страны, а также предоставит альтернативный маршрут доставки контента в другие ближневосточные и азиатские страны.
    - Сингапур
      - Сингапур - Датацентр в Сингапуре позволит обслужить оставшуюся часть Азии, также являющуюся большой долей пользователей сервиса, в частности Малайзию и Филипины. Здесь находится настоящий датацентр Meta.
    - Япония
      - Токио - Снизит нагрузку на датацентр в Сингапуре, покроет восточноазиатский регион.
    - Тайланд
      - Бангкок - Снизит нагрузку на Азиатский регион.
2. Европа
    - Германия
      - Франкфурт - Находясь в самом центре Европы, датацентр здесь способен обеспечить минимальные задержки до большинства стран Еврозоны.
    - Венгрия
      - Будапешт - Обслуживание восточной части Европы, город обладает развитой сетевой инфраструктурой. 
3. Ближний восток
   - Турция
     - Стамбул - Датацентр снизит нагрузку на индийские дц, а также поможет принять часть нагрузки при аварии. 
4. Южная Америка
   - Бразилия 
     - Сан-Паулу - Самый населенный город всего континента, размещение датацентра здесь позволит обслужить всю западную часть континента.
   - Перу
     - Лима - Работа с восточной частью континента.
5. Северная Америка
    - США
      - Техас - Хьюстон, датацентр ориентирован на работу с Мексикой и южно-восточной части США.
      - Юта - Солт-Лейк-Сити, город обладает большим количеством магистральных линий связи[^15], позволяющих эффективно работать с Канадой и северо-западной частью США.

Исходя из этих данных, можем построить карту датацентров:
![Карта Датацентров](diagrams/dc-map.png)

### Разбиение сетевого трафика по датацентрам
| Датацентр      | Процент от общей нагрузки (*) | Средний RPS | Пиковый RPS | Сетевой трафик (средний) | Сетевой трафик (максимальный) |
|----------------|-------------------------------|-------------|-------------|--------------------------|-------------------------------|
| Мумбаи         | 8%                            | 77K         | 154K        | 272Гбит/c                | 544Гбит/с                     |
| Нью-Дели       | 8%                            | 77K         | 154K        | 272Гбит/c                | 544Гбит/с                     |
| Калькутта      | 8%                            | 77K         | 154K        | 272Гбит/c                | 544Гбит/с                     |
| Сингапур       | 8%                            | 77K         | 154K        | 272Гбит/c                | 544Гбит/с                     |
| Бангкок        | 8%                            | 77K         | 154K        | 272Гбит/c                | 544Гбит/с                     |
| Токио          | 7%                            | 67K         | 134K        | 238Гбит/с                | 476Гбит/с                     |
| Франкфурт      | 7%                            | 67K         | 134K        | 238Гбит/с                | 476Гбит/с                     |
| Стамбул        | 7%                            | 67K         | 134K        | 238Гбит/с                | 476Гбит/с                     |
| Будапешт       | 7%                            | 67K         | 134K        | 238Гбит/с                | 476Гбит/с                     |
| Сан-Паулу      | 7%                            | 67K         | 134K        | 238Гбит/с                | 476Гбит/с                     |
| Лима           | 7%                            | 67K         | 134K        | 238Гбит/с                | 476Гбит/с                     |
| Хьюстон        | 8%                            | 77K         | 154K        | 272Гбит/c                | 544Гбит/с                     |
| Солт-Лейк-Сити | 8%                            | 77K         | 154K        | 272Гбит/c                | 544Гбит/с                     |


(*) Процент нагрузки рассчитывается по MAU.

Расположение датацентров выбиралось исходя из [распределения аудитории по странам](#распределение-аудитории-по-странам-5), наземной сетевой инфраструктуры[^15], а также карты оптоволоконных кабелей. ![Карта оптоволоконных кабелей](diagrams/submarine-cable-map.png)

### Используемые технологии
* Для DNS балансировки будет использоваться Geo-based DNS, так как у нас есть несколько датацентров, расположенных в разных частях мира.

* Для балансировки внутри континента, будет использован AnyCast BGP, позволяющий получить доступ к контенту с минимальными задержками. Регионы использования - Индия, а также США.

## 4. Локальная балансировка нагрузки

### Схема балансировки нагрузки
После глобальной балансировки нагрузки, пакет будет прилетать в датацентр, где его будет встречать сначала L4 балансировщик, а затем L7 балансировщик.

### L4 балансировка
Будет использоваться несколько серверов, объединенных VRRP и работающих по схеме active-passive, при выходе из строя одного сервера, активным становится следующий с наивысшим приоритетом.
Далее используя алгоритм round-roubin для выбора L7 балансировщика.

### L7 балансировка
Пиковый RPS одного датацентра составляет ~160k RPS. Принимая во внимание, что в максимальная нагрузка на Nginx с SSL терминацией 
составляет примерно **50К-80К** RPS [^16], то оценим ее среднее значение на примерно на **30K** RPS. Тогда для того, чтобы держать пиковую нагрузку, 
нам необходимо примерно 6 экземпляров Nginx, однако необходимо оставить запас на случай возможного выхода из строя нескольких экземпляров и увеличить итоговое количество до 8 штук.

Также Nginx занимается SSL терминацией, расшифровывая https пакет и превращая его в http.

### Kubernetes
Для работы сервиса используется несколько kubernetes кластеров, трафик на которые перенаправляется в соответствии с типом запроса. Например, запросы на получение поста
с помощью Kubernetes Service и CoreDNS перенаправляются в определенную группу Pod-ов (ClusterIP), где развернут (микро) сервис, работающий с постами.

Далее, когда пакет приходит на ноду k8s, kube-proxy с помощью алгоритма (например, weighed round-robin) выбирает какой pod будет обрабатывать конкретный запрос.

Межсервисное взаимодействие происходит похожим образом, запрос из сервиса резолвится с помощью CoreDNS, далее kube-proxy на втором сервисе выбирает один из своих pod и т.д.

### Масштабируемость и надежность
Для масштабируемости используем K8s HPA - механизм, позволяющий автоматически увеличивать количество Pod-ов при возрастающей нагрузке.
Для безопасности используются healthchecks, например L4 балансировщик сам проверяет доступность Nginx-ов с помощью каких-то сервисных запросов.
Kubernetes сам следит за состоянием pod-ов и при надобности перезапускает их, или исключает из списка доступных.

## Список использованных источников
[^1]: [Instagram users, stats, data & trends](https://datareportal.com/essential-instagram-stats)

[^2]: [Photo Statistics](https://www.linkedin.com/pulse/impact-instagram-50-statistics-you-should-know-2024-szhue#:~:text=Over%20100%20million%20photos%20and%20videos%20are%20uploaded%20to%20Instagram%20daily.)

[^3]: [Most popular social networks worldwide as of April 2024, by MAU](https://www.statista.com/statistics/272014/global-social-networks-ranked-by-number-of-users/)

[^4]: [BackLinko](https://backlinko.com/instagram-users)

[^5]: [semrush.com](https://www.semrush.com/website/instagram.com/overview/)

[^6]: [Instagram statistics](https://onlysocial.io/important-instagram-statistics/)

[^7]: [Instagram image resolution](https://help.instagram.com/1631821640426723)

[^8]: [Image size calculator](https://toolstud.io/photo/filesize.php?imagewidth=1080&imageheight=1080)

[^9]: [Country-based users distribution](https://www.statista.com/statistics/578364/countries-with-most-instagram-users/)

[^10]: [Submarine Cable Map](https://www.submarinecablemap.com/)

[^11]: [Explore page information](https://sproutsocial.com/insights/instagram-explore/#:~:text=,of%20them%20into%20new%20followers)

[^12]: [Instagram limits](https://metricool.com/instagram-limits/#:~:text=interests%20while%20making%20room%20for,new%20connections)

[^13]: [Json size analyzer](https://www.debugbear.com/json-size-analyzer)

[^14]: [Instagram filter usage](https://petapixel.com/2017/10/28/instagrams-photo-filters-used-top-users/#:~:text=Nikon%20users%20use%20filters%20on,and%20iPhone%20users%2018.6)

[^15]: [Infrastructure connectivity map](https://bbmaps.itu.int/bbmaps/)

[^16]: [Nginx load](https://github.com/denji/nginx-tuning)