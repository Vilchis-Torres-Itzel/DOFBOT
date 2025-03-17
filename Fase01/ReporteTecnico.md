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
  DESCRIPCIONES: 
  


DESCRIPCIÓN DE SOFTWARE, ESTRUCTURA DE PAQUETES, DESCRIPCIÓN DE LIBRERÍAS PROPIERARIAS Y DE TERCEROS NECESARIAS, LISTADO DE PROGRAMAS DE OPERACIÓN DEL ROBOT Y DESCRIPCIÓN DE SU PROPÓSITO. 

PROCEDIMIENTO DE ENCENDIDO, OPERACIÓN Y APAGO DEL ROBOT

RESTRICCIONES DE SOFTWARE, HARDWARE Y MECÁNICAS DEL ROBOT

RESUMEN Y CONCLUSIONES DEL REPORTE
