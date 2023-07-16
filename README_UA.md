[UA](README_UA.md) | [ENG](README.md)

***

# Genshin Automation
## Цей інструмент автоматично збиратиме винагороди HoYoLab за щоденний вхід. Це його основна мета.

На жаль, через порушення умов GitHub цей засіб автоматизації не можна опублікувати тут. Через велику кількість форків та активності його двічі видаляли, проте я досі підтримую його та він досі працює, також я зробив аналогічний проєкт для Honkai. Якщо вам потрібен код проєкту ви можете звернутися до мене в [Telegram](https://t.me/call_me_noname) або [Discord](https://discordapp.com/users/237628352914128897/) :)

---

![Genshin Impact daily login rewards](/images/hoyolab/hoyolab-reward-list.png)

---

## Як користуватися цим інструментом?
**Зробіть розгалуження (Fork) цього репозиторію до свого облікового запису GitHub та слідуйте інструкціям.**

# Автоматичний збір винагород Hoyolab за щоденний вхід
  
### 1) Отримайте параметри Cookies своїх акаунтів
  <details>
  <summary>Інструкція</summary>

1. Я використовую браузер Chrome, якщо ви використовуєте інший браузер, деякі назви можуть відрізнятися.
2. Відкрийте файл `siteScript.js` і скопіюйте його вміст. Або скопіюйте код нижче
    ```
    var cookie=start();
    var ask=confirm('Cookie: '+cookie+'\n\nClick confirm to copy Cookie.');if(ask==true){copy(cookie);msg=cookie}else{msg='Cancel'}
    function start() {
        return "ltoken=" + getCookie("ltoken") + ";ltuid=" + getCookie("ltuid") + ";";
        function getCookie(name) {
            const value = ";" + document.cookie;
            const parts = value.split("; " + name + "=");
            if (parts.length === 2) return parts.pop().split(';').shift();
        }
    }
    ```
3. Перейдіть на сторінку https://www.hoyolab.com/genshin/, та увійдіть в свій акаунт.
4. Клацніть правою кнопкою миші на сторінці та виберіть **Переглянути код**, а потім виберіть вкладку **Консоль**.
5. Вставте скопійований код у другий абзац і натисніть **Enter**.
6. У вікні, що з’явиться, натисніть **Ok**, і необхідні параметри cookie будуть автоматично скопійовані в буфер обміну.
![Cookie copy window](/images/hoyolab/h-step-1.png)
</details>


### 2) Налаштуйте змінні в GitHub
<details>
<summary>Інструкція</summary>

1. Давайте додамо параметри cookie до змінної, для цього перейдіть до наступного шляху в клонованому репозиторії.
**Settings** -> **Secrets**  -> **Actions**  -> **New repository secret**
![Path to add Cookies to repository variable](/images/hoyolab/github-1.png)
2. Введіть назву змінної та файли cookie залежно від того, для чого ви хочете налаштувати своє сховище.
![Page for adding variables](/images/hoyolab/github-2.png)
У першому полі потрібно вказати назву змінної, у другому полі Cookies. Дивіться приклади нижче.

##### Приклад для одного облікового запису
3. Назва змінної: `HOYOLAB_COOKIE`, приклад файлів cookie: `ltoken=t************************************ **Q;ltuid=8******4;`
У цьому випадку вам потрібно просто вставити отриманий текст у розділ `1) Отримайте параметри Cookies своїх акаунтів`.
  
![Adding Cookies for One Account](/images/hoyolab/github-2.1.png)

##### Приклад для кількох облікових записів
3. Назва змінної: `HOYOLAB_COOKIES`, приклад файлів cookie: `["ltoken=a************************************** ****B;ltuid=1******2;","ltoken=c**************************** ***********D;ltuid=3******4;","ltoken=e******************** *****************F;ltuid=5******6;"]`
У цьому випадку вам потрібно відкрити квадратні дужки `[`, перерахуйте параметри Cookies які ви отримали в розділі `1) Отримайте параметри Cookies своїх акаунтів`, параметри cookie повинні бути в подвійних лапках `"` та розділеніх комами, коли ви завершите, не забудьте закрити квадратні дужки `]`.
  
![Adding Cookies for Multiple Accounts](/images/hoyolab/github-2.2.png)

###### Підтвердіть створення змінної
4. Натисніть кнопку **Add secret**, щоб додати змінну.
</details>

### 3) Налаштування автоматичного виконання в GitHub
<details>
  <summary>Інструкція</summary>

  Програма, буде самотушки виконуватися щодня о 06:00 (UTC+8)
  **Actions** -> **Hoyolab Automation**  -> **Run workflow**  -> **Run workflow**
  ![Adding Actions](/images/hoyolab/github-3.png)
</details>


#### Після цього винагороди збиратимуться автоматично