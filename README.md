# Net_Practice

Bienvenidos a Net_Practice, un ejercicio exhaustivo destinado a dominar la configuración y resolución de problemas de redes. Este README te guiará a través de los conceptos esenciales requeridos para navegar y tener éxito en este proyecto.

<details>
<summary><strong>Conceptos</strong></summary>
  
### 1. TCP/IP
**IP (Internet Protocol Adresses):** Una cadena única de números separados por puntos (IPv4) o dos puntos (IPv6) que identifica un dispositivo en una red. Una dirección IP consta de dos partes principales: el ID de Red y el ID de Host, diferenciados por una máscara de subred. Por ejemplo, en la dirección IP `192.168.1.1/24`, el ID de Red es `192.168.1` y el ID de Host es `1` .

#### Subcomponentes:
- **Máscara de Subred:** Una combinación de bits que enmascara la dirección IP y divide los componentes de red y host.
- **ID de Red:**  La parte de la dirección IP que identifica la red específica.
- **ID de Host:** La parte de la dirección IP que identifica el dispositivo específico en la red.

### 2. IPv4 vs IPv6

La transición de IPv4 a IPv6 ha introducido cambios significativos en la tecnología del protocolo de internet. A continuación se muestra una tabla comparativa que destaca las diferencias clave entre estas dos versiones:

| Característica         | IPv4                                       | IPv6                                                  |
|------------------------|--------------------------------------------|-------------------------------------------------------|
| **Año de Despliegue**  | 1981                                       | 1998                                                  |
| **Capacidad de Bits**  | 32 bits                                    | 128 bits                                              |
| **Número de Direcciones**| ~4.3 mil millones                         | ~340 undecillones (3.4 × 10^38)                        |
| **Notación de Direcciones**   | Decimal separado por puntos (ej. 192.108.42.64)       | Hexadecimal separado por dos puntos (ej. 2002:0de6:0001:0042:0100:8c2e:0370:7234) |
| **Configuración**      | Configuración manual o DHCP                | Soporta auto-configuración y más opciones automáticas |
| **Uso de Direcciones** | Reutilización de direcciones por limitación de espacio | Cada dispositivo puede tener su propia dirección única |

### 3. Dispositivos

- **Switch:** Conecta dispositivos dentro del mismo segmento de red, reduciendo colisiones de tráfico de datos y gestionando efectivamente el flujo de datos a través de direcciones MAC (Control Media Access).
- **Router:** Enlaza múltiples redes o subredes, ya sean LAN (Red de Área Local) o WAN (Wide Area Network). Asegura la ruta óptima del tráfico, asigna IPs locales y realiza la traducción de direcciones mediante NAT (Network Address Translation). Componentes clave en su tabla de enrutamiento incluyen:
  - **Next Hop:** Indica la dirección IP del próximo router donde se enviarán los paquetes de datos.
  - **Destination:** Especifica la red de destino para los paquetes de datos.

- **Módem:** Un dispositivo que modula y demodula señales digitales y analógicas, permitiendo la conexión de una red a internet al traducir datos entre estos dos tipos de señales.

### 4. Subnetting

Subnetting implica dividir una red IP física en múltiples subredes lógicas. Cada subred opera independientemente en el nivel de envío y recepción de paquetes, aunque todas pertenecen a la misma red física y dominio.

### 5. Dirección Loopback

Un rango de dirección IP especial (127.0.0.0 a 127.255.255.255) reservado para comunicaciones internas dentro de un dispositivo. Esto permite que un dispositivo envíe y reciba paquetes hacia y desde sí mismo, lo cual es crucial para pruebas y gestión de redes.
  
</details>
<details>
<summary><strong>Mask Explanation</strong></summary>

# Mask Explanation

Para comenzar vamos a suponer que la network id abarca los 3 primeros octetos y solo vamos a interactuar con el último que va desde  ``192.168.1.0`` a `192.168.1.255`.

Este último octeto son 8 bytes, cada uno de los cuales puede ser `0` o `1`, por lo que si todos están activados(`11111111`) sería `2 ^ 8` = `256`.

Antes hemos comentado que la ip podíamos dividirla en **Network ID**, y **Host Id**, usando la máscara, de esta forma, cuando asignamos una máscara en notación CDIR `\24` estaríamos asignando los 3 primeros bytes (8 * 3 = 24 primeros bits) para la **Network ID**, y unicamente el último octeto de bits para el host, por lo que esta red (192.168.1.0/24) abarcaría desde ``192.168.1.0`` a `192.168.1.255`, abarcando 255 ip's posibles.

Podemos subdividir esta red en en dos redes de igual tamaño aplicando una máscara /25, es decir dejando libres para el host unicamente los 7 ultimos bits, estaríamos convirtiendo la red en dos redes: 

**Primera**. `192.168.1.0/25` que alberga 128 ip's de la `192.168.1.0` a la `192.168.1.128`.

**Segunda**.`192.168.1.128/25` que alberga 128 ip's de la `192.168.1.128` a la `192.168.1.255`.

De igual forma en vez de dividir la red en notación CDIR podemos hacerlo con la subnet mask, es decir `/25` correspondería con `255.255.255.128` que a su vez correspondería con `11111111.11111111.11111111.10000000` porque al ser el primer bit, `2 ^ 7` = `128`. Esto quiere decir que cada segmento de red con esta máscara abarca 128 posibles ip`s. 

Esto puede parecer un poco complejo, por eso te voy a presentar un cheat Sheat que te permitirá convertir de CDIR a Subnet Mask en 60 segundos.

</details>
<details>
<summary><strong>Cheat Sheet</strong></summary>

# Cheat Sheet

  Group Size  | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-------------|-----|----|----|----|---|---|---|---|
| Subnet Mask | 128 | 192| 224| 240| 248| 252| 254| 255 |
| CIDR        | /25 | /26| /27| /28| /29| /30| /31| /32 |

Crear esta tabla es realmente sencillo, especialmente si sigues estos pasos:

  **1.** La primera fila son 8 potencias de 2, desde `2 ^ 7`hasta `2 ^ 0`.
  
  **2.** La segunda fila la obtendrás de restar a 256 (ip's posibles), el **Group Size**.
  
  **3.** Por ultimo comenzando desde la izquierda, desde ´/25´ porque estás cogiendo el primer bit del 4 octeto hasta el total de bits que caben en 4 bytes.

</details>
<details>
<summary><strong>How to solve</strong></summary>

# How to solve

Primero abordemos una serie de conceptos :
  # Concepts:
  
   - **Network id**: La parte de la dirección IP que identifica la red específica.
   - **First id**: Primera ip util, la obtenemos sumando uno a la **Network id**
   - **Last id**:  última ip util, la obtenemos restando uno a la **Broadcast id**
   - **Broadcast id**: Dirección de red utilizada para transmitir a todos los dispositivos conectados a una red de comunicaciones de acceso múltiple.


Ahora que sabes crear tu propio **Cheat Sheet**, y conoces los conceptos necesarios, no hay escusas, podrás resolver cualquier problema de **Subnetting** en menos de 60 segundos siguiendo estos pasos:

# Steeps
Supongamos que queremos saber a que red pertenece la ip: ``10.2.2.199/26``

  **Steep 1.** 
    
  Miramos en la tabla el `/26` y observamos que como **Subnet Mask** se representaría con 255.255.255.`192`, esto proviene de `11000000`, es decir `2 ^ 7` = `128` + `2 ^ 6` = `64` = `192`, osea disponemos de 6 bits para el host, lo que divide la red en 4 subredes que cubren 64 ips cada una. 

  Podemos hacer lo siguiente:     
  
                                      10.2.2.0 
                                      10.2.2.64 
                                      10.2.2.128  
            **Network id**  ----->    10.2.2.192
                                            `10.2.2.193`     <------  **First id**
                                            `10.2.2.253`     <------  **Last id**
                                            `10.2.2.254`     <------  **Broadcast id**
            **Next id**  -------->    10.2.2.255

Dividimos el octeto .255 en 4 secciones de 64 ips, y vemos entre que segmento se encuentra nuestra ip `10.2.2.199/26`, en este caso vemos que se encuentra en el cuarto segmento, entre `10.2.2.192` y `10.2.2.254`, por lo que este primero será **Network id** y el segundo **Broadcast id**, dejando `64 - 2` = `62` direcciones dispoibles, desde la **First id** hasta la **Last id**.

Ahora que ya sabes resolver esto, puede resultarte incluso sencillo, pero puede resultar un proceso más lento cuando la red se divide en más subredes, por ejemplo si fuese un CDIR `/29`, Y tuviesemos qeu contanr desde `10.2.2.0` hasta `10.2.2.192` de 8 en 8.

Por eso te voy a facilitar los siguientes

# Speed Tricks:

    1. Multiplicar el **Group size** por **10**   EX: 8 * 10 = 80;    --->   .8
                                                                      --->  .80
                                                                      --->  .160  
    
    2. Multiplicar el Multiplicar el **Group size** por **2**         --->  .8
                                                                      --->  .80
                                                                                 x2
                                                                      --->  .160
                                                                      
    3. Todos los grupos pasan por 128, asique podemos partir de este número para iniciar la búsqueda.
    4. Todos los grupos pasan por el subnet Mask de su izquierda en la cheat sheet, asique es un buen momento 
    para hacer uso de esta, y en caso de pasarnos, empezar por un ip superior y restar el group size hasta encontrar el
    segmento al que pertenece nuestro ip objetivo.

</details>
<details>
<summary><strong>Levels</strong></summary>
                                                                                
