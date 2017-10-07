---
title: "aaaAzure AD Java web 應用程式使用者入門 |Microsoft 文件"
description: "建置可使用工作或學校帳戶登入使用者的 Java Web 應用程式。"
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 2b92b605-9cd5-4b99-bcbb-66c026558119
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 02/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 20ae95914e074507ed1a23966565ba950cc3a9dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="java-web-app-sign-in-and-sign-out-with-azure-ad"></a>搭配 Azure AD 的 Java Web 應用程式登入和登出
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

藉由提供單一登入和登出只有幾行程式碼，Azure Active Directory (Azure AD) 可簡化您 toooutsource web 應用程式身分識別管理。 您可以登入和移出 Java web 應用程式的使用者使用 Azure Active Directory Authentication Library for Java (ADAL4J) 社群導向的 hello hello Microsoft 實作。

本文將說明如何 toouse hello ADAL4J 至：

* 登入 tooweb hello 身分識別提供者以使用 Azure AD 的應用程式的使用者。
* 顯示部分使用者資訊。
* 登入超出 hello 應用程式的使用者。

## <a name="before-you-get-started"></a>開始之前

* 下載 hello[應用程式的基本架構](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip)，或下載 hello[完成的範例](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip)。
* 您也需要哪些 tooregister hello 應用程式中的 Azure AD 租用戶。 如果您還沒有 Azure AD 租用戶[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

當您準備好時，請遵循 hello hello 九個接下來的各節中的程序。

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>步驟 1： 使用 Azure AD 註冊 hello 新應用程式
tooset tooauthenticate hello 應用程式的使用者，第一次該租用戶中登錄執行 hello 下列：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶名稱。 在 hello**目錄**清單中，選取 hello Active Directory 租用戶想 tooregister hello 應用程式。
3. 按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選取 [新增]。
5. 請遵循 hello 提示 toocreate **Web 應用程式和/或 WebAPI**。
  * **名稱**描述 hello 應用程式 toousers。
  * **登入 URL**是 hello hello 應用程式基底 URL。 hello 基本架構的預設 URL 為 http://localhost:8080/< adal4jsample /。
6. Hello 註冊完成之後，Azure AD 會指派給 hello 應用程式是唯一的應用程式識別碼。 複製 hello 下一節中的 hello 應用程式頁面 toouse hello 值。
7. 從 hello**設定** -> **屬性**應用程式頁面上，更新 hello 應用程式識別碼 URI。 hello**應用程式識別碼 URI**是 hello 應用程式的唯一識別碼。 hello 命名慣例是`https://<tenant-domain>/<app-name>`(例如， `http://localhost:8080/adal4jsample/`)。

當您在 hello 應用程式的 hello 入口網站中，建立並將複製 hello hello 上的應用程式的索引鍵**設定**頁面。 稍後您將需要 hello 索引鍵。

## <a name="step-2-set-up-hello-app-toouse-hello-adal4j-and-prerequisites-by-using-maven"></a>步驟 2： 設定 hello 應用程式 toouse hello ADAL4J 和使用 Maven 的必要條件
在此步驟中，您可以設定 hello ADAL4J toouse hello OpenID Connect 驗證通訊協定。 您使用 hello ADAL4J tooissue 登入和登出要求、 管理使用者工作階段、 取得使用者資訊等等。

Hello 根目錄中您的專案，開啟/建立`pom.xml`，找出`// TODO: provide dependencies for Maven`，並取代為下列 hello:

```Java

    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4jsample</artifactId>
    <packaging>war</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>adal4jsample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.1</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
        <!-- Spring 3 dependencies -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>${spring.version}</version>
        </dependency>
    </dependencies>

    <build>
        <finalName>sample-for-adal4j</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>2.4</version>
                <configuration>
                    <warName>${project.artifactId}</warName>
                    <source>${project.basedir}\src</source>
                    <target>${maven.compiler.target}</target>
                    <encoding>utf-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
        </plugins>
    </build>

    </project>
```

## <a name="step-3-create-hello-java-web-app-files-web-inf"></a>步驟 3： 建立 hello Java web 應用程式檔案 (INF WEB)
在此步驟中，您可以設定 hello Java web 應用程式 toouse hello OpenID Connect 的驗證通訊協定。 使用 hello ADAL4J tooissue 登入和登出要求、 管理 hello 使用者工作階段、 取得 hello 使用者的相關資訊等等。

1. 開啟 hello web.xml 檔案位於 \webapp\WEB-INF\, ，然後輸入 hello XML 中的 hello 應用程式組態值。 hello XML 檔案應該包含下列程式碼的 hello:

    ```xml

    <?xml version="1.0"?>
    <web-app id="WebApp_ID" version="2.4"
        xmlns="http://java.sun.com/xml/ns/j2ee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee
        http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">
        <display-name>Archetype Created Web Application</display-name>
        <context-param>
            <param-name>authority</param-name>
            <param-value>https://login.microsoftonline.com/</param-value>
        </context-param>
        <context-param>
            <param-name>tenant</param-name>
            <param-value>YOUR_TENANT_NAME</param-value>
        </context-param>
        <filter>
            <filter-name>BasicFilter</filter-name>
            <filter-class>com.microsoft.aad.adal4jsample.BasicFilter</filter-class>
            <init-param>
                <param-name>client_id</param-name>
                <param-value>YOUR_CLIENT_ID</param-value>
            </init-param>
            <init-param>
                <param-name>secret_key</param-name>
                <param-value>YOUR_CLIENT_SECRET</param-value>
            </init-param>
        </filter>
        <filter-mapping>
            <filter-name>BasicFilter</filter-name>
            <url-pattern>/secure/*</url-pattern>
        </filter-mapping>
        <servlet>
            <servlet-name>mvc-dispatcher</servlet-name>
            <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
            <load-on-startup>1</load-on-startup>
        </servlet>
        <servlet-mapping>
            <servlet-name>mvc-dispatcher</servlet-name>
            <url-pattern>/</url-pattern>
        </servlet-mapping>
        <context-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/mvc-dispatcher-servlet.xml</param-value>
        </context-param>
        <listener>
            <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
        </listener>
    </web-app>
    ```

 * YOUR_CLIENT_ID 為 hello**應用程式識別碼**指派 tooyour hello 註冊入口網站中的應用程式。
 * YOUR_CLIENT_SECRET 為 hello**應用程式密碼**hello 入口網站中建立。
 * YOUR_TENANT_NAME 為 hello**租用戶名稱**應用程式 (例如 contoso.onmicrosoft.com)。

 您可以看到 hello XML 檔案中，您要撰寫 JavaServer 頁面 (JSP) 或 Java Servlet web 應用程式呼叫 mvc 發送器使用 BasicFilter，每當您瀏覽 hello / 安全 URL。 在 hello 相同程式碼，您使用，/ 安全 hello 受保護的內容和 tooforce 驗證 tooAzure AD 的位置。

2. 建立 hello mvc-發送器-servlet.xml 檔案位於 \webapp\WEB-INF\,並輸入下列程式碼的 hello:

    ```xml

    <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:context="http://www.springframework.org/schema/context"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="
            http://www.springframework.org/schema/beans     
            http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context-3.0.xsd">
        <context:component-scan base-package="com.microsoft.aad.adal4jsample" />
        <bean
            class="org.springframework.web.servlet.view.InternalResourceViewResolver">
            <property name="prefix">
                <value>/</value>
            </property>
            <property name="suffix">
                <value>.jsp</value>
            </property>
        </bean>
    </beans>
    ```

 這段程式碼會告知 hello web 應用程式 toouse Spring，它會指出 toofind hello JSP 檔案，您撰寫 hello 下一節中的位置。

## <a name="step-4-create-hello-jsp-view-files-for-basicfilter-mvc"></a>步驟 4： 建立 hello JSP 檢視檔案 （適用於 BasicFilter MVC)
您已經到達在 WEB-INF 中設定 Web 應用程式的一半。 接下來，您建立 hello BasicFilter 模型檢視控制器 (MVC)、 哪些 hello web 應用程式執行的 JSP 檔案。 我們在 hello 組態期間建立 hello 檔案有所提示。

較舊版本，才能識別 Java hello 中您擁有的 XML 組態檔`/`載入 JSP 檔案與您的資源有`/secure`通過篩選器，您可以呼叫 BasicFilter 的資源。

toocreate hello JSP 檔案，請勿 hello 遵循：

1. 建立 hello index.jsp 檔案 (位於 \webapp\)，然後貼上 hello 遵循程式碼：

    ```jsp
    <html>
    <body>
        <h2>Hello World!</h2>
        <ul>
        <li><a href="secure/aad">Secure Page</a></li>
        </ul>
    </body>
    </html>
    ```

 此程式碼只會重新導向 tooa 安全網頁 hello 篩選受保護。

2. 在 hello 相同的目錄中建立 error.jsp 檔案 toocatch，可能會發生任何錯誤：

    ```jsp

    <html>
    <body>
        <h2>ERROR PAGE!</h2>
        <p>
            Exception -
            <%=request.getAttribute("error")%></p>
        <ul>
            <li><a href="<%=request.getContextPath()%>/index.jsp">Go Home</a></li>
        </ul>
    </body>
    </html>
    ```
3. 安全網頁的 toomake 底下建立資料夾稱為 \secure hello 目錄現在是 \webapp\secure \webapp。
4. 在 hello \webapp\secure 目錄中，建立 aad.jsp 檔案，然後再貼上下列程式碼的 hello:

    ```jsp

    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
        <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>AAD Secure Page</title>
        </head>
        <body>

        <h1>Directory - Users List</h1>
        <p>${users}</p>
        <ul>
            <li><a href="<%=request.getContextPath()%>/secure/aad?cc=1">Get new Access Token via Client Credentials</a></li>
        </ul>
        <ul>
            <li><a href="<%=request.getContextPath()%>/secure/aad?refresh=1">Get new Access Token via Refresh Token</a></li>
        </ul>
        <ul>
            <li><a href="<%=request.getContextPath()%>/index.jsp">Go Home</a></li>
        </ul>
        </body>
    </html>
    ```

    此頁面會重新導向 toospecific 要求，哪些 hello BasicFilter servlet 讀取，並接著使用 hello ADAJ4J 上執行。

您現在需要 tooset hello Java 檔案，供 hello servlet 執行其工作。

## <a name="step-5-create-some-java-helper-files-for-basicfilter-mvc"></a>步驟 5：建立一些 Java 協助程式檔案 (適用於 BasicFilter MVC)
我們在此步驟中的目標是 toocreate Java 的檔案：

* 允許登入和登出的 hello 使用者。
* 收到 hello 使用者有關的一些資料。

    > [!NOTE]
    > 關於 hello 使用者 tooget 資料使用 hello 從 Azure AD Graph API。 hello Graph API 是安全的 web 服務，可讓您 toograb 資料有關您的組織，包括個別使用者。 這種方法優於在權杖中預先填入機密資料，因為它可確保︰
    > * hello 使用者要求 hello 資料已獲授權。
    > * 可能會發生 toograb hello 語彙基元 （從已進行 jb 破解電話或網頁瀏覽器快取在桌面上，例如） 的人無法取得 hello 使用者或 hello 組織相關的重要詳細資料。

toowrite 某些 Java 檔案這項工作：

1. 建立資料夾根目錄中的目錄稱為 adal4jsample toostore hello Java 的所有檔案。

    在此範例中，您使用 hello 命名空間 com.microsoft.aad.adal4jsample hello Java 檔案中。 大部分 IDE 會針對此目的建立巢狀資料夾結構 (例如，/com/microsoft/aad/adal4jsample)。 您也可以這麼做，但並非必要。

2. 在這個資料夾中，建立一個稱為 JSONHelper.java，您將使用此檔案 toohelp 剖析 hello JSON 資料，從您的語彙基元。 下列程式碼貼上 hello toocreate hello 檔案：

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.lang.reflect.Field;
    import java.util.Arrays;
    import java.util.Enumeration;
    import java.util.List;

    import javax.servlet.http.HttpServletRequest;

    import org.apache.commons.lang3.text.WordUtils;
    import org.apache.log4j.Logger;
    import org.json.JSONArray;
    import org.json.JSONException;
    import org.json.JSONObject;

    /**
     * This class provides hello methods tooparse JSON data from a JSON-formatted
     * string.
     *
     * @author Azure Active Directory contributor
     *
     */
    public class JSONHelper {

        private static Logger logger = Logger.getLogger(JSONHelper.class);

        JSONHelper() {
            // PropertyConfigurator.configure("log4j.properties");
        }

        /**
         * This method parses a JSON array out of a collection of JSON objects
         * within a string.
         *
         * @param jSonData
         *            hello JSON string that holds hello collection
         * @return A JSON array that contains all hello collection objects
         * @throws Exception
         */
        public static JSONArray fetchDirectoryObjectJSONArray(JSONObject jsonObject) throws Exception {
            JSONArray jsonArray = new JSONArray();
            jsonArray = jsonObject.optJSONObject("responseMsg").optJSONArray("value");
            return jsonArray;
        }

        /**
         * This method parses a JSON object out of a collection of JSON objects
         * within a string.
         *
         * @param jsonObject
         * @return A JSON object that contains hello DirectoryObject
         * @throws Exception
         */
        public static JSONObject fetchDirectoryObjectJSONObject(JSONObject jsonObject) throws Exception {
            JSONObject jObj = new JSONObject();
            jObj = jsonObject.optJSONObject("responseMsg");
            return jObj;
        }

        /**
         * This method parses hello skip token from a JSON-formatted string.
         *
         * @param jsonData
         *            hello JSON-formatted string
         * @return hello skipToken
         * @throws Exception
         */
        public static String fetchNextSkiptoken(JSONObject jsonObject) throws Exception {
            String skipToken = "";
            // Parse hello skip token out of hello string.
            skipToken = jsonObject.optJSONObject("responseMsg").optString("odata.nextLink");

            if (!skipToken.equalsIgnoreCase("")) {
                // Remove hello unnecessary prefix from hello skip token.
                int index = skipToken.indexOf("$skiptoken=") + (new String("$skiptoken=")).length();
                skipToken = skipToken.substring(index);
            }
            return skipToken;
        }

        /**
         * @param jsonObject
         * @return
         * @throws Exception
         */
        public static String fetchDeltaLink(JSONObject jsonObject) throws Exception {
            String deltaLink = "";
            // Parse hello skip token out of hello string.
            deltaLink = jsonObject.optJSONObject("responseMsg").optString("aad.deltaLink");
            if (deltaLink == null || deltaLink.length() == 0) {
                deltaLink = jsonObject.optJSONObject("responseMsg").optString("aad.nextLink");
                logger.info("deltaLink empty, nextLink ->" + deltaLink);

            }
            if (!deltaLink.equalsIgnoreCase("")) {
                // Remove hello unnecessary prefix from hello skip token.
                int index = deltaLink.indexOf("deltaLink=") + (new String("deltaLink=")).length();
                deltaLink = deltaLink.substring(index);
            }
            return deltaLink;
        }

        /**
         * This method creates a string consisting of a JSON document with all
         * hello necessary elements set from hello HttpServletRequest request.
         *
         * @param request
         *            hello HttpServletRequest
         * @return hello string containing hello JSON document
         * @throws Exception
         *             If there is any error processing hello request.
         */
        public static String createJSONString(HttpServletRequest request, String controller) throws Exception {
            JSONObject obj = new JSONObject();
            try {
                Field[] allFields = Class.forName(
                        "com.microsoft.windowsazure.activedirectory.sdk.graph.models." + controller).getDeclaredFields();
                String[] allFieldStr = new String[allFields.length];
                for (int i = 0; i < allFields.length; i++) {
                    allFieldStr[i] = allFields[i].getName();
                }
                List<String> allFieldStringList = Arrays.asList(allFieldStr);
                Enumeration<String> fields = request.getParameterNames();

                while (fields.hasMoreElements()) {

                    String fieldName = fields.nextElement();
                    String param = request.getParameter(fieldName);
                    if (allFieldStringList.contains(fieldName)) {
                        if (param == null || param.length() == 0) {
                            if (!fieldName.equalsIgnoreCase("password")) {
                                obj.put(fieldName, JSONObject.NULL);
                            }
                        } else {
                            if (fieldName.equalsIgnoreCase("password")) {
                                obj.put("passwordProfile", new JSONObject("{\"password\": \"" + param + "\"}"));
                            } else {
                                obj.put(fieldName, param);
                            }
                        }
                    }
                }
            } catch (JSONException e) {
                e.printStackTrace();
            } catch (SecurityException e) {
                e.printStackTrace();
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            }            
            return obj.toString();
        }

        /**
         *
         * @param key
         * @param value
         * @return string format of this JSON object
         * @throws Exception
         */
        public static String createJSONString(String key, String value) throws Exception {

            JSONObject obj = new JSONObject();
            try {
                obj.put(key, value);
            } catch (JSONException e) {
                e.printStackTrace();
            }

            return obj.toString();
        }

        /**
         * This is a generic method that copies hello simple attribute values from an
         * argument jsonObject tooan argument generic object.
         *
         * @param jsonObject
         *            hello jsonObject from where hello attributes are toobe copied.
         * @param destObject
         *            hello object where hello attributes should be copied to.
         * @throws Exception
         *             Throws an Exception when hello operation is unsuccessful.
         */
        public static <T> void convertJSONObjectToDirectoryObject(JSONObject jsonObject, T destObject) throws Exception {

            // Get hello list of all hello field names.
            Field[] fieldList = destObject.getClass().getDeclaredFields();

            // For all hello declared field.
            for (int i = 0; i < fieldList.length; i++) {
                // If hello field is of type String, that is
                // if it is a simple attribute.
                if (fieldList[i].getType().equals(String.class)) {
                    // Invoke hello corresponding set method of hello destObject using
                    // hello argument taken from hello jsonObject.
                    destObject
                            .getClass()
                            .getMethod(String.format("set%s", WordUtils.capitalize(fieldList[i].getName())),
                                    new Class[] { String.class })
                            .invoke(destObject, new Object[] { jsonObject.optString(fieldList[i].getName()) });
                }
            }
        }

        public static JSONArray joinJSONArrays(JSONArray a, JSONArray b) {
            JSONArray comb = new JSONArray();
            for (int i = 0; i < a.length(); i++) {
                comb.put(a.optJSONObject(i));
            }
            for (int i = 0; i < b.length(); i++) {
                comb.put(b.optJSONObject(i));
            }
            return comb;
        }

    }

    ```

3. 建立一個叫做 HttpClientHelper.java，您可以將檔案 toohelp 剖析 hello 向 Azure AD 端點的 HTTP 資料。 下列程式碼貼上 hello toocreate hello 檔案：

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.io.BufferedReader;
    import java.io.ByteArrayOutputStream;
    import java.io.IOException;
    import java.io.InputStream;
    import java.io.InputStreamReader;
    import java.io.OutputStreamWriter;
    import java.net.HttpURLConnection;

    import org.json.JSONException;
    import org.json.JSONObject;

    /**
     * This is Helper class for all RestClient class.
     *
     * @author Azure Active Directory Contributor
     *
     */
    public class HttpClientHelper {

        public HttpClientHelper() {
            super();
        }

        public static String getResponseStringFromConn(HttpURLConnection conn, boolean isSuccess) throws IOException {

            BufferedReader reader = null;
            if (isSuccess) {
                reader = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            } else {
                reader = new BufferedReader(new InputStreamReader(conn.getErrorStream()));
            }
            StringBuffer stringBuffer = new StringBuffer();
            String line = "";
            while ((line = reader.readLine()) != null) {
                stringBuffer.append(line);
            }

            return stringBuffer.toString();
        }

        public static String getResponseStringFromConn(HttpURLConnection conn, String payLoad) throws IOException {

            // Send hello http message payload toohello server.
            if (payLoad != null) {
                conn.setDoOutput(true);
                OutputStreamWriter osw = new OutputStreamWriter(conn.getOutputStream());
                osw.write(payLoad);
                osw.flush();
                osw.close();
            }

            // Get hello message response from hello server.
            BufferedReader br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            String line = "";
            StringBuffer stringBuffer = new StringBuffer();
            while ((line = br.readLine()) != null) {
                stringBuffer.append(line);
            }

            br.close();

            return stringBuffer.toString();
        }

        public static byte[] getByteaArrayFromConn(HttpURLConnection conn, boolean isSuccess) throws IOException {

            InputStream is = conn.getInputStream();
            ByteArrayOutputStream baos = new ByteArrayOutputStream();
            byte[] buff = new byte[1024];
            int bytesRead = 0;

            while ((bytesRead = is.read(buff, 0, buff.length)) != -1) {
                baos.write(buff, 0, bytesRead);
            }

            byte[] bytes = baos.toByteArray();
            baos.close();
            return bytes;
        }

        /**
         * for bad response, whose responseCode is not 200 level
         *
         * @param responseCode
         * @param errorCode
         * @param errorMsg
         * @return
         * @throws JSONException
         */
        public static JSONObject processResponse(int responseCode, String errorCode, String errorMsg) throws JSONException {
            JSONObject response = new JSONObject();
            response.put("responseCode", responseCode);
            response.put("errorCode", errorCode);
            response.put("errorMsg", errorMsg);

            return response;
        }

        /**
         * for bad response, whose responseCode is not 200 level
         *
         * @param responseCode
         * @param errorCode
         * @param errorMsg
         * @return
         * @throws JSONException
         */
        public static JSONObject processGoodRespStr(int responseCode, String goodRespStr) throws JSONException {
            JSONObject response = new JSONObject();
            response.put("responseCode", responseCode);
            if (goodRespStr.equalsIgnoreCase("")) {
                response.put("responseMsg", "");
            } else {
                response.put("responseMsg", new JSONObject(goodRespStr));
            }

            return response;
        }

        /**
         * for good response
         *
         * @param responseCode
         * @param responseMsg
         * @return
         * @throws JSONException
         */
        public static JSONObject processBadRespStr(int responseCode, String responseMsg) throws JSONException {

            JSONObject response = new JSONObject();
            response.put("responseCode", responseCode);
            if (responseMsg.equalsIgnoreCase("")) { // good response is empty string
                response.put("responseMsg", "");
            } else { // bad response is json string
                JSONObject errorObject = new JSONObject(responseMsg).optJSONObject("odata.error");

                String errorCode = errorObject.optString("code");
                String errorMsg = errorObject.optJSONObject("message").optString("value");
                response.put("responseCode", responseCode);
                response.put("errorCode", errorCode);
                response.put("errorMsg", errorMsg);
            }

            return response;
        }

    }

    ```

## <a name="step-6-create-hello-java-graph-api-model-files-for-basicfilter-mvc"></a>步驟 6： 建立 hello Java Graph API 模型檔案 （適用於 BasicFilter MVC)
如前所述，您會使用 hello Graph API tooget hello 登入的使用者資料。 此程序會很容易，toomake 建立這兩個檔案 toorepresent 目錄物件和檔案 toorepresent hello 的使用者，所以可使用的 Java hello OO 模式。

1. 建立一個叫做 DirectoryObject.java，您使用檔案 toostore 任何目錄物件的相關基本的資料。 稍後您可以對想要執行的任何其他圖形使用這個檔案。 下列程式碼貼上 hello toocreate hello 檔案：

    ```Java

    package com.microsoft.aad.adal4jsample;

    /**
     * @author Azure Active Directory Contributor
     *
     */
    public abstract class DirectoryObject {

        public DirectoryObject() {
            super();
        }

        /**
         *
         * @return
         */
        public abstract String getObjectId();

        /**
         * @param objectId
         */
        public abstract void setObjectId(String objectId);

        /**
         *
         * @return
         */
        public abstract String getObjectType();

        /**
         *
         * @param objectType
         */
        public abstract void setObjectType(String objectType);

        /**
         *
         * @return
         */
        public abstract String getDisplayName();

        /**
         *
         * @param displayName
         */
        public abstract void setDisplayName(String displayName);

    }

    ```

2. 建立一個叫做 User.java，您使用檔案 toostore hello 目錄的任何使用者有關的基本資料。 這些是基本的 getter 和 setter 方法來目錄資料，讓您可以貼上下列程式碼的 hello:

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.security.acl.Group;
    import java.util.ArrayList;

    import javax.xml.bind.annotation.XmlRootElement;

    import org.json.JSONObject;

    /**
    *  hello **User** class holds together all hello members of a WAAD User entity and all hello access methods and set methods.
    *  @author Azure Active Directory Contributor
    */
    @XmlRootElement
    public class User extends DirectoryObject{

        // hello following are hello individual private members of a User object that holds
        // a particular simple attribute of a User object.
        protected String objectId;
        protected String objectType;
        protected String accountEnabled;
        protected String city;
        protected String country;
        protected String department;
        protected String dirSyncEnabled;
        protected String displayName;
        protected String facsimileTelephoneNumber;
        protected String givenName;
        protected String jobTitle;
        protected String lastDirSyncTime;
        protected String mail;
        protected String mailNickname;
        protected String mobile;
        protected String password;
        protected String passwordPolicies;
        protected String physicalDeliveryOfficeName;
        protected String postalCode;
        protected String preferredLanguage;
        protected String state;
        protected String streetAddress;
        protected String surname;
        protected String telephoneNumber;
        protected String usageLocation;
        protected String userPrincipalName;
        protected boolean isDeleted;  // this will move toodto

        /**
         * These four properties are for future use.
         */
        // managerDisplayname of this user.
        protected String managerDisplayname;

        // hello directReports holds a list of directReports.
        private ArrayList<User> directReports;

        // hello groups holds a list of group entities this user belongs to.
        private ArrayList<Group> groups;

        // hello roles holds a list of role entities this user belongs to.
        private ArrayList<Group> roles;

        /**
         * hello constructor for hello **User** class. Initializes hello dynamic lists and managerDisplayname variables.
         */
        public User(){
            directReports = null;
            groups = new ArrayList<Group>();
            roles = new ArrayList<Group>();
            managerDisplayname = null;
        }
    //    
    //    public User(String displayName, String objectId){
    //        setDisplayName(displayName);
    //        setObjectId(objectId);
    //    }
    //    
    //    public User(String displayName, String objectId, String userPrincipalName, String accountEnabled){
    //        setDisplayName(displayName);
    //        setObjectId(objectId);
    //        setUserPrincipalName(userPrincipalName);
    //        setAccountEnabled(accountEnabled);
    //    }
    //    

        /**
         * @return hello objectId of this user.
         */
        public String getObjectId() {
            return objectId;
        }

        /**
         * @param objectId hello objectId tooset toothis User object.
         */
        public void setObjectId(String objectId) {
            this.objectId = objectId;
        }

        /**
         * @return hello objectType of this user.
         */
        public String getObjectType() {
            return objectType;
        }

        /**
         * @param objectType hello objectType tooset toothis User object.
         */
        public void setObjectType(String objectType) {
            this.objectType = objectType;
        }

        /**
         * @return hello userPrincipalName of this user.
         */
        public String getUserPrincipalName() {
            return userPrincipalName;
        }

        /**
         * @param userPrincipalName hello userPrincipalName tooset toothis User object.
         */
        public void setUserPrincipalName(String userPrincipalName) {
            this.userPrincipalName = userPrincipalName;
        }

        /**
         * @return hello usageLocation of this user.
         */
        public String getUsageLocation() {
            return usageLocation;
        }

        /**
         * @param usageLocation hello usageLocation tooset toothis User object.
         */
        public void setUsageLocation(String usageLocation) {
            this.usageLocation = usageLocation;
        }

        /**
         * @return hello telephoneNumber of this user.
         */
        public String getTelephoneNumber() {
            return telephoneNumber;
        }

        /**
         * @param telephoneNumber hello telephoneNumber tooset toothis User object.
         */
        public void setTelephoneNumber(String telephoneNumber) {
            this.telephoneNumber = telephoneNumber;
        }

        /**
         * @return hello surname of this user.
         */
        public String getSurname() {
            return surname;
        }

        /**
         * @param surname hello surname tooset toothis User object.
         */
        public void setSurname(String surname) {
            this.surname = surname;
        }

        /**
         * @return hello streetAddress of this user.
         */
        public String getStreetAddress() {
            return streetAddress;
        }

        /**
         * @param streetAddress hello streetAddress tooset toothis user.
         */
        public void setStreetAddress(String streetAddress) {
            this.streetAddress = streetAddress;
        }

        /**
         * @return hello state of this user.
         */
        public String getState() {
            return state;
        }

        /**
         * @param state hello state tooset toothis User object.
         */
        public void setState(String state) {
            this.state = state;
        }

        /**
         * @return hello preferredLanguage of this user.
         */
        public String getPreferredLanguage() {
            return preferredLanguage;
        }

        /**
         * @param preferredLanguage hello preferredLanguage tooset toothis user.
         */
        public void setPreferredLanguage(String preferredLanguage) {
            this.preferredLanguage = preferredLanguage;
        }

        /**
         * @return hello postalCode of this user.
         */
        public String getPostalCode() {
            return postalCode;
        }

        /**
         * @param postalCode hello postalCode tooset toothis user.
         */
        public void setPostalCode(String postalCode) {
            this.postalCode = postalCode;
        }

        /**
         * @return hello physicalDeliveryOfficeName of this user.
         */
        public String getPhysicalDeliveryOfficeName() {
            return physicalDeliveryOfficeName;
        }

        /**
         * @param physicalDeliveryOfficeName hello physicalDeliveryOfficeName tooset toothis User object.
         */
        public void setPhysicalDeliveryOfficeName(String physicalDeliveryOfficeName) {
            this.physicalDeliveryOfficeName = physicalDeliveryOfficeName;
        }

        /**
         * @return hello passwordPolicies of this user.
         */
        public String getPasswordPolicies() {
            return passwordPolicies;
        }

        /**
         * @param passwordPolicies hello passwordPolicies tooset toothis User object.
         */
        public void setPasswordPolicies(String passwordPolicies) {
            this.passwordPolicies = passwordPolicies;
        }

        /**
         * @return hello mobile of this user.
         */
        public String getMobile() {
            return mobile;
        }

        /**
         * @param mobile hello mobile tooset toothis User object.
         */
        public void setMobile(String mobile) {
            this.mobile = mobile;
        }

        /**
         * @return hello password of this user.
         */
        public String getPassword() {
            return password;
        }

        /**
         * @param password hello mobile tooset toothis User object.
         */
        public void setPassword(String password) {
            this.password = password;
        }

        /**
         * @return hello mail of this user.
         */
        public String getMail() {
            return mail;
        }

        /**
         * @param mail hello mail tooset toothis User object.
         */
        public void setMail(String mail) {
            this.mail = mail;
        }

        /**
         * @return hello MailNickname of this user.
         */
        public String getMailNickname() {
            return mailNickname;
        }

        /**
         * @param mail hello MailNickname tooset toothis User object.
         */
        public void setMailNickname(String mailNickname) {
            this.mailNickname = mailNickname;
        }

        /**
         * @return hello jobTitle of this user.
         */
        public String getJobTitle() {
            return jobTitle;
        }

        /**
         * @param jobTitle hello jobTitle tooset toothis User object.
         */
        public void setJobTitle(String jobTitle) {
            this.jobTitle = jobTitle;
        }

        /**
         * @return hello givenName of this user.
         */
        public String getGivenName() {
            return givenName;
        }

        /**
         * @param givenName hello givenName tooset toothis User object.
         */
        public void setGivenName(String givenName) {
            this.givenName = givenName;
        }

        /**
         * @return hello facsimileTelephoneNumber of this user.
         */
        public String getFacsimileTelephoneNumber() {
            return facsimileTelephoneNumber;
        }

        /**
         * @param facsimileTelephoneNumber hello facsimileTelephoneNumber tooset toothis User object.
         */
        public void setFacsimileTelephoneNumber(String facsimileTelephoneNumber) {
            this.facsimileTelephoneNumber = facsimileTelephoneNumber;
        }

        /**
         * @return hello displayName of this user.
         */
        public String getDisplayName() {
            return displayName;
        }

        /**
         * @param displayName hello displayName tooset toothis User object.
         */
        public void setDisplayName(String displayName) {
            this.displayName = displayName;
        }

        /**
         * @return hello dirSyncEnabled of this user.
         */
        public String getDirSyncEnabled() {
            return dirSyncEnabled;
        }

        /**
         * @param dirSyncEnabled hello dirSyncEnabled tooset toothis User object.
         */
        public void setDirSyncEnabled(String dirSyncEnabled) {
            this.dirSyncEnabled = dirSyncEnabled;
        }

        /**
         * @return hello department of this user.
         */
        public String getDepartment() {
            return department;
        }

        /**
         * @param department hello department tooset toothis User object.
         */
        public void setDepartment(String department) {
            this.department = department;
        }

        /**
         * @return hello lastDirSyncTime of this user.
         */
        public String getLastDirSyncTime() {
            return lastDirSyncTime;
        }

        /**
         * @param lastDirSyncTime hello lastDirSyncTime tooset toothis User object.
         */
        public void setLastDirSyncTime(String lastDirSyncTime) {
            this.lastDirSyncTime = lastDirSyncTime;
        }

        /**
         * @return hello country of this user.
         */
        public String getCountry() {
            return country;
        }

        /**
         * @param country hello country tooset toothis user.
         */
        public void setCountry(String country) {
            this.country = country;
        }

        /**
         * @return hello city of this user.
         */
        public String getCity() {
            return city;
        }

        /**
         * @param city hello city tooset toothis user.
         */
        public void setCity(String city) {
            this.city = city;
        }

        /**
         * @return hello accountEnabled attribute of this user.
         */
        public String getAccountEnabled() {
            return accountEnabled;
        }

        /**
         * @param accountEnabled hello accountEnabled tooset toothis user.
         */
        public void setAccountEnabled(String accountEnabled) {
            this.accountEnabled = accountEnabled;
        }

        public boolean isIsDeleted() {
            return this.isDeleted;
        }

        public void setIsDeleted(boolean isDeleted) {
            this.isDeleted = isDeleted;
        }

        @Override
        public String toString() {
            return new JSONObject(this).toString();
        }

        public String getManagerDisplayname(){
            return managerDisplayname;
        }

        public void setManagerDisplayname(String managerDisplayname){
            this.managerDisplayname = managerDisplayname;
        }
    }

    /**
    * hello DirectReports class holds hello essential data for a single DirectReport entry. That is,
    * it holds hello displayName and hello objectId of hello direct entry. It also provides the
    * access methods tooset or get hello displayName and hello ObjectId of this entry.
    */
    //class DirectReport extends User{
    //
    //    private String displayName;
    //    private String objectId;
    //     
    //    /**
    //     * Two arguments Constructor for hello DirectReport class.
    //     * @param displayName
    //     * @param objectId
    //     */
    //    public DirectReport(String displayName, String objectId){
    //        this.displayName = displayName;
    //        this.objectId = objectId;
    //    }
    //
    //    /**
    //     * @return hello displayName of this direct report entry.
    //     */
    //    public String getDisplayName() {
    //        return displayName;
    //    }
    //
    //    
    //    /**
    //     *  @return hello objectId of this direct report entry.
    //     */
    //    public String getObjectId() {
    //        return objectId;
    //    }
    //
    //}

    ```

## <a name="step-7-create-hello-authentication-model-and-controller-files-for-basicfilter"></a>步驟 7： 建立 hello 驗證模型和控制器檔案 （適用於 BasicFilter)
我們了解 Java 可能會非常繁複，但是您就快要完成了。 您撰寫 hello BasicFilter servlet toohandle hello 要求之前，您會需要某些更多的協助程式檔案需要 ADAL4J 該 hello toowrite。

1. 建立一個叫做 AuthHelper.java，這樣會提供您方法 toouse toodetermine hello hello 登入的使用者狀態檔案。 hello 方法包括：

 * **isAuthenticated()**： 傳回 hello 使用者是否登入。
 * **containsAuthenticationData()**： 傳回 hello 權杖是否具有資料。
 * **isAuthenticationSuccessful()**： 傳回 hello 驗證是否成功 hello 使用者。

 toocreate hello AuthHelper.java 檔案中，貼上下列程式碼的 hello:

    ```Java
    package com.microsoft.aad.adal4jsample;

    import java.util.Map;

    import javax.servlet.http.HttpServletRequest;

    import com.microsoft.aad.adal4j.AuthenticationResult;
    import com.nimbusds.openid.connect.sdk.AuthenticationResponse;
    import com.nimbusds.openid.connect.sdk.AuthenticationResponseParser;
    import com.nimbusds.openid.connect.sdk.AuthenticationSuccessResponse;

    public final class AuthHelper {

        public static final String PRINCIPAL_SESSION_NAME = "principal";

        private AuthHelper() {
        }

        public static boolean isAuthenticated(HttpServletRequest request) {
            return request.getSession().getAttribute(PRINCIPAL_SESSION_NAME) != null;
        }

        public static AuthenticationResult getAuthSessionObject(
                HttpServletRequest request) {
            return (AuthenticationResult) request.getSession().getAttribute(
                    PRINCIPAL_SESSION_NAME);
        }

        public static boolean containsAuthenticationData(
                HttpServletRequest httpRequest) {
            Map<String, String[]> map = httpRequest.getParameterMap();
            return httpRequest.getMethod().equalsIgnoreCase("POST") && (httpRequest.getParameterMap().containsKey(
                            AuthParameterNames.ERROR)
                            || httpRequest.getParameterMap().containsKey(
                                    AuthParameterNames.ID_TOKEN) || httpRequest
                            .getParameterMap().containsKey(AuthParameterNames.CODE));
        }

        public static boolean isAuthenticationSuccessful(
                AuthenticationResponse authResponse) {
            return authResponse instanceof AuthenticationSuccessResponse;
        }
    }
    ```

2. 建立檔案，稱為 AuthParameterNames.java，它將提供一些不可變的變數 ADAL4J 需要該 hello。 下列程式碼貼上 hello toocreate hello 檔案：

    ```Java
    package com.microsoft.aad.adal4jsample;

    public final class AuthParameterNames {

        private AuthParameterNames() {
        }

        public static String ERROR = "error";
        public static String ERROR_DESCRIPTION = "error_description";
        public static String ERROR_URI = "error_uri";
        public static String ID_TOKEN = "id_token";
        public static String CODE = "code";
    }
    ```

3. 建立一個叫做 AadController.java，也就是 hello controller，MVC 模式的檔案。 hello 檔案可讓您 hello JSP 控制器和公開 hello aad 安全 URL 端點的 hello 應用程式。 hello 檔也包含 hello graph 查詢。 下列程式碼貼上 hello toocreate hello 檔案：

    ```Java
    package com.microsoft.aad.adal4jsample;

    import java.net.HttpURLConnection;
    import java.net.URL;

    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpSession;

    import org.json.JSONArray;
    import org.json.JSONObject;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.ModelMap;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;

    import com.microsoft.aad.adal4j.AuthenticationResult;

    @Controller
    @RequestMapping("/secure/aad")
    public class AadController {

        @RequestMapping(method = { RequestMethod.GET, RequestMethod.POST })
        public String getDirectoryObjects(ModelMap model, HttpServletRequest httpRequest) {
            HttpSession session = httpRequest.getSession();
            AuthenticationResult result = (AuthenticationResult) session.getAttribute(AuthHelper.PRINCIPAL_SESSION_NAME);
            if (result == null) {
                model.addAttribute("error", new Exception("AuthenticationResult not found in session."));
                return "/error";
            } else {
                String data;
                try {
                    data = this.getUsernamesFromGraph(result.getAccessToken(), session.getServletContext()
                            .getInitParameter("tenant"));
                    model.addAttribute("users", data);
                } catch (Exception e) {
                    model.addAttribute("error", e);
                    return "/error";
                }
            }
            return "/secure/aad";
        }

        private String getUsernamesFromGraph(String accessToken, String tenant) throws Exception {
            URL url = new URL(String.format("https://graph.windows.net/%s/users?api-version=2013-04-05", tenant,
                    accessToken));

            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            // Set hello appropriate header fields in hello request header.
            conn.setRequestProperty("api-version", "2013-04-05");
            conn.setRequestProperty("Authorization", accessToken);
            conn.setRequestProperty("Accept", "application/json;odata=minimalmetadata");
            String goodRespStr = HttpClientHelper.getResponseStringFromConn(conn, true);
            // logger.info("goodRespStr ->" + goodRespStr);
            int responseCode = conn.getResponseCode();
            JSONObject response = HttpClientHelper.processGoodRespStr(responseCode, goodRespStr);
            JSONArray users = new JSONArray();

            users = JSONHelper.fetchDirectoryObjectJSONArray(response);

            StringBuilder builder = new StringBuilder();
            User user = null;
            for (int i = 0; i < users.length(); i++) {
                JSONObject thisUserJSONObject = users.optJSONObject(i);
                user = new User();
                JSONHelper.convertJSONObjectToDirectoryObject(thisUserJSONObject, user);
                builder.append(user.getUserPrincipalName() + "<br/>");
            }
            return builder.toString();
        }

    }

    ```

## <a name="step-8-create-hello-basicfilter-file-for-basicfilter-mvc"></a>步驟 8： 建立 hello BasicFilter 檔案 （適用於 BasicFilter MVC)
您現在可以建立 hello BasicFilter.java 檔案，用來處理 hello 源自 hello JSP 檢視檔案。 下列程式碼貼上 hello toocreate hello 檔案：

```Java

package com.microsoft.aad.adal4jsample;

import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.net.URI;
import java.net.URLEncoder;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.UUID;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;
import com.nimbusds.oauth2.sdk.AuthorizationCode;
import com.nimbusds.openid.connect.sdk.AuthenticationErrorResponse;
import com.nimbusds.openid.connect.sdk.AuthenticationResponse;
import com.nimbusds.openid.connect.sdk.AuthenticationResponseParser;
import com.nimbusds.openid.connect.sdk.AuthenticationSuccessResponse;

public class BasicFilter implements Filter {

    private String clientId = "";
    private String clientSecret = "";
    private String tenant = "";
    private String authority;

    public void destroy() {

    }

    public void doFilter(ServletRequest request, ServletResponse response,
            FilterChain chain) throws IOException, ServletException {

        if (request instanceof HttpServletRequest) {
            HttpServletRequest httpRequest = (HttpServletRequest) request;
            HttpServletResponse httpResponse = (HttpServletResponse) response;
            try {

                String currentUri = request.getScheme()
                        + "://"
                        + request.getServerName()
                        + ("http".equals(request.getScheme())
                                && request.getServerPort() == 80
                                || "https".equals(request.getScheme())
                                && request.getServerPort() == 443 ? "" : ":"
                                + request.getServerPort())
                        + httpRequest.getRequestURI();
                String fullUrl = currentUri
                        + (httpRequest.getQueryString() != null ? "?"
                                + httpRequest.getQueryString() : "");
                // check if user has a session
                if (!AuthHelper.isAuthenticated(httpRequest)) {
                    if (AuthHelper.containsAuthenticationData(httpRequest)) {
                        Map<String, String> params = new HashMap<String, String>();
                        for (String key : request.getParameterMap().keySet()) {
                            params.put(key,
                                    request.getParameterMap().get(key)[0]);
                        }
                        AuthenticationResponse authResponse = AuthenticationResponseParser
                                .parse(new URI(fullUrl), params);
                        if (AuthHelper.isAuthenticationSuccessful(authResponse)) {

                            AuthenticationSuccessResponse oidcResponse = (AuthenticationSuccessResponse) authResponse;
                            AuthenticationResult result = getAccessToken(
                                    oidcResponse.getAuthorizationCode(),
                                    currentUri);
                            createSessionPrincipal(httpRequest, result);
                        } else {
                            AuthenticationErrorResponse oidcResponse = (AuthenticationErrorResponse) authResponse;
                            throw new Exception(String.format(
                                    "Request for auth code failed: %s - %s",
                                    oidcResponse.getErrorObject().getCode(),
                                    oidcResponse.getErrorObject()
                                            .getDescription()));
                        }
                    } else {
                            // not authenticated
                            httpResponse.setStatus(302);
                            httpResponse
                                    .sendRedirect(getRedirectUrl(currentUri));
                            return;
                    }
                } else {
                    // if authenticated, how toocheck for valid session?
                    AuthenticationResult result = AuthHelper
                            .getAuthSessionObject(httpRequest);

                    if (httpRequest.getParameter("refresh") != null) {
                        result = getAccessTokenFromRefreshToken(
                                result.getRefreshToken(), currentUri);
                    } else {
                        if (httpRequest.getParameter("cc") != null) {
                            result = getAccessTokenFromClientCredentials();
                        } else {
                            if (result.getExpiresOnDate().before(new Date())) {
                                result = getAccessTokenFromRefreshToken(
                                        result.getRefreshToken(), currentUri);
                            }
                        }
                    }
                    createSessionPrincipal(httpRequest, result);
                }
            } catch (Throwable exc) {
                httpResponse.setStatus(500);
                request.setAttribute("error", exc.getMessage());
                httpResponse.sendRedirect(((HttpServletRequest) request)
                        .getContextPath() + "/error.jsp");
            }
        }
        chain.doFilter(request, response);
    }

    private AuthenticationResult getAccessTokenFromClientCredentials()
            throws Throwable {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(authority + tenant + "/", true,
                    service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", new ClientCredential(clientId,
                            clientSecret), null);
            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }

    private AuthenticationResult getAccessTokenFromRefreshToken(
            String refreshToken, String currentUri) throws Throwable {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(authority + tenant + "/", true,
                    service);
            Future<AuthenticationResult> future = context
                    .acquireTokenByRefreshToken(refreshToken,
                            new ClientCredential(clientId, clientSecret), null,
                            null);
            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;

    }

    private AuthenticationResult getAccessToken(
            AuthorizationCode authorizationCode, String currentUri)
            throws Throwable {
        String authCode = authorizationCode.getValue();
        ClientCredential credential = new ClientCredential(clientId,
                clientSecret);
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(authority + tenant + "/", true,
                    service);
            Future<AuthenticationResult> future = context
                    .acquireTokenByAuthorizationCode(authCode, new URI(
                            currentUri), credential, null);
            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }

    private void createSessionPrincipal(HttpServletRequest httpRequest,
            AuthenticationResult result) throws Exception {
        httpRequest.getSession().setAttribute(
                AuthHelper.PRINCIPAL_SESSION_NAME, result);
    }

    private String getRedirectUrl(String currentUri)
            throws UnsupportedEncodingException {
        String redirectUrl = authority
                + this.tenant
                + "/oauth2/authorize?response_type=code%20id_token&scope=openid&response_mode=form_post&redirect_uri="
                + URLEncoder.encode(currentUri, "UTF-8") + "&client_id="
                + clientId + "&resource=https%3a%2f%2fgraph.windows.net"
                + "&nonce=" + UUID.randomUUID() + "&site_id=500879";
        return redirectUrl;
    }

    public void init(FilterConfig config) throws ServletException {
        clientId = config.getInitParameter("client_id");
        authority = config.getServletContext().getInitParameter("authority");
        tenant = config.getServletContext().getInitParameter("tenant");
        clientSecret = config.getInitParameter("secret_key");
    }

}

```

此 servlet 會公開所有 hello 方法 ADAL4J 就會預期收到 hello 應用程式 toorun 從該 hello。 hello 方法包括：

* **getAccessTokenFromClientCredentials()**: hello 密碼從取得 hello 存取語彙基元。
* **getAccessTokenFromRefreshToken()**： 取得 hello 存取權杖重新整理權杖。
* **getaccesstoken （)**： 取得 hello 存取語彙基元從 OpenID Connect 的流程 （可使用）。
* **createSessionPrincipal()**： 建立工作階段的主體 toouse Graph API 存取。
* **getRedirectUrl()**: hello 與您在 hello 入口網站中輸入值取得 hello redirectURL toocompare。

## <a name="step-9-compile-and-run-hello-sample-in-tomcat"></a>步驟 9： 編譯和執行 Tomcat hello 範例

1. 變更 tooyour 根目錄。
2. 您只要將放在一起使用的 toobuild hello 範例`maven`，請執行 hello 下列命令：

    `$ mvn package`

 此命令會使用您所撰寫的相依性的 hello pom.xml 檔案。

您現在在 /targets 目錄中應該有 adal4jsample.war 檔案。 您可以部署在 Tomcat 容器中的 hello 檔案，並瀏覽 hello http://localhost:8080/< adal4jsample/URL。

> [!NOTE]
> 您可以輕鬆部署最新 Tomcat 伺服器 hello.war 檔案。 移 toohttp://localhost:8080/管理員/，並遵循 hello 指示 hello adal4jsample.war 檔案上傳。 它會為您的 autodeploy 與 hello 正確端點。


## <a name="next-steps"></a>後續步驟
現在，您會有可運作的 Java 應用程式，可以驗證使用者，安全地呼叫 web Api 使用 OAuth 2.0，然後取得 hello 使用者的基本資訊。 如果您沒有已填入您的租用戶與使用者，現在因此是很好的時間 toodo。

如需其他的參考，您可以在兩種方式取得 hello 完成範例 （不含您的組態值）：

* 下載為 [.zip 檔案](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip)。
* 輸入下列命令的 hello 複製從 GitHub hello 檔案：

 ```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```
