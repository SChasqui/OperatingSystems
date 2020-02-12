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
  
  
  
