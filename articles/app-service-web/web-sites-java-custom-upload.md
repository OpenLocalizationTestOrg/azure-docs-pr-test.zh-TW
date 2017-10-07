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
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="4ffbf-103">上傳自訂 Java web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4ffbf-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="4ffbf-104">本主題說明如何 tooupload 自訂 Java web 應用程式太[Azure App Service] Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="4ffbf-105">包含適用於 tooany Java 網站或 web 應用程式，也是特定應用程式的一些範例的資訊是。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="4ffbf-106">請注意，Azure 提供一種方法建立使用 hello Azure 入口網站的組態 UI，Java web 應用程式和 hello Azure Marketplace 述[Java web 應用程式建立 Azure App Service 中](web-sites-java-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="4ffbf-107">本教學課程是針對案例中您不想 toouse hello Azure 入口網站組態 UI 或 hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="4ffbf-108">組態方針</span><span class="sxs-lookup"><span data-stu-id="4ffbf-108">Configuration guidelines</span></span>
<span data-ttu-id="4ffbf-109">hello 以下說明在 Azure 上自訂 Java web 應用程式所預期的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="4ffbf-110">動態指派 hello hello Java 處理序所使用的 HTTP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="4ffbf-111">hello 程序必須使用 hello 環境變數中的 hello 連接埠`HTTP_PLATFORM_PORT`。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="4ffbf-112">除了 hello 單一 HTTP 接聽程式，應該停用，所有接聽連接埠。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="4ffbf-113">在 Tomcat 中，包含 hello 關機、 HTTPS 及 AJP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="4ffbf-114">hello 容器都必須設定為僅 IPv4 流量 toobe。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="4ffbf-115">hello**啟動**命令 hello 應用程式必須 toobe hello 組態中設定。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="4ffbf-116">需要使用目錄的寫入權限的應用程式需要位於 hello Azure web 應用程式的內容目錄，也就是 toobe **D:\home**。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="4ffbf-117">hello 環境變數`HOME`參考 tooD:\home。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="4ffbf-118">Hello web.config 檔案中，您可以視需要設定環境變數。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="4ffbf-119">web.config httpPlatform 組態</span><span class="sxs-lookup"><span data-stu-id="4ffbf-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="4ffbf-120">hello 下列資訊描述 hello **httpPlatform**在 web.config 中的格式。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="4ffbf-121">**arguments** (預設值="")。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-121">**arguments** (Default="").</span></span> <span data-ttu-id="4ffbf-122">引數 toohello 可執行檔或指令碼指定在 hello **processPath**設定。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="4ffbf-123">範例 (顯示內容包括 **processPath** )：</span><span class="sxs-lookup"><span data-stu-id="4ffbf-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="4ffbf-124">**processPath** -路徑 toohello 可執行檔或指令碼，將會啟動接聽 HTTP 要求的處理序。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="4ffbf-125">範例：</span><span class="sxs-lookup"><span data-stu-id="4ffbf-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="4ffbf-126">**rapidFailsPerMinute** (預設值=10)。次數 hello 中指定的處理序**processPath**允許 toocrash 每分鐘。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="4ffbf-127">如果超過此限制， **HttpPlatformHandler**將會停止啟動 hello hello 分鐘的 hello 剩餘的處理序。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="4ffbf-128">**requestTimeout** (預設值="00:02:00")。持續時間的**HttpPlatformHandler** hello 接聽的處理序的回應將會等到`%HTTP_PLATFORM_PORT%`。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="4ffbf-129">**startupRetryCount** (預設值=10)。次數**HttpPlatformHandler**將嘗試 toolaunch hello 處理程序中指定**processPath**。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="4ffbf-130">如需詳細資訊，請參閱 **startupTimeLimit** 。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="4ffbf-131">**startupTimeLimit** (預設值=10 秒)。持續時間的**HttpPlatformHandler**會等待 hello 可執行檔/指令碼 toostart hello 連接埠上接聽的處理序。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="4ffbf-132">如果超過此時間限制， **HttpPlatformHandler**會終止 hello 處理序，然後再次嘗試 toolaunch 再試一次**startupRetryCount**時間。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="4ffbf-133">**stdoutLogEnabled** (預設值="true")。如果為 true， **stdout**和**stderr** hello hello 中指定的處理序**processPath**設定就會重新導向的 toohello 檔案中指定**stdoutLogFile** (請參閱**stdoutLogFile** > 一節)。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="4ffbf-134">**stdoutLogFile** (預設值="d:\home\LogFiles\httpPlatformStdout.log")。絕對檔案路徑的**stdout**和**stderr** hello 程序中指定**processPath**將記錄。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="4ffbf-135">`%HTTP_PLATFORM_PORT%`是特殊的預留位置，以作為的一部份時需要 toospecified**引數**或做為一部分 hello **httpPlatform** **environmentVariables**清單。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="4ffbf-136">這會取代為由內部產生連接埠**HttpPlatformHandler**以便 hello 程序所指定**processPath**可以接聽此連接埠。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="4ffbf-137">部署</span><span class="sxs-lookup"><span data-stu-id="4ffbf-137">Deployment</span></span>
<span data-ttu-id="4ffbf-138">Java 型 web 應用程式可以透過與 hello 網際網路資訊服務 (IIS) 基礎 web 應用程式搭配使用，大部分的 hello 相同表示輕鬆地部署。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="4ffbf-139">FTP、 Git 和 Kudu 的所有支援部署機制，因為是 hello web 應用程式的整合式的 SCM 功能。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="4ffbf-140">WebDeploy 會以通訊協定的方式運作，不過，由於 Java 不是使用 Visual Studio 開發的，WebDeploy 並不適用於 Java Web 應用程式部署使用案例。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="4ffbf-141">應用程式組態範例</span><span class="sxs-lookup"><span data-stu-id="4ffbf-141">Application configuration Examples</span></span>
<span data-ttu-id="4ffbf-142">下列應用程式、 web.config 檔和 hello hello 應用程式設定依現狀範例 tooshow 如何 tooenable 您 App Service Web 應用程式的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="4ffbf-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="4ffbf-143">Tomcat</span></span>
<span data-ttu-id="4ffbf-144">在 Tomcat 上 App Service Web 應用程式提供的兩種變化時，它仍然是很有可能 tooupload 客戶的特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="4ffbf-145">下面是以不同 Java 虛擬機器 (JVM) 安裝 Tomcat 的範例。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

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

<span data-ttu-id="4ffbf-146">在 hello Tomcat 側邊，有幾個需要 toobe 所做的設定變更。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="4ffbf-147">hello server.xml 需要編輯 toobe tooset:</span><span class="sxs-lookup"><span data-stu-id="4ffbf-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="4ffbf-148">關機連接埠 = -1</span><span class="sxs-lookup"><span data-stu-id="4ffbf-148">Shutdown port = -1</span></span>
* <span data-ttu-id="4ffbf-149">HTTP 連接器連接埠 = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="4ffbf-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="4ffbf-150">HTTP 連接器位址 = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="4ffbf-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="4ffbf-151">註解化 HTTPS 和 AJP 連接器</span><span class="sxs-lookup"><span data-stu-id="4ffbf-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="4ffbf-152">hello IPv4 設定也可以設定在您可以在其中加入 hello catalina.properties 檔案中`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="4ffbf-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="4ffbf-153">App Service Web Apps 不支援 Direct3d 呼叫。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="4ffbf-154">toodisable，加入下列 Java 選項應您的應用程式進行這類呼叫 hello:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="4ffbf-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="4ffbf-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="4ffbf-155">Jetty</span></span>
<span data-ttu-id="4ffbf-156">Tomcat hello 案例一樣，客戶可以 Jetty 的上傳自己的執行個體。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="4ffbf-157">Hello 要執行 hello Jetty 的完整安裝的案例中，在 hello 組態看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="4ffbf-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

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

<span data-ttu-id="4ffbf-158">hello Jetty 組態必須變更在 hello start.ini tooset toobe `java.net.preferIPv4Stack=true`。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="4ffbf-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="4ffbf-159">Springboot</span></span>
<span data-ttu-id="4ffbf-160">順序 tooget Springboot 中執行您的應用程式需要 tooupload JAR 或 WAR 檔案，並新增下列 web.config 檔的 hello。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="4ffbf-161">hello web.config 檔案放入 hello wwwroot 資料夾。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="4ffbf-162">在 hello web.config 調整 hello 引數 toopoint tooyour JAR 檔案，在 hello 遵循範例 hello JAR 檔案位於 hello wwwroot 資料夾。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

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


### <a name="hudson"></a><span data-ttu-id="4ffbf-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="4ffbf-163">Hudson</span></span>
<span data-ttu-id="4ffbf-164">我們的測試中使用 hello Hudson 3.1.2 war 和 hello 預設 Tomcat 7.0.50 執行個體但不會使用向上箭號 hello UI tooset 項目。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="4ffbf-165">因為 Hudson 是軟體建置工具，所以建議使用的 tooinstall 它的專用執行個體，其中 hello **AlwaysOn**可以 hello web 應用程式上設定旗標。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="4ffbf-166">在 Web 應用程式的根目錄中 (例如 **d:\home\site\wwwroot**) 建立 **webapps** 目錄 (如果尚未存在)，並將 Hudson.war 放在 **d:\home\site\wwwroot\webapps** 中。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="4ffbf-167">下載 apache maven 3.0.5 (與 Hudson 相容)，並將它放在 **d:\home\site\wwwroot** 中。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="4ffbf-168">建立 web.config 中的**d:\home\site\wwwroot**和 hello 貼上下列內容：</span><span class="sxs-lookup"><span data-stu-id="4ffbf-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
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
   
    <span data-ttu-id="4ffbf-169">此時 hello web 應用程式可以重新啟動的 tootake hello 變更。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="4ffbf-170">連接 toohttp://yourwebapp/hudson toostart Hudson。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="4ffbf-171">Hudson 會將自己設定之後，您應該會看到下列畫面 hello:</span><span class="sxs-lookup"><span data-stu-id="4ffbf-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="4ffbf-173">存取 hello Hudson 組態 頁面上： 按一下**管理 Hudson**，然後按一下**設定系統**。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="4ffbf-174">設定 hello JDK，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4ffbf-174">Configure hello JDK as shown below:</span></span>
   
    ![Hudson configuration](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="4ffbf-176">如下所示設定 Maven：</span><span class="sxs-lookup"><span data-stu-id="4ffbf-176">Configure Maven as shown below:</span></span>
   
    ![Maven configuration](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="4ffbf-178">儲存 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-178">Save hello settings.</span></span> <span data-ttu-id="4ffbf-179">Hudson 現在應已設定完成，並且可以開始使用。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="4ffbf-180">如需 Hudson 的其他資訊，請參閱 [http://hudson-ci.org](http://hudson-ci.org)。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="4ffbf-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="4ffbf-181">Liferay</span></span>
<span data-ttu-id="4ffbf-182">App Service Web Apps 支援 Liferay。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="4ffbf-183">Liferay 可能需要大量記憶體，因為需要由中型或大型專用背景工作，其可提供足夠的記憶體 toorun hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="4ffbf-184">Liferay 也會使用數個分鐘 toostart。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="4ffbf-185">因此，建議您設定 hello web 應用程式太**Always On**。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="4ffbf-186">使用 Tomcat Liferay 6.1.2 Community Edition GA3 結合在一起，hello 下列檔案已編輯下載 Liferay 之後：</span><span class="sxs-lookup"><span data-stu-id="4ffbf-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="4ffbf-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="4ffbf-187">**Server.xml**</span></span>

* <span data-ttu-id="4ffbf-188">變更關機連接埠太-1。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="4ffbf-189">變更 HTTP 連接器嗎`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="4ffbf-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="4ffbf-190">註解 hello AJP 連接器。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="4ffbf-191">在 hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes**資料夾中，建立名為**入口網站 ext.properties**。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="4ffbf-192">此檔案需要 toocontain 一行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4ffbf-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="4ffbf-193">在 hello hello tomcat 7.0.40 資料夾中，相同的目錄層級建立名為**web.config**以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="4ffbf-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

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

<span data-ttu-id="4ffbf-194">在 hello **httpPlatform**封鎖 hello **requestTimeout**設定得"00: 10:00"。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="4ffbf-195">可減少，但接著您就有可能 toosee 時一些逾時錯誤 Liferay 啟動載入。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="4ffbf-196">如果此值已變更，然後 hello **connectionTimeout**在 hello tomcat server.xml 也應修改。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="4ffbf-197">值得注意的 hello JRE_HOME 環境 varariable 上方 web.config toopoint toohello hello 中指定的是 64 位元 JDK。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="4ffbf-198">hello 預設值為 32 位元，但由於 Liferay 可能需要高的層級的記憶體，因此建議 toouse hello 64 位元 JDK。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="4ffbf-199">進行這些變更之後，請重新啟動執行 Liferay 的 Web 應用程式，然後開啟 http://yourwebapp。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="4ffbf-200">hello Liferay 入口網站是可從 hello web 應用程式根目錄。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4ffbf-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ffbf-201">Next steps</span></span>
<span data-ttu-id="4ffbf-202">如需 Liferay 的詳細資訊，請參閱 [http://www.liferay.com](http://www.liferay.com)。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="4ffbf-203">如需 JAVA 的詳細資訊，請瀏覽[適用於 Java 開發人員的 Azure](/java/azure)。</span><span class="sxs-lookup"><span data-stu-id="4ffbf-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
