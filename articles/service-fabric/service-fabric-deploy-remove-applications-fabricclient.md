---
title: "aaaAzure Service Fabric 應用程式部署 |Microsoft 文件"
description: "使用 hello toodeploy FabricClient Api 和服務網狀架構中移除應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>使用 FabricClient 來部署和移除應用程式
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient API](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

[封裝應用程式類型][10]後，即可將它部署至 Azure Service Fabric 叢集中。 部署包含下列三個步驟的 hello:

1. 上傳 hello 應用程式封裝 toohello 映像存放區
2. 註冊 hello 應用程式類型
3. 建立 hello 應用程式執行個體

部署應用程式的執行個體正在執行中 hello 叢集後，您可以刪除 hello 應用程式執行個體和其應用程式類型。 toocompletely 移除從 hello 叢集中的應用程式牽涉到 hello 下列步驟：

1. 移除 （或刪除） 執行應用程式執行個體的 hello
2. 如果您不再需要取消註冊 hello 應用程式類型
3. 移除 hello 映像存放區中的 hello 應用程式套件

如果您使用[用於部署和偵錯應用程式的 Visual Studio](service-fabric-publish-app-remote-cluster.md)在本機開發叢集上，所有 hello 前面的步驟都是透過 PowerShell 指令碼會自動處理。  此指令碼位於 hello*指令碼*hello 應用程式專案的資料夾。 這篇文章提供背景資訊，讓您可以執行，該指令碼內容正在進行 hello Visual Studio 之外，相同的作業。 
 
## <a name="connect-toohello-cluster"></a>Toohello 叢集連線
藉由建立連接 toohello 叢集[FabricClient](/dotnet/api/system.fabric.fabricclient)執行個體，然後再執行任何 hello 程式碼範例在本文中。 如需範例連接 tooa 本機開發叢集，或在遠端叢集或叢集使用 Azure Active Directory，X509 保護的憑證或 Windows Active Directory，請參閱[連接 tooa 安全叢集](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis)。 tooconnect toohello 本機開發叢集，請執行下列 hello:

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>上傳 hello 應用程式套件
假設您在 Visual Studio 中組建並封裝名為 *MyApplication* 的應用程式。 根據預設，hello hello ApplicationManifest.xml 中列出的應用程式類型名稱是"MyApplicationType"。  hello 應用程式封裝，其中包含 hello 必要的應用程式資訊清單、 服務資訊清單，以及程式碼/config/資料的封裝，位於*C:\Users\&lt; username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*。

正在上傳的 hello 應用程式封裝會將它放在 hello 內部的 Service Fabric 元件所存取的位置。 Service Fabric hello 應用程式套件 hello 註冊期間驗證 hello 應用程式套件。 不過，如果您想 tooverify hello 應用程式封裝在本機 （亦即上, 傳之前） 時，使用 hello[測試 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet。

hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API 上傳 hello 應用程式封裝 toohello 叢集映像存放區。 

如果 hello 應用程式套件很大且/或有許多檔案，您可以[壓縮](service-fabric-package-apps.md#compress-a-package)並將它複製 toohello 映像存放區使用 PowerShell。 hello 壓縮會減少 hello 大小和檔案的 hello 數目。

請參閱[hello 映像存放區連接字串了解](service-fabric-image-store-connection-string.md)如需關於 hello 映像存放區，以及映像存放區連接字串的補充資訊。

## <a name="register-hello-application-package"></a>註冊 hello 應用程式套件
hello 應用程式類型和版本 hello 註冊 hello 應用程式封裝時變成可供使用的應用程式資訊清單中宣告。 hello 系統讀取 hello 封裝上傳 hello 上一個步驟中，會驗證 hello 封裝、 處理 hello 套件內容，以及複製 hello 處理封裝 tooan 內部系統位置。  

hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 暫存器 hello hello 叢集中的應用程式類型，並使其可供部署。

hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API 提供已成功註冊應用程式的所有類型的相關資訊。 您可以使用此 API toodetermine hello 註冊完成。

## <a name="create-an-application-instance"></a>建立應用程式執行個體
您可以從已成功註冊使用 hello 任何應用程式類型應用程式具現化[CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync)應用程式開發介面。 每個應用程式的 hello 名稱必須以 hello 開頭*"fabric:"*配置，而且必須是唯一的 （叢集） 內的每個應用程式執行個體。 也會建立任何 hello hello 目標應用程式類型的應用程式資訊清單中定義的預設服務。

多個應用程式執行個體可以針對任何指定的已註冊應用程式類型版本來建立。 每個應用程式執行個體將在隔離狀態下執行，包含本身的工作目錄和程序集。

toosee 名為應用程式和服務正在執行 hello 的 hello 叢集中[GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)和[GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)應用程式開發介面。

## <a name="create-a-service-instance"></a>建立服務執行個體
您可以具現化服務，以從服務型別使用 hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync)應用程式開發介面。  如果 hello 服務宣告為 hello 應用程式資訊清單中的預設服務，hello 應用程式具現化時，會具現化 hello 服務。  呼叫 hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync)已具現化服務 API 會傳回包含錯誤程式碼，其值為 FabricErrorCode.ServiceAlreadyExists FabricException 類型的例外狀況。

## <a name="remove-a-service-instance"></a>移除服務執行個體
當不再需要的服務執行個體時，您可以移除它來呼叫 hello 執行應用程式執行個體的 hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync)應用程式開發介面。  

> [!WARNING]
> 此作業無法回復，且服務狀態無法復原。

## <a name="remove-an-application-instance"></a>移除應用程式執行個體
當不再需要應用程式執行個體時，您可以永久移除它的名稱使用 hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync)應用程式開發介面。 [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync)會自動移除屬於 toohello 應用程式以及，永久移除所有的服務狀態的所有服務。

> [!WARNING]
> 此作業無法回復，且應用程式狀態無法復原。

## <a name="unregister-an-application-type"></a>取消註冊應用程式類型
當不再需要特定版本的應用程式類型時，應該取消註冊該特定版本的 hello 應用程式類型使用 hello[取消註冊 ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync)應用程式開發介面。 應用程式類型版本存放區所使用的空間 hello 映像存放區解除登錄未使用的版本。 只要沒有任何應用程式會針對該版本 hello 應用程式類型的具現化，而且沒有擱置中的應用程式升級正在參考該版本的 hello 應用程式類型，可以取消註冊應用程式類型的版本。

## <a name="remove-an-application-package-from-hello-image-store"></a>移除 hello 映像存放區中的應用程式套件
當不再需要的應用程式封裝時，可以刪除系統資源使用 hello hello 映像存放區 toofree 從[RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage)應用程式開發介面。

## <a name="troubleshooting"></a>疑難排解
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage 要求 ImageStoreConnectionString
hello Service Fabric SDK 環境應該已經有 hello 正確設定預設值。 但所有命令的 hello ImageStoreConnectionString 如有需要應符合 hello 值該 hello Service Fabric 叢集所使用。 您可以在 hello 叢集資訊清單中找到 hello ImageStoreConnectionString 使用 hello 擷取[Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps)和 Get ImageStoreConnectionStringFromClusterManifest 命令：

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet，這是 hello Service Fabric SDK PowerShell 模組的一部分，是使用的 tooget hello 映像儲存連接字串。  tooimport hello SDK 模組，執行：

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


hello ImageStoreConnectionString hello 叢集資訊清單中找到：

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

請參閱[hello 映像存放區連接字串了解](service-fabric-image-store-connection-string.md)如需關於 hello 映像存放區，以及映像存放區連接字串的補充資訊。

### <a name="deploy-large-application-package"></a>部署大型應用程式封裝
問題︰大型應用程式套件 (GB 的順序) 的 [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API 逾時。
請嘗試︰
- 使用 `timeout` 參數指定 [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) 方法的較大逾時。 根據預設，hello 逾時為 30 分鐘的時間。
- 請檢查您的來源電腦與叢集之間的 hello 網路連線。 如果 hello 連接相當緩慢，請考慮使用較佳的網路連線的機器。
如果 hello 用戶端電腦 hello 叢集以外的另一個區域中，請考慮在接近或相同區域內的用戶端電腦使用為 hello 叢集。
- 請檢查是否到達外部節流。 例如，設定的 toouse azure 儲存體 hello 映像存放區時，可能會進行節流處理上傳。

問題︰上傳套件順利完成，但 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 逾時。請嘗試︰
- [壓縮 hello 封裝](service-fabric-package-apps.md#compress-a-package)複製 toohello 映像存放區之前。
hello 壓縮會減少 hello 大小，必須執行 hello 檔案數目，而後者可減少流量的 hello 數量和使用該服務的網狀架構。 hello 上傳作業可能會變慢 （特別是如果您包含 hello 壓縮時間），但註冊和取消註冊 hello 應用程式類型時，速度加快。
- 使用 `timeout` 參數為 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 指定較大的逾時。

### <a name="deploy-application-package-with-many-files"></a>部署具有很多檔案的應用程式封裝
問題︰具有很多檔案的應用程式套件 (以千計的順序) [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) 的逾時。
請嘗試︰
- [壓縮 hello 封裝](service-fabric-package-apps.md#compress-a-package)複製 toohello 映像存放區之前。 hello 壓縮會減少檔案的 hello 數目。
- 使用 `timeout` 參數指定 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) 的較大逾時。

## <a name="code-example"></a>程式碼範例
hello 下列範例複製應用程式封裝 toohello 映像存放區、 佈建新的 hello 應用程式類型，建立應用程式執行個體、 建立服務執行個體，移除 hello 應用程式執行個體，解除佈建 hello 應用程式類型，以及從 hello 映像存放區刪除 hello 應用程式套件。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>後續步驟
[Service Fabric 應用程式升級](service-fabric-application-upgrade.md)

[Service Fabric 健康狀態簡介](service-fabric-health-introduction.md)

[診斷和疑難排解 Service Fabric 服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[在 Service Fabric 中模型化應用程式](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
