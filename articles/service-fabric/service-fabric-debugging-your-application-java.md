---
title: "在 Eclipse 中針對 Azure Service Fabric 應用程式進行偵錯 | Microsoft Docs"
description: "透過 Eclipse 在本機開發叢集上進行服務開發和偵錯，來改善您服務的可靠性和效能。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="77b84-103">使用 Eclipse 針對 Java Service Fabric 應用程式進行偵錯</span><span class="sxs-lookup"><span data-stu-id="77b84-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77b84-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="77b84-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="77b84-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="77b84-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="77b84-106">遵循 [設定 Service Fabric 開發環境](service-fabric-get-started-linux.md)中的步驟來啟動本機開發叢集。</span><span class="sxs-lookup"><span data-stu-id="77b84-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="77b84-107">更新您想要偵錯之服務的 entryPoint.sh，使其以遠端偵錯參數開始 Java 處理程序。</span><span class="sxs-lookup"><span data-stu-id="77b84-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="77b84-108">您可以在以下位置找到此檔案：``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``。</span><span class="sxs-lookup"><span data-stu-id="77b84-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="77b84-109">此範例已設定連接埠 8001 來進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="77b84-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="77b84-110">針對所要偵錯的服務，將執行個體計數或複本計數設定為 1，來更新「應用程式資訊清單」。</span><span class="sxs-lookup"><span data-stu-id="77b84-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="77b84-111">此設定可避免用於偵錯的連接埠發生衝突。</span><span class="sxs-lookup"><span data-stu-id="77b84-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="77b84-112">例如，針對無狀態服務，請設定 ``InstanceCount="1"``，而針對具狀態服務，則請將目標和最小複本集大小設定為 1，如下所示：`` TargetReplicaSetSize="1" MinReplicaSetSize="1"``。</span><span class="sxs-lookup"><span data-stu-id="77b84-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="77b84-113">部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="77b84-113">Deploy the application.</span></span>

5. <span data-ttu-id="77b84-114">在 Eclipse IDE 中，選取 [Run] \(執行) -> [Debug Configurations] \(偵錯組態) -> [Remote Java Application and input connection properties] \(遠端 Java 應用程式和輸入連線屬性)，然後依照下列方式設定屬性：</span><span class="sxs-lookup"><span data-stu-id="77b84-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="77b84-115">在想要的點設定中斷點並對應用程式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="77b84-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="77b84-116">如果應用程式當掉，您可能也會想要啟用核心傾印。</span><span class="sxs-lookup"><span data-stu-id="77b84-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="77b84-117">請在殼層中執行 ``ulimit -c``，如果它傳回 0，則表示未啟用核心傾印。</span><span class="sxs-lookup"><span data-stu-id="77b84-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="77b84-118">若要啟用無限制的核心傾印，請執行下列命令：``ulimit -c unlimited``。</span><span class="sxs-lookup"><span data-stu-id="77b84-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="77b84-119">您也可以使用 ``ulimit -a`` 命令來確認狀態。</span><span class="sxs-lookup"><span data-stu-id="77b84-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="77b84-120">如果您想要更新核心傾印產生路徑，請執行 ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``。</span><span class="sxs-lookup"><span data-stu-id="77b84-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="77b84-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77b84-121">Next steps</span></span>

* <span data-ttu-id="77b84-122">[使用 Linux Azure 診斷來收集記錄檔](service-fabric-diagnostics-how-to-setup-lad.md)。</span><span class="sxs-lookup"><span data-stu-id="77b84-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="77b84-123">[在本機監視及診斷服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="77b84-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
