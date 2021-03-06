<style>
  table th:first-of-type{
  width:200px;}
  </style>

| Term                   | Definition                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Web 2.0 dynamic execution technology | CWS uses a real-world browser sandbox to analyze each webpage, making it easy to cope with various events such as Ajax, Javascript, Render, Reflow, Painting and Event Flow under Web 2.0 and get all links and data sources of the website, which can minimize false positives. |
| Intelligent interaction technology | CWS stays on each webpage loaded into the sandbox for up to 40 seconds during which the program uses an intelligent interaction system to perform various operations such as clicking, dragging layers, moving cursor and filling out forms and tap into each data items on the page to block the entry for any vulnerabilities. |
| Dynamic sandbox and memory monitoring technology | CWS uses the dynamic sandbox and memory monitoring mechanism to easily detect and address malicious code and binary vulnerabilities hidden in webpages. |
| Path execution technology | CWS uses the binary dynamic path execution technology to compile the embedded JavaScript in webpages into binary code and then split it into a tree structure for execution one by one, blocking the entry for any vulnerabilities. |
| Active detection | CWS proactively analyzes the code of application systems of the specific website to speculate about the web backend, hidden paths and sensitive information, acquire pages and detect vulnerabilities based on the characteristics of different web applications and databases. |
| Dynamic sandbox verification | CWS uses dynamic memory sandbox to achieve 100% accuracy when detecting cross-site scripting vulnerabilities (XSS), XML injections and trojans. |
| Online attack verification module | CWS provides an online attack verification module (exploit) for the scanned vulnerabilities which can intuitively demonstrate their various damages. |
| Concurrent connection control technology | Instead of the outdated "concurrent thread control technology" used by many traditional scanners, CWS uses the "concurrent connection control technology" to accurately control the number of concurrent sockets and the traffic transfer speed, limiting the scanning speed to only three requests per second and eliminating the concerns over the risk of downtime. |