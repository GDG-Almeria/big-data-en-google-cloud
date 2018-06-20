# Big data en Google Cloud

Tutorial de implementación de una arquitectura de adquisición, procesamiento, almacenamiento y análisis de datos en Google Cloud.

El sistema simulará una arquitectura de adquisición y análisis de datos de un conteo de entrada y salida de personas de locales comerciales.

## Crear proyecto en Google Cloud

- Si no tienes una cuenta de Google (o GMail), puedes crear una [aquí](https://accounts.google.com/signup/v2/webcreateaccount?flowName=GlifWebSignIn&flowEntry=SignUp). Si dispones de una, puedes pasar al siguiente paso.

- Accede a la consola de Google Cloud Platform: https://console.cloud.google.com/

- Crea un nuevo proyecto y recuerda el ID de proyecto indicado:

![Seleccionar proyecto](https://lh4.googleusercontent.com/d2xV2zKtFXLxHbdYpXAjrnyX8j8TV51at9UixBnZgkOE8VUYes_O9bAzIbulUrzTsLhtPxocTXXBYcNZQfFmvOIeiJH0XIRWGOSRpuEvxr95qtZ0YsOuNlIpX7lrLFeGeKutTSMu)

![Crear proyecto](https://lh4.googleusercontent.com/QPGsJFO0ZCbQyS_ycQw0ziur9EUClITHt6WFdVIjoPF33eHXUh5GmpOdBgkNbT3f4l4pz2Y1yPxHfNTXLx0QNnYiNNHxdmCkENcPLEcOryjQSMFbgdeLqaZjuEBu1CF2PgUPQ_4m)

![ID de proyecto](https://lh3.googleusercontent.com/-PHnsItct9TQtzFVOttrHwtlfbkimdQ_4tiDXYNCV2uhz3Hf7qYKopN-KjdMezLH-rWrj6Pdww6bSg3bNqJPB8Wu5jxcNLSYPpCaA56QX8rtV9Pq6io6ry0_spLU7--wUMMU8htB)

## Activar billing

- Activa una cuenta de gasto para tu proyecto: https://console.cloud.google.com/billing. Ejecutar este tutorial no debe costar más de 1 €. Un nuevo usuario dispone de una [prueba gratuita de $300](https://console.cloud.google.com/freetrial?hl=en).

## Activa las APIs

En el menú, selecciona "APIs & Services > Library" y activa las siguientes APIs:

- Google Compute Engine APIs
- Google Clou Pub/Sub API
- Google Cloud Storage
- Google Dataflow API
- BigQuery API

## Abrir Cloud Shell

Haz click en el icono de Cloud Shell en el menú superior:

![Abrir Cloud Shell](https://lh6.googleusercontent.com/SiUBtFWkjvKqUgeT5n7EEhjOEWOXdRRWuIb2aa3VTHBtkGDG27fCiMUNGWR43_MGa9M3LFrvoeteX-70lrnXlarMvGdViHOUCvK-WBjZobHfmxfvnY99Kt0gWA9xmFNv0Ma4Inya)

## Configurar Cloud SDK

- Comprueba tu cuenta y autenticación:

`gcloud auth list`

- Comprueba la configuración:

`gcloud config list`

- Establece una zona y region por defecto:

```
gcloud config set compute/zone europe-west1
gcloud config set compute/region europe-west1-b
```

## Clonar repositorio

En tu terminal de Cloud Shell, clona este repositorio y accede al mismo:

`git clone XXX`

`cd XXX`

## Crea una cuenta de servicio

- En el menú "APIs & Services > Credentials", pulsa "Crear credencial", "Service account key", "New service account", selecciona de tipo "JSON" y pulsa crear.

- Se descargará un archivo de tipo JSON.

- Abre el editor de texto de Cloud Shell.

- Crea un nuevo archivo de nombre `credentials.json` en la carpeta actual (dentro del repositorio), copia el contenido del archivo descargado y guárdalo.

- Crea la variable de entorno `GOOGLE_APPLICATION_CREDENTIALS` con el valor del path al archivo `credentials.json`, p. ej.:

`export GOOGLE_APPLICATION_CREDENTIALS="/home/info/XXX/service-account-file.json"`

Puedes usar el comando `pwd` para determinar el path del directorio actual.

## Crea un tema de Cloud Pub/Sub

`gcloud pubsub topics create fuente-datos`

## Crea una suscripción de Cloud Pub/Sub

`gcloud pubsub subscriptions create subscripcion-datos --topic fuente-datos`

## Comprueba la publicación y recepción de mensajes

```
gcloud pubsub topics publish fuente-datos --message "hola mundo!"
gcloud pubsub subscriptions pull --auto-ack suscripcion-datos
```

## Crea un dataset en BigQuery

- Crea un dataset con las siguientes características:

- Crea una tabla con las siguientes características:

## Crea el trabajo en Cloud Dataflow

Descripción

## Crea una VM como fuente de datos

- Crea una VM siguiendo los pasos (https://cloud.google.com/compute/docs/instances/create-start-instance#publicimage) con la siguiente configuración:
  - Nombre: cualquiera
  - Región: europe-west1
  - Zona: europe-west1-b
  - Tipo de máquina: n1-standard-1 (1 vCPU, 3.75 GB de memoria)
  - Disco de inicio: Debian GNU/Linux 9 (strech) de 10 GB (por defecto)
  - Firewall: permitir tráfico HTTP y HTTPS

- Crea la instancia y comprueba que está activa.

- Conéctate a dicha instancia a través del botón "SSH" de la consola.

- Clona el repositorio en la instancia:

```
git clone XXX
cd XXX
```

- Crea un nuevo archivo de nombre `credentials.json` en la carpeta actual (dentro del repositorio), copia el contenido del archivo descargado y guárdalo.

`nano credentials.json`

- Crea la variable de entorno `GOOGLE_APPLICATION_CREDENTIALS` con el valor del path al archivo `credentials.json`, p. ej.:

`export GOOGLE_APPLICATION_CREDENTIALS="/home/info/XXX/service-account-file.json"`

## Comienza la publicación de datos

- Ejecuta el script de Python:

`python3 data_publish.py`

- Comprueba la recepción de mensajes:

```
gcloud pubsub subscriptions pull --auto-ack suscripcion-datos
```

## Ejecuta el trabajo de Cloud Dataflow

Descripción

## Comprueba el trabajo de Cloud Dataflow

Descripción

## Comprueba el dataset en BigQuery

Descripción

## Analiza los datos con Cloud Datalab

Descripción

## Crea un cuadro de mandos con Cloud Data Studio

Descripción

## Desactiva los servicios utilizados

Borra los recursos y servicios utilizados para detener la continuación de los gastos asociados.

- Elimina la VM desde el menú "Compute Engine".

- Elimina el trabajo de Dataflow desde el menú "Dataflow".

- Elimina el tema y suscripción desde el menú "Pub/Sub".

- Elimina el dataset desde el menú "BigQuery" (opcional).

- Elimina los bucket creados desde el menú "Storage".

```
gcloud pubsub subscriptions delete my-sub
gcloud pubsub topics delete my-topic
```
