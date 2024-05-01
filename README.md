# corte2_1077721349# Control y seguimiento Control y registro de crros. 


#### Necesidad: se necesita una base de dato para una emresa que requiere control y registro de de autos 



#### Análisis: Definición de requerimientos. 

1. RF1: Tendra un categorias de carros y habran 4 categorias
2. RF1: tendra 6 atributos los Autos con referencia{ref:categoria}
3. RF1: tendra AutosPersona y tendra 4 atributos y con referencias [ref:Autos,ref:persona]
1. RNF1: tendra personas y tendra 6 atributos no tiene ninguna referencia pero se necesita para el Autos Personas


#### Diseñar Base de Datos
Datos a tener en cuenta

| código | Ubicación | Capacidad | Cantidad |  Fecha   | Estado |
|--------|-----------|-----------|----------|----------|--------|
| 101    |C-101      |2500       |0         |          | False  |
| 102    |C-102      |2400       |2000      |17-04-2024| True   |
| 112    |B-112      |600        |600       |17-04-2024| False  |
| 112    |B-112      |600        |400       |20-05-2024| True   |

* De lo anterior, se puede resaltar lo siguiente, si bien es cierto, se puede ingresar los datos sin normalización, se sabe que es necesario para la optimización y traza de los datos. 

En este sentido, se procede a normarlizar de la siguiente manera. 

* La clasificación de la categoria carros , estos son individuales. 
CategoriaCarros
| id |nombre     | descricion| rendimiento |estado     |
|----|-------    |-----------|-----------  |-----------|
|  1 |Deportico  |carro      |2500 v       |True       |
|  2 |formal     |sisi       |2400  s      |True       |


* Se conoce que inicio de un cultivo, se requiere de la disponibilidad del galpon. Al Asignar un grupo de pollos al galpon, se debe ocupar el galpo  

Cultivo
| id    | Cantidad |  Fecha     | GalponId | 
|-------|----------|------------|----------|
|   1   | 1200     | 17-04-2024 |   4      |
|   2   | 600      | 17-04-2024 |   3      |
|   3   | 400      | 20-5-2024  |   3      |


> Ver
![Modelo relacional del ejercicio](bd/MR.png)

> Script de la base de datos
sql
    DROP DATABASE IF EXISTS cultivo;

    CREATE DATABASE ControlAutos;

    USE ControlAutos;

    CREATE table CategoriaCarros(
        id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        nombre VARCHAR(50) NOT NULL UNIQUE,
        descripcion VARCHAR(50) NOT NULL,
        rendimiento NVARCHAR(50) NOT NULL,
        estado BIT DEFAULT TRUE
         
    ); 

    CREATE table Autos(
        id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        nombre VARCHAR(50) NOT NULL UNIQUE,
        modelo VARCHAR(50) NOT NULL,
        TAMAÑO INT NOT NULL,
        puertas INT NOT NULL,
        FOREIGN KEY (CategoriaCarros_id) REFERENCES CategoriaCarros(id)
    ); 
     CREATE table AutosPersona(
        id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
      Fecha DATE NOT NULL,
        FOREIGN KEY (Autos_id) REFERENCES Autos(id)
         FOREIGN KEY (PErsona_id) REFERENCES Persona(id)
    ); 
     CREATE table Persona(
        id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        cedula INT NOT NULL,
        nombre VARCHAR(50) NOT NULL UNIQUE,
        Apellido VARCHAR(50) NOT NULL,
        telefono INT NOT NULL,
        correo VARCHAR(50) NOT NULL,
     
    ); 