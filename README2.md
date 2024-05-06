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

![Imagen de Subnetting](images/mask.png)

**Nota Adicional:**
Dado que el proceso puede parecer complejo, se incluye un cheat sheet que facilita la conversión de CIDR a Subnet Mask en 60 segundos.

</details>

<details>
<summary><strong>Cheat Sheet</strong></summary>

### Cheat Sheet

La forma de interpretar esta **Tabla de Conversión** es la siguiente, cuando queremos descubrir a que red pertenece una ip, por ejemplo `255.255.255.192/26`, observamos que tiene una máscara `CDIR` `/26`, equivalente a `Subnet Mask` `192`, lo que nos indica que estamos dividiendo el 4 octeto en **Group Size** de 64 ips.

de aqui deducimos que son 4 subredes: `255 / 64` = `4`.
Con esta tabla y una serie de **steps** que te explicaré en **How to solve** podrás resolver cualquiér problema de subnetting en menos de 60 segundos, pero primero te explicaré como crear esta tabla desde cero.

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


 Si se utilizara un CIDR `/29`, el proceso implicaría contar de 8 en 8 desde `10.2.2.0` hasta `10.2.2.192`, lo que puede resultar en un proceso realmente lento y aburrido por eso voy a presentarte en el siguinte apartado unos **Speed Tricks**.

 # Speed Tricks:

Para simplificar el proceso a la hora de buscar a qué subred pertenece una ip, especialmente cuando el GROUP SIZE es pequeño, puedes utilizar estos trucos:

**1. Multiplicar el GROUP SIZE por 10:**
   - Ejemplo: 8 * 10 = 80; Resultados: .8, .80, .160

**2. Multiplicar el GROUP SIZE por 2:**
   - Resultados: .8 -> .80 -> .160 (multiplicar .80 por 2)

**3. Todos los grupos pasan por 128**, así que podemos partir de este número para iniciar la búsqueda.

**4. Todos los grupos pasan por la subnet mask de su izquierda en la cheat sheet**, por lo tanto, es un buen momento para hacer uso de esta, y en caso de pasarnos, empezar por una ip superior y restar el GROUP SIZE hasta encontrar el segmento al que pertenece nuestra ip objetivo.


