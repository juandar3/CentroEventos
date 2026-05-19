# CentroEventos
Proyecto Final Ingenieria de Software I realizado por los estudiantes Juan David Reyes y Maria Camila Melo

# Centro Eventos UQ

Aplicación de escritorio para la gestión y compra de boletas de eventos, desarrollada con **Java + JavaFX**. Incluye arquitectura de sockets para múltiples taquillas simultáneas, persistencia en XML y generación de códigos QR.

---

## Requisitos previos

| Herramienta | Versión mínima |
|-------------|----------------|
| Java JDK    | 17             |
| Maven       | 3.8+           |
| JavaFX      | 17.0.2 (incluido vía Maven) |

> **Nota:** el `pom.xml` compila con `--source 14 --target 14`, pero JavaFX 17 requiere JDK 17 o superior.

---

## Cómo ejecutar el proyecto

### 1. Clonar el repositorio

```bash
git clone https://github.com/juandar3/CentroEventos.git
cd CentroEventos
```

### 2. Compilar el proyecto

```bash
mvn clean install -DskipTests
```

### 3. Iniciar el servidor de taquillas

Antes de abrir cualquier cliente, el servidor de sockets debe estar corriendo:

```bash
mvn javafx:run -Djavafx.mainClass=co.edu.uniquindio.edu.co.centroeventosuq/co.edu.uniquindio.edu.co.centroeventosuq.CentroEventosApplication
```

> El servidor escucha en el puerto **8081** (`localhost:8081`).

### 4. Abrir instancias de taquilla (clientes)

Cada instancia representa una taquilla independiente. Puedes abrir hasta 5:

```bash
# Taquilla 1
mvn javafx:run

# Taquilla 2
mvn javafx:run -Djavafx.mainClass=co.edu.uniquindio.edu.co.centroeventosuq/co.edu.uniquindio.edu.co.centroeventosuq.CentroEventosApplication2

# Taquilla 3
mvn javafx:run -Djavafx.mainClass=co.edu.uniquindio.edu.co.centroeventosuq/co.edu.uniquindio.edu.co.centroeventosuq.CentroEventosApplication3
```

---

## Usuarios demo

Al arrancar por primera vez se crean automáticamente:

| Rol           | Correo / Usuario | Contraseña   | Acceso                                         |
|---------------|------------------|--------------|------------------------------------------------|
| Administrador | `admin`          | `admin123`   | Panel de administrador, crear/eliminar eventos |
| Usuario       | `usuario`        | `usuario123` | Catálogo de eventos, compra de boletas         |

> Para reiniciar los usuarios demo elimina `src/main/resources/Persistencia/usuarios.xml` y reinicia la aplicación.

---

## Funcionalidades principales

- Registro e inicio de sesión con roles (Administrador / Usuario)
- Catálogo de eventos con filtro por fecha
- Compra de boletas con selección de localización (Cobre, Plata, Oro)
- Control de concurrencia con semáforos por evento
- Arquitectura cliente-servidor con sockets para múltiples taquillas
- Generación de códigos QR por boleta
- Envío de confirmación por email
- Persistencia de datos en XML (JAXB)
- Logs de acciones de usuario

---

## Dependencias principales

| Dependencia           | Uso                      |
|-----------------------|--------------------------|
| JavaFX 17             | Interfaz gráfica         |
| Lombok                | Reducción de boilerplate |
| JAXB (javax.xml.bind) | Persistencia XML         |
| ZXing (Google)        | Generación de QR         |
| Jakarta Mail          | Envío de correos         |
| JUnit 5               | Pruebas unitarias        |

---

## Consideraciones

- No requiere base de datos, toda la persistencia es en archivos XML locales.
- El servidor de sockets debe iniciarse **antes** que cualquier cliente.
- Si `usuarios.xml` ya existe al arrancar, los usuarios demo no se recrean.
