---
title: "設定獨立 Azure Service Fabric 叢集 | Microsoft Docs"
description: "建立開發獨立叢集，其中包含在同部電腦上執行的三個節點。 完成此設定之後，您就可以開始建立包含多部電腦的叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: 5c8f4c784eed7b64810a3dd1c36c043d22a66936
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="6f671-104">建立您的第一個 Service Fabric 獨立叢集</span><span class="sxs-lookup"><span data-stu-id="6f671-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="6f671-105">您可以在內部部署環境或雲端上，在執行 Windows Server 2012 R2 或 Windows Server 2016 的虛擬機器或電腦上建立 Service Fabric 獨立叢集。</span><span class="sxs-lookup"><span data-stu-id="6f671-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in the cloud.</span></span> <span data-ttu-id="6f671-106">本快速入門可協助您在短短幾分鐘內建立開發獨立叢集。</span><span class="sxs-lookup"><span data-stu-id="6f671-106">This quickstart helps you to create a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="6f671-107">當您完成時，您會具備有一個包含三個節點的叢集，其在您可部署應用程式的單一電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="6f671-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6f671-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="6f671-108">Before you begin</span></span>
<span data-ttu-id="6f671-109">Service Fabric 會提供一個安裝套件以建立 Service Fabric 獨立叢集。</span><span class="sxs-lookup"><span data-stu-id="6f671-109">Service Fabric provides a setup package to create Service Fabric standalone clusters.</span></span>  <span data-ttu-id="6f671-110">[下載安裝套件](http://go.microsoft.com/fwlink/?LinkId=730690)。</span><span class="sxs-lookup"><span data-stu-id="6f671-110">[Download the setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="6f671-111">將安裝套件解壓縮至您在其中設定開發叢集之電腦或虛擬機器上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="6f671-111">Unzip the setup package to a folder on the computer or virtual machine where you are setting up the development cluster.</span></span>  <span data-ttu-id="6f671-112">[這裡](service-fabric-cluster-standalone-package-contents.md)有安裝套件內容的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="6f671-112">The contents of the setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="6f671-113">部署和設定叢集的叢集系統管理員必須具有電腦的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="6f671-113">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span></span> <span data-ttu-id="6f671-114">您無法在網域控制站上安裝 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="6f671-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-the-environment"></a><span data-ttu-id="6f671-115">驗證環境</span><span class="sxs-lookup"><span data-stu-id="6f671-115">Validate the environment</span></span>
<span data-ttu-id="6f671-116">系統會使用獨立套件中的 *TestConfiguration.ps1* 指令碼作為最佳做法分析程式，以驗證是否可以在指定的環境上部署叢集。</span><span class="sxs-lookup"><span data-stu-id="6f671-116">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="6f671-117">[部署準備](service-fabric-cluster-standalone-deployment-preparation.md)會列出必要條件和環境需求。</span><span class="sxs-lookup"><span data-stu-id="6f671-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span></span> <span data-ttu-id="6f671-118">執行指令碼來確認您是否可以建立開發叢集︰</span><span class="sxs-lookup"><span data-stu-id="6f671-118">Run the script to verify if you can create the development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-the-cluster"></a><span data-ttu-id="6f671-119">建立叢集</span><span class="sxs-lookup"><span data-stu-id="6f671-119">Create the cluster</span></span>
<span data-ttu-id="6f671-120">已使用安裝套件安裝數個範例叢集組態檔。</span><span class="sxs-lookup"><span data-stu-id="6f671-120">Several sample cluster configuration files are installed with the setup package.</span></span> <span data-ttu-id="6f671-121">*ClusterConfig.Unsecure.DevCluster.json* 是最簡單的叢集組態︰在單一電腦上執行的不安全叢集 (包含三個節點)。</span><span class="sxs-lookup"><span data-stu-id="6f671-121">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="6f671-122">其他組態檔說明使用 X.509 憑證或 Windows 安全性保護之單一或多重電腦的叢集。</span><span class="sxs-lookup"><span data-stu-id="6f671-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="6f671-123">您不需要修改本教學課程的任何預設組態設定，但請瀏覽組態檔並熟悉設定。</span><span class="sxs-lookup"><span data-stu-id="6f671-123">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span></span>  <span data-ttu-id="6f671-124">**nodes** 區段描述叢集中的三個節點︰名稱、IP 位址、[節點類型、容錯網域和升級網域](service-fabric-cluster-manifest.md#nodes-on-the-cluster)。</span><span class="sxs-lookup"><span data-stu-id="6f671-124">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="6f671-125">**properties** 區段定義叢集的[安全性、可靠性層級、診斷集合和節點類型](service-fabric-cluster-manifest.md#cluster-properties)。</span><span class="sxs-lookup"><span data-stu-id="6f671-125">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span></span>

<span data-ttu-id="6f671-126">此叢集並不安全。</span><span class="sxs-lookup"><span data-stu-id="6f671-126">This cluster is unsecure.</span></span>  <span data-ttu-id="6f671-127">任何人都可以匿名方式連線並執行管理作業，所以一律要使用 X.509 憑證或 Windows 安全性來保護生產叢集。</span><span class="sxs-lookup"><span data-stu-id="6f671-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="6f671-128">只有在建立叢集時才會設定安全性，而且不可能在叢集建立之後啟用安全性。</span><span class="sxs-lookup"><span data-stu-id="6f671-128">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span></span>  <span data-ttu-id="6f671-129">若要深入了解 Service Fabric 叢集安全性，請閱讀[保護叢集](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="6f671-129">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="6f671-130">若要建立包含三個節點的開發叢集，請從系統管理員 PowerShell 工作階段執行 *CreateServiceFabricCluster.ps1* 指令碼：</span><span class="sxs-lookup"><span data-stu-id="6f671-130">To create the three-node development cluster, run the *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="6f671-131">建立叢集時，會自動下載並安裝 Service Fabric 執行階段套件。</span><span class="sxs-lookup"><span data-stu-id="6f671-131">The Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="6f671-132">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="6f671-132">Connect to the cluster</span></span>
<span data-ttu-id="6f671-133">包含三個節點的開發叢集現在正在執行中。</span><span class="sxs-lookup"><span data-stu-id="6f671-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="6f671-134">ServiceFabric PowerShell 模組會隨著執行階段套件一起安裝。</span><span class="sxs-lookup"><span data-stu-id="6f671-134">The ServiceFabric PowerShell module is installed with the runtime.</span></span>  <span data-ttu-id="6f671-135">您可以使用 Service Fabric 執行階段套件，確認叢集是從同部電腦或從遠端電腦執行。</span><span class="sxs-lookup"><span data-stu-id="6f671-135">You can verify that the cluster is running from the same computer or from a remote computer with the Service Fabric runtime.</span></span>  <span data-ttu-id="6f671-136">[Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 會建立叢集連線。</span><span class="sxs-lookup"><span data-stu-id="6f671-136">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="6f671-137">如需連線到叢集的其他範例，請參閱[連線到安全的叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="6f671-137">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="6f671-138">連線到叢集之後，使用 [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) Cmdlet 來顯示叢集中的節點清單以及每個節點的狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="6f671-138">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="6f671-139">每個節點的 **HealthState** 應該為「正常」。</span><span class="sxs-lookup"><span data-stu-id="6f671-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="6f671-140">使用 Service Fabric Explorer 將叢集視覺化</span><span class="sxs-lookup"><span data-stu-id="6f671-140">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="6f671-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 是一個理想的工具，可將叢集視覺化及管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f671-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="6f671-142">Service Fabric Explorer 是在叢集中執行的一項服務，您可以使用瀏覽器瀏覽至 [http://localhost:19080/Explorer](http://localhost:19080/Explorer) 來存取該服務。</span><span class="sxs-lookup"><span data-stu-id="6f671-142">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="6f671-143">叢集儀表板會提供您叢集的概觀，包括應用程式和節點健康情況的摘要。</span><span class="sxs-lookup"><span data-stu-id="6f671-143">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="6f671-144">節點檢視會顯示叢集的實體配置。</span><span class="sxs-lookup"><span data-stu-id="6f671-144">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="6f671-145">對於指定的節點，您可以檢查已經在該節點上部署程式碼的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f671-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-the-cluster"></a><span data-ttu-id="6f671-147">移除叢集</span><span class="sxs-lookup"><span data-stu-id="6f671-147">Remove the cluster</span></span>
<span data-ttu-id="6f671-148">若要移除叢集，請從套件資料夾執行 *RemoveServiceFabricCluster.ps1* PowerShell 指令碼，然後傳入 JSON 組態檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="6f671-148">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="6f671-149">您可以選擇指定刪除作業的記錄檔位置。</span><span class="sxs-lookup"><span data-stu-id="6f671-149">You can optionally specify a location for the log of the deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in the configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="6f671-150">若要從電腦中移除 Service Fabric 執行階段，請從套件資料夾執行下列 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="6f671-150">To remove the Service Fabric runtime from the computer, run the following PowerShell script from the package folder.</span></span>

```powershell
# Removes Service Fabric from the current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="6f671-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f671-151">Next steps</span></span>
<span data-ttu-id="6f671-152">您已設定好開發獨立叢集，請嘗試下列文章︰</span><span class="sxs-lookup"><span data-stu-id="6f671-152">Now that you have set up a development standalone cluster, try the following articles:</span></span>
* <span data-ttu-id="6f671-153">[設定包含多部電腦的獨立叢集](service-fabric-cluster-creation-for-windows-server.md)並啟用安全性。</span><span class="sxs-lookup"><span data-stu-id="6f671-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="6f671-154">使用 PowerShell 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="6f671-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
