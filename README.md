# Test Project
## Bienvenido a la prueba técnica

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](http://ec2-3-135-229-208.us-east-2.compute.amazonaws.com)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](http://ec2-3-135-229-208.us-east-2.compute.amazonaws.com)

### Unity3d 2021.3.13f1

## Puntos a evaluar

- Buenas prácticas y clean code
- Creatividad
- Patrones de diseño: Creación, estructura y comportamiento
- Principios SOLID
- Consumo de API RESTful

Este repositorio posee un proyecto pre-generado con Unity el cual tiene cargado 4 packages para el diseño de un juego 2D de plataforma, y un package el cual contiene assests para el diseño GUI.

La idea principal es crear un videojuego 2D de tipo plataforma, que posea un mundo pregenerado con **Tiles** o **Procedural**, el mundo deberá tener obstáculos y monedas; o algún otro tipo de ítems el cual sea obtenible por el usuario y deberán ser colocados en el mundo de manera procedural o pre-generado según el tipo de mundo que elijan.

``Obstáculos:`` - puede ser cualquier tipo de objeto que represente un peligro para el usuario, pueden ser ítems inamovibles, de IA o con físicas “esto es a su criterio”, al usuario hacer contacto con el objeto se acaba el juego.

``Monedas:``  puede ser cualquier tipo de objeto que represente algo importante de agarrar, buscar, o tomar para el usuario. Cada uno de estos objetos deberán representar un tipo de puntación numérica **“solo números enteros sin signo”** para el usuario **“mientras más obtengas más puntos tienes”**.

``Sistema de puntación:`` Este debe estar representado en la GUI del usuario y debe actualizarse cada vez que el usuario obtenga una moneda u o recompensa. Este sistema debe sincronizarse con la puntación actual del usuario en el servidor.

Escenas: el juego puede tener N cantidad de escenas, pero debe tener como mínimo 3 escenas fundamentales:
- Registro de usuario
- Inicio de sesión
- Puntuación total

``Escena – Registro de usuario:`` Esta escena debe tener dos entradas de textos para la creación de un nuevo usuario:
- **username:** debe ser un campo de tipo string que represente un correo o un alias
- **password:** debe ser un campo de tipo string alfa-numérico

``Escena – Inicio de sesión:`` Esta escena debe tener dos entradas de textos para el inicio de sesión:
- **username:** debe ser un campo de tipo string que represente un correo o un alias
- **password:** debe ser un campo de tipo string alfa-numérico

``Escena – Puntuación total:`` Esta escena deberá mostrar la puntación total que ha acumulado el usuario en el transcurro del juego

## Comunicación al servidor

Para esta prueba se ha asignado un servidor backend que ya posee escrita una Api RESTful, la cual contiene endpoints para manejar los usuarios y sus puntaciones “se trata de un CRUD”.

La idea principal es que el usuario para poder acceder al juego deberá registrarse primero o iniciar sesión si ya está registrado.

No se requiere un control de seguridad o de sesión muy sofisticado, solo un consumo básico de una API RESTful “CRUD” para manejar los estados de usuario; aquí solo se evaluarán tus habilidades para el consumo de Apis por HTTP desde Unity.

Cuando el usuario llegue al GameOver por haber colisionado con un obstáculo, solo en ese momento se deberá guardar – actualizar la puntación del usuario en el servidor “Endpoint: /setscore”

### Api V1: Endpoints ###

> DNS Principal del Test server:
> http://ec2-3-135-229-208.us-east-2.compute.amazonaws.com

| Endpoint | Descripción | HTTP Method | Headers |
| ------ | ------ | ------ |  ------ |
| /register | Registro de usuario | POST | NO
| /login | Inicio de sesión  | POST | NO
| /setscore | Incrementa la puntación del usuario | PUT | **Authorization** |
| /getscore | Obtiene la puntación del usuario  | GET | **Authorization** |
| /clear | Restablece la puntación del usuario a 0 | PUT | **Authorization** |
| /delete | Elimina el usuario | DELETE | **Authorization** |

Las Endpoints marcadas que requieren el Header Authorization deben pasar el token obtenido al iniciar sesión por la cabecera “Header” Authorization, de esa manera al actualizar, limpiar o borrar el servidor sabrá a cual usuario referirse.

Esta permitida cualquier Liberia para la comunicación **HTTP** desde Unity al servidor, pueden usar la nativa de Unity **" UnityWebRequest”** o cualquier otra de su conveniencia.

Nota: Al utilizar **“UnityWebRequest”** se deberá setear explícitamente la cabecera ``“Content-Type: application/json"`` en las peticiones que requieran un body de tipo **JSON**

**El mecanismo utilizado para guardar el token está bajo su criterio.**


**Entra en esta URL para obtener una descripción mas detallada de la API:**

> Swagger OpenApi Doc:
> https://documenter.getpostman.com/view/12165683/2s8YmKSPwV
