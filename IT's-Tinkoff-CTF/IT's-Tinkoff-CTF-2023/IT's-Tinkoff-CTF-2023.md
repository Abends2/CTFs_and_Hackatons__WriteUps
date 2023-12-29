# IT's Tinkoff CTF 2023

---

### Web: Зов Аномалий
Описание:

![ScreenShot](screenshots/1.png)

Осматриваем сайт и находим карту "Зоны":

![ScreenShot](screenshots/2.png)

![ScreenShot](screenshots/3.png)

Выбираем один из артефактов на карте и открываем его в отдельном окне:

![ScreenShot](screenshots/4.png)

![ScreenShot](screenshots/5.png)

Получаем путь до картинки с артефактом:
```sh
https://its-artifacts-jk2dm72.spbctf.ru/wp-content/uploads/2023/07/kandinsky-download-1688481651933.png
```

Меняем название картинки на **flag.png**:

```sh
https://its-artifacts-jk2dm72.spbctf.ru/wp-content/uploads/2023/07/flag.png
```

![ScreenShot](screenshots/6.png)

**its{c0n6r47ul4710n5_y0u_f0und_7h3_m41n_4r71f4c7}**

---

### Web: Планетарная важность
Описание:

![ScreenShot](screenshots/7.png)

Перейдем по ссылке и увидим простой сайт, где из рабочих элементов есть "**Статус пограммы**", который возвращает "**[The system's broken]**":

![ScreenShot](screenshots/8.png)

![ScreenShot](screenshots/9.png)

Проверяем исходный код страницы и находим интересный элемент "**/execute?cmd=get-status**", проверяем, сможет ли он исполнить нашу команду **ls**:

![ScreenShot](screenshots/10.png)

```sh
https://its-broken-cb23byi7.spbctf.ru/execute?cmd=ls
```

![ScreenShot](screenshots/11.png)

К сожалению обнаруживаем, что пробелы не обрабатываются в чистом виде:

```sh
https://its-broken-cb23byi7.spbctf.ru/execute?cmd=ls%20-la
```

![ScreenShot](screenshots/12.png)

Находим способ передачи символа "пробел" через ${IFS}:

```sh
https://its-broken-cb23byi7.spbctf.ru/execute?cmd=ls${IFS}-la
```

![ScreenShot](screenshots/13.png)

Обнаруживаем список файлов и читаем **README.md**

```sh
https://its-broken-cb23byi7.spbctf.ru/execute?cmd=cat${IFS}README.md
```

![ScreenShot](screenshots/14.png)

```sh
	## Панель управления 
	### Старт приложения Для запуска приложения выполните 
	```bash curl http://management:5000/start/ ``` 

	### Обновления Для получения обновлений выполните 
	```bash curl http://management:5000/getUpdates/ ``` 

	### 	Перезагрузка Для перезагрузки приложения выполните 
	```bash curl http://management:5000/restart/ ```
```

Выполняем перезагрузку:

```sh
https://its-broken-cb23byi7.spbctf.ru/execute?cmd=curl${IFS}-s${IFS}http://management:5000/restart/
```

![ScreenShot](screenshots/15.png)

Сказано, двигаться в **/060648ac9456adba9740f7b2b119abf2bcf194c2/**. Двигаемся и находим флаг:

```sh
https://its-broken-cb23byi7.spbctf.ru/060648ac9456adba9740f7b2b119abf2bcf194c2/
```

![ScreenShot](screenshots/16.png)

**its{yoU_54VED_hUMaNi7Y_fRoM_a_M3t3Orite_FALL_w17h_RcE}**

---

### OSINT: Осьмак
Описание:

![ScreenShot](screenshots/17.png)

![ScreenShot](screenshots/18.png)

Перейдем по ссылке и увидим форму, в которую необходимо внести данные, для того, чтобы получить флаг:

![ScreenShot](screenshots/19.png)

![ScreenShot](screenshots/20.png)

Первым делом, пробуем **поиск по картинке**:

![ScreenShot](screenshots/21.png)

Находим что-то похожее на наше изображение. Проверим источник изображения:

![ScreenShot](screenshots/22.png)

Новый ориентир - **Roof Apart Hotel**:

Ищем отель на Google картах, используя данные из ресурсах-источника изображения:

![ScreenShot](screenshots/23.png)

На данном этапе понимаем, что это не тот отель, который нам нужен - обращаем внимание на угол обзора. Скорее всего, нам нужно ориентироваться на два здания, стоящих рядом:

![ScreenShot](screenshots/24.png)

Примерно проверяем еще раз угол обзора, используя вид сверху:

![ScreenShot](screenshots/25.png)

Находим другой отель - Holiday Inn Express:

![ScreenShot](screenshots/26.png)

Копируем его полный адрес:

![ScreenShot](screenshots/27.png)

Первые три пункта формы мы, предположительно, узнали, остается перебрать этажи:

![ScreenShot](screenshots/28.png)

**its{vZLOMSh1KI_ha5-B3EN_fOUND_AnD_neU7r4L1ZED}**

---

### Web: Принцесса в другом замке
Описание:

![ScreenShot](screenshots/29.png)

Переходим на сайт и наблюдаем простой аналог Тиндера. Естественно, лайкаем всех принцесс:

![ScreenShot](screenshots/30.png)

![ScreenShot](screenshots/31.png)

Нажав на кнопку "Купить премиум", нас предупреждают об ограничении покупки якобы в нашем регионе:

![ScreenShot](screenshots/32.png)

В исходном коде находим метод, который позволяет "обращаться напрямую к принцессе", используя id:

![ScreenShot](screenshots/33.png)

Пишем небоьшой скрипт для автоматизации применения параметра id:

![ScreenShot](screenshots/34.png)

Запускаем программу и в одном из ответов на наши запросы находим флаг (https://its-tinderella-w2wfm3xc.spbctf.ru/api/princess-sputnik?id=2):

![ScreenShot](screenshots/35.png)

**its{Its_a_mE_MarIO_FOUnd_a_vuln_and_FOUNd_My_loV3}**

---

### Web: Кефтеме (easy)

Описание:

![ScreenShot](screenshots/36.png)

Переходим на сайт:

![ScreenShot](screenshots/37.png)

Регистрируемся:

![ScreenShot](screenshots/38.png)

Попадаем на сам магазин:

![ScreenShot](screenshots/39.png)

Добавим в корзину товар, на который у нас достаточно средств:

![ScreenShot](screenshots/40.png)

На известен промокод, дающий 5%-ную скидку:

![ScreenShot](screenshots/41.png)

Ловим запрос через Burp Suite и отправляем в Repeater:

![ScreenShot](screenshots/42.png)

![ScreenShot](screenshots/43.png)

Повторяем запрос множество раз (т.е. один и тот же промокод применяется на один товар множество раз):

![ScreenShot](screenshots/44.png)

В итоге получаем прибавление средств:

![ScreenShot](screenshots/45.png)

Снова накручиваем, но уже через другой товар, чтобы сумма прибавления была выше:

![ScreenShot](screenshots/46.png)

![ScreenShot](screenshots/47.png)

![ScreenShot](screenshots/48.png)

![ScreenShot](screenshots/49.png)

![ScreenShot](screenshots/50.png)

В итоге нам хватает денег для покупки основного товара:

![ScreenShot](screenshots/51.png)

![ScreenShot](screenshots/52.png)

**its{ufFf_b4Rh47nYj_FrON7_ONLY_v4liDa7iON_BYP4s5_KEfT3me}**

---

### Crypto: Потерянные в космосе - YES

Описание:

![ScreenShot](screenshots/53.png)

Разбиваем geohash на составные части:

| skpf | 24c8 | 1n0t | jhrg | wr55 | 1mcm | nbub |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 96.564 | -155.97 | -161.71 | 17.133 | 143.143 | -161.943 | 48.805 |

![ScreenShot](screenshots/54.png)

Принцип декодирования через сторонние сервисы:

![ScreenShot](screenshots/55.png)

Для запуска нам необходимо указать Source и Target координаты:

![ScreenShot](screenshots/56.png)

Пример ввода неудачных координат:

![ScreenShot](screenshots/57.png)

На сервисе можно рассчитать geohash:

![ScreenShot](screenshots/58.png)

Методом проб и ошибок подбираем координаты:

![ScreenShot](screenshots/59.png)

Запускаемся:

![ScreenShot](screenshots/60.png)

![ScreenShot](screenshots/61.png)

**its{w3lc0Me_to_OUr_d3Ar_thRee_DiMeNsioNS}**

---

### Web: Пиццаувеличитель (easy)

Описание:

![ScreenShot](screenshots/62.png)

Регистрируемся на сервисе и попадаем в магазин:

![ScreenShot](screenshots/63.png)

![ScreenShot](screenshots/64.png)

Смотрим в сторону обменов:

![ScreenShot](screenshots/65.png)

![ScreenShot](screenshots/66.png)

![ScreenShot](screenshots/67.png)

![ScreenShot](screenshots/68.png)

Как видим, если переводить Беконики в Гастрофранки, а затем обратно, то часть валюты теряется. Операции между одной и той же валютой операции совершать нельзя:

![ScreenShot](screenshots/69.png)

![ScreenShot](screenshots/70.png)

А теперь внимательно:
1) 3 Беконика = 0.01 Гастрофранк
2) 0.01 Гастрофранк = 4.30 Беконика - **профит**!

![ScreenShot](screenshots/71.png)

Ловим запрос - нам нужны куки и прочее для автоматизации (обращаем внимание на session)

![ScreenShot](screenshots/72.png)

Переводим все, что у нас есть в Беконики:

![ScreenShot](screenshots/73.png)

![ScreenShot](screenshots/74.png)

Пишем сплойт, который автоматически может конфертировать валюты (не забываем про сессию):

![ScreenShot](screenshots/75.png)

![ScreenShot](screenshots/76.png)

Переводим все полученные Гастрофранки в Беконики:

![ScreenShot](screenshots/77.png)

Итог - нам хватает валюты для покупки флага:

![ScreenShot](screenshots/78.png)

![ScreenShot](screenshots/79.png)

**its{rOUnD_FUnCtIoN_c4N_BE_7Ricky}**

---

### Web: Бредущий по лезвию (easy)

Описание:

![ScreenShot](screenshots/80.png)

Переходим по ссылке и находим далее директорию **/storage/**, нажав на кнопку:

![ScreenShot](screenshots/81.png)

![ScreenShot](screenshots/82.png)

![ScreenShot](screenshots/83.png)

```sh
https://its-android-storage-w0yjed7.spbctf.ru/storage/ - 403 Forbidden
```

Сканим при помощи Nmap хост:

![ScreenShot](screenshots/84.png)

Находим zeus-admin:

```sh
http://65.109.236.11:9090/metrics
```

Видим, что есть обращения к другому хосту (домену):

![ScreenShot](screenshots/85.png)

Переходим на него:

```sh
https://its-private-domain-for-secure-android-storage-qm8w6et.spbctf.ru/storage/
```

![ScreenShot](screenshots/86.png)

**its{NOW_yoU_h4v3_aLL_7h3_KN0wL3Dge_oF_4NdroID}**

---

