INTRODUCCIÓN
Se trabajará con el "DOFBOT" el cual es un brazo robótico de 6 grados de libertad, entre los propositos de este se encuentra el aprendizaje y desarrollo de aplicaciones en la robótica tales como el control de movimiento e inteligencia artificial. Esta robot se basa en la plataforma de Jetson Nano, el cual es un módulo de cómputo en NVIDIA especializado en procesar datos y aplicarlos para la inteligencia artificial y darle una visión computacional. Sin mencionar que, es compatible con entornos de desarrollo como lo son "OpenCV" y "TensorFlow". 
De los principales usos que le podemos dar se encuentra: el reconocimiento de imagenes, seguimiento de objetos, manipulación de piezas y control por gestos. 
Dentro de este reporte técnico se va a documentar, principalmente, la estructura mecánica, electrónica y de software, incluyendo caracterísitcas, interfaces de comunicación, procesos de operación y restriccones; con el fin de dar una referencia técnica para la instalación y configuración del "DOFBOT". 

DESCRIPCIÓN DEL SISTEMA MECÁNICO
El sistema mecánico cuenta con una estructura que nos garantiza la estabilidad y precisión en los movimientos.
En cuanto a la estructura y materiales, se fabricó con una aleación de aluminio anodizado de 2mm de espesor, cuyos componentes están diseñados para soportar un uso prolongado de tiempo y para prevenir deformaciones. A su vez también cuenta con un diseño modular que facilita su ensamblaje y desmontaje. 
Para alcanzar los 6 grados de libertad se hizo uso de: una base robotica, una articulación de hombro, una articulación de codo, una rotación de muñeca, una flexión de muñeca y una pinza de agarre. A diferencia de la pinza de agarre que requiere de un servomotor de 6 [kg*cm], el resto de los grados de libertad son otorgados por servomotores de 15 [kg*cm] (alimentados con 12V a 5 A) cada uno, estos 5 servomotores cuentan con comunicación por bus. La base cuenta con antideslizantes que aseguran el montaje del "DOFBOT" en diferentes superficies lisas, a su vez tiene la opción de fijarse de manera mecánica a una mesa de trabajo. 

DESCRIPCIÓN DEL SISTEMA ELECTRÓNICO
Su control se basa en la plataforma Jetson Nano, la cual se encarga de proporcionar la conectividad y el procesamiento. La placa de expansión multifuncional permite compatibilidad con; la Jetson Nano, Raspberry Pi, Arduino y Micro:bit, así como con sensores y módulos adicionales. También cuenta con un regulador de voltaje integrado para distribuir alimentación a servomotores. Sin mencionar, la cámara HD con sensor de imagen de alta resolución que puede ser usada para la visión artificial.
Para su interfaz de comunicación cuenta con 6 interfaces de conexión: 
1. GPIO (40 pines de entrada/salida) para sensores y actuadres externos.
2. I2C (comunicación en bus serie) para pantallas, sensores inteligentes y módulos adicionales.
3. PWM (control de servomotores) para el manejo de las articulaciones.
4. UART (comunicación serial) para enlazar microcontroladores
5. USB  (4 puertos USB 3.0 y 2.0) para el uso de las camaras, controladores y almacenamiento externo.
6. Wifi/Bluetooth (comunicación inalámbrica) para el control remoto del robot.
La Jetson Nano (unidad de procesamiento) es el cerebro del "DOFBOT", ejecuta los algoritmos de visión artificial, procesa los datos y controla los movimientos. También se encarga de puertos de comunicación como los GPIO, 12C, UART y USB.
Por otro lado, la placa PCA9685 controla los servomotores por medio de ángulos recibidos por la Jetson Nano.

DESCRIPCIÓN, DIAGRAMA DE BLOQUES Y TABLAS REFERENTES A LOS PUERTOS E INTERFACES DE COMUNICACIÓN DE ELEMENTOS
  DESCRIPCIONES DE LAS INTERFACES DE COMUNICACIÓN: 
  GPIO: Son los pines de entras y salida, pueden recibir señales digitales de los sensores y enviar señales de control, pueden ser operados con 3.3V.
  I2C:Es un bus de comunicación en serie que permite conectar varios dispositivos  con el uso de cambles SDA y SCL. 
  PWM: La señal modulada en ancho de pulso se encarga de controlar la posición de los servomotores, esto lo hace por medio de los ángulos de rotación. 
  UART: Es un protocolo de comunicación serial asíncrona que se utiliza para enviar y recibir datos entre el Jetson Nano y los microcontroladores externos. 
  USB: Esta interfaz permite conectar la cámara HD y otros dispositivos de almacenamiento. 
  Wifi/Bluetooth: Es la conexión inalámbrica que permite controlar el robot desde una PC, teléfono móvil o tablet a través de una aplicación web o SSH. 
  Interfaz PS2: Ayuda a controlar el "DOFBOT" de manera manual, recibiendo señales de botones y joysticks. 
  
  DIAGRAMA DE BLOQUES DEL SISTEMA: 
  Este diagrama muestra la arquitectura de comunicación del DOFBOT:
                   +------------------+
                   |   Jetson Nano    |
                   +------------------+
                             │
       ┌─────────────────────┼───────────────────────────┐
       │                     │                           │
  +-----------+      +------------------+       +-----------------+
  |   GPIO    |      |       I2C        |       |      UART       |
  +-----------+      +------------------+       +-----------------+
       │                     │                           │
       │                     │                           │
  +-----------+      +------------------+       +-------------------+
  |  Sensores |----->|   Módulos I2C    |       |  Microcontrolador |
  |  Digitales|      | (Pantalla LCD,   |       |  (Arduino/ESP32)  |
  +-----------+      |  Sensores, IMU)  |       +-------------------+
                     +------------------+
                            │
                            │
                     +-----------------+
                     |   Servomotores  |
                     |   (PWM control) |
                     +-----------------+
                     
  TABLA REFERENTE A LOS PUERTOS E INTERFACES DE COMUNICACIÓN DE ELEMENTOS:
  Resumen de los puertos de comunicación: 
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |  PUERTO  |    TIPO     |  CANTIDAD |                   DESCRIPCIÓN                   |             APLICACIONES            |
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |   GPIO   |   Digital   | 40 pines  | Pines programables como entrada/salida          |Sensores, LEDs, relés                |
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |    I2C   |    Serial   | 2 buses   | Comunicación con dispositivos I2C               |Controladores inalámbricos           |
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |    PWM   |   Digital   | 6 canales | Modulación de ancho de pulso                    |Control de servomotores              |
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |   UART   |    Serial   | 2 puertos | Comunicación en serie con dispositivos externos |Controladores inalámbricos           |
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |  USB 3.0 |    Serial   | 2 puertos | Alta velocidad de transferencia                 |Conexión de cámara HD, almacenamiento|
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |  USB 2.0 |   Serial    | 2 puertos | Transferencia est+andar                         |Controladores inalámbricos           |
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |   Wifi   | Inalámbrico | 1 módulo  | Comunicación inalámbrica                        |Control remoto robot                 |
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |Bluetooth | Inalámbrico | 1 módulo  | Conexión con dispositivos externos              |Controladores inalámbricos           |
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+
  |    PS2   |   Digital   | 1 puerto  | Conexión de un control                          |Control manual brazo robótico        |
  +----------+-------------+-----------+-------------------------------------------------+-------------------------------------+

  APLICACIONES:
  Aplicaciones y funcionalidades de cada interfaz: 
  +----------+---------------------------------------------+----------------------------------------------------------+
  | INTERFAZ |                FUNCIONALIDAD                |                      EJEMPLOS DE USO                     |
  +----------+---------------------------------------------+----------------------------------------------------------+
  |   GPIO   |Control de sensores y actuadores             |Encender un LED, activar un sensor de proximidad          |
  +----------+---------------------------------------------+----------------------------------------------------------+
  |    I2C   |Comunicación con dispositivos de expansión   |Conectar un módulo IMU para medir inclinación             |
  +----------+---------------------------------------------+----------------------------------------------------------+
  |    PWM   |Control de servomotores                      |Posicionar el brazo en un ángulo específico               |
  +----------+---------------------------------------------+----------------------------------------------------------+
  |   UART   |Comunicación en serie con microcontroladores |Recibir datos de un sensor conectado a un microcontrolador|
  +----------+---------------------------------------------+----------------------------------------------------------+
  |    USB   |Conexión de periféricos                      |Capturar imágenes con la cámara HD                        |
  +----------+---------------------------------------------+----------------------------------------------------------+
  |   Wifi   |Control remoto del robot                     |Enviar comandos desde un smartphone                       |
  +----------+---------------------------------------------+----------------------------------------------------------+
  |Bluetooth |Conexión con controladores inalámbricos      |Control del brazo por medio de botones y joystick         |
  +----------+---------------------------------------------+----------------------------------------------------------+

  CONSIDERACIONES TÉCNICAS:
  +
  +
  +
  +

DESCRIPCIÓN DE SOFTWARE, ESTRUCTURA DE PAQUETES, DESCRIPCIÓN DE LIBRERÍAS PROPIERARIAS Y DE TERCEROS NECESARIAS, LISTADO DE PROGRAMAS DE OPERACIÓN DEL ROBOT Y DESCRIPCIÓN DE SU PROPÓSITO. 
1. Descripción del Software
El software del DOFBOT está diseñado para aprovechar las capacidades del Jetson Nano, integrándose en un entorno Linux (generalmente Ubuntu) y aprovechando herramientas de desarrollo modernas para robótica. Está compuesto por:

Arquitectura modular: El sistema está dividido en varios módulos que gestionan la adquisición de datos de sensores, procesamiento de imagen y ejecución de algoritmos de control.

Integración con ROS: La implementación se apoya en el Robot Operating System (ROS) para gestionar la comunicación entre nodos, facilitando la interoperabilidad de componentes (sensores, actuadores y módulos de inteligencia) y permitiendo la expansión futura.

Soporte para visión y AI: Incluye componentes para el procesamiento de imágenes (por ejemplo, usando OpenCV) y, en algunos casos, integración con frameworks de aprendizaje automático (como TensorFlow o PyTorch) para tareas de reconocimiento o navegación inteligente.

Interfaz de usuario y control remoto: Proporciona herramientas y programas que permiten tanto el control manual (teleoperado) como la operación autónoma del robot.


2. Estructura de Paquetes
El repositorio se organiza de forma que facilita el desarrollo y despliegue del sistema completo. Entre los principales directorios y paquetes se encuentran:

  Espacio de trabajo ROS (ros_ws):
        src: Contiene el código fuente de los nodos ROS desarrollados para DOFBOT. Aquí se alojan los módulos de control, procesamiento de imagen y comunicación.
        launch: Archivos de lanzamiento (launch files) que permiten iniciar de forma conjunta y coordinada los distintos nodos y servicios necesarios para el funcionamiento del robot.
        config: Archivos de configuración con parámetros críticos, como la calibración de sensores, parámetros de control de motores y configuraciones de red.


  Documentación (/doc):
    Este directorio reúne manuales de instalación, guías de uso y notas de desarrollo que ayudan a comprender tanto la estructura interna como el proceso de despliegue del software.

  Scripts (/scripts):
    Scripts de automatización que facilitan tareas comunes, como la inicialización del entorno, actualizaciones de firmware y diagnósticos del sistema.


3. Librerías y Dependencias
Librerías Propietarias
    Drivers y Controladores de Hardware:
    Desarrollados por Yahboom, estos módulos permiten la comunicación directa con los actuadores y sensores específicos del DOFBOT. Incluyen rutinas optimizadas para el manejo de motores, servos y dispositivos     
    periféricos.

    Interfaces de Abstracción:
    Librerías diseñadas para encapsular funciones específicas del hardware, de forma que se simplifique la integración en el ecosistema ROS y se permita la reutilización en otros proyectos de la misma familia de robots.

Librerías de Terceros

  ROS (Robot Operating System):
    El núcleo del sistema se apoya en ROS, que permite la estructuración en nodos, la mensajería entre procesos y la integración con numerosos paquetes disponibles en la comunidad.

  OpenCV:
    Utilizada para el procesamiento de imágenes y visión artificial, facilitando tareas como la detección de obstáculos, seguimiento de objetos y procesamiento en tiempo real.

  Frameworks de Inteligencia Artificial (opcional):
    Dependiendo de la versión o de las aplicaciones específicas, puede incluir integración con TensorFlow o PyTorch para implementar algoritmos de reconocimiento, clasificación o detección.

  Dependencias estándar:
    Bibliotecas de comunicación serial, utilidades en C++ y Python, y otros paquetes necesarios para la interacción con el sistema operativo y la ejecución de tareas en tiempo real.

La correcta instalación y configuración de estas librerías es esencial para garantizar el funcionamiento óptimo del robot, y suelen encontrarse referenciadas en archivos como package.xml, CMakeLists.txt o en scripts de instalación incluidos en el repositorio.


4. Programas de Operación y su Propósito
Dentro del ecosistema de software del DOFBOT se incluyen varios programas (o nodos ROS) que, en conjunto, permiten la operación integral del robot. Algunos de ellos son:

    Nodo de Control Principal (dofbot_control_node):
    Es el encargado de orquestar la recepción de comandos, gestionar la ejecución de rutinas de movimiento y coordinar la interacción entre los diferentes módulos. Su función es la de actuar como “cerebro” del robot, integrando información de sensores y enviando órdenes a los actuadores.

    Nodo de Visión (dofbot_vision_node):
    Implementa algoritmos de procesamiento de imagen utilizando OpenCV, permitiendo la detección de obstáculos, reconocimiento de patrones o seguimiento de objetos en el entorno. Este nodo es crucial para aplicaciones de navegación autónoma y para interactuar de forma inteligente con el entorno.

    Nodo de Navegación (dofbot_navigation_node):
    Desarrollado para integrar datos de sensores (como LIDAR, ultrasonido o cámaras) y algoritmos de planificación de ruta, este programa se encarga de calcular trayectorias seguras y eficientes, permitiendo la operación autónoma del robot en entornos complejos.

    Nodo de Teleoperación (dofbot_teleop_node):
    Permite el control manual del robot a través de interfaces remotas (por ejemplo, mediante un joystick o una aplicación móvil). Facilita la operación directa cuando se requiere intervención humana o pruebas en entornos controlados.

    Herramientas de Diagnóstico y Monitoreo (dofbot_diagnostics):
    Conjunto de utilidades que recogen información en tiempo real sobre el estado del robot (como temperatura, consumo de energía, rendimiento de motores, etc.) y facilitan la identificación de fallos o la optimización del rendimiento.

PROCEDIMIENTO DE ENCENDIDO, OPERACIÓN Y APAGO DEL ROBOT

RESTRICCIONES DE SOFTWARE, HARDWARE Y MECÁNICAS DEL ROBOT
1. Restricciones de Software
    Compatibilidad del Sistema Operativo:
El software está diseñado para ejecutarse sobre distribuciones basadas en Ubuntu, optimizadas para la plataforma Jetson Nano. Esto implica que otros sistemas operativos o versiones de Linux no garantizan el correcto funcionamiento del entorno ROS y las aplicaciones asociadas.

    Dependencias y Versiones Específicas:
La integración de ROS, OpenCV y, en algunos casos, frameworks de inteligencia artificial (como TensorFlow o PyTorch) se debe realizar utilizando versiones recomendadas. La actualización o el uso de versiones no validadas puede generar incompatibilidades o fallas en la ejecución.

    Limitaciones de Recursos Computacionales:
El entorno Jetson Nano, pese a ser adecuado para tareas de procesamiento de imagen e inteligencia artificial, tiene restricciones en cuanto a memoria RAM y potencia de cómputo. Esto condiciona la complejidad y el tamaño de los algoritmos que se pueden ejecutar en tiempo real sin afectar el rendimiento global.

    Integración de Librerías Propietarias:
 Se han desarrollado controladores y módulos de abstracción específicos para el hardware del DOFBOT. Estas librerías propietarias están diseñadas para interactuar con componentes recomendados; su uso fuera del entorno previsto puede limitar la funcionalidad o provocar comportamientos erráticos.


RESUMEN Y CONCLUSIONES DEL REPORTE
