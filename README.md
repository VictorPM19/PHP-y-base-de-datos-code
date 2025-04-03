## 📝 Actividades de PHP y base de datos

### 📊 Proyecto: Tabla de Registro

Este proyecto tiene como objetivo desarrollar una tabla en una base de datos **MySQL** para almacenar datos provenientes de sensores y mostrarlos en una página web. Para lograrlo, se emplean **PHP** y **MySQL** para la gestión de la base de datos y la presentación de la información.

---

## 🛠 Tecnologías Utilizadas

- **PHP**: Se usa para conectar y manejar la base de datos.
- **MySQL**: Sirve como sistema de almacenamiento de datos.
- **HTML**: Permite estructurar y visualizar la tabla en la web.
- **Servidor Web**: Puede ser **Apache** o cualquier servidor compatible con PHP y MySQL.

---

## ⚙ Configuración de la Base de Datos

### 1️⃣ Crear la Base de Datos y la Tabla

Ejecuta este comando SQL en **phpMyAdmin** o en la consola de **MySQL** para preparar la base de datos y la tabla:

```sql
CREATE DATABASE base_de_datos;
USE base_de_datos;

CREATE TABLE registro (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sensor VARCHAR(50) NOT NULL,
    fecha_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    valor FLOAT NOT NULL
);
```

---

## 📂 Archivos del Proyecto

### 1️⃣ `db_config.php` - Configuración de la Conexión a la Base de Datos

Este archivo contiene los datos necesarios para establecer la conexión con **MySQL**.

```php
<?php
  $servername = "bjpgg.site";
  $username = "admin_shagy";
  $password = "Shagy123";
  $dbname = "admin_romerillo";
  
  // Establecer conexión
  $conn = new mysqli($servername, $username, $password, $dbname);
  
  // Comprobar si hay errores
  if ($conn->connect_error) {
    die("Conexión fallida: " . $conn->connect_error);
  }
?>
```

🔹 **Descripción:** Este script define las credenciales (nombre del servidor, usuario, contraseña y nombre de la base de datos) y crea una conexión con **MySQL** usando la clase `mysqli`. Si la conexión falla, muestra un mensaje de error y detiene la ejecución.

---

### 2️⃣ `insert.php` - Insertar Datos en la Tabla

Este archivo permite agregar nuevos registros a la tabla `registro`.

```php
<?php
  include 'db_config.php';
  $sql = "INSERT INTO registro (sensor, valor) VALUES ('temperatura', 22)";
  
  if ($conn->query($sql) === TRUE) {
    echo "¡Registro añadido con éxito! 🌟";
  } else {
    echo "Error: " . $sql . "<br>" . $conn->error;
  }
  
  $conn->close();
?>
```

🔹 **Descripción:** Se incluye el archivo de configuración para usar la conexión establecida. Luego, se ejecuta una consulta SQL para insertar un valor de ejemplo (`sensor: temperatura, valor: 22`). Si la operación es exitosa, se muestra un mensaje positivo; de lo contrario, se indica el error.

---

### 3️⃣ `index.php` - Mostrar Datos en una Tabla

Este script recupera los datos de la base de datos y los presenta en una tabla **HTML**.

```php
<?php
  include 'db_config.php';
  $sql = "SELECT id, sensor, fecha_hora, valor FROM registro";
  $result = $conn->query($sql);
  
  echo "<h2>Registro de Sensores 📊</h2>";
  echo "<table border='1'>
    <tr>
      <th>ID</th>
      <th>Sensor</th>
      <th>Fecha y Hora</th>
      <th>Valor</th>
    </tr>";
  
  if ($result->num_rows > 0) {
    while ($row = $result->fetch_assoc()) {
      echo "<tr>
        <td>" . $row["id"] . "</td>
        <td>" . $row["sensor"] . "</td>
        <td>" . $row["fecha_hora"] . "</td>
        <td>" . $row["valor"] . "</td>
      </tr>";
    }
    echo "</table>";
  } else {
    echo "No hay datos disponibles. 😞";
  }
  
  $conn->close();
?>
```

🔹 **Descripción:** Este código consulta todos los registros de la tabla `registro` y los muestra en una tabla **HTML**. Si hay resultados, los recorre con un bucle `while` e inserta los datos en filas.

---

## 🌐 Proyecto: Registro de Sensores (API)

Este proyecto desarrolla una **API en PHP** que recibe datos en formato **JSON** y los guarda en una base de datos **MySQL**. Es ideal para sistemas **IoT** o aplicaciones que necesiten almacenar datos de sensores en tiempo real.

---

## ⚙ Configuración de la Base de Datos

Asegúrate de preparar la base de datos antes de usar la API:

```sql
CREATE DATABASE admin_romerillo;
USE admin_romerillo;

CREATE TABLE registro (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sensor VARCHAR(50) NOT NULL,
    fecha_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    valor FLOAT NOT NULL
);
```

---

## 📜 Archivos del Proyecto (API)

### 1️⃣ `db_config.php` - Configuración de la Conexión

Archivo para conectar **PHP** con **MySQL**.

```php
<?php
  $servername = "pagina_web";
  $username = "nombre_de_acceso";
  $password = "contraseña";
  $dbname = "nombre_de_la_base_de_datos";
  
  // Crear conexión
  $conn = new mysqli($servername, $username, $password, $dbname);
  
  // Verificar conexión
  if ($conn->connect_error) {
    die("Conexión fallida: " . $conn->connect_error);
  }
?>
```

🔹 **Descripción:** Similar al archivo anterior, este script configura la conexión con credenciales genéricas que deben ajustarse según el entorno real.

---

🚀 ¡Con esto, ya tienes una API funcional para almacenar y consultar datos de sensores en una base de datos MySQL! 🎯
