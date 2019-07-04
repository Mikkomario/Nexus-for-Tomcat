NEXUS FOR TOMCAT    -------------------------

Required Libraries
------------------
    - Utopia Flow
    - Utopia Access
    - Utopia Nexus
    - servlet.api.jar (from Tomcat/lib)

Purpose
-------

    Nexus for Tomcat integrates Utopia Nexus so that it can easily be used with Apache Tomcat.


Main Features
-------------

    Conversion from utopia.nexus.http.Response to javax.servlet.http.HttpServletResponse using Response.update(...)
        - Requires importing utopia.nexus.servlet.HttpExtensions._

    Conversion from javax.servlet.http.HttpServletRequest to utopia.nexus.http.Request using HttpServletRequest.toRequest
        - Requires importing utopia.nexus.servlet.HttpExtensions._

    An Echo server implementation (utopia.nexus.test.servlet.EchoServlet.scala) for creating a simple test server


Usage Notes
-----------

    At program startup, please call utopia.flow.generic.DataType.setup()

    In your servlet implementation, import utopia.nexus.servlet.HttpExtensions._

    Create an implicit val of utopia.nexus.http.ServerSettings, then on your doPost(...), doGet(...) etc, call .toRequest
    on the passed HttpServletRequest.

    When you have created a utopia.nexus.http.Response, at the end of doPost(...) etc. call .update(...) on that response.

    If you want to support multipart requests, please add the following annotation over your servlet class definition:
        @MultipartConfig(
                fileSizeThreshold   = 1048576,  // 1 MB
                maxFileSize         = 10485760, // 10 MB
                maxRequestSize      = 20971520, // 20 MB
                location            = "D:/Uploads" // Replace this with your desired file upload directory path
        )


v1.0.1  --------------------------

    Updates & Changes
    -----------------

        Fixed errors caused by latest Nexus, Access and Flow changes.

    Required Libraries
    ------------------
        - Utopia Flow 1.5+
        - Utopia Access 1.1+
        - Utopia Nexus 1.1+
        - servlet.api.jar (from Tomcat/lib)