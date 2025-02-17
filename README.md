<img src="https://avatars.githubusercontent.com/u/176747543?s=200&v=4" width="180" height="180">

# Gamemode Developing Guidelines &middot;

- [Git](#git)
  - [Основные правила](#main-git-rules)
  - [Культура коммитов](#commit-git-rules)
- [Документация](#docs)
- [Окружения](#env)
- [Правила оформления кода](#code-style)
  - [Именование элементов данных](#element-code-style)
  - [Стилистика](#stylistics-code-style)
  - [Тернарные операторы](#ifelse-code-style)
  - [Общее](#general-code-style)
- [Структура проекта](#structure)
  - [Модули](#module-structure)

<a name="git"></a>
## 1. Git

![Git](https://github.com/elsewhencode/project-guidelines/raw/master/images/branching.png)

<a name="main-git-rules"></a>
### 1.1 Основные правила

Здесь содержатся основные правила работы с Git-репозиторием, которые Вы всегда должны учитывать.

- Работайте в отдельной выделенной ветке под конкретную фичу (каждая ветка индивидуальна для разработчика)

_Почему?_
> Работу нужно осуществлять в изолированной, а не в master или develop ветке. Это позволит Вам избежать нежелательных конфликтов при работе с проектом. Вы сможете делать коммиты не опасаясь испортить главную ветку нестабильным или незавершенным кодом.


- Ответвляйтесь от Вашей feature ветки

_Почему?_
> По нашим правилам, все pull requests осуществляются в develop ветку. Ответвление от develop в feature ветку с последующим суб-ответвлением позволит Вам разрабатывать функционал без опасений конфликтов с другими разработчиками.


- Устраняйте конфликты перед осуществлением pull request

_Почему?_
> Устранение потенциальных конфликтов с другими ветками во время разработки позволит сократить временные затраты на оценку и исправление Вашей версии кода экспертом.


- Используйте `.gitignore` из репозитория с модом

_Почему?_
> Это позволит Вам избежать мусорных файлов внутри репозитория и избежать засорения структуры проекта.

<a name="commit-git-rules"></a>
### 1.2 Культура коммитов

- Используйте английский язык для заголовка коммита и русский для его описания

_Почему?_
> Специфика работы Github даёт некоторые преимущества в отображении английского языка и его использование позволит соблюдать чистоту в репозитории.


- Первая буква в заголовке коммита должна быть заглавной

_Почему?_
> В соответствии с правилами грамматики первое слово предложения начинается с заглавной буквы.


- Сокращайте заголовок до 50 символов и подробно описывайте Description

_Почему?_
> Хороший коммит содержит предельно краткую и понятную тему и исчерпывающее описание. Используйте description для дополнительного описания.


- Избегайте точек в конце заголовка коммита

_Почему?_
> Это моветон :)


- Используйте повелительное наклонение в заголовке коммита

_Почему?_
> Повелительное наклонение позволяет описать, что конкретно делают внесенные изменения и их результат.


- Избегайте пустых заголовков или заголовков без контектста

_Почему?_
> Коммиты по типу `fix` легко запутают команду разработчиков и являются наиболее дурным тоном в разработке.

<a name="docs"></a>
## 2. Документация

Исчерпывающая документация хоть и является маловажной в Agile методологии разработки, но отсутствие документации вовсе уничтожит проект.
Пишите минимально возможную документацию для функций, модулей и иного, это поможет всей команде в дальнейшем.

* Будет дополняться


<a name="env"></a>
## 3. Окружения

Удобно настроенная IDE - залог успеха! Используйте папку `.vscode` из репозитория с модом для настройки Вашей Visual Studio Code. 

- Установите для себя границу символов (ее можно включить для отображения в  VS Code) и переносите строки, чтобы не тянуться постоянно курсором до нужного места, находящегося за пределами видимой области кода. Идеальное значение для предела: 80-100 символов.

    ```pawn
         new const fireObjectId = CreateDynamicObject(
 	                19632, 1000.0, 1000.0, 1000.0, 0.0, 0.0, 0.0, -1, -1, -1, 300.0, 300.0);
    ```


<a name="code-style"></a>
## 4. Правила оформления кода

<a name="element-code-style"></a>
### 4.1 Именование элементов данных

- Название переменных задаются в стиле `camelCase`, где первая буква первого слова является прописной, а все остальные слова начинаются с заглавной буквы. Например: `playerVariable`.
- Названия функций пишутся в стиле `PascalCase`: первая буква во всех словах - заглавная. Например: `GetMaxPlayersCount`
- Названия переменных и функций, хранящих или возвращающих булевое (логическое) значение (`true`/`false` или `0`/`1`) должны иметь префикс `is`/`has`. Например:

    ```pawn
      new const bool:isTuesday = (GetCurrentWeekDay() == WEEK_DAY_TUESDAY);

       stock IsPlayerLoggedIn(playerId)
       {
       	return (
       		IsPlayerConnected(playerid) && 
       		g_playerLoginStatus[playerid] == PLAYER_LOGIN_STATUS_LOGGED_IN
       	);
       } 
    ```

- Названия функций, нацеленных на получение данных должны начинаться с префикса `Get`. Функции, нацеленные на изменение данных - `Set`: `GetPlayerMoney`, `SetPlayerMoney`
- Названия констант (в том числе препроцессорных определением (`#define`) пишутся в стиле `SCREAMING_SNAKE_CASE`: `MAX_PLAYERS`, `MAX_VEHICLES` и пр. Исключения составляют переменные, объявленные в локальной области видимости, которым не разрешено изменять свое значение по логике программы.

  ```pawn
       #define MAX_PLAYER_NAME 24
       // или
       new const MAX_PLAYER_NAME = 24;
      
       
       public OnPlayerConnect(playerid)
       {
       	new playerName[(MAX_PLAYER_NAME + 1)];
       	GetPlayerName(playerid, playerName, sizeof (playerName));
       
       	// Значение переменной `accountId` не может быть изменено в ходе работы кода
       	new const accountId = GetAccountIdByName(playerName);
       	if (accountId != 0)
       	{
       		// ...
       	}
       }
  ```

- Название переменной должно полностью отражать смысл хранимых данных в ней. Например:

  ```pawn
     // Храним в переменной количество денег у игрока
     new g_playerMoney[MAX_PLAYERS];
  ```

- В начале названия обычной или статической переменной в глобальной области видимости должен стоять префикс: `g_` или `s_` соответственно. Например:

  ```pawn
     enum E_PLAYER_DATA
     {
     	// ...
     };
     new g_playerData[MAX_PLAYERS][E_PLAYER_DATA];
     static s_resetPlayerData[E_PLAYER_DATA];
    
     // Пример использования `s_resetPlayerData` для обнуления значений второй ячейки массива в `g_playerData`
     public OnPlayerConnect(playerid)
     {
     	g_playerData[playerid] = s_resetPlayerData;
     }
  ```

- Используйте стиль `SCREAMING_SNAKE_CASE` для названия перечислителя и его элементов. Если перечислитель будет использоваться для заполнения ячейки массива, используйте префикс `E_` для самого перечислителя и его элементов:

  ```pawn
     enum WORK_TYPE
     {
     	WORK_TYPE_CAB_DRIVER,
     	WORK_TYPE_BUS_DRIVER,
     	// ...
     };
    
     enum GENDER_TYPE
     {
     	GENDER_FEMALE,
     	GENDER_MALE,
     };
    
     enum E_PLAYER_DATA
     {
     	E_PLAYER_NAME[MAX_PLAYER_NAME + 1],
     	GENDER_TYPE:E_PLAYER_GENDER,
     };
  ```


<a name="stylistics-code-style"></a>
### 4.2 Стилистика

- Переносите фигурные скобки, открывающие тело блока на следующую строку. В больших конструкциях этот способ поможет избежать путаницы в чтении соседних строк. Согласитесь, читать подобный код куда приятнее:

  ```pawn
     // Неправильно
     stock MyNewFunction(arg1, arg2, arg3, arg4) {
     	if ((arg > 0 && (arg2 + arg3) > 0 && arg4 != 0) || MySomeFunction() > MY_CONSTANT) {
     		// А теперь представьте что тут начинается спагетти-код, используя подобный перенос
     		// ...
     	}
     	return 1;
     }
    
     // Правильно
     stock MyNewFunction(arg1, arg2, arg3, arg4)
     {
     	if (
     		(arg > 0 && (arg2 + arg3) > 0 && arg4 != 0) || 
     		MySomeFunction() > MY_CONSTANT
     	) {
     		// ...
     	}
     	return 1;
     }
  ```

- Используйте пробел для операторов (кроме скобок), перечисления аргументов и параметров функций
- Арифметические операции должны оборачиваться в операторы приоритета (скобки `(`, `)`) для большей читаемости кода. Продвинутые редакторы кода обладают подсветкой пар скобок:

  ```pawn
     // Из этой строки сразу ясно, что сперва мы получаем разницу в секундах, а
     // затем делим полученное значение на 3600, чтобы получить количество часов
     new const differentTimeHours = ((g_lastTickCheckTime - gettime()) / 3600);
  ```

- По возможности, используйте тэги в возвращаемых значениях своих функций и в переменных. В особенности для сущностей (бизнес, дом, личное авто и прочее). Это позволит обеспечить целостность передаваемых данных:

  ```pawn
     #define INVALID_MY_VEHICLE_ID (Vehicle:0)
 
     stock Vehicle:CreateMyVehicle(model, Float: posX, Float: posY, Float: posZ)
     {
     	// ...
    
     	// Для примера
     	return (Vehicle: 1);
     }
    
     stock DeleteMyVehicle(Vehicle:vehicle)
     {
     	// ...
     }
  ```

- Не используйте магические числа в своем коде. Под магическими числами понимаются любые значения, которые в будущем могут измениться в коде, особенно те, которые могут использоваться повсеместно в больших количествах. Вместо этого объявляйте константы - это значительно упростит вам жизнь при изменении необходимых данных:

  ```pawn
    #define MAX_PLAYERS 1000
    new const MAX_PLAYER_OWNED_VEHICLES = 3;
  ```

- Оставляйте запятую у последнего элемента перечислителя (`enum`). Это позволит немного сократить необходимые действия при добавлении новых элементов, улучшит вид истории изменений в системе контроля версий (`git`) и позволит избежать возможных конфликтов при слиянии веток:

  ```pawn
     enum E_PLAYER_DATA
     {
     	E_PLAYER_NAME[MAX_PLAYER_NAME],
     	E_PLAYER_IP[MAX_IP_LEN + 1],
     	Float: E_PLAYER_HEALTH,
     	Float: E_PLAYER_ARMOUR,
     };
  ```

<a name="ifelse-code-style"></a>
### 4.3 Тернарные операторы

- Если вам нужно вывести одно из двух значений, вы можете использовать тернарный оператор, который является сокращенной версией конструкции `if`-`else`: (`(condition) ? true value : false value`). Например:

    ```pawn
      new string[MAX_CHAT_MSG_LEN + 1];
      format(
      	string, sizeof (string),
      	"Игрок %sподключен!",
      	(IsPlayerConnected(targetId) ? "" : "не ")
      );
      SendClientMessage(playerid, 0xFF0000FF, string);
    ```

- Переносите строки, если конструкция тернарного оператора оказалось слишком длинной и не вмещается в одну строку до границы переноса. Так же, оборачивайте условие в оператор приоритета (скобки `(`, `)`):

    ```pawn
      format(
     	string, sizeof (string),
     	"Количество денег у игрока равняется $%d!",
     	(
     		(justVeryLongNameOfVariableForExample)
     			? g_playerData[targetId][E_PLAYER_BANK_MONEY]
     			: g_playerData[targetId][E_PLAYER_MONEY]
     	)
     );
    ```

- Не злоупотребляйте тернарным оператором, не создавайте из него цепочку условий, вместо этого воспользуйтесь операторами `if`, `else if` и `else`, `switch` или массивы, там где это возможно:

  ```pawn
     // Неправильно
     SendClientMessage(playerid, -1, playerData[playerid][pAdmin] == 1 ? "Admin lvl 1" : playerData[playerid][pAdmin] == 2 ? "Admin lvl 2" : playerData[playerid][pAdmin] == 3 ? "Admin lvl 3" : "Admin lvl 4");
  ```

<a name="general-code-style"></a>
### 4.4 Общее

- Не злоупотребляйте конструкциями `if`-`else` или `switch` для написания большого количества кода. В некоторых случаях вместо этого можно использовать массивы:

  ```pawn
     // Неправильно
     switch (type)
     {
     	case 1: ApplyAnimation(playerid, "PED", "WOMAN_IDLESTANCE", 4.0, 1, 0, 0, 0, 0);
     	case 2: ApplyAnimation(playerid, "PED", "CAR_HOOKERTALK", 4.0, 1, 0, 0, 0, 0);
     	case 3: ApplyAnimation(playerid, "FAT", "FatIdle", 4.0, 1, 0, 0, 0, 0);
     	case 4: ApplyAnimation(playerid, "WUZI", "Wuzi_Stand_Loop", 4.0, 1, 0, 0, 0, 0);
     	case 5: ApplyAnimation(playerid, "GRAVEYARD", "mrnm_loop", 4.0, 1, 0, 0, 0, 0);
     	case 6: ApplyAnimation(playerid, "GRAVEYARD", "prst_loopa", 4.0, 1, 0, 0, 0, 0);
     	case 7: ApplyAnimation(playerid, "PED", "idlestance_fat", 4.0, 1, 0, 0, 0, 0);
     	case 8: ApplyAnimation(playerid, "PED", "idlestance_old", 4.0, 1, 0, 0, 0, 0);
     	case 9: ApplyAnimation(playerid, "PED", "turn_l", 4.0, 1, 0, 0, 0, 0);
     	case 10: ApplyAnimation(playerid, "BAR", "Barcustom_loop", 4.0, 1, 0, 0, 0, 0);
     	case 11: ApplyAnimation(playerid, "BAR", "Barserve_loop", 4.0, 1, 0, 0, 0, 0);
     }
    
     // Правильно
     static const WALK_ANIMATION[10][][] =
     {
     	{ "PED", "WOMAN_IDLESTANCE" },
     	{ "PED", "CAR_HOOKERTALK" },
     	{ "FAT", "FatIdle" },
     	{ "WUZI", "Wuzi_Stand_Loop" },
     	{ "GRAVEYARD", "mrnm_loop" },
     	{ "GRAVEYARD", "prst_loopa" },
     	{ "PED", "idlestance_fat" },
     	{ "PED", "idlestance_old" },
     	{ "PED", "turn_l" },
     	{ "BAR", "Barcustom_loop" },
     	{ "BAR", "Barserve_loop" }
     };
     new const walkAnimIndex = ((type - 1) % sizeof (WALK_ANIMATION));
     ApplyAnimation(
     	playerid,
     	WALK_ANIMATION[walkAnimIndex][0],
     	WALK_ANIMATION[walkAnimIndex][1],
     	4.0, 1, 0, 0, 0, 0
     );
  ```

- Не забывайте про валидацию: всегда проверяйте на доступность ячеек массива во избежание выходов за пределы массива; выводите игроку об ошибке, которая произошла в момент работы сервера.
- Логируйте ошибки, связанные с внутренней работой сервера: ошибки при выполнениях запросов к базе данных, чтение файлов и т.п.
- Используйте статические константы там, где это необходимо. В отличии от обычных переменных и констант (объявленных через `new`), статические константы не выгружаются из памяти после завершения работы блока кода. Например, Вы можете использовать динамический подсчет символов в строках для их форматирования:

  ```pawn
     static const FORMAT_STR_TEXT[] = "Вы подкинули монетку Вам выпал%s";
     static const STR_COIN[2][(8 + 1)] = { ": орел", "а: решка" };
     new text[sizeof (FORMAT_STR_TEXT) + (sizeof STR_COIN[] + -2) + 1];
     format(text, sizeof (text), FORMAT_STR_TEXT, STR_COIN[random(sizeof (STR_COIN))]);
     SendClientMessage(playerid, -1, text);
  ```

- Используйте препроцессорные определения (константы) в проверках и строках по небходимости. Использование их в строках может облегчить Вам разработку, избегая излишнего форматирования:

  ```pawn
     #define MIN_PLAYER_NAME 3
     #define MAX_PLAYER_NAME 24
     
     cmd:setname(playerid, params[])
     {
     	if (!(MIN_PLAYER_NAME <= strlen(params) <= MAX_PLAYER_NAME))
     	{
     		SendClientMessage(
     			playerid, -1,
     			"Длина имени от "#MIN_PLAYER_NAME" до "#MAX_PLAYER_NAME" символов!"
     		);
     		return 0;
     	}
    
     	return SetPlayerName(playerid, params);
     }
  ```

- Для пояснения, ключевое # перед названием препроцессорного определения позволяет сконвертировать значение в строку. Обращая внимания на предыдущий пункт: Избавьтесь от оборачивания значений препроцессорных определений в скобок. Это сделает конвертацию определения в строку (с помощью #) невозможным.

  ```pawn
     // Неправильно
     #define MAX_PLAYER_NAME (24)
     // Правильно
     #define MAX_PLAYER_NAME 24
  ```

<a name="structure"></a>
## 5. Структура проекта

<a name="module-structure"></a>
### 5.1 Модули

Типичный модуль состоит из ряда обязательных и опциональных файлов. Ниже приведена структура примерного модуля:

  ```
  .
  └── module_folder
      ├── hooks.pwn          # Здесь подключаем y_hooks и хукаем все подряд: паблики, нативки и даже стоки.
      ├── dialogs.pwn        # Здесь обрабатываем все диалоги (Dialog_Response:: от mdialog) и подобное.
      ├── commands.pwn       # Здесь храним все команды модуля.
      ├── module_name.pwn    # Главный файл, куда подключаются все файлы из папки с модулем.
      ├── functions.pwn      # Здесь находятся все функции модуля.
      ├── timers.pwn         # Здесь храним и обрабатываем все таймеры.
      └── vars.inc           # Здесь храним все переменные, константы, enum и прочее связанное с данными.
  ```

- Максимально изолируйте модуль от остальных систем мода.
- Именуйте функции модуля в формате `ModuleName_SomeFunc`.
- Не стесняйтесь использовать `inline`-функции от `y_inline`. Это полезно и удобно!
