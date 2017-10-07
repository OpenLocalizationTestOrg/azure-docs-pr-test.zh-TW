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
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>什麼是 hello 雲端服務模型，以及如何封裝？
建立雲端服務從三個元件，hello 服務定義*(.csdef)*，hello 服務組態*(.cscfg)*，和服務套件*(.cspkg)*。 這兩個 hello **ServiceDefinition.csdef**和**ServiceConfig.cscfg**檔案是以 XML 為基礎，並描述 hello 雲端服務和其設定方式; hello 結構統稱為 「 hello 模型。 hello **ServicePackage.cspkg** hello 從產生的 zip 檔案**ServiceDefinition.csdef**和在其他方面，包含所有必要的 hello 二進位相依性。 Azure 建立的雲端服務從這兩個 hello **ServicePackage.cspkg**和 hello **ServiceConfig.cscfg**。

一旦 hello 雲端服務在 Azure 中執行，您可加以重新設定透過 hello **ServiceConfig.cscfg**檔案，但您無法改變 hello 定義。

## <a name="what-would-you-like-tooknow-more-about"></a>您想深入了解 tooknow 什麼？
* 我想要深入了解 hello tooknow [ServiceDefinition.csdef](#csdef)和[ServiceConfig.cscfg](#cscfg)檔案。
* 我已經了解，請給我 [一些範例](#next-steps) ，讓我可以設定。
* 我想 toocreate hello [ServicePackage.cspkg](#cspkg)。
* 我打算使用 Visual Studio，而我想要...
  * [建立雲端服務][vs_create]
  * [重新設定現有的雲端服務][vs_reconfigure]
  * [部署雲端服務專案][vs_deploy]
  * [從遠端桌面進入雲端服務執行個體][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
hello **ServiceDefinition.csdef**檔案會指定所使用的 Azure tooconfigure hello 設定雲端服務。 hello [Azure 服務定義結構描述 (.csdef 檔)](https://msdn.microsoft.com/library/azure/ee758711.aspx) hello 允許的格式提供的服務定義檔。 hello 下列範例示範可以針對 hello Web 和背景工作角色定義的 hello 設定：

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

您可以使用參照 toohello[服務定義結構描述](https://msdn.microsoft.com/library/azure/ee758711.aspx)進一步了解 hello 這裡使用的 XML 結構描述，不過，以下是一些 hello 元素的簡短說明：

**Sites**  
包含在 IIS7 中所裝載的網站或 web 應用程式的 hello 定義。

**InputEndpoints**  
包含端點的 hello 定義使用 toocontact hello 雲端服務。

**InternalEndpoints**  
包含端點所使用的角色執行個體 toocommunicate 彼此 hello 定義。

**ConfigurationSettings**  
包含 hello 設定功能的定義特定角色。

**憑證**  
包含憑證所需的角色定義 hello。 hello 先前的程式碼範例示範使用 hello 設定 Azure Connect 的憑證。

**LocalResources**  
包含本機儲存體資源的 hello 定義。 本機儲存體資源是 hello hello 虛擬機器角色的執行個體執行所在的檔案系統上的預留的目錄。

**Imports**  
包含 hello 定義匯入的模組。 hello 上述程式碼範例顯示遠端桌面連線與 Azure Connect 的 hello 模組。

**Startup**  
包含 hello 角色啟動時執行的工作。 hello 工作是在.cmd 或可執行檔中定義。

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
hello 的 hello 設定您的雲端服務的組態由在 hello hello 值**ServiceConfiguration.cscfg**檔案。 您指定您想 toodeploy，這個檔案中每個角色執行個體的 hello 數目。 hello hello 在 hello 服務定義檔中所定義的組態設定的值會加入 toohello 服務組態檔。 hello 與 hello 雲端服務相關聯的任何管理憑證指紋也會加入 toohello 檔案。 hello [Azure 服務組態結構描述 (.cscfg 檔)](https://msdn.microsoft.com/library/azure/ee758710.aspx) hello 允許的格式提供的服務組態檔。

hello 服務組態檔不會封裝與 hello 應用程式，但會以個別檔案上傳的 tooAzure 和使用的 tooconfigure hello 雲端服務。 您可以上傳新的服務組態檔，無需重新部署您的雲端服務。 hello 雲端服務執行時，可以變更 hello hello 雲端服務的組態值。 hello 下列範例顯示 hello 可以針對 hello Web 和背景工作角色定義的組態設定：

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

您可以使用參照 toohello[服務組態結構描述](https://msdn.microsoft.com/library/azure/ee758710.aspx)為了更佳了解 hello XML 結構描述在此使用，不過，以下是 hello 元素的簡短說明：

**Instances**  
設定執行 hello 角色執行個體的 hello 數目。 您的雲端服務從可能變成無法使用在升級期間 tooprevent，建議您部署的直接存取 web 之角色的多個執行個體。 藉由部署多個執行個體，您符合 hello toohello 指導方針[Azure 計算服務等級協定 (SLA)](http://azure.microsoft.com/support/legal/sla/)，可保證當兩個網際網路對向角色 99.95%外部連線或多個角色服務上部署執行個體。

**ConfigurationSettings**  
設定執行中角色執行個體的 hello hello 設定。 hello hello 名稱`<Setting>`項目必須符合 hello 服務定義檔中的 hello 設定定義。

**憑證**  
設定 hello hello 服務所使用的憑證。 hello 先前的程式碼範例示範如何 toodefine hello hello RemoteAccess 模組的憑證。 hello 值 hello*指紋*屬性必須設定 hello 憑證 toouse toohello 指紋。

<p/>

> [!NOTE]
> hello hello 憑證指紋可加入 toohello 組態檔使用文字編輯器。 或者，可以在 hello 加入 hello 值**憑證**hello 索引標籤**屬性**hello 角色在 Visual Studio 中的頁面。
> 
> 

## <a name="defining-ports-for-role-instances"></a>定義角色執行個體的連接埠
Azure 可讓您只有一個進入點 tooa web 角色。 這表示所有流量都是透過一個 IP 位址發生。 您可以設定您的網站 tooshare 連接埠設定 hello 主機標頭 toodirect hello 要求 toohello 正確的位置。 您也可以在 hello IP 位址上設定您的應用程式 toolisten toowell 已知連接埠。

hello 下列範例顯示 hello 的網站及 web 應用程式的 web 角色的組態。 hello 網站會設定為連接埠 80 上的 hello 預設進入位置，而且 hello web 應用程式會從名為"mail.mysite.cloudapp.net"的替代主機標頭設定的 tooreceive 要求。

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


## <a name="changing-hello-configuration-of-a-role"></a>變更角色 hello 組態
在 Azure 中，而未離線 hello 服務執行時，您可以更新您的雲端服務的 hello 組態。 toochange 組態資訊，您可以上傳新的組態檔，或編輯 hello 設定檔中的放置，並將它套用 tooyour 執行服務。 hello 進行下列變更可以 toohello 服務組態：

* **變更組態設定的 hello 值**  
  當組態設定變更，角色執行個體可以選擇 tooapply hello 變更 hello 執行個體仍在線上運作或 toorecycle hello 執行個體依正常程序並套用 hello 變更 hello 執行個體處於離線狀態。
* **變更角色執行個體的 hello 服務拓撲**  
  ：拓撲變更不會影響執行中的執行個體，但是要移除的執行個體除外。 所有剩餘的執行個體通常不需要 toobe 回收。不過，您可以選擇 toorecycle 角色執行個體中回應 tooa 拓撲變更。
* **變更 hello 憑證指紋**  
  ：當角色執行個體離線時，您可以只更新憑證。 如果憑證已加入、 刪除或變更的角色執行個體在線上時，Azure 依正常程序會 hello 執行個體離線 tooupdate hello 憑證，並且讓它重新上線 hello 變更完成之後。

### <a name="handling-configuration-changes-with-service-runtime-events"></a>使用服務執行階段事件處理組態變更
hello [Azure 執行階段程式庫](https://msdn.microsoft.com/library/azure/mt419365.aspx)包含 hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx)命名空間，提供在角色中的 Azure 環境互動 hello 的類別。 hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx)類別會定義下列組態變更之前和之後所引發之事件的 hello:

* **[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) 事件**  
  發生這種情況的 hello 組態變更之前套用的 tooa 指定如有必要，向 hello 角色執行個體的機率 tootake 讓您的角色執行個體。
* **[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) 事件**  
  Hello 組態變更套用的 tooa 指定角色執行個體之後，就會發生。

> [!NOTE]
> 因為憑證變更一律離線 hello 角色執行個體，因此不會引發 hello RoleEnvironment.Changing 或 RoleEnvironment.Changed 事件。
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
toodeploy 為 Azure 中雲端服務的應用程式，您必須 hello 適當格式中的第一個套件 hello 應用程式。 您可以使用 hello **CSPack**命令列工具 (隨 hello [Azure SDK](https://azure.microsoft.com/downloads/)) 做為替代的 tooVisual Studio toocreate hello 封裝檔案。

**CSPack**使用 hello hello 服務定義檔和服務組態檔 toodefine hello hello 套件內容的內容。 **CSPack**使用 hello 所產生應用程式封裝檔 (.cspkg)，您可以上傳 tooAzure [Azure 入口網站](cloud-services-how-to-create-deploy-portal.md#create-and-deploy)。 根據預設，名為 hello 封裝`[ServiceDefinitionFileName].cspkg`，但是您可以指定不同的名稱使用 hello`/out`選項**CSPack**。

**CSPack** 位於  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> CSPack.exe （在 windows 上），就可以使用執行 hello **Microsoft Azure 命令提示字元**捷徑與 hello SDK 一起安裝。  
> 
> 執行 hello CSPack.exe 程式本身 toosee 所有 hello 可能交換器與命令相關的文件。
> 
> 

<p />

> [!TIP]
> 在本機執行雲端服務，在 hello **Microsoft Azure 計算模擬器**，使用 hello **/copyonly**選項。 此選項會複製 hello 應用程式 tooa 目錄配置從中他們可以執行 hello 計算模擬器中的 hello 二進位檔案。
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>範例命令 toopackage 雲端服務
hello 下列範例會建立應用程式封裝，其中包含 web 角色的 hello 資訊。 hello 命令指定 hello 服務定義檔 toouse，其中可以是二進位檔案的 hello 目錄找不到，hello hello 封裝檔案的名稱。

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

如果 hello 應用程式包含 web 角色和背景工作角色，hello 使用下列命令：

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

其中 hello 變數的定義方式如下：

| 變數 | 值 |
| --- | --- |
| \[DirectoryName\] |hello hello 根專案目錄下 hello hello Azure 專案.csdef 檔案的子目錄。 |
| \[ServiceDefinition\] |hello hello 服務定義檔的名稱。 根據預設，此檔案的名稱為 ServiceDefinition.csdef。 |
| \[OutputFileName\] |hello hello 名稱產生套件檔案。 一般而言，這會設定 toohello hello 應用程式名稱。 如果沒有任何檔案名稱指定，hello 應用程式封裝會建立為\[ApplicationName\].cspkg。 |
| \[RoleName\] |hello hello 服務定義檔中所定義的 hello 角色名稱。 |
| \[RoleBinariesDirectory] |hello hello hello 角色二進位檔位置。 |
| \[VirtualPath\] |hello hello hello 服務定義 Sites 區段中定義的每個虛擬路徑的實體目錄。 |
| \[PhysicalPath\] |hello hello 內容 hello hello 服務定義的網站 節點中定義的每個虛擬路徑的實體目錄。 |
| \[RoleAssemblyName\] |hello hello hello 角色二進位檔名稱。 |

## <a name="next-steps"></a>後續步驟
我打算建立雲端服務封裝，而且我想要...

* [設定雲端服務執行個體的遠端桌面][remotedesktop]
* [部署雲端服務專案][deploy]

我打算使用 Visual Studio，而我想要...

* [建立新的雲端服務][vs_create]
* [重新設定現有的雲端服務][vs_reconfigure]
* [部署雲端服務專案][vs_deploy]
* [設定雲端服務執行個體的遠端桌面][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
