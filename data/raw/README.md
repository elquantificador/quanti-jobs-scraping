# Raw Data

## Purpose
Contiene los cortes acumulados de ofertas publicas usados como insumo del analisis reproducible.

## Contents
Los cortes `ofertas_2026-06-17.csv`, `ofertas_2026-07-16.csv` y `ofertas_2026-07-26.csv` no se publican en el repositorio (contienen contenido de terceros). Coloca aqui tus copias para replicar el analisis. Ver `DATA-NOTICE.md`.

## Naming Convention
Cada archivo usa la fecha del corte en formato `YYYY-MM-DD`.

## Dependencies
Estos archivos se leen directamente en `code/cleaning/01_build_analysis_sample.R`, que acumula los cortes de junio y julio y luego elimina duplicados entre publicaciones repetidas.
