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


Para efectuar la detección facial podemos utilizar la implementacion de OpenCV o la implementación de 
[IPAZC](https://github.com/ipazc/mtcnn).
<br/>

En el caso de OpenCV , la detección facial está implementando mediante el uso de [Haar](http://www.willberger.org/cascade-haar-explained/) cascades, en cambio, la implementación de [IPAZC](https://github.com/ipazc/mtcnn) usa como referencia la implementación de MTCNN FaceNet’s. Se encuentra basada en el paper Zhang, K et al. (2016) [ZHANG2016](https://ieeexplore.ieee.org/document/7553523)
<br/>

He decidido utilizar la implementación de [IPAZC](https://github.com/ipazc/mtcnn). 
<br/>



