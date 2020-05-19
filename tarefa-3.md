# Tarefa 3

# Creacion de Bases de datos

# INDICE

- [Instalacion Base de datos Naves Espaciales](#5)
- [Instalacion Base de datos Proyecto investigación](#6)


# Creacion Base de datos Naves Espaciales <a name="5"></a>

- Sino estamos como root, nos logeamos con __sudo su__ y escribimos la contraseña.

- Después ponemos __mysql__ para hacer a la base de datos

- Y luego escribimos la siguiente sentencia:

![Alt text](https://github.com/ToniChoren/BasesDeDatos/blob/master/InstalacionMySQL/capturas/capturas%20ubuntu/captura4_Servicio.png)

- Despues vamos introduciendo las sentencias o importarla desde un archivo. 

      En mi caso las voy a introducir mediante consola.

![Alt text](https://github.com/ToniChoren/BasesDeDatos/blob/master/InstalacionMySQL/capturas/capturas%20ubuntu/captura5_Servicio.png)


- Cuando terminemos mostramos la bese de datos con el comando:

      show databases
 
![Alt text](https://github.com/ToniChoren/BasesDeDatos/blob/master/InstalacionMySQL/capturas/capturas%20ubuntu/database01.PNG)

- Para hacer uso de una bases de datos  se haría de la siguiente manera:

      use navesEspaciales

- Después mostramos las tablas creadas con anterioridad con el siguiente comando

      show tables
      
 ![Alt text](https://github.com/ToniChoren/BasesDeDatos/blob/master/InstalacionMySQL/capturas/capturas%20ubuntu/mostrar_navesEspaciales.PNG)
     
 
 - Podemos mostrar la descripcion utilizando el comando __desc__
 
 ![Alt text](https://github.com/ToniChoren/BasesDeDatos/blob/master/InstalacionMySQL/capturas/capturas%20ubuntu/desc_planteta.PNG)


[⬆⬆ INDICE ⬆⬆](#INDICE)

---
 
 # Creacion Base de datos Proyecto Investigación <a name="6"></a>
 
 - Sino estamos como root, nos logeamos con __sudo su__ y escribimos la contraseña.

 - Después ponemos __mysql__ para hacer a la base de datos

 - Escribimos el siguiente comando para crear la base de datos: 
      
        CREATE SCHEMA proInv;
    
 - Y luego escribimos la siguiente sentencia:
 
      show databases;
 
 ![Alt text](https://github.com/ToniChoren/BasesDeDatos/blob/master/InstalacionMySQL/capturas/capturas%20ubuntu/showDatabaes.PNG)
 
 - Para selecionarla:
 
        use proInv
        
 - Y luego para visializar las sentencias escribimos  __show tables__.
 
 ![Alt text](https://github.com/ToniChoren/BasesDeDatos/blob/master/InstalacionMySQL/capturas/capturas%20ubuntu/showTables.PNG)

[⬆⬆ INDICE ⬆⬆](#INDICE)

***
