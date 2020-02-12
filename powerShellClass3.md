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


  
  
