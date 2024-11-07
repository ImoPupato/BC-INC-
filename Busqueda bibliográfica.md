### Utilización del paquete 'rentrez' para la búsqueda:
```r
busqueda_geo <- entrez_search(db = "gds",
                           term = "(Ribociclib OR Kisqali OR LEE011 OR Palbociclib OR Ibrance OR 
                           Abemaciclib OR Verzenio OR LY2835219 OR Dinaciclib OR SCH727965 OR 
                           Flavopiridol OR Alvocidib OR HMR-1275 OR Roscovitine OR Seliciclib OR 
                           CYC202 OR SNS-032 OR BMS-387032 OR AT7519 OR 'BAY 1000394' OR 
                           Roniciclib OR TG02 OR SB1317) AND 
                           (BREAST[TITL] AND (neoplasms OR cancer)) AND 
                           (microarray OR (rnaseq OR rna-seq)) AND 
                           (survival OR recurrence)",
                           retmax = 10000)
```
Donde:
- db = "gds": Define la base de datos donde se realizará la búsqueda, en este caso, GEO DataSets (gds).  
- term = "...": Especifica los términos de búsqueda combinados mediante operadores lógicos (OR, AND).  
_Los términos buscan Inhibidores de CDK4/6 que incluye una lista de nombres genéricos y comerciales para medicamentos como Ribociclib, Palbociclib, Abemaciclib, y otros inhibidores relacionados, usando OR para combinarlos._
- Tipo de cáncer: Filtra por estudios que incluyan la palabra "breast" en el título (BREAST[TITL]) y términos como "neoplasms" o "cancer".
- Plataforma tecnológica: Filtra estudios que hayan utilizado tecnología de microarrays o RNA-seq (rnaseq OR rna-seq).
- Datos clínicos: Filtra estudios que contengan datos sobre supervivencia (survival) o recurrencia (recurrence).
- retmax = 10000: Establece el número máximo de resultados que se desean recuperar, en este caso, hasta 10000 estudios.
Luego, se obtuvieron los números de acceso y de identificación de cada publicación utilizando la función entrez_summary:
```r
geo_resumen <- entrez_summary(db="gds", id = busqueda_geo$ids)
gse_accession <- c()
for (i in 1:length(geo_resumen)) {
  gse_accession[i] <- geo_resumen[[i]]$accession}
```
Donde: 
- geo_resumen <- entrez_summary(db="gds", id = busqueda_geo$ids) utiliza la función entrez_summary para obtener un resumen de los conjuntos de datos encontrados en la búsqueda anterior, almacenada en busqueda_geo$ids.  
- El parámetro db="gds" indica que se está trabajando con la base de datos GEO DataSets.
- busqueda_geo$ids contiene los identificadores únicos de los resultados de la búsqueda, y el código descarga un resumen detallado de cada uno de esos conjuntos de datos.
- gse_accession <- c() almacena los números de acceso de cada conjunto de datos.
- for (i in 1:length(geo_resumen)) { gse_accession[i] <- geo_resumen[[i]]$accession } utiliza un bucle for para recorrer cada uno de los resúmenes obtenidos en geo_resumen, geo_resumen[[i]]$accession extrae el número de acceso (un identificador único) de cada resumen, y lo asigna a la posición correspondiente en el vector gse_accession.
 
