# corte2_1077721349 - Control y seguimiento de carros.

Necesidad:
La empresa requiere un sistema de recordatorio personalizado para sus empleados, con el fin de mejorar la gestión del tiempo y las responsabilidades laborales y personales.

#### Análisis: Definición de requerimientos.
### Requerimientos Funcionales

1. **RF1: Gestión de Usuarios**
   - El sistema debe permitir el registro de usuarios, incluyendo atributos como país, primer nombre, segundo nombre, contraseña, rol y nombre de usuario.

2. **RF2: Gestión de Categorías de Recordatorios**
   - El sistema debe tener la capacidad de clasificar los recordatorios en diferentes categorías, cada una asociada a un usuario específico.

3. **RF3: Gestión de Recordatorios**
   - El sistema debe permitir a los usuarios crear recordatorios personalizados, especificando detalles como archivo adjunto, descripción, fecha, hora, título y categoría..



### Requerimientos No Funcionales

1. **RNF1: Integridad de Datos**
   - El sistema debe asegurar la integridad de los datos, mediante el uso de claves primarias y foráneas en las tablas de la base de datos.

2. **RNF2: Rendimiento del Sistema**
   - El sistema debe ser capaz de manejar múltiples usuarios y recordatorios simultáneamente, sin afectar significativamente su rendimiento.


3. **RNF3: Seguridad de Datos**
   - El sistema debe proteger la información almacenada, asegurando que solo el personal autorizado tenga acceso a los recordatorios y datos de los usuarios.

4. **RNF4: Escalabilidad**
   - El sistema debe ser escalable para soportar un crecimiento en el número de usuarios y recordatorios sin requerir cambios importantes en su estructura.

5. **RNF5: Disponibilidad y Recuperación de Datos**
   - El sistema debe garantizar la disponibilidad de los datos y contar con mecanismos de respaldo para la recuperación ante posibles fallos o pérdida de información.


#### Diseñar Base de Datos


> Ver:
![modelo relacional](IMG/MR.png)

> Script de la base de datos:
```sql
   DROP DATABASE IF EXISTS SistemaDeRecordatorioPersonalizado;

    CREATE DATABASE SistemaDeRecordatorioPersonalizado;

    USE SistemaDeRecordatorioPersonalizado;

    CREATE table User(
        Id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        País VARCHAR(50) NOT NULL,
        Primer nombre VARCHAR(50) NOT NULL,
        Segundo nombre VARCHAR(50) NOT NULL,
        Contraseña VARCHAR(50) NOT NULL,
        Rol VARCHAR(50) NOT NULL,
        Username VARCHAR(50) NOT NULL,
        
    ); 

    CREATE table Categoria(
        Id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        Descripcion VARCHAR(50) NOT NULL,
        User_Id INT NOT NULL,
        FOREIGN KEY (User_Id) REFERENCES User(Id)
    ); 

    CREATE table Recordatorio(
        Id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        Archivo VARCHAR(50) NOT NULL,
        Descripcion VARCHAR(50) NOT NULL ,
        Fecha DATE NOT NULL,
        Hora DATETIME,
        Titulo VARCHAR(50) NOT NULL ,
        Categoria_Id INT NOT NULL,
        FOREIGN KEY (Categoria_Id) REFERENCES Categoria(Id)
        
    );
# Ver planificación 
[Ver Aquí](https://trello.com/b/1rmrAMV0/parcialanalisis1077721349)
