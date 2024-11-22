# SENSAPHONE VULNERABILITY DISCLOSURE 

## Summary  

In mid-September 2024, I identified several medium-to-low severity security issues in the [Sensaphone Web600 Monitoring System](https://sensaphone.com/products/sensaphone-web600-monitoring-system), including stored cross-site scripting (XSS) vulnerabilities in the system Setup, Profile, and Zone options. Remote authenticated attackers can exploit the flaw to inject arbitrary JavaScript payloads in a variety of elements throughout the Web600 dashboard. The severity of the issues is limited; however, it would allow lower privileged users to steal session tokens from administrative accounts and effectively increase their system access and make unauthorized modifications. The vulnerability was tested on Sensaphone Web600 firmware version v.1.6.5.H. In october, Sensaphone confirmed they were aware of the vulnerabilities. They did not respond to requests for if a patch will be issued and pointed out that the product is recommended to be run on private networks, which reduces the risk of exploitation. 

<img src="https://github.com/user-attachments/assets/b646e476-ba58-4925-a9b1-b66d5adee589" width="200" height="200">


### 1) Stored Cross-Site Scripting (XSS) via Web600 Setup  

The Web600 monitoring system is vulnerable to several stored XSS vulnerabilities through the device setup options. Specifically, remote authenticated attackers and inject arbitrary JavaScript payloads in the System settings in the name, description, and location fields. Attackers can exploit the vulnerability via crafted GET requests to /@.xml, placing payloads in the g7200, g7300, and g7300 parameters which represent name, description, and location respectively. The payloads execute in each section of the Web600 server, such as in the Summary, Setup, Zones, Outputs, Profiles, and History sections. The below proof of concept uses the URL encoded payload of <img src/onerror=alert(1)>.

![poc 1](https://github.com/user-attachments/assets/1323e67f-8550-43f9-aac4-823efc429a1c)

### 2) Stored Cross-Site Scripting (XSS) via Web600 Profiles  

The Web600 monitoring system is vulnerable to a stored XSS vulnerabilities through the device profile options. Specifically, remote authenticated attackers can inject arbitrary JavaScript payloads via crafted GET requests to /@.xml, placing payloads in the g4601 parameter representing the user’s profile name. The payload executes on the Profile page. The below proof of concept uses the URL-encoded payload of <img src/onerror=alert(9)>.  

![poc 2](https://github.com/user-attachments/assets/bf0a4c33-6c86-43bb-ae8c-293132b75bd1)  

### 3) Stored Cross-Site Scripting (XSS) via Web600 Zones  

The Web600 monitoring system is vulnerable to a stored XSS vulnerabilities through the Zone options. Specifically, remote authenticated attackers can inject arbitrary JavaScript payloads via crafted GET requests to /@.xml, placing the payload in the g1F02 parameter representing the Zone name. Payloads will execute on the main summary page and the Zone settings page. The below POC uses the url-encoded payload of <img src/onerror=alert(1)>.

![poc 3](https://github.com/user-attachments/assets/c55420e9-00d4-4f2b-9451-13bda56489fb)
