# Laboratorio: DNS/Dig 🌐

1. Si queremos conocer la **dirección IP** asociada a un **dominio** usaremos **`nslookup`**

```sql
nslookup <Dominio>
```

![nslookup.PNG](./assets/DNS-Dig/01-nslookup.png)

2. Podemos realizar diferentes tipos de **solicitudes** con **`nslookup`** en este caso realizaremos una **petición PTR** a la **dirección IP 173.0.87.51**

```sql
dig -query=PTR 173.0.87.51
```

![output.PNG](./assets/DNS-Dig/02-output.png)

3. Para revisar **servidores de correo** asociados a un dominio usaremos **`dig`**

```sql
dig MX <Dominio>
```

![ip.PNG](./assets/DNS-Dig/03-ip.png)

- El primer **servidor de correo asociado** es **mx1.paypalcorp.com**