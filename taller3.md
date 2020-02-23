##Preguntas
1. Cree dos archivos de texto similares (con una o dos líneas diferentes).
   Compárelos empleando ``diff``.
   ```console
   PS C:\Users\Nicolas> notepad test1.txt
   PS C:\Users\Nicolas> notepad test2.txt
   PS C:\Users\Nicolas> type test1.txt
   pruebita
   PS C:\Users\Nicolas> type test2.txt
   pruebita2
   PS C:\Users\Nicolas> diff -ReferenceObject (Get-Content test1.txt) -DifferenceObject (Get-Content test2.txt)
   InputObject SideIndicator
   ----------- -------------
   pruebita2   =>           
   pruebita    <=    
   ``` 
2. Qué ocurre si se ejecuta:
   ```powershell
   get-service | export-csv servicios.csv | out-file
   ```
   Por qué?
   ```powershell
      out-file : No se puede procesar el argumento porque el valor del argumento "path" es NULL. Cambie el valor del argumento "path" a       un valor no nulo.
      En línea: 1 Carácter: 42
      + get-service | export-csv servicios.csv | out-file
      +                                          ~~~~~~~~
         + CategoryInfo          : InvalidArgument: (:) [Out-File], PSArgumentNullException
         + FullyQualifiedErrorId : ArgumentNull,Microsoft.PowerShell.Commands.OutFileCommand
   ```
   
   Esto pasa ya que cuando se va a ejecutar el out-line el pipe no puede exportar nada porque esta vacio 
   
3. Cómo haría para crear un archivo delimitado por puntos y comas (;)?
   PISTA: Se emplea ``export-csv``, pero con un parámetro adicional.
   ```console 
   PS C:\Users\Nicolas> Get-Process | Export-Csv procesos.csv
   ```
4. ``Export-cliXML`` y ``Export-CSV`` modifican el sistema, porque pueden crear
   y sobreescribir archivos. Existe algún parámetro que evite la
   sobreescritura de un archivo existente? Existe algún parámetro que
   permita que el comando pregunte antes de sobresscribir un archivo?
   ```console
   PS C:\Users\Nicolas> Get-Process | Export-Csv procesos.csv -NoClobber
   ```
5. Windows emplea configuraciones regionales, lo que incluye el separador de
   listas. En Windows en inglés, el separador de listas es la coma (,).
   Cómo se le dice a ``Export-CSV`` que emplee el separador del sistema en lugar
   de la coma?
   ```console
   PS C:\Users\Nicolas> Set-WinUserLanguageList -LanguageList (New-WinUserLanguageList -Language en-GB) -Force
   ```
6. Identifique un cmdlet que permita generar un número aleatorio.
   ```console
   PS C:\Users\Nicolas> Get-Random
   ```
7. Identifique un cmdlet que despliegue la fecha y hora actuales.
   ```console
   PS C:\Users\Nicolas> Get-Date
   ```
8. Qué tipo de objeto produce el cmdlet de la pregunta 7?
   el tipo de archivo System.DateTime
9. Usando el cmdlet de la pregunta 7 y ``select-object``, despliegue solamente
   el día de la semana, así:

   ```console
   DayOfWeek
   ---------
    Thursday
   ```
   ```console
      PS C:\Users\Nicolas> Get-Date | Select-Object -Property DayOfWeek
   ```
10. Identifique un cmdlet que muestre información acerca de parches (hotfixes)
    instalados en el sistema.
    ```console
       PS C:\Users\Nicolas> Get-HotFix 
    ```
 11. Empleando el cmdlet de la pregunta 10, muestre una lista de parches
    instalados. Luego extienda la expresión para ordenar la lista por fecha
    de instalación, y muestre en pantalla únicamente la fecha de instalación,
    el usuario que instaló el parche, y el ID del parche. Recuerde examinar
    los nombres de las propiedades.
    
    ```powershell
       PS C:\Users\Nicolas> Get-HotFix | Select-Object -Property InstallDate,InstalledBy, HotFixID |  Sort-Object -Property InstallDate
    ```
 12. Complemente la solución a la pregunta 11, para que el sistema ordene los
    resultados por la descripción del parche, e incluya en el listado la
    descripción, el ID del parche, y la fecha de instalación.
    Escriba los resultados a un archivo HTML.
    
    ```powershell
       PS C:\Users\Nicolas> Get-HotFix | Sort-Object -Property Description | Select-Object -Property Description, HotFixID, InstalledOn        | ConvertTo-Html | Out-file HotFix.html
    ```
 13. Muestre una lista de las 50 entradas más nuevas del log de eventos System.
    Ordene la lista de modo que las entradas más antiguas aparezcan primero;
    las entradas producidas al mismo tiempo deben ordenarse por número índice.
    Muestre el número índice, la hora y la fuente para cada entrada. Escriba
    esta información en un archivo de texto plano.
    
    ```powershell
       PS C:\Users\Nicolas> Get-EventLog -LogName system -Newest 50| Sort-Object -Property TimeWritten,Index | Select-Object -Property          Index, TimeWritten, Source
    ```
    

    
