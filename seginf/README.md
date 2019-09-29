SEGURIDAD INFORMATICA
=============

* Virus / antivirus
* Cripto simetrica asimetrica
* Paradigma de seguridad
* Norma ISO 27001: como trabajar con la norma, puntos de control

Conceptos básicos
=====================

## ¿Qué es la seguridad de la información?
La seguridad de la información es la protección de la información de una amplia variedad de
amena-zas, con el objeto de asegurar la continuidad del negocio, minimizar los riesgos y maximizar
el retorno de inversión y las oportunidades de negocio.

## ¿Cómo se consigue?
A través de _controles_. El grado de controles necesarios se hace a través de una _evaluación de riesgos_

## Control
Un control es una manera de manejar riesgos: incluye políticas, estructuras, prácticas o procedimientos
que pueden ser técnicos, legales, etc.

Paradigma de seguridad
===================

## Características de la información
La seguridad se encarga de asegurarse de la
* Confidencialidad: que la información esté disponible solo para quien se quiera que esté disponible
* Disponibilidad: que la información pueda ser accedida cuando se lo requiera
* Integridad: que la información no haya sido modificada sin autorización
* No repudio: que el emisor no pueda negar haber mandado un mensaje si lo hizo, ni el receptor negar haberlo recibido si lo hizo
* Autenticación de origen: que se conozca la identidad del autor del mensaje

Diferentes evaluaciones de riesgo pueden concluir en diferentes requisitor para la información
que maneje un sistema.

Una nota sobre no repudio
---------------------
Legalmente se da en caso solo de firmas electrónica (con aprevio cuerdo de partes) o digitales.

Normativa
=========
Muy por arriba: se recomiendan las cosas razonables.
* Que seguridad sea un area gerencial
* Enfoque multidisplinario
* Contacto con especialistas tecnicos externos
* Establecimiento de procesos
* Se recomienda tener un inventario de los activos
* RRHH: trabajar con empleados para que entiendan sus responsabilidades.

## Politicas
Es muy importante tener politicas de seguridad: proporciona direccion
y apoyo a otras areas para mantenerse alineadas a los requerimientos
de seguridad del negocio.

Virus
=========

## Caracteristicas
Un virus sigue el patron DAS: **D***añino **A***utoreproductor **S**urrepticio

1. siempre inflije daño
2. siempre busca replicarse
3. actua de manera que un usuario normal no se da cuenta de que esta por ahi

## Modelado
* Modulo de reproduccion: hace copias de si mismo en el mismo o en otro sistema
* Modulo de ataque: impacto sobre integridad, disponibilidad o quizas confiencivilidad
* Modulo de defensa: refuerza la surreptividad del virus, lo esconde
El unico obligatorio es el de reproduccion

## Requsitos
Un programa necesita tiempo de procesamiento, memoria y que alguien lo ejecute.
Para lograr que alguien lo ejecute lo metes en un programa que parece cool.

## Consecuencias
El virus puede causas darnio en perfomrance, informacion, hardware
El virtus tiene danio explicito (lo que quiere hacer) e implicito (por ejemplo ocupa recursos)
Dice que el virus no puede hacer danio de hardware para mi humo

### Historia
El concepto de virus aparece en el 86.

Sistemas antivirus
======================
## Modelado
* modulo de control
** administracion de recursos
** identificacion de codigo
** verificacion de integridad
* modulo de respuesta
** alarma
** reparacion
** evitar

## Tipos
* Heuristicos: encuentran amenazanas desconocida analizando comportamientos
sospechosos
* Deterministicos: encuentras amenazas conocidas comparando fingerprints de
archivos contra una base de dato

Cripto
===============
Simetrica
---------
Muy facil: hay una contraseña (_key_) que te sirve para encriptar.
Se la pasas a otro chabon y el chabon puede desencriptar.

## Algoritmos
* AES: usado ahora, formato 256, 192, 128 bits.
* DES
* Triple DES

Asimetrica
---------

Tenes una llave publica y una privada.
Lo que se encripta con publica se desencripta con privada, lo que se encripta
con privada se desencripta con publica.
Toda la magia se puede pensar si tenes claro esto.

Si quiero mandarle a Brunito el mensaje "hola brunito"
sin que se entere Alguien, encripto con la publica de Brunito
como solo él tiene su privada, el solo lo va a poder leer.

Si brunito quiere contestarme OK, agarra mi publica
y encripta el OK y yo solo lo puedo leer.


Potencial problema: Nachito ve estos mensajes, aunque no los puede entender.
Pero me puede mandar un mensaje encriptado con mi publica
diciendome "soy brunito y no quiero que me saludes más"

Solución:  brunito encripta su mensaje con mi publica y luego
encripta eso con su privada: ahora el mensaje solo pudo haber
sido emitido por brunito. Esto es lo que se conoce como no
repudio. Cuando el mesnaje me llega, agarro la publica de brunito,
desencripto, ahora agarro mi privada, desencripto, y ahora
tengo el mensaje.

### No repudio
Legalmente, el no repudio requiere de una ley
de firma electrónica o al menos un acuerdo entre partes.

Firmas
-------
Electronicas son todas las firmas. Es cualquier sistema
donde yo uso un sistema de hashing/fingerprint para
tener presuncion de origen e integridad.

Lo que se hace es hashear un mensaje, encriptar ese
hash con mi privada, luego enviar mensaje y el hash
encriptado. El que recibe, puede chequear
que el hash del mensaje es tal, y que solo yo lo pude
haber generado porque solo yo tengo mi privada, para esto
claramente necesita mi publica.

Firma digital es el sistema de firma electrónico respaldado
por la ley de firma digital argentina.

### Firma digital y Diffie&Hellman
En principio, cualquier algoritmo de criptografía asimétrica
puede usarse para implementar firmas electrónicas. Pero
la firma digital argentina requiere que el sistema
sea de "append": el hash firmado va concatenado
al mensaje que se quiere firmar.

Sistema de firmas de Diffie y Hellman no sigue este sistema,
por lo tanto no puede usarse en Argentina para implementar
uan firma digital.

Hashing
--------
Un hash es un choclo de numeros que es mas-o-menos
unico para un archivo. Todos los hashes ocupan
la misma cantidad de bytes (son igual de largos).

### Ejemplo:

```
>>> hashlib.sha256(b"hola brunito").digest() # como bytes puritos
b'm\x88\x19\x97Eb\xe0\xbf\x1e\x90\n\x9e\x962\xbbg\xe9\x81\x81\xe4o\xa6\xc7\x99c\xa3a \xae"a\xd8'
>>> hashlib.sha256(b"hola brunito").hexdigest() # en hexa
'6d8819974562e0bf1e900a9e9632bb67e98181e46fa6c79963a36120ae2261d8
```

### ¿Por qué más o menos único?
Si lo pensás un segundo se ve fácil.
Si un hash siempre tiene la misma longitud, pero
hay una infinita cantidad de longitudes de mensajes posibles,
en algún momento los hashes se van a repetir.

Dicho de otra manera, hay más mensajes posibles que hashes posibles,
por lo tanto si hasheo todos los mensajes en algún momento voy a repetir hashes.

Lo importante en un sistema de hash es que un hash no sea reversible
(no pueda conocer el texto que lo genero de una manera más barata que bruteforcing) y
que no pueda generar colisiones arbitrarias (dado un hash, generar un mensaje, aunque
no sea el original, que tenga el mismo hash).
