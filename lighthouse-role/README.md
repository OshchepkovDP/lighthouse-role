# LightHouse Role

Ansible-роль для установки и настройки [LightHouse](https://github.com/VKCOM/lighthouse) —
веб-интерфейса для ClickHouse. В качестве веб-сервера используется NGINX.

## Требования

- Ansible >= 2.10
- Ubuntu 20.04+ / Debian 11+
- Права sudo (become)

## Переменные роли

### Пользовательские переменные (`defaults/main.yml`)

| Переменная                    | Значение по умолчанию                        | Описание                        |
|-------------------------------|----------------------------------------------|---------------------------------|
| `lighthouse_repo`             | `https://github.com/VKCOM/lighthouse.git`    | URL git-репозитория LightHouse  |
| `lighthouse_version`          | `master`                                     | Ветка или тег для checkout      |
| `lighthouse_install_dir`      | `/var/www/lighthouse`                        | Директория установки            |
| `lighthouse_nginx_port`       | `80`                                         | Порт, на котором слушает NGINX  |
| `lighthouse_nginx_server_name`| `_`                                          | Директива server_name NGINX     |

### Внутренние переменные (`vars/main.yml`)

| Переменная                       | Описание                              |
|----------------------------------|---------------------------------------|
| `lighthouse_nginx_config_path`   | Путь к конфигу в sites-available      |
| `lighthouse_nginx_enabled_path`  | Путь к symlink в sites-enabled        |

## Зависимости

Нет. NGINX и Git устанавливаются задачами роли.

## Пример использования

```yaml
- name: Install LightHouse
  hosts: lighthouse
  become: true
  roles:
    - role: lighthouse-role
      vars:
        lighthouse_nginx_port: 8080
        lighthouse_nginx_server_name: "lighthouse.example.com"
