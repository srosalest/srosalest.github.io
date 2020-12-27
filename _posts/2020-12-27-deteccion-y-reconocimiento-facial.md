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
```
# initialize the face detector
face_detector = mtcnn.MTCNN()

#detect the faces
detection = face_detector.detect_faces(image_data)

#at this point we have already detected the faces 
and get all the data from the mtcnn algorithm 
(bounding box, main face points)
```