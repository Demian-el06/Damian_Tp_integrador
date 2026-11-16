# Buques grandes y peaje en la Vía Navegable Troncal, 2024

**Autor:** Damian Silva   -  **Fecha:** noviembre de 2026

## Pregunta

- ¿Cómo cambiaría el calado real con el que salen los buques del Gran Rosario al océano si el canal pasa de 34 a 36 pies (etapa 1) y a 40 pies (etapa 2)?
- ¿Cuánto cambiaría la recaudación del peaje si a los viajes de 2024 se les cobrara la tarifa de la etapa 0 del nuevo pliego?
- ¿Cómo se reparten en el mapa los viajes según el puerto del que salen?

**Unidad de análisis:** el viaje de un buque grande entre dos secciones de la VNT. En el mapa, el puerto de origen.
**Período:** 2024.

**Por qué importa.** La licitación de la nueva concesión fija cuánto se profundiza el canal y cuánto se cobra de peaje. El calado limita cuánta carga puede llevar cada buque que sale del Gran Rosario, por donde sale la mayor parte de las exportaciones agroindustriales, y el peaje es lo que financia el dragado y el balizamiento. Responder las preguntas da inicio a un analisis de cuánto recaudará la empresa encargada (Jan de Nul), para mas adelante compararlo con los costos y riesgos de brindar estos servicios y ver sus posibles beneficios.

## Fuentes

| Fuente | Quién la produce | URL | Fecha de descarga | Licencia o condiciones | Cómo se obtiene |
| --- | --- | --- | --- | --- | --- |
| Base de buques grandes 2024 (Anexo V de la licitación de la VNT) | Agencia Nacional de Puertos y Navegación (ANPyN) | https://www.argentina.gob.ar/economia/agencia-nacional-de-puertos-y-navegacion/llamado-licitacion-publica-nacional-e | 04/11/2026 | Publicación oficial | *Scraping* del HTML para encontrar el link y descarga con `requests` |
| Cuadro tarifario (Anexo 8 de la Resolución 308/2021) | Estado Nacional (InfoLEG) | https://www.argentina.gob.ar/sites/default/files/infoleg/353762/res308-9.pdf | 13/11/2026 | Norma pública | Descarga del PDF y extracción de la tabla |
| Capa "Puerto" (`puntos_de_puertos_y_muelles_BB005`) | Instituto Geográfico Nacional (IGN) | https://wms.ign.gob.ar/geoserver/ows | 04/11/2026 | Datos abiertos del IGN | Servicio WFS con `requests` |
| Ríos de la Hidrovía (`areas_de_aguas_continentales_BH140`) | IGN | https://wms.ign.gob.ar/geoserver/ows | 04/11/2026 | Datos abiertos del IGN | Servicio WFS |
| Provincias (CABA, Buenos Aires, Corrientes, Entre Ríos y Santa Fe) | API Georef (datos.gob.ar) | https://apis.datos.gob.ar/georef/api/provincias | 15/11/2026 | Datos abiertos | API |
| Países (escala 1:10m) | Natural Earth | https://naciscdn.org/naturalearth/10m/cultural/ne_10m_admin_0_countries.zip | 15/11/2026 | Dominio público | Descarga directa |

**Valores cargados a mano en el notebook:**
- Tarifa básica 2024: 3,06 hasta el 25/9/2024; después, 4,30 USD y 824,80 ARS. fuente: https://www.argentina.gob.ar/sites/default/files/a7_-_if-2024-101835899-apn-dctyhmtr_-_anexo_ndeg_7_cuadro_tarifario.pdf
- Tarifas por etapa del pliego: 3,80, 4,65 y 5,78 USD. fuente: https://www.argentina.gob.ar/sites/default/files/2025/12/contrato_de_concesion_de_la_via_navegable_troncal.pdf
- Coordenadas de 4 puertos que no están en el IGN: Nueva Palmira, Tigre, Fray Bentos y AGD. coordinadas aproximadas del google maps.

## Cómo ejecutar

1. Clonar el repo y crear el entorno (Python 3.13):
   ```bash
   python -m venv .venv
   .venv\Scripts\python -m pip install -r requirements.txt
   ```
2. Tener **Java** instalado porque `tabula` lo necesita para leer el PDF.
3. Abrir `TP6.ipynb`, elegir como kernel el Python de `.venv` y ejecutar todo.
   - Con los datos que ya están en `datos/`, no descarga nada y tarda menos de un minuto.
   - Si se borran, los vuelve a descargar.

## Estructura

```
├── README.md
├── requirements.txt
├── .gitignore
├── TP6.ipynb                  # notebook principal, en tres partes:
│                              #   01 obtención, 02 limpieza e integración, 03 análisis
├── PythEcon_tp6_final.ipynb   # consigna del TP
└── datos/
    ├── crudo/                 # tal cual se descargaron, no se editan:
    │                          #   base de buques (.xlsx) y Resolución 308 (.pdf)
    ├── geo/                   # capas geográficas: puertos y ríos (IGN),
    │                          #   provincias (Georef) y países (Natural Earth)
    └── procesado/             # buques_2024.csv.gz: base final de viajes, con coordenadas 
                                  del puerto de origen, cuadro tarifario y cálculos de tarifa
```

## Principales resultados

- **Calado:**
  - Más de la mitad de los buques que salen del Gran Rosario al océano podría ir más hundido de lo que permite el canal de 34 pies. Su calado de diseño tiene una mediana de 41,3 pies, pero salen con una mediana de 32,5. De los 2.132 viajes con calado real informado, 863 salieron limitados por el canal. Con la profundización, el calado real medio aumentaría.
  - Aunque se da esta profundización, dada la distribución del calado de los buques, la mayoría de los que salen con carga parcial tienen un calado de diseño mayor a los 40 pies, por lo que de igual manera seguirían sin completar su carga.
- **Recaudación con la tarifa de la etapa 0:**
  - En USD, de 232,9 M a 261,1 M (+28,2 M, +12,1 %).
  - En ARS, de 735,8 M a 2.747,2 M, porque hasta el 25/9/2024 la tarifa en pesos era de 3,06.
- **Mapa:**
  - San Lorenzo concentra el 20 % de las salidas desde puertos, y le siguen Campana y Rosario.

## Qué verifiqué y qué no

El detalle está al final de `TP6.ipynb`.

## Bitácora de uso de IA

Usé la IA de VS Studio que te autocompleta pedacitos de código solo por comodidad

Claude para:

- Buscar los links exactos de los archivos que debía descargar.
- Ayudo a encontrar qué filtro debía usar en la IGN y de Georef para extraer los datos que necesitaba.
- Algunas funciones del regex.
- Durante el curso fui copiando algo de la estructura y el orden que usa la IA y esto lo traje al tp final, como escribir en mayuscula algunos marcadores.
- Proyección de las etapas 1 y 2: Es menor, pero hice unos supuestos iniciales e itere un poco con la IA para ver si era razonable. 
Al final le pedi que  me los ordene porque me habia hecho un barullo en la cabeza.
- Gráficos: Acá es donde más me ayudo, no el orden de los comandos, sino la sintaxis de lo que hicimos en clase y tódas las opciones de personalización que había.
- Ayuda con comandos: describia algo que queria hacer y no me salía y le pedia una pista y un comando clave y como usarlo. Eso ya me daba el pie para seguir.
- Revisión del notebook para ver qué faltaba.

**Un caso en que la IA se equivocó:**
- Las equivocaciones fueron realmente debido a una incorrecta descripción de mi problema por parte mia.
