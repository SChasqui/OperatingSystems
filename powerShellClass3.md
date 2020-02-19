# PREGUNTAS EJERCICIO CLASE 3

1. Cree dos archivos de texto similares (con una o dos líneas diferentes). Compárelos empleando diff.

Este es el contenido del archivo 1 (ejer1)
```console 
hola
este
es
ejer1
mejorado
```

Este es el contenido del archivo 2 (ejer2)

```console 
hola
este
es
ejer1
mejorado
```

Al invocar el comando diff se están comparando los archivos
  
```powershell
diff -ReferenceObject (type ejerm.txt) -DifferenceObject (type .\ejem2.txt)
```
Esta es la salida del cmdlet anterior
```console
InputObject SideIndicator
----------- -------------
ejer2       =>           
pobre       =>           
ejer1       <=           
mejorado    <=         
```
  Una flecha hacia la derecha indica que este nombre está en la lista nueva, pero no está en la vieja
  Una flecha hacia la derecha indica que este nombre está en la lista vieja, pero no está en la nueva


2. Qué ocurre si se ejecuta:

```console
get-service | export-csv servicios.csv | out-file
```
  Por qué?

Esta es la salida de ejecutar el comando anterior
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
  
  Simplemente definiendo el parametro -Delimiter
```powershell
Get-Process | Export-Csv ejemplo.csv -Delimiter ";"
```

4. Export-cliXML y Export-CSV modifican el sistema, porque pueden crear y sobreescribir archivos. Existe algún parámetro que evite la sobreescritura de un archivo existente? Existe algún parámetro que permita que el comando pregunte antes de sobresscribir un archivo?

  Para evitar la sobreescritura, se puede utilizar el parámetro -NoClobber
```powershell
Get-Process | Out-File -FilePath .\ejer1.txt -NoClobber
```
  Al tratar de sobreescribir el archivo ejer1, se obtiene el isguiente resultado:
  
```console
Out-File : El archivo 'C:\Users\santi\ejer1.txt' ya existe.
En línea: 1 Carácter: 15
+ Get-Process | Out-File -FilePath .\ejer1.txt -NoClobber
+               ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ResourceExists: (C:\Users\santi\ejer1.txt:String) [Out-File], IOException
    + FullyQualifiedErrorId : NoClobber,Microsoft.PowerShell.Commands.OutFileCommand
```
  Por otro lado, para que el comando pregunte antes de hacer la acción de sobreescritura, se utiliza el parámetro -Confirm, el cual sacará en pantalla un pront de confirmación.
  
```powershell
Get-Process | Out-File -FilePath .\ejer1.txt -Confirm
```
  
5. Windows emplea configuraciones regionales, lo que incluye el separador de listas. En Windows en inglés, el separador de listas es la coma (,). Cómo se le dice a Export-CSV que emplee el separador del sistema en lugar de la coma?

  El comando Get-Culture permite obtener información de configuración del sistema, como el lenguaje, la fecha y demás.
```powershell
Get-Process | Export-Csv csvSistema.csv -Delimiter (Get-Culture).TextInfo.ListSeparator
```
Con el siguiente comando se muestra el contenido del archivo csvSistema
```powershell
type .\csvSistema.csv
```
Y este es el resultado:
```powershell
#TYPE System.Diagnostics.Process
"Name";"SI";"Handles";"VM";"WS";"PM";"NPM";"Path";"Company";"CPU";"FileVersion";"ProductVersion";"Description";"Product";"__NounName";"BasePriority";"ExitCode
";"HasExited";"ExitTime";"Handle";"SafeHandle";"HandleCount";"Id";"MachineName";"MainWindowHandle";"MainWindowTitle";"MainModule";"MaxWorkingSet";"MinWorkingS
et";"Modules";"NonpagedSystemMemorySize";"NonpagedSystemMemorySize64";"PagedMemorySize";"PagedMemorySize64";"PagedSystemMemorySize";"PagedSystemMemorySize64";
"PeakPagedMemorySize";"PeakPagedMemorySize64";"PeakWorkingSet";"PeakWorkingSet64";"PeakVirtualMemorySize";"PeakVirtualMemorySize64";"PriorityBoostEnabled";"Pr
iorityClass";"PrivateMemorySize";"PrivateMemorySize64";"PrivilegedProcessorTime";"ProcessName";"ProcessorAffinity";"Responding";"SessionId";"StartInfo";"Start
Time";"SynchronizingObject";"Threads";"TotalProcessorTime";"UserProcessorTime";"VirtualMemorySize";"VirtualMemorySize64";"EnableRaisingEvents";"StandardInput"
;"StandardOutput";"StandardError";"WorkingSet";"WorkingSet64";"Site";"Container"
"AdaptiveSleepService";"0";"163";"4389011456";"7471104";"1777664";"9192";;;;;;;;"Process";"8";;;;;;"163";"2928";".";"0";"";;;;;"9192";"9192";"1777664";"177766
4";"113032";"113032";"1888256";"1888256";"7933952";"7933952";"98308096";"4393275392";;;"1777664";"1777664";;"AdaptiveSleepService";;"True";"0";"System.Diagnos
tics.ProcessStartInfo";;;"System.Diagnostics.ProcessThreadCollection";;;"94044160";"4389011456";"False";;;;"7471104";"7471104";;
"ApplicationFrameHost";"1";"370";"2203559665664";"29110272";"9388032";"21480";"C:\WINDOWS\system32\ApplicationFrameHost.exe";"Microsoft Corporation";"2";"10.0
.18362.1 (WinBuild.160101.0800)";"10.0.18362.1";"Application Frame Host";"Microsoft? Windows? Operating System";"Process";"8";;"False";;"1992";"Microsoft.Win3
2.SafeHandles.SafeProcessHandle";"370";"12208";".";"197622";"Universidad ?- OneNote";"System.Diagnostics.ProcessModule (ApplicationFrameHost.exe)";"1413120";"
204800";"System.Diagnostics.ProcessModuleCollection";"21480";"21480";"9388032";"9388032";"333928";"333928";"12767232";"12767232";"30367744";"30367744";"249630
720";"2203567853568";"True";"Normal";"9388032";"9388032";"00:00:01.0468750";"ApplicationFrameHost";"15";"True";"1";"System.Diagnostics.ProcessStartInfo";"12/0
2/2020 12:55:38 p.m.";;"System.Diagnostics.ProcessThreadCollection";"00:00:02";"00:00:00.9531250";"241442816";"2203559665664";"False";;;;"29110272";"29110272"
;;
```

6. Identifique un cmdlet que permita generar un número aleatorio.

```powershell
Get-Random
```

7. Identifique un cmdlet que despliegue la fecha y hora actuales.

```powershell
Get-Date
```

8. Qué tipo de objeto produce el cmdlet de la pregunta 7?
  
  Esto se puede ver por medio del comando Get-Member o gm
```powershell
Get-Date | gm
```
  La salida de este comando es la siguiente:
```console


   TypeName: System.DateTime

Name                 MemberType     Definition                                                                                                               
----                 ----------     ----------                   
```

  Podemos observar que se produce un objeto de tipo DateTime (ver líneas de comando).
  
 9. Usando el cmdlet de la pregunta 7 y select-object, despliegue solamente el día de la semana, así:
 
```powershell
   DayOfWeek
  ---------
    Thursday
 ```
  El comando que lo permite es:
```powershell
 Get-Date | Select-Object -Property "dayofweek"
```
  Y la salida es la siguiente:
```console
DayOfWeek
---------
Wednesday
 ```
 
10. Identifique un cmdlet que muestre información acerca de parches (hotfixes) instalados en el sistema.
  
  Para obtener los parches se obtienen mediante el siguiente comando:
```powershell
Get-HotFix
```
  A continuación el resultado:
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

11. Empleando el cmdlet de la pregunta 10, muestre una lista de parches instalados. Luego extienda la expresión para ordenar la lista por fecha de instalación, y muestre en pantalla únicamente la fecha de instalación, el usuario que instaló el parche, y el ID del parche. Recuerde examinar los nombres de las propiedades.

  Es posible lograr el requerimiento anterior mediante:
    
```powershell
Get-HotFix | Select-Object -Property InstalledOn,InstalledBy,HotFixID | Sort-Object -Property InstalledOn 
```
  Y muestra como resultado
```console
InstalledOn              InstalledBy         HotFixID 
-----------              -----------         -------- 
21/09/2019 12:00:00 a.m. NT AUTHORITY\SYSTEM KB4515383
21/09/2019 12:00:00 a.m. NT AUTHORITY\SYSTEM KB4515530
21/09/2019 12:00:00 a.m. NT AUTHORITY\SYSTEM KB4516115
4/10/2019 12:00:00 a.m.  NT AUTHORITY\SYSTEM KB4520390
13/10/2019 12:00:00 a.m. NT AUTHORITY\SYSTEM KB4521863
14/11/2019 12:00:00 a.m. NT AUTHORITY\SYSTEM KB4524569
20/01/2020 12:00:00 a.m. NT AUTHORITY\SYSTEM KB4528759
20/01/2020 12:00:00 a.m. NT AUTHORITY\SYSTEM KB4528760
10/02/2020 12:00:00 a.m. NT AUTHORITY\SYSTEM KB4534132
```
  
12. Complemente la solución a la pregunta 11, para que el sistema ordene los resultados por la descripción del parche, e incluya en el listado la descripción, el ID del parche, y la fecha de instalación. Escriba los resultados a un archivo HTML.
  
  
```powershell
Get-HotFix | Select-Object -Property hotfixID,Description,installedOn | Sort-Object -Property Description | ConvertTo-Html | Out-File parches.html
```
Muestra del archivo creado (parches.html)
```powershell
  type .\parches.html
```

Y a continuación el resultado:

```console
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>HTML TABLE</title>
</head><body>
<table>
<colgroup><col/><col/><col/></colgroup>
<tr><th>hotfixID</th><th>Description</th><th>InstalledOn</th></tr>
<tr><td>KB4515383</td><td>Security Update</td><td>21/09/2019 12:00:00 a.m.</td></tr>
<tr><td>KB4515530</td><td>Security Update</td><td>21/09/2019 12:00:00 a.m.</td></tr>
<tr><td>KB4516115</td><td>Security Update</td><td>21/09/2019 12:00:00 a.m.</td></tr>
<tr><td>KB4520390</td><td>Security Update</td><td>4/10/2019 12:00:00 a.m.</td></tr>
<tr><td>KB4521863</td><td>Security Update</td><td>13/10/2019 12:00:00 a.m.</td></tr>
<tr><td>KB4524569</td><td>Security Update</td><td>14/11/2019 12:00:00 a.m.</td></tr>
<tr><td>KB4528759</td><td>Security Update</td><td>20/01/2020 12:00:00 a.m.</td></tr>
<tr><td>KB4534132</td><td>Update</td><td>10/02/2020 12:00:00 a.m.</td></tr>
<tr><td>KB4528760</td><td>Update</td><td>20/01/2020 12:00:00 a.m.</td></tr>
</table>
</body></html>
```
  
13. Muestre una lista de las 50 entradas más nuevas del log de eventos System. Ordene la lista de modo que las entradas más antiguas aparezcan primero; las entradas producidas al mismo tiempo deben ordenarse por número índice. Muestre el número índice, la hora y la fuente para cada entrada. Escriba esta información en un archivo de texto plano.

  Se utiliza el siguiente comando
```powershell
Get-EventLog -LogName System -Newest 50 | Sort-Object -Property TimeGenerated | Sort-Object -Property Index | Select-Object -Property index,TimeGenerated,source | Out-File archivoPrueba.txt
```
  Muestra del archivo de texto plano creado:
```console
type .\archivoPrueba.txt

Index TimeGenerated            Source                                
----- -------------            ------                                
26019 12/02/2020 12:22:08 p.m. Microsoft-Windows-Kernel-Power        
26020 12/02/2020 12:37:50 p.m. Microsoft-Windows-Kernel-General      
26021 12/02/2020 12:37:51 p.m. Microsoft-Windows-Kernel-Power        
26022 12/02/2020 12:37:52 p.m. VBoxNetLwf                            
26023 12/02/2020 12:37:52 p.m. VBoxNetLwf                            
26024 12/02/2020 12:37:52 p.m. Microsoft-Windows-Kernel-Boot         
26025 12/02/2020 12:37:52 p.m. Microsoft-Windows-Kernel-Boot         
26026 12/02/2020 12:37:52 p.m. Microsoft-Windows-Kernel-Boot         
26027 12/02/2020 12:37:52 p.m. Microsoft-Windows-Kernel-Boot         
26028 12/02/2020 12:37:52 p.m. Microsoft-Windows-Kernel-Boot         
26029 12/02/2020 12:37:55 p.m. Microsoft-Windows-UserModePowerService
26030 12/02/2020 12:37:55 p.m. Microsoft-Windows-UserModePowerService
26031 12/02/2020 12:37:56 p.m. Microsoft-Windows-Power-Troubleshooter
26032 12/02/2020 12:38:05 p.m. Microsoft-Windows-DNS-Client          
26033 12/02/2020 12:38:12 p.m. Microsoft-Windows-Time-Service        
26034 12/02/2020 12:39:02 p.m. Microsoft-Windows-DNS-Client          
26035 12/02/2020 12:55:17 p.m. Microsoft-Windows-Time-Service        
26036 12/02/2020 1:59:26 p.m.  Microsoft-Windows-WindowsUpdateClient 
26037 12/02/2020 1:59:26 p.m.  Microsoft-Windows-WindowsUpdateClient 
26038 12/02/2020 1:59:45 p.m.  Microsoft-Windows-WindowsUpdateClient 
26039 12/02/2020 2:32:05 p.m.  Service Control Manager               
26040 12/02/2020 2:35:09 p.m.  Service Control Manager               
26041 12/02/2020 2:37:14 p.m.  Service Control Manager               
26042 12/02/2020 3:16:14 p.m.  Microsoft-Windows-Kernel-Power        
26043 12/02/2020 3:16:39 p.m.  Microsoft-Windows-UserModePowerService
26044 12/02/2020 3:16:39 p.m.  Microsoft-Windows-UserModePowerService
26045 12/02/2020 3:16:43 p.m.  Microsoft-Windows-Kernel-Power        
26046 12/02/2020 3:16:49 p.m.  Microsoft-Windows-Kernel-Power        
26047 12/02/2020 3:20:44 p.m.  Microsoft-Windows-Kernel-General      
26048 12/02/2020 3:20:45 p.m.  Microsoft-Windows-Kernel-Power        
26049 12/02/2020 3:20:50 p.m.  VBoxNetLwf                            
26050 12/02/2020 3:20:50 p.m.  VBoxNetLwf                            
26051 12/02/2020 3:20:53 p.m.  Microsoft-Windows-Power-Troubleshooter
26052 12/02/2020 3:21:06 p.m.  Microsoft-Windows-Kernel-Power        
26053 12/02/2020 3:21:15 p.m.  Microsoft-Windows-Kernel-Power        
26054 12/02/2020 4:22:43 p.m.  Microsoft-Windows-Kernel-General      
26055 12/02/2020 4:22:45 p.m.  Microsoft-Windows-Kernel-Power        
26056 12/02/2020 4:22:45 p.m.  Microsoft-Windows-Kernel-Boot         
26057 12/02/2020 4:22:45 p.m.  Microsoft-Windows-Kernel-Boot         
26058 12/02/2020 4:22:45 p.m.  Microsoft-Windows-Kernel-Boot         
26059 12/02/2020 4:22:45 p.m.  Microsoft-Windows-Kernel-Boot         
26060 12/02/2020 4:22:45 p.m.  Microsoft-Windows-Kernel-Boot         
26061 12/02/2020 4:22:46 p.m.  VBoxNetLwf                            
26062 12/02/2020 4:22:46 p.m.  VBoxNetLwf                            
26063 12/02/2020 4:22:50 p.m.  Microsoft-Windows-UserModePowerService
26064 12/02/2020 4:22:50 p.m.  Microsoft-Windows-UserModePowerService
26065 12/02/2020 4:22:52 p.m.  Microsoft-Windows-Power-Troubleshooter
26066 12/02/2020 4:23:01 p.m.  Microsoft-Windows-DNS-Client          
26067 12/02/2020 4:31:33 p.m.  Microsoft-Windows-DNS-Client          
26068 12/02/2020 4:33:10 p.m.  VBoxNetLwf               

```

