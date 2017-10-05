---
title: "設定 Azure 微服務的開發環境 | Microsoft Docs"
description: "安裝執行階段、SDK 和工具，並建立本機開發叢集。 完成此設定之後，您就可以開始建置應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: f0c6957217c21bdfd76498944e248fc808f2d271
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="8a270-104">準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="8a270-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a270-105">Windows</span><span class="sxs-lookup"><span data-stu-id="8a270-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="8a270-106">Linux</span><span class="sxs-lookup"><span data-stu-id="8a270-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="8a270-107">OSX</span><span class="sxs-lookup"><span data-stu-id="8a270-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="8a270-108">若要在您的開發機器上建置並執行 [Azure Service Fabric 應用程式][1]，請安裝執行階段、SDK 和工具。</span><span class="sxs-lookup"><span data-stu-id="8a270-108">To build and run [Azure Service Fabric applications][1] on your development machine, install the runtime, SDK, and tools.</span></span> <span data-ttu-id="8a270-109">您也必須執行 SDK 中包含的 Windows PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8a270-109">You also need to enable execution of the Windows PowerShell scripts included in the SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a270-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8a270-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="8a270-111">支援的作業系統版本</span><span class="sxs-lookup"><span data-stu-id="8a270-111">Supported operating system versions</span></span>
<span data-ttu-id="8a270-112">下列為支援開發的作業系統版本：</span><span class="sxs-lookup"><span data-stu-id="8a270-112">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="8a270-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8a270-113">Windows 7</span></span>
* <span data-ttu-id="8a270-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8a270-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="8a270-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8a270-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="8a270-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8a270-116">Windows Server 2016</span></span>
* <span data-ttu-id="8a270-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="8a270-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="8a270-118">根據預設，Windows 7 只包含 Windows PowerShell 2.0。</span><span class="sxs-lookup"><span data-stu-id="8a270-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="8a270-119">Service Fabric PowerShell Cmdlet 需要 PowerShell 3.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8a270-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="8a270-120">您可以從 Microsoft 下載中心[下載 Windows PowerShell 5.0][powershell5-download]。</span><span class="sxs-lookup"><span data-stu-id="8a270-120">You can [download Windows PowerShell 5.0][powershell5-download] from the Microsoft Download Center.</span></span>
> 
> 

## <a name="install-the-sdk-and-tools"></a><span data-ttu-id="8a270-121">安裝 SDK 和工具</span><span class="sxs-lookup"><span data-stu-id="8a270-121">Install the SDK and tools</span></span>
### <a name="to-use-visual-studio-2017"></a><span data-ttu-id="8a270-122">若要使用 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8a270-122">To use Visual Studio 2017</span></span>
<span data-ttu-id="8a270-123">Service Fabric 工具屬於 Visual Studio 2017 中的 Azure 開發和管理工作負載。</span><span class="sxs-lookup"><span data-stu-id="8a270-123">Service Fabric Tools are part of the Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="8a270-124">啟用此工作負載作為 Visual Studio 安裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="8a270-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="8a270-125">此外，您必須使用 Web Platform Installer 來安裝 Microsoft Azure Service Fabric SDK。</span><span class="sxs-lookup"><span data-stu-id="8a270-125">In addition, you need to install the Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="8a270-126">[安裝 Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="8a270-126">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="8a270-127">若要使用 Visual Studio 2015 (需要 Visual Studio 2015 Update 2 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="8a270-127">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="8a270-128">在 Visual Studio 2015 中，使用 Web Platform Installer，Service Fabric 工具會與 SDK 一起安裝︰</span><span class="sxs-lookup"><span data-stu-id="8a270-128">For Visual Studio 2015, Service Fabric tools are installed together with the SDK, using the Web Platform Installer:</span></span>

* <span data-ttu-id="8a270-129">[安裝 Microsoft Azure Service Fabric SDK 和工具][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="8a270-129">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="8a270-130">僅限 SDK 安裝</span><span class="sxs-lookup"><span data-stu-id="8a270-130">SDK installation only</span></span>
<span data-ttu-id="8a270-131">如果您只需要 SDK，您可以安裝此套件︰</span><span class="sxs-lookup"><span data-stu-id="8a270-131">If you only need the SDK, you can install this package:</span></span>
* <span data-ttu-id="8a270-132">[安裝 Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="8a270-132">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="8a270-133">目前的版本如下︰</span><span class="sxs-lookup"><span data-stu-id="8a270-133">The current versions are:</span></span>
* <span data-ttu-id="8a270-134">Service Fabric SDK 2.7.198</span><span class="sxs-lookup"><span data-stu-id="8a270-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="8a270-135">Service Fabric 執行階段 5.7.198</span><span class="sxs-lookup"><span data-stu-id="8a270-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="8a270-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="8a270-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="8a270-137">Visual Studio 2017 Update 2 包含 Service Fabric Tools for Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="8a270-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="8a270-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) 包含 Service Fabric Tools for Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="8a270-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="8a270-139">如需支援版本的清單，請參閱[Service Fabric 支援](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="8a270-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="8a270-140">啟用 PowerShell 指令碼執行</span><span class="sxs-lookup"><span data-stu-id="8a270-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="8a270-141">Service Fabric 會使用 Windows PowerShell 指令碼，以便建立本機開發叢集，以及從 Visual Studio 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a270-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="8a270-142">根據預設，Windows 會封鎖這些指令碼的執行。</span><span class="sxs-lookup"><span data-stu-id="8a270-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="8a270-143">若要啟用其，您必須修改 PowerShell 執行原則。</span><span class="sxs-lookup"><span data-stu-id="8a270-143">To enable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="8a270-144">以系統管理員身分開啟 PowerShell 並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="8a270-144">Open PowerShell as an administrator and enter the following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="8a270-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a270-145">Next steps</span></span>
<span data-ttu-id="8a270-146">現在您的開發環境已完成設定，您可以開始建置和執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a270-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="8a270-147">在 Visual Studio 中建立第一個 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a270-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="8a270-148">了解如何在本機叢集上部署和管理應用程式</span><span class="sxs-lookup"><span data-stu-id="8a270-148">Learn how to deploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="8a270-149">深入了解程式設計模型：Reliable Services 和 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="8a270-149">Learn about the programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="8a270-150">請查看 GitHub 上的 Service Fabric 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="8a270-150">Check out the Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="8a270-151">使用 Service Fabric 總管將叢集視覺化</span><span class="sxs-lookup"><span data-stu-id="8a270-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="8a270-152">遵循 Service Fabric 學習路徑來取得廣泛的平台簡介</span><span class="sxs-lookup"><span data-stu-id="8a270-152">Follow the Service Fabric learning path to get a broad introduction to the platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="8a270-153">了解 [Service Fabric 支援選項](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="8a270-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

<span data-ttu-id="8a270-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric 活動頁面"</span><span class="sxs-lookup"><span data-stu-id="8a270-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric campaign page"</span></span>
<span data-ttu-id="8a270-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span><span class="sxs-lookup"><span data-stu-id="8a270-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span></span>
<span data-ttu-id="8a270-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI 連結"</span><span class="sxs-lookup"><span data-stu-id="8a270-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"</span></span>
<span data-ttu-id="8a270-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI 連結"</span><span class="sxs-lookup"><span data-stu-id="8a270-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"</span></span>
<span data-ttu-id="8a270-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI 連結"</span><span class="sxs-lookup"><span data-stu-id="8a270-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"</span></span>
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
