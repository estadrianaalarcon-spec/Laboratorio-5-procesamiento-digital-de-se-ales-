# Laboratorio 5 procesamiento digital de señales HRV
#### Adriana Valentina Alarcon Ramirez 5600850

#### Liseth Yulialan Calvijo Mesa 5600862

## Introducción

La variabilidad de la frecuencia cardíaca (Heart Rate Variability, HRV) es una medida que describe las fluctuaciones temporales emtre latidos consecutivos del corazón, entre intervalos R-R obtenidos a partir de la señal electrocardiográfica (ECG).

El analisis de la HRV permite evaluar el funcionamiento del sistema nervioso autónomo, particularmente el equilibrio entre la actividad simpática y parasimpática, las cuales regulan la respuestas cardiovascular del organismo frente a diferentes estímulos fisiológicos y emocionales. El sistema nervioso simpático se asocia principalmente con respuestas de alerta, estrés y aumento en la frecuenica cardíaca, mientras que el sistema parasimpático favorece estados de relajación y recuperación, disminuyendo la frecuencia cardíaca , debido a esto la HRV se considera una herramienta importante para estudiar la regulación autonómica cardíaca y detectar cambios producidos por actividades físicas, cognitivas o emocionales.

En esta práctica se adquirio una señal ECG en condiciones de reposo y lectura en voz alta, posteriormente se realizo el procesamiento digital de la señal mediante filtradon deteccion de picos R y cálculo de intervalos R-R, con el fin de analizar la variabilidad cardíaca en el dominio del tiempo y mediante digrama de Poincaré se commpararos parámetros obtenidos para identificar cambios en el balance autonómico generados por la actividad de verbalización.

### Parte A - Fundamento teórico

#### Sistema nervioso autónomo de la actividad simpática y parasimpática.

El sistema nervioso autonómo (SNA) es el encargado de regulat funciones innvoluntarias del organismo, como la respiración, la presión arterial y la actividad cardíaca, este sistema se divide en dos ramas principales: sistema nervioso simpático y el sistema nervioso parasimpático.

<img width="1152" height="904" alt="image" src="https://github.com/user-attachments/assets/2f6278f7-58fc-4efd-a5c0-d34275b59ecd" />

El sistema nervioso simpático prepara el organismo para situaciones de alerta o estrés, generando una respuesta fisiológica como aumento de la frecuencia cardáca, incremento de la presión arterial y mayor consumo energetico en el organismo, en el corazón la actividad simpática provoca un aumento en la velocidad de despolarización del nodo sonoauricular, produciendo latidos más rápidos y una disminución relativa de la variabilidad entre latidos.

El sistema nerviosos parasimpático se relaciona con el estado de reposo y recuperación, sobre el corazonsu acción principal ocurre mediante el nervio vago encargado de disminuir la frecuencia cardíaca y favorece una mayor vatiabilidad entre los latidos consecutivos, esto se asocia a un mejor balance autonómico y una mayor capacidad de adaptacion fisiológica.
Un equilibrio adecuado entre ambas ramas del SNA permite matener la homeostasis cardiovascular frente a diferentes estimulos internos y externos.

#### Efecto de la actividad simpática y parasimpática en la frecuencia cardíaca.

La frecuencia cardiaca depende directamente de la interacción entre la actividad simpática y parasimpática sobre el nodo sinuauricular del corazón, cuando la actividad simpática predomina se liberan catecolaminas como la adrenalina y la noradrenalina, aumentano la frecuencia cardíaca y disminuyendo el tiempo entre latidos, esto ocurre durante actividades físicas, situaciones de estrés o tareas que impliquen mayor atención 
