# Otus. Linux Basic

## 3. Bash. Написание простых скриптов

Вот все примеры кода из урока, которые ты показывал студентам. Их можно оформить в репозиторий на GitHub. 🚀

---

### 1. Первый Bash-скрипт

```bash
#!/bin/bash
echo "Привет, Bash!"

📌 Запуск:

chmod +x script.sh
./script.s
```

---

### 2. Работа с переменными

```bash
#!/bin/bash
name="Анна"
echo "Привет, $name!"
```

📌 Ввод от пользователя:

```bash
read -p "Введите имя: " username
echo "Добро пожаловать, $username!"
```

---

### 3. Аргументы командной строки

```bash
#!/bin/bash
echo "Привет, $1!"
```

📌 Запуск:

```sh
./script.sh Алексей
```

---

### 4. Проверка аргументов

```bash
#!/bin/bash
if [ -z "$1" ]; then
    echo "Ошибка: не передан аргумент"
    exit 1
fi
echo "Передан аргумент: $1"
```

---

### 5. Условные конструкции (if, case)

```bash
#!/bin/bash
if [ "$1" == "start" ]; then
    echo "Запуск..."
elif [ "$1" == "stop" ]; then
    echo "Остановка..."
else
    echo "Неизвестная команда"
fi
```

📌 Альтернатива с case:

```bash
#!/bin/bash
case "$1" in
    start) echo "Запуск...";;
    stop) echo "Остановка...";;
    *) echo "Неизвестная команда";;
esac
```

---

### 6. Циклы (for, while)

📌 Цикл for (перебор значений):

```bash
#!/bin/bash
for name in Анна Алексей Иван; do
    echo "Привет, $name!"
done
```

📌 Цикл while (пока условие истинно):

```bash
#!/bin/bash
count=1
while [ "$count" -le 5 ]; do
    echo "Счётчик: $count"
    ((count++))
done
```

---

### 7. Работа с файлами и директориями

📌 Проверка существования файла:

```bash
#!/bin/bash
if [ -e "file.txt" ]; then
    echo "Файл существует!"
else
    echo "Файл НЕ существует!"
fi
```

📌 Удаление файлов (.bak, .tmp, .backup)

```bash
#!/bin/bash
for ext in bak tmp backup; do
    for file in *.$ext; do
        [ -e "$file" ] && echo "Удаляю: $file" && rm "$file"
    done
done
```

---

### 8. Работа с конфигурационными файлами

📌 Чтение resolv.conf

```bash
cat /etc/resolv.conf
```

📌 Изменение resolv.conf (sed)

```bash
sed -i '' 's/nameserver .*/nameserver 8.8.8.8/' resolv.conf
```

📌 Безопасное изменение с бэкапом:

```bash
cp resolv.conf resolv.conf.bak
sed -i '' 's/nameserver .*/nameserver 8.8.8.8/' resolv.conf
```

---

### 9. Итоговый мини-проект: Очистка временных файлов

```bash
#!/bin/bash

if [ -z "$1" ]; then
    echo "Ошибка: не указана директория"
    exit 1
fi

if [ ! -d "$1" ]; then
    echo "Ошибка: директория не существует"
    exit 2
fi

for ext in bak tmp backup; do
    for file in "$1"/*.$ext; do
        [ -e "$file" ] && echo "Удаляю: $file" && rm "$file"
    done
done

echo "Очистка завершена!"
```

📌 Запуск:

```bash
./clean_temp.sh /путь/к/папке
```

---
