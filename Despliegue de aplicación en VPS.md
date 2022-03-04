### Despliegue de aplicación en VPS

> Tarea realizada por Miguel Valle, Alejandro Cortina y Rubén Gómez

- Instalamos mysql

```bash
sudo apt-get install mysql-server mysql-client
```

![1 install mysql](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/1%20install%20mysql.png)

```bash
sudo mysql
```

![2 mysql](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/2%20mysql.png)

```bash
sudo mysql_secure_installation
```

![3 mysql secure instlallation](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/3%20mysql%20secure%20instlallation.png)

Borramos usuarios anónimos y eliminamos el root `login` remoto.

![4 remove anonymous users](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/4%20remove%20anonymous%20users.png)

![5 disallow root](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/5%20disallow%20root.png)

Eliminamos la base de datos de pruebas y recargamos los privilegios de la base de datos.

![6](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/6.png)

![7](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/7.png)

```mysql
alter user 'root'@'localhost' identified with mysql_native_password by 'area';
```

![8. alter user](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/8.%20alter%20user.png)

```mysql
mysql -u root -p
```

![9 entramos mysql](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/9%20entramos%20mysql.png)

```mysql
create database test_virtual;
```

![10](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/10.png)

```mysql
show database;
```

![11 se encuentra la bdd que hemos creado](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/11%20se%20encuentra%20la%20bdd%20que%20hemos%20creado.png)

```mysql
create user 'user'@'localhost' identified by 'user';
```

![12](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/12.png)

```mysql
select user from mysql.user;
```

![13 se encuentra user](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/13%20se%20encuentra%20user.png)

```mysql
grant all privileges on test_virtaul.* to 'user'@'localhost' with grant Option;
```

![14 doy permisos](C:/Users/diurno/Desktop/tarea%20despliegue%20ftp/1/14%20doy%20permisos.png)

```mysql
mysql -u user -p
```

![15](tarea%20despliegue%20ftp/1/15.png)

```mysql
show databases;
```

![16](tarea%20despliegue%20ftp/1/16.png)

```mysql
mysql -u root -p
```

![17 entramos con root](tarea%20despliegue%20ftp/1/17%20entramos%20con%20root.png)

```mysql
flush prvileges;
```

![18 flush privilegies](tarea%20despliegue%20ftp/1/18%20flush%20privilegies.png)

- Instalamos maven

```bash
sudo apt-get install maven
```

![19 install maven](tarea%20despliegue%20ftp/1/19%20install%20maven.png)

- Instalamos jdk8

```bash
sudo apt-get install openjdk-8-jdk
```

![20 install jdk8](tarea%20despliegue%20ftp/1/20%20install%20jdk8.png)

```bash
java -version
```

![21 java version](tarea%20despliegue%20ftp/1/21%20java%20version.png)

```bash
javac -version
```

![22 javac version](tarea%20despliegue%20ftp/1/22%20javac%20version.png)

```bash
systemctl status vsftpd
```

![25 tener instaldo vsftpd](tarea%20despliegue%20ftp/1/25%20tener%20instaldo%20vsftpd.png)

```bash
sudo nano /etc/vsftpd.conf
```

![26](tarea%20despliegue%20ftp/1/26.png)

```nano
#Uncomment ths to enable any form of FTP write command.
write_enable=YES
```

![](tarea%20despliegue%20ftp/1/27%20enable%20yes.png)

```bash
sudo systemctl restart vsftpd.service
```

![28 restart](tarea%20despliegue%20ftp/1/28%20restart.png)

```bash
sudo systemctl is-enabled vsftpd.service enabled
```

![29 comprobamos servicio](tarea%20despliegue%20ftp/1/29%20comprobamos%20servicio.png)

```bash
git clone https://github.com/cavanosa/virtualBACK.git
```

![30 git clone](tarea%20despliegue%20ftp/1/30%20git%20clone.png)

- FileZilla

![31 entramos filezilla](tarea%20despliegue%20ftp/1/31%20entramos%20filezilla.png)

![32 transferimos la carpeta con git a master](tarea%20despliegue%20ftp/1/32%20transferimos%20la%20carpeta%20con%20git%20a%20master.png)

```bash
ls
mvn clean
ls

```

![33 ](tarea%20despliegue%20ftp/1/33%20.png)



![34 mvn clean](tarea%20despliegue%20ftp/1/34%20mvn%20clean.png)

![35 build succes](tarea%20despliegue%20ftp/1/35%20build%20succes.png)

![36 ls + nano pom.xml](tarea%20despliegue%20ftp/1/36%20ls%20+%20nano%20pom.xml.png)

- Comprobamos `pom.xml`

![37 agregamos finalName](tarea%20despliegue%20ftp/1/37%20agregamos%20finalName.png)

```bash
mvn install
```

![38 mvn install](tarea%20despliegue%20ftp/1/38%20mvn%20install.png)

![39 build success](tarea%20despliegue%20ftp/1/39%20build%20success.png)

```bash
sudo ufw allow 8080/tcp
```

![39.2 allow puerto 8080](tarea%20despliegue%20ftp/1/39.2%20allow%20puerto%208080.png)

```bash
ls
java -jar target/virtual.jar
```

![40 ](tarea%20despliegue%20ftp/1/40%20.png)

![41 java.jar](tarea%20despliegue%20ftp/1/41%20java.jar.png)

![42](tarea%20despliegue%20ftp/1/42.png)

- Accedemos desde el navegador web

![43 accedemos](tarea%20despliegue%20ftp/1/43%20accedemos.png)

![44 accedemos -apache Opcional](tarea%20despliegue%20ftp/1/44%20accedemos%20-apache%20Opcional.png)

![45 accedemos ruta](tarea%20despliegue%20ftp/1/45%20accedemos%20ruta.png)

![46 detalle 4](tarea%20despliegue%20ftp/1/46%20detalle%204.png)

```bash
sudo nano /etc/systemd/systemd/system/spring.service
```

![47 creamos ](tarea%20despliegue%20ftp/1/47%20creamos%20.png)

```bash
[Unit]
Properties=my spring boot app

[Service]
Restart=always
ExecStart=
SuccessExitStatus=143

[Install]
wanted-by=multi-user.target
```

![48 escribimos y guardamos](tarea%20despliegue%20ftp/1/48%20escribimos%20y%20guardamos.png)

```bash
sudo nano /etc/systemd/system/spring.service
pwd /home/master/virtualBACK 
cd target
ls
pwd /home/master/virtualBACK/target
```

![49](tarea%20despliegue%20ftp/1/49.png)

```bash
sudo nano /etc/systemd/system/spring/spring.service
```

![50 volvemos a abrir](tarea%20despliegue%20ftp/1/50%20volvemos%20a%20abrir.png)

![51 cambiamos](tarea%20despliegue%20ftp/1/51%20cambiamos.png)

```bash
sudo systemctl enable spring.service
```

![52 status spring ](tarea%20despliegue%20ftp/1/52%20status%20spring%20.png)

![53 volvemos a cambiar](tarea%20despliegue%20ftp/1/53%20volvemos%20a%20cambiar.png)

```bash
sudo systemctl enable spring.service
```

![54](tarea%20despliegue%20ftp/1/54.png)

```bash
sudo systemctl is-enabled spring.service enabled
```

![55 enabled](tarea%20despliegue%20ftp/1/55%20enabled.png)

```bash
sudo systemctl status start spring.service
sudo systemctl is-active spring.service active
```

![56 active](tarea%20despliegue%20ftp/1/56%20active.png)

- Instalamos Apache

```bash
sudo apt-get install apache2
```

![1 install apache2](tarea%20despliegue%20ftp/2/1%20install%20apache2.PNG)

```bash
sudo systemctl is-enabled apache2 enabled
```

![2 enabled apache2](tarea%20despliegue%20ftp/2/2%20enabled%20apache2.PNG)

```bash
sudo systemctl is-active apache2 active
```

![3 active apache2](tarea%20despliegue%20ftp/2/3%20active%20apache2.PNG)

![4 vemos que tenemos apache](tarea%20despliegue%20ftp/2/4%20vemos%20que%20tenemos%20apache.PNG)

```bash
sudo nano /var/www/html/index.html
```

![5 entramos](tarea%20despliegue%20ftp/2/5%20entramos.PNG)

Modificamos el documento html

![6 podemos modificar la pagina de apache](tarea%20despliegue%20ftp/2/6%20podemos%20modificar%20la%20pagina%20de%20apache.PNG)

```bash
sudo mv /var/www/html/index.html home/master
cd ..
ls
cd master
ls
```

![7 movemos a master el index.html](tarea%20despliegue%20ftp/2/7%20movemos%20a%20master%20el%20index.html.png)

Nos queda la lista vacía:

![7 nos queda la lista vacia](tarea%20despliegue%20ftp/2/7%20nos%20queda%20la%20lista%20vacia.PNG)

Creamos carpeta VirtualFRONT con el contenido de los archivos de `github.`

![8 creamos carpeta virtualFRONT con lo de github](tarea%20despliegue%20ftp/2/8%20creamos%20carpeta%20virtualFRONT%20con%20lo%20de%20github.PNG)

- En VScode

```bash
ftp
cd virtualFRONT
code .
```

![9 lanzamos code . en cmd](tarea%20despliegue%20ftp/2/9%20lanzamos%20code%20.%20en%20cmd.PNG)

```bash
git clone https://github.com/cavanosa/virtualFRONT.git
cd virtualFRONT
code .
```

![9 v2](tarea%20despliegue%20ftp/2/9%20v2.png)

Abrimos el documento en VScode:

![10 nos abre](tarea%20despliegue%20ftp/2/10%20nos%20abre.png)

Desde su terminal ejecutamos el comando `npm update`:

![11 hacemos npm update](tarea%20despliegue%20ftp/2/11%20hacemos%20npm%20update.PNG)

![12](tarea%20despliegue%20ftp/2/12.png)

![13](tarea%20despliegue%20ftp/2/13.png)

```bash
npm install -g @angular/cli
```

![14 instalamos angular](tarea%20despliegue%20ftp/2/14%20instalamos%20angular.png)

- Abrimos powershell, damos permisos a angular.

```cmd
Set-ExecutionPolicy Unrestricted
```

![15 permitimos lanzar scripts en virtual visual code](tarea%20despliegue%20ftp/2/15%20permitimos%20lanzar%20scripts%20en%20virtual%20visual%20code.png)

```bash
ng serve -o
```

![16 ng serve](tarea%20despliegue%20ftp/2/16%20ng%20serve.png)

Comprobamos los cambios en la página:

![17 ](tarea%20despliegue%20ftp/2/17%20.png)

Modificamos el documento `tio.service.ts`

![18 cambiamos](tarea%20despliegue%20ftp/2/18%20cambiamos.png)

Añadimos un usuario nuevo desde la página:

![19 añadimos](tarea%20despliegue%20ftp/2/19%20a%C3%B1adimos.png)

Se guardan los cambios.

![20 se guarda](tarea%20despliegue%20ftp/2/20%20se%20guarda.png)

```bash
ng build --prod
```

![21 ng build --prod](tarea%20despliegue%20ftp/2/21%20ng%20build%20--prod.png)

```bash
whoami
sudo chown -R master /var/www/html
sudo chmod -R 755 /var/www/html/
```

![22 permisos](tarea%20despliegue%20ftp/2/22%20permisos.png)

![23](tarea%20despliegue%20ftp/2/23.png)

![26 con ip](tarea%20despliegue%20ftp/2/26%20con%20ip.png)![24 nos movemos a var ww html](tarea%20despliegue%20ftp/2/24%20nos%20movemos%20a%20var%20ww%20html.png)

Por último, modificamos el archivo `app-routing.module.ts`:

![27 cambiamos](tarea%20despliegue%20ftp/2/27%20cambiamos.png)