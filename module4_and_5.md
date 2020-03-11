# Módulo 4 Powershell

## EJERCICIOS
1. Mostrar una tabla de procesos que incluya únicamente los nombres de los
   procesos, sus IDs, y si están respondiendo a Windows (la propiedad
   ``Responding`` muestra eso). Haga que la tabla tome el mínimo de espacio
   horizontal, pero no permita que la información se trunque.
   
   ```powershell
   Get-Process | ft -Property name, ID, Responding -AutoSize -Wrap
   ```

2. Muestre una tabla de procesos que incluya los nombres de los procesos y sus
   IDs. También incluya columnas para uso de memoria virtual y física;
   exprese dichos valores en megabytes (MB).
   
   ```powershell
   Get-Process | ft -Property name, ID, @{n='VM (MB)';e={$_.VM/1MB -as [int]}}, @{n='PM (MB)';e={$_.PM/1MB -as [int]}}
   ```

3. Emplee ``Get-EventLog`` para mostrar una lista de los logs de eventos
   disponibles (revise la ayuda para encontrar el parámetro que le permitirá
   obtener dicha información). Formatee la salida como una tabla que incluya
   el nombre de despliegue del log y el período de retención. Los encabezados
   de columna deben ser NombreLog y Per-Retencion.
   
   ```powershell
   Get-EventLog -List | ft -Property @{n='NombreLog';e={$_.LogDisplayName}}, @{n='Per-Retencion';e={$_.MinimumRetentionDays}}
   ```

4. Muestre una lista de servicios, de tal manera que aparezcan agrupados los
   servicios que están iniciados y los que están detenidos. Los que están
   iniciados deben aparecer primero.
   
   ```powershell
   Get-Service | Sort-Object -Property status -Descending | ft -GroupBy status
   ```

5. Mostrar una lista a cuatro columnas de todos los directorios que están en
   el raíz de la unidad ``C:``
   
   ```powershell
   ls -Path C:\ | fw -Column 4
   ```

6. Cree una lista formateada de todos los archivos ``.exe`` del directorio
   ``C:\Windows``. Debe mostrarse el nombre, la información de versión, y el
   tamaño del archivo. La propiedad de tamaño se llama ``length`` en Powershell,
   pero para mayor claridad, la columna se debe llamar **Tamaño** en su listado.
   
   ```powershell
   Get-ChildItem -Path C:\Windows | where -filter {$_.Name -like "*.exe"} | fl  Name,VersionInfo, @{n='Tamano';e={$_.Length}}
   ```

7. Importe el módulo ``NetAdapter`` (empleando el comando ``Import-Module
   NetAdapter``).
   Empleando el cmdlet ``Get-NetAdapter``, muestre una lista de adaptadores no
   virtuales (adaptadores cuya propiedad Virtual sea falsa. El valor lógico
   falso es representado por Powershell como ``$False``).
   
   ```powershell
   Get-NetAdapter | Where-Object -Filter {$_.Virtual -like $False} | fl
   ```

8. Importe el módulo ``DnsClient``. Empleando el cmdlet `` ``,
   muestre una lista de los registros ``A`` y ``AAAA`` que estén en el caché.
   Sugerencia: Si el caché está vacío, visite algunos sitios web para poblarlo.
   
   ```powershell
   Get-DnsClientCache | Where -Filter {$_.Type -like 1 -or ($_.Type -like 28)} | fl
   ```

9. Genere una lista de todos los archivos ``.exe`` del directorio
   ``C:\Windows\System32`` que tengan más de 5 MB.
   
   ```powershell
   Get-ChildItem -Path C:\Windows\System32 | where -FilterScript {$_.Length -gt 5MB} | fl
   ```

10. Muestre una lista de parches que sean actualizaciones de seguridad.

   ```powershell
   Get-HotFix | where -FilterScript {$_.Description -like "Security Update"} | fl
   ```

11. Muestre una lista de parches que hayan sido instalados por el
    usuario ``Administrador``, que sean actualizaciones. Si no tiene ninguno,
    busque parches instalados por el usuario ``System``. Note que algunos parches
    no tienen valor en el campo ``Installed By``.

   ```powershell
   Get-HotFix | where -filter {$_.Description -like "*Update*"} |where -FilterScript {$_.InstalledBy -like "*System*"}
   ```
12. Genere una lista de todos los procesos que estén corriendo con el nombre
    **Conhost** o **Svchost**.
   ```powershell
   Get-Process | Where-Object {$_.Name -like '*conhost*' -or ($_.Name -like 'svchost')} | fl
   ```   
    
# Módulo 5 Powershell

## EJERCICIOS
1. ¿Cuál clase puede emplearse para consultar la dirección IP de un adaptador
   de red? ¿Posee dicha clase algún método para liberar un préstamo de
   dirección (lease) DHCP?
   ```powershell
   
   ```   
   
2. Despliegue una lista de parches empleando WMI (Microsoft se refiere a los
   parches con el nombre **quick-fix engineering**). Es diferente el listado al
   que produce el cmdlet ``Get-Hotfix``?
   
   ```powershell
   Get-WmiObject -Class Win32_NetworkAdapterConfiguration | gm
   ```    
   
   ```console
   TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name                         MemberType    Definition                                                                                     
----                         ----------    ----------                                                                                     
PSComputerName               AliasProperty PSComputerName = __SERVER                                                                      
DisableIPSec                 Method        System.Management.ManagementBaseObject DisableIPSec()                                          
EnableDHCP                   Method        System.Management.ManagementBaseObject EnableDHCP()                                            
EnableIPSec                  Method        System.Management.ManagementBaseObject EnableIPSec(System.String[] IPSecPermitTCPPorts, Syst...
EnableStatic                 Method        System.Management.ManagementBaseObject EnableStatic(System.String[] IPAddress, System.String...
ReleaseDHCPLease             Method        System.Management.ManagementBaseObject ReleaseDHCPLease()                                      
RenewDHCPLease               Method        System.Management.ManagementBaseObject RenewDHCPLease()     
   ``` 

3. Empleando WMI, muestre una lista de servicios, que incluya su status actual,
   su modalidad de inicio, y las cuentas que emplean para hacer login.
   
   ```powershell
   
   ``` 
4. Empleando cmdlets de CIM, liste todas las clases del namespace
   ``SecurityCenter2``, que tengan **product** como parte del nombre.
   
   ```powershell
   
   ``` 
5. Empleando cmdlets de CIM, y los resultados del ejercicio anterior, muestre
   los nombres de las aplicaciones antispyware instaladas en el sistema.
   También puede consultar si hay productos antivirus instalados en el sistema.
   
   ```powershell
   
   ``` 
