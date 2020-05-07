---
page_type: sample
products:
- ms-graph
languages:
- csharp
description: "Los datos de seguridad a los que se obtiene acceso a través de la API Microsoft Graph Security son muy confidenciales y, por lo tanto, están protegidos por permisos y roles de Azure AD"
extensions:
  contentType: samples
  technologies:
  - Mcirosoft Graph
  - Microsoft Graph
  services:
  - Security 
  createdDate: 4/19/2018 10:35:33 AM
---
# Aplicación de ejemplo de autenticación de Microsoft Graph en C#

## Introducción

Los datos de seguridad a los que se obtiene acceso a través de la API Microsoft Graph Security son muy confidenciales y, por lo tanto, están protegidos por permisos (también denominados ámbitos) y roles de Azure AD (AAD). La API Microsoft Graph Security exige la autenticación y la autorización (AuthNZ) para proteger los datos confidenciales a los que da acceso.
Puede encontrar información más detallada en [Understanding authorization when calling the Microsoft Graph Security API](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2) (Descripción de la autorización al llamar a la API Microsoft Graph Security), en la comunidad técnica de la API Microsoft Graph Security. 

## Autenticación y autorización en Microsoft Graph

La API Microsoft Graph Security admite dos tipos de autorización (también denominada AuthNZ) y autenticación de aplicaciones:
* **Autorización solo de la aplicación**, donde no hay ningún usuario que haya iniciado sesión (por ejemplo, un SIEM estándar o un escenario de automatización).
En este caso, los permisos o ámbitos que se conceden a la aplicación determinan la autorización
* **Autorización delegada por el usuario**, donde ha iniciado sesión un usuario que es miembro del inquilino de AAD.

Para llamar a la API Microsoft Graph Security, el usuario debe pertenecer al rol de administrador limitado de lector de seguridad de AAD, deben definirse los permisos necesarios (también denominados ámbitos) en el [**registro de la aplicación**](https://go.microsoft.com/fwlink/?linkid=2083908), y la aplicación debe tener los permisos necesarios concedidos por el administrador del inquilino de Azure AD. Este proceso también se describe en [Microsoft Graph Security API Sample for ASP.NET 4.6 (REST)](https://github.com/microsoftgraph/aspnet-security-api-sample) \[Ejemplo de la API Microsoft Graph Security para ASP.NET 4.6 (REST)].

Este ejemplo de la aplicación de autenticación de Graph ofrece más visibilidad sobre los dos tipos de AuthNZ al llamar la API Microsoft Graph Security, ya que en él se muestra el contenido del token de autenticación, así como el contenido y los encabezados de respuesta.
La aplicación tiene una pestaña para la autenticación delegada por el usuario y otra para la autenticación solo para la aplicación.
También tiene una pestaña **Ayuda** donde se muestran errores y correcciones comunes.
La aplicación también le permite escribir la consulta de REST de su elección para poder ver la respuesta. 

## Información necesaria para ejecutar la aplicación

Información que necesitará para ejecutar la aplicación de autenticación de Graph:
![Para ambos tipos de autenticación]:
* **Id. de la aplicación**: del registro de la aplicación (todo lo que necesita para la autenticación delegada por el usuario).
![Para la autenticación solo para la aplicación] (además del Id. de la aplicación)
* **Clave de la aplicación** (también denominada secreto de la aplicación): también del registro de la aplicación
* **Id. del inquilino** (Id. del inquilino de Azure AD): es una propiedad obligatoria de cualquier entidad (respuesta) de la API Microsoft Graph Security.

## Introducción a la aplicación de ejemplo de autenticación de Graph

 1. Descargue o clone el ejemplo de autenticación de Microsoft Graph

 2. Si aún no ha registrado ninguna aplicación, no ha definido los permisos necesarios y no ha concedido explícitamente esos permisos, siga las instrucciones que se indican en [Microsoft Graph Security API Sample for ASP.NET 4.6 (REST)](https://github.com/microsoftgraph/aspnet-security-api-sample) \[Ejemplo de la API Microsoft Graph Security para ASP.NET 4.6 (REST)] para hacerlo. \[Asegúrese de guardar la clave de la aplicación (también denominada secreto de la aplicación) cuando registre la aplicación de ejemplo].

 3. Si está ejecutando el ejemplo de ASP.NET, asegúrese de agregar **aplicación nativa** en la página de registro de la aplicación. Esto es necesario para la aplicación de ejemplo de autenticación de seguridad de Microsoft Graph.
 
 ## Configurar y ejecutar la aplicación de ejemplo
 1. Abra el proyecto Open the Graph\_Security\_API\_Auth\_Sample.
 
 2. Pulse F5 para compilar y ejecutar el ejemplo. Esto restaurará las dependencias de paquetes de NuGet y abrirá la aplicación.

   >Si observa algún error durante la instalación de los paquetes, asegúrese de que la ruta de acceso local donde colocó la solución no es demasiado larga o profunda. Para resolver este problema, mueva la solución más cerca de la raíz de la unidad.

## Usar la aplicación de ejemplo de autenticación de Microsoft Graph

1. Al iniciar la aplicación de ejemplo, se mostrará la interfaz de usuario de la aplicación de ejemplo.

![Interfaz de usuario de la aplicación de ejemplo de autenticación de Graph](readme-images/Default_screen.png)

2. Escriba el Id. de la aplicación en el cuadro de texto de la parte superior de la página.

## Probar la autorización delegada por el usuario

1. Para ejecutar el flujo de autenticación delegada por usuarios, haga clic en el botón **Enviar solicitud**. Se abrirá el cuadro de diálogo de autenticación de Microsoft.

2. Inicie sesión con su cuenta profesional o educativa.

3. En el panel izquierdo de la interfaz de usuario de la aplicación de ejemplo se mostrará el token de autenticación, tal y como puede verse a continuación. 

![Ejemplo de autenticación de Graph: autorización delegada por el usuario](readme-images/User_delegated_auth.png)

* La propiedad **scp** (resaltada) muestra los ámbitos o permisos concedidos al usuario
* La propiedad **wids** muestra los GUID de los grupos de usuarios a los que pertenece el usuario que ha iniciado sesión.

4. La respuesta a la consulta de REST que aparece en el cuadro de texto de la URL de Graph (su valor predeterminado devuelve la alerta principal, es decir, la última). Esta es la respuesta completa JSON que se recibe de la API Microsoft Graph Security. Al hacer clic en la pestaña **Encabezado**de la respuesta se mostrarán los encabezados HTTP de la respuesta.

* Nota: Puede cambiar la consulta de REST que se ha enviado a la API Microsoft Graph Security editando la URL del cuadro de texto **URL de Graph**

## Probar la autorización solo de la aplicación (ningún usuario ha iniciado sesión)

1. Para ejecutar el flujo de autenticación solo de la aplicación, tiene que:

* Escribe la clave de aplicación (o secreto de la aplicación) que se generó al registrar la aplicación.
* Escribir el Id. del inquilino de AAD (puede tomarlo de la propiedad "azureTenantId" en la respuesta del flujo anterior de autorización delegada por usuarios).
* Hacer clic en el botón **Enviar solicitud**. 

2. En el panel izquierdo de la interfaz de usuario de la aplicación de ejemplo se mostrará el token de autenticación solo de la aplicación, tal y como puede verse a continuación. 

![Ejemplo de autenticación de Graph: autorización solo de la aplicación](readme-images/App_only_auth.png)

* En este caso, la propiedad **roles** (resaltada) muestra los ámbitos o permisos concedidos a la aplicación.
* La respuesta JSON a la consulta REST es la misma que en el ejemplo anterior.

## La pestaña Ayuda

La pestaña **Ayuda** contiene algunos errores comunes, el motivo por el que se producen y las formas de solucionarlos (corregirlos). 

![Ejemplo de autenticación de Graph: pestaña Ayuda](readme-images/Help_tab.png)

## Recursos

Documentación:
* [Understanding authorization when calling the Microsoft Graph Security API](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2) (Descripción de la autorización al llamar a la API Microsoft Graph Security)
* [Referencia de permisos de Microsoft Graph](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference)

Otros ejemplos:
* [Microsoft Graph Security API Sample for ASP.NET 4.6 (REST)](https://github.com/microsoftgraph/aspnet-security-api-sample) [Ejemplo de la API Microsoft Graph Security para ASP.NET 4.6 (REST)]
