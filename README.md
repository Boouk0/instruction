# instruction
# 🚀 GigaChat Survival Kit (Терминал, без браузера)

Инструкция для развертывания, использования и очистки GigaChat на чужом ПК (Windows, PowerShell).

## 📌 Что нужно знать перед началом
1. Ссылка на файл с ключом: https://raw.githubusercontent.com/Boouk0/my_gigachat_project/main/gigachat_key.txt
2. Твой PAT от GitHub (если репозиторий приватный).
3. На компьютере должен быть установлен Python.

---

## 🛠️ Шаг 1: Подготовка ключа и скачивание кода

Открой PowerShell (обычный, не от администратора).

1.1. Скачиваем ключ в память (не на диск!):
Замени ТВОЙ_PAT на свой токен. (Если репозиторий публичный, удали часть -Headers @{Authorization="token ТВОЙ_PAT"})

$env:GIGACHAT_API_KEY = Invoke-RestMethod -Uri "https://raw.githubusercontent.com/Boouk0/my_gigachat_project/main/gigachat_key.txt" -Headers @{Authorization="token ТВОЙ_PAT"}

1.2. Скачиваем скрипты из репозитория (чтобы не писать их руками):
Выполни эти две команды, чтобы сохранить файлы chat.py и chat_loop.py на компьютер:

Invoke-RestMethod -Uri "https://raw.githubusercontent.com/Boouk0/my_gigachat_project/main/chat.py" -OutFile "chat.py"
Invoke-RestMethod -Uri "https://raw.githubusercontent.com/Boouk0/my_gigachat_project/main/chat_loop.py" -OutFile "chat_loop.py"

---

## ⚙️ Шаг 2: Установка библиотеки

Выполни в терминале:
pip install gigachat
(Если pip ругается на права доступа: pip install --user gigachat)

⚠️ Если PyPI заблокирован (нет интернета к Python):
В репозитории есть папка wheels с файлами библиотеки. Установи её локально:
pip install --no-index --find-links=./wheels gigachat

---

## 🤖 Шаг 3: Запуск и работа

Как включить (Запуск):
python chat_loop.py
Появится приглашение "Вы: ". Пиши свой вопрос и жми Enter.

Как выключить (Выход):
В окне чата напиши exit (или выход) и нажми Enter. Либо нажми Ctrl + C.

Как использовать Pro/Ultra модели:
По умолчанию используется GigaChat-2. Чтобы переключиться на мощную модель для кода, открой chat_loop.py блокнотом (notepad chat_loop.py) и измени строку:
with GigaChat(model="GigaChat-2-Pro") as client:
Доступные модели: GigaChat-2, GigaChat-2-Pro, GigaChat-2-Max, GigaChat-3-Ultra.

Как спросить один раз (без входа в чат):
python chat.py "Напиши функцию на Python для сортировки списка"

---

## 🚨 Решение проблем (Troubleshooting)

1. Ошибка SSL (CERTIFICATE_VERIFY_FAILED)
Отключи проверку сертификатов в текущем сеансе:
$env:GIGACHAT_VERIFY_SSL_CERTS="false"
После этого запусти python chat_loop.py заново.

2. Кракозябры вместо русских букв
Выполни chcp 65001 перед запуском.

3. Ошибка Illegal header value
Убедись, что ты скачал скрипты из этого репозитория (они используют правильный метод авторизации).

---

## 🧹 Шаг 4: Очистка следов (ОБЯЗАТЕЛЬНО)

1. Очисти историю команд PowerShell:
Clear-Content (Get-PSReadLineOption).HistorySavePath

2. Очисти «Диспетчер учетных данных» Windows:
Нажми Win, начни вводить «Диспетчер учетных данных», открой его.
Выбери «Учетные данные Windows».
Найди и удали всё, что связано с github.com или git:.

3. Удали временные файлы:
Remove-Item chat.py, chat_loop.py -Force
(Если папка wheels скачивалась, удали и её: Remove-Item -Recurse -Force wheels)

4. Удали библиотеку (опционально):
pip uninstall gigachat -y

---

## 🔒 Действия после возвращения
1. Отзови (Revoke) свой PAT на GitHub.
2. Пересоздай ключ GigaChat в личном кабинете Sber Studio.
3. Удали файл gigachat_key.txt из репозитория (git rm gigachat_key.txt, затем commit и push).



Инструкция V2
# 1. Создать папку и зайти в нее
mkdir gigachat_work
cd gigachat_work

# 2. Скачать скрипты (замени ТВОЙ_PAT в двух местах!)
Invoke-RestMethod -Uri "https://raw.githubusercontent.com/Boouk0/my_gigachat_project/main/chat.py" -Headers @{Authorization="token ТВОЙ_PAT"} -OutFile "chat.py"
Invoke-RestMethod -Uri "https://raw.githubusercontent.com/Boouk0/my_gigachat_project/main/chat_loop.py" -Headers @{Authorization="token ТВОЙ_PAT"} -OutFile "chat_loop.py"

# 3. Скачать ключ в память (замени ТВОЙ_PAT!)
$env:GIGACHAT_API_KEY = Invoke-RestMethod -Uri "https://raw.githubusercontent.com/Boouk0/my_gigachat_project/main/gigachat_key.txt" -Headers @{Authorization="token ТВОЙ_PAT"}

# 4. Установить библиотеку (если нет интернета, см. README про папку wheels)
pip install gigachat

# 5. Запустить нейросеть!
python chat_loop.py
