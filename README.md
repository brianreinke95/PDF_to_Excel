# PDF_to_Excel
1 week proyect. pdf to excel tables.

**Durante una semana trabajé en pasar tablas en formato pdf a excel para una firma de abogados.
Se puede ver desde el caso 1 al caso 29 la evolución del código utilizado para realizar la tarea. Pasé de estar todo un día 
pasando 1 solo archivo a realizar 15 en el mismo equivalente de tiempo.**

Las tablas contaban en 6 columnas: Día, Nombre, Descripción, Horas, Cobro por Hora, Total. 
Los datos corresponden a los servicios cobrados por los empleados dentro de la firma.

El IDE donde se trabajó fue en Jupyter Notebook y el lenguaje de programación Python.

Los pasos para el correcto pasaje de un formato al otro fueron los siguientes:

1. ### Lectura del pdf utilizando tabula-py
2. ### Limpieza de los DataFrames:
   - Eliminación de datos basura. Rótulo, columnas vacías, etc.
   - Ordenar los datos: 
     - La función read_pdf de tabula nunca pasaba datos limpios del formato pdf debido a las particularidades mismas
        de este tipo de archivo. Por lo tanto muy frecuentemente había datos mezclados entre columnas que debían ser ordenados.
   - Limpieza general: Lavado de cara a los DataFrames una vez realizados los procesos anteriores. Por ejemplo reiniciar el index.
  
3. ### Separar cada dato en su columna correspondiente:  
   - Los procesos anteriores dejan a cada DataFrame con una disposición distinta. 
   - Es decir, tal vez el df[1] tenía 3 columnas con los siguientes datos dentro: 
     - Date/Name | Description | Hours/Rate/Totals
   - y el df[3] tenía 1 columna con todos los datos dentro de la misma:
     - Date/Name/Description/Hours/Rate/Totals.
                  
    Por lo tanto para cada caso mediante análisis de strings se debía extraer la información. Se utilizó mucho las funcionalidades
    que ofrece pandas con sus Series. 
    
 4. ### Visualización de errores:
 
    Una vez que cada DataFrame quedó con sus 6 respectivas columnas se debía hacer un análisis visual de los datos
    para observar errores. 
    Para esto se realizaron estos 3 repasos rápidos sobre la muestra:
    - Cantidad de líneas por dataframe (cada dataframe corresponde a una página del pdf)
    - Nombres inválidos. Debido a la forma que se utiliza regex a veces parte del texto de la descripción se mezclaba con
             la columna de nombres. Una vez identificado el nombre inválido se lo agregaba a una lista para que no volviera a ocurrir.
    - Fechas faltantes: Por errores en la interpretación de tabula al leer el pdf había fechas que aparecían con errores de
             tipero. Por ejemplo "7i7/2019". Y pasaban de largo. Una vez identificado el error se modificaba la fecha y se volvía a
             intentar.
    - Valores en horas, rates y totales irrisorios o exagerados. Corrección manual. En general era un problema con la sintaxis
             utilizando regex.
         
5. ### Carga de los datos:
    Al estar seguros de que los datos que se tenía eran los correctos se concatenaban todos los DataFrames en 1 solo y se lo 
    cargaba a un excel utilizando la función de pandas pd.to_excel.
       
