# Proyecto LaTeX - Notas y Apuntes

Este proyecto contiene documentos LaTeX para notas universitarias, cursos de Platzi y talleres.

## Estructura del Proyecto

- **notas_u/**: Notas de cursos universitarios como Análisis Matemático, Ecuaciones Diferenciales, etc.
- **platzi/**: Apuntes de cursos de Platzi como Programación en Go, Introducción al Desarrollo Backend, etc.
- **taller final tex/**: Taller final con documentos y recursos.

Cada directorio incluye archivos fuente `.tex`, imágenes y archivos compilados en `build/`.

## Uso

Para compilar los documentos LaTeX, usa un compilador como pdflatex o latexmk.

Ejemplo:
```
latexmk archivo.tex
```

## Construcción

Los PDFs compilados se generan en los subdirectorios `build/`.