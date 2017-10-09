---
title: "Linux 和 Windows 之間的差異 aaaAzure Service Fabric |Microsoft 文件"
description: "在 Windows Azure Service Fabric hello on Linux 的 Azure 服務網狀架構預覽之間的差異。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="e6b31-103">Linux (預覽) 和 Windows (正式推出) 上 Service Fabric 之間的差異</span><span class="sxs-lookup"><span data-stu-id="e6b31-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="e6b31-104">由於 Linux 上的 Service Fabric 是預覽，有一些 Windows 上支援的功能在 Linux 上尚未支援。</span><span class="sxs-lookup"><span data-stu-id="e6b31-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="e6b31-105">最後，hello 功能集，會在同位在 Linux 上的 Service Fabric 正式推出時。</span><span class="sxs-lookup"><span data-stu-id="e6b31-105">Eventually, hello feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="e6b31-106">在即將推出的版本中，兩者間的功能差異會減少。</span><span class="sxs-lookup"><span data-stu-id="e6b31-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="e6b31-107">hello 下列之間存在差異 hello 最新可用版本 (也就是在 Windows 和 Linux 上的 5.5 版上 5.6 版本之間):</span><span class="sxs-lookup"><span data-stu-id="e6b31-107">hello following differences exist between hello latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="e6b31-108">可靠的集合 (和可靠的具狀態服務)</span><span class="sxs-lookup"><span data-stu-id="e6b31-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="e6b31-109">ReverseProxy</span><span class="sxs-lookup"><span data-stu-id="e6b31-109">ReverseProxy</span></span> 
* <span data-ttu-id="e6b31-110">獨立安裝程式</span><span class="sxs-lookup"><span data-stu-id="e6b31-110">Standalone installer</span></span> 
* <span data-ttu-id="e6b31-111">資訊清單檔案的 XML 結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="e6b31-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="e6b31-112">主控台重新導向</span><span class="sxs-lookup"><span data-stu-id="e6b31-112">Console redirection</span></span> 
* <span data-ttu-id="e6b31-113">hello 錯誤 Analysis Service (FAS)</span><span class="sxs-lookup"><span data-stu-id="e6b31-113">hello Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="e6b31-114">容器的 Docker Compose 和磁碟區與記錄驅動程式</span><span class="sxs-lookup"><span data-stu-id="e6b31-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="e6b31-115">容器和服務的資源管理</span><span class="sxs-lookup"><span data-stu-id="e6b31-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="e6b31-116">DNS 服務</span><span class="sxs-lookup"><span data-stu-id="e6b31-116">DNS service</span></span>
* <span data-ttu-id="e6b31-117">Azure Active Directory 支援</span><span class="sxs-lookup"><span data-stu-id="e6b31-117">Azure Active Directory support</span></span>
* <span data-ttu-id="e6b31-118">某些 Powershell 命令的對等 CLI 命令</span><span class="sxs-lookup"><span data-stu-id="e6b31-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="e6b31-119">針對 Linux 叢集 （如展開 hello 下一節），可以執行 Powershell 命令的子集。</span><span class="sxs-lookup"><span data-stu-id="e6b31-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in hello next section).</span></span>

>[!NOTE]
><span data-ttu-id="e6b31-120">在生產環境叢集中不支援主控台重新導向，即使是在 Windows 上亦然。</span><span class="sxs-lookup"><span data-stu-id="e6b31-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="e6b31-121">Windows 與 Linux 上的開發工具也不同。</span><span class="sxs-lookup"><span data-stu-id="e6b31-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="e6b31-122">在 Windows 上使用 VisualStudio、Powershell、VSTS 和 ETW，而在 Linux 上使用 Yeoman、Eclipse、Jenkins 和 LTTng。</span><span class="sxs-lookup"><span data-stu-id="e6b31-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="e6b31-123">無法針對 Linux Service Fabric 叢集運作的 Powershell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e6b31-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="e6b31-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="e6b31-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="e6b31-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="e6b31-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="e6b31-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="e6b31-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="e6b31-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="e6b31-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="e6b31-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="e6b31-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="e6b31-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e6b31-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="e6b31-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e6b31-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="e6b31-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="e6b31-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="e6b31-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="e6b31-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="e6b31-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="e6b31-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="e6b31-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="e6b31-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="e6b31-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="e6b31-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="e6b31-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="e6b31-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="e6b31-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="e6b31-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="e6b31-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="e6b31-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="e6b31-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="e6b31-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="e6b31-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="e6b31-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="e6b31-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="e6b31-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="e6b31-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="e6b31-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="e6b31-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="e6b31-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="e6b31-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="e6b31-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="e6b31-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="e6b31-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="e6b31-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="e6b31-146">Cmd</span></span>
* <span data-ttu-id="e6b31-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="e6b31-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="e6b31-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="e6b31-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="e6b31-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="e6b31-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="e6b31-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="e6b31-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="e6b31-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="e6b31-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="e6b31-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="e6b31-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="e6b31-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e6b31-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="e6b31-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="e6b31-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="e6b31-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="e6b31-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="e6b31-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="e6b31-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="e6b31-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="e6b31-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="e6b31-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="e6b31-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="e6b31-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="e6b31-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="e6b31-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="e6b31-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="e6b31-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="e6b31-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="e6b31-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="e6b31-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="e6b31-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="e6b31-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="e6b31-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="e6b31-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="e6b31-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="e6b31-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="e6b31-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="e6b31-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="e6b31-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="e6b31-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="e6b31-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="e6b31-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="e6b31-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="e6b31-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="e6b31-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="e6b31-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="e6b31-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="e6b31-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="e6b31-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="e6b31-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="e6b31-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="e6b31-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="e6b31-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="e6b31-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="e6b31-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="e6b31-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="e6b31-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="e6b31-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="e6b31-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6b31-177">Next steps</span></span>
* [<span data-ttu-id="e6b31-178">在 Linux 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="e6b31-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="e6b31-179">在 OSX 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="e6b31-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="e6b31-180">使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="e6b31-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="e6b31-181">在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="e6b31-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="e6b31-182">在 Linux 上建立第一個 CSharp 應用程式</span><span class="sxs-lookup"><span data-stu-id="e6b31-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="e6b31-183">使用 hello 服務網狀架構 CLI toomanage 您應用程式</span><span class="sxs-lookup"><span data-stu-id="e6b31-183">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
