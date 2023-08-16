# MireaCTF 1 (06.11.2022)

---

## Task 1: Date Service

Заходим на сайт и нажимаем на кнопку «Get Date». После чего видим появившуюся дату:

![ScreenShot](screenshots/1.png)

Зайдем в инспектор и посмотрим на исходный код страницы. Из интересного сразу бросается в глаза скрытый «input» (hidden):

![ScreenShot](screenshots/2.png)

Попробуем ввести в поле «value» другое значение, например, «whoami» (проверка на RCE – Remote code execution – удаленное внедрение кода на сервере):

![ScreenShot](screenshots/3.png)

В итоге получаем ответ «user», что означает наличие RCE:

![ScreenShot](screenshots/4.png)

Далее посмотрим, какие команды нам доступны, при помощи ввода «help»:

![ScreenShot](screenshots/5.png)

Список команд:

![ScreenShot](screenshots/6.png)

После этого пробуем ввести «ls», но результата не получаем, поэтому попробуем «echo \*»:

![ScreenShot](screenshots/7.png)

![ScreenShot](screenshots/8.png)

Как итог, «echo \*» сработал, а это означает, что мы находимся в командной оболочке Bash. Осталось только прочитать флаг.

![ScreenShot](screenshots/9.png)

Флаг: flag{4n07h3r_w4y_t0_r34d_7h3_f1l3}

---

## Task 2: On takeoff! – Part 1

Переходим по ссылке и видим стартовую страницу:

![ScreenShot](screenshots/10.png)

Попробуем перейти в какую-нибудь другую директорию. Переходим видим 404, но после слова Page, вывелась директория, в которую мы хотели перейти. Попробуем вместо директории ввести что-то по интереснее. Ориентируемся на шаблон:

![ScreenShot](screenshots/11.png)

Вводим выражение:

![ScreenShot](screenshots/12.png)

Результат – вычисление введенного выражения:

![ScreenShot](screenshots/13.png)

Впишем в URL `{{ config.items() }}`, в результате получим словарь с конфигурационными значениями flask.

![ScreenShot](screenshots/14.png)

![ScreenShot](screenshots/15.png)

Если до вас никто не решал этот таск, то у вас будет меньше значений, так как еще никто не подключил библиотеку os.

![ScreenShot](screenshots/16.png)

Далее пишем `{{ ''.__class__.__mro__ }}`, это выведет список существующих классов (впереди две одинарные кавычки):

![ScreenShot](screenshots/17.png)

![ScreenShot](screenshots/18.png)

Нам нужны подклассы класса object, пишем `{{''.__class__.__mro__[1].__subclasses__() }}`

![ScreenShot](screenshots/19.png)

![ScreenShot](screenshots/20.png)

Получаем список, в нем ищем что-то, что позволит исполнять команды. В данном случае это **subprocess.Popen**

Теперь нужно узнать какой у него номер в этом списке. Для этого пишем `{{''.__class__.__mro__[1].__subclasses__()[266:] }}` и подбираем такое число, чтобы subprocess.Popen был в начале списка.

![ScreenShot](screenshots/21.png)

(не получилось)

Получается `{{ ''.\_\_class\_\_.\_\_mro\_\_[1].\_\_subclasses\_\_()[394:] }}`:

![ScreenShot](screenshots/22.png)

![ScreenShot](screenshots/23.png)

Теперь, когда мы нашли нужны класс, попробуем выполнить команду на сервере (RCE).

![ScreenShot](screenshots/24.png)

![ScreenShot](screenshots/25.png)

Команда исполнилась! Теперь найдем и прочитаем флаг:

![ScreenShot](screenshots/26.png)

![ScreenShot](screenshots/27.png)

Первый флаг мы получили! Но нам этого мало, нам нужно все.

Флаг: flag{py7h0n_fl45k_5s71}

---

Task 2: On takeoff! – Part 2

Повышаем привилегии. Проверяем, какие программы нам доступны с правами рута без пароля:

![ScreenShot](screenshots/28.png)

![ScreenShot](screenshots/29.png)

Видим, что мы можем запускать **/usr/bin/vim** от имени рута без пароля. Мы можем повысить свои привилегии с его помощью, так как он умеет выполнять системные команды.

Гуглим что-то вроде «vim privesc» и попадаем на сайт: https://gtfobins.github.io/gtfobins/vim/

![ScreenShot](screenshots/30.png)

Первый вариант нам подойдет, но если его вставить в URL, то получим ошибку, так как шаблонизатор не может обработать знаки.

Команда: `sudo /usr/bin/vim –c ‘:!ls /root/’` - её мы преобразуем в base64 и вставляем в наш шаблон:

![ScreenShot](screenshots/31.png)

Результат:

![ScreenShot](screenshots/32.png)

Обнаруживаем что страница долго висит, а потом падает в 504. Это происходит из-за того, что vim работает в интерактивном режиме, а браузер его не поддерживает. В итоге нам нужно переделать команду так, чтобы vim выполнял команду и закрывался без перехода в интерактивный режим. Немного изучив документацию vim’а у получается такая команда:

`sudo /usr/bin/vim --cmd ':!ls /root/' -ec 'qa!'` – её тоже в base64 и в шаблон

Результат:

![ScreenShot](screenshots/33.png)

Все работает! Забираем флаг

`sudo /usr/bin/vim --cmd ':!cat /root/root_flag.txt' -ec 'qa!'` - тоже в base64 и в шаблон

![ScreenShot](screenshots/34.png)

Флаг: flag{35c4p3_fr0m_v1m}

---
