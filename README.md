# Net_Practice

<p align="center">
  <img src="https://github.com/ayogun/42-project-badges/blob/main/badges/netpracticem.png" alt="Net Practice">
</p>

Bienvenidos a **Net_Practice**, un ejercicio destinado a dominar la configuración y resolución de problemas de redes. Este README te guiará a través de los conceptos esenciales requeridos para conectar dispositivos en un misma red, dividir redes y conectarlas para tener éxito en este proyecto.

### How to Practice

Al `Maestro` lo hace la practica, asique para practicar este ejercicio, sigue estos pasos:

1. **Clona el repositorio:**
   ```bash
   git clone git@github.com:Pablo-Palma/Net_Practice.git
   ```

2. **Entra en el directorio que contiene el `index.html`:**
   ```bash
   cd Net_Practice/net_practice
   ```

3. **Lanza el archivo con:**
   ```bash
   open index.html
   ```

Esto abrirá en tu navegador una web con una serie de niveles interactivos. Deberás introducir tu nombre o apodo e ir superando uno a uno estos niveles hasta llegar al máximo nivel.

Si ya tienes cierta soltura, puedes dejar el nombre vacío y te saldrán `3` niveles aleatorios del `6` al `10`, para que puedas ponerte a prueba.

Te recomiendo comenzar entendiendo los **Concepts** y como funciona el protocolo **TCP/IP addressing** y echar un vistazo al **Cheat Sheet** y los **Speed tricks** que te proporciono para que puedas llevar tus habilidades al siguiente nivel.


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

<details >
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

     ## Nivel 6: Configuración de Redes con Router
  
  ### Estructura de la Red
  El nivel 6 involucra dos redes conectadas por un router:
  - **Primera red:** Directamente conectada a `internet`.
  - **Segunda red:** Conectada a través de un switch, terminando en `Host A`.
  
  ### Configuración de la Segunda Red
  Para la segunda red, se aplican las siguientes configuraciones:
  - **Máscara de Subred:** `255.255.255.128` (`/25`)
  - **Dirección IP de Host A:** `110.98.32.227`
  
  ### División de la Red
  La red `110.98.32.0/24` se divide en dos grupos de 128 direcciones IP cada uno. Utilizaremos el segundo grupo, que comprende:
  - **ID de Red:** `110.98.32.128`
  - **ID de Broadcast:** `110.98.32.255`
  
  Las direcciones válidas para la interfaz del router están entre `110.98.32.129` y `110.98.32.254`, excluyendo los IDs de red y broadcast.
  
  ### Objetivo Clave
  Es crucial asegurarse de que el destino del tráfico de internet esté configurado para apuntar a la red `110.98.32.128/25` para facilitar el flujo adecuado del tráfico.


  
  <img src="images/Level6.png" alt="Level 6 image" width="85%" height="85%">

  </details>

- <details>
  <summary><strong>Level 7</strong></summary>

  ### Descripción del Escenario
  Este nivel involucra la configuración de una conexión entre dos routers, cada uno conectando un host. Se requiere dividir la red `105.198.14.0/24`.

  ### División de la Red
  Para una organización eficiente, la red se divide en `4` subredes de `64` IPs cada una, utilizando una máscara de subred `/26`:
  - **Primera Subred:** Utilizada para conectar `A1` y `R1` (Direcciones entre .0 y .64).
  - **Última Subred:** (Direcciones entre .192 y .255) Usada para conectar los dos routers.
  - **Segunda o Tercera Subred:** Para conectar `R2` y `C1`. (Direcciones entre .64 y .192).
 
  Es esencial evitar el `overlapping`.

  ### Configuración de la Tabla de Enrutamiento
  - **Destinos:** Los destinos pueden configurarse con los valores por defecto.
  - **Next Hop:** Es crucial que el `Next Hop` en los routers esté configurado para apuntarse entre sí, permitiendo un intercambio eficiente de tráfico. Los hosts deben apuntar al router siguiente.

  ![Diagrama del Nivel 7](images/Level7.png)

  </details>

- <details>
  <summary><strong>Level 8</strong></summary>

    ### Descripción del Escenario
  En el nivel 8, dos routers forman el núcleo de la configuración:
  - **R1:** Conectado directamente a internet.
  - **R2:** Conecta dos redes que a su vez conectan los hosts `D` y `C`.

  ### Configuración de Conexión entre Routers
  Se prefiere utilizar una máscara de red `/30` para la conexión entre routers, proporcionando 4 IPs:
  - **ID de Red:** Excluida.
  - **ID de Broadcast:** Excluida.
  - **IPs Disponibles:** Dos, utilizadas para los interfaces de `R1` y `R2` respectivamente.
  
  El **Next Hop** de `R2` utiliza la IP de la interfaz `R13`, y la interfaz `R21` puede usar una IP menor dentro del mismo rango.

  ### Subnetting y Conexión a Internet
  Se realiza subnetting en la red `158.46.67.0/26` con una máscara `/28`, que proporciona 16 IPs por subred:
  - **Para Host D:** Utiliza cualquiera de las primeras 16 IPs (excluyendo ID de red y broadcast).
  - **Para Host C:** Ocupa el rango de `.17` a `.30` bajo la misma máscara `/28`, asegurando no solapar con el rango usado para los routers.

  ### Rutas y Enrutamiento
  - **Destino de la Red de Hosts:** `158.46.67.0/26`.
  - **Next Hop de Internet:** Debe configurarse en la interfaz del siguiente router.

  ![Diagrama del Nivel 8](images/Level8.png)

  </details>

- <details>
  <summary><strong>Level 9</strong></summary>

  
  ### Descripción General
  Este nivel presenta la tarea de conectar tres redes a internet, con enfoques específicos para los Hosts A y B, y para los Hosts C y D, coordinados a través de dos routers, R1 y R2.

  ### Paso 1: Conexión de los Hosts C y D
  - **IP de la interfaz R23:** `94.8.218.81` con una máscara `/18`.
  - **Rango de Red D:** 
    - **Network ID:** `94.8.192.0/18`
    - **Broadcast ID:** `94.8.255.255/18`
  - **Rango de Red C:** 
    - Puedes establecer cualquier IP válida de tu elección para el **Host C**, Para simplificar, se usará la red `42.24.42.0/25`, dividiéndola en dos subredes de 128 IPs cada una, y se empleará la primera para el **Host C**, dandote libre elección entre los valores de:
      - **Network ID:** `42.24.42.0/25`
      - **Broadcast ID:** `42.24.42.128/25`  

  ### Paso 2: Conexión de los dos Routers
  - **Configuración de Máscara CDIR `/30` para R1 y R2:** Esta configuración proporciona 4 IPs, dos de las cuales son útiles.
  - **Ejemplo de Red:** `192.32.4.0/30`.
  - Es esencial que cada Router apunte su **Next Hop** al otro router. Además, el destino en el primer router debe incluir tanto la red del `Host C` para acceso a `internet` como la del `Host D` para la conexión con `Host A`.

  ### Paso 3: Conexión de los Hosts A y B
  - Se conectan tres dispositivos en la misma red `33.63.9.0/25`.
  - Es importante que el **Next Hop** en ambos Hosts A y B apunte a la interfaz de R11.

  ### Paso 4: Configuración de la Tabla de Enrutamiento de Internet
  - **Next Hop:** Configurado para apuntar a la interfaz del router.
  - **Destinos:** Debe configurarse para incluir las redes del Host C `42.24.42.0/25` y la red que conecta A y B `33.63.9.0/25`, que son esenciales para la conexión a internet.

  ![Diagrama del Nivel 9](images/Level9.png)
  
  </details>

- <details>
  <summary><strong>Level 10</strong></summary>

  ### Descripción General
  Último nivel! No es tan complicado como parece. Tenemos un esquema donde el router **R1** conecta internet con los dos primeros hosts a través de un switch, y también conecta con otro router, **R2**, que a su vez conecta dos redes que terminan en **Host 3** y **Host 4**.

  La clave aquí es que los hosts 1, 3 y 4 deben conectarse a internet, pero la tabla de enrutamiento de internet solo reconoce un `destino` para todo el rango `140.45.158.0/24`.

  ### Paso 1: Conexión de los Primeros Dos Hosts
  - Se asigna una máscara `/25`, permitiendo IPs en el último octeto desde `.0` a `.128`.

  ### Paso 2: Conexión entre Routers R1 y R2
  - Se establece una máscara `/30` (`255.255.255.252`), lo que nos deja 4 IPs, dos de las cuales son efectivamente útiles después de excluir la **Network ID** y la **Broadcast ID**.

  ### Paso 3: Conexión de los Últimos Dos Hosts
  - Hosts 3 y 4 se conectan a **R2** bajo una máscara `255.255.255.192` (`/26`), ocupando desde `.128` a `.192`.
  - Para evitar solapamientos con la red `140.45.158.252/30` usada entre R1 y R2, aplicamos para el Host 4 una máscara `/27` que cubre 32 IPs, usando el rango `140.45.158.192` a `140.45.158.224`.

  ![Diagrama del Nivel 10](images/Level10.png)

  Si has llegado hasta aquí, supongo que, eres de ese tipo de persona que comienza un libro por la última página o qué te ha sido útil esta guía.
  
  Enhorabuena!, estás a un paso de convertirte en un `master` del `Networking` y ese paso es la práctica.
  Si te ha servido esta guía no dudes en darle una estrella al repo para consultarlo más adelante y compartirlo con tus amigos para que también se conviertan en unos `Masters!`.

  No dudes en contactarme si te ha quedado alguna duda o quieres aportar mejoras, un saludo.

  Pablo Palma.
</details>                            
