# PythonLinux_HW04
# Автоматизация тестирования консольных приложений Linux на Python (семинары)
Урок 4. Реализации автодеплоя и тестов по SSH
Данное задание является промежуточной аттестацией.

Задание 1.

Условие:
Переделать все шаги позитивных тестов на выполнение по SSH. Проверить работу.

Задание 2. (дополнительное задание)

Условие:
Переделать все шаги негативных тестов на выполнение по SSH. Проверить работу.

Конфигурационный файл config.yaml содержит информацию о хосте, пользователе, пароле и других параметрах, необходимых для соединения с удаленным сервером.

conftest.py:

Функция create_deploy: Загружает файл {folder_in}/{file}.deb на удаленный сервер, устанавливает его с помощью команды dpkg -i, и проверяет статус установки.
Функция make_folders: Создает необходимые папки на удаленном сервере.
Функция delete_folders: Удаление папок на удаленном сервере после завершения тестов.
Функция make_files: Создает случайные файлы на удаленном сервере в папке {folder_user_in}.
Функция delete_deploy: Удаляет файл {file} с удаленного сервера с помощью команды dpkg -r.
sshcheckers.py:

Функция ssh_checkout: Устанавливает SSH-соединение с удаленным сервером, выполняет заданную команду cmd с использованием указанных учетных данных (host, user, passwd), и проверяет, содержится ли указанный текст text в выводе команды. Возвращает True, если команда выполняется успешно и содержит указанный текст, иначе возвращает False.
Функция upload_files: Загружает файл с локальной машины (local_path) на удаленный сервер (remote_path) с использованием указанных учетных данных (host, user, passwd).
Функция ssh_checkout_negative: Аналогична функции ssh_checkout, но возвращает True, если выполнение команды завершается неуспешно, и содержит указанный текст text, иначе возвращает False.
test_deploy.py:

Тестовый класс TestHW с двумя тестовыми методами:
Тест test_step_1: Создает архив типа {type} с использованием команды 7z, архивируя файлы в папке {folder_user_in} и сохраняя результат в папке {folder_user_out}. Проверяет, что вывод команды содержит текст "Everything is Ok".
Тест test_step_2: Извлекает файлы из архива с использованием команды 7z из папки {folder_user_out} в папку {folder_user_ex} на удаленном сервере. Проверяет, что вывод команды содержит текст "Everything is Ok".
