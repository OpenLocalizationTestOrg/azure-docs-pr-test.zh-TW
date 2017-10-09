---
title: "開發環境，如 Azure microservices aaaSet |Microsoft 文件"
description: "安裝 hello 執行階段、 SDK 和工具，並建立本機開發叢集。 完成此安裝之後，您將準備 toobuild 應用程式。"
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
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="8c354-104">準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="8c354-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c354-105">Windows</span><span class="sxs-lookup"><span data-stu-id="8c354-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="8c354-106">Linux</span><span class="sxs-lookup"><span data-stu-id="8c354-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="8c354-107">OSX</span><span class="sxs-lookup"><span data-stu-id="8c354-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="8c354-108">toobuild 並執行[Azure Service Fabric 應用程式][ 1]在您的開發電腦上安裝 [hello 執行階段、 SDK 和工具。</span><span class="sxs-lookup"><span data-stu-id="8c354-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="8c354-109">您也需要 tooenable hello hello SDK 中包含的 Windows PowerShell 指令碼執行。</span><span class="sxs-lookup"><span data-stu-id="8c354-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c354-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8c354-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="8c354-111">支援的作業系統版本</span><span class="sxs-lookup"><span data-stu-id="8c354-111">Supported operating system versions</span></span>
<span data-ttu-id="8c354-112">開發可支援下列作業系統版本的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c354-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="8c354-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8c354-113">Windows 7</span></span>
* <span data-ttu-id="8c354-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8c354-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="8c354-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8c354-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="8c354-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8c354-116">Windows Server 2016</span></span>
* <span data-ttu-id="8c354-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="8c354-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="8c354-118">根據預設，Windows 7 只包含 Windows PowerShell 2.0。</span><span class="sxs-lookup"><span data-stu-id="8c354-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="8c354-119">Service Fabric PowerShell Cmdlet 需要 PowerShell 3.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8c354-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="8c354-120">您可以[下載 Windows PowerShell 5.0] [ powershell5-download]從 Microsoft 下載中心 hello。</span><span class="sxs-lookup"><span data-stu-id="8c354-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="8c354-121">安裝 hello SDK 和工具</span><span class="sxs-lookup"><span data-stu-id="8c354-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="8c354-122">Visual Studio 2017 toouse</span><span class="sxs-lookup"><span data-stu-id="8c354-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="8c354-123">Service Fabric 工具是在 Visual Studio 2017 hello Azure 開發和管理工作負載的一部分。</span><span class="sxs-lookup"><span data-stu-id="8c354-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="8c354-124">啟用此工作負載作為 Visual Studio 安裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="8c354-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="8c354-125">此外，您需要 tooinstall hello Microsoft Azure Service Fabric SDK，使用 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="8c354-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="8c354-126">[安裝 Microsoft Azure Service Fabric SDK hello][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="8c354-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="8c354-127">toouse Visual Studio 2015 （需要 Visual Studio 2015 Update 2 或更新版本）</span><span class="sxs-lookup"><span data-stu-id="8c354-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="8c354-128">Visual Studio 2015，Service Fabric 工具會安裝與 hello SDK，使用 Web Platform Installer hello:</span><span class="sxs-lookup"><span data-stu-id="8c354-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="8c354-129">[安裝 Microsoft Azure Service Fabric SDK hello 和工具][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="8c354-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="8c354-130">僅限 SDK 安裝</span><span class="sxs-lookup"><span data-stu-id="8c354-130">SDK installation only</span></span>
<span data-ttu-id="8c354-131">如果您只需要 hello SDK，您可以安裝此套件：</span><span class="sxs-lookup"><span data-stu-id="8c354-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="8c354-132">[安裝 Microsoft Azure Service Fabric SDK hello][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="8c354-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="8c354-133">hello 目前的版本如下：</span><span class="sxs-lookup"><span data-stu-id="8c354-133">hello current versions are:</span></span>
* <span data-ttu-id="8c354-134">Service Fabric SDK 2.7.198</span><span class="sxs-lookup"><span data-stu-id="8c354-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="8c354-135">Service Fabric 執行階段 5.7.198</span><span class="sxs-lookup"><span data-stu-id="8c354-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="8c354-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="8c354-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="8c354-137">Visual Studio 2017 Update 2 包含 Service Fabric Tools for Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="8c354-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="8c354-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) 包含 Service Fabric Tools for Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="8c354-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="8c354-139">如需支援版本的清單，請參閱[Service Fabric 支援](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="8c354-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="8c354-140">啟用 PowerShell 指令碼執行</span><span class="sxs-lookup"><span data-stu-id="8c354-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="8c354-141">Service Fabric 會使用 Windows PowerShell 指令碼，以便建立本機開發叢集，以及從 Visual Studio 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c354-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="8c354-142">根據預設，Windows 會封鎖這些指令碼的執行。</span><span class="sxs-lookup"><span data-stu-id="8c354-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="8c354-143">tooenable 它們，您必須修改您的 PowerShell 執行原則。</span><span class="sxs-lookup"><span data-stu-id="8c354-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="8c354-144">系統管理員身分開啟 PowerShell 並輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c354-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="8c354-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c354-145">Next steps</span></span>
<span data-ttu-id="8c354-146">現在您的開發環境已完成設定，您可以開始建置和執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c354-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="8c354-147">在 Visual Studio 中建立第一個 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="8c354-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="8c354-148">深入了解如何 toodeploy 和管理您的本機叢集上的應用程式</span><span class="sxs-lookup"><span data-stu-id="8c354-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="8c354-149">深入了解 hello 程式設計模型： 可靠的服務和 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="8c354-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="8c354-150">簽出 hello Service Fabric GitHub 上的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="8c354-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="8c354-151">使用 Service Fabric 總管將叢集視覺化</span><span class="sxs-lookup"><span data-stu-id="8c354-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="8c354-152">請遵循 hello Service Fabric 學習路徑 tooget 廣泛簡介 toohello 平台</span><span class="sxs-lookup"><span data-stu-id="8c354-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="8c354-153">了解 [Service Fabric 支援選項](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="8c354-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric 活動頁面"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI 連結"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI 連結"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI 連結"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
