# Gateway-Appliance-Juniper-vSRX-version-20.4


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
   <img src=https://https://github.com/emeloibmco/Gateway-Appliance-Juniper-vSRX-version-20.4/blob/5743e32c5535533a8b69da0db87a0f410c485e0c/Imagenes/Crear%20Gateway%20Appliance.gif>
   </p>
  
<br />

## Ingresar a Juniper
Luego de desplegar el ```Gateway Appliance``` siga los pasos que se indican a continuación para ingresar a Juniper:

1. En el recurso desplegado, de click en la pestaña ```Visión general/Overview``` y allí visualice la sección ```vSRX```. Identifique los siguientes datos:

   * ```IP Pública```.
   * ```IP Privada```.
   * ```Nombres de usuario```: root y admin.
   * ```Contraseñas```.

2. En el navegador (se recomienda usar Firefox) coloque la ip pública y el puerto 8443, de la siguiente manera:

   ```
   https://ip_publica:8443
   ```
   
   Espera mientras carga la página
   
3. Una vez cargue la ventana, se le solicitará que coloque usuario y contraseña para acceder a Juniper. Complete los campos teniendo en cuenta:

   * ```Username```: coloque *admin*.
   * ```Password```: coloque la contraseña para el usuario *admin* obtenida en la sección ```vSRX```.

4. De click en el botón ```Log In``` para iniciar sesión en Juniper.

  <p align="center">
  <img src=https://github.com/emeloibmco/PowerVS-Conectividad/blob/main/Imagenes/Juniper.PNG>
  </p>
  
<br />
