## Что такое промпт (prompt)?
Промты начинаются с команды `/imagine` и могут включать текст, ссылки на изображение и параметры. Английский - основной язык Midjourney.
* **текст** описывает, какое изображение вы хотите сгенерировать
* **ссылки на иозбражения** могут быть добавлены в промт, чтобы задать стиль генерируемой картинки. Ссылки всегда идут в начале промта
* **параметры** задают версию Midjourney, стиль, размер изобажения. Параметры указываются в конце через два дефиса `--`

Также Midjourney умеет объединять два разных изображения в одно:
1. Загрузите исходное изображение (или два) на сервисы [Imgur](https://img.doerig.dev/) или [Postimages](https://postimages.org/ru/) и получите ссылки на них в формате .png, .jpg или .webp;
2. Вставьте ссылку в начало промта, а затем добавьте текстовое описание;
3. Чтобы объединить два изображения в одно, вставьте две ссылки на них подряд через запятую (торт + замок, цветочки + Александр)

```python
/imagine https://i.imgur.com/Z5UIh53.jpg торт на день рождения
```

## Использование параметров
Параметры всегда добавляются в конец промта, важно писать их правильно, через два дефиса `--` и с пробелом перед цифрами: </br>
`--v 6` для генерации изображения будет использоваться самая новая модель Midjourney V6. По умолчанию используется версия Midjourney 5.2 </br>
`--v 5` или `--v 4` для генерации изображения будет использоваться предыдущая версия Midjourney </br>
`--niji` изображение будет генерироваться в стиле аниме </br>
`--aspect` или `--ar` изменение соотношения сторон генерируемого изображения </br>
`--style raw` позволяет получить более натуральные и реалистичные изображения, уменьшая влияние эстетической обработки Midjourney </br>
`--stylize` или `--s` также влияет на художественную обработку изображения. Низкие значения создают более естественные картинки, высокие - более обработанные. По умолчанию 100, параметр варьируется от 0 до 1000 </br>
`--chaos` более высокие значения создают **более разнообразные** и **не похожие друг на друга** начальные варианты изображения, варьируется от 0 до 100 </br>
`--weird` используется для добавления необычных и эксцентричных качеств к изображениям, что приводит к уникальным и неожиданным результатам. Параметры варьируются от 0 до 3000, где 0 - отсутствие странности </br>
`--no` указывает на то, чего в изображение быть не должно: `--no цветы` </br>
`--seed` позволяет повторить или незначительно поменять результаты генерации, в случае его установки </br>
`--sameseed` </br>
`--uplight` ламповое освещение </br>
`--hd`

**Сосредоточьтесь на основной концепции. </br>
Сокращайте, когда это возможно. </br>
Меньше слов означает, что каждое из них будет иметь больший вес. </br>
Думайте о том, что важно.**

При составлении промпта рекомендуется использовать двойные двоеточия `::`
```python
/imagine astronaut on the moon :: the earth in background :: ultra realistic
```
Если используется сложный промпт с различными объектами, то рекомендуется использоваться вес объектов `dog::2`, указывающий на их важность. Используются числа от 0 до 100.

## Команды-подсказки для подготовки промпта
`/describe` + загрузка изображения: Midjourney пришлёт несколько вариантов промпта для этого изображения </br>
`/shorten` + текстовый промпт: Midjourney проанализирует промпт и даст рекомендации по его улучшению: какие слова лишние и не участвуют в генерации изображения, а какие ключевые 

Эти команды не расходуют генерации и позволяют взглянуть на промпты глазами Midjourney, чтобы лучше понять принципы их составления.

После отправки команды `/imagine` с вашим промптом начинается генерация 4 начальных изображений, она обычно занимает 1-3 минуты. </br>
Вместе с картинками появляется два ряда кнопок:
* `U` увеличивает выбранное изображение и добавляет детализацию
* `V` создаёт 4 новые вариации выбранного изображения, создаётся новая сетка изображения, аналогичная общему стилю и композиции выбранного изображения
* Повтор генерирует изображения заново с тем же промптом
* Конвертик позволяет получить `--seed` изображения, зная который можно незначительно менять результаты генерации
* `/split` вместе с загрузкой изображения разделяет сгенерированные Midjourney изображения на 4 отдельних картинки

После увеличения `U` изображения появляются новые кнопки:
* `Vary` создаёт 4 новые вариации с большими Strong или меньшими Subtle изменениями
* `Zoom out` отдаляет изображение и дорисовывает новые детали (1.5х или 2х)
* `Pan` дорисовывает изображение в выбранную сторону

## Как разместить текст на изображении?
Midjourney V6 умеет генерировать небольшой объём текста на изображениях:
* Добавьте параметр `--v 6` в конце промпта;
* Пишите текст на английском языке и в `"`кавычках`"`

```python
/imagine a photo of text "Hello World" written with a marker on a sticky note --v 6
```

## Как добиться фотореалистичного изображения?
* Добавьте параметр `--v 6` в конце промпта
* Добавьте параметр `--style raw` для снижения художественной обработки
* Используйте более низкие значения стилизации вроде `--s 0`
* Не используйте словесный мусор вроде "фотореалистично", 4k, 8k
* Можно указать тип камеры или плёнки, на которую сделан снимок: `фото на Canon R6 Mark II, 35 mm lens`, `фото на iPhone 14`, `old Kodak photo` или `плёнка llford` (чёрное-белое фото) </br>
Если указать параметр `--ar 9:16` получится вертикальное фото на телефон. Соответственно `--ar 16:9` позволяет сделать более панорамный снимки.
* Поработать с освещением и контрастностью:
    * `high key` и `low key` - высокий и низкий уровень освещённости
    * `high contrast` и `low contrast` - контрастность изображения
    * `natural light` - естественный свет
    * `uplight` - ламповая (светящаяся лампа) атмосфера
    * `global illumination` - свет распространяется, отражаясь от объектов и освещая поверхности
    * `backlit` - подсветка сзади, свет располагается позади объекта
  
## Как управлять камерой в Midjourney V6?
Как менять план:
* `Macro` - макросъёмка
* `Close-Up Shot` - крупный план
* `Full Shot` - полный кадр
* `Wide-Angle Shot` - общий план
* `Establishing Shot` - общий план, но видно больше окружения
* ~~`Extremely wide shot`~~
* `Aerial or Drone Shot` - съёмка с дрона, можно указать марку дрона `Captured by DJI MAvic 3`
* `Birds-eye-view photo`
* `View from afar`
* `Wallpaper`

Как менять ракурс:
* `Eye-level Shot` - на уровне глаз
* `Low-Angle Shot` или `Photo from below` - съёмка снизу
* `High-Angle Shot` или `Photo from above` - съёмка сверху
* `Side Profile Shot` - в профиль
* `Shot from behind` - сзади
* `Oblique Angle` - под углом
* `Over-the-Shoulder Shot` - через плечо персонажа
* ~~`Off-Center Shot`~~ - персонаж не в центре кадра
* `Fish-eye` - могут получиться крутые кадры
* `Extreme` - можно использовать эту приставку, чтобы усилить эффект названных ключевых слов

Ракурс или план лучше указывать после описания сюжета изображения. </br>
Если указывать конкретную модель, то нужно будет удостовериться, что на неё можно будет снимать данный тип плана.

## Как в Midjourney V6 создавать кинокадры
Структура промпта
```python
/imagine a cinematic scene from YEAR, MOVIE NAME, SHOT TYPE, SCENE / SUBJECT / ACTION captured by CINEMATIC CAMERA, film directed by DIRECTOR, EMOTION, LIGHTING --ar 16:9 --style raw --v 6
```
* YEAR, MOVIE NAME - в каком году вышел фильм, как называется
* SHOT TYPE - план кадра
   * `Wide shot` - широкий кадр, когда виден объект целиком и окружение
   * `A first-person shot` - снимок от первого лица
   * `Portrait` - лица крупным планом
   * `Silhoutte shot` - силуэт
* SCENE / SUBJECT / ACTION - что должно происходить в кадре: героев, их действия, пейзаж, погоду, костюмы
* CINEMATIC CAMERA - указать любую камеру со спецэффектами при киносъёмке, такие как:
   * `Super 16`, `Kodak Portra 800 film` - ретро-эффект
   * `Sony CineAlta`, `Canon Cinema EOS` - универсальные кинокамеры
   * `Phantom High-Speed Camera` - камера для скоростной съёмки
   * `DJI Phantom 4 Pro drone camera` - аэросъёмка
* DIRECTOR - указать режиссёра, чтобы добавить его авторский стиль. </br> **Необязательно, чтобы режиссёр, фильм, эпоха и жанр совпадали**
* EMOTION - `восторг`, `злость`, `удивление`, эмоциональное состояние, котороё придаёт кадру соответствующую атмосферу
* LIGHTING - освещение, `Dramatic lighting`, о выставление света есть информация выше
```python
/imagine a cinematic scene from 1914, Harry Potter ...
```
* MORE KEY WORDS
   * `Dynamic motion` - для передачи движения
   * `Details of his / her costume` - внимание к костюму персонажа
   * `Historical accuracy` - историческая правдоподобность
   * `Won the Oscar`

ФИЛЬМ | ГОД | РЕЖИССЁР
---   | --- | ---
The Man in the High Castle | 2015 | Daniel Percival
Fargo | 2014 | Matt Shakman, Colin Bucksey
Slow Horses | 2022 | James Hawes
The Young Pope | 2016 | Paolo Sorrentino
Babylon Berlin | 2017 | Henk Handloegten

## [Как Midjourney видит мир?](https://aesthetics.fandom.com/wiki/Terrorwave)
* `heroic masculinity`
* `mosscore` / `swordpunk`
* `medieval-inspired`
* `in the style of military scenes` / `in the style of terrorwave` / `in the style of romantic depictions of historical events`
* `intense close-ups` / `strong facial expression` / `detailed close-up image of a female hand`
* `wearing a burnt costume`
* `emotive body language`
* `a scene of a crowd of dressed and armed people`, `historical accuracy`
* `full of movement`
* `in military uniform`
* `during WWI era`
* `photo of nice looking white hair mustache german politician in suit and tie`
* `surrounded by swirling smoke`
* `splashy action poses`
* `facing off against a death knight with chains and a skull head`
* `fighting against an armored man holding chainsaws on his hands`
* `you have a kissing / fighting scene. he is holding his young wife's face to kiss her`
* `she exudes a captivating aura as she confidently throws her legs up on the table`
* `her eyes ablaze with determination`
```python
/imagine robert downey jr plays a communist in the style of detailed crowd scenes, violent
```

## Создание похожих персонажей в Midjourney
1. Создайте образец персонажа, сгенерировав его изображение в Midjourney;
2. Загрузите изображение на любой фотохостинг и скопируйте ссылку в формате .jpg;
3. Отправьте новый запрос на генерацию картинки Midjourney и добавьте в конце промпта параметр `--cref` и ссылку на изображение вашего персонажа;
4. С помощью параметра `--cw` от 0 до 100 можно управлять степенью похожести: при `--cw 100` копируются черты лица, причёска и одежда, при `--cw 0` - тольцо лицо.
Опция хорошо работает со сгенерированными картинками и **не предназначена** для обработки фото реальных людей.

## Копирование стилей в Midjourney
1. Загрузите изображение на любой фотохостинг и скопируйте ссылку в формате .jpg;
2. Отправьте запрос на генерацию Midjourney и добавьте в конце промта параметр `--sref` и ссылка на изображение-образец стиля;
3. С помощью параметра `--sw` можно управлять, насколько сильно образец влияет на стиль (по умолчанию `--sw 100`

## February Series. Что работает?
`свет проникает сквозь окна`, `medieval-inspired`, `динамичный кадр из фильма`, `terrorwave`, `global illumination`, `strong facial expression`, `pre-revolutionary Petersburg`, `establishing shot`, `cinematic scene from Babylon Berlin`, `Rufus Sewell`, `Crystal Marie Reed`, `Phantom High-Speed Camera`, `full of movement`, `in a film about first Russian revolution of 1905`
