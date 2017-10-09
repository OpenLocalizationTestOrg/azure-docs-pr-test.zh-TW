---
title: "aaaDebug 在 Eclipse 中您 Azure Service Fabric 應用程式 |Microsoft 文件"
description: "開發和偵錯在 Eclipse 中的本機開發叢集上以改進 hello 可靠性和效能，您的服務。"
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
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="9bd4b-103">使用 Eclipse 針對 Java Service Fabric 應用程式進行偵錯</span><span class="sxs-lookup"><span data-stu-id="9bd4b-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9bd4b-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="9bd4b-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="9bd4b-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="9bd4b-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="9bd4b-106">中的 hello 步驟來啟動本機開發叢集[設定 Service Fabric 開發環境](service-fabric-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="9bd4b-107">更新 entryPoint.sh 的 hello 服務想 toodebug，使其具有遠端偵錯參數開始 hello java 處理序。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="9bd4b-108">這個檔案位於下列位置的 hello: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="9bd4b-109">此範例已設定連接埠 8001 來進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="9bd4b-110">更新應用程式資訊清單的 hello 藉由設定 hello 執行個體計數或 hello 複本計數 hello 服務正在偵錯 too1。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="9bd4b-111">此設定可避免用來偵錯的 hello 連接埠衝突。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="9bd4b-112">例如，對於無狀態服務，設定``InstanceCount="1"``和可設定狀態的服務組 hello 目標和最小複本集大小 too1，如下所示： `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="9bd4b-113">部署 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-113">Deploy hello application.</span></span>

5. <span data-ttu-id="9bd4b-114">在 hello Eclipse IDE 中，選取**執行偵錯組態]-> [遠端 Java 應用程式]-> [輸入連接屬性和**並設定 hello 屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bd4b-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="9bd4b-115">設定所需的時間點的中斷點，偵錯 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="9bd4b-116">如果 hello 應用程式損毀，您可能也想 tooenable coredumps。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="9bd4b-117">請在殼層中執行 ``ulimit -c``，如果它傳回 0，則表示未啟用核心傾印。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="9bd4b-118">tooenable 無限制的 coredumps，執行下列命令的 hello: ``ulimit -c unlimited``。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="9bd4b-119">您也可以確認 hello 狀態使用 hello 命令``ulimit -a``。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="9bd4b-120">如果您想 tooupdate hello coredump 產生路徑時，執行``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="9bd4b-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9bd4b-121">Next steps</span></span>

* <span data-ttu-id="9bd4b-122">[使用 Linux Azure 診斷來收集記錄檔](service-fabric-diagnostics-how-to-setup-lad.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="9bd4b-123">[在本機監視及診斷服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd4b-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
