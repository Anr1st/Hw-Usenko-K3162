# Hw-Usenko-K3162
Домашняя работа Усенко Елизавета Валерьевна K3162, Информ 1 K24 1.2

# Лабораторная работа: "Работа с командой grep: поиск и фильтрация данных"
## Тема: команда grep

Описание: 

  1. Цель работы:
     Изучить работу с утилитой grep для поиска текстовой информации в файлах, а также применение регулярных выражений для фильтрации данных.
     
  3. Ссылки на материалы:
     
     https://www.google.ru/

     https://www.gnu.org/software/grep/manual/grep.html

     https://losst.pro/gerp-poisk-vnutri-fajlov-v-linux
     
# Ход работы (не включается в отчет по работе)

## Шаг №1. Подготовка рабочей среды.

  1. Создайте тестовый файл:
 ```
 echo -e "Linux is great.\nLearning grep is useful.\nGrep helps find text in files.\n" > testfile.txt
 ```

## Шаг №2. Поиск строки.

  1. Поиск строки с ключевым словом "grep":
 ```
  grep "grep" testfile.txt
 ```

 2. Результат:
 ```
 Learning grep is useful.
 Grep helps find text in files.
 ```

# Задание

## Часть 1.

  - Создать текстовый файл со следующими данными:
```
2024-12-25 10:00:01 INFO: Connection from 192.168.0.1
2024-12-25 10:05:12 ERROR: Failed to connect to 10.0.0.5
2024-12-25 10:10:34 INFO: User 192.168.1.5 logged in
2024-12-25 10:15:44 WARNING: Low disk space
2024-12-25 10:20:00 ERROR: Timeout while connecting to 172.16.0.3
```
  - Использовать grep для:
      1. Поиска строк, содержащих IP-адреса,
      2. Вывода всех строк, кроме содержащих слово "error" без учета регистра,
      3. Поиска строк, начинающихся с определенной даты, дата должна быть подсвечена,
      4. Поиска строк, содержащих слово "INFO" или "WARNING" с указанием номера строки.
         
## Часть 2.

  - Создать Bash скрипт, который:
      1. Принимает ключевые слова от пользователя,
      2. Использует grep для поиска по указанному файлу,
      3. Записывает найденные строки в новый файл.

# Решения задания.

# Часть 1.
 1. Срздание файла:
```
echo -e  "2024-12-25 10:00:01 INFO: Connection from 192.168.0.1\n2024-12-25 10:05:12 ERROR: Failed to connect to 10.0.0.5\n2024-12-25 10:10:34 INFO: User 192.168.1.5 logged in\n2024-12-25 10:15:44 WARNING: Low disk space\n2024-12-25 10:20:00 ERROR: Timeout while connecting to 172.16.0.3" > logs.txt
```
 2. Поиск строк, содержащих IP-адреса:
```
grep -E "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" logs.txt
```
 3. Вывод всех строк, кроме содержащих слово "error" без учета регистра:
```
grep -vi "error" logs.txt
```
 4. Поиск строк, начинающихся с определенной даты:
```
grep "^2024-12-25" logs.txt
``` 
 5. Поиск строк, содержащих слово "INFO" или "WARNING" с указанием номера строки:
```
grep -n -E "INFO|WARNING" logs.txt
```

# Часть 2.
1. Bash скрипт:
```
#!/bin/bash

# Проверяем, передан ли путь к файлу
if [ -z "$1" ]; then
    echo "Ошибка: Укажите путь к файлу для поиска."
    exit 1
fi

# Проверяем, существует ли файл
if [ ! -f "$1" ]; then
    echo "Ошибка: Файл не существует."
    exit 1
fi

# Принимаем ключевое слово от пользователя
echo "Введите ключевое слово для поиска:"
read keyword

# Проверяем, введено ли ключевое слово
if [ -z "$keyword" ]; then
    echo "Ошибка: Не указано ключевое слово для поиска."
    exit 1
fi

# Запрашиваем имя файла для сохранения результатов
echo "Введите имя файла для сохранения результатов:"
read output_file

# Используем grep для поиска по файлу и записываем результат в новый файл
grep "$keyword" "$1" > "$output_file"

echo "Поиск завершен. Результаты сохранены в файл: $output_file"
```
2. Передача прав файлу на исполнение (пусть файл называется search_script.sh, например):
```
cnmod +x search_script.sh
```
3. Запуск скрипта с передачей ему пути к файлу для поиска (пусть он называется results.txt, например):
```
./search_script.sh results.txt
```
