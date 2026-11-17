# 🛒 ANKAR Software de Gestión | Tiendas Mass
### Sistema Integral de Comercio Omnicanal, Gestión Comercial y Control Inteligente de Inventarios PEPS (FIFO)

![PHP](https://img.shields.io/badge/PHP-8.2%2B-777BB4?style=for-the-badge&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0%2B-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-4.7-010101?style=for-the-badge&logo=socket.io&logoColor=white)
![XAMPP](https://img.shields.io/badge/XAMPP-Ready-FB7A24?style=for-the-badge&logo=xampp&logoColor=white)
![WCAG](https://img.shields.io/badge/WCAG-2.1_AA-005A9C?style=for-the-badge)

---

## 📌 Visión General del Proyecto

**ANKAR Software de Gestión** es una plataforma tecnológica empresarial concebida para modernizar, optimizar y automatizar la operativa comercial, logística y de e-commerce omnicanal en cadenas de retail bajo el modelo de descuento duro (*hard discount*) y tiendas de conveniencia (enfocado en la canasta básica familiar de **Tiendas Mass**).

El sistema erradica la desconexión físico-digital entre la tienda online y los almacenes físicos, eliminando falsos agotamientos, mitigando pérdidas por caducidad mediante algoritmos de rotación **PEPS / FIFO** (conforme a la **Norma Internacional de Contabilidad NIC 2 - Inventarios**) y garantizando una experiencia de compra accesible, rápida y confiable.

---

## 🌟 Características y Módulos Principales

### 1. 🛍️ Portal E-Commerce Omnicanal para Clientes
* **Catálogo Dinámico e Interactivo:** Presentación visual con la identidad corporativa de Tiendas Mass (`#FDCB02` y `#E30613`), filtros por categorías, productos destacados y ofertas bomba.
* **Búsqueda Ultrarrápida con Debounce de 500ms y AbortController:** Búsqueda en tiempo real por nombre, marca o SKU. Cancela peticiones previas en vuelo para evitar condiciones de carrera (*race conditions*) y optimizar el consumo de la red.
* **Modalidad de Entrega Flexible:**
  * **Delivery Programado:** Cotización automática de flete por geolocalización y cálculo de distancia kilométrica (integración con *Google Maps Distance Matrix*).
  * **Recojo en Tienda (*Click & Collect*):** Verificación instantánea de disponibilidad de stock en la sede seleccionada, detección de traslados inter-sucursales y selección de fecha límite de recojo.
* **Flujo Post-Pago y Comprobante Digital:**
  * Soporte para **Compra como Invitado (*Guest Checkout*)** y **Clientes Registrados** (autenticación estricta con DNI de 8 dígitos o Pasaporte).
  * Emisión automática de **Boleta Electrónica (`EB01-XXXXXX`)** con desglose oficial de IGV (18%).
  * Generación de código único y enlace de seguimiento público (`?tracking=PED-XXXX`).
* **Seguimiento de Despacho en Vivo:** Monitoreo del motorizado y estado del delivery (`EN_PREPARACION`, `EN_RUTA`, `ENTREGADO`) conectado a WebSockets en tiempo real.
* **Panel de Accesibilidad Universal (WCAG 2.1 AA):** Alternador de alto contraste, tipografía adaptada para dislexia, escala tipográfica dinámica y anuncios automáticos para lectores de pantalla.

---

### 2. 📊 Panel de Administración Corporativo (Backoffice)
* **Dashboard Ejecutivo con Indicadores Clave (KPIs):**
  * Ventas del día en curso y comparativas mensuales.
  * **Margen de Utilidad Bruta Real:** Cálculo exacto `(Ingresos - Costo Mercadería Vendida) / Ingresos * 100`.
  * Distribución de ingresos por **Métodos de Pago Independientes** (Yape, Plin, Tarjetas de Débito/Crédito y Efectivo contra entrega).
  * **Comparativa Multisede:** Desempeño comercial por sucursal, ticket promedio y volumen transaccional.
* **Gestión del Catálogo Maestro:** Creación, edición, activación/desactivación de productos, control de precios, costos base e importación masiva mediante plantillas Excel.
* **Control Central de Usuarios y Roles:**
  * Administración de accesos para Administradores y Supervisores.
  * **Regla de Negocio Mandatoria:** Todo supervisor debe pertenecer obligatoriamente a una sucursal asignada (validado a nivel de controlador y mediante *triggers* transaccionales en MySQL).
* **Gestión de Banners y Campañas Publicitarias:** Publicación directa de banners para la tienda virtual con programación por vigencia y sede específica.

---

### 3. 🏬 Panel Operativo de Supervisor de Sede
* **Control de Inventarios por Lotes PEPS / FIFO:**
  * Ingreso y recepción de mercadería con registro de lote, costo unitario, fecha de ingreso y fecha de caducidad.
  * Descuento secuencial automático: la mercadería más antigua y con vencimiento más próximo se despacha primero.
* **Matriz de Clasificación ABC (Principio de Pareto 80/20):**
  * Estratificación de productos en Clase A (80% valor de inversión), Clase B (15%) y Clase C (5%).
  * Recálculo automatizado para optimizar las políticas de abastecimiento.
* **Punto de Reorden ($POR$) e Índice de Obsolescencia ($IOI$):**
  * Alertas automáticas basadas en fórmula estocástica: $\text{POR} = (d \times L) + SS$.
  * Semaforización de productos perecederos a 30, 15 y 7 días de caducar (Consumo Responsable).
* **Alertas Críticas de Stock Bajo ($\le 5$ unidades):**
  * Tabla dedicada y disparador (*trigger*) automático que alerta inmediatamente cuando las existencias en tienda llegan a 5 o menos unidades.
* **Módulo de Auditoría de Desmedros y Mermas:**
  * Registro de bajas por caducidad, deterioro, rotura o pérdida de cadena de frío.
  * Identificación obligatoria del usuario responsable, sucursal, lote afectado, impacto económico y ajuste automático al Kardex físico-valorado.
* **Conteos Cíclicos y Auditorías Físicas:**
  * Programación de conteos por estrato ABC, asignación de personal auditor y cálculo de discrepancias contra el sistema.

---

## 🏗️ Arquitectura del Sistema

El proyecto implementa un patrón desacoplado y de alto rendimiento:

```
ANKAR_Software_De_Gestion/
│
├── frontend/                               # Capa de Presentación (Dual Mode)
│   ├── index.html                          # Tienda Virtual Cliente (Ejecución directa en XAMPP)
│   ├── admin.html                          # Backoffice Administrador (Ejecución directa)
│   ├── supervisor.html                     # Portal Supervisor de Sede (Ejecución directa)
│   ├── css/ & js/                          # Estilos corporativos y módulos de accesibilidad
│   ├── assets/                             # Logos oficiales, imágenes de productos y banners
│   └── src/                                # Código fuente SPA modular (React 18 + Vite)
│       ├── interfaz-cliente/               # Vistas y componentes del cliente
│       ├── interfaz-administrador/         # Vistas administrativas y reportes
│       ├── interfaz-supervisor/            # Vistas del supervisor de tienda
│       ├── modules/ & services/            # Servicios de API y lógica compartida
│       └── shared/                         # Utilidades y configuración
│
├── backend/                                # API RESTful en PHP Nativo (MVC Limpio)
│   ├── app/
│   │   ├── Controllers/                    # Controladores (Producto, Pedido, Inventario, Usuario, etc.)
│   │   ├── Repositories/                   # Consultas SQL optimizadas con PDO y Prepared Statements
│   │   ├── Services/                       # Lógica de Negocio (PEPS, ABC, Reorden, Despacho, Maps)
│   │   ├── Middleware/                     # Autenticación JWT, CORS y Validación de Roles (RBAC)
│   │   ├── Helpers/                        # Conexión DB, respuestas JSON estandarizadas y Validador
│   │   └── Routes/                         # Router RESTful con prefijos y middlewares
│   ├── config/config.php                   # Configuración del entorno y credenciales
│   └── public/                             # Front Controller (index.php) y directorio de uploads
│
├── database/                               # Capa de Persistencia Relacional
│   ├── tiendas_mass.sql                    # Script DDL completo con tablas, triggers y seeders
│   └── migrations/                         # Migraciones incrementales de funcionalidades
│
├── node-services/                          # Microservicio de Tiempo Real
│   ├── src/server.js                       # Servidor WebSocket (Socket.IO) para GPS de delivery
│   └── package.json
│
├── docs/ & DOC/                            # Documentación técnica, diagramas y matrices de auditoría
├── .env.example                            # Plantilla de variables de entorno
└── .htaccess                               # Reglas de reescritura de URL para Apache
```

---

## 🛠️ Stack Tecnológico

| Capa | Tecnologías |
| :--- | :--- |
| **Backend** | PHP 8.1 / 8.2+ Nativo, Arquitectura MVC, PDO, JWT (JSON Web Tokens), Apache mod_rewrite |
| **Base de Datos** | MySQL 8.0 / MariaDB, Triggers transaccionales, Stored Procedures, Claves foráneas en Cascada |
| **Frontend (Directo)** | HTML5 Semántico, CSS3, JavaScript ES6+, React 18 UMD, Babel Standalone, Tailwind CSS |
| **Frontend (SPA Modular)** | React 18, Vite 5, React Router DOM 6, Axios, Lucide Icons, Socket.io-client |
| **Microservicio WebSocket** | Node.js 18+, Express, Socket.IO 4.7 |
| **APIs Externas** | Google Maps JavaScript API, Google Distance Matrix API, Places Autocomplete |
| **Entorno de Despliegue** | XAMPP (Apache + MySQL), Linux / Windows Server, Docker-ready |

---

## 🚀 Guía de Instalación y Puesta en Marcha

### Prerrequisitos
* Tener instalado **XAMPP** (con PHP 8.1 o superior y MySQL).
* Git instalado en el equipo.
* (Opcional) Node.js 18+ si se desea levantar el microservicio de seguimiento GPS en vivo.

---

### Paso 1: Clonar el Repositorio en la Carpeta `htdocs` de XAMPP

Abre una terminal o consola de comandos y clona el proyecto dentro del directorio de Apache:

```bash
cd C:\xampp\htdocs
git clone https://github.com/Arny5555/ANKAR_Software_De_Gestion.git tiendasmass
```

---

### Paso 2: Importar la Base de Datos en MySQL

1. Inicia los módulos de **Apache** y **MySQL** desde el Panel de Control de XAMPP.
2. Abre **phpMyAdmin** en tu navegador (`http://localhost/phpmyadmin/`) o ingresa por la terminal de MySQL:
   ```bash
   mysql -u root -p
   ```
3. Ejecuta el script principal ubicado en `database/tiendas_mass.sql`:
   ```sql
   CREATE DATABASE IF NOT EXISTS tiendas_mass_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   USE tiendas_mass_db;
   SOURCE C:/xampp/htdocs/tiendasmass/database/tiendas_mass.sql;
   ```
4. Aplica las migraciones complementarias si se requieren:
   ```sql
   SOURCE C:/xampp/htdocs/tiendasmass/database/migrations/04_nuevas_funcionalidades_ecommerce_inventario.sql;
   ```

---

### Paso 3: Configurar Variables de Entorno

Copia el archivo `.env.example` como `.env` en la raíz del proyecto:

```bash
cd C:\xampp\htdocs\tiendasmass
copy .env.example .env
```

Verifica o ajusta los parámetros de conexión en `.env`:

```env
APP_ENV=development
APP_DEBUG=true
APP_URL=http://localhost/tiendasmass

# Base de Datos
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=tiendas_mass_db
DB_USERNAME=root
DB_PASSWORD=

# JWT y Seguridad
JWT_SECRET=tu_clave_secreta_super_segura_tiendas_mass_2026
JWT_EXPIRATION=86400

# Google Maps API (Opcional para cálculo de rutas en vivo)
GOOGLE_MAPS_API_KEY=
```

---

### Paso 4: Probar la Aplicación en el Navegador

Una vez que Apache y MySQL estén corriendo, accede directamente a las siguientes rutas:

| Módulo | Enlace Local | Descripción |
| :--- | :--- | :--- |
| **Tienda Virtual (Cliente)** | `http://localhost/tiendasmass/` | Catálogo de compras, búsqueda y checkout |
| **Panel Administrador** | `http://localhost/tiendasmass/admin` | Dashboard ejecutivo, reportes, usuarios y catálogo |
| **Panel Supervisor** | `http://localhost/tiendasmass/supervisor` | Gestión de almacén, lotes PEPS, mermas y auditorías |
| **API RESTful (JSON)** | `http://localhost/tiendasmass/backend/public/api/productos` | Endpoint maestro de productos |

---

### Paso 5 (Opcional): Iniciar el Microservicio de Telemetría (Node.js)

Para habilitar la transmisión en tiempo real de la posición de los repartidores:

```bash
cd C:\xampp\htdocs\tiendasmass\node-services
npm install
node src/server.js
```
El servidor de WebSockets escuchará en el puerto `3001`.

---

## 🔐 Credenciales y Usuarios de Demostración

El script `tiendas_mass.sql` incluye usuarios semilla con contraseñas encriptadas con **Bcrypt**:

| Rol | Correo Electrónico | Contraseña | Sucursal Asignada |
| :--- | :--- | :--- | :--- |
| **Administrador** | `admin@tiendasmass.pe` | `Admin123!` | *Acceso Global Corporativo* |
| **Supervisor** | `supervisor.centro@tiendasmass.pe` | `Super123!` | Tienda Mass - Huancayo Centro (ID: 1) |
| **Supervisor** | `supervisor.sancarlos@tiendasmass.pe` | `Super123!` | Tienda Mass - San Carlos (ID: 2) |
| **Cliente Registrado** | `juan.perez@gmail.com` | `Cliente123!` | DNI: `72458912` |

---

## 📡 Resumen de Endpoints de la API REST

### Autenticación y Usuarios
* `POST /api/auth/login`: Autenticación de Administradores y Supervisores (retorna token JWT).
* `POST /api/auth/cliente-login`: Inicio de sesión para clientes compradores.
* `GET /api/auth/me`: Datos del usuario autenticado vía JWT.
* `GET /api/usuarios`: Listado de usuarios internos (Exclusivo Administrador).
* `POST /api/usuarios`: Alta de supervisores con sucursal mandatoria.
* `PUT /api/usuarios/{id}`: Actualización de datos y reasignación de sucursal.
* `PATCH /api/usuarios/{id}/toggle`: Activar o desactivar cuenta de usuario.

### Catálogo y Sucursales
* `GET /api/sucursales`: Listado de sucursales activas con coordenadas geográficas.
* `GET /api/categorias`: Categorías de productos.
* `GET /api/productos`: Catálogo filtrable por sucursal, categoría y término de búsqueda.
* `POST /api/productos`: Registro de nuevo producto en catálogo maestro.
* `POST /api/productos/import-excel`: Carga masiva de productos desde hoja de cálculo.

### Inventarios, Lotes y Algoritmos Inteligentes
* `GET /api/inventarios`: Existencias consolidadas por sucursal.
* `GET /api/lotes`: Listado detallado de lotes con fechas de ingreso y vencimiento.
* `POST /api/lotes/recepcion`: Entrada por compra con registro de nuevo lote PEPS y actualización en Kardex.
* `GET /api/inventarios/low-stock-alerts`: Listado de productos con stock crítico $\le 5$ unidades.
* `POST /api/inventarios/mermas`: Registro de desmedro/merma con auditoría de usuario y rebaja en PEPS.
* `GET /api/inventarios/abc`: Clasificación de productos según el valor de rotación (Pareto 80/20).
* `GET /api/inventarios/reorder-alerts`: Alertas de reposición según Punto de Reorden ($POR$).
* `GET /api/inventarios/obsolescence`: Análisis de lotes próximos a vencer ($IOI$).
* `GET /api/inventarios/kardex`: Reporte físico-valorado de movimientos.

### Pedidos, Ventas y Tracking
* `POST /api/pedidos/validar-stock-recojo`: Validación de existencias inmediatas en la sede elegida.
* `POST /api/pedidos`: Creación de pedido, asignación y deducción secuencial de lotes PEPS, y emisión de Boleta Electrónica.
* `GET /api/pedidos/seguimiento/{codigo}`: Consulta pública de estado y tracking de pedido.
* `POST /api/delivery/cotizar`: Estimación de tarifa de envío y validación de radio de cobertura.

### Reportería y KPIs
* `GET /api/reportes/dashboard-kpi`: Resumen ejecutivo de métricas clave.
* `GET /api/reportes/general-admin`: Reporte detallado con Ventas Día, Ventas Mes, Margen de Utilidad Bruta y Métodos de Pago.
* `GET /api/reportes/mermas`: Reporte histórico de desmedros valorizados.

---

## ⚖️ Licencia y Créditos

Desarrollado para el proyecto de modernización y gestión comercial omnicanal **ANKAR Software de Gestión** (Tiendas Mass).  
Todos los derechos reservados © 2026.
