---
title: "服務網狀架構裝載模型 aaaAzure |Microsoft 文件"
description: "說明已部署之 Servic Fabric 的複本 (或執行個體) 與服務主機處理序之間的關聯性。"
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Service Fabric 主控模型
這篇文章提供應用程式裝載服務網狀架構所提供的模型的概觀，並描述 hello 差異 hello**共用程序**和**獨佔的程序**模型。 本主題描述 Service Fabric 節點和複本 （或執行個體） 的 hello 服務和 hello 服務主機處理序之間的關聯性上部署的應用程式的外觀。

在進一步進行之前，請確定您熟悉 [Service Fabric 應用程式模型][a1]，並了解它們之間的各種概念與關聯性。 

> [!NOTE]
> 在本文中，為了簡單起見，除非明確指出，否則：
>
> - 使用 word 的所有*複本*參考 tooboth 具狀態的服務或 statless 服務的執行個體的複本。
> - *CodePackage*太視為對等項目*ServiceHost*註冊的處理序*ServiceType*與服務的主機複本*ServiceType*.
>

toounderstand hello 裝載模型，讓我們逐步解說的範例。 假設我們有一個 *ApplicationType* 'MyAppType'，其 *ServiceType* 為 'MyServiceType' 並且是由 *ServicePackage* 'MyServicePackage' 所提供，而此 ServicePackage 具有一個會在執行時註冊 *ServiceType* 'MyServiceType' 的 *CodePackage* 'MyCodePackage'。

假設我們有一個含有 3 個節點的叢集，並且建立一個類型為 'MyAppType' 的「應用程式」**fabric:/App1**。 在這個「應用程式」**fabric:/App1** 中，我們會建立一個類型為 'MyServiceType' 的服務 **fabric:/App1/ServiceA**，此服務具有 2 個分割區 (即 **P1** & **P2**) 且每一分割區有 3 個複本。 hello 下列圖表顯示最後會 hello 檢視此應用程式，因為它已部署的節點上。

<center>
![已部署之應用程式的節點檢視][node-view-one]
</center>

Service Fabric 啟動 'MyServicePackage' 啟動 'MyCodePackage'，也就是裝載來自兩個 hello 資料分割複本**P1** & **P2**。 請注意 hello 叢集中的所有 hello 節點將會都有相同的檢視，因為我們選擇 hello 叢集中的每個磁碟分割等於 toonumber 節點的複本數目。 讓我們在應用程式 **fabric:/App1** 中建立另一個服務 **fabric:/App1/ServiceB**，此服務具有 1 個分割區 (即 **P3**) 且每一分割區有 3 個複本。 下圖顯示 hello hello 節點上新的檢視：

<center>
![已部署之應用程式的節點檢視][node-view-two]
</center>

我們可以看到 Service Fabric 放置 hello 新磁碟分割複本**P3**服務的**fabric: / App1/ServiceB** hello 現有啟用的 'MyServicePackage' 中。 現在，讓我們建立另一個 'MyAppType' 類型的「應用程式」**fabric:/App2**，並在 **fabric:/App2** 中建立服務 **fabric:/App2/ServiceA**，此服務具有 2 個分割區 (即 **P4** & **P5**) 且每一分割區有 3 個複本。 下列圖表顯示新節點檢視 hello:

<center>
![已部署之應用程式的節點檢視][node-view-three]
</center>

這次 Service Fabric 啟用了一份新的 'MyServicePackage'，這個 'MyServicePackage' 會啟動一份新的 'MyCodePackage'，而來自服務 **fabric:/App2/ServiceA** 之兩個分割區 (即 **P4** & **P5**) 的複本則會放在這份新的 'MyCodePackage' 中。

## <a name="shared-process-model"></a>共用處理序模型
我們看到上述 hello 預設裝載服務的網狀架構所提供的模型，也稱為 tooas**共用程序**模型。 在此模型中，針對給定*應用程式*，只有一個副本給定*ServicePackage*上啟動*節點*(以便啟動所有的 hello *CodePackages*包含) 和所有 hello 複本的所有服務的給定*ServiceType*會放在 hello *CodePackage* ，該別名登錄*ServiceType*. 換句話說，所有 hello 的所有服務的複本時指定*ServiceType*共用 hello 相同的程序。

## <a name="exclusive-process-model"></a>專屬處理序模型
hello Service Fabric 所提供其他裝載模型是**獨佔的程序**模型。 在此模型中，在給定*節點*，放置每個複本，Service Fabric 啟動的新副本*ServicePackage* (以便啟動所有的 hello *CodePackages*其包含的)，而複本放在 hello *CodePackage*該註冊的 hello *ServiceType*複本所屬的 hello 服務 toowhich。 換句話說，每個複本都存在於自己的專屬處理序中。 

從 Service Fabric 5.6 版開始即支援此模型。 **排除處理程序**模型可以選擇建立 hello 服務的 hello 次 (使用[PowerShell][p1]， [REST] [ r1]或[FabricClient][c1]) 藉由指定**ServicePackageActivationMode**為 'ExclusiveProcess'。

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

如果您的應用程式資訊清單中有預設的服務，您可以依以下所示的方式指定 **ServicePackageActivationMode** 屬性，來選擇「專屬處理序」模型：

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
繼續上述範例中，讓我們建立另一個服務**網狀架構: / App1/ServiceC**應用程式中**fabric: / App1**具有 2 個資料分割 (假設**P6**  &  **P7**) 和每個資料分割具有 3 個複本**ServicePackageActivationMode**設定 too'ExclusiveProcess'。 下圖顯示 hello 節點上新的檢視：

<center>
![已部署之應用程式的節點檢視][node-view-four]
</center>

如您所見，Service Fabric 啟用了兩份新的 'MyServicePackage' (針對來自分割區 **P6** & **P7** 的每個複本各啟用一份)，並將每個複本放在其專用的一份 *CodePackage* 中。 另一件事 toonote 這裡是，當**獨佔的程序**使用模型時，針對給定*應用程式*的多份複本指定*ServicePackage* 上作用中*節點*。 在上述範例中，我們看到 **fabric:/App1** 有三份作用中的 'MyServicePackage'。 這每一份作用中的 'MyServicePackage' 都有相關的 **ServicePackageAtivationId**，用來作為它們在「應用程式」**fabric:/App1** 中的身分識別。

如果針對「應用程式」(例如上述範例中的 **fabric:/App2**) 只使用「共用處理序」模型，則一個「節點」上只會有一份作用中 *ServicePackage*，而這個 *ServicePackage* 啟用項的 **ServicePackageAtivationId** 則會是「空字串」。

> [!NOTE]
>- **共用處理程序**裝載模型對應太**ServicePackageAtivationMode**等於**SharedProcess**。 這是 hello 裝載模型的預設值和**ServicePackageAtivationMode**不需要指定在建立 hello 服務的 hello 階段。
>
>- **排除處理程序**裝載模型對應太**ServicePackageAtivationMode**等於**ExclusiveProcess** ，而且需要明確指定在 hello 建立 hello toobe服務。 
>
>- 藉由查詢 hello 已知服務的裝載模型[服務描述][ p2]並查看值**ServicePackageAtivationMode**。
>
>

## <a name="working-with-deployed-service-package"></a>使用已部署的服務套件
節點上一份作用中的 *ServicePackage* 稱為[已部署的服務套件][p3]。 如前所述，當**獨佔的程序**模型用於建立服務，指定*應用程式*，可能有多個已部署的服務封裝 hello 相同*ServicePackage*。 在執行作業時要特定 toodeployed 服務封裝[報告已部署的服務封裝健全狀況][ p4]或[重新啟動已部署的服務封裝的程式碼封裝][ p5]等等**ServicePackageActivationId**需求 toobe 提供 tooidentify 特定部署的服務封裝。

 **ServicePackageActivationId**已部署的服務封裝可取得透過查詢 hello 清單[部署服務套件][ p3]節點上。 當查詢[部署的服務型別][p6]，[部署複本][ p7]和[部署的程式碼封裝] [ p8]節點上，hello 查詢結果也包含 hello **ServicePackageActivationId**父系已部署服務封裝。

> [!NOTE]
>- 在「共用處理序」主控模型下，於指定的「節點」上，針對指定的「應用程式」，只會啟用一份 *ServicePackage*。 它有**ServicePackageActivationId**太等於*空字串*並不需要指定時執行的已部署的服務套件相關作業。 
>
> - 在「專屬處理序」主控模型下，於指定的「節點」上，針對指定的「應用程式」，會有一或多份作用中的 *ServicePackage*。 每個啟用具有*非空白* **ServicePackageActivationId**且需要 toobe 指定，但執行已部署的服務套件相關作業。 
>
> - 如果**ServicePackageActivationId**是 ommited 預設 too'empty 字串 '。 如果已部署的服務封裝，已啟用下**共用程序**模型已存在，則會執行作業，否則 hello 作業將會失敗。
>
> - 建議您不要一次 tooquery 和快取**ServicePackageActivationId**因為它動態產生，而且因為各種原因而可以變更。 之前執行的作業會需要**ServicePackageActivationId**，您應該先查詢 hello 清單[部署服務套件][ p3]上的節點，然後使用*ServicePackageActivationId** 從查詢結果 tooperform hello 原始作業。
>
>

## <a name="guest-executable-and-container-applications"></a>客體可執行檔和容器應用程式
Service Fabric 會將[客體可執行檔][a2]和[容器][a3]應用程式視為獨立的無狀態服務，亦即 *ServiceHost* (一個處理序或容器) 中沒有任何 Service Fabric 執行階段。 由於這些服務是獨立的，因此每一 *ServiceHost* 的複本數並不適用於這些服務。 hello 與這些服務使用的最常見組態是單一資料分割與[InstanceCount] [ c2]等於太是-1 （也就是一份 hello 叢集的每個節點上執行的服務程式碼）。 

hello 預設**ServicePackageActivationMode**對於這些服務是**SharedProcess** Service Fabric 這種情況下只能啟動一份*ServicePackage*上*節點*針對給定*應用程式*這表示只能有一個複本的服務程式碼會執行*節點*。 如果您要多份您的服務程式碼 toorun*節點*當您建立多個服務 (*Service1*太*ServiceN*) 的*ServiceType*(指定在*ServiceManifest*) 或當您的服務是多重資料分割，您應該指定**ServicePackageActivationMode**為**ExclusiveProcess**建立 hello 服務的 hello 次。

## <a name="changing-hosting-model-of-an-existing-service"></a>變更現有服務的主控模型
變更從現有服務的裝載模型**共用程序**太**獨佔的程序**，反之亦然透過升級或更新機制 （或在預設服務應用程式中的規格目前不支援資訊清單）。 在未來的版本中將會新增此功能。

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>在共用處理序與專屬處理序模型之間做選擇
這些裝載模型有其優缺點和使用者需要的 tooevaluate 哪一個最符合其需求。 **共用處理程序**模型可讓較佳的 OS 資源使用率，因為會產生較少的處理程序，在多個複本 hello 相同處理程序可以共用連接埠等。不過，如果其中一個 hello 複本叫用它需要 toobring hello 服務主機關閉的其中一個錯誤時，它會影響相同的程序中的所有其他複本。

 「專屬處理序」模型會讓每個複本處於自己的處理序中，而可提供較佳的隔離，發生問題的複本將不會影響到其他複本。 它派上用場的情況下，連接埠共用不支援 hello 通訊協定。 它能 hello 能力 tooapply 資源控管在複本層級。 在 hello 相反地，**獨佔的程序**會耗用更多 OS 資源，因為它會繁衍 hello 節點上每個複本的其中一個處理序。

## <a name="exclusive-process-model-and-application-model-considerations"></a>專屬處理序眉型和應用程式模型考量
hello 建議的方式 toomodel Service Fabric 應用程式是一個 tookeep *ServiceType*每*ServicePackage*及此模型適用於大部分的 hello 應用程式。 

不過，tooenable 特殊案例一*ServiceType*每*ServicePackage*可能不需要這樣做，在功能上，Service Fabric 允許 toohave 一個以上*ServiceType*每*ServicePackage* (一個*CodePackage*可以註冊多個*ServiceType*)。 以下是一些 hello 案例，這些設定可以是很有用：

- 您想要 toooptimize OS 資源使用率繁衍 （spawn） 較少的處理程序，以及取得每個處理序更高的複本密度。
- 從不同的 ServiceTypes 複本都必須 tooshare 一些常見的資料具有較高的初始化或成本的記憶體。
- 您有可用的服務供應項目，而且您想 tooput 資源使用量的限制將 hello 服務的所有複本放在相同的程序中。

「專屬處理序」主控模型與每一 *ServicePackage* 有多個 *ServiceType* 的應用程式模型並不相同。 這是因為多個*ServiceTypes*每*ServicePackage*是設計的 tooachieve 較高的資源，在複本之間共用，可讓每個處理序更高的複本密度。 這是反對 toowhat**獨佔的程序**模型是設計的 tooachieve。

請考慮多個 hello 情況*ServiceTypes*每*ServicePackage*不同*CodePackage*註冊每個*ServiceType*. 假設我們有一個 *ServicePackage* 'MultiTypeServicePackge'，其中包含兩個 *CodePackage*：

- 註冊 *ServiceType* 'MyServiceTypeA' 的 'MyCodePackageA'。
- 註冊 *ServiceType* 'MyServiceTypeB' 的 'MyCodePackageB'。

現在，假設我們建立一個「應用程式」**fabric:/SpecialApp**，並使用「專屬處理序」模型在 **fabric:/SpecialApp** 中建立下列兩個服務：

- 'MyServiceTypeA' 類型的服務 **fabric:/SpecialApp/ServiceA**，此服務有兩個分割區 (即 **P1** 和 **P2**) 且每一分割區有 3 個複本。
- 'MyServiceTypeB' 類型的服務 **fabric:/SpecialApp/ServiceB**，此服務有兩個分割區 (即 **P3** 和 **P4**) 且每一分割區有 3 個複本。

指定節點上，這兩個 hello 服務會有兩個複本。 因為我們使用**獨佔的程序**模型 toocreate hello 服務，Service Fabric 會啟用 'MyServicePackge' 每個複本的新副本。 每個 'MultiTypeServicePackge' 啟用項都會啟動一份 'MyCodePackageA' 和 'MyCodePackageB'。 不過，'MyCodePackageA' 或 'MyCodePackageB' 其中之一將裝載 hello 複本啟動 'MultiTypeServicePackge' 時。 下圖顯示 hello 節點檢視：

<center>
![已部署之應用程式的節點檢視][node-view-five]
</center>

 我們可以看到中的 'MultiTypeServicePackge' hello 啟用分割區的複本**P1**服務的**fabric: / SpecialApp/Services**，'MyCodePackageA' 裝載 hello 複本和 'MyCodePackageB' 只要啟動並執行。 同樣地，在啟用 'MultiTypeServicePackge' 的分割區的複本**P3**服務的**fabric: / SpecialApp/ServiceB**裝載 hello 複本 'MyCodePackageB'，'MyCodePackageA'只要啟動且正在執行等等。 因此，多 hello 數目*CodePackages* (註冊不同*ServiceTypes*) 每秒*ServicePackage*，更高版本將會是多餘的資源使用狀況。 
 
 在 hello 另一方面，如果我們建立服務**fabric: / SpecialApp/Services**和**網狀架構: / SpecialApp/ServiceB**與**共用程序**模型，Service Fabric 會為啟用 'MultiTypeServicePackge' 只能有一個複本*應用程式* **fabric: / SpecialApp** （如先前所見）。 'MyCodePackageA' 將裝載服務的所有複本**fabric: / SpecialApp/Services** （或任何類型 'MyServiceTypeA' toobe 更精確的服務） 而且 'MyCodePackageB' 會都裝載服務的所有複本**fabric: /SpecialApp/ServiceB** （或任何類型 'MyServiceTypeB' toobe 更精確的服務）。 下圖顯示此設定中的 hello 節點檢視： 

<center>
![已部署之應用程式的節點檢視][node-view-six]
</center>

在上述範例中的 hello，您可能會認為是否 'MyCodePackageA' 註冊 'MyServiceTypeA' 和 'MyServiceTypeB'，而且沒有任何 'MyCodePackageB'，則會有不重複*CodePackage*執行。 這個想法是正確的，不過，如先前所述，此應用程式模型與「專屬處理序」主控模型並不相同。 如果目標是 tooput 每個複本在它自己專用然後對兩者進行註冊的程序*ServiceTypes*來自相同*CodePackage*不需要並將每個放*ServiceType*中自己*ServicePacakge*是較合理的選擇。

## <a name="next-steps"></a>後續步驟
[封裝應用程式][ a4]並取得它準備好 toodeploy。

[部署和移除應用程式][ a5]描述如何 toouse PowerShell toomanage 應用程式執行個體。

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage