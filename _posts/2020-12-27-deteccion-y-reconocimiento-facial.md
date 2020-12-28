---
layout: post
title: Detección y reconocimiento facial [1/3]
autor: Sebastián Rosales
---

<p align=justify>
    Hace unas semanas vi un post de una gran empresa nacional, donde se mostraba una imagen RGB a la cual se le aplico 
    un algoritmo de detección visual. Surgió una reflexión, <strong><i>¿Cómo se puede realizar la detección facial, reconocimiento y cómo podemos aplicarlo en la realidad?</i></strong>
    <br/>
    <br/>
</p>

**La finalidad de estas tres entregas:**
* **Detección y reconocimiento facial [1/3]:**  Implementación de detección facial.<br/>
<br/>
* **Detección y reconocimiento facial [2/3]:** Implementación de una red neuronal de reconocimiento facial, utilizando redes pre-entrenadas y autoencoders.<br/>
<br/>
* **Detección y reconocimiento facial [3/3]:**  Aplicación biométrica y como reconocer *“sentimientos”*.<br/>

***

## ¿Como realizamos la detección? 

<div style="text-align: justify" markdown="1">Para efectuar la detección facial podemos utilizar la implementacion de OpenCV o la implementación de 
[IPAZC](https://github.com/ipazc/mtcnn).
</div>

<div style="text-align: justify" markdown="1">En el caso de OpenCV , la detección facial está implementando mediante el uso de [Haar](http://www.willberger.org/cascade-haar-explained/) cascades, en cambio, la implementación de [IPAZC](https://github.com/ipazc/mtcnn) usa como referencia la implementación de MTCNN FaceNet’s. Se encuentra basada en el paper Zhang, K et al. (2016) [ZHANG2016](https://ieeexplore.ieee.org/document/7553523).
</div>

<div style="text-align: justify" markdown="1">He decidido utilizar la implementación de [IPAZC](https://github.com/ipazc/mtcnn).
</div>

<div style="text-align: justify" markdown="1"> <strong>Los pasos a seguir son los siguientes: </strong>

* Pre-procesar las imágenes, asegurarse que sean RGB y transfórmalas a un Array (utilizaremos Numpy Arrays). 

* Inicializamos el detector de rostros [IPAZC](https://github.com/ipazc/mtcnn) y procesamos nuestra imagen.

* Obtenemos el centro del rostro a partir de los puntos reconocidos por el detector. 

* Visualizamos el resultado obtenido. 

</div>

***
<p class="message" align=justify markdown="1">
 El código completo se encuentra en el siguiente repositorio de github [<span style="color:blue">FaceDetection-srosalest-dev</span>](https://github.com/srosalest/FaceDetection-Recognition-srosalest-dev/blob/main/FaceDetection.ipynb), disponible en formato de Python notebook.
</p>
***

### Pre-procesamos las imágenes:

```
#pre-process the data

#load image.
image = Image.open("/content/prueba-2.jpeg")
black_image = np.zeros([image.size[1],image.size[0],3])
black_image.fill(0)

#if image isn't RGB transform it.
if(image.getbands() != ('R','G','B')):
    image = image.convert('RGB')

#get data array from the image.
image_data = np.asarray(image);

#check the shape of the array
#image_data.shape
```

### Inicializamos el detector y procesamos la imagen:
```
# initialize the face detector
face_detector = mtcnn.MTCNN()

#detect the faces
detection = face_detector.detect_faces(image_data)

"""
at this point we have already detected the faces 
and get all the data from the mtcnn algorithm 
(bounding box, main face points)
"""
```

### Obtenemos el centro del rostro
```
# get all data to get the center of the face and the confidence
data_faces = np.array([[]])
init_flag = True

for each_item in detection:
    #if true initialize array, else append it
    x_mouth,y_mouth = ((each_item['keypoints']['mouth_right'][0] + each_item['keypoints']['mouth_left'][0])/2 , (each_item['keypoints']['mouth_right'][1] + each_item['keypoints']['mouth_left'][1])/2)
    x_eye, y_eye = ((each_item['keypoints']['right_eye'][0] + each_item['keypoints']['left_eye'][0])/2,(each_item['keypoints']['right_eye'][1] + each_item['keypoints']['left_eye'][1])/2)
    x_nose, y_nose = (each_item['keypoints']['nose'][0], each_item['keypoints']['nose'][1])
    (x_center, y_center) = ((x_nose + x_mouth + x_eye)/3 , (y_nose + y_mouth + y_eye)/3)
    confidence = each_item['confidence']
    if init_flag:
        #get a particular bounding box dimensions
        data_faces = np.array([[(x_center, y_center) ,confidence]])
        init_flag = False
    else:
        data_faces = np.vstack((data_faces,[(x_center, y_center),confidence]))
```

## Resultados obtenidos:



***
<p class="message" align=justify markdown="1">
**_IMPORTANTE:_** La imagen utiliza es de propiedad de [<span style="color:blue">cronista.com</span>](https://www.cronista.com/internacionales/Chile-el-Congreso-evaluara-la-reforma-a-la-Constitucion-20191103-0013.html) y su uso fue exclusivamente informativo, no se procesó información biométrica a partir de ella.
</p>

