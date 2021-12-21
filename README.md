# Gateway-Appliance-Juniper-vSRX-version-20.4

IBM Cloud Juniper vSRX le permite enrutar selectivamente el tráfico de red pública y privada, a través de un firewall de nivel empresarial que funciona con características de software de JunOS, como stack de enrutamiento completo, tráfico compartido, enrutamiento basado en políticas y VPN. En este repositorio se encuentran los pasos necesarios para crear y configurar una conexion entre una VPN for VPC y un Power Virtual Server.


## Crear servicio Gateway Appliance
Para desplegar un dispositivo de pasarela ```Gateway Appliance``` realice lo siguiente:

1. De click en la pestaña del catálogo y en la barra de búsqueda escriba ```Gateway Appliance```.

2. Seleccione la opción ```Gateway Appliance By IBM ```. Una vez cargue la ventana de click en el botón ```Crear/Create```.

3. Complete los campos solicitados para la creación del recurso de la siguiente manera:

   **Detalles de recurso**
   * ```Proveedor```: seleccione el proveedor, para este caso es *Juniper*.
   * ```Versión```: seleccione la versión, para este caso es *20.4R2-S2 (up to 1 Gbps)*.
   * ```Licencia```: indique la licencia que utilizará, en este caso *Standard License*.
   * ```Nombre del Host```: asigne un nombre exclusivo para el host.
   * ```Dominio```: deje el dominio que aparece por defecto o indique uno nuevo.
   * ```Alta disponibilidad```: deje esta opción sin seleccionar.

   **Ubicación**
   * Seleccione la ubicación en donde desplegará el recurso.

   **Perfil del servidor**
   * ```Perfil```: deje el perfil que aparece por defecto, en este caso: *Intel Xeon 4210, 20 núcleos, 64 GB de RAM*.
   * ```RAM```: indique la cantidad de memoria RAM que necesita, por ejemplo: *32 GB*.

   **Discos de almacenamiento**
   * ```Tipo```: indique el tipo de disco de almacenamiento, en este caso *RAID 1*.
   * ```Discos```: establezca el número de discos, por ejemplo 2.
   * ```Repuestos en caliente```: deje este campo con el valor por defecto.
   * ```Soporte de disco```: deje este campo con el valor por defecto.

   **Interfaz de red**
   * ```Interfaz```: seleccione la opción *Público y privado*.
   * ```Redundancia de puertos```: seleccione la opción *Automático*.
   * ```Velocidad del puerto```: indique la velocidad del puerto, por ejemplo: *1 Gbps (20,00 US$)*.
   *  ```Salida pública - ancho de banda```: seleccione el ancho de banda, en este caso *5000 GB (0,00 US$)*.

   Los demás campos nos los modifique, deje los valores que salen por defecto. Para finalizar, de click en el botón ```Crear/Create```.
   
   <p align="center">
   <img src=https://github.com/emeloibmco/Gateway-Appliance-Juniper-vSRX-version-20.4/blob/main/Imagenes/Crear.gif>
   </p>
  
<br />

## Ingresar a Juniper

### Ingresar por consola
Luego de desplegar el ```Gateway Appliance``` siga los pasos que se indican a continuación para ingresar a Juniper:

1. En el recurso desplegado, de click en la pestaña ```Visión general/Overview``` y allí visualice la sección ```vSRX```. Identifique los siguientes datos:

   * ```IP Pública```.
   * ```IP Privada```.
   * ```Nombres de usuario```: root y admin.
   * ```Contraseñas```.

2. En el navegador (se recomienda usar Firefox) coloque la ip pública (vSRX) y el puerto 8443, de la siguiente manera:

   ```
   https://ip_publica:8443
   ```
   
   Espera mientras carga la página
   
3. Una vez cargue la ventana, se le solicitará que coloque usuario y contraseña para acceder a Juniper. Complete los campos teniendo en cuenta:

   * ```Username```: coloque *admin*.
   * ```Password```: coloque la contraseña para el usuario *admin* obtenida en la sección ```vSRX```.

4. De click en el botón ```Log In``` para iniciar sesión en Juniper.

  <p align="center">
   <img src=https://github.com/emeloibmco/Gateway-Appliance-Juniper-vSRX-version-20.4/blob/main/Imagenes/Juniper.png>
   </p>
 
### Ingresar por linea de comando SHH
En la línea de comandos de su equipo ingrese el comando de conexión SSH:
```
ssh admin@<ip_publica>
```
Cuando se le pida la contraseña ingrese la contraseña para el usuario *admin* obtenida en la sección ```vSRX```. Podrá rectificar que se encuentra en la consola del dispositivo al ver la etiqueta con el nombre que le dio a su instancia.
 
 
## Configuración VPN site to site Juniper
Antes de iniciar con la configuración es necesario crear una VPN en VPC, para esto tenga en cuenta el siguiente **repositorio**.

### Creación de nuevos segmentos de red
Luego de crear la VPN for VPC siguiendo los pasos explicados en el repositorio debe crear los nuevos segmentos de red en el global adress book en Juniper para la VPN y la VLAN creados anteriormente. Para esto una vez iniciada sesión en Juniper siga la ruta ```Security Policies and Objects > Global Addresses  > Icono de lápiz > +``` para agregar una nueva dirección global. Esto abrirá un menú de configuración, aquí ingrese la siguiente información:
* ```Address Name```: Ingrese un nombre distintivo para la dirección
* ```Value```: Ingrese el segmento de red privado del servicio creado anteriormente.
* De click en ```Ok```
* De click en ```Commit```> ```Commit configuration```

Luego de esto repita el proceso tanto para la VPN como para la VLAN

### Creación de una dirección de Zona 
Siga la ruta ```Security Policies and Objects > Zones/Screens > +```para agregar una nueva zona. Esto abrirá un menú de configuración, aquí ingrese la siguiente información:
* ```Zone Name```: Ingrese un nombre distintivo para la zona
* ```Zone Type```: Seleccione ```Security```.
* De click en ```Ok```
* De click en ```Commit```> ```Commit configuration```

### Creación de una nueva interface
Siga la ruta ```Network > Connectivity > Interfaces``` y tenga en cuenta los siguientes pasos para agregar una nueva Interfaz. 
* Seleccione la interfaz st0 en el menú desplegable.
* De click en el botón ```Create``` > ```Logical interface```. Esto abrirá un menú de configuración, aqui ingrese la siguiente información.
  * ```Tunnel interface st0```: ingrese ```0``
  * ```Zone```: Seleccione la Zona creada anteriormente.
  * ```Address type```: Seleccione ```Unumbered```.
* De click en ```Ok```
* De click en ```Commit```> ```Commit configuration```


### Creación de VPN site to site
para esto siga la ruta ```VPN > create VPN > site to site```. Esto abrirá una pestaña de configuración, aquí ingrese la siguiente información.
* ```Name```: Ingrese un nombre para la conexión.
* De click sobre el icono de ```Remote Gateway```.Esto abrira una nueva pestaña de configuración, aquí ingrese la siguiente información:
  * ```External IP address```: ingrese la IP de Gateway de la VPN for VPC.
  * ```Protected networks```: Seleccione el segmento de red privado de la VPN que se creo anteriormente
  *  De click en ```Ok```
*  De click sobre el icono de ```Local Gateway```.Esto abrira una nueva pestaña de configuración, aquí ingrese la siguiente información:
  * ```Tunnel Interface```: Seleccione la interfaz creada anteriormente.
  * ```Pre-shared key```: Ingrese la misma contraseña que utilizo en la creación de la conexión VPN para VPC
  * ```Protected networks```: De click en ```+```y seleccione la zona privada de la VLAN creada anteriormente
  * De click en ```Ok```
* ```De click en IKE and IPsec Settings``` para configurar las políticas de acuerdo a las establecidas en la creación de la VPN for VPC que se encuentran en el siguiente repositorio.
* De click en ```Save```
* De click en ```Commit```> ```Commit configuration```

<br />
