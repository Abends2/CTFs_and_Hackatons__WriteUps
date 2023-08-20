# Atom Skills 2023 - Mirea Qualifying Stage 2/2 - CTF

---

## Stego: New image

Для начала нам дано изображение:

![ScreenShot](screenshots/1.png)

Проверим его через Aperi'Solve:

![ScreenShot](screenshots/2.png)

При просмотре различных цветовых каналов изображения, находим флаг:

![ScreenShot](screenshots/3.png)

Флаг: REACTF{S0m3An0th3RFl5g}

---

## Stego: Mysterious QR

Дано изображение с разноцветным QR-кодом:

![ScreenShot](screenshots/4.png)

Переносим изображение в Paint и превращаем его в ч/б изображение:

![ScreenShot](screenshots/5.png)

Затем считываем информацию:

![ScreenShot](screenshots/6.png)

Флаг: REACTF{QRcodes_1ts_v3ry_simpl3}

---

## Stego: Take a toad

Дано изображение:

![ScreenShot](screenshots/7.png)

Проверяем его через Aperi'Solve и в разделе Zsteg находим флаг:

![ScreenShot](screenshots/8.png)

Флаг: flag{l1k3_1f_l0ve_th3_t0ads}

---

## Stego: Mint

Исходное изображение:

![ScreenShot](screenshots/9.jpg)

Через binwalk находим вложенный в изображение архив формата RAR:

![ScreenShot](screenshots/10.png)

![ScreenShot](screenshots/11.png)

Далее получаем хэш при помощи rar2john, который будем брутить:

![ScreenShot](screenshots/12.png)

В архиве находится файл, который содержит в себе строку формата base64:

![ScreenShot](screenshots/13.png)

Декодируем ее и получаем флаг:

![ScreenShot](screenshots/14.png)

Флаг: flag{k33p_th3_w0r!d_fr()m_c@t$}

---

## Stego: 01010001001

Нам дан файл, внутри которого находятся 0 и 1:

![ScreenShot](screenshots/15.png)

Формируем из имеющихся данных QR-код: 

![ScreenShot](screenshots/16.png)

Сканируем его и получаем флаг:

![ScreenShot](screenshots/17.png)

Флаг: flag{are_you_robot?}

---

## Crypto: Some RSA

Дано:
n=2575907945382619141476197046730769503363459
e=65567
c=612868338425011852037646590456016465505370

Декодируем RSA при помощи dCode.fr:

![ScreenShot](screenshots/18.png)

REACTF{0x8d9d55d9989279b5352764159c20c07307a}

---
## Stego: Your Favourite Salad

Дано обрезанное изображение:

![ScreenShot](screenshots/19.png)

Через binwalk извлекаем архив:

![ScreenShot](screenshots/20.png)

Получаем хэш и брутим:

![ScreenShot](screenshots/21.png)

![ScreenShot](screenshots/22.png)

В архиве находим вторую часть QR-кода:

![ScreenShot](screenshots/23.png)

Соединяем два изображения и получаем целый QR

![ScreenShot](screenshots/24.png)

Читаем и забираем флаг:

![ScreenShot](screenshots/25.png)

flag{R@!f$_!fw!f$_N43d@c_m3_w!v3}

---
