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

#### **Paso 3: Consideraciones para Subnetting más Detallado**

- **Reto con subredes menores:** Si se utilizara un CIDR `/29`, el proceso implicaría contar de 8 en 8 desde `10.2.2.0` hasta `10.2.2.192`.

#### **Speed Tricks para Facilitar el Proceso**

Estos trucos de velocidad te ayudarán a manejar subnets más pequeñas de manera más eficiente, especialmente útiles cuando la red se divide en más subredes y necesitas ubicar rápidamente la posición de una IP específica dentro de esta estructura.

