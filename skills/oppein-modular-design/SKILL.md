---
name: oppein-modular-design
description: "Diseño generativo, modulación milimétrica industrial y mapeo de catálogo de productos Oppein. A partir de bocetos o planos técnicos (CAXA/CAD/mano alzada), vincula automáticamente los productos del catálogo oficial para generar despieces con etiquetas [01], [02], cotas de medidas exactas y órdenes de fabricación listas para fábrica."
argument-hint: "[tipo-mueble-o-boceto] [dimensiones] [acabados-y-serie]"
version: "2.0.0"
author: "WilliamAWSOFTWARE (riune)"
license: "MIT"
---

# Oppein Modular Design 📐🚪
### Sistema Experto de Modulación, Catálogo de Productos y Despiece Etiquetado

Esta skill implementa la lógica de modulación milimétrica, ergonomía y estándares de producción industrial de **Oppein**. Convierte cualquier boceto (de CAXA, software Oppein CAD, o dibujo preliminar a mano) en una modulación estandarizada, ergonómica, alimentada con el catálogo oficial de productos y lista para fabricación y renderizado fotorrealista con etiquetas técnicas y cotas de medidas.

---

## 📦 1. Catálogo Base de Productos Oppein

Cada módulo identificado en un boceto se mapea con su código oficial, nombre de producto, medidas estándar y herrajes europeos:

### Cocinas Modulares (Kitchen Series):
| Código Oppein | Nombre de Producto | Dimensiones Estándar (W x D x H mm) | Descripción & Accesorios | Herrajes |
| :--- | :--- | :--- | :--- | :--- |
| **`OP-BC-600-2D`** | Gabinete Bajo 2 Gavetas Caceroleras | `600 x 560 x 780` | Gavetas de extracción total para ollas y vajillas pesadas. | Blum Tandembox / Soft-close 50kg |
| **`OP-BC-900-2D`** | Gabinete Bajo 2 Gavetas Anchas | `900 x 560 x 780` | Módulo principal bajo placa de cocción o isla. | Blum Blumotion con organizador interno |
| **`OP-BC-900-SINK`** | Módulo Fregadero Bajo Encimera | `900 x 560 x 780` | Fondo revestido en lámina de aluminio hidrófugo anticorrosión. | Bisagras Blum Clip Top 110° con freno |
| **`OP-BC-150-SPICE`** | Módulo Botellero / Especiero | `150 x 560 x 780` | Carrito extraíble de acero inoxidable 304 de 2 niveles. | Guías ocultas con cierre amortiguado |
| **`OP-BC-CRN-900`** | Módulo Rinconero Mágico | `900/1050 x 560 x 780` | Bandejas articuladas extraíbles tipo "Magic Corner". | Sistema de extracción telescópico asistido |
| **`OP-WC-600`** | Gabinete Aéreo 1 Puerta Batiente | `600 x 350 x 720/840` | Repisas interiores graduables con soporte anti-vuelco. | Blum Clip Top Blumotion 110° |
| **`OP-WC-900-AV`** | Gabinete Aéreo Doble Puerta Plegable | `900 x 350 x 720/840` | Puerta doble elevable con frente de vidrio bronce / laca. | Sistema de elevación Blum Aventos HF |
| **`OP-TALL-600-OV`** | Columna Torre de Hornos | `600 x 580 x 2150/2400`| Nichos empotrados para horno microondas y horno convencional. | Ventilaciones térmicas traseras integradas |
| **`OP-TALL-600-PAN`** | Columna Despensa Extraíble | `600 x 580 x 2150/2400`| Despensa alta con 5 cestas cromadas de extracción sincronizada. | Guías pesadas de extracción total 80kg |
| **`OP-IS-1800-WF`** | Isla Central con Cascada | `1800 x 950 x 900` | Barra desayunadora en voladizo (300mm) y gavetas dobles. | Encimera cuarzo/piedra sinterizada en cascada |

### Clósets y Vestidores (Wardrobe Series):
| Código Oppein | Nombre de Producto | Dimensiones Estándar (W x D x H mm) | Configuración Interior |
| :--- | :--- | :--- | :--- |
| **`OP-CL-DR-500`** | Módulo Cajonero con Joyero Superior | `500 x 550 x 1000` | 3 gavetas + 1 joyero superior con divisores de terciopelo y tapa de cristal templado. |
| **`OP-CL-SH-800`** | Módulo Zapatero Inclinado | `800 x 400 x 1200` | 5 bandejas inclinadas con tope metálico y luz LED rasante en perfil. |
| **`OP-CL-HANG-1000`** | Módulo Colgado Abatible | `1000 x 550 x 1200` | Barra hidráulica basculante abatible para aprovechar altura hasta 2600mm. |
| **`OP-CL-TOWER-600`** | Módulo Estantería Abierta | `600 x 500 x 2400` | Repisas abiertas con iluminación LED vertical empotrada en fresado 45°. |

---

## 🍳 2. Estándares y Secciones de Cocinas Modulares Oppein

```
       ┌──────────────────────┐  ▲ Profundidad: 350 mm
       │   GABINETES AÉREOS   │  │ Altura: 600 / 720 / 840 / 900 mm
       └──────────────────────┘  ▼
             ▲ Salpicadero / Backsplash: 550 - 650 mm
             ▼
   ══════════════════════════════ Encimera (Cuarzo / Piedra Sinterizada 20-30mm)
       ┌──────────────────────┐  ▲ Altura caja: 750 - 800 mm
       │   GABINETES BAJOS    │  │ Profundidad mueble: 560 mm (Encimera: 600-650 mm)
       ├──────────────────────┤  ▼
       │   Zócalo (80-100mm)  │  ▲ Altura final de trabajo: 880 - 920 mm
```

---

## 🏷️ 3. Generación de Lista con Etiquetas Técnicas y Medidas (BOM)

A partir de cualquier boceto Oppein suministrado (plano en planta o elevación), la skill genera una **capa de anotación con etiquetas [01], [02], [03]** que vinculan la imagen con una lista técnica estructurada:

```
ELEVACIÓN PRINCIPAL COCINA (Pared 3450 mm):

 [01]          [02]                 [03]          [04]         [05]
┌────────────┬────────────────────┬────────────┬────────────┬──────────┐
│ OP-BC-900  │   OP-BC-900-SINK   │ OP-BC-900  │ OP-BC-600  │ AJUSTE   │
│ Gavetero   │ Módulo Fregadero   │ Placa Ind. │ Especiero  │ Regleta  │
│ 900x560mm  │ 900x560mm          │ 900x560mm  │ 600x560mm  │ 150mm    │
└────────────┴────────────────────┴────────────┴────────────┴──────────┘
 ◄── 900mm ──►◄───── 900mm ──────►◄── 900mm ──►◄── 600mm ──►◄─ 150mm ─►
```

| Etiqueta | Código Oppein | Nombre de Producto | Medidas (W x D x H) | Acabado Puerta Oppein | Tirador / Herraje |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **`[01]`** | `OP-BC-900-2D` | Gavetero Bajo 2 Caceroleras | `900 x 560 x 780 mm` | Laca Super-Mate Gris Cachemira | Perfil Gola Negro Anodizado / Blum |
| **`[02]`** | `OP-BC-900-SINK`| Módulo Fregadero Bajo Encimera | `900 x 560 x 780 mm` | Laca Super-Mate Gris Cachemira | Bisagras Blum Clip Top Blumotion 110° |
| **`[03]`** | `OP-BC-900-2D` | Gavetero Placa de Inducción | `900 x 560 x 780 mm` | Laca Super-Mate Gris Cachemira | Guías ocultas Blum 50kg soft-close |
| **`[04]`** | `OP-BC-600-SPICE`| Módulo Despensa Baja / Especiero | `600 x 560 x 780 mm` | Laca Super-Mate Gris Cachemira | Extracción telescópica asistida |
| **`[05]`** | `OP-REG-150` | Regleta de Ajuste a Pared | `150 x 18 x 780 mm` | Laca Super-Mate Gris Cachemira | N/A (Fijación oculta) |
| **`[06]`** | `OP-WC-900-AV` | Gabinete Aéreo Doble Plegable | `900 x 350 x 840 mm` | Vidrio Bronce marco aluminio negro | Elevador Blum Aventos HF + LED 2700K |

---

## ⌨️ Comandos Rápidos

* **`/oppein sketch [tipo-boceto]`**: Procesa un boceto preliminar de Oppein y genera la modulación optimizada.
* **`/oppein bom [medidas-o-espacio]`**: Genera la lista con etiquetas `[01], [02]...`, códigos de producto Oppein, medidas y herrajes.
* **`/oppein kitchen [medidas] [serie]`**: Modulación milimétrica de cocina Oppein con serie específica.
* **`/oppein closet [medidas] [estilo]`**: Distribución de vestidor con módulos organizadores, joyeros y zapateras.
