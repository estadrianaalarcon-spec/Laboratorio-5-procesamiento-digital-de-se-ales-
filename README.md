# Laboratorio 5 procesamiento digital de señales HRV

## Docente: Carolina Corredor 
## Integrantes:
#### Adriana Valentina Alarcon Ramirez 5600850
#### Liseth Yulialan Calvijo Mesa 5600862
#### Fecha: Mayo 2026
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

<img width="616" height="1024" alt="image" src="https://github.com/user-attachments/assets/a164b1e3-2c74-4074-ad77-6aa1367df4f4" />


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


En las gráficas se observa una comparación entre una señal de ECG original y la misma señal después de aplicar un proceso de filtrado. En la gráfica superior, correspondiente al ECG original, se pueden identificar los complejos QRS mediante los picos altos y pronunciados que representan la actividad eléctrica ventricular del corazón. Aunque los latidos se observan de manera relativamente periódica, la señal presenta ruido, pequeñas oscilaciones y variaciones en la línea base, especialmente alrededor de los 3.2 a 3.6 segundos, lo que puede deberse a movimientos, respiración, interferencia de los electrodos o artefactos durante la adquisición de la señal. Estas alteraciones dificultan un análisis preciso de la actividad cardíaca.

En la gráfica inferior se muestra el ECG filtrado, donde se evidencia una mejora importante en la calidad de la señal. Después del filtrado, la línea base queda centrada alrededor de cero y se reducen considerablemente las interferencias y el ruido presentes en la señal original. Además, los complejos QRS se observan más definidos y fáciles de identificar, lo que facilita la detección de los picos R, el cálculo de intervalos RR y el análisis de la frecuencia cardíaca. En general, el filtrado permitió conservar la información importante del ECG mientras eliminó componentes no deseadas, haciendo que la señal sea más adecuada para el procesamiento y análisis biomédico.



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


La figura muestra la detección de los picos R en un segmento de la señal ECG filtrada y el cálculo de los intervalos RR correspondientes. En la gráfica superior, la señal azul representa el ECG procesado, mientras que los puntos rojos indican los picos R identificados automáticamente por el algoritmo. Estos picos corresponden a la máxima amplitud del complejo QRS y permiten determinar cada latido cardíaco. Se observa que la mayoría de los picos fueron detectados correctamente, aunque existen pequeñas variaciones en la amplitud debido al ruido residual de la señal y a posibles artefactos producidos por movimiento o interferencias durante la adquisición.

Los valores mostrados debajo de la gráfica corresponden a los intervalos RR, es decir, el tiempo transcurrido entre un latido y el siguiente. Estos intervalos presentan ligeras variaciones, lo cual es normal en una señal fisiológica real, ya que el ritmo cardíaco no es completamente constante. En la gráfica inferior se representa la variación de los intervalos RR a lo largo del tiempo, observándose algunos aumentos y disminuciones entre latidos consecutivos. Sin embargo, la mayoría de los valores se mantienen dentro de un rango relativamente estable, indicando un comportamiento cardíaco regular.

Finalmente, a partir de los intervalos RR se calculó una frecuencia cardíaca promedio de aproximadamente 72 BPM, valor que se encuentra dentro del rango normal para una persona en estado de reposo. En general, las gráficas permiten evidenciar que el procesamiento aplicado al ECG fue adecuado para detectar los latidos y analizar la dinámica cardíaca del segmento estudiado.






INTERVALO RR SEGMENTO 2

<img width="1065" height="323" alt="image" src="https://github.com/user-attachments/assets/2320b21b-5053-43cb-870e-845d05057bf1" />

<img width="481" height="68" alt="image" src="https://github.com/user-attachments/assets/237c6f77-bcc1-485a-a883-7c326add4b1e" />

<img width="843" height="330" alt="image" src="https://github.com/user-attachments/assets/dfa7ae54-11b5-4c89-9659-fdc7638c2163" />

<img width="272" height="38" alt="image" src="https://github.com/user-attachments/assets/9bda7a3c-56cd-4deb-bffe-d65c3cc16805" />


La figura correspondiente al segmento 2 muestra el comportamiento de la señal ECG cuando la persona se encontraba hablando durante la adquisición de los datos. En la gráfica superior se observa la señal ECG filtrada junto con la detección de los picos R, identificados mediante los puntos rojos. En comparación con el segmento anterior, donde la persona se encontraba en reposo y únicamente respirando, en este caso la señal presenta mayores variaciones y oscilaciones en la amplitud. Esto se debe a que al hablar se generan movimientos musculares y cambios en la respiración que introducen ruido e interferencias en la señal electrocardiográfica.

Además, se evidencia un aumento notable de amplitud alrededor de los 15 segundos y varias perturbaciones posteriores, las cuales pueden asociarse a artefactos producidos por el movimiento durante el habla. A pesar de estas alteraciones, el algoritmo logró detectar correctamente la mayoría de los picos R, permitiendo calcular los intervalos RR entre cada latido cardíaco.

Los intervalos RR obtenidos presentan una mayor variabilidad respecto al segmento en reposo, lo cual se observa tanto en los valores numéricos como en la gráfica inferior. En esta última, la curva muestra cambios más bruscos y fluctuaciones más marcadas entre un latido y otro. Estas variaciones pueden estar relacionadas con la actividad muscular, el patrón respiratorio y las interferencias generadas mientras la persona hablaba durante la adquisición de la señal.





## d. Análisis de la HRV en el dominio del tiempo 
Comparar los valores de los parámetros básicos de la HRV en el dominio del tiempo, como la media de los intervalos R-R y su desviación estándar, entre çambos segmentos de señal ECG. 



```python

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# ======================================
# HRV EN DOMINIO DEL TIEMPO
# ======================================

def hrv_time_domain(rr):

    mean_rr = np.mean(rr)

    sdnn = np.std(rr, ddof=1)

    rmssd = np.sqrt(np.mean(np.diff(rr)**2))

    return mean_rr, sdnn, rmssd

mean1, sdnn1, rmssd1 = hrv_time_domain(rr1)

mean2, sdnn2, rmssd2 = hrv_time_domain(rr2)

# TABLA

tabla = pd.DataFrame({

    "Métrica": [
        "Media RR (s)",
        "SDNN (s)",
        "RMSSD (s)"
    ],

    "Segmento 1": [
        mean1,
        sdnn1,
        rmssd1
    ],

    "Segmento 2": [
        mean2,
        sdnn2,
        rmssd2
    ]

})

print(tabla)

# GRAFICA

metricas = ["Media RR", "SDNN", "RMSSD"]

seg1 = [mean1, sdnn1, rmssd1]
seg2 = [mean2, sdnn2, rmssd2]

x = np.arange(len(metricas))

ancho = 0.35

plt.figure(figsize=(8,5))

plt.bar(
    x - ancho/2,
    seg1,
    width=ancho,
    label='Segmento 1'
)

plt.bar(
    x + ancho/2,
    seg2,
    width=ancho,
    label='Segmento 2'
)

plt.xticks(x, metricas)

plt.ylabel('Valor [s]')

plt.title('HRV en Dominio del Tiempo')

plt.legend()

plt.grid(True, linestyle='--', linewidth=0.5)

plt.show()

```

<img width="594" height="435" alt="image" src="https://github.com/user-attachments/assets/4fda7db1-4305-4b94-9430-869b2a61cf12" />


Esta gráfica muestra un análisis de la variabilidad de la frecuencia cardíaca (HRV) en el dominio del tiempo para dos segmentos diferentes del ECG. El Segmento 1 corresponde al estado de reposo, mientras que el Segmento 2 corresponde al momento en que la persona estaba hablando. Las métricas utilizadas fueron la Media RR, SDNN y RMSSD.

La Media RR representa el tiempo promedio entre latidos cardíacos. En el Segmento 2 el valor es ligeramente mayor, lo que indica pequeñas variaciones en el ritmo cardíaco mientras la persona hablaba. La métrica SDNN mide la variabilidad general de los intervalos RR y en el Segmento 2 presenta un valor más alto, evidenciando una mayor variabilidad cardíaca debido a los cambios respiratorios y musculares generados por el habla.

Por otro lado, el RMSSD evalúa las variaciones rápidas entre latidos consecutivos y está relacionado con la actividad del sistema nervioso parasimpático. En la gráfica se observa que el Segmento 2 tiene un RMSSD considerablemente mayor que el Segmento 1, lo que indica que hablar produjo cambios más notorios en la dinámica cardíaca y aumentó la variabilidad de corto plazo.



## e. Construcción del diagrama de Poincaré 
Obtener el diagrama de Poincaré para cada segmento de señal ECG y comparar la dispersión de la nube de puntos que se obtuvo para cada caso.   
Calcular los valores de los índices tanto de actividad vagal (CVI) como de actividad simpática (CSI) que se obtienen a partir del diagrama de Poincaré. 



```python

import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
def poincare_indices(rr):

    rr = np.asarray(rr)

    rr_n = rr[:-1]
    rr_n1 = rr[1:]

    diff_rr = rr_n1 - rr_n

    sd1 = np.sqrt(0.5) * np.std(diff_rr, ddof=1)

    sd2 = np.sqrt(
        2 * np.std(rr, ddof=1)**2
        - 0.5 * np.std(diff_rr, ddof=1)**2
    )

    cvi = np.log10(sd1 * sd2)

    csi = sd2 / sd1

    return rr_n, rr_n1, sd1, sd2, cvi, csi

rr1_n, rr1_n1, sd1_1, sd2_1, cvi_1, csi_1 = poincare_indices(rr1)


rr2_n, rr2_n1, sd1_2, sd2_2, cvi_2, csi_2 = poincare_indices(rr2)


print("Segmento 1")

print("SD1 =", sd1_1, "s")
print("SD2 =", sd2_1, "s")
print("CVI =", cvi_1)
print("CSI =", csi_1)

print("\nSegmento 2")

print("SD1 =", sd1_2, "s")
print("SD2 =", sd2_2, "s")
print("CVI =", cvi_2)
print("CSI =", csi_2)

# ============================================
# POINCARE SEGMENTO 1
# ============================================

plt.figure(figsize=(6,6))

plt.scatter(
    rr1_n,
    rr1_n1,
    alpha=0.6
)

plt.plot(
    [min(rr1), max(rr1)],
    [min(rr1), max(rr1)],
    'r--',
    label='y=x'
)

plt.xlabel("RRₙ (s)")
plt.ylabel("RRₙ₊₁ (s)")

plt.title("Diagrama de Poincaré - Segmento 1")

plt.grid(True, linestyle='--', linewidth=0.5)

plt.axis('equal')

plt.legend()

plt.tight_layout()

plt.show()

# ============================================
# POINCARE SEGMENTO 2
# ============================================

plt.figure(figsize=(6,6))

plt.scatter(
    rr2_n,
    rr2_n1,
    alpha=0.6
)

plt.plot(
    [min(rr2), max(rr2)],
    [min(rr2), max(rr2)],
    'r--',
    label='y=x'
)

plt.xlabel("RRₙ (s)")
plt.ylabel("RRₙ₊₁ (s)")

plt.title("Diagrama de Poincaré - Segmento 2")

plt.grid(True, linestyle='--', linewidth=0.5)

plt.axis('equal')

plt.legend()

plt.tight_layout()

plt.show()

tabla_poincare = pd.DataFrame({

    "Métrica": [
        "SD1 (s)",
        "SD2 (s)",
        "CVI",
        "CSI"
    ],

    "Segmento 1": [
        sd1_1,
        sd2_1,
        cvi_1,
        csi_1
    ],

    "Segmento 2": [
        sd1_2,
        sd2_2,
        cvi_2,
        csi_2
    ]

})

print("\nTabla índices Poincaré")

print(tabla_poincare)

```




<img width="515" height="659" alt="image" src="https://github.com/user-attachments/assets/869f784a-c204-4b68-a7b8-f36bd080bcc0" />
<img width="519" height="496" alt="image" src="https://github.com/user-attachments/assets/ccc54ce2-d7a9-41f1-a6c4-7b54ad356576" />


Estas gráficas corresponden al análisis de variabilidad cardíaca mediante el diagrama de Poincaré, una herramienta utilizada para evaluar cómo cambian los intervalos RR entre latidos consecutivos. En el gráfico, cada punto representa la relación entre un intervalo RR actual (RRn) y el siguiente intervalo RR (RRn+1). La línea roja punteada corresponde a la recta y=x, que sirve como referencia para observar qué tan similares son los intervalos consecutivos.

En el Segmento 1, correspondiente al estado de reposo, la mayoría de los puntos se concentran cerca de la línea diagonal, lo que indica que los intervalos RR consecutivos son relativamente similares y que el ritmo cardíaco es más estable. Sin embargo, también se observan algunos puntos más alejados de la diagonal, los cuales representan variaciones mayores entre ciertos latidos.

Los parámetros SD1 y SD2 permiten cuantificar esta dispersión. El valor SD1 representa la variabilidad de corto plazo entre latidos consecutivos, mientras que SD2 representa la variabilidad de largo plazo de la señal. En este caso, SD2 es mayor que SD1, indicando que existen variaciones más importantes en la dinámica general del ritmo cardíaco que en los cambios instantáneos entre latidos consecutivos.

El índice CSI se relaciona con la actividad simpática del sistema nervioso autónomo y refleja qué tan alargada es la distribución de los puntos, mientras que el índice CVI está asociado a la variabilidad cardíaca global. Al comparar ambos segmentos, se observa que en el Segmento 2, donde la persona estaba hablando, el valor de SD1 aumenta, indicando una mayor variabilidad de corto plazo causada por la actividad muscular y respiratoria asociada al habla. Además, el CSI disminuye respecto al Segmento 1, lo que evidencia cambios en la dinámica cardíaca durante la conversación


## Conclusiones

-El procesamiento y filtrado de la señal ECG permitió reducir el ruido y las interferencias presentes durante la adquisición, facilitando la detección de los picos R y el cálculo de los intervalos RR para el análisis de la actividad cardíaca.
-Se observó que el estado de reposo presentó una señal más estable y con menor variabilidad cardíaca, mientras que durante el habla aumentaron las fluctuaciones en los intervalos RR debido a los movimientos musculares y cambios respiratorios asociados a esta actividad.
-Las métricas de HRV y los diagramas de Poincaré evidenciaron una mayor variabilidad cardíaca en el segmento donde la persona estaba hablando, demostrando que las actividades fisiológicas y el movimiento influyen directamente en el comportamiento de la señal electrocardiográfica.





La frecuencia cardiaca depende directamente de la interacción entre la actividad simpática y parasimpática sobre el nodo sinuauricular del corazón, cuando la actividad simpática predomina se liberan catecolaminas como la adrenalina y la noradrenalina, aumentano la frecuencia cardíaca y disminuyendo el tiempo entre latidos, esto ocurre durante actividades físicas, situaciones de estrés o tareas que impliquen mayor atención 
