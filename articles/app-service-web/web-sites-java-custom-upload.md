---
title: "將自訂 Java Web 應用程式上傳至 Azure"
description: "本教學課程說明如何將自訂 Java Web 應用程式上傳至 Azure App Service Web Apps。"
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
ms.openlocfilehash: 9c8f9ee7780859f7640ac82d6ebce85082170ad7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-custom-java-web-app-to-azure"></a><span data-ttu-id="1b823-103">將自訂 Java Web 應用程式上傳至 Azure</span><span class="sxs-lookup"><span data-stu-id="1b823-103">Upload a custom Java web app to Azure</span></span>
<span data-ttu-id="1b823-104">本主題說明如何將自訂 Java Web 應用程式上傳至 [Azure App Service] Web Apps。</span><span class="sxs-lookup"><span data-stu-id="1b823-104">This topic explains how to upload a custom Java web app to [Azure App Service] Web Apps.</span></span> <span data-ttu-id="1b823-105">內容包括適用於任何 Java 網站或 Web 應用程式的資訊，以及針對特定應用程式的一些範例。</span><span class="sxs-lookup"><span data-stu-id="1b823-105">Included is information that applies to any Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="1b823-106">請注意，如同 [在 Azure App Service 中建立 Java Web 應用程式](web-sites-java-get-started.md)中的說明一樣，Azure 提供了使用 Azure 入口網站的組態 UI 和 Azure Marketplace 來建立 Java Web 應用程式的方法。</span><span class="sxs-lookup"><span data-stu-id="1b823-106">Note that Azure provides a means for creating Java web apps using the Azure Portal's configuration UI, and the Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="1b823-107">本教學課程適用於您不打算使用 Azure 入口網站組態 UI 或 Azure Marketplace 的案例。</span><span class="sxs-lookup"><span data-stu-id="1b823-107">This tutorial is for scenarios in which you do not want to use the Azure Portal configuration UI or the Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="1b823-108">組態方針</span><span class="sxs-lookup"><span data-stu-id="1b823-108">Configuration guidelines</span></span>
<span data-ttu-id="1b823-109">下列內容說明在 Azure 上自訂 Java Web 應用程式的預期設定。</span><span class="sxs-lookup"><span data-stu-id="1b823-109">The following describes the settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="1b823-110">系統會動態指派 Java 程序所使用的 HTTP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="1b823-110">The HTTP port used by the Java process is dynamically assigned.</span></span>  <span data-ttu-id="1b823-111">此程序必須使用來自環境變數 `HTTP_PLATFORM_PORT`的連接埠。</span><span class="sxs-lookup"><span data-stu-id="1b823-111">The process must use the port from the environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="1b823-112">您應停用所有的接聽連接埠 (單一 HTTP 接聽程式除外)。</span><span class="sxs-lookup"><span data-stu-id="1b823-112">All listen ports other than the single HTTP listener should be disabled.</span></span>  <span data-ttu-id="1b823-113">在 Tomcat 中，這包括了關機、HTTPS 和 AJP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="1b823-113">In Tomcat, that includes the shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="1b823-114">僅需針對 IPv4 流量設定容器。</span><span class="sxs-lookup"><span data-stu-id="1b823-114">The container needs to be configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="1b823-115">組態中必須設定應用程式的 **startup** 命令。</span><span class="sxs-lookup"><span data-stu-id="1b823-115">The **startup** command for the application needs to be set in the configuration.</span></span>
* <span data-ttu-id="1b823-116">要求目錄具備寫入權限的應用程式必須位於 Azure Web 應用程式的內容目錄，也就是 **D:\home**。</span><span class="sxs-lookup"><span data-stu-id="1b823-116">Applications that require directories with write permission need to be located in the Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="1b823-117">環境變數 `HOME` 是指 D:\home。</span><span class="sxs-lookup"><span data-stu-id="1b823-117">The environmental variable `HOME` refers to D:\home.</span></span>  

<span data-ttu-id="1b823-118">您可以在 web.config 檔案中視需要設定環境變數。</span><span class="sxs-lookup"><span data-stu-id="1b823-118">You can set environment variables as required in the web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="1b823-119">web.config httpPlatform 組態</span><span class="sxs-lookup"><span data-stu-id="1b823-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="1b823-120">下列資訊說明 web.config 內的 **httpPlatform** 格式。</span><span class="sxs-lookup"><span data-stu-id="1b823-120">The following information describes the **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="1b823-121">**arguments** (預設值="")。</span><span class="sxs-lookup"><span data-stu-id="1b823-121">**arguments** (Default="").</span></span> <span data-ttu-id="1b823-122">在 **processPath** 設定中所指定的可執行檔或指令檔的引數。</span><span class="sxs-lookup"><span data-stu-id="1b823-122">Arguments to the executable or script specified in the **processPath** setting.</span></span>

<span data-ttu-id="1b823-123">範例 (顯示內容包括 **processPath** )：</span><span class="sxs-lookup"><span data-stu-id="1b823-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="1b823-124">**processPath** - 將會啟動接聽 HTTP 要求程序的可執行檔或指令檔路徑。</span><span class="sxs-lookup"><span data-stu-id="1b823-124">**processPath** - Path to the executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="1b823-125">範例：</span><span class="sxs-lookup"><span data-stu-id="1b823-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="1b823-126">**rapidFailsPerMinute** (預設值=10)。**processPath** 中指定程序可容許的每分鐘當機次數。</span><span class="sxs-lookup"><span data-stu-id="1b823-126">**rapidFailsPerMinute** (Default=10.) Number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="1b823-127">如果超過此限制， **HttpPlatformHandler** 便會停止在此分鐘剩餘時間內啟動程序。</span><span class="sxs-lookup"><span data-stu-id="1b823-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching the process for the remainder of the minute.</span></span>

<span data-ttu-id="1b823-128">**requestTimeout** (預設值="00:02:00")。**HttpPlatformHandler** 會等待接聽 `%HTTP_PLATFORM_PORT%` 程序回應的持續時間。</span><span class="sxs-lookup"><span data-stu-id="1b823-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from the process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="1b823-129">**startupRetryCount** (預設值=10)。**HttpPlatformHandler** 會嘗試啟動 **processPath** 中指定程序的次數。</span><span class="sxs-lookup"><span data-stu-id="1b823-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try to launch the process specified in **processPath**.</span></span> <span data-ttu-id="1b823-130">如需詳細資訊，請參閱 **startupTimeLimit** 。</span><span class="sxs-lookup"><span data-stu-id="1b823-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="1b823-131">**startupTimeLimit** (預設值=10 秒)。**HttpPlatformHandler** 會等待可執行檔/指令檔啟動接聽連接埠程序的持續時間。</span><span class="sxs-lookup"><span data-stu-id="1b823-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for the executable/script to start a process listening on the port.</span></span>  <span data-ttu-id="1b823-132">如果超過此時間限制，**HttpPlatformHandler** 會中止程序，並嘗試將它重新啟動 **startupRetryCount** 次。</span><span class="sxs-lookup"><span data-stu-id="1b823-132">If this time limit is exceeded, **HttpPlatformHandler** will kill the process and try to launch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="1b823-133">**stdoutLogEnabled** (預設值="true")。如果為 true，則 **processPath** 設定中指定程序的 **stdout** 和 **stderr**會被重新導向至 **stdoutLogFile** 中的指定檔案 (請參閱 **stdoutLogFile** 區段)。</span><span class="sxs-lookup"><span data-stu-id="1b823-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for the process specified in the **processPath** setting will be redirected to the file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="1b823-134">**stdoutLogFile** (預設值="d:\home\LogFiles\httpPlatformStdout.log")。**processPath** 中指定程序之 **stdout** 和 **stderr** 的絕對檔案路徑將會被記錄下來。</span><span class="sxs-lookup"><span data-stu-id="1b823-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="1b823-135">`%HTTP_PLATFORM_PORT%` 是個特殊預留位置，它必須以 **arguments** 的一部分或 **httpPlatform** **environmentVariables** 清單的一部分進行指定。</span><span class="sxs-lookup"><span data-stu-id="1b823-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs to specified either as part of **arguments** or as part of the **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="1b823-136">這將會被透過 **HttpPlatformHandler** 內部產生的連接埠取代，以便 **processPath** 所指定的程序可以接聽此連接埠。</span><span class="sxs-lookup"><span data-stu-id="1b823-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that the process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="1b823-137">部署</span><span class="sxs-lookup"><span data-stu-id="1b823-137">Deployment</span></span>
<span data-ttu-id="1b823-138">您可透過與 Internet Information Services (IIS) 架構 Web 應用程式中使用的大部分相同方式，來輕鬆部署 Java 型 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b823-138">Java based web apps can be deployed easily through most of the same means that are used with the Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="1b823-139">FTP、Git 和 Kudu 為支援的部署機制，如同 Web 應用程式的整合式 SCM 功能。</span><span class="sxs-lookup"><span data-stu-id="1b823-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is the integrated SCM capability for web apps.</span></span> <span data-ttu-id="1b823-140">WebDeploy 會以通訊協定的方式運作，不過，由於 Java 不是使用 Visual Studio 開發的，WebDeploy 並不適用於 Java Web 應用程式部署使用案例。</span><span class="sxs-lookup"><span data-stu-id="1b823-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="1b823-141">應用程式組態範例</span><span class="sxs-lookup"><span data-stu-id="1b823-141">Application configuration Examples</span></span>
<span data-ttu-id="1b823-142">在下列應用程式中，我們將提供 web.config 檔案和應用程式組態作為範例，說明如何啟用 App Service Web Apps 上的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b823-142">For the following applications, a web.config file and the application configuration is provided as examples to show how to enable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="1b823-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="1b823-143">Tomcat</span></span>
<span data-ttu-id="1b823-144">App Service Web Apps 隨附了兩個 Tomcat 變化，但很有可能您仍然可以上傳客戶特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="1b823-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible to upload customer specific instances.</span></span> <span data-ttu-id="1b823-145">下面是以不同 Java 虛擬機器 (JVM) 安裝 Tomcat 的範例。</span><span class="sxs-lookup"><span data-stu-id="1b823-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

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
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default to %programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="1b823-146">在 Tomcat 端，您必須進行幾個組態變更。</span><span class="sxs-lookup"><span data-stu-id="1b823-146">On the Tomcat side, there are a few configuration changes that need to be made.</span></span> <span data-ttu-id="1b823-147">必須編輯 server.xml 以設定下列選項：</span><span class="sxs-lookup"><span data-stu-id="1b823-147">The server.xml needs to be edited to set:</span></span>

* <span data-ttu-id="1b823-148">關機連接埠 = -1</span><span class="sxs-lookup"><span data-stu-id="1b823-148">Shutdown port = -1</span></span>
* <span data-ttu-id="1b823-149">HTTP 連接器連接埠 = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="1b823-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="1b823-150">HTTP 連接器位址 = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="1b823-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="1b823-151">註解化 HTTPS 和 AJP 連接器</span><span class="sxs-lookup"><span data-stu-id="1b823-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="1b823-152">您也可以在 catalina.properties 檔案中進行 IPv4 設定，在此檔案中，您可以新增 `java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="1b823-152">The IPv4 setting can also be set in the catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="1b823-153">App Service Web Apps 不支援 Direct3d 呼叫。</span><span class="sxs-lookup"><span data-stu-id="1b823-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="1b823-154">若要將其停用，請新增下列 Java 選項，您的應用程式即可進行下列呼叫： `-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="1b823-154">To disable those, add the following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="1b823-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="1b823-155">Jetty</span></span>
<span data-ttu-id="1b823-156">和 Tomcat 的情況一様，客戶可以上傳他們自己的 Jetty 執行個體。</span><span class="sxs-lookup"><span data-stu-id="1b823-156">As is the case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="1b823-157">在執行 Jetty 完整安裝的情況下，組態看來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1b823-157">In the case of running the full install of Jetty, the configuration would look like this:</span></span>

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

<span data-ttu-id="1b823-158">Jetty 組態必須在 start.ini 中進行變更，進而設定 `java.net.preferIPv4Stack=true`。</span><span class="sxs-lookup"><span data-stu-id="1b823-158">The Jetty configuration needs to be changed in the start.ini to set `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="1b823-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="1b823-159">Springboot</span></span>
<span data-ttu-id="1b823-160">若要執行 Springboot 應用程式，您必須上傳 JAR 或 WAR 檔案，並加入下列 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="1b823-160">In order to get a Springboot application running you need to upload your JAR or WAR file and add the following web.config file.</span></span> <span data-ttu-id="1b823-161">Web.config 檔案會移至 wwwroot 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="1b823-161">The web.config file goes into the wwwroot folder.</span></span> <span data-ttu-id="1b823-162">在 web.config 中調整引數以指向您的 JAR 檔案，在下列範例的 JAR 檔案也位於 wwwroot 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="1b823-162">In the web.config adjust the arguments to point to your JAR file, in the following example the JAR file is located in the wwwroot folder as well.</span></span>  

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


### <a name="hudson"></a><span data-ttu-id="1b823-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="1b823-163">Hudson</span></span>
<span data-ttu-id="1b823-164">我們的測試使用了 Hudson 3.1.2 war 和預設 Tomcat 7.0.50 執行個體，但沒有使用 UI 進行選項設定。</span><span class="sxs-lookup"><span data-stu-id="1b823-164">Our test used the Hudson 3.1.2 war and the default Tomcat 7.0.50 instance but without using the UI to set things up.</span></span>  <span data-ttu-id="1b823-165">因為 Hudson 是個軟體建置工具，建議您將它安裝在專屬執行個體上，您可以在專屬執行個體中設定 Web 應用程式的 **AlwaysOn** 旗標。</span><span class="sxs-lookup"><span data-stu-id="1b823-165">Because Hudson is a software build tool, it is advised to install it on dedicated instances where the **AlwaysOn** flag can be set on the web app.</span></span>

1. <span data-ttu-id="1b823-166">在 Web 應用程式的根目錄中 (例如 **d:\home\site\wwwroot**) 建立 **webapps** 目錄 (如果尚未存在)，並將 Hudson.war 放在 **d:\home\site\wwwroot\webapps** 中。</span><span class="sxs-lookup"><span data-stu-id="1b823-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="1b823-167">下載 apache maven 3.0.5 (與 Hudson 相容)，並將它放在 **d:\home\site\wwwroot** 中。</span><span class="sxs-lookup"><span data-stu-id="1b823-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="1b823-168">在 **d:\home\site\wwwroot** 中建立 web.config，並將下列內容貼入 web.config：</span><span class="sxs-lookup"><span data-stu-id="1b823-168">Create web.config in **d:\home\site\wwwroot** and paste the following contents in it:</span></span>
   
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
   
    <span data-ttu-id="1b823-169">此時，您可以重新啟動 Web 應用程式以接受變更。</span><span class="sxs-lookup"><span data-stu-id="1b823-169">At this point the web app can be restarted to take the changes.</span></span>  <span data-ttu-id="1b823-170">連線至 http://yourwebapp/hudson 以啟動 Hudson。</span><span class="sxs-lookup"><span data-stu-id="1b823-170">Connect to http://yourwebapp/hudson to start Hudson.</span></span>
4. <span data-ttu-id="1b823-171">在 Hudson 自行設定之後，您應該可以看到下列畫面：</span><span class="sxs-lookup"><span data-stu-id="1b823-171">After Hudson configures itself, you should see the following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="1b823-173">存取 Hudson 組態頁面：按一下 [Manage Hudson]，再按一下 [設定系統]。</span><span class="sxs-lookup"><span data-stu-id="1b823-173">Access the Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="1b823-174">如下所示設定 JDK：</span><span class="sxs-lookup"><span data-stu-id="1b823-174">Configure the JDK as shown below:</span></span>
   
    ![Hudson configuration](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="1b823-176">如下所示設定 Maven：</span><span class="sxs-lookup"><span data-stu-id="1b823-176">Configure Maven as shown below:</span></span>
   
    ![Maven configuration](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="1b823-178">儲存設定。</span><span class="sxs-lookup"><span data-stu-id="1b823-178">Save the settings.</span></span> <span data-ttu-id="1b823-179">Hudson 現在應已設定完成，並且可以開始使用。</span><span class="sxs-lookup"><span data-stu-id="1b823-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="1b823-180">如需 Hudson 的其他資訊，請參閱 [http://hudson-ci.org](http://hudson-ci.org)。</span><span class="sxs-lookup"><span data-stu-id="1b823-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="1b823-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="1b823-181">Liferay</span></span>
<span data-ttu-id="1b823-182">App Service Web Apps 支援 Liferay。</span><span class="sxs-lookup"><span data-stu-id="1b823-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="1b823-183">因為 Liferay 需要大量記憶體，Web 應用程式必須在可提供足夠記憶體的中型或大型專用背景工作上執行。</span><span class="sxs-lookup"><span data-stu-id="1b823-183">Since Liferay can require significant memory, the web app needs to run on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="1b823-184">另外，Liferay 需要數分鐘的時間才能啟動。</span><span class="sxs-lookup"><span data-stu-id="1b823-184">Liferay also takes several minutes to start up.</span></span> <span data-ttu-id="1b823-185">基於這個理由，建議您將 Web 應用程式設為 [Always On] 。</span><span class="sxs-lookup"><span data-stu-id="1b823-185">For that reason, it is recommended that you set the web app to **Always On**.</span></span>  

<span data-ttu-id="1b823-186">使用隨附於 Tomcat 的 Liferay 6.1.2 Community Edition GA3 時，下列檔案在下載 Liferay 之後遭到編輯：</span><span class="sxs-lookup"><span data-stu-id="1b823-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, the following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="1b823-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="1b823-187">**Server.xml**</span></span>

* <span data-ttu-id="1b823-188">關機連接埠變為 -1。</span><span class="sxs-lookup"><span data-stu-id="1b823-188">Change Shutdown port to -1.</span></span>
* <span data-ttu-id="1b823-189">將 HTTP 連接器變更為 `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="1b823-189">Change HTTP connector to       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="1b823-190">註解化 AJP 連接器。</span><span class="sxs-lookup"><span data-stu-id="1b823-190">Comment out the AJP connector.</span></span>

<span data-ttu-id="1b823-191">在 **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** 資料夾中，建立名為 **portal-ext.properties** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="1b823-191">In the **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="1b823-192">此檔案必須包含一行程式碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1b823-192">This file needs to contain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="1b823-193">在與 tomcat-7.0.40 資料夾相同的目錄層級中，根據下列內容建立名為 **web.config** 的檔案：</span><span class="sxs-lookup"><span data-stu-id="1b823-193">At the same directory level as the tomcat-7.0.40 folder, create a file named **web.config** with the following content:</span></span>

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

<span data-ttu-id="1b823-194">在 **httpPlatform** 區塊底下，**requestTimeout** 已設為 “00:10:00”。</span><span class="sxs-lookup"><span data-stu-id="1b823-194">Under the **httpPlatform** block, the **requestTimeout** is set to “00:10:00”.</span></span>  <span data-ttu-id="1b823-195">您可以降低此值，但如此一來，您很有可能會在啟動載入 Liferay 時看到一些逾時錯誤。</span><span class="sxs-lookup"><span data-stu-id="1b823-195">It can be reduced but then you are likely to see some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="1b823-196">如果此值遭到變更，則 tomcat server.xml 中的 **connectionTimeout** 也會同時進行修改。</span><span class="sxs-lookup"><span data-stu-id="1b823-196">If this value is changed, then the **connectionTimeout** in the tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="1b823-197">值得一提的是，JRE_HOME 環境變數會在上述的 web.config 中進行指定，並指向 64 位元 JDK。</span><span class="sxs-lookup"><span data-stu-id="1b823-197">It is worth noting that the JRE_HOME environnment varariable is specified in the above web.config to point to the 64-bit JDK.</span></span> <span data-ttu-id="1b823-198">預設值為 32 位元，但是因為 Liferay 可能需要高階記憶體，建議您使用 64 位元 JDK。</span><span class="sxs-lookup"><span data-stu-id="1b823-198">The default is 32-bit, but since Liferay may require high levels of memory, it is recommended to use the 64-bit JDK.</span></span>

<span data-ttu-id="1b823-199">進行這些變更之後，請重新啟動執行 Liferay 的 Web 應用程式，然後開啟 http://yourwebapp。</span><span class="sxs-lookup"><span data-stu-id="1b823-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="1b823-200">您可以在 Web 應用程式根目錄中找到 Liferay 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1b823-200">The Liferay portal is available from the web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1b823-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b823-201">Next steps</span></span>
<span data-ttu-id="1b823-202">如需 Liferay 的詳細資訊，請參閱 [http://www.liferay.com](http://www.liferay.com)。</span><span class="sxs-lookup"><span data-stu-id="1b823-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="1b823-203">如需 JAVA 的詳細資訊，請瀏覽[適用於 Java 開發人員的 Azure](/java/azure)。</span><span class="sxs-lookup"><span data-stu-id="1b823-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
