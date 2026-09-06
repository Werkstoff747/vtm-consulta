# Censo de Vástagos — Chicago (Módulo de Consulta)

Este repositorio contiene la aplicación web ligera de consulta para el censo de personajes de nuestra crónica de *Vampiro: La Mascarada 5ª Edición*. Está diseñada como una *Single Page Application* (SPA) que se conecta directamente a una hoja de cálculo en la nube para sincronizar dinámicamente la información de la Jyhad local.

---

## 1. Resumen de la Parte del Proyecto

Este módulo (`vtm-consulta`) actúa como el directorio público y privado de la crónica. Permite a los jugadores consultar los PNJs de la ciudad según su nivel de conocimiento, mientras proporciona al Narrador una puerta trasera protegida por contraseña para auditar secretos, fichas profundas y personajes ocultos sin necesidad de recargar la aplicación ni mantener bases de datos complejas.

---

## 2. Estructura y Funcionamiento de `index.html`

El archivo principal agrupa toda la interfaz, los estilos CSS adaptados a la estética oficial de V5 (con soporte para modo claro/oscuro) y la lógica JavaScript de procesamiento.

*   **Carga de Datos Asíncrona:** Utiliza la librería *PapaParse* para leer en tiempo real un archivo CSV publicado desde Google Sheets (`SHEET_CSV_URL`).
*   **Motor de Renderizado (`renderVampiros`):** Recorre los registros, ordena los personajes de forma numérica según su ID y construye dinámicamente las tarjetas en el DOM.
*   **Filtrado y Búsqueda en Vivo:** Escucha los eventos de la barra de búsqueda y del selector de facciones (`applyFilters`), actualizando el contador de resultados de manera instantánea sin latencia.
*   **Control de Acceso (Modo Narrador):** Se comunica con *Firebase Realtime Database* para verificar una palabra de pase cifrada. Al validarla, añade la clase `narrator-mode` al cuerpo del documento, revelando información clasificada mediante reglas CSS.

---

## 3. Lógica de Visibilidad y Uso de Etiquetas

Para simular la filtración de información y el dominio público de la Camarilla, el sistema evalúa el campo **Estatus** y la presencia de cargos institucionales de forma automatizada:

*   **Interactuado:** El grupo de jugadores ha tratado directamente con el PNJ. Se muestra la tarjeta completa con su retrato, clan, facción, ocupación y ubicación. Su etiqueta superior derecha es de color verde.
*   **Conocido de Oídas:** Información de corrillo o referencias generales en la ciudad. La tarjeta mantiene datos visibles pero con un enfoque más superficial. Su etiqueta superior derecha muestra un verde sutil y clarito.
*   **Rumor:** Nivel mínimo de información flotante en las calles (por ejemplo, leyendas urbanas). La tarjeta oculta todos los detalles profundos e imagen, renderizando únicamente el nombre en una vista minimalista con una etiqueta de estatus en gris.
*   **Oculto / Desconocido:** Personajes totalmente fuera del radar de los jugadores o información reservada de trama. La tarjeta no se renderiza en absoluto en el DOM para los usuarios estándar.
*   **Modo Narrador (Desbloqueado):** Fuerza la visibilidad absoluta de todas las tarjetas (incluyendo las ocultas) y destapa los bloques privados (*Sire*, *Menciones*, *Ficha* y *Secretos*).

---

## 4. Funcionamiento de `ficha.html`

`ficha.html` es la vista detallada e individual para profundizar en la historia de un personaje específico.

*   **Lectura de Parámetros por URL:** Captura el identificador mediante la *query string* (ej. `ficha.html?id=01`) para consultar el registro exacto dentro de la base de datos de Google Sheets.
*   **Desglose Narrativo:** Diseñada para mostrar las notas profundas del PNJ, sus vínculos de sangre (*Sire*), trasfondo ampliado y conexiones políticas dentro de la críptica sociedad de Chicago.

---

## 5. Guía de Despliegue: Monta tu Propia Crónica

Si deseas clonar esta estructura para dirigir tu propia crónica de rol, los archivos necesarios y los pasos de configuración son los siguientes:

### Archivos Necesarios en el Repositorio

```text
/
├── index.html          # Panel principal del censo y buscador
├── ficha.html          # Vista detallada de trasfondos individuales
├── iconos/             # Directorio de recursos gráficos y símbolos de clan
└── retratos/           # Directorio de imágenes de los Vástagos (nombradas por ID o Slug)
```

### Pasos para el Despliegue

1. **Configurar la Base de Datos (Google Sheets):**
   * Crea una hoja de cálculo con las 13 columnas obligatorias: `ID`, `Archivo de Imagen`, `Nombre del Personaje`, `Clan`, `Profesion_Ocupacion`, `Ubicación / Dominio habitual`, `Facción`, `Sire / Creador`, `Ficha / Perfil`, `Menciones`, `Secretos`, `Cargo_Oficial` y `Estatus`.
   * Publica la hoja en la Web en formato CSV (*Archivo* > *Compartir* > *Publicar en la web* > *Valores separados por comas*).
   * Sustituye la constante `SHEET_CSV_URL` en el código de `index.html` por tu nuevo enlace de publicación.

2. **Configurar la Autenticación (Firebase):**
   * Crea un proyecto gratuito en Firebase y habilita *Realtime Database*.
   * Crea un nodo raíz llamado `password_narrador` que contenga la contraseña que usarán los narradores para desbloquear el modo oculto.
   * Actualiza el objeto `firebaseConfig` dentro del bloque `<script type="module">` de tu `index.html`.

3. **Aprovisionar Activos Visuales:**
   * Coloca los iconos oficiales de clanes en la ruta `./iconos/clanes/`.
   * Sube los retratos de los PNJs a la carpeta `./retratos/` asegurándote de que coincidan con los nombres especificados en la columna de la hoja de cálculo (por defecto vincula por ID, ej: `01.jpg`).

4. **Publicar en la Web:**
   * Sube los archivos a un repositorio de GitHub y activa *GitHub Pages* en la rama principal (`main` / `root`) para tener la aplicación en línea de forma gratuita e instantánea.
