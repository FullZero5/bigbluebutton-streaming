<h1 align="center">BigBlueButton Streaming</h1>
<p align="center">BigBlueButton Streaming — ваше бесплатное, открытое решение для расширения ваших виртуальных классов на тысячи учеников по всему миру. Транслируйте живые видео на YouTube, Facebook, Vimeo или любой RTMP-сервер прямо из BigBlueButton. Больше нет ограничений по пользователям — обучайте без границ.</p>

<br /><br/>
<img style="width: 100%; height: auto;" src="/static/bigbluebutton-streaming.gif" alt="bigbluebutton-streaming" /> <br/><br/>

<p>Воплотите безграничный образовательный опыт с помощью BigBlueButton Streaming, конечного решения для ваших растущих образовательных потребностей. Разработанное как бесплатное расширение с открытым исходным кодом, BigBlueButton Streaming позволяет расширить ваши виртуальные классы на тысячи учеников по всему миру.

Широко признанный как ведущее программное обеспечение для открытых классов, BigBlueButton доверяют многочисленные образовательные учреждения по всему миру. Однако, с ограничением в 100 пользователей на класс, проведение крупных образовательных мероприятий стало проблемой — до сегодняшнего дня.

Представляем BigBlueButton Streaming, ваш ключ к проведению масштабных одноразовых мероприятий или регулярных переполненных занятий. Беспрепятственно транслируйте ваши виртуальные классы прямо из BigBlueButton на такие платформы, как YouTube, Facebook, Vimeo или любой RTMP-сервер.

Это просто в использовании — введите URL-адрес RTMP и ключ доступа, нажмите "Начать трансляцию", и вуаля! Ваш класс становится доступен и теперь может охватить тысячи студентов одновременно. Это интуитивно понятный, удобный инструмент разрушает границы в цифровом обучении, приближая образование к тем, кто его жаждет.

Испытайте это революционное расширение уже сегодня. Раскройте весь потенциал виртуального обучения с помощью BigBlueButton Streaming, потому что образование не должно знать границ.</p>


<br/><br/>

## 📋 Требования

Для установки этого программного обеспечения необходимо установить BigBlueButton.

**Минимальные требования к окружающей среде**

- Программное обеспечение совместимо с версиями BigBlueButton ['2.6.10', '2.6.12', '2.7.0-beta.2', '2.7.12']. Убедитесь, что одна из этих версий предварительно установлена.
- Docker должен быть установлен на системе для управления контейнеризацией и развертыванием BigBlueButton.
- Необходим правильно настроенный и функционирующий TURN-сервер для обеспечения реального времени коммуникации и медиа-ретрансляции.
- У вас должна быть учетная запись пользователя на вашей системе, настроенная для выполнения команд sudo без необходимости ввода пароля каждый раз. Это важно для некоторых процессов установки, требующих прав администратора.

<br/><br/>


## 📦 Установка

- Клонируйте репозиторий.
- Перейти в каталог `bigbluebutton-streaming/`
- Запустите install.sh

```bash
git clone https://github.com/FullZero5/bigbluebutton-streaming

cd bigbluebutton-streaming

bash install.sh
```

> 🚨 Примечание: install.sh перезапустит сервер bigbluebutton, пожалуйста, убедитесь, что на сервере нет запущенных встреч.

> 💡 Убедитесь, что остановили трансляцию перед завершением сессии BigBlueButton.


<br/>
<br/>

## 🔗🔑 Установка URL и ключа доступа по умолчанию для RTMP сервера

После установки можно установить URL сервера потоковой передачи по умолчанию и ключ доступа, 
отредактировав файл `/usr/share/meteor/bundle/programs/server/assets/app/config/settings.yml`.

```bash
public:
  app:
    # BigBlueButton-streaming rtmp URL and stream key.
    # set default streaming server URL and access key here.
    rtmpURL: ''
    streamKey: ''
```

После установки URL-адреса rtmp и ключа потока перезапустите клиент html5 bigbluebutton.

```bash
sudo systemctl restart bbb-html5
```

<br/><br/>

## 🔄 Concurrent Streaming

If you aim to host multiple meetings simultaneously on your single BigBlueButton server and require concurrent streaming for each, follow these steps to set it up.

- Navigate to the streaming server directory:
```bash
cd bigbluebutton-streaming/streaming-server/
```

- Open the .env file for editing using sudo privileges. For instance, with the vi editor:
```bash
sudo vi .env
```

- In the .env file, modify the NUMBER_OF_CONCURRENT_STREAMINGS variable to indicate the number of simultaneous streams you want to handle. For instance, to enable three concurrent streams:
```bash
NUMBER_OF_CONCURRENT_STREAMINGS=3
```

- Save your changes and exit the file editor.

- Build  Docker image:
```bash
docker build -t bbb-stream:v1.0 .
```

- Finally, restart your bbb-streaming service with pm2:
```bash
pm2 restart bbb-streaming
```

<br />
Теперь ваш сервер может обрабатывать количество одновременных потоков, которое вы указали, позволяя каждой встрече транслироваться одновременно.


<br /> <br />


<div align="center">
  <img alt="bbb-streaming-error" width="100%" src="static/bigbluebutton-streaming-error.png"> 
</div>

<br />

> 🚨 Примечание: Если вы столкнулись с ошибкой, показанной выше, это указывает на то, что ваш сервер достиг лимита для одновременных потоков.

<br />

> 💡 Запомните: Успешная работа одновременной потоковой передачи сильно зависит от мощности вашего сервера. Убедитесь, что ваш сервер способен обрабатывать количество одновременных потоков, которое вы установили.

<br/><br/>



## 🗑️ Удаление

- Перейдите в каталог `bigbluebutton-streaming/`.
- run `uninstall.sh`.
```bash
cd bigbluebutton-streaming

bash uninstall.sh
```

<br/><br/>


## 🛠️ Troubleshooting

<br />

<div align="center">
  <img alt="bbb-streaming-error" width="90%" src="static/streaming-error-1.png"> 
</div>
<br/>

1. 🚨 Когда вы сталкиваетесь с указанной ошибкой, скорее всего, бэкенд BigBlueButton-streaming (bbb-streaming) не запущен. Пожалуйста, следуйте приведенным ниже шагам для устранения неполадок:

    - Выполните команду, чтобы проверить, присутствует ли pm2 и запущено ли приложение node на вашем сервере BigBlueButton:

        ```bash
        pm2 list
        ```
    
    <div align="center">
      <img alt="bbb-streaming-error" width="90%" src="static/streaming-error-2.png"> 
    </div>
     <br/>

    - Если вы видите bbb-streaming в списке выше со статусом, отличным от online, вам нужно перезапустить bbb-streaming, используя следующую команду:

        ```bash
        pm2 restart bbb-streaming
        ```

    - Теперь вы должны увидить, что статус bbb-streaming отображается как online. 

    <div align="center">
      <img alt="bbb-streaming-error" width="90%" src="static/streaming-error-3.png"> 
    </div>

    <br/>


2. 🚨 Если есть еще ошибками, посмотрите журналы ошибок, выполнив следующую команду:

      ```bash
      pm2 logs bbb-streaming
      ```
<br/>

  - Если вы видите журнал ошибок, как показано ниже, это означает, что сообщение об ошибке, которое вы видите, обычно возникает при попытке использовать sudo в скрипте или автоматизированном процессе, где нет доступного терминала для интерактивного ввода пароля.

    <div align="center">
      <img alt="bbb-streaming-error" width="90%" src="static/streaming-error-4.png"> 
    </div>
    <br/>

    - To fix this, a user to run sudo without needing to enter a password, you can modify the sudoers file.Here are the steps:

        - Open a terminal.
        - Type `sudo visudo`. This will open the sudoers file in the system's default text editor. The visudo command checks the syntax of the sudoers file to help prevent you from accidentally locking yourself out of the system.

        - Scroll down to the section of the file that looks like this:

        ```bash
        # User privilege specification
        root    ALL=(ALL:ALL) ALL
        ```

        - Underneath the root user, add the following line, replacing `username` with the username for which you want to allow passwordless sudo commands:

        ```bash
        username ALL=(ALL:ALL) NOPASSWD: ALL
        ```

        - Press `Ctrl+X` to exit the editor, then `Y` to save changes, and `Enter` to confirm.

        - Now Restart the `bbb-streaming` service by running the following command:

        ```bash
        pm2 restart bbb-streaming
        ```

        <br />

        Now, the user you added will be able to use `sudo` without being asked for a password. 

<br/>

> 📝If you find diffrent logs, share with us by creating an issue on this repository 📮. Please ensure to include relevant screenshots and a detailed description of the problem for better assistance.
 
<br /> <br />

3. 🚨 When you run `bash uninstall.sh`, and if encounter below error:
    ```
    permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json?filters=%7B%22ancestor%22%3A%7B%22bbb-stream%3Av1.0%22%3Atrue%7D%7D": dial unix /var/run/docker.sock: connect: permission denied
    ```
    - The error message you're encountering is related to the Docker permissions. Your user does not have the required permissions to interact with the Docker daemon. To fix this:
    
    - **Add your user to the docker group:** This is the most straightforward solution. It allows your user to interact with the Docker daemon as if you were the root user. 

        ```bash
        sudo usermod -aG docker $USER
        ```

      And then **log out and log back in** so that your group membership is re-evaluated.

    - Run again `bash uninstall.sh` and you should be good to go.

<br />
<br /><br />

## 🔎 Как это работает

1. 🚀 Приложение Node.js: Приложение Node.js запускает контейнер для потоковой передачи, выступая в роли контроллера для трансляции встреч BigBlueButton.

2. 📬 REST API: Приложение предоставляет REST API для получения запросов на начало и остановку потоковой передачи.

3. 🔑 Переменные окружения: Чувствительные данные, такие как URL BigBlueButton, секрет и другие конфигурации, хранятся в переменных окружения, загружаемые из файла .env.

4. 🔗 Интеграция Puppeteer: Puppeteer используется для запуска headless браузера Chrome, позволяя программно взаимодействовать с пользовательским интерфейсом встречи BigBlueButton.

5. 🖥️ Виртуальный дисплей: Xvfb создает виртуальный дисплей для Chrome, позволяя ему работать без физического сервера отображения.

6. 🤝 Присоединение к встрече: Приложение настраивает Puppeteer для присоединения к встрече BigBlueButton в качестве зрителя с определенными настройками, такими как режим только прослушивания и видимость элементов.

7. 📼 Запись экрана: Дочерний процесс вызывает ffmpeg для записи экрана встречи и потоковой передачи его на указанный RTMP-сервер.

8. ⏹️ Остановка потоковой передачи: Приложение ожидает остановки потоковой передачи или завершения встречи и останавливает процесс ffmpeg, завершая процесс потоковой передачи.
<br /> <br />
<img alt="bbb-streaming"  src="/static/bigbluebutton-streaming-sequence.png"/>
