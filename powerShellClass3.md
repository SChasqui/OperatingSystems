# PREGUNTAS EJERCICIO CLASE 3

1. Cree dos archivos de texto similares (con una o dos líneas diferentes). Compárelos empleando diff.
  
```powershell
diff -ReferenceObject (type ejerm.txt) -DifferenceObject (type .\ejem2.txt)
```

2. Qué ocurre si se ejecuta:

```console
get-service | export-csv servicios.csv | out-file
```
  Por qué?


```console
  out-file : No se puede procesar el argumento porque el valor del argumento "path" es NULL. Cambie el valor del argumento "path" a un valor no 
nulo.
En línea: 1 Carácter: 42
+ get-service | export-csv servicios.csv | out-file
+                                          ~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Out-File], PSArgumentNullException
    + FullyQualifiedErrorId : ArgumentNull,Microsoft.PowerShell.Commands.OutFileCommand
```

  Este comando no funciona debido a que el archivo servicios.csv no existe.
  
3. Cómo haría para crear un archivo delimitado por puntos y comas (;)? PISTA: Se emplea export-csv, pero con un parámetro adicional.
 
```powershell
Get-Process | Export-Csv ejemplo.csv -Delimiter ";"
```

4. Export-cliXML y Export-CSV modifican el sistema, porque pueden crear y sobreescribir archivos. Existe algún parámetro que evite la sobreescritura de un archivo existente? Existe algún parámetro que permita que el comando pregunte antes de sobresscribir un archivo?

  Para evitar la sobreescritura, es posible cambiar los atributos del archivo y ponerlo como sólo lectura.
```powershell
Set-ItemProperty .\ejemplo.csv -Name Attributes -Value "readonly,archive"
```
  Por otro lado, para que el comando pregunte antes de hacer la acción de sobreescritura, se utiliza el parámetro -Confirm, el cual sacará en pantalla un pront de confirmación.
  
5. Windows emplea configuraciones regionales, lo que incluye el separador de listas. En Windows en inglés, el separador de listas es la coma (,). Cómo se le dice a Export-CSV que emplee el separador del sistema en lugar de la coma?

6. Identifique un cmdlet que permita generar un número aleatorio.

```powershell
Get-Random
```

7. Identifique un cmdlet que despliegue la fecha y hora actuales.

```powershell
Get-Date
```

8. Qué tipo de objeto produce el cmdlet de la pregunta 7?

```powershell
Get-Date | gm
```

```console


   TypeName: System.DateTime

Name                 MemberType     Definition                                                                                                               
----                 ----------     ----------                   
```

  Produceun objeto de tipo DateTime (ver líneas de comando).
  
 9. Usando el cmdlet de la pregunta 7 y select-object, despliegue solamente el día de la semana, así:
 
```powershell
   DayOfWeek
  ---------
    Thursday
 ```
  El comando que lo permite es:
```powershell
 Get-Date | Select-Object -Property "dayofweek"

DayOfWeek
---------
Wednesday
 ```
 
10. Identifique un cmdlet que muestre información acerca de parches (hotfixes) instalados en el sistema.

```powershell
Get-HotFix
```

```console
Source        Description      HotFixID      InstalledBy          InstalledOn              
------        -----------      --------      -----------          -----------              
MYLAP         Update           KB4534132     NT AUTHORITY\SYSTEM  10/02/2020 12:00:00 a.m. 
MYLAP         Security Update  KB4515383     NT AUTHORITY\SYSTEM  21/09/2019 12:00:00 a.m. 
MYLAP         Security Update  KB4515530     NT AUTHORITY\SYSTEM  21/09/2019 12:00:00 a.m. 
MYLAP         Security Update  KB4516115     NT AUTHORITY\SYSTEM  21/09/2019 12:00:00 a.m. 
MYLAP         Security Update  KB4520390     NT AUTHORITY\SYSTEM  4/10/2019 12:00:00 a.m.  
MYLAP         Security Update  KB4521863     NT AUTHORITY\SYSTEM  13/10/2019 12:00:00 a.m. 
MYLAP         Security Update  KB4524569     NT AUTHORITY\SYSTEM  14/11/2019 12:00:00 a.m. 
MYLAP         Security Update  KB4528759     NT AUTHORITY\SYSTEM  20/01/2020 12:00:00 a.m. 
MYLAP         Update           KB4528760     NT AUTHORITY\SYSTEM  20/01/2020 12:00:00 a.m. 
```

    


  
  
  
