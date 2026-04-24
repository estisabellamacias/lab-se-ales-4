# **Señales electromiográficas EMG**

## *Contexto teorico* 
La fatiga muscular reduce la capacidad del músculo para controlar cargas y mantener contracciones eficaces, como consecuencia de la acumulación de lactato y la disminución del adenosín trifosfato (ATP). Un músculo fatigado tiene más riesgo de lesiones, por lo que es importante identificar la fatiga muscular de manera objetiva y oportuna. Una de las formas más comunes de evaluar la fatiga muscular es medir el lactato en la sangre ya que, durante ejercicios muy intensos, su nivel aumenta debido al proceso anaeróbico que tiene lugar para la generación de energía. No obstante, este método es invasivo y poco práctico en escenarios no controlados. Métodos alternativos incluyen la electromiografía de superficie (sEMG), técnica que registra la actividad eléctrica de los músculos desde la piel, capturando la suma de los potenciales de acción generados por las fibras musculares durante la contracción de las unidades motoras. Existen métricas, tanto en el dominio del tiempo como en el de la frecuencia, que pueden aportar información referente a la fatiga muscular. 

## *Objetivos* 
***Objetivo General:*** dentificar cambios en las características espectrales de una señal electromiográfica (EMG) cuando se alcanza la fatiga muscular.

***Objetivos especificos:***
1. Aplicar el filtrado de señales continuas para el procesamiento una señal electromiográfica (EMG).
   
2. Detectar la aparición de fatiga muscular mediante el análisis espectral de contracciones musculares individuales.

3. Comparar el comportamiento de una señal emulada y una señal real en términos de frecuencia media y mediana.
   
4. Emplear herramientas computacionales para el procesamiento, segmentación y análisis de señales biomédicas.

## *Desarrollo de la practica* 
El laboratorio se dividió en tres partes principales:

### *PARTE A – Captura de la señal emulada*

/a. Configurar el generador de señales biológicas en modo EMG, simulando
aproximadamente cinco contracciones musculares voluntarias.
b. Adquirir y almacenar la señal generada para su posterior análisis.
c. Segmentar la señal obtenida en las cinco contracciones simuladas.
d. Calcular para cada contracción:
 Frecuencia media
 Frecuencia mediana
e. Presentar los resultados de cada contracción en una tabla y representar
gráficamente la evolución de las frecuencias.
f. Analizar cómo varían estas frecuencias a lo largo de las contracciones
simuladas./

<p align="center">
<img src="PARTE A/.jpg" width="600">
</p>
<p align="center">
<em>Imagen . .</em>
</p>

### *PARTE B – Captura de la señal de paciente*

a. Colocar los electrodos sobre el grupo muscular definido por el grupo (por
ejemplo, antebrazo o bíceps).
b. Registrar la señal EMG de un paciente o voluntario sano realizando
contracciones repetidas hasta la fatiga (o la falla).
c. Aplicar un filtro pasa banda (20–450 Hz) para eliminar ruido y artefactos.
d. Dividir la señal en el número de contracciones realizadas.
e. Calcular para cada contracción:
 Frecuencia media
 Frecuencia mediana
f. Graficar los resultados obtenidos y analizar la tendencia de la frecuencia
media y mediana a medida que progresa la fatiga muscular.
g. Discutir la relación entre los cambios de frecuencia y la fisiología de la fatiga
muscular.
NOTA: Para observar las frecuencias se debe realizar y graficar la transformada de
Fourier

<p align="center">
<img src="PARTE B/.jpg" width="600">
</p>
<p align="center">
<em>Imagen . .</em>
</p>

### *PARTE C – Análisis espectral mediante FFT*

a. Aplicar la Transformada Rápida de Fourier (FFT) a cada contracción de la
señal EMG real.
b. Graficar el espectro de amplitud (frecuencia vs. magnitud) para observar
cómo cambia el contenido de frecuencia.
c. Comparar los espectros de las primeras contracciones con los de las últimas.
d. Identificar la reducción del contenido de alta frecuencia asociada con la fatiga
muscular.
e. Calcular y discutir el desplazamiento del pico espectral y su relación con el
esfuerzo sostenido.
f. Redactar conclusiones sobre el uso del análisis espectral como herramienta
diagnóstica en electromiografía. 


<p align="center">
<img src="PARTE C/.jpg" width="600">
</p>
<p align="center">
<em>Imagen . .</em>
</p>

## *Diagrama de flujo*

<p align="center">
<img src="Diagrama de flujo/toma señal del generador.png" width="600">
</p>
<p align="center">
<em>Imagen . Diagrama de flujo del codigo para la toma de la señal del generador.</em>
</p>


<p align="center">
<img src="Diagrama de flujo/Adquicision del EMG.png" width="600">
</p>
<p align="center">
<em>Imagen . Diagrama de flujo del codigo para la adquisición del EMG.</em>
</p>

## *Codigos*

### Codigo para la toma de la señal del generador:

***Módulo DAQ:***

* **`nidaqmx.Task()`**
  Crea la tarea de adquisición y permite la comunicación con la DAQ.

* **`add_ai_voltage_chan()`**
  Configura el canal de entrada analógica desde donde se captura la señal.

* **`cfg_samp_clk_timing()`**
  Define la frecuencia de muestreo (`fs`) y el modo continuo de adquisición.

* **`task.read()`**
  Lee bloques de datos desde la DAQ en tiempo real.

* **`adquirir_datos()`**
  Función principal de adquisición: Inicializa la DAQ, lee datos continuamente, controla el flujo de adquisición.

***Módulo de procesamiento de datos:***

* **`np.roll()`**
  Implementa un buffer circular desplazando los datos para mantener solo las muestras más recientes.

* **`np.zeros()`**
  Inicializa el buffer de almacenamiento de datos.

* **`np.savetxt()`**
  Guarda los datos adquiridos en un archivo `.txt`.

* **`time.sleep()`**
  Introduce pausas cortas para evitar sobrecarga del sistema.

***Módulo de interfaz gráfica:***

* **`tk.Tk()`**
  Crea la ventana principal de la aplicación.

* **`tk.Button()`**
  Botón para iniciar/detener la grabación de datos.

* **`tk.Label()`**
  Muestra el estado del sistema (grabando o visualizando).

* **`toggle_guardado()`**
  Controla el estado de grabación y actualiza la interfaz.

***Módulo de visualización:***

* **`plt.subplots()`**
  Crea la figura y los ejes para graficar la señal.

* **`ax.plot()`**
  Inicializa la gráfica de la señal.

* **`set_ydata()`**
  Actualiza los valores de la señal en la gráfica en tiempo real.

* **`draw_idle()`**
  Refresca la gráfica de forma eficiente.

* **`root.after()`**
  Controla la actualización periódica de la gráfica.

* **`actualizar_plot()`**
  Función encargada de refrescar la visualización continuamente.

***Módulo de ejecución concurrente:***

* **`threading.Thread()`**
  Ejecuta la adquisición de datos en paralelo a la interfaz gráfica, evitando bloqueos.

### Código para la adquisición del EMG

***Módulo DAQ:***

* **`nidaqmx.Task()`**
  Crea la tarea de adquisición y gestiona la comunicación con la DAQ.

* **`add_ai_voltage_chan()`**
  Configura el canal de entrada analógica (`canal_daq`) desde donde se captura la señal.

* **`cfg_samp_clk_timing()`**
  Define la frecuencia de muestreo (`fs`) y el modo de adquisición finito (número fijo de muestras).

* **`task.read()`**
  Realiza la lectura completa de las muestras definidas (`muestras`) desde la DAQ.

***Módulo de procesamiento de datos:***

* **`filtro_pasabanda()`**
  Función que aplica un filtro pasabanda a la señal para eliminar ruido fuera del rango de interés.

* **`butter()`**
  Diseña el filtro digital pasabanda según las frecuencias de corte.

* **`filtfilt()`**
  Aplica el filtro a la señal sin desfase (filtrado hacia adelante y hacia atrás).

* **`np.array()`**
  Convierte los datos adquiridos a un arreglo de NumPy para facilitar su procesamiento.

***Módulo de almacenamiento***

* **`np.savetxt()`**
  Guarda la señal procesada en un archivo `.txt` en formato de una sola columna.

***Módulo de visualización:***

* **`np.linspace()`**
  Genera el vector de tiempo para graficar la señal.

* **`plt.figure()`**
  Crea la figura donde se mostrará la señal.

* **`plt.plot()`**
  Grafica la señal en el dominio del tiempo.

* **`plt.title()`**, **`plt.xlabel()`**, **`plt.ylabel()`**
  Configuran el título y las etiquetas de la gráfica.

* **`plt.grid()`**
  Activa la cuadrícula para mejorar la visualización.

* **`plt.show()`**
  Muestra la gráfica final.

***Módulo de manejo de errores:***

* **`try / except`**
  Permite capturar errores durante la conexión o adquisición con la DAQ, evitando que el programa falle abruptamente.

***Salida:***

* **`print()`**
  Muestra mensajes informativos: Inicio de la captura, finalización exitosa, guardado de datos, errores en la adquisición.


## *Analisis de resultados*

***1. Identifique el mecanismo fisiológico mediante el cual parámetros como la frecuencia media y frecuencia mediana experimentan cambios a medida que el músculo tiende a fatigarse.***

Durante la fatiga muscular, la señal electromiográfica (EMG) presenta un desplazamiento del espectro hacia bajas frecuencias, lo que se refleja en la disminución de la frecuencia media y la frecuencia mediana.

Este comportamiento se explica principalmente por:

- Disminución de la velocidad de conducción: causada por la acumulación de metabolitos (como lactato), lo que ralentiza los potenciales de acción musculares.
- Aumento en la duración de los potenciales de acción, generando mayor contenido de bajas frecuencias.
- Cambios en el reclutamiento de unidades motoras, con mayor participación de fibras de contracción lenta.

Como resultado, el espectro EMG se comprime y pierde componentes de alta frecuencia, fenómeno conocido como corrimiento espectral.

***2. Determine el alcance y las posibles limitaciones de emplear parámetros del dominio frecuencial en contextos como fisiología del deporte.***

En el contexto deportivo, los parámetros frecuenciales de la señal EMG (como la MNF y MDF) se utilizan para evaluar cómo responde el músculo durante el ejercicio y detectar la aparición de fatiga.

### *Alcances* 

* **Monitoreo de fatiga en tiempo real:**
Durante actividades prolongadas (ciclismo, running, entrenamiento de fuerza), la disminución progresiva de la frecuencia media o mediana indica que el músculo está entrando en fatiga. Esto permite identificar el punto en el que el rendimiento comienza a deteriorarse.

* **Optimización del entrenamiento:**
Los entrenadores pueden usar estos parámetros para: ajustar la intensidad y duración del ejercicio, evitar el sobreentrenamiento o diseñar rutinas más eficientes
Por ejemplo, si la frecuencia disminuye muy rápido, puede indicar que la carga es demasiado alta para el atleta.

* **Prevención de lesiones:** La fatiga muscular está asociada con una pérdida de control neuromuscular, lo que aumenta el riesgo de lesiones.
El análisis frecuencial permite detectar fatiga antes de que aparezcan fallos mecánicos en el movimiento.

### *Posibles limitaciones*

* **Influencia del movimiento (condiciones dinámicas):** En el deporte real, los movimientos son dinámicos (correr, saltar, pedalear), lo que introduce: Cambios en la posición de los electrodos/Variaciones en la longitud muscular/Ruido por movimiento (artefactos)
Esto puede distorsionar el espectro de la señal EMG y afectar la estimación de la frecuencia.

* **Variabilidad entre individuos:** No todos los músculos responden igual. Factores como: Tipo de fibras (rápidas vs lentas), nivel de entrenamiento , edad o condición física. Pueden hacer que la misma disminución de frecuencia tenga significados distintos entre atletas.

* **No son indicadores exclusivos de fatiga:** Una disminución en la frecuencia no siempre implica fatiga. También puede deberse a:
Cambios en la fuerza aplicada, reclutamiento de diferentes unidades motoras, modificaciones en la técnica del movimiento
Esto puede llevar a interpretaciones erróneas si se analiza de forma aislada.

## *Conclusiones*

/Tras la realización de esta práctica, el estudiante debe concluir incluyendo una
breve reflexión sobre la factibilidad de emplear técnicas espectrales en la detección
de la fatiga muscular en escenarios no controlados como, por ejemplo, durante
entrenamiento de atletas./

## *Preguntas para la discusión*

* **¿Cambian los valores de frecuencia media y mediana a medida que el músculo se acerca a la fatiga?**

Sí. A medida que el músculo se fatiga, tanto la frecuencia media como la frecuencia mediana tienden a disminuir progresivamente.

Esto ocurre porque el contenido de la señal EMG se desplaza hacia frecuencias más bajas, fenómeno conocido como corrimiento espectral.

* **¿A qué podría atribuirse este cambio?**
  
La disminución de la frecuencia media y la frecuencia mediana está asociada a cambios en el comportamiento eléctrico del músculo cuando aparece la fatiga.

Durante una contracción prolongada, el músculo comienza a acumular metabolitos como el lactato y se producen cambios en el pH. Esto afecta la membrana de las fibras musculares, provocando que los impulsos eléctricos se propaguen más lentamente. Como consecuencia, las señales electromiográficas se vuelven más “largas” en el tiempo, lo que se traduce en un mayor contenido de bajas frecuencias.

Además, el sistema neuromuscular modifica el reclutamiento de unidades motoras para mantener la contracción, incorporando fibras más lentas y resistentes a la fatiga, lo que también influye en la distribución espectral de la señal.

* **¿Cómo justifica el uso de herramientas como la transformada de Fourier en escenarios como, por ejemplo, terapias de rehabilitación?**

La transformada de Fourier permite analizar la señal electromiográfica (EMG) en el dominio de la frecuencia, facilitando la identificación de cambios en la actividad muscular que no son evidentes en el tiempo.

En rehabilitación, esto resulta útil para detectar la fatiga muscular de forma objetiva, mediante la disminución de parámetros como la frecuencia media y mediana. Además, permite hacer seguimiento al progreso del paciente, evaluando cómo cambia la respuesta muscular a lo largo del tratamiento.

También ayuda a ajustar la intensidad de los ejercicios terapéuticos, evitando sobrecargas y favoreciendo una recuperación más controlada.

En conjunto, esta herramienta permite obtener información cuantitativa que apoya la evaluación y el control de la función muscular durante la rehabilitación.
