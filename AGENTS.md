# Instrucciones para Agentes de IA (AGENTS.md) - Proyecto EverShop

## 1. Contexto del Proyecto
Este repositorio contiene un proyecto basado en **EverShop**, una plataforma de comercio electrónico "Developer-Centric". 
* **Arquitectura:** Monolito Modular (Modular Monolith) y Headless.
* **Stack Tecnológico:**
  * **Backend:** Node.js, Express.
  * **API:** GraphQL (Apollo Server).
  * **Frontend (Storefront & Admin):** React, Tailwind CSS.
  * **Base de Datos:** PostgreSQL.
  * **Lenguaje Principal:** TypeScript / JavaScript (ES6+).

## 2. Reglas Arquitectónicas Estrictas (Módulos)
La regla de oro de este proyecto es la **modularidad**. Todo el código debe estar encapsulado en módulos independientes.
* **No crear dependencias circulares:** Un módulo no debe depender directamente de la lógica interna de otro módulo de forma acoplada.
* **Interacción entre módulos:** La comunicación debe darse a través de eventos, hooks o la capa de GraphQL, nunca modificando directamente las tablas de otro módulo en la base de datos.
* **Ubicación:** Las nuevas funcionalidades o integraciones deben crearse como un módulo nuevo dentro de la carpeta correspondiente (por ejemplo, `/modules/tu-nuevo-modulo`), o extender un módulo existente utilizando los mecanismos de extensión de EverShop.

## 3. Guías de Desarrollo por Capas

### Base de Datos (PostgreSQL)
* **Esquemas:** Utiliza sentencias SQL estándar compatibles con PostgreSQL.
* **Migraciones:** Cualquier cambio en la base de datos (creación de tablas, alteración de columnas) DEBE realizarse a través de scripts de migración formales dentro de la carpeta de migraciones del módulo correspondiente.
* **Nomenclatura:** Usa `snake_case` para tablas y columnas.

### Backend y API (Node.js & GraphQL)
* **GraphQL First:** Cualquier dato que necesite el frontend debe ser expuesto a través de consultas (Queries) o mutaciones (Mutations) de GraphQL.
* **Resolvers:** Mantén los resolvers delgados. La lógica de negocio pesada debe residir en servicios o controladores separados que el resolver invoca.
* **Seguridad:** Valida siempre los permisos y la autenticación en el contexto del resolver antes de ejecutar mutaciones sensibles.

### Frontend (React & Tailwind CSS)
* **Componentes Funcionales:** Usa exclusivamente componentes funcionales de React y Hooks. No utilices componentes de clase.
* **Estilos:** Utiliza Tailwind CSS para todo el estilizado. Evita crear archivos CSS o SCSS personalizados a menos que sea estrictamente necesario para animaciones complejas de terceros.
* **Consultas de Datos:** Utiliza los hooks proporcionados por el ecosistema de EverShop (o Apollo Client) para consumir la API GraphQL. Maneja siempre los estados de carga (`loading`) y error (`error`).

## 4. Flujo de Trabajo del Agente de IA
Cuando se te asigne una tarea (crear una función, editar un bug o refactorizar), debes seguir este proceso:

1. **Análisis de Impacto:** Antes de escribir código, identifica qué módulos existentes se verán afectados.
2. **Revisión de Esquemas:** Si la tarea involucra datos, define primero cómo cambiará el esquema de la base de datos y el esquema de GraphQL (`schema.graphql`).
3. **Desarrollo Iterativo:** * Escribe el código del backend/API primero.
   * Escribe el código del frontend después.
4. **Validación:** Asegúrate de que no haya errores de TypeScript (si aplica) y que los nombres de variables sigan las convenciones del proyecto (`camelCase` para JS/TS, `PascalCase` para componentes React).
5. **Documentación:** Si creas un nuevo módulo, añade un archivo `README.md` corto dentro de su directorio explicando su propósito.

## 5. Comandos Frecuentes de Referencia
* *(Agente: Ten en cuenta estos comandos para entender el ciclo de vida del proyecto)*
* Instalación: `npm install`
* Construcción: `npm run build`
* Desarrollo: `npm run dev`