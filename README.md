# MTC Cloud Academy - Desarrollo de aplicaciones Inteligentes con GitHub Copilot y CodeSpaces

Este repositorio tiene el paso a paso para crear una aplicación inteligente de tipo conversacional usando Azure Open AI, GitHub y sus herramientas.

El objetivo es mostrar que se pueden construir aplicaciones con inteligencia artificial generativa con GH Copilot, GH Codespaces y usando servicios PaaS de Azure.

Cada sección tiene como objetivo principal mostrar una o varias características de Azure Open AI, GH Copilot, las cuales se especifican en cada sección, no es necesario contar con un ambiente de desarrollo porque usaremos GH Codespaces que ya tiene las extensiones y frameworks necesarios para ejecutar el taller.

Lo ideal es crear un Fork de este repositorio y utilizar el ambiente de Azure proporcionado en la sesión.

A continuación se muestra el contenido de la guía recomendada del workshop:
- [MTC Cloud Academy - Desarrollo de aplicaciones Inteligentes con GitHub Copilot y CodeSpaces](#mtc-cloud-academy---desarrollo-de-aplicaciones-inteligentes-con-github-copilot-y-codespaces)
  - [Escenarios de Negocio aplicables](#escenarios-de-negocio-aplicables)
  - [Prerequisitos](#prerequisitos)
  - [Paso a paso](#paso-a-paso)
    - [Habilitación de Azure Open AI , Servicios de búsqueda y Storage Account en Azure](#habilitación-de-azure-open-ai--servicios-de-búsqueda-y-storage-account-en-azure)
      - [A. Creación de Grupo de Recursos](#a-creación-de-grupo-de-recursos)
      - [B. Creación de Azure Storage Account](#b-creación-de-azure-storage-account)
      - [C. Creación de Azure Cognitive Search](#c-creación-de-azure-cognitive-search)
      - [D. Creación de Azure Open AI](#d-creación-de-azure-open-ai)
      - [E. Creación del Despliegue de ChatGPT](#e-creación-del-despliegue-de-chatgpt)
      - [F. Trae tus datos a Azure OpenAI](#f-trae-tus-datos-a-azure-openai)
    - [Creación de Azure Bot Service](#creación-de-azure-bot-service)
    - [Construcción del Bot](#construcción-del-bot)
    - [Adición de inteligencia artificial generativa usando el SDK del  Azure Open AI](#adición-de-inteligencia-artificial-generativa-usando-el-sdk-del--azure-open-ai)
    - [Integración del bot con Microsoft Teams](#integración-del-bot-con-microsoft-teams)


## Escenarios de Negocio aplicables

Los bots inteligentes que utilizan Azure Open AI y Azure Bot pueden ser implementados en una variedad de escenarios de negocio para mejorar la eficiencia, proporcionar soporte al cliente y optimizar operaciones. Aquí algunos ejemplos de cómo podrías usar un bot inteligente en diferentes industrias:

1. Servicio al Cliente y Soporte Técnico:
 - Automatización de respuestas a preguntas frecuentes.
 - Gestión de tickets de soporte con clasificación y priorización automática.
 - Resolución proactiva de problemas basada en la detección de patrones comunes en las consultas de los clientes.
2. E-commerce y Retail:
 - Bots de chat para asistir en la navegación de productos, recomendaciones personalizadas y soporte postventa.
 - Automatización del proceso de compra y asistencia en el seguimiento de pedidos.
 - Análisis de sentimientos de las reseñas de los clientes para mejorar la oferta de productos.
3. Finanzas y Banca:
 - Bots para ayudar en la consulta de saldos, transacciones, y servicios bancarios básicos.
 - Asistencia en la gestión de inversiones y recomendaciones financieras personalizadas.
 - Detección y alerta temprana de posibles fraudes o actividades sospechosas.
4. Salud y Asistencia Médica:
 - Bots para pre-triagé médico que pueden dirigir a los pacientes al especialista adecuado o aconsejar sobre la necesidad de una cita médica.
 - Asistencia en la gestión de citas y recordatorios para medicamentos.
 - Bots educativos que proporcionan información sobre condiciones médicas y tratamientos.
5. Turismo y Hospitalidad:
 - Bots que ofrecen servicios de conserjería virtual, ayudando a los huéspedes con reservas, información local, y recomendaciones.
 - Gestión y optimización de reservas y check-ins/check-outs mediante automatización.
 - Recolección de feedback de los huéspedes para mejorar el servicio.
6. Recursos Humanos:
 - Automatización de la captación de talento, filtrando CVs y programando entrevistas.
 - Bots para la orientación y formación de nuevos empleados.
 - Facilitación de respuestas a preguntas frecuentes sobre políticas de la empresa y beneficios.
7. Educación:
 - Bots tutoriales que proporcionan asistencia y recursos educativos a los estudiantes.
 - Automatización de la administración educativa, como la inscripción de cursos y gestión de horarios.
 - Facilitar la comunicación entre estudiantes, profesores y administrativos.

Estos bots se pueden personalizar y escalar según las necesidades específicas de cada negocio, proporcionando soluciones eficientes que mejoran la experiencia del usuario y optimizan los recursos internos.

En la guía estamos planteando un bot relacionado con Buceo, pero es recomendable que el escenario lo relaciones con la industria de tu escenario de negocio.

Buscamos habilitar el siguiente escenario técnico:
![alt text](images/image-a55.png)


## Prerequisitos

Para poder ejecutar la demo es necesario seguir los siguientes pasos: 

1. Contar con una suscripción de Azure, si no cuentas con una puedes crear una cuenta gratuita en [Azure](https://azure.microsoft.com/es-es/free/). Para el taller contamos con un ambiente de Azure proporcionado por el instructor, el les hará llegar un correo con las instrucciones para acceder al ambiente (Es necesario registrarse en la liga que esta en el correo, ingresar el código y posteriormente dar clic en el botón "Launch Lab").

2. Vamos al repositorio (https://github.com/demoedrmmsft/mtc-cloud-academy-openai-ghcopilot) y le damos clic en el botón de "Fork" ![alt text](images/image-a1.png)

3. Posteriormente le damos clic en "Create A new fork" ![alt text](images/image-a2.png) 

4. Especificamos el nombre del Repositorio (Podemos dejar el mismo nombre) y damos clic en "Create Fork" ![alt text](images/image-a3.png)

5. Crear una rama en el repositorio, siguiendo los siguientes paso:
   - a. Vamos a la sección de código, posteriormente en el menu de ramas damos clic ![alt text](images/image-1.png)
   - b. Especificamos el nombre de la rama (recomendable demo-"tualias") y del damos clic en Create branch demo-"tualias" from main ![alt text](images/image-2.png)
   - c. Una vez que estas en la rama recién creada le damos clic en "Code" -> En la sección de Codespaces le damos clic en el botón de "+" ![alt text](images/image-3.png)

6. Puede que intente abrir con Visual Studio code si lo tienes habilitado, si no puedes usar el navegador web. En caso que no visualizar el codespace, en nuestra rama, damos clic al botón de "Code" -> Damos clic en las elipses del codespace de nuestra rama y posteriormente en la opción de "Open in Browser" ![alt text](images/image-4.png)

7. Estas listo para seguir la guía y crear un bot inteligente que usa Azure Open AI .


## Paso a paso

Dentro del escenario tenemos un Bot inteligente que usara Azure OpenAI para agregar inteligencia artificial generativa, este Bot se podrá integrar con microsoft teams y con un portal web.  


### Habilitación de Azure Open AI , Servicios de búsqueda y Storage Account en Azure

En esta sección vamos a habilitar los servicios de Azure necesarios para el desarrollo de la solución. Para esto es necesario seguir los siguiente pasos:


#### A. Creación de Grupo de Recursos

El grupo de recursos es el contenedor que agrupa los recursos de Azure, en este caso vamos a crear un grupo de recursos para organizar los recursos que vamos a crear.

1. En el ambiente de Azure proporcionado por el instructor o en tu suscripción, vamos a la sección de "Resource Groups" y creamos un grupo de recursos. ![alt text](images/image-a4.png)

2. Especificamos el nombre (podemos usar el siguiente formato "rg-dev-"iniciales"+"-aoaighcopilotws") y la región y damos clic en "Review + Create". ![alt text](images/image-a5.png)


#### B. Creación de Azure Storage Account

El Storage Account de Azure es un servicio de almacenamiento en la nube seguro y altamente disponible que facilita el almacenamiento de datos estructurados y no estructurados en la nube. En nuestro escenario nos permitirá almacenar los archivos que queremos que use Azure OpenAI para darnos respuestas inteligentes a traves de nuestro Bot. Para crear una cuenta de almacenamiento en Azure, sigue estos pasos:

1. En portal de Azure, vamos al grupo que recién creamos, damos clic en "Create", buscamos la sección de "Storage accounts" y creamos una cuenta de almacenamiento. ![alt text](images/image-a6.png)

2. Especificamos el nombre de la cuenta de almacenamiento (podemos usar el siguiente formato "sadev"+"iniciales"+"aoaighcopilotws", seleccionamos "Standard" en Performance y la región. damos clic en "Review + Create" y posteriormente en el botón de "Create". ![alt text](images/image-a7.png) ![alt text](images/image-a8.png)


#### C. Creación de Azure Cognitive Search

Azure Cognitive Search es un servicio de búsqueda en la nube completamente administrado que proporciona la capacidad de agregar una búsqueda enriquecida a las aplicaciones web y móviles. En nuestro escenario nos permitirá buscar información en los archivos que almacenamos en el Storage Account y proporcionar un mecanismo efectivo de búsqueda a Azure OpenAI. Para crear un servicio de búsqueda en Azure, sigue estos pasos:

1. En el portal de Azure, vamos al grupo de recursos que creamos, damos clic en "Create", buscamos la sección de "Azure AI Search" y creamos un servicio de búsqueda. ![alt text](images/image-a9.png)

2. Especificamos el nombre del servicio de búsqueda (podemos usar el siguiente formato "aais-dev-"+"iniciales"+"-aoaighcopilotws", seleccionamos la región, y el pricing tier (Standard funciona bien para nuestro escenario) y damos clic en "Review + Create"; posteriormente en el botón de "Create". ![alt text](images/image-a10.png) ![alt text](images/image-a11.png)

#### D. Creación de Azure Open AI

Azure OpenAI es un servicio de inteligencia artificial generativa que permite a los desarrolladores crear aplicaciones inteligentes que pueden generar texto de forma natural y conversar con los usuarios de manera efectiva. En nuestro escenario nos permitirá agregar inteligencia a nuestro Bot para responder preguntas de forma inteligente. Para crear un servicio de Azure OpenAI, sigue estos pasos:

1. En el portal de Azure, vamos al grupo de recursos que creamos, damos clic en "Create", buscamos la sección de "Azure OpenAI" y creamos un servicio de Azure OpenAI. ![alt text](images/image-a12.png)

2. Especificamos el nombre del servicio de Azure OpenAI (podemos usar el siguiente formato "aoai-dev-"+"iniciales"+"-aoaighcopilotws", seleccionamos la región, y el pricing tier (S0 funciona bien para nuestro escenario) y damos clic en "Next" hasta llegar a la sección de "Review + submit"; posteriormente en el botón de "Create". ![alt text](images/image-a13.png) ![alt text](images/image-a14.png)

#### E. Creación del Despliegue de ChatGPT

Los Despliegues proveen endpoints a los modelos base de Azure OpenAI, en especial buscamos configurar el modelo de LLM (Large Language Model) que usaremos para hacer nuestro Bot Inteligente. En esta sección vamos a crear un despliegue de ChatGPT en Azure OpenAI, para esto es necesario seguir los siguientes pasos:

1. En el portal de Azure, vamos al servicio de Azure OpenAI que creamos, en la sección de "Deployments" damos clic en "Create Deployment". ![alt text](images/image-a15.png)

2. Damos clic en "Manage Deployments" para poder acceder a la consola de Azure OpenAI Studio ![alt text](images/image-a16.png)

3. Damos clic en "Create New Deployment" ![alt text](images/image-a17.png)

4. Especificamos el nombre del despliegue, podemos usar el siguiente formato "gpt-35-turbo", Importante  seleccionamos el modelo "gpt-35-turbo", modelo a escoger es el 0301; damos clic en "Create". ![alt text](images/image-a29.png)

#### F. Trae tus datos a Azure OpenAI

Para poder usar Azure OpenAI necesitamos traer nuestros datos a Azure OpenAI, en este caso vamos a especificar en el deployment que acabamos de configurar de donde obtendrá los datos con lo que nos ayudará de un archivo de texto que contiene información sobre Buceo. Para traer los datos a Azure OpenAI, sigue estos pasos:

1. En el portal de Azure, vamos al servicio de Azure OpenAI que creamos, en la sección de "Deployments", seleccionamos el Deployment que creamos y damos clic en "Open in Playground". ![alt text](images/image-a19.png)

2. Ahora vemos el Playground de Azure OpenAI, podemos ver que si interactuamos con el modelo de ChatGPT, nos da respuestas inteligentes, pero provenientes de su base de conocimiento publica. ![alt text](images/image-a20.png)

3. Por lo que si queremos acotarlo a que responda con datos de una fuente especifica necesitamos indicarlo al deployment. para esto en el panel lateral izquierdo le damos clic en "Add your Data" -> "Add a data source" ![alt text](images/image-a21.png)

4. Seleccionamos los siguientes datos y damos clic en "Next":
   - Data source:  Upload files
   - Suscripción de Azure
   - Azure Blob Storage
   - Puede que nos pida permisos para acceder a la cuenta de almacenamiento, damos clic en "Turn on CORS"
   - Azure AI Search
   - nombre del indice: contentindex
   ![alt text](images/image-a22.png)

5. Posteriormente nos solicita subir un archivo, damos clic en "Upload files" y seleccionamos el cualquier archivo que se encuentre en la carpeta "dataFiles" de nuestro repositorio y damos clic en "Upload files". ![alt text](images/image-a23.png)

6. Una vez que se subió el archivo, damos clic en "Next" ![alt text](images/image-a24.png)

7. En la siguiente pantalla nos solicita que indiquemos el tipo de Búsqueda, solo esta disponible la opción "Keyword", posteriormente seleccionamos el tamaño del Chunk; dejamos la opción por defecto.Damos clic en "Next" ![alt text](images/image-a25.png)

8. Nos muestra un resumen de la configuración, damos clic en el botón de "Save and close" ![alt text](images/image-a26.png)

9. Ahora podemos ver que esta ejecutándose el proceso de ingestion e indexación, esperamos a que terminen ambos procesos ![alt text](images/image-a27.png)

10. Una vez que termino el proceso de ingestion e indexación, podemos ver que el modelo de ChatGPT ya esta listo para responder con la información que se encuentra en el archivo que subimos. ![alt text](images/image-a28.png).

### Creación de Azure Bot Service

Azure Bot Service es un servicio de Azure que permite a los desarrolladores crear, conectar y administrar bots inteligentes que interactúan con los usuarios a través de canales populares como Microsoft Teams, Slack, Facebook Messenger, y otros. En nuestro escenario vamos a crear un Bot Service para alojar nuestro Bot inteligente que usará Azure OpenAI para responder preguntas de forma inteligente. Para crear un Azure Bot Service, sigue estos pasos:

1. En el portal de Azure, necesitamos crear primero el app service plan donde vamos a alojar el nuestro bot; para esto vamos al grupo de recursos que creamos, damos clic en "Create", buscamos la sección de "App Service Plan" y le damos clic en "Create". ![alt text](images/image-a30.png)

2. Especificamos el nombre del App Service Plan (podemos usar el siguiente formato "asp-dev-"+"iniciales"+"-aoaighcopilotws"), especificamos como sistema operativo Linux, seleccionamos la región, el pricing tier (S1 funciona bien para nuestro escenario) y damos clic en "Review + Create"; posteriormente en el botón de "Create". ![alt text](images/image-a31.png) ![alt text](images/image-a32.png)

3. Una vez que se creo el App Service Plan necesitamos crear un web app, vamos al grupo de recursos que creamos, damos clic en "Create", buscamos la sección de "Web App" y creamos le damos clic en "Create un Bot Service. ![alt text](images/image-a33.png)

4. Especificamos el nombre del Web App (podemos usar el siguiente formato "webapp-dev-"+"iniciales"+"-aoaighcopilotws"), seleccionamos el tipo de publish = "Code", el Runtime Stack = ".NET 6 (LTS), Sistema operativo = "Linux",  el App Service Plan que creamos, la región, y damos clic en "Review + Create"; posteriormente en el botón de "Create". ![alt text](images/image-a34.png) ![alt text](images/image-a35.png)

5. Una vez que se creo el Web App, necesitamos crear un Bot Service, vamos al grupo de recursos que creamos, damos clic en "Create", buscamos la sección de "Azure Bot" y creamos le damos clic en "Create". ![alt text](images/image-a36.png)

6. Especificamos el nombre del Bot (podemos usar el siguiente formato "bot-dev-"+"iniciales"+"-aoaighcopilotws"), seleccionamos el Data REsidency = "Global, Pricing Tier Standard, Type of App: User-Assigned Managed Identity y el Creation Type: Create new Microsoft App ID; damos clic en "Review + Create"; posteriormente en el botón de "Create". ![alt text](images/image-a37.png) ![alt text](images/image-a38.png)

7. Una vez que se creo el Bot Service, necesitamos configurar el messaging endpoint, para esto agregamos la url del web app anteriormente creada mas el posfijo de "/api/messages"; damos clic en "Apply". ![alt text](images/image-a39.png)

8. Por ultimo necesitamos habilitar el proceso de despliegue continuo en Github para que publique directamente en el web app, como primer paso habilitamos el SCM Basic Auth Publishing y FTP Basic Auth Publishing en la sección de configuración, damos clic en "Save" ![alt text](images/image-a40.png)

9. Posteriormente en la sección de "Overview" seleccionamos "Download publish profile". ![alt text](images/image-a41.png)

10. Abrimos el archivo en Notepad o el editor de texto de tu predilección, copiamos el contenido; vamos a Github en el repositorio al que le hicimos fork, vamos a la sección de Settings y después a "Secrets and Variables" -> Actions ![alt text](images/image-a42.png)

11. Creamos un nuevo secreto dando clic en el botón de "New repository secret" ![alt text](images/image-a43.png)

12. Especificamos el nombre= "AZUREAPPSERVICE_PUBLISHPROFILE" y el Secret con el valor que copiamos anteriormente.![alt text](images/image-a44.png)

13. Agregamos otro secreto llamado AZUREWEBAPP_NAME con el valor del nombre del web app que creamos. ![alt text](images/image-a45.png)

14. Agregamos un ultimo secreto llamado PROJECT_NAME con el nombre de nuestro proyecto, que para efectos prácticos puede ser "YourBot". ![alt text](images/image-a46.png)

15. En el web app es importante asignar el User Assigned Managed Identity que creamos en el Bot Service, para esto vamos a la sección de "Identity" y damos clic en "User Assigned" ![alt text](images/image-a47.png)

Con esto ya tenemos configurado el despliegue continuo de nuestro Bot en Azure Bot Service. Vamos a codificar nuestro Bot.

### Construcción del Bot

Una vez abierto nuestro Codespace en el navegador, en esta sección necesitamos platicar de las siguientes funcionalidades de GH Copilot: 

- Vemos que es muy fácil integrarlo en nuestro IDE (Visual Studio Code):
  1. Vamos al panel lateral izquierdo y damos clic en el menu de extensiones ó con el shortcut de "Ctrl+Shift+X" ![alt text](images/image-5.png)
  
  2. En la barra de Búsqueda buscamos "GitHub Copilot", tenemos disponible la ayuda disponible inline con GH Copilot y con un asistente Virtual con Github Copilot y esta al alcance de un clic en el botón instalar. ![alt text](images/image-6.png)
- Una vez explicado lo anterior vamos al panel lateral izquierdo y le damos clic en el menu de "Chat"; ahí vemos que tenemos una interfaz conversacional donde podemos poner nuestros prompts. ![alt text](images/image-7.png)

Procedemos a construir nuestro bot:

1. En el asistente de GH Copilot escribimos el siguiente prompt: "Como desarrollador, necesito crear una aplicación web de tipo bot en .Net Core llamada YourBot, donde utilice el template de EchoBot del Bot Framework de Microsoft". Si la Respuesta es similar a la siguiente imagen le damos clic en botón de thumbs up para indicar que lo que nos recomendó fue acertado (con eso le indicamos a GH Copilot que nos dio una respuesta correcta y en futuras interacciones no dará respuestas mas adecuadas). ![alt text](images/image-8.png)

2. Es importante recalcar que la estructura del prompt anterior es del tipo "Zero Prompt", sin embargo al usar técnicas como especificar cual es nuestro rol, expresar una acción y detallar un contexto nos permite tener respuestas mas certeras para usarlas en el desarrollo de nuestra solución. Ahora necesitamos aplicar lo que nos recomienda. Para esto vamos a instalar las platillas , abrimos una terminal en el Codespace de la siguiente forma: Menu Contextual -> Terminal -> New Terminal ![alt text](images/image-9.png)

3. Posteriormente posicionamos el cursor en la primera recomendación y seleccionamos la opción de "Insert in Terminal", ejecutamos el comando. ![alt text](images/image99.png)
   Puede ser que falle nuestro comando.
   ![alt text](images/image-199.png)

4. En dado caso que falle, una de las ventajas que tenemos es que podemos usar GH copilot, tiene la posibilidad de usar comandos para poder obtener recomendaciones para resolver un error en la terminal, en la ventana de copilot escribimos el prompt "@terminal /explain #terminalLastCommand" donde con la @ especificamos el area de trabajo que en nuestro caso es la consola, / usamos el comando para que GH Copilot nos explique porque esta mal el comando anterior y con el # especificamos que comando que en nuestro caso es el ultimo. lo cual nos ayuda a no cambiar de contexto y seguir trabajando en el IDE. ![alt text](images/image-299.png)

5. Aplicamos las recomendaciones e intentamos ejecutar el comando anterior y vemos que esta mal de nuevo. ![alt text](images/image-399.png)

6. Es posible que ya no se encuentre este paquete por lo que vamos a cambiar nuestro prompt anterior. Necesitamos usar el template de EchoBot, por lo que necesitamos ejecutar el siguiente prompt "Como desarrollador, necesito crear una aplicación web de tipo bot en .Net Core llamada YourBot, donde utilice el template de EchoBot del Bot Framework de Microsoft. El template de EchoBot para C# lo necesito instalar con el comando dotnet -i, usando dotnet new -i Microsoft.Bot.Framework.CSharp.EchoBot"![alt text](images/image-499.png)

7. Seguimos las recomendaciones ejecutamos el comando ![alt text](images/image-599.png)

8. Creamos nuestro proyecto ejecutando el comando de creación recomendado. ![alt text](images/image-699.png)

9. Nos cambiamos de repositorio y ejecutamos el proyecto. ![alt text](images/image-799.png)

10. Si estamos en el browser, nos va a preguntar si queremos abrirlo en el browser, le damos clic ![alt text](images/image-899.png)

11. El api de nuestro bot esta lista. ![alt text](images/image-999.png)

12. Ahora ya tenemos el cascaron de nuestro bot, podemos usar una funcionalidad para realizar un renombre en el archivo de YourBot/Bots/EchoBots.cs. Vamos entender como esta conformada esta clase. Abrimos el archivo ![alt text](images/image-1099.png)

13. Puede resultar confuso si no tengo el conocimiento de como funciona un bot, por tal motivo vamos a pedirle a GH Copilot para que nos explique. Abrimos el GH Copilot Chat y con el archivo abierto escribimos @workspace /explain. ![alt text](images/image-1199.png)

14. GH Copilot nos explica el contenido de nuestro Bot ![alt text](images/image-1299.png)

15. Pedimos a Copilot que nos ayude a renombrar EchoBot por YourBot, para esto escribimos el siguiente prompt "Renombrar EchoBot.cs por YourBot" ![alt text](images/image-1399.png)

16. Seguimos el procedimiento para realizar el rename de EchoBot.cs ![alt text](images/image-1499.png)

17. Cambiamos donde diga EchoBot por YourBot presionamos Ctrl+Shipt+H y reemplazamos ![alt text](images/image-1599.png)  

18. Volvemos a ejecutar el bot, abrimos a la terminal y ejecutamos el siguiente comando: "dotnet run" ![alt text](images/image-1699.png)

19. Nuestro bot esta listo para ser Desplegado en Azure ![alt text](images/image-1799.png)

20. Ya existe un recurso de Azure Bot configurado, en la sección de Configuración encontraremos el Microsoft App ID y el App Tenant ID,  es necesario ir al archivo appsettings.json y los reemplazamos e indicamos la siguiente información:
    - "MicrosoftAppType": "UserAssignedMSI",
    - "MicrosoftAppId": "XXXXX-XXXX-XXXX-XXXX-XXXXX",
    - "MicrosoftAppPassword": "",
    - "MicrosoftAppTenantId": "xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx"
  
   Tal y como lo vemos en la siguiente imagen ![alt text](images/image-2099.png)

21. El proyecto ya tiene un definición de un workflow que despliega la solución en un Azure Bot. por lo tanto debemos ir a panel lateral izquierdo en la sección de Source Control, demos especificar el mensaje y podemos utilizar a GH Copilot para que nos recomiende una descripción ![alt text](images/image-2199.png)

22. Una vez generado el comentario le damos clic en el Botón de "Commit" ![alt text](images/image-2299.png)

23. Sincronizamos los cambios dando clic en el botón de "Sync Changes" ![alt text](images/image-2399.png)

24. Al realizar esto se ejecuta el workflow que despliega la solución usando el workflow de Github actions a los servicios de Azure. Para visualizarlo le damos clic en el proyecto de github en la sección de Actions ![alt text](images/image-2499.png)

25. Para ver el detalle le damos clic en el ultimo despliegue y vemos el detalle, en nuestro caso fue exitoso. ![alt text](images/image-2599.png) 

Procedemos a hacer inteligente nuestro bot

### Adición de inteligencia artificial generativa usando el SDK del  Azure Open AI

Para este escenario necesitamos agregar inteligencia a nuestro bot, por lo que nos auxiliaremos de Github Copilot para usar Azure OpenAI para alcanzar este objetivo. 

1. Donde le vamos a agregar inteligencia es en el archivo de Bots/YourBot.cs, por lo que procedemos a abrirlo

2. En GH Copilot Chat indicamos el siguiente prompt : "Como instalar la librería de Azure y Azure.AI.OpenAI esta ultima en modo prerelease" (Importante agregar el using correspondiente "Azure.AI.OpenAI" y los que falten)
3. Seguimos el procedimiento indicado en la consola ( es importante que estemos en la carpeta del proyecto usando el comando "cd YourBot") ![alt text](images/image-2799.png)

4. Vamos a usar el encadenamiento de prompts para mejorar la eficiencia de las recomendaciones del Gh Copilot in lines en los archivos que estamos trabajando.  En la linea 12 damos un salto de linea y ponemos un comentario con el siguiente prompt : "Generar 2 propiedades para la llave y el endpoint de Azure OpenAI, con un valor predeterminado"

5. Vamos al recurso de Azure OpenAI y buscamos Key 1 y endpoint en la sección "Keys and EndPoint",  procedemos a reemplazar los siguientes valores en el código:
   - Key de Azure OpenAI = "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
   - Endpoint de Azure OpenAI = "https://xxxxxxxxxxxx.openai.azure.com/"

6. Necesitamos generar un método para invocar a OpenAI por lo que ponemos un comentario en la linea 16 con el siguiente prompt : "Generar un método asíncrono que regrese un string y que reciba como parámetro un texto, el método esta vacío" ![alt text](images/image-2999.png)

7. Damos un salto de linea en la linea 19 y escribimos el siguiente prompt como comentario para generar la llave para acceder al cliente de Azure Open AI: "generar un AzureKeyCredential con la llave de OpenAI"![alt text](images/image-3099.png)

8. Damos un salto de linea y escribimos el siguiente prompt como comentario = " inicializar el cliente de OpenAIClient con el endpoint de OpenAI y el AzureKeyCredential" ![alt text](images/image-3199.png)

9. Ingresamos el siguiente comentario para inicializar las opciones de nuestro cliente "Inicializar las opciones de ChatCompletionsOptions de forma inline indicando el parámetro de DeploymentName de tipo gpt-35-turbo y Messages recibido de la variable text de tipo ChatRequestUserMessage. Siguiendo el formato new Class { Property = Value }" ![alt text](images/image-3299.png)

10. Si existe algún error pueden usar el siguiente código:
            "var options = new ChatCompletionsOptions
            {
                  DeploymentName="gpt-35-turbo",
                  Messages = {
                      new ChatRequestUserMessage (text )
                  },                
             };"

11. Invocamos el método y ponemos el siguiente comentario: "Invocar el método GetChatCompletionsAsync y regresar la respuesta de la llamada" ![alt text](images/image-3399.png)

12. Regresar la respuesta es el siguiente paso, por lo que ponemos el siguiente comentario: "regresar el texto de la respuesta de Choices" ![alt text](images/image-3499.png)

13. En el método de OnMessageActivityAsync eliminamos la linea donde esta la variable de replytext y ponemos el siguiente comentario: "Declarar una variable de tipo string llamada replyText y asignarle el valor de la respuesta de GetOpenAIResponseAsync con el parámetro de texto de la actividad recibida" el nombre del método puede variar usa el que te genero anteriormente. ![alt text](images/image-3599.png)
14. El código debe quedar de la siguiente forma: ![alt text](images/image-a54.png)

15. Procedemos a hacer el commit y el push para que se despliegue el bot. ![alt text](images/image-3699.png)

### Integración del bot con Microsoft Teams

Una vez desplegado el Bot, procedemos a probarlo, para esto vamos al recurso de azure bot, e interactuamos con el en la opción de Test in Web Chat ![alt text](images/image-a48.png)

Para instalarlo en MS Teams , en el recurso de Azure Bot, nos vamos a Channels -> Microsoft Teams ![alt text](images/image-a49.png)

Indicamos que estamos de acuerdo con los términos del servicio ![alt text](images/image-a50.png)

En la sección de Messaging indicamos que es para "Microsoft Teams Commercial" y damos clic en "Apply" y despues en "close"  ![alt text](images/image-a51.png)

En channels seleccionamos "Open in Teams" ![alt text](images/image-a52.png)

Nos vamos a Teams, puedes ingresar el prompt que corresponda al documento que elegiste. ![alt text](images/image-a53.png)