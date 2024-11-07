# Práctica 4 - Procesamiento de Audio

*Autores*: Alejandro Bolaños García y David García Díaz

## Introducción
La presente práctica tiene como objetivo principal el análisis y procesamiento de audio digital mediante Python. Para ello, se implementan funciones que permiten aplicar transformadas de Fourier para visualizar el espectro de frecuencias, identificar notas musicales en archivos de audio y aplicar filtros de paso de banda para mejorar la calidad de las señales. También se construye una interfaz gráfica que permite aplicar diferentes tipos de filtros sobre archivos de audio, visualizar las señales y guardar los resultados.

## Ejercicio 1: Identificador de Notas Musicales

Este ejercicio desarrolla un identificador de notas musicales que permite reconocer la nota tocada en un archivo de audio. La implementación emplea técnicas de procesamiento de señales, incluyendo la Transformada Rápida de Fourier (FFT) para analizar el espectro de frecuencias, filtros de paso de banda para reducir ruido, y un diccionario de referencia que asocia cada frecuencia dominante con una nota musical. Este identificador está diseñado para funcionar con un único instrumento, lo que simplifica el análisis de la señal.

### Funciones Principales

- **fft_plot()**: Carga un archivo de audio en formato .wav y aplica la Transformada Rápida de Fourier (FFT) para convertir la señal al dominio de frecuencias. Además, muestra el espectro de frecuencias, destacando los picos de frecuencias dominantes, y extrae la frecuencia fundamental.
- **notas_frecuencias**: Diccionario que asocia cada nota musical (como Do, Re, Mi, etc.) con sus frecuencias correspondientes en distintas octavas. Este diccionario sirve como referencia para identificar la nota que corresponde a la frecuencia dominante detectada.
- **identificador_nota(frecuencia)**: Recibe una frecuencia en Hz y determina la nota musical correspondiente utilizando el diccionario notas_frecuencias, empleando una tolerancia del 5%.
- **filtro_pasa_banda()**: Implementa un filtro pasa banda utilizando un filtro Butterworth para eliminar frecuencias fuera del rango de interés, ayudando a reducir el ruido de fondo y mejorar la claridad de la señal.
- **get_frecuencia_sonido()**: Lee un archivo de audio y calcula la frecuencia fundamental utilizando la FFT y llama a identificador_nota para determinar la nota correspondiente.

### Problemas Encontrados y Soluciones

- *Ruido en el Espectro de Frecuencias*: Solucionado mediante filtro_pasa_banda(), aplicando un filtro de paso banda para limitar las frecuencias al rango esperado del instrumento.
- *Desviación en la Frecuencia de las Notas*: Añadida una tolerancia del 5% en identificador_nota para compensar ligeras desviaciones en la frecuencia de las notas.
- **Diferencias en la Detección con find_peaks**: Mantenidas dos versiones de procesamiento (con y sin find_peaks de scipy) para facilitar futuras pruebas y posibles aplicaciones de detección de acordes.

Estas soluciones mejoraron la precisión y robustez del identificador de notas musicales, haciéndolo adecuado para configuraciones de audio variadas.

## Ejercicio 2: Interfaz gráfica para filtrar audios

Este programa en Python implementa una aplicación de filtrado de audio que permite cargar archivos .wav, aplicar distintos tipos de filtros, reproducir el audio procesado y visualizar tanto la señal original como la filtrada en el dominio del tiempo y de la frecuencia. La interfaz gráfica está construida con Tkinter, y los filtros se implementan mediante funciones de scipy.signal.

### Funciones Principales

- **open_file()**: Permite al usuario seleccionar un archivo de audio y lo carga en el programa.
- **low_pass_filter(), high_pass_filter(), filtro_pasa_banda(), filtro_rechaza_banda()**: Implementan filtros de audio utilizando butter de scipy.signal para calcular los coeficientes de un filtro Butterworth y filtfilt para aplicarlo.
- **apply_filter()**: Aplica el filtro seleccionado por el usuario y visualiza la señal filtrada en el dominio del tiempo y de la frecuencia.
- **play_audio() y stop_audio()**: Reproducen y detienen el audio cargado o filtrado mediante la biblioteca sounddevice.
- **save_filtered_audio()**: Guarda la señal de audio filtrada en un nuevo archivo .wav, asegurando que esté dentro del rango de amplitud adecuado.

### Aportaciones Adicionales

- *Botones de Reproducción y Detención del Audio*: Añadidos botones para reproducir y detener el archivo de audio original, permitiendo al usuario comparar la señal antes y después de aplicar los filtros.
- *Opción para Guardar el Audio Filtrado*: La función save_filtered_audio() permite guardar el audio filtrado en formato .wav.
- *Etiqueta de Nombre de Archivo*: Muestra el nombre del archivo de audio actualmente cargado para referencia visual.

### Problemas Encontrados y Soluciones

- *Error al intentar graficar una señal filtrada no generada*: Resuelto con una verificación que muestra un mensaje de advertencia si no se selecciona un filtro válido.
- *Frecuencias de corte incorrectas*: Solucionado con una comprobación en los filtros de paso y rechazo de banda para advertir si las frecuencias de corte están en el orden incorrecto.
- *Normalización de la señal filtrada*: Implementada para asegurar que la señal esté dentro del rango permitido en la reproducción y almacenamiento en formato .wav.
- *Verificación de la señal filtrada antes de guardarla*: Añadida una comprobación en save_filtered_audio() para evitar intentos de guardar una señal no filtrada.

## Conclusión

Esta práctica nos ha permitido adentrarnos en el fascinante mundo del procesamiento de audio digital, explorando tanto el análisis de señales como el desarrollo de herramientas interactivas en Python. A través del identificador de notas musicales y la interfaz gráfica de filtrado de audio, hemos aplicado conceptos como la Transformada Rápida de Fourier (FFT) y el uso de filtros para mejorar la claridad de las señales. Este conocimiento sienta una buena base para futuros proyectos en los que queramos combinar análisis de señales con aplicaciones prácticas y visuales.
