---
title: "Azure Service Fabric 主控模型 | Microsoft Docs"
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
ms.openlocfilehash: ca7092a06a9ffce8383ca8bc9f70ce312cdf9de4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-hosting-model"></a><span data-ttu-id="1abc6-103">Service Fabric 主控模型</span><span class="sxs-lookup"><span data-stu-id="1abc6-103">Service Fabric hosting model</span></span>
<span data-ttu-id="1abc6-104">本文提供 Service Fabric 所提供之應用程式主控模型的概觀，並說明「共用處理程序」與「專屬處理序」模型之間的差異。</span><span class="sxs-lookup"><span data-stu-id="1abc6-104">This article provides an overview of application hosting models provided by Service Fabric, and describes the differences between the **Shared Process** and **Exclusive Process** models.</span></span> <span data-ttu-id="1abc6-105">本文說明已部署之應用程式在 Service Fabric 節點上看起來的樣子，以及服務的複本 (或執行個體) 與服務主機處理序之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="1abc6-105">It describes how a deployed application looks on a Service Fabric node and relationship between replicas (or instances) of the service and the service-host process.</span></span>

<span data-ttu-id="1abc6-106">在進一步進行之前，請確定您熟悉 [Service Fabric 應用程式模型][a1]，並了解它們之間的各種概念與關聯性。</span><span class="sxs-lookup"><span data-stu-id="1abc6-106">Before proceeding further, make sure that you are familiar with [Service Fabric Application Model][a1] and understand various concepts and relation among them.</span></span> 

> [!NOTE]
> <span data-ttu-id="1abc6-107">在本文中，為了簡單起見，除非明確指出，否則：</span><span class="sxs-lookup"><span data-stu-id="1abc6-107">In this article, for simplicity, unless explicitly mentioned:</span></span>
>
> - <span data-ttu-id="1abc6-108">所有用到「複本」一字的地方都是指具狀態服務的複本或靜態服務執行個體的複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-108">All uses of word *replica* refers to both a replica of a stateful service or an instance of a statless service.</span></span>
> - <span data-ttu-id="1abc6-109">*CodePackage* 會被視為等同於註冊 *ServiceType* 並裝載該 *ServiceType* 之服務複本的 *ServiceHost* 處理序。</span><span class="sxs-lookup"><span data-stu-id="1abc6-109">*CodePackage* is treated equivalent to *ServiceHost* process that registers a *ServiceType* and hosts replicas of services of that *ServiceType*.</span></span>
>

<span data-ttu-id="1abc6-110">為了了解主控模型，我們將逐步解說範例。</span><span class="sxs-lookup"><span data-stu-id="1abc6-110">To understand the hosting model, let us walk through an example.</span></span> <span data-ttu-id="1abc6-111">假設我們有一個 *ApplicationType* 'MyAppType'，其 *ServiceType* 為 'MyServiceType' 並且是由 *ServicePackage* 'MyServicePackage' 所提供，而此 ServicePackage 具有一個會在執行時註冊 *ServiceType* 'MyServiceType' 的 *CodePackage* 'MyCodePackage'。</span><span class="sxs-lookup"><span data-stu-id="1abc6-111">Let us say, we have an *ApplicationType* 'MyAppType' which has a *ServiceType* 'MyServiceType' which is provided by *ServicePackage* 'MyServicePackage' which has a *CodePackage* 'MyCodePackage' which registers *ServiceType* 'MyServiceType' when it runs.</span></span>

<span data-ttu-id="1abc6-112">假設我們有一個含有 3 個節點的叢集，並且建立一個類型為 'MyAppType' 的「應用程式」**fabric:/App1**。</span><span class="sxs-lookup"><span data-stu-id="1abc6-112">Let's say we have a 3 node cluster and we create an *application* **fabric:/App1** of type 'MyAppType'.</span></span> <span data-ttu-id="1abc6-113">在這個「應用程式」**fabric:/App1** 中，我們會建立一個類型為 'MyServiceType' 的服務 **fabric:/App1/ServiceA**，此服務具有 2 個分割區 (即 **P1** & **P2**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-113">Inside this *application* **fabric:/App1** we create a service **fabric:/App1/ServiceA** of type 'MyServiceType' which has 2 partitions (say **P1** & **P2**) and 3 replicas per partition.</span></span> <span data-ttu-id="1abc6-114">下圖顯示此應用程式最後部署在節點上時的檢視。</span><span class="sxs-lookup"><span data-stu-id="1abc6-114">The following diagram shows the view of this application as it ends up deployed on a node.</span></span>

<span data-ttu-id="1abc6-115"><center>
![已部署之應用程式的節點檢視][node-view-one]
</center></span><span class="sxs-lookup"><span data-stu-id="1abc6-115"><center>
![Node view of deployed application][node-view-one]
</center></span></span>

<span data-ttu-id="1abc6-116">Service Fabric 啟用了 'MyServicePackage'，而 'MyServicePackage' 則啟動了裝載來自兩個分割區 (即 **P1** & **P2**) 之複本的 'MyCodePackage'。</span><span class="sxs-lookup"><span data-stu-id="1abc6-116">Service Fabric activated 'MyServicePackage' which started 'MyCodePackage' which is hosting replicas from both the partitions i.e. **P1** & **P2**.</span></span> <span data-ttu-id="1abc6-117">請注意，此叢集內的所有節點都具有相同檢視，因為我們所選擇的每一分割區複本數目等於此叢集內的節點數目。</span><span class="sxs-lookup"><span data-stu-id="1abc6-117">Note that all the nodes in the cluster will have same view since we chose number of replicas per partition equal to number of nodes in the cluster.</span></span> <span data-ttu-id="1abc6-118">讓我們在應用程式 **fabric:/App1** 中建立另一個服務 **fabric:/App1/ServiceB**，此服務具有 1 個分割區 (即 **P3**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-118">Let's create another service **fabric:/App1/ServiceB** in application **fabric:/App1** which has 1 partition (say **P3**) and 3 replicas per partition.</span></span> <span data-ttu-id="1abc6-119">下圖顯示節點上的新檢視：</span><span class="sxs-lookup"><span data-stu-id="1abc6-119">Following diagram shows the new view on the node:</span></span>

<span data-ttu-id="1abc6-120"><center>
![已部署之應用程式的節點檢視][node-view-two]
</center></span><span class="sxs-lookup"><span data-stu-id="1abc6-120"><center>
![Node view of deployed application][node-view-two]
</center></span></span>

<span data-ttu-id="1abc6-121">如我們所見，Service Fabric 在現有的 'MyServicePackage' 啟用項中，放置了服務 **fabric:/App1/ServiceB** 之分割區 **P3** 的新複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-121">As we can see Service Fabric placed the new replica for partition **P3** of service **fabric:/App1/ServiceB** in the existing activation of 'MyServicePackage'.</span></span> <span data-ttu-id="1abc6-122">現在，讓我們建立另一個 'MyAppType' 類型的「應用程式」**fabric:/App2**，並在 **fabric:/App2** 中建立服務 **fabric:/App2/ServiceA**，此服務具有 2 個分割區 (即 **P4** & **P5**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-122">Now lets create another *application* **fabric:/App2** of type 'MyAppType' and inside **fabric:/App2** create service **fabric:/App2/ServiceA** which has 2 partitions (say **P4** & **P5**) and 3 replicas per partition.</span></span> <span data-ttu-id="1abc6-123">下圖顯示新的節點檢視：</span><span class="sxs-lookup"><span data-stu-id="1abc6-123">Following diagrams shows the new node view:</span></span>

<span data-ttu-id="1abc6-124"><center>
![已部署之應用程式的節點檢視][node-view-three]
</center></span><span class="sxs-lookup"><span data-stu-id="1abc6-124"><center>
![Node view of deployed application][node-view-three]
</center></span></span>

<span data-ttu-id="1abc6-125">這次 Service Fabric 啟用了一份新的 'MyServicePackage'，這個 'MyServicePackage' 會啟動一份新的 'MyCodePackage'，而來自服務 **fabric:/App2/ServiceA** 之兩個分割區 (即 **P4** & **P5**) 的複本則會放在這份新的 'MyCodePackage' 中。</span><span class="sxs-lookup"><span data-stu-id="1abc6-125">This time Service Fabric has activated a new copy of 'MyServicePackage' which starts a new copy of 'MyCodePackage' and replicas from both partitions of service **fabric:/App2/ServiceA** (i.e. **P4** & **P5**) are placed in this new copy 'MyCodePackage'.</span></span>

## <a name="shared-process-model"></a><span data-ttu-id="1abc6-126">共用處理序模型</span><span class="sxs-lookup"><span data-stu-id="1abc6-126">Shared process model</span></span>
<span data-ttu-id="1abc6-127">上面所見即為 Service Fabric 提供的預設主控模型，並且稱為「共用處理序」模型。</span><span class="sxs-lookup"><span data-stu-id="1abc6-127">What we saw above is the default hosting model provided by Service Fabric and is referred to as **Shared Process** model.</span></span> <span data-ttu-id="1abc6-128">在此模型中，針對指定的「應用程式」，在一個「節點」上只會啟用一份指定的 *ServicePackage* (這會啟動其包含的所有 *CodePackage*)，而指定的 *ServiceType* 之所有服務的所有複本則會放在註冊該 *ServiceType* 的 *CodePackage* 中。</span><span class="sxs-lookup"><span data-stu-id="1abc6-128">In this model, for a given *application*, only one copy of a given *ServicePackage* is activated on a *Node* (which starts all the *CodePackages* contained in it) and all the replicas of all services of a given  *ServiceType* are placed in the *CodePackage* that registers that *ServiceType*.</span></span> <span data-ttu-id="1abc6-129">換句話說，指定的 *ServiceType* 之所有服務的所有複本會共用相同的處理序。</span><span class="sxs-lookup"><span data-stu-id="1abc6-129">In other words, all the replicas of all services of a given *ServiceType* share the same process.</span></span>

## <a name="exclusive-process-model"></a><span data-ttu-id="1abc6-130">專屬處理序模型</span><span class="sxs-lookup"><span data-stu-id="1abc6-130">Exclusive process model</span></span>
<span data-ttu-id="1abc6-131">Service Fabric 所提供的另一個主控模型是「專屬處理序」模型。</span><span class="sxs-lookup"><span data-stu-id="1abc6-131">The other hosting model provided by Service Fabric is **Exclusive Process** model.</span></span> <span data-ttu-id="1abc6-132">在此模型中，在指定的「節點」上，為了放置每個複本，Service Fabric 會啟用一份新的 *ServicePackage* (這會啟動其包含的所有 *CodePackage*)，而複本則會放在註冊複本所屬服務之 *ServiceType* 的 *CodePackage* 中。</span><span class="sxs-lookup"><span data-stu-id="1abc6-132">In this model, on a given *Node*, for placing each replica, Service Fabric activates a new copy of *ServicePackage* (which starts all the *CodePackages* contained in it) and replica is placed in the *CodePackage* that registered the *ServiceType* of the service to which replica belongs.</span></span> <span data-ttu-id="1abc6-133">換句話說，每個複本都存在於自己的專屬處理序中。</span><span class="sxs-lookup"><span data-stu-id="1abc6-133">In other words, each replica lives in its own dedicated process.</span></span> 

<span data-ttu-id="1abc6-134">從 Service Fabric 5.6 版開始即支援此模型。</span><span class="sxs-lookup"><span data-stu-id="1abc6-134">This model is supported starting version 5.6 of Service Fabric.</span></span> <span data-ttu-id="1abc6-135">您可以在建立服務時 (使用 [PowerShell][p1]、[REST][r1] 或 [FabricClient][c1]) 將 **ServicePackageActivationMode** 指定為 'ExclusiveProcess' 來選擇「專屬處理序」模型。</span><span class="sxs-lookup"><span data-stu-id="1abc6-135">**Exclusive Process** model can be chosen at the time of creating the service (using [PowerShell][p1], [REST][r1] or [FabricClient][c1]) by specifying **ServicePackageActivationMode** as 'ExclusiveProcess'.</span></span>

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

<span data-ttu-id="1abc6-136">如果您的應用程式資訊清單中有預設的服務，您可以依以下所示的方式指定 **ServicePackageActivationMode** 屬性，來選擇「專屬處理序」模型：</span><span class="sxs-lookup"><span data-stu-id="1abc6-136">If you have a default service in your application manifest, you can choose **Exclusive Process** model by specifying **ServicePackageActivationMode** attribute as shown below:</span></span>

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
<span data-ttu-id="1abc6-137">繼續進行上述範例，讓我們在應用程式 **fabric:/App1** 中建立另一個服務 **fabric:/App1/ServiceC**，此服務有 2 個分割區 (即 **P6** & **P7**) 且每一分割區有 3 個複本，並且 **ServicePackageActivationMode** 已設定為 'ExclusiveProcess'。</span><span class="sxs-lookup"><span data-stu-id="1abc6-137">Continuing with our example above, lets create another service **fabric:/App1/ServiceC** in application **fabric:/App1** which has 2 partitions (say **P6** & **P7**) and 3 replicas per partition with **ServicePackageActivationMode** set to 'ExclusiveProcess'.</span></span> <span data-ttu-id="1abc6-138">下圖顯示節點上的新檢視：</span><span class="sxs-lookup"><span data-stu-id="1abc6-138">Following diagram shows new view on the node:</span></span>

<span data-ttu-id="1abc6-139"><center>
![已部署之應用程式的節點檢視][node-view-four]
</center></span><span class="sxs-lookup"><span data-stu-id="1abc6-139"><center>
![Node view of deployed application][node-view-four]
</center></span></span>

<span data-ttu-id="1abc6-140">如您所見，Service Fabric 啟用了兩份新的 'MyServicePackage' (針對來自分割區 **P6** & **P7** 的每個複本各啟用一份)，並將每個複本放在其專用的一份 *CodePackage* 中。</span><span class="sxs-lookup"><span data-stu-id="1abc6-140">As you can see, Service Fabric activated two new copies of 'MyServicePackage' (one for each replica from partition **P6** & **P7**) and placed each replica in its dedicated copy of *CodePackage*.</span></span> <span data-ttu-id="1abc6-141">這裡有另一個需要注意的事項，就是使用「專屬處理序」模型時，就指定的「應用程式」而言，一個「節點」 上可以有多份作用中的指定 *ServicePackage*。</span><span class="sxs-lookup"><span data-stu-id="1abc6-141">Another thing to note here is, when **Exclusive Process** model is used, for a given *application*, multiple copies of a given *ServicePackage* can be active on a *Node*.</span></span> <span data-ttu-id="1abc6-142">在上述範例中，我們看到 **fabric:/App1** 有三份作用中的 'MyServicePackage'。</span><span class="sxs-lookup"><span data-stu-id="1abc6-142">In above example, we see that three copies of 'MyServicePackage' are active for **fabric:/App1**.</span></span> <span data-ttu-id="1abc6-143">這每一份作用中的 'MyServicePackage' 都有相關的 **ServicePackageAtivationId**，用來作為它們在「應用程式」**fabric:/App1** 中的身分識別。</span><span class="sxs-lookup"><span data-stu-id="1abc6-143">Each of these active copies of 'MyServicePackage' has a **ServicePackageAtivationId** associated with it which identifies that copy within *application* **fabric:/App1**.</span></span>

<span data-ttu-id="1abc6-144">如果針對「應用程式」(例如上述範例中的 **fabric:/App2**) 只使用「共用處理序」模型，則一個「節點」上只會有一份作用中 *ServicePackage*，而這個 *ServicePackage* 啟用項的 **ServicePackageAtivationId** 則會是「空字串」。</span><span class="sxs-lookup"><span data-stu-id="1abc6-144">When only **Shared Process** model is used for an *application*, like **fabric:/App2** in above example, there is only one active copy of *ServicePackage* on a *Node* and **ServicePackageAtivationId** for this activation of *ServicePackage* is 'empty string'.</span></span>

> [!NOTE]
>- <span data-ttu-id="1abc6-145">「共用處理序」主控模型會與等於 **SharedProcess** 的 **ServicePackageAtivationMode** 對應。</span><span class="sxs-lookup"><span data-stu-id="1abc6-145">**Shared Process** hosting model corresponds to **ServicePackageAtivationMode** equal **SharedProcess**.</span></span> <span data-ttu-id="1abc6-146">這是預設的主控模型，在建立服務時不須指定 **ServicePackageAtivationMode**。</span><span class="sxs-lookup"><span data-stu-id="1abc6-146">This is the default hosting model and **ServicePackageAtivationMode** need not be specified at the time of creating the service.</span></span>
>
>- <span data-ttu-id="1abc6-147">「專屬處理序」主控模型會與等於 **ExclusiveProcess** 的 **ServicePackageAtivationMode** 對應，在建立服務時必須明確指定。</span><span class="sxs-lookup"><span data-stu-id="1abc6-147">**Exclusive Process** hosting model corresponds to **ServicePackageAtivationMode** equal **ExclusiveProcess** and need to be explicitly specified at the time of creating the service.</span></span> 
>
>- <span data-ttu-id="1abc6-148">您可以透過查詢[服務描述][p2]並查看 **ServicePackageAtivationMode** 的值，來得知服務的主控模型。</span><span class="sxs-lookup"><span data-stu-id="1abc6-148">Hosting model of a service can be known by querying the [service description][p2] and looking at value of **ServicePackageAtivationMode**.</span></span>
>
>

## <a name="working-with-deployed-service-package"></a><span data-ttu-id="1abc6-149">使用已部署的服務套件</span><span class="sxs-lookup"><span data-stu-id="1abc6-149">Working with deployed service package</span></span>
<span data-ttu-id="1abc6-150">節點上一份作用中的 *ServicePackage* 稱為[已部署的服務套件][p3]。</span><span class="sxs-lookup"><span data-stu-id="1abc6-150">An active copy of a *ServicePackage* on a node is referred as [deployed service package][p3].</span></span> <span data-ttu-id="1abc6-151">如先前所述，使用「專屬處理序」模型來建立服務時，就指定的「應用程式」而言，同一個 *ServicePackage* 可能會有多個已部署的服務套件。</span><span class="sxs-lookup"><span data-stu-id="1abc6-151">As previously mentioned above, when **Exclusive Process** model is used for creating services, for a given *application*, there could be multiple deployed service packages for the same *ServicePackage*.</span></span> <span data-ttu-id="1abc6-152">執行已部署之服務套件的特定作業 (例如[回報已部署之服務套件的健康情況][p4]或[重新啟動已部署之服務套件的程式碼套件][p5]等) 時，必須提供 **ServicePackageActivationId** 來識別特定的已部署服務套件。</span><span class="sxs-lookup"><span data-stu-id="1abc6-152">While performing operations specific to deployed service package like [reporting health of a deployed service package][p4] or [restarting code package of a deployed service package][p5] etc., **ServicePackageActivationId** needs to be provided to identify a specific deployed service package.</span></span>

 <span data-ttu-id="1abc6-153">您可以查詢節點上[已部署的服務套件][p3]清單，來取得已部署之服務套件的 **ServicePackageActivationId**。</span><span class="sxs-lookup"><span data-stu-id="1abc6-153">**ServicePackageActivationId** of a deployed service package can be obtained by querying the list of [deployed service packages][p3] on a node.</span></span> <span data-ttu-id="1abc6-154">查詢節點上的[已部署的服務類型][p6]、[已部署的複本][p7]及[已部署的程式碼套件][p8]時，查詢結果也會包含父代已部署服務套件的 **ServicePackageActivationId**。</span><span class="sxs-lookup"><span data-stu-id="1abc6-154">When querying [deployed service types][p6], [deployed replicas][p7] and [deployed code packages][p8] on a node, the query result also contains the **ServicePackageActivationId** of parent deployed service package.</span></span>

> [!NOTE]
>- <span data-ttu-id="1abc6-155">在「共用處理序」主控模型下，於指定的「節點」上，針對指定的「應用程式」，只會啟用一份 *ServicePackage*。</span><span class="sxs-lookup"><span data-stu-id="1abc6-155">Under **Shared Process** hosting model, on a given *node*, for a given *application*, only one copy of a *ServicePackage* is activated.</span></span> <span data-ttu-id="1abc6-156">其 **ServicePackageActivationId** 會等於「空字串」，在執行已部署之服務套件的相關作業時不須指定。</span><span class="sxs-lookup"><span data-stu-id="1abc6-156">It has **ServicePackageActivationId** equal to *empty string* and need not be specified while performing deployed service package related operations.</span></span> 
>
> - <span data-ttu-id="1abc6-157">在「專屬處理序」主控模型下，於指定的「節點」上，針對指定的「應用程式」，會有一或多份作用中的 *ServicePackage*。</span><span class="sxs-lookup"><span data-stu-id="1abc6-157">Under **Exclusive Process** hosting model, on a given *node*, for a given *application*, one or more copies of a *ServicePackage* can be active.</span></span> <span data-ttu-id="1abc6-158">每個啟動項都有一個「非空白」的 **ServicePackageActivationId**，在執行已部署之服務套件的相關作業時必須加以指定。</span><span class="sxs-lookup"><span data-stu-id="1abc6-158">Each activation has a *non-empty* **ServicePackageActivationId** and needs to be specified while performing deployed service package related operations.</span></span> 
>
> - <span data-ttu-id="1abc6-159">如果省略 **ServicePackageActivationId**，它會預設為「空字串」。</span><span class="sxs-lookup"><span data-stu-id="1abc6-159">If **ServicePackageActivationId** is ommited it defaults to 'empty string'.</span></span> <span data-ttu-id="1abc6-160">如果有在「共用處理序」模型下啟用的已部署服務套件存在，系統就會在該套件上執行作業，否則作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="1abc6-160">If a deployed service package that was activated under **Shared Process** model is present, then operation will be performed on it, otherwise the operation will fail.</span></span>
>
> - <span data-ttu-id="1abc6-161">不建議執行一次查詢並快取 **ServicePackageActivationId**，因為這是動態產生的，可能因各種原因而有所變更。</span><span class="sxs-lookup"><span data-stu-id="1abc6-161">It is not recommended to query once and cache **ServicePackageActivationId** as it is dynamically generated and can change for various reasons.</span></span> <span data-ttu-id="1abc6-162">在執行需要 **ServicePackageActivationId** 的作業之前，您應該先查詢節點上[已部署的服務套件][p3]清單，然後再使用來自查詢結果的 *ServicePackageActivationId** 來執行原先的作業。</span><span class="sxs-lookup"><span data-stu-id="1abc6-162">Before performing an operation that needs **ServicePackageActivationId**, you should first query the list of [deployed service packages][p3] on a node and then use *ServicePackageActivationId** from query result to perform the original operation.</span></span>
>
>

## <a name="guest-executable-and-container-applications"></a><span data-ttu-id="1abc6-163">客體可執行檔和容器應用程式</span><span class="sxs-lookup"><span data-stu-id="1abc6-163">Guest executable and container applications</span></span>
<span data-ttu-id="1abc6-164">Service Fabric 會將[客體可執行檔][a2]和[容器][a3]應用程式視為獨立的無狀態服務，亦即 *ServiceHost* (一個處理序或容器) 中沒有任何 Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="1abc6-164">Service Fabric treats [Guest executable][a2] and [container][a3] applications as statless services which are self-contained i.e. there is no Service Fabric runtime in *ServiceHost* (a process or container).</span></span> <span data-ttu-id="1abc6-165">由於這些服務是獨立的，因此每一 *ServiceHost* 的複本數並不適用於這些服務。</span><span class="sxs-lookup"><span data-stu-id="1abc6-165">Since these services are self-contained, number of replicas per *ServiceHost* is not applicable for these services.</span></span> <span data-ttu-id="1abc6-166">與這些服務搭配使用的最常見組態是 [InstanceCount][c2] 等於 -1 的單一分割區 (亦即在叢集的每個節點上都會執行一份服務程式碼)。</span><span class="sxs-lookup"><span data-stu-id="1abc6-166">The most common configuration used with these services is single-partition with [InstanceCount][c2] equal to -1 (i.e. one copy of the service code running on each node of cluster).</span></span> 

<span data-ttu-id="1abc6-167">這些服務的預設 **ServicePackageActivationMode** 是 **SharedProcess**，在此情況下，Service Fabric 會針對指定的「應用程式」在一個「節點」上啟用一份 *ServicePackage*，這意謂著一個「節點」上只會執行一份服務程式碼。</span><span class="sxs-lookup"><span data-stu-id="1abc6-167">The default **ServicePackageActivationMode** for these services is **SharedProcess** in which case Service Fabric only activates one copy of *ServicePackage* on a *Node* for a given *application* which means only one copy of service code will run a *Node*.</span></span> <span data-ttu-id="1abc6-168">當您建立多個 *ServiceType* 類型 (在 *ServiceManifest* 中指定) 的服務 (*Service1* 到 *ServiceN*) 時，或當您的服務具有多個分割區時，如果您想要讓多份服務程式碼在「節點」上執行，您應該在建立服務時，將 **ServicePackageActivationMode** 指定為 **ExclusiveProcess**。</span><span class="sxs-lookup"><span data-stu-id="1abc6-168">If you want multiple copies of your service code to run on a *Node* when you create multiple services (*Service1* to *ServiceN*) of *ServiceType* (specified in *ServiceManifest*) or when your service is multi-partitioned, you should specify **ServicePackageActivationMode** as **ExclusiveProcess** at the time of creating the service.</span></span>

## <a name="changing-hosting-model-of-an-existing-service"></a><span data-ttu-id="1abc6-169">變更現有服務的主控模型</span><span class="sxs-lookup"><span data-stu-id="1abc6-169">Changing hosting model of an existing service</span></span>
<span data-ttu-id="1abc6-170">目前不支援透過升級或更新機制 (或在應用程式資訊清單的預設服務規格中)，將現有服務的主控模型從「共用處理序」變更為「專屬處理序」，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="1abc6-170">Changing hosting model of an existing service from **Shared Process** to **Exclusive Process** and vice-versa through upgrade or update mechanism (or in default service specification in application manifest) is currently not supported.</span></span> <span data-ttu-id="1abc6-171">在未來的版本中將會新增此功能。</span><span class="sxs-lookup"><span data-stu-id="1abc6-171">Support for this feature will come in future versions.</span></span>

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a><span data-ttu-id="1abc6-172">在共用處理序與專屬處理序模型之間做選擇</span><span class="sxs-lookup"><span data-stu-id="1abc6-172">Choosing between shared process and exclusive process model</span></span>
<span data-ttu-id="1abc6-173">這兩個主控模型各有其優缺點，使用者必須評估哪一個模型最符合其需求。</span><span class="sxs-lookup"><span data-stu-id="1abc6-173">Both these hosting models have its pros and cons and user needs to evaluate which one fits their requirements best.</span></span> <span data-ttu-id="1abc6-174">「共用處理序」模型可提升 OS 資源的使用率，因為產生的處理序較少、同一個處理序中的多個複本可以共用連接埠等。不過，如果其中一個複本發生錯誤而必須關閉服務主機，就會影響到該相同處理序中的所有其他複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-174">**Shared Process** model enables better utilization of OS resources because fewer processes are spawned, multiple replicas in the same process can share ports, etc. However, if one of the replicas hits an error where it needs to bring down the service host, it will impact all other replicas in same process.</span></span>

 <span data-ttu-id="1abc6-175">「專屬處理序」模型會讓每個複本處於自己的處理序中，而可提供較佳的隔離，發生問題的複本將不會影響到其他複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-175">**Exclusive Process** model provides better isolation with every replica in its own process and a misbehaving replica will not impact other replicas.</span></span> <span data-ttu-id="1abc6-176">這適用於通訊協定不支援連接埠共用的情況。</span><span class="sxs-lookup"><span data-stu-id="1abc6-176">It comes in handy for cases where port sharing is not supported by the communication protocol.</span></span> <span data-ttu-id="1abc6-177">它可協助在複本層級套用資源管理。</span><span class="sxs-lookup"><span data-stu-id="1abc6-177">It facilitates the ability to apply resource governance at replica level.</span></span> <span data-ttu-id="1abc6-178">另一方面，「專屬處理序」會取用較多的 OS 資源，因為它會為節點上的每個複本都產生一個處理序。</span><span class="sxs-lookup"><span data-stu-id="1abc6-178">On the other hand, **Exclusive Process** will consume more OS resources as it spawns one process for each replica on the node.</span></span>

## <a name="exclusive-process-model-and-application-model-considerations"></a><span data-ttu-id="1abc6-179">專屬處理序眉型和應用程式模型考量</span><span class="sxs-lookup"><span data-stu-id="1abc6-179">Exclusive process model and application model considerations</span></span>
<span data-ttu-id="1abc6-180">在 Service Fabric 中，建議的應用程式模型建立方式是維持每一 *ServicePackage* 一個 *ServiceType*，這個模型適用於大多數應用程式。</span><span class="sxs-lookup"><span data-stu-id="1abc6-180">The recommended way to model your application in Service Fabric is to keep one *ServiceType* per *ServicePackage* and this model works well for most of the applications.</span></span> 

<span data-ttu-id="1abc6-181">不過，若要啟用每一 *ServicePackage* 一個 *ServiceType* 可能不符合需求的特殊案例，就功能而言，Service Fabric 允許每一 *ServicePackage* 有多個 *ServiceType* (而且一個 *CodePackage* 可以註冊多個 *ServiceType*)。</span><span class="sxs-lookup"><span data-stu-id="1abc6-181">However, to enable special scenarios where one *ServiceType* per *ServicePackage* may not be desirable, functionally, Service Fabric allows to have more than one *ServiceType* per *ServicePackage* (and one *CodePackage* can register more than one *ServiceType*).</span></span> <span data-ttu-id="1abc6-182">以下是這些組態可能有用的一些案例：</span><span class="sxs-lookup"><span data-stu-id="1abc6-182">Following are some of the scenarios where these configurations can be useful:</span></span>

- <span data-ttu-id="1abc6-183">您想要藉由減少產生處理序並提高每一處理序的複本密度，將 OS 資源使用率最佳化。</span><span class="sxs-lookup"><span data-stu-id="1abc6-183">You want to optimize OS resource utilization by spawning fewer processes and having higher replica density per process.</span></span>
- <span data-ttu-id="1abc6-184">來自不同 ServiceType 的複本需要共用一些具有高初始化或記憶體成本的通用資料。</span><span class="sxs-lookup"><span data-stu-id="1abc6-184">Replicas from different ServiceTypes need to share some common data that has a high initialization or memory cost.</span></span>
- <span data-ttu-id="1abc6-185">您有免費的服務方案，而您想要透過將服務的所有複本都放在同一個處理序中，為資源使用量設定限制。</span><span class="sxs-lookup"><span data-stu-id="1abc6-185">You have a free service offering and you want to put a limit on resource utilization by putting all replicas of the service in same process.</span></span>

<span data-ttu-id="1abc6-186">「專屬處理序」主控模型與每一 *ServicePackage* 有多個 *ServiceType* 的應用程式模型並不相同。</span><span class="sxs-lookup"><span data-stu-id="1abc6-186">**Exclusive Process** hosting model is not coherent with application model having multiple *ServiceTypes* per *ServicePackage*.</span></span> <span data-ttu-id="1abc6-187">這是因為每一 *ServicePackage* 多個 *ServiceType* 的設計是用來提高複本間的資源共用，以及提高每一處理序的複本密度。</span><span class="sxs-lookup"><span data-stu-id="1abc6-187">This is because multiple *ServiceTypes* per *ServicePackage* is designed to achieve higher resource sharing among replicas and enables higher replica density per process.</span></span> <span data-ttu-id="1abc6-188">這項設計與「專屬處理序」的設計目的相反。</span><span class="sxs-lookup"><span data-stu-id="1abc6-188">This is contrary to what **Exclusive Process** model is designed to achieve.</span></span>

<span data-ttu-id="1abc6-189">思考一下每一 *ServicePackage* 有多個 *ServiceType* 的案例，其中是由不同的 *CodePackage* 註冊每個 *ServiceType*。</span><span class="sxs-lookup"><span data-stu-id="1abc6-189">Consider the case of multiple *ServiceTypes* per *ServicePackage* with different *CodePackage* registering each *ServiceType*.</span></span> <span data-ttu-id="1abc6-190">假設我們有一個 *ServicePackage* 'MultiTypeServicePackge'，其中包含兩個 *CodePackage*：</span><span class="sxs-lookup"><span data-stu-id="1abc6-190">Let's say we have a *ServicePackage* 'MultiTypeServicePackge' which has two *CodePackages*:</span></span>

- <span data-ttu-id="1abc6-191">註冊 *ServiceType* 'MyServiceTypeA' 的 'MyCodePackageA'。</span><span class="sxs-lookup"><span data-stu-id="1abc6-191">'MyCodePackageA' which registers *ServiceType* 'MyServiceTypeA'.</span></span>
- <span data-ttu-id="1abc6-192">註冊 *ServiceType* 'MyServiceTypeB' 的 'MyCodePackageB'。</span><span class="sxs-lookup"><span data-stu-id="1abc6-192">'MyCodePackageB' which registers *ServiceType* 'MyServiceTypeB'.</span></span>

<span data-ttu-id="1abc6-193">現在，假設我們建立一個「應用程式」**fabric:/SpecialApp**，並使用「專屬處理序」模型在 **fabric:/SpecialApp** 中建立下列兩個服務：</span><span class="sxs-lookup"><span data-stu-id="1abc6-193">Now, lets say, we create an *application* **fabric:/SpecialApp** and inside **fabric:/SpecialApp** we create following two services with **Exclusive Process** model:</span></span>

- <span data-ttu-id="1abc6-194">'MyServiceTypeA' 類型的服務 **fabric:/SpecialApp/ServiceA**，此服務有兩個分割區 (即 **P1** 和 **P2**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-194">Service **fabric:/SpecialApp/ServiceA** of type 'MyServiceTypeA' with two partitions (say **P1** and **P2**) and 3 replicas per partition.</span></span>
- <span data-ttu-id="1abc6-195">'MyServiceTypeB' 類型的服務 **fabric:/SpecialApp/ServiceB**，此服務有兩個分割區 (即 **P3** 和 **P4**) 且每一分割區有 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-195">Service **fabric:/SpecialApp/ServiceB** of type 'MyServiceTypeB' with two partitions (say **P3** and **P4**) and 3 replicas per partition.</span></span>

<span data-ttu-id="1abc6-196">在指定的節點上，這兩個服務將各有兩個複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-196">On a given node, both the services will have two replicas each.</span></span> <span data-ttu-id="1abc6-197">由於我們已使用「專屬處理序」模型來建立這些服務，因此 Service Fabric 會為每個複本建立一份新的 'MyServicePackge'。</span><span class="sxs-lookup"><span data-stu-id="1abc6-197">Since we used **Exclusive Process** model to create the services, Service Fabric will activate a new copy of 'MyServicePackge' for each replica.</span></span> <span data-ttu-id="1abc6-198">每個 'MultiTypeServicePackge' 啟用項都會啟動一份 'MyCodePackageA' 和 'MyCodePackageB'。</span><span class="sxs-lookup"><span data-stu-id="1abc6-198">Each activation of 'MultiTypeServicePackge' will start a copy of 'MyCodePackageA' and 'MyCodePackageB'.</span></span> <span data-ttu-id="1abc6-199">不過，'MyCodePackageA' 或 'MyCodePackageB' 只有其中之一會裝載作為 'MultiTypeServicePackge' 啟用對象的複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-199">However, only one of 'MyCodePackageA' or 'MyCodePackageB' will host the replica for which 'MultiTypeServicePackge' was activated.</span></span> <span data-ttu-id="1abc6-200">下圖顯示節點檢視：</span><span class="sxs-lookup"><span data-stu-id="1abc6-200">Following diagram shows the node view:</span></span>

<span data-ttu-id="1abc6-201"><center>
![已部署之應用程式的節點檢視][node-view-five]
</center></span><span class="sxs-lookup"><span data-stu-id="1abc6-201"><center>
![Node view of deployed application][node-view-five]
</center></span></span>

 <span data-ttu-id="1abc6-202">如我們所見，在服務 **fabric:/SpecialApp/ServiceA** 分割區 **P1** 之複本的 'MultiTypeServicePackge' 啟用項中，是由 'MyCodePackageA' 裝載複本，而 'MyCodePackageB' 則只是已啟動並在執行中。</span><span class="sxs-lookup"><span data-stu-id="1abc6-202">As we can see, in the activation of 'MultiTypeServicePackge' for replica of partition **P1** of service **fabric:/SpecialApp/ServiceA**, 'MyCodePackageA' is hosting the replica and 'MyCodePackageB' is just up and running.</span></span> <span data-ttu-id="1abc6-203">同樣地，在服務 **fabric:/SpecialApp/ServiceB** 分割區 **P3** 之複本的 'MultiTypeServicePackge' 啟用項中，是由 'MyCodePackageB' 裝載複本，而 'MyCodePackageA' 則只是已啟動並在執行中。</span><span class="sxs-lookup"><span data-stu-id="1abc6-203">Similarly, in activation of 'MultiTypeServicePackge' for replica of partition **P3** of service **fabric:/SpecialApp/ServiceB**, 'MyCodePackageB' is hosting the replica and 'MyCodePackageA' is just up and running and so on.</span></span> <span data-ttu-id="1abc6-204">因此，每一 *ServicePackage* 的 *CodePackage* (註冊不同的 *ServiceType*) 數目越多，備援資源的使用量就越高。</span><span class="sxs-lookup"><span data-stu-id="1abc6-204">Hence, more the number of *CodePackages* (registering different *ServiceTypes*) per *ServicePackage*, higher will be redundant resource usage.</span></span> 
 
 <span data-ttu-id="1abc6-205">另一方便，如果我們使用「共用處理序」來建立服務 **fabric:/SpecialApp/ServiceA** 和 **fabric:/SpecialApp/ServiceB**，則 Service Fabric 將只會為「應用程式」**fabric:/SpecialApp** 啟用一份 'MultiTypeServicePackge' (如我們先前所見)。</span><span class="sxs-lookup"><span data-stu-id="1abc6-205">On the other hand if we create services **fabric:/SpecialApp/ServiceA** and **fabric:/SpecialApp/ServiceB** with **Shared Process** model, Service Fabric will activate only one copy of 'MultiTypeServicePackge' for *application* **fabric:/SpecialApp** (as we saw previously).</span></span> <span data-ttu-id="1abc6-206">'MyCodePackageA' 將會裝載服務 **fabric:/SpecialApp/ServiceA** (或更精確地說，是 'MyServiceTypeA' 類型的任何服務) 的所有複本，而 'MyCodePackageB' 則會裝載服務 **fabric:/SpecialApp/ServiceB** (或更精確地說，是 'MyServiceTypeB' 類型的任何服務) 的所有複本。</span><span class="sxs-lookup"><span data-stu-id="1abc6-206">'MyCodePackageA' will host all replicas for service **fabric:/SpecialApp/ServiceA** (or of any service of type 'MyServiceTypeA' to be more precise) and 'MyCodePackageB' will host all replicas for service **fabric:/SpecialApp/ServiceB** (or of any service of type 'MyServiceTypeB' to be more precise).</span></span> <span data-ttu-id="1abc6-207">下圖顯示此設定中的節點檢視：</span><span class="sxs-lookup"><span data-stu-id="1abc6-207">Following diagram shows the node view in this setting:</span></span> 

<span data-ttu-id="1abc6-208"><center>
![已部署之應用程式的節點檢視][node-view-six]
</center></span><span class="sxs-lookup"><span data-stu-id="1abc6-208"><center>
![Node view of deployed application][node-view-six]
</center></span></span>

<span data-ttu-id="1abc6-209">在上述範例中，您可能會認為如果 'MyCodePackageA' 既註冊 'MyServiceTypeA' 也註冊 'MyServiceTypeB'，而沒有 'MyCodePackageB' 存在，就不會執行備援的 *CodePackage*。</span><span class="sxs-lookup"><span data-stu-id="1abc6-209">In the above example, you might think if 'MyCodePackageA' registers both 'MyServiceTypeA' and 'MyServiceTypeB' and there is no 'MyCodePackageB', then there will be no redundant *CodePackage* running.</span></span> <span data-ttu-id="1abc6-210">這個想法是正確的，不過，如先前所述，此應用程式模型與「專屬處理序」主控模型並不相同。</span><span class="sxs-lookup"><span data-stu-id="1abc6-210">This is correct, however, as mentioned previously, this application model does not align with **Exclusive Process** hosting model.</span></span> <span data-ttu-id="1abc6-211">如果目標是要將每個複本放在其自己的專用處理序中，就不需要從同一個 *CodePackage* 註冊兩個 *ServiceType*，將每個 *ServiceType* 放在其自己的 *ServicePacakge* 才是較自然的選擇。</span><span class="sxs-lookup"><span data-stu-id="1abc6-211">If goal is to put each replica in its own dedicated process then registering both *ServiceTypes* from same *CodePackage* is not needed and putting each *ServiceType* in its own *ServicePacakge* is a more natural choice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1abc6-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1abc6-212">Next steps</span></span>
<span data-ttu-id="1abc6-213">[對應用程式進行封裝][a4]並使它準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="1abc6-213">[Package an application][a4] and get it ready to deploy.</span></span>

<span data-ttu-id="1abc6-214">[部署與移除應用程式][a5]說明如何使用 PowerShell 來管理應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="1abc6-214">[Deploy and remove applications][a5] describes how to use PowerShell to manage application instances.</span></span>

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before the slash-->
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