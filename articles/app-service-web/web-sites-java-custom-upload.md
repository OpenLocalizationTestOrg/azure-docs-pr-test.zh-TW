---
title: "aaaUpload 自訂 Java web 應用程式 tooAzure"
description: "本教學課程會示範如何 tooupload 自訂 Java web 應用程式 tooAzure App Service Web 應用程式。"
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a>上傳自訂 Java web 應用程式 tooAzure
本主題說明如何 tooupload 自訂 Java web 應用程式太[Azure App Service] Web 應用程式。 包含適用於 tooany Java 網站或 web 應用程式，也是特定應用程式的一些範例的資訊是。

請注意，Azure 提供一種方法建立使用 hello Azure 入口網站的組態 UI，Java web 應用程式和 hello Azure Marketplace 述[Java web 應用程式建立 Azure App Service 中](web-sites-java-get-started.md)。 本教學課程是針對案例中您不想 toouse hello Azure 入口網站組態 UI 或 hello Azure Marketplace。  

## <a name="configuration-guidelines"></a>組態方針
hello 以下說明在 Azure 上自訂 Java web 應用程式所預期的 hello 設定。

* 動態指派 hello hello Java 處理序所使用的 HTTP 連接埠。  hello 程序必須使用 hello 環境變數中的 hello 連接埠`HTTP_PLATFORM_PORT`。
* 除了 hello 單一 HTTP 接聽程式，應該停用，所有接聽連接埠。  在 Tomcat 中，包含 hello 關機、 HTTPS 及 AJP 連接埠。
* hello 容器都必須設定為僅 IPv4 流量 toobe。
* hello**啟動**命令 hello 應用程式必須 toobe hello 組態中設定。
* 需要使用目錄的寫入權限的應用程式需要位於 hello Azure web 應用程式的內容目錄，也就是 toobe **D:\home**。  hello 環境變數`HOME`參考 tooD:\home。  

Hello web.config 檔案中，您可以視需要設定環境變數。

## <a name="webconfig-httpplatform-configuration"></a>web.config httpPlatform 組態
hello 下列資訊描述 hello **httpPlatform**在 web.config 中的格式。

**arguments** (預設值="")。 引數 toohello 可執行檔或指令碼指定在 hello **processPath**設定。

範例 (顯示內容包括 **processPath** )：

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -路徑 toohello 可執行檔或指令碼，將會啟動接聽 HTTP 要求的處理序。

範例：

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (預設值=10)。次數 hello 中指定的處理序**processPath**允許 toocrash 每分鐘。 如果超過此限制， **HttpPlatformHandler**將會停止啟動 hello hello 分鐘的 hello 剩餘的處理序。

**requestTimeout** (預設值="00:02:00")。持續時間的**HttpPlatformHandler** hello 接聽的處理序的回應將會等到`%HTTP_PLATFORM_PORT%`。

**startupRetryCount** (預設值=10)。次數**HttpPlatformHandler**將嘗試 toolaunch hello 處理程序中指定**processPath**。 如需詳細資訊，請參閱 **startupTimeLimit** 。

**startupTimeLimit** (預設值=10 秒)。持續時間的**HttpPlatformHandler**會等待 hello 可執行檔/指令碼 toostart hello 連接埠上接聽的處理序。  如果超過此時間限制， **HttpPlatformHandler**會終止 hello 處理序，然後再次嘗試 toolaunch 再試一次**startupRetryCount**時間。

**stdoutLogEnabled** (預設值="true")。如果為 true， **stdout**和**stderr** hello hello 中指定的處理序**processPath**設定就會重新導向的 toohello 檔案中指定**stdoutLogFile** (請參閱**stdoutLogFile** > 一節)。

**stdoutLogFile** (預設值="d:\home\LogFiles\httpPlatformStdout.log")。絕對檔案路徑的**stdout**和**stderr** hello 程序中指定**processPath**將記錄。

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`是特殊的預留位置，以作為的一部份時需要 toospecified**引數**或做為一部分 hello **httpPlatform** **environmentVariables**清單。 這會取代為由內部產生連接埠**HttpPlatformHandler**以便 hello 程序所指定**processPath**可以接聽此連接埠。
> 
> 

## <a name="deployment"></a>部署
Java 型 web 應用程式可以透過與 hello 網際網路資訊服務 (IIS) 基礎 web 應用程式搭配使用，大部分的 hello 相同表示輕鬆地部署。  FTP、 Git 和 Kudu 的所有支援部署機制，因為是 hello web 應用程式的整合式的 SCM 功能。 WebDeploy 會以通訊協定的方式運作，不過，由於 Java 不是使用 Visual Studio 開發的，WebDeploy 並不適用於 Java Web 應用程式部署使用案例。

## <a name="application-configuration-examples"></a>應用程式組態範例
下列應用程式、 web.config 檔和 hello hello 應用程式設定依現狀範例 tooshow 如何 tooenable 您 App Service Web 應用程式的 Java 應用程式。

### <a name="tomcat"></a>Tomcat
在 Tomcat 上 App Service Web 應用程式提供的兩種變化時，它仍然是很有可能 tooupload 客戶的特定執行個體。 下面是以不同 Java 虛擬機器 (JVM) 安裝 Tomcat 的範例。

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

在 hello Tomcat 側邊，有幾個需要 toobe 所做的設定變更。 hello server.xml 需要編輯 toobe tooset:

* 關機連接埠 = -1
* HTTP 連接器連接埠 = ${port.http}
* HTTP 連接器位址 = "127.0.0.1"
* 註解化 HTTPS 和 AJP 連接器
* hello IPv4 設定也可以設定在您可以在其中加入 hello catalina.properties 檔案中`java.net.preferIPv4Stack=true`

App Service Web Apps 不支援 Direct3d 呼叫。 toodisable，加入下列 Java 選項應您的應用程式進行這類呼叫 hello:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Tomcat hello 案例一樣，客戶可以 Jetty 的上傳自己的執行個體。 Hello 要執行 hello Jetty 的完整安裝的案例中，在 hello 組態看起來會像這樣：

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

hello Jetty 組態必須變更在 hello start.ini tooset toobe `java.net.preferIPv4Stack=true`。

### <a name="springboot"></a>Springboot
順序 tooget Springboot 中執行您的應用程式需要 tooupload JAR 或 WAR 檔案，並新增下列 web.config 檔的 hello。 hello web.config 檔案放入 hello wwwroot 資料夾。 在 hello web.config 調整 hello 引數 toopoint tooyour JAR 檔案，在 hello 遵循範例 hello JAR 檔案位於 hello wwwroot 資料夾。  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a>Hudson
我們的測試中使用 hello Hudson 3.1.2 war 和 hello 預設 Tomcat 7.0.50 執行個體但不會使用向上箭號 hello UI tooset 項目。  因為 Hudson 是軟體建置工具，所以建議使用的 tooinstall 它的專用執行個體，其中 hello **AlwaysOn**可以 hello web 應用程式上設定旗標。

1. 在 Web 應用程式的根目錄中 (例如 **d:\home\site\wwwroot**) 建立 **webapps** 目錄 (如果尚未存在)，並將 Hudson.war 放在 **d:\home\site\wwwroot\webapps** 中。
2. 下載 apache maven 3.0.5 (與 Hudson 相容)，並將它放在 **d:\home\site\wwwroot** 中。
3. 建立 web.config 中的**d:\home\site\wwwroot**和 hello 貼上下列內容：
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    此時 hello web 應用程式可以重新啟動的 tootake hello 變更。  連接 toohttp://yourwebapp/hudson toostart Hudson。
4. Hudson 會將自己設定之後，您應該會看到下列畫面 hello:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. 存取 hello Hudson 組態 頁面上： 按一下**管理 Hudson**，然後按一下**設定系統**。
6. 設定 hello JDK，如下所示：
   
    ![Hudson configuration](./media/web-sites-java-custom-upload/hudson2.png)
7. 如下所示設定 Maven：
   
    ![Maven configuration](./media/web-sites-java-custom-upload/maven.png)
8. 儲存 hello 設定。 Hudson 現在應已設定完成，並且可以開始使用。

如需 Hudson 的其他資訊，請參閱 [http://hudson-ci.org](http://hudson-ci.org)。

### <a name="liferay"></a>Liferay
App Service Web Apps 支援 Liferay。 Liferay 可能需要大量記憶體，因為需要由中型或大型專用背景工作，其可提供足夠的記憶體 toorun hello web 應用程式。 Liferay 也會使用數個分鐘 toostart。 因此，建議您設定 hello web 應用程式太**Always On**。  

使用 Tomcat Liferay 6.1.2 Community Edition GA3 結合在一起，hello 下列檔案已編輯下載 Liferay 之後：

**Server.xml**

* 變更關機連接埠太-1。
* 變更 HTTP 連接器嗎`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* 註解 hello AJP 連接器。

在 hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes**資料夾中，建立名為**入口網站 ext.properties**。 此檔案需要 toocontain 一行，如下所示：

    liferay.home=%HOME%/site/wwwroot/liferay

在 hello hello tomcat 7.0.40 資料夾中，相同的目錄層級建立名為**web.config**以 hello 下列內容：

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

在 hello **httpPlatform**封鎖 hello **requestTimeout**設定得"00: 10:00"。  可減少，但接著您就有可能 toosee 時一些逾時錯誤 Liferay 啟動載入。  如果此值已變更，然後 hello **connectionTimeout**在 hello tomcat server.xml 也應修改。  

值得注意的 hello JRE_HOME 環境 varariable 上方 web.config toopoint toohello hello 中指定的是 64 位元 JDK。 hello 預設值為 32 位元，但由於 Liferay 可能需要高的層級的記憶體，因此建議 toouse hello 64 位元 JDK。

進行這些變更之後，請重新啟動執行 Liferay 的 Web 應用程式，然後開啟 http://yourwebapp。 hello Liferay 入口網站是可從 hello web 應用程式根目錄。 

## <a name="next-steps"></a>後續步驟
如需 Liferay 的詳細資訊，請參閱 [http://www.liferay.com](http://www.liferay.com)。

如需 JAVA 的詳細資訊，請瀏覽[適用於 Java 開發人員的 Azure](/java/azure)。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
