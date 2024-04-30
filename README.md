# Net_Practice

Bienvenidos a Net_Practice, un ejercicio exhaustivo destinado a dominar la configuración y resolución de problemas de redes. Este README te guiará a través de los conceptos esenciales requeridos para navegar y tener éxito en este proyecto.

<details>
<summary><strong>Conceptos</strong></summary>
  
### 1. TCP/IP
**IP (Internet Protocol Adresses):** Una cadena única de números separados por puntos (IPv4) o dos puntos (IPv6) que identifica un dispositivo en una red. Una dirección IP consta de dos partes principales: el ID de Red y el ID de Host, diferenciados por una máscara de subred. Por ejemplo, en la dirección IP `192.168.1.1/24`, el ID de Red es `192.168.1` y el ID de Host es `1` .

#### Subcomponentes:
- **Máscara de Subred:** Una combinación de bits que enmascara la dirección IP y divide los componentes de red y host.
- **ID de Red:** La parte de la dirección IP que identifica la red específica.
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
