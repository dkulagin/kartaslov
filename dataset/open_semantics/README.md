# Датасет: открытая семантика русского языка

Датасет содержит результаты разметки слов и выражений русского языка по семантическим срезам (проекциям, аспектам). Например: относится ли существительное к материальным предметам, называет ли слово вещество, предмет, конструкцию или живое существо, является ли контейнером и т.д.

На данный момент подробно описаны конкретные имена существительные, для абстрактных приводится очень поверхностная классификация. Разметка глаголов и имён прилагательных находится в процессе активной разработки и в настоящем наборе не приводится.

Тональный словарь русского языка, где слова и выражения размечены по эмоционально-оценочной полярности с указанием силы заряда (свобода +++, у разбитого корыта --), было решено вынести в [отдельный датасет](../kartaslovsent).

## Интерактивный навигатор и облегчённая версия

По мере развития разметка неизбежно усложняется, но нам важно сохранить прозрачность и удобство использования данных. Мы пошли по двум направлениям:

1. Вы можете детально исследовать приведённые данные без необходимости скачивания в [интерактивном навигаторе].
2. Существует облегчённая версия датасета, где каждому слову сопоставлен ровно один крупный тег (человек, предмет, действие, сооружение и т.д.) и которую можно использовать прямо из коробки: [облегчённая версия датасета].

## Структура записи и формат датасета

Слова и выражения размечены по нескольким срезам (slices). В рамках каждой семантической проекции существует несколько вариантов ответа, которые будут описаны ниже для каждого аспекта в отдельности.

В датасете одновременно приводится как краудсорсинговая разметка, так и предсказание созданной нами модели.

Итого, каждая запись включает в себя следующие поля:

| Поле  | Комментарий |
| ------------- | ------------- |
| term  | слово или выражение (обобщённо «терм»)  |
| slice | срез (смысловой аспект, семантическая проекция)  |
| answerA | предсказание А  |
| probaA | уверенность А  |
| answerB | предсказание Б  |
| probaB | уверенность Б  |
| hmAnswerA | разметка А  |
| hmAnswerB | разметка Б  |
| hmRatio | соотношение разметки А/Б  |
| otherRatio | уровень сброса  |

[Подробное описание полей разметки]

Все файлы имеют формат CSV, разделитель точка с запятой, кодировка UTF-8.

## Иерархия семантических проекций

Каждый терм может быть размечен несколькими семантическими тегами, которые могут образовывать между собой иерархические связи. Соответственно все проекции можно представить в виде леса деревьев. В каждом узле дерева записывается название смыслового среза и указываются возможные значения для данного конкретного терма. Лучше всего посмотреть вживую в [интерактивном навигаторе].

```
== ИЕРАРХИЯ СЕМАНТИЧЕСКИХ ПРОЕКЦИЙ ==

ENTITY
|_ PHYSICAL:ROLE
  |_ PHYSICAL:ORGANIC:ROLE
  |_ PHYSICAL:INORGANIC:ROLE
    |_ PHYSICAL:CONSTRUCTION:ROLE
    |_ ATTR:INORGANIC:WEARABLE
    |_ PHYSICAL:THING:ROLE
      |_ PHYSICAL:TOOLS:ROLE
|_ ATTR:PHYSICAL:CONTAINER
  |_ ATTR:PHYSICAL:CONTAINER:TYPE
|_ ATTR:PHYSICAL:PLACE
|_ ATTR:PHYSICAL:PHY_STATE
|_ ABSTRACT:ROLE
|_ ATTR:ABSTRACT:CONTAINER
  |_ ATTR:ABSTRACT:CONTAINER:TYPE
|_ ATTR:ABSTRACT:PLACE
|_ ATTR:ABSTRACT:PHY_STATE
EMOTION

== ОТВЕТЫ & СТАТИСТИКА ==

                        slice |            answer | count |
                              |                   |       |
                       ENTITY |          PHYSICAL | 18071 |
                       ENTITY |          ABSTRACT | 14327 |
                              |                   |       |
                PHYSICAL:ROLE |           ORGANIC | 10082 |
                PHYSICAL:ROLE |         INORGANIC |  7989 |
                              |                   |       |
        PHYSICAL:ORGANIC:ROLE |             HUMAN |  7189 |
        PHYSICAL:ORGANIC:ROLE |            ANIMAL |  1214 |
        PHYSICAL:ORGANIC:ROLE |              FOOD |   850 |
        PHYSICAL:ORGANIC:ROLE |             PLANT |   509 |
        PHYSICAL:ORGANIC:ROLE |           ANATOMY |   320 |
                              |                   |       |
      PHYSICAL:INORGANIC:ROLE |             THING |  4226 |
      PHYSICAL:INORGANIC:ROLE |      CONSTRUCTION |  2812 |
      PHYSICAL:INORGANIC:ROLE |         SUBSTANCE |   951 |
                              |                   |       |
   PHYSICAL:CONSTRUCTION:ROLE |         APARTMENT |  1392 |
   PHYSICAL:CONSTRUCTION:ROLE |           TERRAIN |   968 |
   PHYSICAL:CONSTRUCTION:ROLE |         TRANSPORT |   452 |
                              |                   |       |
      ATTR:INORGANIC:WEARABLE |      NON_WEARABLE |  3089 |
      ATTR:INORGANIC:WEARABLE |          WEARABLE |  1137 |
                              |                   |       |
          PHYSICAL:THING:ROLE |             TOOLS |  1177 |
          PHYSICAL:THING:ROLE |          WEARABLE |   559 |
          PHYSICAL:THING:ROLE |            DISHES |   312 |
          PHYSICAL:THING:ROLE |           WEAPONS |   138 |
          PHYSICAL:THING:ROLE | MUSIC_INSTRUMENTS |    67 |
                              |                   |       |
          PHYSICAL:TOOLS:ROLE |   PHY_INTERACTION |   412 |
          PHYSICAL:TOOLS:ROLE |       INFORMATION |   209 |
          PHYSICAL:TOOLS:ROLE |         EM_ENERGY |   128 |
                              |                   |       |
      ATTR:PHYSICAL:CONTAINER |   NOT_A_CONTAINER | 13190 |
      ATTR:PHYSICAL:CONTAINER |         CONTAINER |  2683 |
                              |                   |       |
 ATTR:PHYSICAL:CONTAINER:TYPE |    CONFINED_SPACE |  1338 |
 ATTR:PHYSICAL:CONTAINER:TYPE |         CONTAINER |   786 |
 ATTR:PHYSICAL:CONTAINER:TYPE |          OPEN_AIR |   305 |
 ATTR:PHYSICAL:CONTAINER:TYPE |        BAG_OR_BOX |   133 |
 ATTR:PHYSICAL:CONTAINER:TYPE |            CAVITY |   121 |
                              |                   |       |
          ATTR:PHYSICAL:PLACE |       NOT_A_PLACE | 14982 |
          ATTR:PHYSICAL:PLACE |             PLACE |  3089 |
                              |                   |       |
      ATTR:PHYSICAL:PHY_STATE |             SOLID | 14751 |
      ATTR:PHYSICAL:PHY_STATE |             FLUID |  1634 |
      ATTR:PHYSICAL:PHY_STATE |            FABRIC |   837 |
      ATTR:PHYSICAL:PHY_STATE |           PLASTIC |   469 |
      ATTR:PHYSICAL:PHY_STATE |              SAND |   380 |
                              |                   |       |
                ABSTRACT:ROLE |            ACTION |  6985 |
                ABSTRACT:ROLE |             HUMAN |  4379 |
                ABSTRACT:ROLE |           PHYSICS |  1526 |
                ABSTRACT:ROLE |       INFORMATION |  1014 |
                ABSTRACT:ROLE |          ABSTRACT |   423 |
                              |                   |       |
      ATTR:ABSTRACT:CONTAINER |   NOT_A_CONTAINER |  6504 |
      ATTR:ABSTRACT:CONTAINER |         CONTAINER |   852 |
                              |                   |       |
 ATTR:ABSTRACT:CONTAINER:TYPE |    CONFINED_SPACE |   760 |
 ATTR:ABSTRACT:CONTAINER:TYPE |          OPEN_AIR |    64 |
 ATTR:ABSTRACT:CONTAINER:TYPE |         CONTAINER |    21 |
 ATTR:ABSTRACT:CONTAINER:TYPE |            CAVITY |     6 |
 ATTR:ABSTRACT:CONTAINER:TYPE |        BAG_OR_BOX |     1 |
                              |                   |       |
          ATTR:ABSTRACT:PLACE |       NOT_A_PLACE |  5896 |
          ATTR:ABSTRACT:PLACE |             PLACE |  1460 |
                              |                   |       |
      ATTR:ABSTRACT:PHY_STATE |             SOLID |  5957 |
      ATTR:ABSTRACT:PHY_STATE |             FLUID |  1399 |
                              |                   |       |
                      EMOTION |         NEUT:PSTV | 21552 |
                      EMOTION |              NGTV | 14557 |
                      EMOTION |              PSTV | 14044 |
                      EMOTION |              NEUT |  8895 |
                      EMOTION |         NEUT:NGTV |  8344 |
```

Машиночитаемая версия иерархии находится в файле [hierarchy.csv]:

| Поле (hierarchy.csv)  | Комментарий |
| ------------- | ------------- |
| slice | семантическая проекция |
| parent | родительская проекция; для верхних срезов — пустая строка |
| depth | глубина; для верхних срезов равна 0 |
| answers | варианты ответов, перечисленные через ЗАПЯТУЮ |

## Известные проблемы и допущения
* Некоторые растения и животные годятся для употребления в пищу, соответственно ряд термов может плавать между классами `FOOD/PLANT` и `FOOD/ANIMAL` в срезе `PHYSICAL:ORGANIC:ROLE`. При автоматической разметке классу `«еда» (FOOD)` отдаётся наименьший приоритет, т.е. туда стремится попасть только та пища, которая лишена описанной неоднозначности.

   В будущем решить данную проблему планируется введением атрибута `«съедобности»`, не привязанного к тому или иному классу. 
* (В дополнение к предыдущему пункту.) Некоторые принимаемые внутрь жидкости попадают в категорию `SUBSTANCE` проекции `PHYSICAL:INORGANIC:ROLE`.
* В аспекте `PHYSICAL:CONSTRUCTION:ROLE` допустимо попадание некоторых конструкций и мебели («стремянка», «гильотина») в класс `APARTMENT`. Для отделения помещений следует использовать атрибут `ATTR:PHYSICAL:CONTAINER:CLASS`, маркирующий их как `CONFINED_SPACE («замкнутое пространство»)`;
* Класс `MUSIC_INSTRUMENTS` должен называться `MUSICAL_INSTRUMENTS`. Поправим в следующей версии.

## Предыдущие версии

Разметка является экспериментальной, её структура с течением времени переосмысливается и меняется. Мы решили, что будет разумно сохранять предыдущие версии датасета: [предыдущие версии].

## Лицензия

Данный датасет распространяется по лицензии [CC BY-NC-SA 4.0]. Простыми словами — вы можете свободно использовать его в личных, научных, исследовательских и любых других целях, не подразумевающих получения дохода коммерческим путём. При этом от вас требуется указать ссылку на лицензию и на этот репозиторий. Производные работы должны распространятся под аналогичной лицензией.

Будем признательны, если вы скинете несколько строк на kartaslov@mail.ru о том, как вы планируете использовать датасет — нам это интересно, как исследователям, и поможет сделать датасет лучше в будущем.

По вопросам использования датасета в коммерческих целях смотрите развёрнутый комментарий: [использование данных в коммерческих целях].

[использование данных в коммерческих целях]: <../../readme/commercial_use.md>
[CC BY-NC-SA 4.0]: https://creativecommons.org/licenses/by-nc-sa/4.0/
[интерактивном навигаторе]: https://research.kartaslov.ru/
[предыдущие версии]: <../open_semantics_history>
[Подробное описание полей разметки]: <readme/format.md>
[облегчённая версия датасета]: <simple>
[hierarchy.csv]: <hierarchy.csv>