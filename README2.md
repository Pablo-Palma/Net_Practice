

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

**Tabla de Conversión:**

| Tamaño de Grupo | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----------------|-----|----|----|----|---|---|---|---|
| Máscara de Subred | 128 | 192| 224| 240| 248| 252| 254| 255 |
| CIDR             | /25 | /26| /27| /28| /29| /30| /31| /32 |

**Pasos para Crear la Tabla:**
1. **Primera fila:** Representa las potencias de 2, desde `2^7` hasta `2^0`.
2. **Segunda fila:** Se obtiene restando a 256 (número total de IPs en un octeto), el tamaño de grupo correspondiente.
3. **Cálculo CIDR:** Comenzando desde la izquierda, con `/25` tomando el primer bit del cuarto octeto hasta cubrir todos los bits posibles en cuatro octetos.

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

**IP: 10.2.2.199/26**

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


- **Reto con subredes menores:** Si se utilizara un CIDR `/29`, el proceso implicaría contar de 8 en 8 desde `10.2.2.0` hasta `10.2.2.192`, lo que puede resultar en un proceso realmente lento y aburrido por eso voy a presentarte en el siguinte apartado unos **Speed Tricks**.

