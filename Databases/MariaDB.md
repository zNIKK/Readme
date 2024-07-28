
# Instalação

## Em docker

```bash
sudo docker run --restart always -d --name bdmariadb1 -p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=SUA_SENHA_FORTE mariadb
```