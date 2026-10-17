# Ficha del artículo

Completa esta ficha al crear el repositorio y mantenla al día. Es el único
lugar con datos propios del artículo; el README es igual en todos los
repositorios.

## Identificación

- **Título:** ¿Qué quieren los empleadores ecuatorianos cuando buscan perfiles de datos?
- **Autoría:** Daniel Sánchez Pazmiño
- **Fecha de publicación:** 2026-08-06
- **Artículo publicado:** https://elquantificador.org/post/economia/2026-08-06-que-quieren-los-empleadores-ecuatorianos/
- **Categoría:** Economía
- **Edición:** Julio-Diciembre 2026

## Estado

Publicado el 2026-08-06. En el sitio, el repositorio enlazado es `dsanchezp18/quanti-jobs-scraping`; este es su repositorio en la organización. El borrador `final_version/index.Rmd` usa un slug distinto del publicado; el título coincide.

## Pregunta y alcance

El artículo pregunta qué piden hoy los empleadores ecuatorianos cuando contratan perfiles vinculados a datos, con foco en herramientas y competencias técnicas. Usa ofertas laborales públicas de Multitrabajos, Computrabajo y Mipleo, acumuladas en tres cortes entre el 17 de junio y el 26 de julio de 2026, con cobertura nacional. La unidad de análisis es la oferta única por portal y anuncio: 1.536 registros brutos, 916 ofertas únicas, 523 en el universo analítico y 457 con habilidades declaradas.

## Requisitos

- R: no documentada en el repositorio (los scripts terminan con `sessionInfo()`, pero su resultado no se guardó).
- Paquetes de R: dplyr, forcats, ggplot2, readr, scales, stringr, svglite, tibble, tidyr.

## Fuentes de datos

| Fuente | Institución | Periodo | Acceso | Script |
|---|---|---|---|---|
| Ofertas laborales públicas de Multitrabajos, Computrabajo y Mipleo (tres cortes acumulados) | Portales Multitrabajos, Computrabajo y Mipleo; recolección por un pipeline separado de LIDE, no publicado | 2026-06-17 a 2026-07-26 | Manual: los cortes crudos ya no se publican y se guardan en Google Drive (carpeta "Habilidades en ofertas de datos Ecuador 2026", id `1Z_-KHkDkI-1l5l89uROfBb5n_A8HZqAz`) | `code/cleaning/01_build_analysis_sample.R` lee `data/raw/` |

Los cortes `ofertas_2026-06-17.csv`, `ofertas_2026-07-16.csv` y `ofertas_2026-07-26.csv` contienen texto de ofertas, nombres de empresas y enlaces de portales de terceros, por lo que LIDE decidió no publicarlos (ver `DATA-NOTICE.md`). Se guardan en la carpeta de Google Drive indicada; para obtenerlos, escribe a elquantificador@laboratoriolide.org y colócalos en `data/raw/`. El código de scraping no forma parte de este repositorio. Ni el repositorio ni el artículo citan una dirección oficial de cada portal.

## Salidas

- `outputs/tables/`: `embudo_muestra.csv` y `cortes_acumulados.csv` (conteos del filtrado y de los cortes); `herramientas_demandadas.csv`, `competencias_tecnicas.csv`, `habilidades_suaves.csv` y `combinaciones_herramientas.csv` (menciones en ofertas con habilidades); `familias_ocupacionales.csv`, `skills_familias_principales.csv`, `fuentes_ofertas.csv`, `ciudades_ofertas.csv` y `modalidad_ofertas.csv` (composición del universo por familia, portal, ciudad y modalidad).
- `outputs/figures/`: `familias_ocupacionales`, `herramientas_demandadas`, `competencias_tecnicas` y `habilidades_suaves`, en `.png` y `.svg`.
- `outputs/mercado_datos_resumen.rds`: resumen serializado de las tablas.
- `final_version/images/grafico1` a `grafico4` (`.png` y `.svg`): copias numeradas de las figuras según el orden del texto (1 familias, 2 herramientas, 3 competencias, 4 habilidades suaves).
- `data/intermediate/ofertas_unicas.rds`, `data/final/ofertas_universo_analitico.csv` y `data/final/ofertas_con_habilidades.csv`: se generan al correr el flujo y no se versionan.

## Cómo replicar en este repositorio

1. Abre el proyecto desde la raíz del repositorio e instala los paquetes de la lista de requisitos.
2. Obtén los tres cortes crudos de la carpeta de Google Drive "Habilidades en ofertas de datos Ecuador 2026" (id `1Z_-KHkDkI-1l5l89uROfBb5n_A8HZqAz`; pide acceso a elquantificador@laboratoriolide.org) y colócalos en `data/raw/`. El script de limpieza se detiene si no encuentra archivos de junio o julio.
3. Corre `source("MASTER.R")`. Ejecuta en orden `code/cleaning/01_build_analysis_sample.R` (acumula los cortes, elimina duplicados por portal y anuncio, filtra el universo analítico y la submuestra con habilidades) y `code/analysis/01_market_tools_outputs.R` (tablas, figuras, resumen `.rds` y copia de las figuras a `final_version/images/`).
4. Para ver el artículo: `quarto render final_version/index.Rmd --to html --embed-resources`. El HTML no se versiona.

Sin los cortes crudos solo se pueden consultar las tablas agregadas de `outputs/tables/`.

## README anterior

Texto del README de este repositorio antes de adoptar el README estándar,
conservado sin cambios de contenido para no perder información.

### quanti-jobs-scraping

#### Overview

Analisis reproducible en R del mercado laboral de datos en Ecuador, con foco en las herramientas y competencias tecnicas que aparecen en ofertas publicas de empleo.

Este repositorio usa cortes acumulados de ofertas laborales publicas en Multitrabajos, Computrabajo y Mipleo, tomados entre el 17 de junio y el 26 de julio de 2026. Contiene el dataset de entrada para el analisis, el codigo para construir la muestra analitica y las salidas que alimentan un articulo tecnico de El Quantificador. No publica el codigo de scraping ni su metodologia detallada.

#### How to Replicate

1. Abre el proyecto desde la raiz del repositorio.
2. Verifica que tengas instalados `dplyr`, `ggplot2`, `readr`, `scales`, `stringr` y `tidyr`.
3. Corre `source("MASTER.R")`.

`MASTER.R` acumula los cortes disponibles de junio y julio, construye la muestra analitica y luego exporta tablas, figuras y un resumen serializado.

#### Project Structure

```text
.
├── MASTER.R
├── borrador_articulo_quantificador.md
├── code/
│   ├── cleaning/
│   └── analysis/
├── data/
│   ├── raw/
│   ├── intermediate/
│   └── final/
├── outputs/
│   ├── figures/
│   └── tables/
└── documentation/
    └── archive/
```

#### Data Access

Los insumos provienen de un pipeline de recoleccion separado que consolida ofertas laborales publicas para roles de datos y tecnologia en Ecuador. La capa de scraping se documenta por separado y por ahora no se transparenta en este repositorio.

Los cortes crudos (`ofertas_2026-06-17.csv`, `ofertas_2026-07-16.csv` y `ofertas_2026-07-26.csv`) ya no se publican en este repositorio. Contienen texto de ofertas, nombres de empresas y enlaces tomados de portales de terceros, sobre los cuales LIDE no tiene derechos. Las tablas agregadas que sustentan el articulo siguen disponibles en `outputs/tables/`.

Para replicar el analisis desde los cortes crudos, escribe a elquantificador@laboratoriolide.org y evaluamos el acceso caso por caso. Una vez que tengas los archivos, colocalos en `data/raw/` y corre `source("MASTER.R")`.

#### Current Analytical Scope

El flujo actual:

1. acumula todos los cortes disponibles de junio y julio;
2. elimina duplicados por `source` y `job_id`, conservando la observacion mas reciente y con descripcion mas completa;
3. filtra al universo analitico marcado por el pipeline de recoleccion;
4. construye una submuestra con ofertas que declaran habilidades;
5. calcula herramientas, competencias tecnicas, combinaciones y composicion ocupacional.

Las cifras se regeneran cada vez que se ejecuta `MASTER.R`, por lo que los totales dependen de los cortes acumulados presentes en `data/raw/`.

#### Outputs

Las principales salidas actuales son:

- figuras en `outputs/figures/`;
- tablas en `outputs/tables/`;
- un resumen serializado en `outputs/mercado_datos_resumen.rds`.

#### Article Draft

La version lista para El Quantificador vive en `final_version/`, siguiendo el formato de los repositorios de articulos de la publicacion:

```text
final_version/
├── index.Rmd
└── images/grafico1..4.png
```

`index.Rmd` es la fuente del articulo. Las figuras de `final_version/images/` las copia el script de analisis desde `outputs/figures/`, asi que no se editan a mano. Para previsualizar:

```bash
quarto render final_version/index.Rmd --to html --embed-resources
```

El HTML resultante es un artefacto de compilacion: se regenera cuando haga falta y no se versiona.

`borrador_articulo_quantificador.md` es el borrador previo a la conversion al formato de la publicacion. Las versiones anteriores se guardan en `documentation/archive/`.

#### Article Status

Este repositorio ya deja lista la base reproducible del analisis. El siguiente paso es refrescar el borrador del articulo con las nuevas cifras acumuladas de junio y julio, manteniendo el foco en lo que el mercado realmente pide en las vacantes publicas.
