# Laboratorio 5 procesamiento digital de señales HRV
## Docente: Carolina Corredor 
#### Adriana Valentina Alarcon Ramirez 5600850

#### Liseth Yulialan Calvijo Mesa 5600862

## Introducción

La variabilidad de la frecuencia cardíaca (Heart Rate Variability, HRV) es una medida que describe las fluctuaciones temporales emtre latidos consecutivos del corazón, entre intervalos R-R obtenidos a partir de la señal electrocardiográfica (ECG).

El analisis de la HRV permite evaluar el funcionamiento del sistema nervioso autónomo, particularmente el equilibrio entre la actividad simpática y parasimpática, las cuales regulan la respuestas cardiovascular del organismo frente a diferentes estímulos fisiológicos y emocionales. El sistema nervioso simpático se asocia principalmente con respuestas de alerta, estrés y aumento en la frecuenica cardíaca, mientras que el sistema parasimpático favorece estados de relajación y recuperación, disminuyendo la frecuencia cardíaca , debido a esto la HRV se considera una herramienta importante para estudiar la regulación autonómica cardíaca y detectar cambios producidos por actividades físicas, cognitivas o emocionales.

En esta práctica se adquirio una señal ECG en condiciones de reposo y lectura en voz alta, posteriormente se realizo el procesamiento digital de la señal mediante filtradon deteccion de picos R y cálculo de intervalos R-R, con el fin de analizar la variabilidad cardíaca en el dominio del tiempo y mediante digrama de Poincaré se commpararos parámetros obtenidos para identificar cambios en el balance autonómico generados por la actividad de verbalización.

### Parte A - Fundamento teórico

### Sistema nervioso autónomo de la actividad simpática y parasimpática.

El sistema nervioso autonómo (SNA) es el encargado de regulat funciones innvoluntarias del organismo, como la respiración, la presión arterial y la actividad cardíaca, este sistema se divide en dos ramas principales: sistema nervioso simpático y el sistema nervioso parasimpático.

<img width="1152" height="904" alt="image" src="https://github.com/user-attachments/assets/2f6278f7-58fc-4efd-a5c0-d34275b59ecd" />

El sistema nervioso simpático prepara el organismo para situaciones de alerta o estrés, generando una respuesta fisiológica como aumento de la frecuencia cardáca, incremento de la presión arterial y mayor consumo energetico en el organismo, en el corazón la actividad simpática provoca un aumento en la velocidad de despolarización del nodo sonoauricular, produciendo latidos más rápidos y una disminución relativa de la variabilidad entre latidos.

El sistema nerviosos parasimpático se relaciona con el estado de reposo y recuperación, sobre el corazonsu acción principal ocurre mediante el nervio vago encargado de disminuir la frecuencia cardíaca y favorece una mayor vatiabilidad entre los latidos consecutivos, esto se asocia a un mejor balance autonómico y una mayor capacidad de adaptacion fisiológica.
Un equilibrio adecuado entre ambas ramas del SNA permite matener la homeostasis cardiovascular frente a diferentes estimulos internos y externos.

#### Efecto de la actividad simpática y parasimpática en la frecuencia cardíaca.

La frecuencia cardíaca depende directamente de la interacción entre la actividad simpática y parasimpática sobre el nodo sinoauricular del corazón.

Cuando predomina la actividad simpática, se liberan catecolaminas como la adrenalina y la noradrenalina, aumentando la frecuencia cardíaca y disminuyendo el tiempo entre latidos, esto ocurre durante actividades físicas, situaciones de estrés o tareas de mayor atención.

Cuando predomina la actividad parasimpática principalmente mediante la acetilcolina, la frecuencia cardíaca disminuye y los intervalos entre latidos aumentan, este comportamiento es común durante estados como el reposo, los cambios en este balance autonómico pueden analizarse mendiante la variabilidad de la frecuencia cardíaca, ya que una menor variabilidad suele asociarse con predominio simpático, mientras que una mayor variabilidad refleja mayor influencia parasimpática.

### Variabilidad de la frecuencia cardíaca (HRV)

La variabilidad de la frecuencia cardíaca (HRV) corresponde a las varaciones temporales existentes entre intervalos consecutivos R-R obtenidos a partir de una señal electrocardiografica ECG, aunque el corazón mantiene un ritmo constante, el tiempo entre latidos nunca es exactamente igual debido a la regulación continua ejercida por el sistema nervioso autónomo.

para obtener la HRV, primero se identifican los picos R del electrocardiograma y posteriormenete se calculan los intervalos de tiempo entre latidos consecutivos, estos intervalos permiten construir una nueva serie tenmporal conocida como serie R-R, entre los parámetros utilizados en el dominio del tiempo se encunetran.


- Medida de los intervalos R-R, esta representa el promedio entre latidos consecutivos 

- SDNN (Standard Deviation of Normal to Notmal intervals), corresponde a la desviación estandár de los intervalos R-R y refleja la variabilidad de la señal.

Una HRV elevada generalmente indica buena adaptación autonómica y predominio parasimpático, mientras que una HRV reducuda puede asociarse con fatiga o prediminio simpático.

### Diagrama de Poincaré

el diagrama de Poincaré es una herramienta gráfica utilizada para analizar la dinánica de la variabilidad cardíaca, este método consisten en representar cada intervalo R-R en función del intervalo anterior: RRn+1 vs RRn

<img width="326" height="251" alt="image" src="https://github.com/user-attachments/assets/3f164e03-0f71-46cc-9e83-2622c213c84f" />
<img width="276" height="282" alt="image" src="https://github.com/user-attachments/assets/6a4a0c65-4ba0-4044-99f3-5267bcec785a" />


La distribución de los puntos obtenidos permite observa el comportamiento autonómico del corazón, cuendo existen una alta variabilidad la nube de puntos presenta mayor dispersión, mientras que una menor dispersión indica menor variabilidad y posible predominio simpático.

Con el diagrama de Poincaré pueden calcularse indices cuantitativos como:

- CSI cardiac Sympathetic Index: Relacionado con la actividad simpática
- CVI Cardiac Vagal Index: asociado con la actividad parasimpática

Estos índices permiten comparar el comportemiento cardíaco en diferentes condiciones fisiológicas.

### Plan de acción de la práctica


# PARTE B 
#### c. Pre-procesamiento de la señal 
Aplicar los filtros digitales necesarios para eliminar el ruido de la señal, 
demostrando su diseño. 
-Diseñar un filtro IIR de acuerdo con los parámetros de la señal, 
-Obtener la ecuación en diferencias del filtro, 
-Implementar el filtro a la señal obtenida asumiendo parámetros iniciales en 0. 



```python

lowcut = 1
highcut = 35
orden = 4
nyquist = fs / 2
low = lowcut / nyquist
high = highcut / nyquist
b, a = butter(orden, [low, high], btype='band')
ecg_filtrado = filtfilt(b, a, ecg)
print("Coeficientes b:")
print(b)
print("\nCoeficientes a:")
print(a)
plt.style.use('default')
inicio = 0
fin = 4
muestra_inicio = int(inicio * fs)
muestra_fin = int(fin * fs)


```

<img width="1070" height="646" alt="image" src="https://github.com/user-attachments/assets/073a87fd-dc23-4c7e-9328-805ed3f257de" />


<img width="1072" height="323" alt="image" src="https://github.com/user-attachments/assets/c042771d-8adb-4dd6-b7a6-294c8de6f971" />



Dividir la señal filtrada en dos segmentos de señal con duración de 2 minutos cada uno. 
Identificar los picos R en cada uno de los segmentos, calcular los intervalos 
R-R y obtener una nueva señal con dicha información. 

```python
# DIVIDIR EN DOS SEGMENTOS
total_muestras = len(ecg_filtrado)
mitad = total_muestras // 2
segmento1 = ecg_filtrado[:mitad]
segmento2 = ecg_filtrado[mitad:]
t1 = np.arange(len(segmento1)) / fs
t2 = np.arange(len(segmento2)) / fs
# PICOS R
peaks1, _ = find_peaks(
    segmento1,
    distance=0.6*fs,
    prominence=0.08
)
peaks2, _ = find_peaks(
    segmento2,
    distance=0.6*fs,
    prominence=0.08
)
# SEGMENTO 1
plt.figure(figsize=(15,4))
plt.plot(t1, segmento1)
plt.plot(
    peaks1/fs,
    segmento1[peaks1],
    'ro'
)
plt.title('Picos R - Segmento 1')
plt.xlabel('Tiempo [s]')
plt.ylabel('Amplitud')
plt.grid(True, which='both', linestyle='--', linewidth=0.5)
plt.minorticks_on()
plt.show()
# SEGMENTO 2
plt.figure(figsize=(15,4))
plt.plot(t2, segmento2)
plt.plot(
    peaks2/fs,
    segmento2[peaks2],
    'ro'
)
plt.title('Picos R - Segmento 2')
plt.xlabel('Tiempo [s]')
plt.ylabel('Amplitud')
plt.grid(True, which='both', linestyle='--', linewidth=0.5)
plt.minorticks_on()
plt.show()

```
INTERVALO RR SEGMENTO 1
<img width="1057" height="321" alt="image" src="https://github.com/user-attachments/assets/05434389-1dab-44ee-b381-09c46395e6c6" />

<img width="508" height="73" alt="image" src="https://github.com/user-attachments/assets/123dee59-8147-4ce0-87da-604e1595ba64" />

<img width="827" height="321" alt="image" src="https://github.com/user-attachments/assets/a88b988f-098e-4aea-a5f5-8170b763202c" />

<img width="272" height="35" alt="image" src="https://github.com/user-attachments/assets/f2fde1e6-7bb6-48b0-b822-d99bfd0596cf" />


INTERVALO RR SEGMENTO 2

<img width="1065" height="323" alt="image" src="https://github.com/user-attachments/assets/2320b21b-5053-43cb-870e-845d05057bf1" />

<img width="481" height="68" alt="image" src="https://github.com/user-attachments/assets/237c6f77-bcc1-485a-a883-7c326add4b1e" />

<img width="843" height="330" alt="image" src="https://github.com/user-attachments/assets/dfa7ae54-11b5-4c89-9659-fdc7638c2163" />

<img width="272" height="38" alt="image" src="https://github.com/user-attachments/assets/9bda7a3c-56cd-4deb-bffe-d65c3cc16805" />
















La frecuencia cardiaca depende directamente de la interacción entre la actividad simpática y parasimpática sobre el nodo sinuauricular del corazón, cuando la actividad simpática predomina se liberan catecolaminas como la adrenalina y la noradrenalina, aumentano la frecuencia cardíaca y disminuyendo el tiempo entre latidos, esto ocurre durante actividades físicas, situaciones de estrés o tareas que impliquen mayor atención 
