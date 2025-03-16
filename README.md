# Домашнее задание к занятию «Введение в Terraform»

### Цели задания

1. Установить и настроить Terrafrom.
2. Научиться использовать готовый код.

------

### Чек-лист готовности к домашнему заданию

1. Скачайте и установите **Terraform** версии ~>1.8.4 . Приложите скриншот вывода команды ```terraform --version```.
2. Скачайте на свой ПК этот git-репозиторий. Исходный код для выполнения задания расположен в директории **01/src**.
3. Убедитесь, что в вашей ОС установлен docker.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. Репозиторий с ссылкой на зеркало для установки и настройки Terraform: [ссылка](https://github.com/netology-code/devops-materials).
2. Установка docker: [ссылка](https://docs.docker.com/engine/install/ubuntu/). 
------
### Внимание!! Обязательно предоставляем на проверку получившийся код в виде ссылки на ваш github-репозиторий!
------

### Задание 1

1. Перейдите в каталог [**src**](https://github.com/netology-code/ter-homeworks/tree/main/01/src). Скачайте все необходимые зависимости, использованные в проекте. 
2. Изучите файл **.gitignore**. В каком terraform-файле, согласно этому .gitignore, допустимо сохранить личную, секретную информацию?(логины,пароли,ключи,токены итд)
3. Выполните код проекта. Найдите  в state-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.
4. Раскомментируйте блок кода, примерно расположенный на строчках 29–42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните, в чём заключаются намеренно допущенные ошибки. Исправьте их.
5. Выполните код. В качестве ответа приложите: исправленный фрагмент кода и вывод команды ```docker ps```.
6. Замените имя docker-контейнера в блоке кода на ```hello_world```. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду ```terraform apply -auto-approve```.
Объясните своими словами, в чём может быть опасность применения ключа  ```-auto-approve```. Догадайтесь или нагуглите зачем может пригодиться данный ключ? В качестве ответа дополнительно приложите вывод команды ```docker ps```.
8. Уничтожьте созданные ресурсы с помощью **terraform**. Убедитесь, что все ресурсы удалены. Приложите содержимое файла **terraform.tfstate**. 
9. Объясните, почему при этом не был удалён docker-образ **nginx:latest**. Ответ **ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ**, а затем **ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ** строчкой из документации [**terraform провайдера docker**](https://docs.comcloud.xyz/providers/kreuzwerker/docker/latest/docs).  (ищите в классификаторе resource docker_image )

## Ответ: 
### Задание 1
### 1-3
![1](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.0.jpg)
![2](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.1.jpg)
![3](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.2.jpg)
![4](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.3.jpg)

Личную, секретную информацию можно хранить в файле terraform.tfvars или другом файле с расширением .tfvars, который игнорируется Git.

### 4-5
![5](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.4.jpg)

Линия 24. Не указано имя ресурса для docker_image добавляем "nginx"

Линия 29. Имя "должно начинаться с буквы или подчеркивания и может содержать только буквы, цифры, подчеркивания, и тире." Убираем число перед именем рессурса контейнера 1nginx, меняем на nginx.

Линия 31. "random_string_FAKE" не объявлен в корневом модуле "random_password". Убираем FAKE и меням resulT на result.


### Было:

![6](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.5.jpg)

### Стало: 

![7](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.6.jpg)

![8](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.7.jpg)

### 6-8

![9](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.8.jpg)
![10](https://github.com/Sawyer086/Terraform_01/blob/main/1/1.9.jpg)

Команда terraform apply -auto-approve автоматически применяет изменения без подтверждения пользователем. Можно случайно удалить или изменить важные ресурсы.

Можно применять:
- в автоматизированных CI/CD пайплайнах;
- в тестовых средах при незначительных изменениях конфигурации.

![9](https://github.com/Sawyer086/Terraform_01/blob/main/1/2.0.jpg)

Строчка из документации terraform провайдера docker:

"keep_locally (Boolean) If true, then the Docker image won't be deleted on destroy operation.

If this is false, it will delete the image from the docker local storage on destroy operation."

Ответ в коде main.tf:
keep_locally = true -это означает, что Terraform будет сохранять образ даже после выполнения команды destroy.

![11](https://github.com/Sawyer086/Terraform_01/blob/main/1/2.1.jpg)
