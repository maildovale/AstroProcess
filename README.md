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
