# Detección de Vehículos y Motos para Estacionamiento en Jetson Nano
Este repositorio contiene el código y los recursos necesarios para ejecutar un modelo de detección de vehículos y motocicletas en un Jetson Nano. El proyecto utiliza un modelo preentrenado en formato PHT para realizar inferencia en tiempo real, aprovechando las capacidades de procesamiento del Jetson Nano y mostrando los resultados de la detección usando OpenCV.

## Descripcion
Este proyecto se centra en la detección de vistas frontales y traseras de vehículos y motocicletas utilizando un modelo de aprendizaje profundo entrenado para Jetson Nano. El repositorio incluye:

- Modelos preentrenados en formato PHT con diferentes números de épocas.
- Código para detección en tiempo real utilizando OpenCV (cv2).
- Uso de las bibliotecas jetson-inference y jetson-utils de NVIDIA para la inferencia optimizada.
- Instrucciones para convertir los modelos PHT a formato ONNX, optimizando la inferencia en Jetson Nano.
  
Utilizamos el modelo entrenado con 14 épocas para la inferencia, ya que proporciona el mejor equilibrio entre rendimiento y precisión.


## Instalacion

    $ git clone https://github.com/AlejoVargasO/programacion.git
    $ cd programacion
    $ docker/run.sh

## Conversion de Modelos a ONNX

    
## 3. Uso

### Ejecución del Modelo de Detección

  1. El código está configurado para ejecutar el modelo y mostrar las cajas delimitadoras en una transmisión de video utilizando OpenCV.

  2. El modelo predeterminado utilizado para la inferencia es el entrenado con 14 épocas. Puedes modificar el código para usar otro modelo si lo prefieres.

  Para ejecutar el script de detección:

    
### Convertir modelo a formato ONNX para TensorRT

    $   python3 onnx_export.py --model-dir=models/Car_Detection 


### Montar el docker con nuestro modelo ya entrenado
    *   Creamos una carpeta en el directorio raiz (fuera del docker)
    *   Copiamos en la carpeta los archivos labels.txt, ssd-mobilenet.onnx y nuestro programa my_detection.py (por ahora este archivo vacío)
    *   Si es necesario dar permisos a la carpeta usando chmod
    *   Montamos el docker agregando esta carpeta
    
    $ sudo mkdir my_project
    $ sudo chmod -R a+rwx my_project
    $ cd jetson-inference
    $ docker/run.sh --volume ~/my_project:/my_project


### Prueba de nuestro código

    $ python3 /my_project/Car_Detection.py
    

Algunas instrucciones que usamos en consola

    $   docker/run.sh --volume ~/my_project:/my_project
    $   python3 onnx_export.py --model-dir=models/Car_Detection 
    $   detectnet --model=models/Car_Detection/ssd-mobilenet.onnx --labels=models/Car_Detection/labels.txt --input-blob=input_0 --output-cvg=scores --output-bbox=boxes /dev/video0
    $   python3 /my_project/Car_Detection.py

## 4. Inferencia de modelo SSD en video (.mp4) / Modificación de threshold usando argparse

Modificamos la captura de video para leer un archivo .mp4 y no la cámara web

    $  camera = cv2.VideoCapture("/my_project/videoprueba.mp4")

Usamos argparse para modificar por parámetro el threshold de detection

    $   python3 /my_project/Car_Detection.py --threshold 0.5
