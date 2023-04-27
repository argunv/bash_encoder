Документация по использованию скрипта script.sh
Этот скрипт позволяет зашифровать содержимое файла в кодировку 
шестнадцатеричных символов и записать его в новый .sh файл.

Использование
Для использования скрипта необходимо выполнить следующие действия:

Откройте терминал и перейдите в каталог, содержащий файл, содержимое 
которого вы хотите зашифровать.

Важно! Если в вашем скрипте есть строка "!/bin/bash", её необходимо удалить.

Запустите скрипт, передав в качестве аргумента путь к файлу, который нужно 
зашифровать, например: ./script.sh /path/to/file.sh.

Если аргумент не был передан, то скрипт выводит сообщение об использовании 
скрипта и завершает работу.

В переменную code_hex записывается результат выполнения команды xxd, 
которая конвертирует файл в кодировку шестнадцатеричных символов с 
использованием опции -p и выводит результат в стандартный вывод. Опция -c 
10000 позволяет указать максимальное количество символов в строке. Команда 
sed заменяет каждые два символа в выводе на \x и добавляет их в переменную 
code_hex.

Создается новый .sh файл с расширением .enc.sh, в который записывается код 
для декодирования переменной code_hex.

При помощи команды sed в строке code_bytes=$(echo $code_hex | sed 
's/\\\\x//g' | xxd -r -p) удаляются символы \x из переменной code_hex, 
после чего переменная code_bytes получает декодированное содержимое файла 
в бинарном виде.

Команда tr удаляет из переменной code_bytes все символы новой строки.

В строке eval $code_str переменная code_str содержит раскодированную 
строку, которая выполняется при помощи eval.

Выводится сообщение о том, что зашифрованный скрипт сохранен в новом 
файле.
