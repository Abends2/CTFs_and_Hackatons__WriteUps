# MireaCTF 3

---

### Everyday crypto (crypto)

Нам дана последовательность из emoji:

```sh
🙙😳🙬🙩🙚🙘🙊😷🙤🙗😴🙸🙙🙺🙂🙫🙍😱😸🙸🙎🙖😹🙪🙣🙪🙆🙵🙎🙪🙎😹
```

![ScreenShot](screenshots/1.png)

Закидываем всю эту последлвательность в `Emoji dissector`, чтобы узнать их значения в виде кодов:

![ScreenShot](screenshots/2.png)

Выписываем их:

![ScreenShot](screenshots/3.png)

Оставляем только по два последних символа от кодов. Декодируем полученные байты в текст:

![ScreenShot](screenshots/4.png)

Затем декодируем из base64:

![ScreenShot](screenshots/5.png)

**Флаг**: cyber{un1c0d3_15_cr1n63}

---

### CS 1.6 (web)

Заходим на сервис:

![ScreenShot](screenshots/6.png)

Из хорошего - у нас есть исходники:

![ScreenShot](screenshots/7.png)

Сервис написан на python и имеет в себе секретные страницы:

![ScreenShot](screenshots/8.png)

Копание в сторону хэшей нам ничего не дало, но зато мы заметили, что у нас есть папка `.git`

![ScreenShot](screenshots/9.png)

А вот и коммиты в мастер:

![ScreenShot](screenshots/10.png)

Можно посмотреть `robots.txt`, что помогает нам найти `/super_secret_flag`

![ScreenShot](screenshots/11.png)

Естественно, доступа у нас нет

![ScreenShot](screenshots/12.png)

Открываем оснастку Git и переходим в раздел с приложением:

![ScreenShot](screenshots/13.png)

При помощи `git log` просматриваем коммиты:

![ScreenShot](screenshots/14.png)

Замечаем два потенциально интересных коммита, связанных с авторизацией:

![ScreenShot](screenshots/15.png)

![ScreenShot](screenshots/16.png)

Теперь просматриваем коммиты и нахожим `username` и `password` в открытом виде

![ScreenShot](screenshots/17.png)

Авторизуемся:

![ScreenShot](screenshots/18.png)

![ScreenShot](screenshots/19.png)

И да, мы на странице админа! Переходим в найденную директорию с флагом:

![ScreenShot](screenshots/20.png)

**Флаг**: mireaCTF{d3Cen7raliZed_baCkup_1SNT_G0OD}

---

### Joy-OSINT (OSINT)

Исходное изображение

![ScreenShot](screenshots/21.png)

Посмотрим более детально на отражение в зеркале машины:

![ScreenShot](screenshots/22.png)

Из зацепок - `Konkovo Market`, что сильно снижает диапазон поиска. Гуглим этот магазин:

![ScreenShot](screenshots/23.png)

А вот и машина с номером (год 2021 был взят из описания таска)

![ScreenShot](screenshots/24.png)

Проверяем по ОСАГО:

![ScreenShot](screenshots/25.png)

Страхователь до конца неизвестен, но если погуглить

![ScreenShot](screenshots/26.png)

Для флага нам нужен ОГРНИП страховщика

![ScreenShot](screenshots/27.png)

**Флаг**: cyber{322774600224540}

---

### Президентское празднование (OSINT)

Для начала описание таска:

```sh
Друг позвал меня отпраздновать свой день рождения в ресторан, в котором в далеком 2000 году праздновал свой президент нашей страны. Все бы ничего, но себе он заказал что-то хорошее, а мне самое дешевое блюдо из детского меню. Помоги мне, пожалуйста, найти это блюдо.
```

Гуглим про день рождениия 2000 года президента РФ и находим это:

![ScreenShot](screenshots/28.png)

Зацепка - ресторан "Подворье". Исследуем меню и получаем флаг

![ScreenShot](screenshots/29.png)

**Флаг**: MireaCTF{картофель_фри_с_кетчупом}

---

### Визит посла (OSINT)

Исходное изображение:

![ScreenShot](screenshots/30.png)

Описание:

```sh
Чтобы избежать международного конфликта наш посол прибыл на переговоры. Но вот незадача, он совсем заблудился. Помоги ему разобраться, где он находится. Флаг - координаты рекламного столба, округлённые до десятитысячных. Например, MireaCTF{12.3456,12.3456}
```

![ScreenShot](screenshots/31.png)

Цепляет необычное строение на фоне, так вот и ищем, где оно находится, название есть (может быть плоховато на скрине, но решение именно такое)

![ScreenShot](screenshots/32.png)

По картам находим столб

![ScreenShot](screenshots/33.png)

Коорлинаты

![ScreenShot](screenshots/34.png)

**Флаг**: MireaCTF{41.2385,69.3299}

---

### Фанат Геншина (OSINT)

Ищем официальный ресурс с моделями Genshin Impact:

![ScreenShot](screenshots/35.png)

![ScreenShot](screenshots/36.png)

В задании указан формат флага `mctf{}`, поэтому попробуем поискать на ресурсе что-то связанное с этим

![ScreenShot](screenshots/37.png)

И да, мы находим нужный раздел с моделями

![ScreenShot](screenshots/38.png)

Для загрузки необходимо зарегистрироваться, поставить лайк и добавить раздел в избранное:

![ScreenShot](screenshots/39.png)

Пароль для скачивания указан в шапке профиля

![ScreenShot](screenshots/40.png)

Осталось найти подходящую картинку:

![ScreenShot](screenshots/41.png)

![ScreenShot](screenshots/42.png)

![ScreenShot](screenshots/43.png)

---

### Крокодил (OSINT)

Описание:

```sh
На каком самолете летел крокодил?
```

![ScreenShot](screenshots/44.png)

Первый же запрос в гугл дает ответ на таск:

![ScreenShot](screenshots/45.png)

**Флаг**: MireaCTF{Let L-410 Turbolet}

---

### Найди меня, если сможешь (OSINT)

Описание:

```sh
Однажды я поспорил с подругой, что смогу найти, где она живёт лишь по одной фотографии. Давай проверим, сможешь ли ты это сделать. Флаг - широта и долгота дома на yandex maps с точностью до миллионных.
```

Исходник:

![ScreenShot](screenshots/46.png)

Вот тут сразу две зацепки - `Moscow City` и, похоже, что `МГУ`, но последнее еще предстоит проверить. Сразу сверяемся с картой и примерно понимаем, где примерно было снято изображение (ориентируемся на угол обзора изображения)

![ScreenShot](screenshots/47.png)

А вот и та самая местность:

![ScreenShot](screenshots/48.png)

Остается найти правильно координаты:

![ScreenShot](screenshots/49.png)

![ScreenShot](screenshots/50.png)

---

### Чего (Stegano)

У нас есть какое-то непонятное сообщение, при этом оно бессмысленно. Оказывается, в этом и суть!

![ScreenShot](screenshots/51.png)

![ScreenShot](screenshots/52.png)

Для копирования:

```sh
Dear Friend , This letter was specially selected to be sent to you ! We will comply with all removal requests ! This mail is being sent in compliance with Senate bill 1624 ; Title 6 , Section 302 ! Do NOT confuse us with Internet scam artists . Why work for somebody else when you can become rich within 96 WEEKS . Have you ever noticed society seems to be moving faster and faster & society seems to be moving faster and faster . Well, now is your chance to capitalize on this ! We will help you decrease perceived waiting time by 170% plus use credit cards on your website . You can begin at absolutely no cost to you ! But don't believe us . Prof Simpson of New York tried us and says "My only problem now is where to park all my cars" ! We are licensed to operate in all states . We implore you - act now ! Sign up a friend and you'll get a discount of 30% ! Thanks ! Dear Friend ; Especially for you - this breath-taking announcement ! We will comply with all removal requests ! This mail is being sent in compliance with Senate bill 2716 , Title 1 ; Section 303 . THIS IS NOT A GET RICH SCHEME . Why work for somebody else when you can become rich inside 28 weeks . Have you ever noticed more people than ever are surfing the web and most everyone has a cellphone ! Well, now is your chance to capitalize on this ! WE will help YOU increase customer response by 140% plus decrease perceived waiting time by 150% ! The best thing about our system is that it is absolutely risk free for you ! But don't believe us . Mrs Simpson who resides in Wyoming tried us and says "I was skeptical but it worked for me" . We assure you that we operate within all applicable laws ! If not for you then for your LOVED ONES - act now ! Sign up a friend and your friend will be rich too . Thank-you for your serious consideration of our offer .
```

**Флаг**: MireaCTF{c@n1_deC0d3_m3}

---

### Современное искусство (Stegano)

И вновь исходник:

![ScreenShot](screenshots/53.png)

Внутри изображения запароленный архив:

![ScreenShot](screenshots/54.png)

![ScreenShot](screenshots/55.png)

Декодим:

![ScreenShot](screenshots/56.png)

Применяем пароль:

![ScreenShot](screenshots/57.png)

Открываем "правильно" аудиофайл:

![ScreenShot](screenshots/58.png)
 
**Флаг**: mctf{@rt_1s_L!fe}

---

### Тайна Леонардо да Винчи (Stegano)

Исходное изображение:

![ScreenShot](screenshots/59.png)

В скатерти спрятана морзянка:

![ScreenShot](screenshots/60.png)

Декодируем:

![ScreenShot](screenshots/61.png)

**Флаг**: mctf{A_trip_to_an_art_gallery}

---

