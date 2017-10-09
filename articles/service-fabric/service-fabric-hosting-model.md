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
# <a name="service-fabric-hosting-model"></a><span data-ttu-id="1bc17-103">Service Fabric 主控模型</span><span class="sxs-lookup"><span data-stu-id="1bc17-103">Service Fabric hosting model</span></span>
<span data-ttu-id="1bc17-104">這篇文章提供應用程式裝載服務網狀架構所提供的模型的概觀，並描述 hello 差異 hello**共用程序**和**獨佔的程序**模型。</span><span class="sxs-lookup"><span data-stu-id="1bc17-104">This article provides an overview of application hosting models provided by Service Fabric, and describes hello differences between hello **Shared Process** and **Exclusive Process** models.</span></span> <span data-ttu-id="1bc17-105">本主題描述 Service Fabric 節點和複本 （或執行個體） 的 hello 服務和 hello 服務主機處理序之間的關聯性上部署的應用程式的外觀。</span><span class="sxs-lookup"><span data-stu-id="1bc17-105">It describes how a deployed application looks on a Service Fabric node and relationship between replicas (or instances) of hello service and hello service-host process.</span></span>

<span data-ttu-id="1bc17-106">在進一步進行之前，請確定您熟悉 [Service Fabric 應用程式模型][a1]，並了解它們之間的各種概念與關聯性。</span><span class="sxs-lookup"><span data-stu-id="1bc17-106">Before proceeding further, make sure that you are familiar with [Service Fabric Application Model][a1] and understand various concepts and relation among them.</span></span> 

> [!NOTE]
> <span data-ttu-id="1bc17-107">在本文中，為了簡單起見，除非明確指出，否則：</span><span class="sxs-lookup"><span data-stu-id="1bc17-107">In this article, for simplicity, unless explicitly mentioned:</span></span>
>
> - <span data-ttu-id="1bc17-108">使用 word 的所有*複本*參考 tooboth 具狀態的服務或 statless 服務的執行個體的複本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-108">All uses of word *replica* refers tooboth a replica of a stateful service or an instance of a statless service.</span></span>
> - <span data-ttu-id="1bc17-109">*CodePackage*太視為對等項目*ServiceHost*註冊的處理序*ServiceType*與服務的主機複本*ServiceType*.</span><span class="sxs-lookup"><span data-stu-id="1bc17-109">*CodePackage* is treated equivalent too*ServiceHost* process that registers a *ServiceType* and hosts replicas of services of that *ServiceType*.</span></span>
>

<span data-ttu-id="1bc17-110">toounderstand hello 裝載模型，讓我們逐步解說的範例。</span><span class="sxs-lookup"><span data-stu-id="1bc17-110">toounderstand hello hosting model, let us walk through an example.</span></span> <span data-ttu-id="1bc17-111">假設我們有一個 *ApplicationType* 'MyAppType'，其 *ServiceType* 為 'MyServiceType' 並且是由 *ServicePackage* 'MyServicePackage' 所提供，而此 ServicePackage 具有一個會在執行時註冊 *ServiceType* 'MyServiceType' 的 *CodePackage* 'MyCodePackage'。</span><span class="sxs-lookup"><span data-stu-id="1bc17-111">Let us say, we have an *ApplicationType* 'MyAppType' which has a *ServiceType* 'MyServiceType' which is provided by *ServicePackage* 'MyServicePackage' which has a *CodePackage* 'MyCodePackage' which registers *ServiceType* 'MyServiceType' when it runs.</span></span>

<span data-ttu-id="1bc17-112">假設我們有一個含有 3 個節點的叢集，並且建立一個類型為 'MyAppType' 的「應用程式」**fabric:/App1**。</span><span class="sxs-lookup"><span data-stu-id="1bc17-112">Let's say we have a 3 node cluster and we create an *application* **fabric:/App1** of type 'MyAppType'.</span></span> <span data-ttu-id="1bc17-113">在這個「應用程式」**fabric:/App1** 中，我們會建立一個類型為 'MyServiceType' 的服務 **fabric:/App1/ServiceA**，此服務具有 2 個分割區 (即 **P1** & **P2**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-113">Inside this *application* **fabric:/App1** we create a service **fabric:/App1/ServiceA** of type 'MyServiceType' which has 2 partitions (say **P1** & **P2**) and 3 replicas per partition.</span></span> <span data-ttu-id="1bc17-114">hello 下列圖表顯示最後會 hello 檢視此應用程式，因為它已部署的節點上。</span><span class="sxs-lookup"><span data-stu-id="1bc17-114">hello following diagram shows hello view of this application as it ends up deployed on a node.</span></span>

<span data-ttu-id="1bc17-115"><center>
![已部署之應用程式的節點檢視][node-view-one]
</center></span><span class="sxs-lookup"><span data-stu-id="1bc17-115"><center>
![Node view of deployed application][node-view-one]
</center></span></span>

<span data-ttu-id="1bc17-116">Service Fabric 啟動 'MyServicePackage' 啟動 'MyCodePackage'，也就是裝載來自兩個 hello 資料分割複本**P1** & **P2**。</span><span class="sxs-lookup"><span data-stu-id="1bc17-116">Service Fabric activated 'MyServicePackage' which started 'MyCodePackage' which is hosting replicas from both hello partitions i.e. **P1** & **P2**.</span></span> <span data-ttu-id="1bc17-117">請注意 hello 叢集中的所有 hello 節點將會都有相同的檢視，因為我們選擇 hello 叢集中的每個磁碟分割等於 toonumber 節點的複本數目。</span><span class="sxs-lookup"><span data-stu-id="1bc17-117">Note that all hello nodes in hello cluster will have same view since we chose number of replicas per partition equal toonumber of nodes in hello cluster.</span></span> <span data-ttu-id="1bc17-118">讓我們在應用程式 **fabric:/App1** 中建立另一個服務 **fabric:/App1/ServiceB**，此服務具有 1 個分割區 (即 **P3**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-118">Let's create another service **fabric:/App1/ServiceB** in application **fabric:/App1** which has 1 partition (say **P3**) and 3 replicas per partition.</span></span> <span data-ttu-id="1bc17-119">下圖顯示 hello hello 節點上新的檢視：</span><span class="sxs-lookup"><span data-stu-id="1bc17-119">Following diagram shows hello new view on hello node:</span></span>

<span data-ttu-id="1bc17-120"><center>
![已部署之應用程式的節點檢視][node-view-two]
</center></span><span class="sxs-lookup"><span data-stu-id="1bc17-120"><center>
![Node view of deployed application][node-view-two]
</center></span></span>

<span data-ttu-id="1bc17-121">我們可以看到 Service Fabric 放置 hello 新磁碟分割複本**P3**服務的**fabric: / App1/ServiceB** hello 現有啟用的 'MyServicePackage' 中。</span><span class="sxs-lookup"><span data-stu-id="1bc17-121">As we can see Service Fabric placed hello new replica for partition **P3** of service **fabric:/App1/ServiceB** in hello existing activation of 'MyServicePackage'.</span></span> <span data-ttu-id="1bc17-122">現在，讓我們建立另一個 'MyAppType' 類型的「應用程式」**fabric:/App2**，並在 **fabric:/App2** 中建立服務 **fabric:/App2/ServiceA**，此服務具有 2 個分割區 (即 **P4** & **P5**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-122">Now lets create another *application* **fabric:/App2** of type 'MyAppType' and inside **fabric:/App2** create service **fabric:/App2/ServiceA** which has 2 partitions (say **P4** & **P5**) and 3 replicas per partition.</span></span> <span data-ttu-id="1bc17-123">下列圖表顯示新節點檢視 hello:</span><span class="sxs-lookup"><span data-stu-id="1bc17-123">Following diagrams shows hello new node view:</span></span>

<span data-ttu-id="1bc17-124"><center>
![已部署之應用程式的節點檢視][node-view-three]
</center></span><span class="sxs-lookup"><span data-stu-id="1bc17-124"><center>
![Node view of deployed application][node-view-three]
</center></span></span>

<span data-ttu-id="1bc17-125">這次 Service Fabric 啟用了一份新的 'MyServicePackage'，這個 'MyServicePackage' 會啟動一份新的 'MyCodePackage'，而來自服務 **fabric:/App2/ServiceA** 之兩個分割區 (即 **P4** & **P5**) 的複本則會放在這份新的 'MyCodePackage' 中。</span><span class="sxs-lookup"><span data-stu-id="1bc17-125">This time Service Fabric has activated a new copy of 'MyServicePackage' which starts a new copy of 'MyCodePackage' and replicas from both partitions of service **fabric:/App2/ServiceA** (i.e. **P4** & **P5**) are placed in this new copy 'MyCodePackage'.</span></span>

## <a name="shared-process-model"></a><span data-ttu-id="1bc17-126">共用處理序模型</span><span class="sxs-lookup"><span data-stu-id="1bc17-126">Shared process model</span></span>
<span data-ttu-id="1bc17-127">我們看到上述 hello 預設裝載服務的網狀架構所提供的模型，也稱為 tooas**共用程序**模型。</span><span class="sxs-lookup"><span data-stu-id="1bc17-127">What we saw above is hello default hosting model provided by Service Fabric and is referred tooas **Shared Process** model.</span></span> <span data-ttu-id="1bc17-128">在此模型中，針對給定*應用程式*，只有一個副本給定*ServicePackage*上啟動*節點*(以便啟動所有的 hello *CodePackages*包含) 和所有 hello 複本的所有服務的給定*ServiceType*會放在 hello *CodePackage* ，該別名登錄*ServiceType*.</span><span class="sxs-lookup"><span data-stu-id="1bc17-128">In this model, for a given *application*, only one copy of a given *ServicePackage* is activated on a *Node* (which starts all hello *CodePackages* contained in it) and all hello replicas of all services of a given  *ServiceType* are placed in hello *CodePackage* that registers that *ServiceType*.</span></span> <span data-ttu-id="1bc17-129">換句話說，所有 hello 的所有服務的複本時指定*ServiceType*共用 hello 相同的程序。</span><span class="sxs-lookup"><span data-stu-id="1bc17-129">In other words, all hello replicas of all services of a given *ServiceType* share hello same process.</span></span>

## <a name="exclusive-process-model"></a><span data-ttu-id="1bc17-130">專屬處理序模型</span><span class="sxs-lookup"><span data-stu-id="1bc17-130">Exclusive process model</span></span>
<span data-ttu-id="1bc17-131">hello Service Fabric 所提供其他裝載模型是**獨佔的程序**模型。</span><span class="sxs-lookup"><span data-stu-id="1bc17-131">hello other hosting model provided by Service Fabric is **Exclusive Process** model.</span></span> <span data-ttu-id="1bc17-132">在此模型中，在給定*節點*，放置每個複本，Service Fabric 啟動的新副本*ServicePackage* (以便啟動所有的 hello *CodePackages*其包含的)，而複本放在 hello *CodePackage*該註冊的 hello *ServiceType*複本所屬的 hello 服務 toowhich。</span><span class="sxs-lookup"><span data-stu-id="1bc17-132">In this model, on a given *Node*, for placing each replica, Service Fabric activates a new copy of *ServicePackage* (which starts all hello *CodePackages* contained in it) and replica is placed in hello *CodePackage* that registered hello *ServiceType* of hello service toowhich replica belongs.</span></span> <span data-ttu-id="1bc17-133">換句話說，每個複本都存在於自己的專屬處理序中。</span><span class="sxs-lookup"><span data-stu-id="1bc17-133">In other words, each replica lives in its own dedicated process.</span></span> 

<span data-ttu-id="1bc17-134">從 Service Fabric 5.6 版開始即支援此模型。</span><span class="sxs-lookup"><span data-stu-id="1bc17-134">This model is supported starting version 5.6 of Service Fabric.</span></span> <span data-ttu-id="1bc17-135">**排除處理程序**模型可以選擇建立 hello 服務的 hello 次 (使用[PowerShell][p1]， [REST] [ r1]或[FabricClient][c1]) 藉由指定**ServicePackageActivationMode**為 'ExclusiveProcess'。</span><span class="sxs-lookup"><span data-stu-id="1bc17-135">**Exclusive Process** model can be chosen at hello time of creating hello service (using [PowerShell][p1], [REST][r1] or [FabricClient][c1]) by specifying **ServicePackageActivationMode** as 'ExclusiveProcess'.</span></span>

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

<span data-ttu-id="1bc17-136">如果您的應用程式資訊清單中有預設的服務，您可以依以下所示的方式指定 **ServicePackageActivationMode** 屬性，來選擇「專屬處理序」模型：</span><span class="sxs-lookup"><span data-stu-id="1bc17-136">If you have a default service in your application manifest, you can choose **Exclusive Process** model by specifying **ServicePackageActivationMode** attribute as shown below:</span></span>

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
<span data-ttu-id="1bc17-137">繼續上述範例中，讓我們建立另一個服務**網狀架構: / App1/ServiceC**應用程式中**fabric: / App1**具有 2 個資料分割 (假設**P6**  &  **P7**) 和每個資料分割具有 3 個複本**ServicePackageActivationMode**設定 too'ExclusiveProcess'。</span><span class="sxs-lookup"><span data-stu-id="1bc17-137">Continuing with our example above, lets create another service **fabric:/App1/ServiceC** in application **fabric:/App1** which has 2 partitions (say **P6** & **P7**) and 3 replicas per partition with **ServicePackageActivationMode** set too'ExclusiveProcess'.</span></span> <span data-ttu-id="1bc17-138">下圖顯示 hello 節點上新的檢視：</span><span class="sxs-lookup"><span data-stu-id="1bc17-138">Following diagram shows new view on hello node:</span></span>

<span data-ttu-id="1bc17-139"><center>
![已部署之應用程式的節點檢視][node-view-four]
</center></span><span class="sxs-lookup"><span data-stu-id="1bc17-139"><center>
![Node view of deployed application][node-view-four]
</center></span></span>

<span data-ttu-id="1bc17-140">如您所見，Service Fabric 啟用了兩份新的 'MyServicePackage' (針對來自分割區 **P6** & **P7** 的每個複本各啟用一份)，並將每個複本放在其專用的一份 *CodePackage* 中。</span><span class="sxs-lookup"><span data-stu-id="1bc17-140">As you can see, Service Fabric activated two new copies of 'MyServicePackage' (one for each replica from partition **P6** & **P7**) and placed each replica in its dedicated copy of *CodePackage*.</span></span> <span data-ttu-id="1bc17-141">另一件事 toonote 這裡是，當**獨佔的程序**使用模型時，針對給定*應用程式*的多份複本指定*ServicePackage* 上作用中*節點*。</span><span class="sxs-lookup"><span data-stu-id="1bc17-141">Another thing toonote here is, when **Exclusive Process** model is used, for a given *application*, multiple copies of a given *ServicePackage* can be active on a *Node*.</span></span> <span data-ttu-id="1bc17-142">在上述範例中，我們看到 **fabric:/App1** 有三份作用中的 'MyServicePackage'。</span><span class="sxs-lookup"><span data-stu-id="1bc17-142">In above example, we see that three copies of 'MyServicePackage' are active for **fabric:/App1**.</span></span> <span data-ttu-id="1bc17-143">這每一份作用中的 'MyServicePackage' 都有相關的 **ServicePackageAtivationId**，用來作為它們在「應用程式」**fabric:/App1** 中的身分識別。</span><span class="sxs-lookup"><span data-stu-id="1bc17-143">Each of these active copies of 'MyServicePackage' has a **ServicePackageAtivationId** associated with it which identifies that copy within *application* **fabric:/App1**.</span></span>

<span data-ttu-id="1bc17-144">如果針對「應用程式」(例如上述範例中的 **fabric:/App2**) 只使用「共用處理序」模型，則一個「節點」上只會有一份作用中 *ServicePackage*，而這個 *ServicePackage* 啟用項的 **ServicePackageAtivationId** 則會是「空字串」。</span><span class="sxs-lookup"><span data-stu-id="1bc17-144">When only **Shared Process** model is used for an *application*, like **fabric:/App2** in above example, there is only one active copy of *ServicePackage* on a *Node* and **ServicePackageAtivationId** for this activation of *ServicePackage* is 'empty string'.</span></span>

> [!NOTE]
>- <span data-ttu-id="1bc17-145">**共用處理程序**裝載模型對應太**ServicePackageAtivationMode**等於**SharedProcess**。</span><span class="sxs-lookup"><span data-stu-id="1bc17-145">**Shared Process** hosting model corresponds too**ServicePackageAtivationMode** equal **SharedProcess**.</span></span> <span data-ttu-id="1bc17-146">這是 hello 裝載模型的預設值和**ServicePackageAtivationMode**不需要指定在建立 hello 服務的 hello 階段。</span><span class="sxs-lookup"><span data-stu-id="1bc17-146">This is hello default hosting model and **ServicePackageAtivationMode** need not be specified at hello time of creating hello service.</span></span>
>
>- <span data-ttu-id="1bc17-147">**排除處理程序**裝載模型對應太**ServicePackageAtivationMode**等於**ExclusiveProcess** ，而且需要明確指定在 hello 建立 hello toobe服務。</span><span class="sxs-lookup"><span data-stu-id="1bc17-147">**Exclusive Process** hosting model corresponds too**ServicePackageAtivationMode** equal **ExclusiveProcess** and need toobe explicitly specified at hello time of creating hello service.</span></span> 
>
>- <span data-ttu-id="1bc17-148">藉由查詢 hello 已知服務的裝載模型[服務描述][ p2]並查看值**ServicePackageAtivationMode**。</span><span class="sxs-lookup"><span data-stu-id="1bc17-148">Hosting model of a service can be known by querying hello [service description][p2] and looking at value of **ServicePackageAtivationMode**.</span></span>
>
>

## <a name="working-with-deployed-service-package"></a><span data-ttu-id="1bc17-149">使用已部署的服務套件</span><span class="sxs-lookup"><span data-stu-id="1bc17-149">Working with deployed service package</span></span>
<span data-ttu-id="1bc17-150">節點上一份作用中的 *ServicePackage* 稱為[已部署的服務套件][p3]。</span><span class="sxs-lookup"><span data-stu-id="1bc17-150">An active copy of a *ServicePackage* on a node is referred as [deployed service package][p3].</span></span> <span data-ttu-id="1bc17-151">如前所述，當**獨佔的程序**模型用於建立服務，指定*應用程式*，可能有多個已部署的服務封裝 hello 相同*ServicePackage*。</span><span class="sxs-lookup"><span data-stu-id="1bc17-151">As previously mentioned above, when **Exclusive Process** model is used for creating services, for a given *application*, there could be multiple deployed service packages for hello same *ServicePackage*.</span></span> <span data-ttu-id="1bc17-152">在執行作業時要特定 toodeployed 服務封裝[報告已部署的服務封裝健全狀況][ p4]或[重新啟動已部署的服務封裝的程式碼封裝][ p5]等等**ServicePackageActivationId**需求 toobe 提供 tooidentify 特定部署的服務封裝。</span><span class="sxs-lookup"><span data-stu-id="1bc17-152">While performing operations specific toodeployed service package like [reporting health of a deployed service package][p4] or [restarting code package of a deployed service package][p5] etc., **ServicePackageActivationId** needs toobe provided tooidentify a specific deployed service package.</span></span>

 <span data-ttu-id="1bc17-153">**ServicePackageActivationId**已部署的服務封裝可取得透過查詢 hello 清單[部署服務套件][ p3]節點上。</span><span class="sxs-lookup"><span data-stu-id="1bc17-153">**ServicePackageActivationId** of a deployed service package can be obtained by querying hello list of [deployed service packages][p3] on a node.</span></span> <span data-ttu-id="1bc17-154">當查詢[部署的服務型別][p6]，[部署複本][ p7]和[部署的程式碼封裝] [ p8]節點上，hello 查詢結果也包含 hello **ServicePackageActivationId**父系已部署服務封裝。</span><span class="sxs-lookup"><span data-stu-id="1bc17-154">When querying [deployed service types][p6], [deployed replicas][p7] and [deployed code packages][p8] on a node, hello query result also contains hello **ServicePackageActivationId** of parent deployed service package.</span></span>

> [!NOTE]
>- <span data-ttu-id="1bc17-155">在「共用處理序」主控模型下，於指定的「節點」上，針對指定的「應用程式」，只會啟用一份 *ServicePackage*。</span><span class="sxs-lookup"><span data-stu-id="1bc17-155">Under **Shared Process** hosting model, on a given *node*, for a given *application*, only one copy of a *ServicePackage* is activated.</span></span> <span data-ttu-id="1bc17-156">它有**ServicePackageActivationId**太等於*空字串*並不需要指定時執行的已部署的服務套件相關作業。</span><span class="sxs-lookup"><span data-stu-id="1bc17-156">It has **ServicePackageActivationId** equal too*empty string* and need not be specified while performing deployed service package related operations.</span></span> 
>
> - <span data-ttu-id="1bc17-157">在「專屬處理序」主控模型下，於指定的「節點」上，針對指定的「應用程式」，會有一或多份作用中的 *ServicePackage*。</span><span class="sxs-lookup"><span data-stu-id="1bc17-157">Under **Exclusive Process** hosting model, on a given *node*, for a given *application*, one or more copies of a *ServicePackage* can be active.</span></span> <span data-ttu-id="1bc17-158">每個啟用具有*非空白* **ServicePackageActivationId**且需要 toobe 指定，但執行已部署的服務套件相關作業。</span><span class="sxs-lookup"><span data-stu-id="1bc17-158">Each activation has a *non-empty* **ServicePackageActivationId** and needs toobe specified while performing deployed service package related operations.</span></span> 
>
> - <span data-ttu-id="1bc17-159">如果**ServicePackageActivationId**是 ommited 預設 too'empty 字串 '。</span><span class="sxs-lookup"><span data-stu-id="1bc17-159">If **ServicePackageActivationId** is ommited it defaults too'empty string'.</span></span> <span data-ttu-id="1bc17-160">如果已部署的服務封裝，已啟用下**共用程序**模型已存在，則會執行作業，否則 hello 作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="1bc17-160">If a deployed service package that was activated under **Shared Process** model is present, then operation will be performed on it, otherwise hello operation will fail.</span></span>
>
> - <span data-ttu-id="1bc17-161">建議您不要一次 tooquery 和快取**ServicePackageActivationId**因為它動態產生，而且因為各種原因而可以變更。</span><span class="sxs-lookup"><span data-stu-id="1bc17-161">It is not recommended tooquery once and cache **ServicePackageActivationId** as it is dynamically generated and can change for various reasons.</span></span> <span data-ttu-id="1bc17-162">之前執行的作業會需要**ServicePackageActivationId**，您應該先查詢 hello 清單[部署服務套件][ p3]上的節點，然後使用*ServicePackageActivationId** 從查詢結果 tooperform hello 原始作業。</span><span class="sxs-lookup"><span data-stu-id="1bc17-162">Before performing an operation that needs **ServicePackageActivationId**, you should first query hello list of [deployed service packages][p3] on a node and then use *ServicePackageActivationId** from query result tooperform hello original operation.</span></span>
>
>

## <a name="guest-executable-and-container-applications"></a><span data-ttu-id="1bc17-163">客體可執行檔和容器應用程式</span><span class="sxs-lookup"><span data-stu-id="1bc17-163">Guest executable and container applications</span></span>
<span data-ttu-id="1bc17-164">Service Fabric 會將[客體可執行檔][a2]和[容器][a3]應用程式視為獨立的無狀態服務，亦即 *ServiceHost* (一個處理序或容器) 中沒有任何 Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="1bc17-164">Service Fabric treats [Guest executable][a2] and [container][a3] applications as statless services which are self-contained i.e. there is no Service Fabric runtime in *ServiceHost* (a process or container).</span></span> <span data-ttu-id="1bc17-165">由於這些服務是獨立的，因此每一 *ServiceHost* 的複本數並不適用於這些服務。</span><span class="sxs-lookup"><span data-stu-id="1bc17-165">Since these services are self-contained, number of replicas per *ServiceHost* is not applicable for these services.</span></span> <span data-ttu-id="1bc17-166">hello 與這些服務使用的最常見組態是單一資料分割與[InstanceCount] [ c2]等於太是-1 （也就是一份 hello 叢集的每個節點上執行的服務程式碼）。</span><span class="sxs-lookup"><span data-stu-id="1bc17-166">hello most common configuration used with these services is single-partition with [InstanceCount][c2] equal too-1 (i.e. one copy of hello service code running on each node of cluster).</span></span> 

<span data-ttu-id="1bc17-167">hello 預設**ServicePackageActivationMode**對於這些服務是**SharedProcess** Service Fabric 這種情況下只能啟動一份*ServicePackage*上*節點*針對給定*應用程式*這表示只能有一個複本的服務程式碼會執行*節點*。</span><span class="sxs-lookup"><span data-stu-id="1bc17-167">hello default **ServicePackageActivationMode** for these services is **SharedProcess** in which case Service Fabric only activates one copy of *ServicePackage* on a *Node* for a given *application* which means only one copy of service code will run a *Node*.</span></span> <span data-ttu-id="1bc17-168">如果您要多份您的服務程式碼 toorun*節點*當您建立多個服務 (*Service1*太*ServiceN*) 的*ServiceType*(指定在*ServiceManifest*) 或當您的服務是多重資料分割，您應該指定**ServicePackageActivationMode**為**ExclusiveProcess**建立 hello 服務的 hello 次。</span><span class="sxs-lookup"><span data-stu-id="1bc17-168">If you want multiple copies of your service code toorun on a *Node* when you create multiple services (*Service1* too*ServiceN*) of *ServiceType* (specified in *ServiceManifest*) or when your service is multi-partitioned, you should specify **ServicePackageActivationMode** as **ExclusiveProcess** at hello time of creating hello service.</span></span>

## <a name="changing-hosting-model-of-an-existing-service"></a><span data-ttu-id="1bc17-169">變更現有服務的主控模型</span><span class="sxs-lookup"><span data-stu-id="1bc17-169">Changing hosting model of an existing service</span></span>
<span data-ttu-id="1bc17-170">變更從現有服務的裝載模型**共用程序**太**獨佔的程序**，反之亦然透過升級或更新機制 （或在預設服務應用程式中的規格目前不支援資訊清單）。</span><span class="sxs-lookup"><span data-stu-id="1bc17-170">Changing hosting model of an existing service from **Shared Process** too**Exclusive Process** and vice-versa through upgrade or update mechanism (or in default service specification in application manifest) is currently not supported.</span></span> <span data-ttu-id="1bc17-171">在未來的版本中將會新增此功能。</span><span class="sxs-lookup"><span data-stu-id="1bc17-171">Support for this feature will come in future versions.</span></span>

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a><span data-ttu-id="1bc17-172">在共用處理序與專屬處理序模型之間做選擇</span><span class="sxs-lookup"><span data-stu-id="1bc17-172">Choosing between shared process and exclusive process model</span></span>
<span data-ttu-id="1bc17-173">這些裝載模型有其優缺點和使用者需要的 tooevaluate 哪一個最符合其需求。</span><span class="sxs-lookup"><span data-stu-id="1bc17-173">Both these hosting models have its pros and cons and user needs tooevaluate which one fits their requirements best.</span></span> <span data-ttu-id="1bc17-174">**共用處理程序**模型可讓較佳的 OS 資源使用率，因為會產生較少的處理程序，在多個複本 hello 相同處理程序可以共用連接埠等。不過，如果其中一個 hello 複本叫用它需要 toobring hello 服務主機關閉的其中一個錯誤時，它會影響相同的程序中的所有其他複本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-174">**Shared Process** model enables better utilization of OS resources because fewer processes are spawned, multiple replicas in hello same process can share ports, etc. However, if one of hello replicas hits an error where it needs toobring down hello service host, it will impact all other replicas in same process.</span></span>

 <span data-ttu-id="1bc17-175">「專屬處理序」模型會讓每個複本處於自己的處理序中，而可提供較佳的隔離，發生問題的複本將不會影響到其他複本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-175">**Exclusive Process** model provides better isolation with every replica in its own process and a misbehaving replica will not impact other replicas.</span></span> <span data-ttu-id="1bc17-176">它派上用場的情況下，連接埠共用不支援 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="1bc17-176">It comes in handy for cases where port sharing is not supported by hello communication protocol.</span></span> <span data-ttu-id="1bc17-177">它能 hello 能力 tooapply 資源控管在複本層級。</span><span class="sxs-lookup"><span data-stu-id="1bc17-177">It facilitates hello ability tooapply resource governance at replica level.</span></span> <span data-ttu-id="1bc17-178">在 hello 相反地，**獨佔的程序**會耗用更多 OS 資源，因為它會繁衍 hello 節點上每個複本的其中一個處理序。</span><span class="sxs-lookup"><span data-stu-id="1bc17-178">On hello other hand, **Exclusive Process** will consume more OS resources as it spawns one process for each replica on hello node.</span></span>

## <a name="exclusive-process-model-and-application-model-considerations"></a><span data-ttu-id="1bc17-179">專屬處理序眉型和應用程式模型考量</span><span class="sxs-lookup"><span data-stu-id="1bc17-179">Exclusive process model and application model considerations</span></span>
<span data-ttu-id="1bc17-180">hello 建議的方式 toomodel Service Fabric 應用程式是一個 tookeep *ServiceType*每*ServicePackage*及此模型適用於大部分的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bc17-180">hello recommended way toomodel your application in Service Fabric is tookeep one *ServiceType* per *ServicePackage* and this model works well for most of hello applications.</span></span> 

<span data-ttu-id="1bc17-181">不過，tooenable 特殊案例一*ServiceType*每*ServicePackage*可能不需要這樣做，在功能上，Service Fabric 允許 toohave 一個以上*ServiceType*每*ServicePackage* (一個*CodePackage*可以註冊多個*ServiceType*)。</span><span class="sxs-lookup"><span data-stu-id="1bc17-181">However, tooenable special scenarios where one *ServiceType* per *ServicePackage* may not be desirable, functionally, Service Fabric allows toohave more than one *ServiceType* per *ServicePackage* (and one *CodePackage* can register more than one *ServiceType*).</span></span> <span data-ttu-id="1bc17-182">以下是一些 hello 案例，這些設定可以是很有用：</span><span class="sxs-lookup"><span data-stu-id="1bc17-182">Following are some of hello scenarios where these configurations can be useful:</span></span>

- <span data-ttu-id="1bc17-183">您想要 toooptimize OS 資源使用率繁衍 （spawn） 較少的處理程序，以及取得每個處理序更高的複本密度。</span><span class="sxs-lookup"><span data-stu-id="1bc17-183">You want toooptimize OS resource utilization by spawning fewer processes and having higher replica density per process.</span></span>
- <span data-ttu-id="1bc17-184">從不同的 ServiceTypes 複本都必須 tooshare 一些常見的資料具有較高的初始化或成本的記憶體。</span><span class="sxs-lookup"><span data-stu-id="1bc17-184">Replicas from different ServiceTypes need tooshare some common data that has a high initialization or memory cost.</span></span>
- <span data-ttu-id="1bc17-185">您有可用的服務供應項目，而且您想 tooput 資源使用量的限制將 hello 服務的所有複本放在相同的程序中。</span><span class="sxs-lookup"><span data-stu-id="1bc17-185">You have a free service offering and you want tooput a limit on resource utilization by putting all replicas of hello service in same process.</span></span>

<span data-ttu-id="1bc17-186">「專屬處理序」主控模型與每一 *ServicePackage* 有多個 *ServiceType* 的應用程式模型並不相同。</span><span class="sxs-lookup"><span data-stu-id="1bc17-186">**Exclusive Process** hosting model is not coherent with application model having multiple *ServiceTypes* per *ServicePackage*.</span></span> <span data-ttu-id="1bc17-187">這是因為多個*ServiceTypes*每*ServicePackage*是設計的 tooachieve 較高的資源，在複本之間共用，可讓每個處理序更高的複本密度。</span><span class="sxs-lookup"><span data-stu-id="1bc17-187">This is because multiple *ServiceTypes* per *ServicePackage* is designed tooachieve higher resource sharing among replicas and enables higher replica density per process.</span></span> <span data-ttu-id="1bc17-188">這是反對 toowhat**獨佔的程序**模型是設計的 tooachieve。</span><span class="sxs-lookup"><span data-stu-id="1bc17-188">This is contrary toowhat **Exclusive Process** model is designed tooachieve.</span></span>

<span data-ttu-id="1bc17-189">請考慮多個 hello 情況*ServiceTypes*每*ServicePackage*不同*CodePackage*註冊每個*ServiceType*.</span><span class="sxs-lookup"><span data-stu-id="1bc17-189">Consider hello case of multiple *ServiceTypes* per *ServicePackage* with different *CodePackage* registering each *ServiceType*.</span></span> <span data-ttu-id="1bc17-190">假設我們有一個 *ServicePackage* 'MultiTypeServicePackge'，其中包含兩個 *CodePackage*：</span><span class="sxs-lookup"><span data-stu-id="1bc17-190">Let's say we have a *ServicePackage* 'MultiTypeServicePackge' which has two *CodePackages*:</span></span>

- <span data-ttu-id="1bc17-191">註冊 *ServiceType* 'MyServiceTypeA' 的 'MyCodePackageA'。</span><span class="sxs-lookup"><span data-stu-id="1bc17-191">'MyCodePackageA' which registers *ServiceType* 'MyServiceTypeA'.</span></span>
- <span data-ttu-id="1bc17-192">註冊 *ServiceType* 'MyServiceTypeB' 的 'MyCodePackageB'。</span><span class="sxs-lookup"><span data-stu-id="1bc17-192">'MyCodePackageB' which registers *ServiceType* 'MyServiceTypeB'.</span></span>

<span data-ttu-id="1bc17-193">現在，假設我們建立一個「應用程式」**fabric:/SpecialApp**，並使用「專屬處理序」模型在 **fabric:/SpecialApp** 中建立下列兩個服務：</span><span class="sxs-lookup"><span data-stu-id="1bc17-193">Now, lets say, we create an *application* **fabric:/SpecialApp** and inside **fabric:/SpecialApp** we create following two services with **Exclusive Process** model:</span></span>

- <span data-ttu-id="1bc17-194">'MyServiceTypeA' 類型的服務 **fabric:/SpecialApp/ServiceA**，此服務有兩個分割區 (即 **P1** 和 **P2**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-194">Service **fabric:/SpecialApp/ServiceA** of type 'MyServiceTypeA' with two partitions (say **P1** and **P2**) and 3 replicas per partition.</span></span>
- <span data-ttu-id="1bc17-195">'MyServiceTypeB' 類型的服務 **fabric:/SpecialApp/ServiceB**，此服務有兩個分割區 (即 **P3** 和 **P4**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-195">Service **fabric:/SpecialApp/ServiceB** of type 'MyServiceTypeB' with two partitions (say **P3** and **P4**) and 3 replicas per partition.</span></span>

<span data-ttu-id="1bc17-196">指定節點上，這兩個 hello 服務會有兩個複本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-196">On a given node, both hello services will have two replicas each.</span></span> <span data-ttu-id="1bc17-197">因為我們使用**獨佔的程序**模型 toocreate hello 服務，Service Fabric 會啟用 'MyServicePackge' 每個複本的新副本。</span><span class="sxs-lookup"><span data-stu-id="1bc17-197">Since we used **Exclusive Process** model toocreate hello services, Service Fabric will activate a new copy of 'MyServicePackge' for each replica.</span></span> <span data-ttu-id="1bc17-198">每個 'MultiTypeServicePackge' 啟用項都會啟動一份 'MyCodePackageA' 和 'MyCodePackageB'。</span><span class="sxs-lookup"><span data-stu-id="1bc17-198">Each activation of 'MultiTypeServicePackge' will start a copy of 'MyCodePackageA' and 'MyCodePackageB'.</span></span> <span data-ttu-id="1bc17-199">不過，'MyCodePackageA' 或 'MyCodePackageB' 其中之一將裝載 hello 複本啟動 'MultiTypeServicePackge' 時。</span><span class="sxs-lookup"><span data-stu-id="1bc17-199">However, only one of 'MyCodePackageA' or 'MyCodePackageB' will host hello replica for which 'MultiTypeServicePackge' was activated.</span></span> <span data-ttu-id="1bc17-200">下圖顯示 hello 節點檢視：</span><span class="sxs-lookup"><span data-stu-id="1bc17-200">Following diagram shows hello node view:</span></span>

<span data-ttu-id="1bc17-201"><center>
![已部署之應用程式的節點檢視][node-view-five]
</center></span><span class="sxs-lookup"><span data-stu-id="1bc17-201"><center>
![Node view of deployed application][node-view-five]
</center></span></span>

 <span data-ttu-id="1bc17-202">我們可以看到中的 'MultiTypeServicePackge' hello 啟用分割區的複本**P1**服務的**fabric: / SpecialApp/Services**，'MyCodePackageA' 裝載 hello 複本和 'MyCodePackageB' 只要啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="1bc17-202">As we can see, in hello activation of 'MultiTypeServicePackge' for replica of partition **P1** of service **fabric:/SpecialApp/ServiceA**, 'MyCodePackageA' is hosting hello replica and 'MyCodePackageB' is just up and running.</span></span> <span data-ttu-id="1bc17-203">同樣地，在啟用 'MultiTypeServicePackge' 的分割區的複本**P3**服務的**fabric: / SpecialApp/ServiceB**裝載 hello 複本 'MyCodePackageB'，'MyCodePackageA'只要啟動且正在執行等等。</span><span class="sxs-lookup"><span data-stu-id="1bc17-203">Similarly, in activation of 'MultiTypeServicePackge' for replica of partition **P3** of service **fabric:/SpecialApp/ServiceB**, 'MyCodePackageB' is hosting hello replica and 'MyCodePackageA' is just up and running and so on.</span></span> <span data-ttu-id="1bc17-204">因此，多 hello 數目*CodePackages* (註冊不同*ServiceTypes*) 每秒*ServicePackage*，更高版本將會是多餘的資源使用狀況。</span><span class="sxs-lookup"><span data-stu-id="1bc17-204">Hence, more hello number of *CodePackages* (registering different *ServiceTypes*) per *ServicePackage*, higher will be redundant resource usage.</span></span> 
 
 <span data-ttu-id="1bc17-205">在 hello 另一方面，如果我們建立服務**fabric: / SpecialApp/Services**和**網狀架構: / SpecialApp/ServiceB**與**共用程序**模型，Service Fabric 會為啟用 'MultiTypeServicePackge' 只能有一個複本*應用程式* **fabric: / SpecialApp** （如先前所見）。</span><span class="sxs-lookup"><span data-stu-id="1bc17-205">On hello other hand if we create services **fabric:/SpecialApp/ServiceA** and **fabric:/SpecialApp/ServiceB** with **Shared Process** model, Service Fabric will activate only one copy of 'MultiTypeServicePackge' for *application* **fabric:/SpecialApp** (as we saw previously).</span></span> <span data-ttu-id="1bc17-206">'MyCodePackageA' 將裝載服務的所有複本**fabric: / SpecialApp/Services** （或任何類型 'MyServiceTypeA' toobe 更精確的服務） 而且 'MyCodePackageB' 會都裝載服務的所有複本**fabric: /SpecialApp/ServiceB** （或任何類型 'MyServiceTypeB' toobe 更精確的服務）。</span><span class="sxs-lookup"><span data-stu-id="1bc17-206">'MyCodePackageA' will host all replicas for service **fabric:/SpecialApp/ServiceA** (or of any service of type 'MyServiceTypeA' toobe more precise) and 'MyCodePackageB' will host all replicas for service **fabric:/SpecialApp/ServiceB** (or of any service of type 'MyServiceTypeB' toobe more precise).</span></span> <span data-ttu-id="1bc17-207">下圖顯示此設定中的 hello 節點檢視：</span><span class="sxs-lookup"><span data-stu-id="1bc17-207">Following diagram shows hello node view in this setting:</span></span> 

<span data-ttu-id="1bc17-208"><center>
![已部署之應用程式的節點檢視][node-view-six]
</center></span><span class="sxs-lookup"><span data-stu-id="1bc17-208"><center>
![Node view of deployed application][node-view-six]
</center></span></span>

<span data-ttu-id="1bc17-209">在上述範例中的 hello，您可能會認為是否 'MyCodePackageA' 註冊 'MyServiceTypeA' 和 'MyServiceTypeB'，而且沒有任何 'MyCodePackageB'，則會有不重複*CodePackage*執行。</span><span class="sxs-lookup"><span data-stu-id="1bc17-209">In hello above example, you might think if 'MyCodePackageA' registers both 'MyServiceTypeA' and 'MyServiceTypeB' and there is no 'MyCodePackageB', then there will be no redundant *CodePackage* running.</span></span> <span data-ttu-id="1bc17-210">這個想法是正確的，不過，如先前所述，此應用程式模型與「專屬處理序」主控模型並不相同。</span><span class="sxs-lookup"><span data-stu-id="1bc17-210">This is correct, however, as mentioned previously, this application model does not align with **Exclusive Process** hosting model.</span></span> <span data-ttu-id="1bc17-211">如果目標是 tooput 每個複本在它自己專用然後對兩者進行註冊的程序*ServiceTypes*來自相同*CodePackage*不需要並將每個放*ServiceType*中自己*ServicePacakge*是較合理的選擇。</span><span class="sxs-lookup"><span data-stu-id="1bc17-211">If goal is tooput each replica in its own dedicated process then registering both *ServiceTypes* from same *CodePackage* is not needed and putting each *ServiceType* in its own *ServicePacakge* is a more natural choice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bc17-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1bc17-212">Next steps</span></span>
<span data-ttu-id="1bc17-213">[封裝應用程式][ a4]並取得它準備好 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="1bc17-213">[Package an application][a4] and get it ready toodeploy.</span></span>

<span data-ttu-id="1bc17-214">[部署和移除應用程式][ a5]描述如何 toouse PowerShell toomanage 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="1bc17-214">[Deploy and remove applications][a5] describes how toouse PowerShell toomanage application instances.</span></span>

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