# AstroProcess: Pipeline Completo de Astrofotografía

Notebook interactiva para procesar imágenes astrónomicas desde archivos FITS crudos
hasta una imagen final en color.

### Modos soportados:

| Modo | Filtros | Asignación de color | Uso típico |
|------|---------|--------------------|-----------| 
| **SHO** (Paleta Hubble) | SII, Ha, OIII | S&rarr;R, H&rarr;G, O&rarr;B | Nebulosas de emisión |
| **RGB** (Color natural) | R, G, B | R&rarr;R, G&rarr;G, B&rarr;B | Galaxias, cúmulos |
| **HaRGB** | R, G, B + Ha | Ha se mezcla en luminancia roja | Galaxias con regiones HII |
| **HaOIII-RGB** | R, G, B + Ha + OIII | Ha&rarr;R, OIII&rarr;B mezclados con RGB | Objetos mixtos |

Todos los modos soportan **Luminancia (L)** opcional para agregar detalle.

### Características:

- Auto-detección de objetos y filtros disponibles
- Calibración completa (bias, dark, flat, pedestal)
- Alineación **interactiva con sliders** (resultado en vivo)
- Post-procesamiento **interactivo con sliders**
- Explicaciones en cada paso

---
## Referencia rápida

### Pipeline completo:

```
  FITS crudos
     |
  [1] Calibración: (light - (dark - pedestal)) / flat
     |
  [2] Alineación intra-filtro (phase correlation)
     |
  [3] Apilado (mediana)
     |
  [4] Alineación inter-filtro (sliders interactivos)
     |
  [5] Composición (SHO o RGB) + stretch
     |
  [6] LRGB (opcional)
     |
  [7] Post-procesado (sliders interactivos)
     |
  PNG + TIFF finales
```

### Parámetros por modo:

| Parámetro | SHO | RGB | HaRGB / HaOIII-RGB |
|-----------|-----|-----|---------------------|
| STRETCH | 0.05-0.1 | 0.2-0.5 | 0.2-0.5 |
| GAMMA | 3.0-4.0 | 2.0-3.0 | 2.0-3.0 |
| SAT_FACTOR | 1.5-2.5 | 1.0-1.5 | 1.2-1.8 |
| SCNR | 0.7-0.9 | >1.0 (off) | >1.0 (off) |
| G_FACTOR | 0.7-0.8 | 1.0 | 1.0 |
| NB_MIX | n/a | n/a | 0.2-0.5 |

### Problemas comunes:

| Problema | Solución |
|----------|----------|
| Imagen muy oscura | Bajar STRETCH, subir GAMMA o Gamma extra |
| Imagen muy verde | Bajar G en post-procesado, bajar SCNR |
| Imagen púrpura | Subir SCNR (a 0.95+), bajar B |
| Colores debiles/grises | Subir Saturación (siempre &ge; 1.0!) |
| Estrellas con franjas | Ajustar sliders de alineación |
| Mucho ruido | Subir Denoise (7-9) o capturar más frames |

### Para procesar otro objeto:

1. Vuelve al **Paso 4** y selecciona otro objeto en el dropdown
2. Selecciona el modo deseado (el dropdown se actualiza automáticamente)
3. Ejecuta todas las celdas de nuevo (Kernel &rarr; Restart & Run All)

### Para mejorar la captura:

- Más frames por filtro (10-20) mejora el SNR dramáticamente
- Mas exposición de luminancia (5-10 &times; 300s) para LRGB efectivo
- Dithering entre frames elimina patrones del sensor
- La calidad es proporcional al **tiempo total de integración**

### Si los sliders no aparecen:

```python
!pip install ipywidgets ipympl
!jupyter nbextension enable --py widgetsnbextension
```

Si usas JupyterLab: `!jupyter labextension install @jupyter-widgets/jupyterlab-manager`

Si `%matplotlib widget` da error, reemplázalo por `%matplotlib inline` en la celda de imports.
