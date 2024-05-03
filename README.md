# corte2_1077721349 - Control y seguimiento de carros.

#### Necesidad:
Se necesita una base de datos para una taller que requiere control y registro de autos.

#### Análisis: Definición de requerimientos.
### Requerimientos Funcionales

1. **RF1: Clasificación de Categorías de Carros**
   - El sistema debe tener la capacidad de almacenar diferentes categorías de carros, cada una con sus propias propiedades como nombre, descripción, rendimiento y estado.

2. **RF2: Registro de Autos**
   - El sistema debe permitir el registro de autos, incluyendo atributos como nombre, modelo, tamaño, número de puertas y referencia a la categoría del carro.

3. **RF3: Relación entre Autos y Personas**
   - El sistema debe mantener una relación entre autos y personas mediante la tabla "AutosPersona". Esta tabla debe incluir atributos como fecha de asociación y referencias a los autos y las personas.

4. **RF4: Registro de Personas**
   - El sistema debe permitir el registro de personas con atributos como cédula, nombre, apellido, teléfono y correo electrónico.

### Requerimientos No Funcionales

1. **RNF1: Integridad Referencial**
   - El sistema debe asegurar la integridad referencial entre las tablas, mediante claves foráneas y restricciones adecuadas.

2. **RNF2: Rendimiento del Sistema**
   - El sistema debe ser capaz de manejar múltiples operaciones simultáneamente sin degradación significativa del rendimiento.

3. **RNF3: Seguridad de Datos**
   - El sistema debe proteger los datos almacenados y asegurar que solo el personal autorizado tenga acceso a información sensible.

4. **RNF4: Escalabilidad**
   - El sistema debe ser capaz de escalar para acomodar un creciente número de autos y personas sin requerir cambios significativos en la estructura de la base de datos.

5. **RNF5: Disponibilidad y Recuperación de Desastres**
   - El sistema debe tener mecanismos para garantizar la alta disponibilidad y proporcionar planes de recuperación ante fallos o desastres.


#### Diseñar Base de Datos

- La clasificación de las categorías de carros, estos son individuales.

##### Tabla: CategoriaCarros
| id  | nombre    | descripción | rendimiento | estado |
|-----|-----------|-------------|--------------|--------|
|  1  | Deportico | carro rápido| 2500 v       | True   |
|  2  | Formal    | carro lujoso| 2400 s       | True   |

##### Tabla: Autos
| id  | nombre  | modelo | tamaño | puertas | CategoriaCarros_id |
|-----|---------|--------|--------|---------|--------------------|
|  1  | Mustang | GT     | 450    | 2       | 1                  |
|  2  | Accord  | LX     | 350    | 4       | 2                  |

##### Tabla: AutosPersona
| id  | fecha       | Autos_id | Persona_id |
|-----|-------------|----------|------------|
|  1  | 2023-05-01  | 1        | 1          |
|  2  | 2023-06-15  | 2        | 2          |

##### Tabla: Persona
| id  | cédula  | nombre    | apellido  | teléfono  | correo            |
|-----|---------|-----------|-----------|-----------|------------------|
|  1  | 1234567 | Juan      | Pérez     | 5551234567| juan@example.com |
|  2  | 7654321 | María     | García    | 5557654321| maria@example.com|
|  3  | 7654322 | Marío     | García    | 5557654322| mario@example.com|

---

> Ver:
![modelo relacional](IMG/MR.png)

> Script de la base de datos:
```sql
DROP DATABASE IF EXISTS cultivo;

CREATE DATABASE ControlAutos;

USE ControlAutos;

CREATE TABLE CategoriaCarros (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50) NOT NULL UNIQUE,
    descripcion VARCHAR(50) NOT NULL,
    rendimiento NVARCHAR(50) NOT NULL,
    estado BIT DEFAULT TRUE
);

CREATE TABLE Autos (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50) NOT NULL UNIQUE,
    modelo VARCHAR(50) NOT NULL,
    tamaño INT NOT NULL,
    puertas INT NOT NULL,
    FOREIGN KEY (CategoriaCarros_id) REFERENCES CategoriaCarros(id)
);

CREATE TABLE AutosPersona (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    fecha DATE NOT NULL,
    FOREIGN KEY (Autos_id) REFERENCES Autos(id),
    FOREIGN KEY (Persona_id) REFERENCES Persona(id)
);

CREATE TABLE Persona (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    cédula INT NOT NULL,
    nombre VARCHAR(50) NOT NULL UNIQUE,
    apellido VARCHAR(50) NOT NULL,
    teléfono INT NOT NULL,
    correo VARCHAR(50) NOT NULL
);

# Ver planificación 
[Ver Aquí](https://trello.com/b/1rmrAMV0/parcialanalisis1077721349)
