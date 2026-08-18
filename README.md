# 🧛 Compendio de Disciplinas - Vampiro: La Mascarada (V5)

Aplicación web interactiva y gestor de cartas imprimibles para **Vampiro: La Mascarada (5ª Edición)**. Diseñada específicamente para jugadores y Narradores que buscan consultar y gestionar de forma rápida las disciplinas, rituales, ceremonias y fórmulas alquímicas del Mundo de Tinieblas, respetando la estética oficial y optimizando los datos para evitar duplicidades.

---

## 🛠️ Tecnologías y Librerías Utilizadas
* **HTML5 / CSS3 / JavaScript (Vanilla)** (Estructura y lógica interactiva sin frameworks pesados).
* **PapaParse.js** (Para la lectura y procesamiento en tiempo real de archivos CSV alojados en Google Sheets).
* **Google Fonts (`Cinzel` y tipografías institucionales)** para emular el diseño formal de los manuales de V5.

---

## ✨ Características Principales

1. **Conexión Dinámica con Google Sheets:** 
   * Carga automática de la base de datos principal de poderes mediante CSV.
   * Lectura de fuentes editoriales desde una pestaña auxiliar para unificar los nombres de los manuales (Libro Básico, Guía de Juego, Sellos de Sangre, Sabbat, etc.).
2. **Sistema de Temas Dual (Noche / Día):**
   * *Modo Noche (Medianoche Vampírica):* Tonos oscuros de alta elegancia con detalles dorados y acentos en rojo sangre (`--accent-red`).
   * *Modo Día (Gris Pizarra / Pergamino Neutro):* Estética clara adaptada para una lectura cómoda bajo cualquier circunstancia, con tarjetas limpias sobre fondo neutro.
3. **Filtros Avanzados e Intuitivos:**
   * Buscador en tiempo real por nombre en castellano, nombre en inglés, efecto o descripción.
   * Filtro por nivel (del 1 al 5 y opción de mostrar todos).
   * Filtro por fuente o libro oficial.
   * Botonera principal por Disciplina (con iconos oficiales integrados) y **subcategorías dinámicas** (Poderes Estándar, Amalgamas, Rituales, Ceremonias, Fórmulas) que aparecen automáticamente según la disciplina seleccionada.
4. **Diseño de Tarjetas Optimizadas:**
   * Títulos principales en negrita y versalitas (`small-caps`).
   * Nombre en inglés situado de forma sutil y cercana justo debajo del título principal.
   * **Cuadro rojo vino (`#5c101c`)** destacado para indicar claramente el nivel de la disciplina.
   * Referencia de libro y página limpia en la esquina superior derecha en dos líneas.
   * Cajas de tiradas de dados y notas adicionales integradas visualmente.
5. **Versión Imprimible de Cartas (Formato Tabla / Grid):**
   * Estructura pensada para maquetación de 9 cartas por página en formato A4 (medidas estándar tipo carta de póker).
   * Fondo blanco transparente y uso de logotipos en marca de agua con opacidad para un máximo ahorro de tinta en impresión física.

---

## 📂 Estructura del Repositorio

```text
├── index.html            # Archivo principal con toda la lógica web, estilos CSS y motor de renderizado
├── README.md             # Documentación oficial del proyecto
└── iconos/               # Carpeta con los recursos gráficos e iconografía oficial V5
    ├── drRol.png         # Favicon de la aplicación
    ├── VTM-Ank.png       # Ankh oficial de Vampiro V5
    ├── VTM-Logo-Largo.png# Logotipo principal de la línea
    └── *_symbol.png      # Iconos vectoriales específicos de cada Disciplina (Animalismo, Auspex, etc.)
```
## 📊 Criterio de Consolidación de Datos (Fuentes y Erratas)
Para mantener la base de datos limpia de duplicados y errores mecánicos, se sigue estrictamente la jerarquía oficial de publicaciones de V5:

* **Guía de Juego (Player's Guide):** Prioridad absoluta para unificar reglas, erratas y poderes de clanes recopilados.
* **Sellos de Sangre (Blood Sigils):** Fuente de referencia principal para Hechicería de Sangre y Alquimia de Sangre Débil.
* **Suplementos Específicos (Sabbat, Chicago Nocturno, etc.):** Usados para mecánicas de trasfondo exclusivas que no hayan sido reeditadas posteriormente.

---

## 📜 Aviso Legal
Esta aplicación es una herramienta/ayuda de juego no oficial para jugadores y Narradores, creada sin ánimo de lucro. *Vampiro: La Mascarada*, *Mundo de Tinieblas* y sus logotipos son marcas registradas de **Paradox Interactive AB**. El material original y sus traducciones oficiales pertenecen a Paradox Interactive, White Wolf y Nosolorol Ediciones.
