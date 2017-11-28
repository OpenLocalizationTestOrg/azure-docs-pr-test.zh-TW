---
title: "aaaWhat 是雲端服務模型和封裝 |Microsoft 文件"
description: "描述 hello 的雲端服務模型 （.csdef，.cscfg） 和 Azure 中的封裝 (.cspkg)"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="b041f-103">什麼是 hello 雲端服務模型，以及如何封裝？</span><span class="sxs-lookup"><span data-stu-id="b041f-103">What is hello Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="b041f-104">建立雲端服務從三個元件，hello 服務定義*(.csdef)*，hello 服務組態*(.cscfg)*，和服務套件*(.cspkg)*。</span><span class="sxs-lookup"><span data-stu-id="b041f-104">A cloud service is created from three components, hello service definition *(.csdef)*, hello service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="b041f-105">這兩個 hello **ServiceDefinition.csdef**和**ServiceConfig.cscfg**檔案是以 XML 為基礎，並描述 hello 雲端服務和其設定方式; hello 結構統稱為 「 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="b041f-105">Both hello **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe hello structure of hello cloud service and how it's configured; collectively called hello model.</span></span> <span data-ttu-id="b041f-106">hello **ServicePackage.cspkg** hello 從產生的 zip 檔案**ServiceDefinition.csdef**和在其他方面，包含所有必要的 hello 二進位相依性。</span><span class="sxs-lookup"><span data-stu-id="b041f-106">hello **ServicePackage.cspkg** is a zip file that is generated from hello **ServiceDefinition.csdef** and among other things, contains all hello required binary-based dependencies.</span></span> <span data-ttu-id="b041f-107">Azure 建立的雲端服務從這兩個 hello **ServicePackage.cspkg**和 hello **ServiceConfig.cscfg**。</span><span class="sxs-lookup"><span data-stu-id="b041f-107">Azure creates a cloud service from both hello **ServicePackage.cspkg** and hello **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="b041f-108">一旦 hello 雲端服務在 Azure 中執行，您可加以重新設定透過 hello **ServiceConfig.cscfg**檔案，但您無法改變 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="b041f-108">Once hello cloud service is running in Azure, you can reconfigure it through hello **ServiceConfig.cscfg** file, but you cannot alter hello definition.</span></span>

## <a name="what-would-you-like-tooknow-more-about"></a><span data-ttu-id="b041f-109">您想深入了解 tooknow 什麼？</span><span class="sxs-lookup"><span data-stu-id="b041f-109">What would you like tooknow more about?</span></span>
* <span data-ttu-id="b041f-110">我想要深入了解 hello tooknow [ServiceDefinition.csdef](#csdef)和[ServiceConfig.cscfg](#cscfg)檔案。</span><span class="sxs-lookup"><span data-stu-id="b041f-110">I want tooknow more about hello [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="b041f-111">我已經了解，請給我 [一些範例](#next-steps) ，讓我可以設定。</span><span class="sxs-lookup"><span data-stu-id="b041f-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="b041f-112">我想 toocreate hello [ServicePackage.cspkg](#cspkg)。</span><span class="sxs-lookup"><span data-stu-id="b041f-112">I want toocreate hello [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="b041f-113">我打算使用 Visual Studio，而我想要...</span><span class="sxs-lookup"><span data-stu-id="b041f-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="b041f-114">[建立雲端服務][vs_create]</span><span class="sxs-lookup"><span data-stu-id="b041f-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="b041f-115">[重新設定現有的雲端服務][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="b041f-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="b041f-116">[部署雲端服務專案][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="b041f-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="b041f-117">[從遠端桌面進入雲端服務執行個體][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="b041f-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="b041f-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="b041f-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="b041f-119">hello **ServiceDefinition.csdef**檔案會指定所使用的 Azure tooconfigure hello 設定雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b041f-119">hello **ServiceDefinition.csdef** file specifies hello settings that are used by Azure tooconfigure a cloud service.</span></span> <span data-ttu-id="b041f-120">hello [Azure 服務定義結構描述 (.csdef 檔)](https://msdn.microsoft.com/library/azure/ee758711.aspx) hello 允許的格式提供的服務定義檔。</span><span class="sxs-lookup"><span data-stu-id="b041f-120">hello [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides hello allowable format for a service definition file.</span></span> <span data-ttu-id="b041f-121">hello 下列範例示範可以針對 hello Web 和背景工作角色定義的 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="b041f-121">hello following example shows hello settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="b041f-122">您可以使用參照 toohello[服務定義結構描述](https://msdn.microsoft.com/library/azure/ee758711.aspx)進一步了解 hello 這裡使用的 XML 結構描述，不過，以下是一些 hello 元素的簡短說明：</span><span class="sxs-lookup"><span data-stu-id="b041f-122">You can refer toohello [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of hello XML schema used here, however, here is a quick explanation of some of hello elements:</span></span>

<span data-ttu-id="b041f-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="b041f-123">**Sites**</span></span>  
<span data-ttu-id="b041f-124">包含在 IIS7 中所裝載的網站或 web 應用程式的 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="b041f-124">Contains hello definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="b041f-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="b041f-125">**InputEndpoints**</span></span>  
<span data-ttu-id="b041f-126">包含端點的 hello 定義使用 toocontact hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b041f-126">Contains hello definitions for endpoints that are used toocontact hello cloud service.</span></span>

<span data-ttu-id="b041f-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="b041f-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="b041f-128">包含端點所使用的角色執行個體 toocommunicate 彼此 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="b041f-128">Contains hello definitions for endpoints that are used by role instances toocommunicate with each other.</span></span>

<span data-ttu-id="b041f-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="b041f-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="b041f-130">包含 hello 設定功能的定義特定角色。</span><span class="sxs-lookup"><span data-stu-id="b041f-130">Contains hello setting definitions for features of a specific role.</span></span>

<span data-ttu-id="b041f-131">**憑證**</span><span class="sxs-lookup"><span data-stu-id="b041f-131">**Certificates**</span></span>  
<span data-ttu-id="b041f-132">包含憑證所需的角色定義 hello。</span><span class="sxs-lookup"><span data-stu-id="b041f-132">Contains hello definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="b041f-133">hello 先前的程式碼範例示範使用 hello 設定 Azure Connect 的憑證。</span><span class="sxs-lookup"><span data-stu-id="b041f-133">hello previous code example shows a certificate that is used for hello configuration of Azure Connect.</span></span>

<span data-ttu-id="b041f-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="b041f-134">**LocalResources**</span></span>  
<span data-ttu-id="b041f-135">包含本機儲存體資源的 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="b041f-135">Contains hello definitions for local storage resources.</span></span> <span data-ttu-id="b041f-136">本機儲存體資源是 hello hello 虛擬機器角色的執行個體執行所在的檔案系統上的預留的目錄。</span><span class="sxs-lookup"><span data-stu-id="b041f-136">A local storage resource is a reserved directory on hello file system of hello virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="b041f-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="b041f-137">**Imports**</span></span>  
<span data-ttu-id="b041f-138">包含 hello 定義匯入的模組。</span><span class="sxs-lookup"><span data-stu-id="b041f-138">Contains hello definitions for imported modules.</span></span> <span data-ttu-id="b041f-139">hello 上述程式碼範例顯示遠端桌面連線與 Azure Connect 的 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="b041f-139">hello previous code example shows hello modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="b041f-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="b041f-140">**Startup**</span></span>  
<span data-ttu-id="b041f-141">包含 hello 角色啟動時執行的工作。</span><span class="sxs-lookup"><span data-stu-id="b041f-141">Contains tasks that are run when hello role starts.</span></span> <span data-ttu-id="b041f-142">hello 工作是在.cmd 或可執行檔中定義。</span><span class="sxs-lookup"><span data-stu-id="b041f-142">hello tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="b041f-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="b041f-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="b041f-144">hello 的 hello 設定您的雲端服務的組態由在 hello hello 值**ServiceConfiguration.cscfg**檔案。</span><span class="sxs-lookup"><span data-stu-id="b041f-144">hello configuration of hello settings for your cloud service is determined by hello values in hello **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="b041f-145">您指定您想 toodeploy，這個檔案中每個角色執行個體的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="b041f-145">You specify hello number of instances that you want toodeploy for each role in this file.</span></span> <span data-ttu-id="b041f-146">hello hello 在 hello 服務定義檔中所定義的組態設定的值會加入 toohello 服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="b041f-146">hello values for hello configuration settings that you defined in hello service definition file are added toohello service configuration file.</span></span> <span data-ttu-id="b041f-147">hello 與 hello 雲端服務相關聯的任何管理憑證指紋也會加入 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b041f-147">hello thumbprints for any management certificates that are associated with hello cloud service are also added toohello file.</span></span> <span data-ttu-id="b041f-148">hello [Azure 服務組態結構描述 (.cscfg 檔)](https://msdn.microsoft.com/library/azure/ee758710.aspx) hello 允許的格式提供的服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="b041f-148">hello [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides hello allowable format for a service configuration file.</span></span>

<span data-ttu-id="b041f-149">hello 服務組態檔不會封裝與 hello 應用程式，但會以個別檔案上傳的 tooAzure 和使用的 tooconfigure hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b041f-149">hello service configuration file is not packaged with hello application, but is uploaded tooAzure as a separate file and is used tooconfigure hello cloud service.</span></span> <span data-ttu-id="b041f-150">您可以上傳新的服務組態檔，無需重新部署您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b041f-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="b041f-151">hello 雲端服務執行時，可以變更 hello hello 雲端服務的組態值。</span><span class="sxs-lookup"><span data-stu-id="b041f-151">hello configuration values for hello cloud service can be changed while hello cloud service is running.</span></span> <span data-ttu-id="b041f-152">hello 下列範例顯示 hello 可以針對 hello Web 和背景工作角色定義的組態設定：</span><span class="sxs-lookup"><span data-stu-id="b041f-152">hello following example shows hello configuration settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="b041f-153">您可以使用參照 toohello[服務組態結構描述](https://msdn.microsoft.com/library/azure/ee758710.aspx)為了更佳了解 hello XML 結構描述在此使用，不過，以下是 hello 元素的簡短說明：</span><span class="sxs-lookup"><span data-stu-id="b041f-153">You can refer toohello [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding hello XML schema used here, however, here is a quick explanation of hello elements:</span></span>

<span data-ttu-id="b041f-154">**Instances**</span><span class="sxs-lookup"><span data-stu-id="b041f-154">**Instances**</span></span>  
<span data-ttu-id="b041f-155">設定執行 hello 角色執行個體的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="b041f-155">Configures hello number of running instances for hello role.</span></span> <span data-ttu-id="b041f-156">您的雲端服務從可能變成無法使用在升級期間 tooprevent，建議您部署的直接存取 web 之角色的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="b041f-156">tooprevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="b041f-157">藉由部署多個執行個體，您符合 hello toohello 指導方針[Azure 計算服務等級協定 (SLA)](http://azure.microsoft.com/support/legal/sla/)，可保證當兩個網際網路對向角色 99.95%外部連線或多個角色服務上部署執行個體。</span><span class="sxs-lookup"><span data-stu-id="b041f-157">By deploying more than one instance, you are adhering toohello guidelines in hello [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="b041f-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="b041f-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="b041f-159">設定執行中角色執行個體的 hello hello 設定。</span><span class="sxs-lookup"><span data-stu-id="b041f-159">Configures hello settings for hello running instances for a role.</span></span> <span data-ttu-id="b041f-160">hello hello 名稱`<Setting>`項目必須符合 hello 服務定義檔中的 hello 設定定義。</span><span class="sxs-lookup"><span data-stu-id="b041f-160">hello name of hello `<Setting>` elements must match hello setting definitions in hello service definition file.</span></span>

<span data-ttu-id="b041f-161">**憑證**</span><span class="sxs-lookup"><span data-stu-id="b041f-161">**Certificates**</span></span>  
<span data-ttu-id="b041f-162">設定 hello hello 服務所使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="b041f-162">Configures hello certificates that are used by hello service.</span></span> <span data-ttu-id="b041f-163">hello 先前的程式碼範例示範如何 toodefine hello hello RemoteAccess 模組的憑證。</span><span class="sxs-lookup"><span data-stu-id="b041f-163">hello previous code example shows how toodefine hello certificate for hello RemoteAccess module.</span></span> <span data-ttu-id="b041f-164">hello 值 hello*指紋*屬性必須設定 hello 憑證 toouse toohello 指紋。</span><span class="sxs-lookup"><span data-stu-id="b041f-164">hello value of hello *thumbprint* attribute must be set toohello thumbprint of hello certificate toouse.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="b041f-165">hello hello 憑證指紋可加入 toohello 組態檔使用文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="b041f-165">hello thumbprint for hello certificate can be added toohello configuration file by using a text editor.</span></span> <span data-ttu-id="b041f-166">或者，可以在 hello 加入 hello 值**憑證**hello 索引標籤**屬性**hello 角色在 Visual Studio 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="b041f-166">Or, hello value can be added on hello **Certificates** tab of hello **Properties** page of hello role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="b041f-167">定義角色執行個體的連接埠</span><span class="sxs-lookup"><span data-stu-id="b041f-167">Defining ports for role instances</span></span>
<span data-ttu-id="b041f-168">Azure 可讓您只有一個進入點 tooa web 角色。</span><span class="sxs-lookup"><span data-stu-id="b041f-168">Azure allows only one entry point tooa web role.</span></span> <span data-ttu-id="b041f-169">這表示所有流量都是透過一個 IP 位址發生。</span><span class="sxs-lookup"><span data-stu-id="b041f-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="b041f-170">您可以設定您的網站 tooshare 連接埠設定 hello 主機標頭 toodirect hello 要求 toohello 正確的位置。</span><span class="sxs-lookup"><span data-stu-id="b041f-170">You can configure your websites tooshare a port by configuring hello host header toodirect hello request toohello correct location.</span></span> <span data-ttu-id="b041f-171">您也可以在 hello IP 位址上設定您的應用程式 toolisten toowell 已知連接埠。</span><span class="sxs-lookup"><span data-stu-id="b041f-171">You can also configure your applications toolisten toowell-known ports on hello IP address.</span></span>

<span data-ttu-id="b041f-172">hello 下列範例顯示 hello 的網站及 web 應用程式的 web 角色的組態。</span><span class="sxs-lookup"><span data-stu-id="b041f-172">hello following sample shows hello configuration for a web role with a website and web application.</span></span> <span data-ttu-id="b041f-173">hello 網站會設定為連接埠 80 上的 hello 預設進入位置，而且 hello web 應用程式會從名為"mail.mysite.cloudapp.net"的替代主機標頭設定的 tooreceive 要求。</span><span class="sxs-lookup"><span data-stu-id="b041f-173">hello website is configured as hello default entry location on port 80, and hello web applications are configured tooreceive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a><span data-ttu-id="b041f-174">變更角色 hello 組態</span><span class="sxs-lookup"><span data-stu-id="b041f-174">Changing hello configuration of a role</span></span>
<span data-ttu-id="b041f-175">在 Azure 中，而未離線 hello 服務執行時，您可以更新您的雲端服務的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="b041f-175">You can update hello configuration of your cloud service while it is running in Azure, without taking hello service offline.</span></span> <span data-ttu-id="b041f-176">toochange 組態資訊，您可以上傳新的組態檔，或編輯 hello 設定檔中的放置，並將它套用 tooyour 執行服務。</span><span class="sxs-lookup"><span data-stu-id="b041f-176">toochange configuration information, you can either upload a new configuration file, or edit hello configuration file in place and apply it tooyour running service.</span></span> <span data-ttu-id="b041f-177">hello 進行下列變更可以 toohello 服務組態：</span><span class="sxs-lookup"><span data-stu-id="b041f-177">hello following changes can be made toohello configuration of a service:</span></span>

* <span data-ttu-id="b041f-178">**變更組態設定的 hello 值**</span><span class="sxs-lookup"><span data-stu-id="b041f-178">**Changing hello values of configuration settings**</span></span>  
  <span data-ttu-id="b041f-179">當組態設定變更，角色執行個體可以選擇 tooapply hello 變更 hello 執行個體仍在線上運作或 toorecycle hello 執行個體依正常程序並套用 hello 變更 hello 執行個體處於離線狀態。</span><span class="sxs-lookup"><span data-stu-id="b041f-179">When a configuration setting changes, a role instance can choose tooapply hello change while hello instance is online, or toorecycle hello instance gracefully and apply hello change while hello instance is offline.</span></span>
* <span data-ttu-id="b041f-180">**變更角色執行個體的 hello 服務拓撲**</span><span class="sxs-lookup"><span data-stu-id="b041f-180">**Changing hello service topology of role instances**</span></span>  
  <span data-ttu-id="b041f-181">：拓撲變更不會影響執行中的執行個體，但是要移除的執行個體除外。</span><span class="sxs-lookup"><span data-stu-id="b041f-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="b041f-182">所有剩餘的執行個體通常不需要 toobe 回收。不過，您可以選擇 toorecycle 角色執行個體中回應 tooa 拓撲變更。</span><span class="sxs-lookup"><span data-stu-id="b041f-182">All remaining instances generally do not need toobe recycled; however, you can choose toorecycle role instances in response tooa topology change.</span></span>
* <span data-ttu-id="b041f-183">**變更 hello 憑證指紋**</span><span class="sxs-lookup"><span data-stu-id="b041f-183">**Changing hello certificate thumbprint**</span></span>  
  <span data-ttu-id="b041f-184">：當角色執行個體離線時，您可以只更新憑證。</span><span class="sxs-lookup"><span data-stu-id="b041f-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="b041f-185">如果憑證已加入、 刪除或變更的角色執行個體在線上時，Azure 依正常程序會 hello 執行個體離線 tooupdate hello 憑證，並且讓它重新上線 hello 變更完成之後。</span><span class="sxs-lookup"><span data-stu-id="b041f-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes hello instance offline tooupdate hello certificate and bring it back online after hello change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="b041f-186">使用服務執行階段事件處理組態變更</span><span class="sxs-lookup"><span data-stu-id="b041f-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="b041f-187">hello [Azure 執行階段程式庫](https://msdn.microsoft.com/library/azure/mt419365.aspx)包含 hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx)命名空間，提供在角色中的 Azure 環境互動 hello 的類別。</span><span class="sxs-lookup"><span data-stu-id="b041f-187">hello [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with hello Azure environment from a role.</span></span> <span data-ttu-id="b041f-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx)類別會定義下列組態變更之前和之後所引發之事件的 hello:</span><span class="sxs-lookup"><span data-stu-id="b041f-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines hello following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="b041f-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) 事件**</span><span class="sxs-lookup"><span data-stu-id="b041f-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="b041f-190">發生這種情況的 hello 組態變更之前套用的 tooa 指定如有必要，向 hello 角色執行個體的機率 tootake 讓您的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="b041f-190">This occurs before hello configuration change is applied tooa specified instance of a role giving you a chance tootake down hello role instances if necessary.</span></span>
* <span data-ttu-id="b041f-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) 事件**</span><span class="sxs-lookup"><span data-stu-id="b041f-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="b041f-192">Hello 組態變更套用的 tooa 指定角色執行個體之後，就會發生。</span><span class="sxs-lookup"><span data-stu-id="b041f-192">Occurs after hello configuration change is applied tooa specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="b041f-193">因為憑證變更一律離線 hello 角色執行個體，因此不會引發 hello RoleEnvironment.Changing 或 RoleEnvironment.Changed 事件。</span><span class="sxs-lookup"><span data-stu-id="b041f-193">Because certificate changes always take hello instances of a role offline, they do not raise hello RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="b041f-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="b041f-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="b041f-195">toodeploy 為 Azure 中雲端服務的應用程式，您必須 hello 適當格式中的第一個套件 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b041f-195">toodeploy an application as a cloud service in Azure, you must first package hello application in hello appropriate format.</span></span> <span data-ttu-id="b041f-196">您可以使用 hello **CSPack**命令列工具 (隨 hello [Azure SDK](https://azure.microsoft.com/downloads/)) 做為替代的 tooVisual Studio toocreate hello 封裝檔案。</span><span class="sxs-lookup"><span data-stu-id="b041f-196">You can use hello **CSPack** command-line tool (installed with hello [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello package file as an alternative tooVisual Studio.</span></span>

<span data-ttu-id="b041f-197">**CSPack**使用 hello hello 服務定義檔和服務組態檔 toodefine hello hello 套件內容的內容。</span><span class="sxs-lookup"><span data-stu-id="b041f-197">**CSPack** uses hello contents of hello service definition file and service configuration file toodefine hello contents of hello package.</span></span> <span data-ttu-id="b041f-198">**CSPack**使用 hello 所產生應用程式封裝檔 (.cspkg)，您可以上傳 tooAzure [Azure 入口網站](cloud-services-how-to-create-deploy-portal.md#create-and-deploy)。</span><span class="sxs-lookup"><span data-stu-id="b041f-198">**CSPack** generates an application package file (.cspkg) that you can upload tooAzure by using hello [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="b041f-199">根據預設，名為 hello 封裝`[ServiceDefinitionFileName].cspkg`，但是您可以指定不同的名稱使用 hello`/out`選項**CSPack**。</span><span class="sxs-lookup"><span data-stu-id="b041f-199">By default, hello package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using hello `/out` option of **CSPack**.</span></span>

<span data-ttu-id="b041f-200">**CSPack** 位於</span><span class="sxs-lookup"><span data-stu-id="b041f-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="b041f-201">CSPack.exe （在 windows 上），就可以使用執行 hello **Microsoft Azure 命令提示字元**捷徑與 hello SDK 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="b041f-201">CSPack.exe (on windows) is available by running hello **Microsoft Azure Command Prompt** shortcut that is installed with hello SDK.</span></span>  
> 
> <span data-ttu-id="b041f-202">執行 hello CSPack.exe 程式本身 toosee 所有 hello 可能交換器與命令相關的文件。</span><span class="sxs-lookup"><span data-stu-id="b041f-202">Run hello CSPack.exe program by itself toosee documentation about all hello possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="b041f-203">在本機執行雲端服務，在 hello **Microsoft Azure 計算模擬器**，使用 hello **/copyonly**選項。</span><span class="sxs-lookup"><span data-stu-id="b041f-203">Run your cloud service locally in hello **Microsoft Azure Compute Emulator**, use hello **/copyonly** option.</span></span> <span data-ttu-id="b041f-204">此選項會複製 hello 應用程式 tooa 目錄配置從中他們可以執行 hello 計算模擬器中的 hello 二進位檔案。</span><span class="sxs-lookup"><span data-stu-id="b041f-204">This option copies hello binary files for hello application tooa directory layout from which they can be run in hello compute emulator.</span></span>
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a><span data-ttu-id="b041f-205">範例命令 toopackage 雲端服務</span><span class="sxs-lookup"><span data-stu-id="b041f-205">Example command toopackage a cloud service</span></span>
<span data-ttu-id="b041f-206">hello 下列範例會建立應用程式封裝，其中包含 web 角色的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="b041f-206">hello following example creates an application package that contains hello information for a web role.</span></span> <span data-ttu-id="b041f-207">hello 命令指定 hello 服務定義檔 toouse，其中可以是二進位檔案的 hello 目錄找不到，hello hello 封裝檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="b041f-207">hello command specifies hello service definition file toouse, hello directory where binary files can be found, and hello name of hello package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="b041f-208">如果 hello 應用程式包含 web 角色和背景工作角色，hello 使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="b041f-208">If hello application contains both a web role and a worker role, hello following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="b041f-209">其中 hello 變數的定義方式如下：</span><span class="sxs-lookup"><span data-stu-id="b041f-209">Where hello variables are defined as follows:</span></span>

| <span data-ttu-id="b041f-210">變數</span><span class="sxs-lookup"><span data-stu-id="b041f-210">Variable</span></span> | <span data-ttu-id="b041f-211">值</span><span class="sxs-lookup"><span data-stu-id="b041f-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b041f-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="b041f-212">\[DirectoryName\]</span></span> |<span data-ttu-id="b041f-213">hello hello 根專案目錄下 hello hello Azure 專案.csdef 檔案的子目錄。</span><span class="sxs-lookup"><span data-stu-id="b041f-213">hello subdirectory under hello root project directory that contains hello .csdef file of hello Azure project.</span></span> |
| <span data-ttu-id="b041f-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="b041f-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="b041f-215">hello hello 服務定義檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="b041f-215">hello name of hello service definition file.</span></span> <span data-ttu-id="b041f-216">根據預設，此檔案的名稱為 ServiceDefinition.csdef。</span><span class="sxs-lookup"><span data-stu-id="b041f-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="b041f-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="b041f-217">\[OutputFileName\]</span></span> |<span data-ttu-id="b041f-218">hello hello 名稱產生套件檔案。</span><span class="sxs-lookup"><span data-stu-id="b041f-218">hello name for hello generated package file.</span></span> <span data-ttu-id="b041f-219">一般而言，這會設定 toohello hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="b041f-219">Typically, this is set toohello name of hello application.</span></span> <span data-ttu-id="b041f-220">如果沒有任何檔案名稱指定，hello 應用程式封裝會建立為\[ApplicationName\].cspkg。</span><span class="sxs-lookup"><span data-stu-id="b041f-220">If no file name is specified, hello application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="b041f-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="b041f-221">\[RoleName\]</span></span> |<span data-ttu-id="b041f-222">hello hello 服務定義檔中所定義的 hello 角色名稱。</span><span class="sxs-lookup"><span data-stu-id="b041f-222">hello name of hello role as defined in hello service definition file.</span></span> |
| <span data-ttu-id="b041f-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="b041f-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="b041f-224">hello hello hello 角色二進位檔位置。</span><span class="sxs-lookup"><span data-stu-id="b041f-224">hello location of hello binary files for hello role.</span></span> |
| <span data-ttu-id="b041f-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="b041f-225">\[VirtualPath\]</span></span> |<span data-ttu-id="b041f-226">hello hello hello 服務定義 Sites 區段中定義的每個虛擬路徑的實體目錄。</span><span class="sxs-lookup"><span data-stu-id="b041f-226">hello physical directories for each virtual path defined in hello Sites section of hello service definition.</span></span> |
| <span data-ttu-id="b041f-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="b041f-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="b041f-228">hello hello 內容 hello hello 服務定義的網站 節點中定義的每個虛擬路徑的實體目錄。</span><span class="sxs-lookup"><span data-stu-id="b041f-228">hello physical directories of hello contents for each virtual path defined in hello site node of hello service definition.</span></span> |
| <span data-ttu-id="b041f-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="b041f-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="b041f-230">hello hello hello 角色二進位檔名稱。</span><span class="sxs-lookup"><span data-stu-id="b041f-230">hello name of hello binary file for hello role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b041f-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b041f-231">Next steps</span></span>
<span data-ttu-id="b041f-232">我打算建立雲端服務封裝，而且我想要...</span><span class="sxs-lookup"><span data-stu-id="b041f-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="b041f-233">[設定雲端服務執行個體的遠端桌面][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="b041f-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="b041f-234">[部署雲端服務專案][deploy]</span><span class="sxs-lookup"><span data-stu-id="b041f-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="b041f-235">我打算使用 Visual Studio，而我想要...</span><span class="sxs-lookup"><span data-stu-id="b041f-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="b041f-236">[建立新的雲端服務][vs_create]</span><span class="sxs-lookup"><span data-stu-id="b041f-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="b041f-237">[重新設定現有的雲端服務][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="b041f-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="b041f-238">[部署雲端服務專案][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="b041f-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="b041f-239">[設定雲端服務執行個體的遠端桌面][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="b041f-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
