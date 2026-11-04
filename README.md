# Damian_Tp_integrador

- **Pregunta:** ¿Cómo se distribuye entre puertos y tramos de la Vía Navegable Troncal el peaje pagado por los buques en 2024, y cuánto cambiaría con las tarifas de las etapas 0, 1 y 2 del nuevo pliego de concesión?
- **Fuente:** ANPyN, Anexo V de la licitación de la VNT (base de buques 2024): https://www.argentina.gob.ar/economia/agencia-nacional-de-puertos-y-navegacion/llamado-licitacion-publica-nacional-e. Capas geográficas: IGN (puertos y ríos, https://wms.ign.gob.ar/geoserver/ows), API Georef (provincias) y Natural Earth (países).
- **Método de obtención:** scraping de la página de la ANPyN, API del IGN y descarga directa de Georef y Natural Earth.
- **Unidad de observación y período:** tránsito de buques grandes con su tarifa (de un puerto o zona a otro), año 2024.
- **Condiciones de uso o licencia:** publicación oficial de la ANPyN. IGN y Georef con licencia abierta de datos públicos y Natural Earth ya de por si es de dominio público.
- **Cómo voy a verificar los datos:** Probablemente con muchos 'assert'. Además voy a comparar los totales de peaje con cifras publicadas y revisar en el mapa que los puertos estén sobre los ríos.
- **Para qué me sirve en la tesis:** No tengo pensado nada aún para mi tesis.
