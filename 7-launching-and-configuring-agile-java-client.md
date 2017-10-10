# 7 Launching and Configuring Agile Java Client

## 7.1 Agile Java Client Requirements

You must have a Java Runtime Environment \(JRE\) or Java Development Kit \(JDK\) version 8 or later installed on your computer to use Agile Java Client.

The server-side files required for Agile Java Client are installed with the Agile Application Server.

| Note: The Agile PLM administrator must send users the URL to connect to the Agile Java Client. In addition, there is a new Java client access privilege that must be granted for users to use the Java client. |
| :--- |


## 7.2 Installing the Agile Java Client

To use the Agile Java Client, you must have JRE 8.0 installed on your client computer. Agile Java Client uses Java Web Start technology to download the software and keep it updated.

To launch the Agile Java Client:

1. Open your browser and type the following:

   http://&lt;hostname&gt;.&lt;domain&gt;:&lt;port&gt;/JavaClient/start.html

   For example, the URL might look something like this:

   `http://plmserver.mycompany.com/JavaClient/start.html`

2. Click Launch.
   Java Web Start proceeds to download Java Client files and install them on your computer. This may take a few minutes.

3. If a Security Warning dialog box appears, click Start.
4. If the Agile 9.3.4 Desktop Integration dialog box appears, click Yes to integrate the Agile Java Client with your desktop.
   You are prompted to log in to the Agile server.

5. Enter your Agile PLM username and password, and then click OK.
   The main Agile Java Client window opens.

## 7.3 Reconfiguring Java Client JNLP Files

When you install the Agile Application Server, the following three JNLP files are configured for the Agile Java Client. These files are embedded with the application.ear file and deployed with the application:

* pcclient.jnlp

* ext.jnlp

* custom.jnlp

A JNLP file is an XML document that describes a Java application to be launched by Java Web Start. Ordinarily, the JNLP files are configured correctly during installation of Agile PLM. However, if you have an application server cluster and are unable to start Java Client and download its classes, you may need to reconfigure the JNLP files on the Administration server to use the correct URLs.

## 7.4 Modifying the JNLP Files

Agile provides two utilities for unpacking the JNLP files from the application.ear file and repacking them again after you have modified them, ExtractJNLPFiles and RepackJNLPFiles.

To extract and modify the Java Client JNLP files:

1. Stop the Agile Application Server.

2. On the application server machine \(the admin server machine in a WebLogic cluster\), open a command prompt window.

3. Change to the AGILE\_HOME\Install\bin directory and run the ExtractJNLPFiles script to extract the JNLP files from the application.ear file.

   AGILE\_HOME\install\bin\ExtractJNLPFiles

4. Open the pcclient.jnlp file in a text editor. The file is located in the AGILE\_HOME\agileDomain\applications directory.

5. Find the following tags and edit the values listed below:

   jnlp:

   &lt;jnlp spec="1.0+" codebase="http://&lt;proxy/loadbalancer&gt;.&lt;domain&gt;:&lt;port&gt;/JavaClient"&gt;

   serverURL:

   &lt;argument&gt;serverURL=&lt;protocol&gt;://&lt;appserver/loadbalancer&gt;.&lt;domain&gt;:&lt;port&gt;

   webserverName:

   &lt;argument&gt;webserverName=&lt;proxy/loadbalancer&gt;.&lt;domain&gt;:&lt;port&gt;&lt;/argument&gt;

   where

   &lt;protocol&gt; is the protocol used by the application server. Enter t3 for Oracle WebLogic Server

   &lt;proxy/loadbalancer&gt; is the Web proxy server hostname or the alias for the load balancer

   &lt;domain&gt; is the fully qualified domain name

   &lt;port&gt; is the Web proxy server port or virtual port for the load balancer

6. Save the file.

7. Open the ext.jnlp file in a text editor. The file is located in a wls subdirectory beneath the AGILE\_HOME\agileDomain\applications directory.

8. Find the following tag and edit the values listed below:

   jnlp:

   &lt;jnlp spec="1.0+" codebase="http://&lt;proxy/loadbalancer&gt;.&lt;domain&gt;:&lt;port&gt;/JavaClient"&gt;

   where

   &lt;proxy/loadbalancer&gt; is the Web proxy server hostname or the alias for the load balancer

   &lt;domain&gt; is the fully qualified domain name

   &lt;port&gt; is the Web proxy server port or virtual port for the load balancer.

9. Save the file.

10. Open the custom.jnlp file in a text editor. The file is located in the AGILE\_HOME\agileDomain\applications directory.

11. Find the following tag and edit the values listed below:

    jnlp:

    &lt;jnlp spec="1.0+" codebase="http://&lt;proxy/loadbalancer&gt;.&lt;domain&gt;:&lt;port&gt;/JavaClient"&gt;

    where

    &lt;proxy/loadbalancer&gt; is the Web proxy server hostname or the alias for the load balancer

    &lt;domain&gt; is the fully qualified domain name

    &lt;port&gt; is the Web proxy server port or virtual port for the load balancer.

12. Save the file.

13. Change to the AGILE\_HOME\Install\bin directory and run the RepackJNLPFiles script to replace the JNLP files into the application.ear file.

14. Start the Agile Application Server.

## 7.5 Configuring the JNLP MIME Type on UNIX

To successfully download and install application using Java Web Start, you must configure the JNLP MIME type for your server.

Add the following line to the mime.types file in the /oracle\_home/Apache/Apache/conf directory of each application server:

application/x-java-jnlp-file JNLP

