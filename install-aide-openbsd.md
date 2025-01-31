# INSTALAR AIDE NO OPENBSD

> AIDE é um sistema de detecção de intrusão baseado em host (HIDS) para verificar a integridade de arquivos. 
Ele faz isso criando um banco de dados de linha de base de arquivos em uma execução inicial e, em seguida, 
verifica esse banco de dados em relação ao sistema em execuções subsequentes.

## 1. Vire ROOT:

```
SU -
```
## 2. Atualize e instale a lista de pacotes:

```
pkg_add -u
```

## 3. Instale o aide:

```
pkg_add aide
```

## 4. No terminal crie um banco de dados usando o comando abaixo:

```
aide --init
```

> O comando a cima gera um novo banco de dados em /var/db/aide.db.new
{.is-info}

## 4. Instale o banco de dados recem gerado:

```
cp /var/db/aide.db.new /var/db/aide.db 
```

## 5. Crie um novo arquivo de configuração do Aide. Você pode fazer isso com o seguinte comando:

```
aide -c /etc/aide.conf --update
```

## 6. EDITE O ARQUIVO aide.conf no /etc/aide.conf

```
vim /etc/aide.conf
```

## 7. NO ARQUIVO LOCALIZE "database=file:/var/db/aide.db" e adicione abaixo dele o parametro:

```
database_new=file:/var/db/aide.db.new
```

## 8. NO ARQUIVO LOCALIZE "=/home$      R" e adicione abaixo dele os diretorios que deseja monitorar 

```
=/home$           R
/root/            R
/etc/             R
```

**SAIA DO ARQUIVO SALVANDO.** 

## 9. Faça um teste, criando diretorio e arquivos.

```
mkdir /root/aide-test
touch /root/aide-test/test1
touch /root/aide-test/test2
```

## 10. Execute o Aide check para detectar novos arquivos e diretórios com o seguinte comando:

```
aide -c /etc/aide.conf --check
```
