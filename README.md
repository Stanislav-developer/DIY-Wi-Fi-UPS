# DIY WiFi-UPS
## Джерело безперебійного живлення для WiFi роутерів та ONU терміналів

<!-- Коментар -->
<img src="/Photos/Image_1.JPG" alt="Main_Image" width="80%">

# Опис:
WiFi-UPS (ДБЖ для роутера) — це пристрій, який забезпечує безперебійне живлення для вашого Wi-Fi роутера та ONU-терміналу. Він складається з доступних компонентів і електронних модулів, що робить його простим для повторення. У цьому репозиторії описано будову та принцип роботи пристрою, наведено список необхідних компонентів і покрокову інструкцію зі збірки.

# Технічна інформація:
Особливістю цього безперебійника є безшовне перемикання на резервне живлення, тобто роутер не буде перезавантажуватися під час відключень електроенергії. Живлення безперебійника можливе як від блока живлення роутера (9–12 В, 600 мА–2 А), так і від стандартного блока живлення смартфона через USB Type-C (5 В, 1–3 А).
Пристрій має 2 входи та 2 виходи.
Характеристики вхідних портів:
• IN1 — розʼєм 5.5×2.1 мм, напруга від 6 до 20 В, струм до 3 А;
• IN2 — розʼєм USB Type-C, напруга 4.5–5.5 В, струм до 3 А.
Характеристики вихідних портів:
• OUT1, OUT2 — розʼєм 5.5×2.1 мм, напруга 9/12 В (за потреби може бути налаштована в діапазоні 5–25 В), струм до 1 А на порт.
Максимальна сумарна вихідна потужність на два порти становить 24 Вт.
Також на передній панелі розташовані індикатор заряду акумулятора та вимикач. Як елементи живлення використовуються 4 Li-Ion акумулятори формату 18650 з ємністю понад 1500 мА·год кожен.

# Характеристики у зручній таблиці:

| КАТЕГОРІЯ | ЗНАЧЕННЯ |
| :---: | :---: |
| Час автономної роботи | до 10 годин|
| Тип акумуляторів | Li-Ion 18650 |
| З'єднання елементів | 1s4p |
| Мін. ємність на комірку| 1500mAh |
| К-сть входів| 2 |
| К-сть виходів| 2 |
| Макс. потужність на 2 виходи| 24W |
| IN1 | 5-20 V (max 3A) |
| IN2 | 5V (max 3A) |
| OUT1 | 5/9/12V (max 1A) |
| OUT2 | 5/9/12V (max 1A) |

# Схема
<img src="Circuit_Image.png" alt="Circuit_Image" width="80%">

[Переглянути схему у повній якості](/Circuit_Image.png)

# Принцип роботи
1. Акумулятори під'єднані до плати BMS 1S 15A, ця плата виконує функцію захисту від перерозряду та короткого замикання. Чому обрана саме ця бмс? Тому що струм на вході підвищуючих перетворювачів MT3608 може сягати 6 Ампер і стандартна BMS 1S яка розрахована на 3A буде йти в захист.
2. До плати заряду IP2312 підєднаний понижуючий dc-dc перетворювач MINI360 призначений для конвертування напруги 9,12 вольт що поступає від блоку живлення роутеру у безпечні 5 вольт для плати заряду.
3. Функцію перемикання живлення від акумуляторів або від мережі виконують 2 діоди шотткі. VD1 пропускає напругу 5 вольт якщо присутня мережа, оскільки на цьому діоді більший потенціал то VD2 закритий і напруга з акумуляторів не поступає до підвищуючих перетворювачів та плата заряду безпечно їх заряджає. Якщо електроенергія у мережі зникає, потенціал на VD1 дорівнює 0 і VD2 відкривається та живлення на перетворювачі поступає від акумуляторів. Таким чином виходить система: Присутня мережа - живимо роутер та термінал від мережі та паралельно заряджаємо акумулятори. Мережа зникла - моментально перемикаємося на живлення від акумуляторів(роутер не перезавантажується).
4. Коли ми вмикаємо вимикач, струм паралельно поступає на 2 dc-dc підвищуючі модулі MT3608 та на індикатор заряду акумулятора. Таким чином ми вмикаємо безперебійник.
   
# Корпус

Корпус моделювався у програмі Fusion360, у папці [3D models](/3D%20Models/) розміщений файл проекту [f3z](/3D%20Models/V1.1%20(Latest)/Fusion%20file) та [STL](/3D%20Models/V1.1%20(Latest)/STLs) файли для друку. Файли рекомендовано використовувати з папки [V1.1(Latest)](/3D%20Models/V1.1%20(Latest)/) оскільки це остання версія де виправлені деякі дрібні недоліки.

---

<img src="3D Models/Renders/Image_1.png" alt="Circuit_Image" width="80%">
<img src="3D Models/Renders/Image_2.png" alt="Circuit_Image" width="80%">
<img src="3D Models/Renders/Image_3.png" alt="Circuit_Image" width="80%">
<img src="3D Models/Renders/Image_4.png" alt="Circuit_Image" width="80%">
<img src="3D Models/Renders/Image_5.png" alt="Circuit_Image" width="80%">
<img src="3D Models/Renders/Image_6.png" alt="Circuit_Image" width="80%">
<img src="3D Models/Renders/Image_7.png" alt="Circuit_Image" width="80%">
<img src="3D Models/Renders/Image_8.png" alt="Circuit_Image" width="80%">

Корпус проектувався модульно та складається з 5 частин:
1. Основний кейс
2. Передня панель
3. Задня панель
4. Кришка
5. Букви

Складання корпусу:
У основному кейсі є 4 отвори під гайки М3 та спеціальні пази з двох сторін у які вставляється передня та задня панелі, верхня кришка їх прижимає і закручується болтами M3x6 до основного кейсу, на верхню кришку ми наносимо суперклей у отвори під букви та закладаємо їх.

<img src="3D Models/Renders/Image_9.png" alt="Circuit_Image" width="80%">
<img src="3D Models/Renders/Image_10.png" alt="Circuit_Image" width="80%">

## [Файл Fusion f3z для редагування](/3D%20Models/V1.1%20(Latest)/Fusion%20file)
## [STL файли для друку](/3D%20Models/V1.1%20(Latest)/STLs)

# Необхідні компоненти для збірки

| НОМЕР | НАЗВА | КІЛЬКІСТЬ |
| :---: | :---: | :--: |
| 1 | [Холдер для 4-х акумуляторів 18650](https://www.rcscomponents.kiev.ua/product/korpus-dlia-4x18650-gt-18650-pc8_179556.html) | 1шт |
| 2 | [Підвищуючий dc-dc перетворювач MT3608](https://www.rcscomponents.kiev.ua/product/rehulovanyi-dc-dc-step-up-modul-zhyvlennia-mt3608_123033.html) | 2шт |
| 3 | [Плата заряду IP2312](https://www.rcscomponents.kiev.ua/product/modul-zariadnyi-type-c-dlia-18650-1s-3a-4-2v_188209.html) | 1шт |
| 4 | [Понижувальний dc-dc модуль MINI360](https://www.rcscomponents.kiev.ua/product/dc-dc-ponyzhuiuchyi-peretvoriuvach-z-rehuliuvanniam-mini-360-vkhid-4-75v-23v-vykhid-1-0v-17v-2a_200045.html) | 1шт |
| 5 | [Плата BMS 1S 15A](https://myproject.com.ua/bms-6mos-modul-zakhystu-dlia-li-ion-akumuliatora-1s.html) | 1шт |
| 6 | [Індикатор заряду для 1s Li-Ion](https://www.rcscomponents.kiev.ua/product/indykator-zariadu-litiievoi-batarei-1s-synii_211004.html) | 1шт |
| 7 | [DC гніздо 5.5x2.1mm](https://www.rcscomponents.kiev.ua/product/hnizdo-zhyvlennia-chorne-na-korpus-5-5x2-1mm-dc-022b_213085.html) | 3шт |
| 8 | [DC штекер 5.5x2.1mm](https://www.rcscomponents.kiev.ua/product/shteker-na-kabel-2-1-5-5-korotkyi-pc-2-1-5-5-vylka-zhyvlennia-dc-mama-z-korpusom-2-1-5-5-mm-dovzhyna-9mm_25189.html) | 4шт |
| 9 | [Вимикач KCD-11](https://www.rcscomponents.kiev.ua/product/kcd-11-on-off-spst-2p-vymykaie-0-vmykaie-peremykach-klavishnyi-rocker-global-tone_211814.html) | 1шт |
| 10 | [TypeC плата адаптер](https://myproject.com.ua/usb31-type-c-plata-perekhidnyk.html) | 1шт |
| 11 | [Діоди Шотткі 1N5820/SR540](https://www.rcscomponents.kiev.ua/product/sr540_20328.html) | 2шт |
| 12 | [Макетна плата (необов'язково)](https://www.rcscomponents.kiev.ua/product/maketna-plata-2x8-dvostoronnia-zelena_144385.html) | 1шт |
| 13 | [Силіконовий термостійкий кабель 20AWG](https://www.rcscomponents.kiev.ua/product/sylikonovyi-provid-20awg-0-5mm-100-0-08ts-korychnevyi_210526.html) | 3м |
| 14 | [Болти M3x6](https://www.rcscomponents.kiev.ua/product/hvynt-iz-sferychnoiu-holovkoiu-m3x6-nerzhaviiucha-stal-304-ph-din-7985_194111.html) | 12шт |
| 15 | [Гайки М3](https://www.rcscomponents.kiev.ua/product/haika-m3-otsynk-bila-din934-b3-bn117_26436.html) | 4шт |
| 16 | Акумулятори 18650 ємністю > 1500mAh | 4шт |
| 17 | Роздрукований корпус | 1шт |
