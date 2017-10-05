---
title: "什麼是雲端服務模型和封裝 | Microsoft Docs"
description: "說明 Azure 中的雲端服務模型 (.csdef、.cscfg) 和封裝 (.cspkg)"
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
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="3fa8b-103">什麼是雲端服務模型？如何封裝？</span><span class="sxs-lookup"><span data-stu-id="3fa8b-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="3fa8b-104">雲端服務是從三個元件建立的，也就是服務定義 (.csdef)、服務組態 (.cscfg) 和服務封裝 (.cspkg)。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="3fa8b-105">**ServiceDefinition.csdef** 和 **ServiceConfig.cscfg** 這兩個檔案是以 XML 為基礎，描述雲端服務的結構及其設定方式，統稱為模型。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="3fa8b-106">**ServicePackage.cspkg** 是從 **ServiceDefinition.csdef** 產生的 zip 檔案，此外，包含所有必要的二進位型相依性。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="3fa8b-107">Azure 會從 **ServicePackage.cspkg** 和 **ServiceConfig.cscfg** 建立雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="3fa8b-108">一旦雲端服務在 Azure 中執行之後，您就可以透過 **ServiceConfig.cscfg** 檔案重新設定它，但您無法改變定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="3fa8b-109">您想要深入了解什麼？</span><span class="sxs-lookup"><span data-stu-id="3fa8b-109">What would you like to know more about?</span></span>
* <span data-ttu-id="3fa8b-110">我想要深入了解 [ServiceDefinition.csdef](#csdef) 和 [ServiceConfig.cscfg](#cscfg) 檔案。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="3fa8b-111">我已經了解，請給我 [一些範例](#next-steps) ，讓我可以設定。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="3fa8b-112">我想要建立 [ServicePackage.cspkg](#cspkg)。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="3fa8b-113">我打算使用 Visual Studio，而我想要...</span><span class="sxs-lookup"><span data-stu-id="3fa8b-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="3fa8b-114">[建立雲端服務][vs_create]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="3fa8b-115">[重新設定現有的雲端服務][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="3fa8b-116">[部署雲端服務專案][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="3fa8b-117">[從遠端桌面進入雲端服務執行個體][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="3fa8b-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="3fa8b-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="3fa8b-119">**ServiceDefinition.csdef** 檔案會指定 Azure 所使用的設定來設定雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="3fa8b-120">[Azure 服務定義結構描述 (.csdef 檔)](https://msdn.microsoft.com/library/azure/ee758711.aspx) 會為服務定義檔提供允許的格式。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="3fa8b-121">以下範例顯示可以針對 Web 和背景工作角色定義的設定：</span><span class="sxs-lookup"><span data-stu-id="3fa8b-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="3fa8b-122">您可以參考[服務定義結構描述](https://msdn.microsoft.com/library/azure/ee758711.aspx)，進一步了解此處所使用的 XML 結構描述，不過，以下是某些元素的簡短說明：</span><span class="sxs-lookup"><span data-stu-id="3fa8b-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="3fa8b-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-123">**Sites**</span></span>  
<span data-ttu-id="3fa8b-124">包含 IIS7 中所裝載的網站或 Web 應用程式的定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="3fa8b-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-125">**InputEndpoints**</span></span>  
<span data-ttu-id="3fa8b-126">包含用來連絡雲端服務的端點的定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="3fa8b-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="3fa8b-128">包含角色執行個體用來彼此通訊的端點的定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="3fa8b-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="3fa8b-130">包含特定角色功能的設定定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="3fa8b-131">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-131">**Certificates**</span></span>  
<span data-ttu-id="3fa8b-132">包含角色所需的憑證的定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="3fa8b-133">上述程式碼範例顯示用於設定 Azure Connect 的憑證。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="3fa8b-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-134">**LocalResources**</span></span>  
<span data-ttu-id="3fa8b-135">包含本機儲存資源的定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="3fa8b-136">本機儲存資源是執行中角色執行個體所在之虛擬機器的檔案系統上的保留目錄。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="3fa8b-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-137">**Imports**</span></span>  
<span data-ttu-id="3fa8b-138">包含匯入的模組的定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="3fa8b-139">上述程式碼範例顯示遠端桌面連線與 Azure Connect 的模組。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="3fa8b-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-140">**Startup**</span></span>  
<span data-ttu-id="3fa8b-141">包含角色啟動時執行的工作。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="3fa8b-142">這些工作是在 .cmd 或可執行檔中定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="3fa8b-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="3fa8b-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="3fa8b-144">雲端服務設定的組態取決於 **ServiceConfiguration.cscfg** 檔案中的值。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="3fa8b-145">您可以指定您想要在此檔案中為每個角色部署的執行個體的數目。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="3fa8b-146">您在服務定義檔中定義的組態設定的值會加入至服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="3fa8b-147">與雲端服務相關聯的任何管理憑證的指紋也會加入至檔案。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="3fa8b-148">[Azure 服務組態結構描述 (.cscfg 檔)](https://msdn.microsoft.com/library/azure/ee758710.aspx) 為服務組態檔提供允許的格式。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="3fa8b-149">服務組態檔沒有與應用程式封裝在一起，但是做為個別的檔案上傳至 Azure，並用來設定雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="3fa8b-150">您可以上傳新的服務組態檔，無需重新部署您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="3fa8b-151">雲端服務執行時，可以變更雲端服務的組態值。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="3fa8b-152">以下範例顯示可以針對 Web 和背景工作角色定義的組態設定：</span><span class="sxs-lookup"><span data-stu-id="3fa8b-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="3fa8b-153">您可以參考 [服務組態結構描述](https://msdn.microsoft.com/library/azure/ee758710.aspx) ，進一步了解此處所使用的 XML 結構描述，不過，以下是元素的簡短說明：</span><span class="sxs-lookup"><span data-stu-id="3fa8b-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="3fa8b-154">**Instances**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-154">**Instances**</span></span>  
<span data-ttu-id="3fa8b-155">設定執行中角色執行個體的數目。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="3fa8b-156">為防止您的雲端服務在升級期間可能變成無法使用，建議您部署多個 Web 對向角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="3fa8b-157">部署多個執行個體的做法符合 [Azure 計算服務等級協定 (SLA)](http://azure.microsoft.com/support/legal/sla/)中的指導方針，當您為服務部署兩個或更多個角色執行個體時，此等級協定可保證網際網路對向角色有 99.95% 的外部連線能力。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="3fa8b-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="3fa8b-159">設定執行中角色執行個體的設定。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="3fa8b-160">`<Setting>` 元素的名稱必須符合服務定義檔中的設定定義。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="3fa8b-161">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-161">**Certificates**</span></span>  
<span data-ttu-id="3fa8b-162">設定服務所使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="3fa8b-163">上述程式碼範例顯示如何定義 RemoteAccess 模組的憑證。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="3fa8b-164">*thumbprint* 屬性的值必須設定為要使用的憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="3fa8b-165">您可以使用文字編輯器，將憑證指紋新增至組態檔。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="3fa8b-166">或者，在 Visual Studio 中，也可以在角色 [屬性] 頁面的 [憑證] 索引標籤上新增值。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="3fa8b-167">定義角色執行個體的連接埠</span><span class="sxs-lookup"><span data-stu-id="3fa8b-167">Defining ports for role instances</span></span>
<span data-ttu-id="3fa8b-168">Azure 對於 Web 角色，僅允許一個進入點。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="3fa8b-169">這表示所有流量都是透過一個 IP 位址發生。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="3fa8b-170">您可以設定您的網站共用連接埠，方法是設定主機標頭，將要求導向到正確的位置。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="3fa8b-171">您也可以設定您的應用程式接聽 IP 位址的公認連接埠。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="3fa8b-172">以下範例顯示具有網站及 Web 應用程式的 Web 角色的組態。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="3fa8b-173">網站會設定為連接埠 80 上的預設進入位置，而 Web 應用程式則會設定為從稱為 "mail.mysite.cloudapp.net" 的替代主機標頭接收要求。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

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


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="3fa8b-174">變更角色的組態</span><span class="sxs-lookup"><span data-stu-id="3fa8b-174">Changing the configuration of a role</span></span>
<span data-ttu-id="3fa8b-175">您可以在雲端服務於 Azure 中執行的同時，更新該雲端服務的組態，而不讓服務離線。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="3fa8b-176">若要變更組態資訊，您可以上傳新的組態檔，或就地編輯現有的組態檔，並將其套用到執行中的服務。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="3fa8b-177">您可以針對服務的組態進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="3fa8b-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="3fa8b-178">**變更組態設定的值**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="3fa8b-179">：當組態設定變更時，角色執行個體可以選擇在執行個體上線時套用變更，或是正常回收執行個體，並在執行個體離線時套用變更。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="3fa8b-180">**變更角色執行個體的服務拓撲**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="3fa8b-181">：拓撲變更不會影響執行中的執行個體，但是要移除的執行個體除外。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="3fa8b-182">其餘所有執行個體通常不需要進行回收，不過，您可以選擇回收角色執行個體，以回應拓撲變更。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="3fa8b-183">**變更憑證指紋**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="3fa8b-184">：當角色執行個體離線時，您可以只更新憑證。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="3fa8b-185">如果在角色執行個體上線時加入、刪除或變更憑證，Azure 會讓執行個體正常離線以更新憑證，並在變更完成後讓它再次上線。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="3fa8b-186">使用服務執行階段事件處理組態變更</span><span class="sxs-lookup"><span data-stu-id="3fa8b-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="3fa8b-187">[Azure 執行階段程式庫](https://msdn.microsoft.com/library/azure/mt419365.aspx)包含 [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) 命名空間，其中提供從角色來與 Azure 環境互動的類別。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="3fa8b-188">[RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) 類別會定義組態變更前後會引發的下列事件：</span><span class="sxs-lookup"><span data-stu-id="3fa8b-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="3fa8b-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) 事件**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="3fa8b-190">這會在組態變更套用至指定的角色執行個體之前發生，讓您有機會記下角色執行個體 (如有需要)。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="3fa8b-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) 事件**</span><span class="sxs-lookup"><span data-stu-id="3fa8b-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="3fa8b-192">：在組態變更套用至指定的角色執行個體之後發生。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="3fa8b-193">由於憑證變更時，一律會讓角色執行個體離線，因此不會引發 RoleEnvironment.Changing 或 RoleEnvironment.Changed 事件。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="3fa8b-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="3fa8b-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="3fa8b-195">若要將應用程式部署為 Azure 中的雲端服務，您必須先使用適當的格式封裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="3fa8b-196">您可以使用 **CSPack** 命令列工具 (隨 [Azure SDK](https://azure.microsoft.com/downloads/)安裝) 做為 Visual Studio 的替代方案，以建立封裝檔案。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="3fa8b-197">**CSPack** 會使用服務定義檔和服務組態檔的內容，定義封裝的內容。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="3fa8b-198">**CSPack** 會產生應用程式封裝檔案 (.cspkg)，您可以使用 [Azure 入口網站](cloud-services-how-to-create-deploy-portal.md#create-and-deploy)，將其上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="3fa8b-199">根據預設，套件的名稱為 `[ServiceDefinitionFileName].cspkg`，但是您可以使用 **CSPack** 的 `/out` 選項指定不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="3fa8b-200">**CSPack** 位於</span><span class="sxs-lookup"><span data-stu-id="3fa8b-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="3fa8b-201">CSPack.exe (在 Windows 上) 可以透過執行隨 SDK 一起安裝的 **Microsoft Azure 命令提示字元** 捷徑來使用。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="3fa8b-202">執行 CSPack.exe 程式本身，以查看所有可能的參數和命令的相關文件。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="3fa8b-203">在本機於 **Microsoft Azure 計算模擬器**中執行雲端服務，並使用 **/copyonly** 選項。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="3fa8b-204">此選項會將應用程式的二進位檔案複製到目錄配置中，在計算模擬器中就可以從那裡執行它們。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="3fa8b-205">封裝雲端服務的範例命令</span><span class="sxs-lookup"><span data-stu-id="3fa8b-205">Example command to package a cloud service</span></span>
<span data-ttu-id="3fa8b-206">下列範例會建立應用程式封裝，其中包含 Web 角色的資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="3fa8b-207">此命令會指定要使用的服務定義檔、可以找到二進位檔案所在的目錄，以及封裝檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="3fa8b-208">如果應用程式同時包含 Web 角色和背景工作角色，則會使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3fa8b-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="3fa8b-209">其中的變數定義如下：</span><span class="sxs-lookup"><span data-stu-id="3fa8b-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="3fa8b-210">變數</span><span class="sxs-lookup"><span data-stu-id="3fa8b-210">Variable</span></span> | <span data-ttu-id="3fa8b-211">值</span><span class="sxs-lookup"><span data-stu-id="3fa8b-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fa8b-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-212">\[DirectoryName\]</span></span> |<span data-ttu-id="3fa8b-213">專案根目錄底下的子目錄，其中包含 Azure 專案的 .csdef 檔案。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="3fa8b-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="3fa8b-215">服務定義檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-215">The name of the service definition file.</span></span> <span data-ttu-id="3fa8b-216">根據預設，此檔案的名稱為 ServiceDefinition.csdef。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="3fa8b-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-217">\[OutputFileName\]</span></span> |<span data-ttu-id="3fa8b-218">所產生的封裝檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-218">The name for the generated package file.</span></span> <span data-ttu-id="3fa8b-219">一般而言，這是設定為應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="3fa8b-220">如果沒有指定檔案名稱，就會將應用程式封裝建立為 \[ApplicationName\].cspkg。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="3fa8b-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-221">\[RoleName\]</span></span> |<span data-ttu-id="3fa8b-222">服務定義檔中所定義的角色名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="3fa8b-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="3fa8b-224">角色的二進位檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="3fa8b-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-225">\[VirtualPath\]</span></span> |<span data-ttu-id="3fa8b-226">在服務定義的 Sites 區段中定義的每個虛擬路徑的實體目錄。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="3fa8b-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="3fa8b-228">在服務定義的 site 節點中定義的每個虛擬路徑內容的實體目錄。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="3fa8b-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="3fa8b-230">角色的二進位檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa8b-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3fa8b-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fa8b-231">Next steps</span></span>
<span data-ttu-id="3fa8b-232">我打算建立雲端服務封裝，而且我想要...</span><span class="sxs-lookup"><span data-stu-id="3fa8b-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="3fa8b-233">[設定雲端服務執行個體的遠端桌面][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="3fa8b-234">[部署雲端服務專案][deploy]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="3fa8b-235">我打算使用 Visual Studio，而我想要...</span><span class="sxs-lookup"><span data-stu-id="3fa8b-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="3fa8b-236">[建立新的雲端服務][vs_create]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="3fa8b-237">[重新設定現有的雲端服務][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="3fa8b-238">[部署雲端服務專案][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="3fa8b-239">[設定雲端服務執行個體的遠端桌面][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="3fa8b-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
