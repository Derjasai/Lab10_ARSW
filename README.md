### Escuela Colombiana de Ingeniería
### Arquitecturas de Software - ARSW

## Escalamiento en Azure con Maquinas Virtuales, Sacale Sets y Service Plans

### Dependencias
* Cree una cuenta gratuita dentro de Azure. Para hacerlo puede guiarse de esta [documentación](https://azure.microsoft.com/es-es/free/students/). Al hacerlo usted contará con $100 USD para gastar durante 12 meses.
Antes de iniciar con el laboratorio, revise la siguiente documentación sobre las [Azure Functions](https://www.c-sharpcorner.com/article/an-overview-of-azure-functions/)

### Parte 0 - Entendiendo el escenario de calidad

Adjunto a este laboratorio usted podrá encontrar una aplicación totalmente desarrollada que tiene como objetivo calcular el enésimo valor de la secuencia de Fibonnaci.

**Escalabilidad**
Cuando un conjunto de usuarios consulta un enésimo número (superior a 1000000) de la secuencia de Fibonacci de forma concurrente y el sistema se encuentra bajo condiciones normales de operación, todas las peticiones deben ser respondidas y el consumo de CPU del sistema no puede superar el 70%.

### Escalabilidad Serverless (Functions)

1. Cree una Function App tal cual como se muestra en las  imagenes.

![](images/part3/part3-function-config.png)

![](images/part3/part3-function-configii.png)

2. Instale la extensión de **Azure Functions** para Visual Studio Code.

![](images/part3/part3-install-extension.png)

3. Despliegue la Function de Fibonacci a Azure usando Visual Studio Code. La primera vez que lo haga se le va a pedir autenticarse, siga las instrucciones.

![](images/part3/part3-deploy-function-1.png)

![](images/part3/part3-deploy-function-2.png)

4. Dirijase al portal de Azure y pruebe la function.

![](images/part3/part3-test-function.png)

5. Modifique la coleción de POSTMAN con NEWMAN de tal forma que pueda enviar 10 peticiones concurrentes. Verifique los resultados y presente un informe.

6. Cree una nueva Function que resuleva el problema de Fibonacci pero esta vez utilice un enfoque recursivo con memoization. Pruebe la función varias veces, después no haga nada por al menos 5 minutos. Pruebe la función de nuevo con los valores anteriores. ¿Cuál es el comportamiento?.

**Preguntas**

* ¿Qué es un Azure Function?

Es una solución sin servidor que permite escribir menos código, mantener menos infraestructura y ahorrar costos. La infraestructura de la nube proporciona todos los recursos actualizados necesarios para mantener sus aplicaciones en funcionamiento. No se debe configurar la infraestructura necesaria.

* ¿Qué es serverless?

Serveless significa sin servidor, es una solución que permite crear y ejecutar aplicaciones con rapidez y al menos costo total, ya que no es necesario aprovisionar o administrar infraestructura. El proveedor de nube se encarga de la administración, por lo tanto, la persona solo se debe centrar en el código de la aplicación. El código, generalmente, se ejecuta dentro de contenedores sin estado que pueden ser activados por una variedad de eventos que incluyen solicitudes HTTP, eventos de base de datos, servicios de colas, alertas de monitoreo, carga de archivos, eventos programados, entre otros.

* ¿Qué es el runtime y que implica seleccionarlo al momento de crear el Function App?

Hace referencia al sistema en tiempo de ejecución, actúa como un pequeño sistema operativo y proporcionan toda la funcionalidad que los programas necesitan para ejecutarse. Esta carga todas las aplicaciones de un programa y las ejecuta en una plataforma. Al seleccionarlas se pueden escoger funciones básicas para la memoria, las redes y el hardware necesario para la ejecución de la función. Las ejecuta independientemente del sistema operativo.

* ¿Por qué es necesario crear un Storage Account de la mano de un Function App?

El Storage Account proporciona un espacio de nombres único para sus datos al que se puede acceder desde cualquier parte del mundo a través de HTTP o HTTPS, los datos son duraderos y de alta disponibilidad, seguros y enormemente escalables. Es necesario crearla de la mano de un Function App para las operaciones de almacenamiento y administración que realizan en la ejecución de las diferentes funciones.

* ¿Cuáles son los tipos de planes para un Function App?, ¿En qué se diferencias?, mencione ventajas y desventajas de cada uno de ellos.

Existen tres tipos de planes:

- Plan de Consumo: Escala automáticamente y se paga solo por los recursos de proceso cuando se ejecutan las funciones. Las instancias del host de Functions se agregan y quitan dinámicamente en función del número de eventos entrantes.
o	Plan de hospedaje predeterminado.
o	Se paga solo cuando se ejecutan las funciones.
o	Escala de forma automática, también durante periodos de carga elevada.

- Plan Premium: Escala automáticamente en función de la demanda, se usan los trabajos preparados previamente para ejecutar las aplicaciones sin demora después de haber estado inactivas, se ejecutan instancias más eficaces y se conectan a redes virtuales.
o	La aplicación de funciones se ejecuta de manera continua o casi continua.
o	Tiene muchas ejecuciones pequeñas y una factura de ejecución elevada.
o	Necesitan más opciones de CPU o memoria.
o	Su código debe ejecutarse durante más tiempo.
o	Se necesitan más características como la conectividad con red virtual.

- Plan de Azure App Service: Se ejecutan Functions a las tarifas normales del plan de App Service. Se usa en operaciones de larga duración, también cuando se requieren costos y escalado más predictivos.
o	Tiene máquinas virtuales infrautilizadas que ya ejecutan otras instancias de App Service.
o	Ejecuta una imagen personalizada en donde se ejecutan sus funciones.

* ¿Por qué la memorization falla o no funciona de forma correcta?

Esté falla o no funciona de manera correcta debido a al mecanismo de recursividad al implementarlo, los valores buscados se almacenan para facilitar y optimizar su futura búsqueda, sin embargo, gracias al gran tamaño de los números ingresados en las diferentes consultas, hace que la memoria se consuma con rapidez, impidiendo que la función sirva de manera correcta.

* ¿Cómo funciona el sistema de facturación de las Function App?

Esta se factura dependiendo del consumo de recursos observados (los cuales se miden en gigabytes por segundo GB*s), se calcula multiplicando el tamaño medio de la memoria en GB por el tiempo en milisegundos que es lo que dura una ejecución de la función. La memoria de una función se mide redondeando al alza a los 128 MB más cercanos hasta un tamaño de memoria máximo de 1.536 MB, y el tiempo de ejecución se redondea al alza a los 1 ms más cercanos. Para el tiempo de ejecución, el mínimo es de 100 ms. Los precios de Function tienen una concesión gratuita al mes.

* Informe

Se puede observar el desarrollo del laboratorio en cada uno de los pasos solicitados anteriormente.
