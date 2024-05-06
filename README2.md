# Net_Practice

Bienvenidos a Net_Practice, un ejercicio destinado a dominar la configuración y resolución de problemas de redes. Este README te guiará a través de los conceptos esenciales requeridos para navegar y tener éxito en este proyecto.

<details>
<summary><strong>Concepts</strong></summary>
  
### 1. TCP/IP
**IP (Internet Protocol Adresses):** Una cadena única de números separados por puntos (IPv4) o dos puntos (IPv6) que identifica un dispositivo en una red. Una dirección IP consta de dos partes principales: el **Network Id** y el **Host Id**, diferenciados por una **Subnet Mask** o máscara de subred. Por ejemplo, en la dirección IP `192.168.1.1/24`, el Network Id es `192.168.1` y el Host Id  es `1` .

#### Subcomponentes:
- **Subnet Mask:** Una combinación de bits que enmascara la dirección IP y divide los componentes de red y host.
- **Network Id:**  La parte de la dirección IP que identifica la red específica.
- **Host Id:** La parte de la dirección IP que identifica el dispositivo específico en la red.

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

### Introducción a la Máscara de Subred

**Contexto Inicial:**
Suponemos que la ID de red (Network ID) abarca los tres primeros octetos y solo interactuamos con el último octeto que va desde `192.168.1.0` hasta `192.168.1.255`.

**Detalles del Último Octeto:**
Este último octeto consta de 8 bits, cada uno de los cuales puede ser `0` o `1`. Si todos los bits están activados (`11111111`), el resultado es `2^8 = 256`.

**División de la IP:**
La dirección IP puede dividirse en **Network ID** y **Host ID** usando la máscara de subred. Asignando una máscara en notación CIDR `/24`, estaríamos designando los tres primeros octetos (24 bits) para la **Network ID** y solo el último octeto para el host, cubriendo así un rango de `192.168.1.0` a `192.168.1.255` con 256 IPs posibles.

### Subdivisión de la Red

**Aplicación de la Máscara /25:**
Podemos subdividir esta red en dos redes de igual tamaño usando una máscara `/25`, lo que deja libres solo los 7 últimos bits para el host. Esto convierte la red original en dos redes:

- **Primera Red:** `192.168.1.0/25` que alberga 128 IPs desde `192.168.1.0` hasta `192.168.1.128`.
- **Segunda Red:** `192.168.1.128/25` que alberga 128 IPs desde `192.168.1.128` hasta `192.168.1.255`.

**Notación de la Subnet Mask:**
Alternativamente, en lugar de usar la notación CIDR, podemos emplear la subnet mask directa `/25`, que corresponde a `255.255.255.128`. Esta máscara en binario es `11111111.11111111.11111111.10000000`, donde el primer bit `2^7 = 128` indica que cada segmento de red con esta máscara abarca 128 IPs posibles.

**Nota Adicional:**
Dado que el proceso puede parecer complejo, se incluye un cheat sheet que facilita la conversión de CIDR a Subnet Mask en 60 segundos.

</details>

<details>
<summary><strong>Cheat Sheet</strong></summary>

### Cheat Sheet

La forma de interpretar esta **Tabla de Conversión** es la siguiente, cuando queremos descubrir a que red pertenece una ip, por ejemplo `255.255.255.192/26`, observamos que tiene una máscara `CDIR` `/26`, equivalente a `Subnet Mask` `192`, lo que nos indica que estamos dividiendo el 4º octeto en **Group Sizes** de 64 ips.

De esta forma deducimos que son 4 subredes: `256 / 64` = `4`.
Con esta tabla y una serie de **steps** que te explicaré en la siguiente sección: **How to solve** podrás resolver cualquiér problema de subnetting en menos de 60 segundos, pero primero te explicaré como crear esta tabla desde cero.

| Tamaño de Grupo | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----------------|-----|----|----|----|---|---|---|---|
| Máscara de Subred | 128 | 192| 224| 240| 248| 252| 254| 255 |
| CIDR             | /25 | /26| /27| /28| /29| /30| /31| /32 |

**Pasos para Crear la Tabla:**
1. **Primera fila:** Representa las potencias de 2, desde `2^7` hasta `2^0`.
2. **Segunda fila:** Se obtiene restando a 256 (número total de IPs en un octeto), el tamaño de grupo correspondiente.
3. **Cálculo CIDR:** Comenzando desde la izquierda, con `/25` tomando el primer bit del cuarto octeto hasta cubrir todos los bits posibles en cuatro octetos.

si necesitas dividir el tercer octeto, unicamente tienes que añadir una fila más, empezando por le `/24`de derecha a izquierda. 

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

![Imagen de Subnetting](images/mask.png)

Ahora que sabes crear tu propio **Cheat Sheet**, y conoces los conceptos necesarios, no hay escusas, podrás resolver cualquier problema de **Subnetting** en menos de 60 segundos siguiendo estos pasos:

### **Steeps**.

Supongamos que queremos averiguar a que red pertenece la siguiente **IP: 10.2.2.199/26**

#### **Paso 1: Analizar la Máscara de Subred**

- **Máscara de Subred:** `/26` que corresponde a `255.255.255.192`. Esto se deriva del patrón binario `11000000`, que indica:
  - `2^7 = 128`
  - `2^6 = 64`
  - Suma de bits: `128 + 64 = 192`
- Con esta configuración, disponemos de 6 bits para el host, dividiendo la red en 4 subredes que cubren 64 IPs cada una.

#### **Paso 2: Identificar las Subredes y Posicionar la IP Dada**

- **Subredes Disponibles:**
  1. `10.2.2.0` a `10.2.2.63`
  2. `10.2.2.64` a `10.2.2.127`
  3. `10.2.2.128` a `10.2.2.191`
  4. `10.2.2.192` a `10.2.2.255` (la subred de interés)

- **Detalles de la Subred de Interés:**
  - **Network ID:** `10.2.2.192`
  - **First ID:** `10.2.2.193`
  - **Last ID:** `10.2.2.253`
  - **Broadcast ID:** `10.2.2.254`
  - **Next ID:** `10.2.2.255`

- **Posición de la IP `10.2.2.199/26`:** 
  - Se encuentra dentro de la cuarta subred (`10.2.2.192` a `10.2.2.254`).
  - **Disponibilidad de Direcciones:** `64 - 2 = 62` direcciones, desde la `First ID` hasta la `Last ID`.


 Si se utilizara un CIDR `/29`, el proceso implicaría contar de 8 en 8 desde `10.2.2.0` hasta `10.2.2.192`, lo que puede resultar en un proceso realmente lento y aburrido por eso voy a presentarte en el siguiente apartado unos **Speed Tricks** que llevarán tu eficiencia al siguiente nivel.

 # Speed Tricks:

Para simplificar el proceso a la hora de buscar a qué subred pertenece una ip, especialmente cuando el GROUP SIZE es pequeño, puedes utilizar estos trucos:

**1. Multiplicar el GROUP SIZE por 10:**
   - Ejemplo: 8 * 10 = 80; Resultados: .8, .80, .160

**2. Multiplicar el GROUP SIZE por 2:**
   - Resultados: .8 -> .80 -> .160 (multiplicar .80 por 2)

**3. Todos los grupos pasan por 128**, así que podemos partir de este número para iniciar la búsqueda.

**4. Todos los grupos pasan por la subnet mask de su izquierda en la cheat sheet**, por lo tanto, es un buen momento para hacer uso de esta, y en caso de pasarnos, empezar por una ip superior y restar el GROUP SIZE hasta encontrar el segmento al que pertenece nuestra ip objetivo.

</details>

<details>
<summary><strong>Levels</strong></summary>

- <details>
  <summary><strong>Level 6</strong></summary>

   El nivel 6 presenta dos redes conectadas por un router, la primera parte de `internet` y la segunda pasando por un switch desemboca en `Host A`.
  Nos condicionan que en esta segunda red usaremos una máscara `255.255.255.128` es decir `/25` y la interfaz del host en `110.98.32.227`, por lo que estamos diviendo la red `110.98.32.0/24` en dos grupos de 128 y vamos a usar el segundo, por lo que cualquier valor entre `110.98.32.128`(Network Id) y `110.98.32.255`(Broadcast Id), estos no incluidos, nos valdria para la interfaz del router.

  Lo importante en este nivel es que el destino del internet apunte a esta red (`110.98.32.128/25`) para permitir el tráfico.
  
  <img src="images/Level6.png" alt="Level 6 image" width="85%" height="85%">

  </details>

- <details>
  <summary><strong>Level 7</strong></summary>

  En este nivel, se da una conexión entre dos routers, cada uno de los cuales conecta con un host, ambas interfaces de R1 nos condicionan a dividir la red `105.198.14.0/24`, por lo que, para mí, lo más oportuno en este caso es dividirla en `4` subredes de `64` ip's aplicando una máscara `26`, usando la primera subred creada para conectar `A1` y `R1`, la última (entre 192 y 255) para conectar los routers, y la segunda o la tercera para conectar R2 y C1.
  
  En cuanto a la **Routing Table**, es los destinos se pueden dejar por defecto, lo importante es que el **Next Hop** de los routers se apunten entre sí, para intercambiar el tráfico, y ambos host deben apuntar al siguiente router.
   
  <img src="images/Level7.png" alt="Level 7 image" width="90%" height="90%">

  </details>

- <details>
  <summary><strong>Level 8</strong></summary>

  En el nivel 8 tenemos dos routers conectados, el primero conecta con internet, y el segundo conecta a través de dos redes al host D y C.
  
  A mí entre routers me gusta usar una máscara de red `/30`, es decir 4 ips, de las cuales, si excluimos la **Network id** y la **Broadcast id**, nos quedan dos, es decir las necesarias para conectar dos routers, en este caso el **Next Hop** de **R2**, nos proporciona la ip de la interface R13, y para la de R21 podemos usar un valor por debajo.
  
  Por último, intenet solo tiene destino en una red: `158.46.67.0/26` asique haremos subnetting de esta, para conectar ambos host a internet. se nos proporciona una máscara `255.255.255.240`, es decir `/28`, que alberga 16 ips, esto es muy sencillo de comprobar con la **Cheat Sheet** que te proporcioné anteriormente.
  
  Asique para el Host D, podemos usar caulquier valor entre los 16 primeros ips, Network id y Broadcats ip excluidos, y para el Host C del `.17` hasta el `.30` si mantenemos la máscara `/28`, asegurandonos así que no hacemos **overlapping** con el rango que usamos para conectar los routers.

  No te ovlides de establecer el destino en la red de los host `158.46.67.0/26` y el **Next Hop** de internet en la interfaz del siguiente router.
  
   <img src="images/Level8.png" alt="Level 8 image" width="90%" height="90%">

  </details>

- <details>
  <summary><strong>Level 9</strong></summary>

  Este nivel presenta tres redes que deben conectarse a internet, Host A y B, que deben conecarse entre sí, y a R1 a través de un switch, por lo que los albergaremos en una misma red. una red que conecta los routers, R1 y R2, este último conecta dos redes una que concluye en Host D y otra en Host C.

  Será sencillo si dividimos el problema en pequeñas fracciones.

  **step1. Conectar los host C y D**
  - Se nos impone la IP de la interfaz R23, ya que es el **Next Hop** de la **Routing Table** de D1, con una máscara de `/18`, si nos fijamos en el **Cheat Sheet**, nos será fácil descubrir que el **Group size** es de 64 IP's, en el 3º octeto, así que dado que la IP de la interfaz R23 es `94.8.218.81`, sabemos que la **Network id** es: `94.8.192.0/18` y la **Broadcast id** es `94.8.255.255/18` y cualquier valor entre estos nos valdría.
  - Para conectar el Host C, puedes establecer cualquier IP de tu elección, y cualquier máscara de red, nosotros para hacerlo sencillo elegiremos `42.24.42.0/25`, dividiendo la red en dos subredes de '128', y utilizaremos la primera.

  **step2. Conectar los dos Routers**
  - Como venimos practicando, se establece una máscara CDIR `/30`, que contiene 4 IPs de las cuales dos son útiles, para mantenerlo sencillo podríamos elegir cubrir las 4 primeras IPs de cualquier red a tu elección, en este caso elegimos: `192.32.4.0/30`.
  - He aquí la cuestión de este nivel, conectar las **Routing Table**, cada Router **Next Hop** debe apuntar al siguiente router, pero en el destino del primero, debemos apuntar tanto a la red del Host C (Para conectarlo a internet), como a la red del Host D para conectarlo con Host A.

  **step3. Conectar los Host A y B**
  - Tenemos 3 dispositivos, en una misma red, lo único importante es que en ambos Host, el Next Hop apunte a la interfaz de R11, en este caso hemos elegido esta red `33.63.9.0/25`.

  **step4. Routing Table de internet**
  - El Next Hop está configurado a la interfaz del router, bastaría con configurar dos destinos a las redes del Host C, `42.24.42.0/25` y la red que conecta A y B `33.63.9.0/25`, que son lo que no se piden que conecte a internet.  
  
   <img src="images/Level9.png" alt="Level 9 image" width="90%" height="90%">
  </details>

- <details>
  <summary><strong>Level 10</strong></summary>

  Last level!, no te asustes aonque parezca compliado es bastante sencillo, tenemos una red que conecta internet con un router, **R1**, este router conecta con una red que une los dos primeros host con un switch, por otro lado **R1** conecta con un segundo router **R2**, que conecta dos redes que desembocan en **Host 3** y **Host 4**.

  La cuestión es que los host 1, 3 y 4 deben conectar a internet, pero internet, en su **Routing Table** solo tiene un `destino`, asique la logica nos lleva a hacer subnetting de la red en `140.45.158.0/24`, y establecer esta como destino(tanto en internet como en **R1**), así llegando a cualquier host que se albergue en el rango `0-255`.
  dividamos el problema en subproblemas:

  **step1. Conectar los dos primeros host**

   nos condicionan con una máscara `/25` asique asignamos cuaqluier valor entre .0 y .255 ambos incluidos al último octeto.

  **step2. Conexión entre routers**

  nos condicionan con un `255.255.255.252` es decir `/30`es decir 4 ips, de las cuales, si excluimos la **Network id** y la **Broadcast id**, nos quedan dos, es decir las necesarias para conectar dos routers.
  Esto es una buena práctica, no usar más ips de las requeridas.

  **step3. Conectar los dos últimos host**

   Conectar los Host 3 y 4 al Router 2, estamos condicionados por el router 3 a una máscara `255.255.255.192` que en CDIR es `/26`(**Group size** de 64 ip's), fijándonos en las ip´s que nos proporcionan estaríamos ocupando desde `.128` a `.192`.
  por lo tanto para conectar el Host 4, si pusisiesemos también una máscara /26 ocuparíamos desde la `192` hasta `255`, y estaríamos haciendo **overlapping**, es decir se estaría solapando con la red `140.45.158.252/30`que hemos usado previamente como conexión entre routers.
  Para soluccionar esto es tan sencillo como aplicar una máscara `/27`que ocupa 32 ips, y estableciendo estas en un rango entre `140.45.158.192` y `140.45.158.224`.

   <img src="images/Level10.png" alt="Level 10 image" width="90%" height="90%">
</details                             
