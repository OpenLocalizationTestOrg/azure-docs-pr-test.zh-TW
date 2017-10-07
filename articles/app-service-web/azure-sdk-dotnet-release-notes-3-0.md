---
title: "aaaAzure SDK for.NET 3.0 版本資訊 |Microsoft 文件"
description: "Azure SDK for .NET 3.0 版本資訊"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="75192-103">Azure SDK for .NET 3.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="75192-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="75192-104">本主題包含適用於.NET 的 3.0 版的 hello Azure SDK 版本資訊。</span><span class="sxs-lookup"><span data-stu-id="75192-104">This topic includes release notes for version 3.0 of hello Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="75192-105">Azure SDK for .NET 3.0 發行摘要</span><span class="sxs-lookup"><span data-stu-id="75192-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="75192-106">發行日期︰2017/03/07</span><span class="sxs-lookup"><span data-stu-id="75192-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="75192-107">在此版本中引進了沒有重大變更 toohello Azure SDK 3.0。</span><span class="sxs-lookup"><span data-stu-id="75192-107">No breaking changes toohello Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="75192-108">沒有也需要升級的程序 tooleverage 此 SDK 與現有的雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="75192-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="75192-109">tooallow 使用 hello Azure SDK 3.0 而不需要升級程序，Azure SDK 3.0 安裝 toohello 為 Azure SDK 2.9 中相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="75192-109">tooallow use of hello Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs toohello same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="75192-110">大部分的 hello 元件並未從 2.9 變更 hello 主要版本，但改為更新 hello 組建編號。</span><span class="sxs-lookup"><span data-stu-id="75192-110">Most hello components did not change hello major version from 2.9 but instead just updated hello build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="75192-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="75192-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="75192-112">在 Visual Studio 2017，這一版的 hello Azure SDK for.NET 內建 toohello Azure 工作負載。</span><span class="sxs-lookup"><span data-stu-id="75192-112">In Visual Studio 2017, this release of hello Azure SDK for .NET is built in toohello Azure Workload.</span></span> <span data-ttu-id="75192-113">Toodo Azure 開發所需的所有 hello 工具將會都是 Visual Studio 2017 往後的一部分。</span><span class="sxs-lookup"><span data-stu-id="75192-113">All hello tools you need toodo Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="75192-114">Visual Studio 2015 的 hello SDK 仍可透過 WebPI。</span><span class="sxs-lookup"><span data-stu-id="75192-114">For Visual Studio 2015 hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="75192-115">現在既然已釋出 Visual Studio 2017，我們已不再提供 Visual Studio 2013 適用的 Azure SDK .NET 版本。</span><span class="sxs-lookup"><span data-stu-id="75192-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="75192-116">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="75192-116">Azure Diagnostics</span></span>

- <span data-ttu-id="75192-117">已變更的 hello 行為 tooonly 儲存部分連接字串與 hello 索引鍵的雲端服務診斷儲存體連接字串語彙基元所取代。</span><span class="sxs-lookup"><span data-stu-id="75192-117">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="75192-118">hello 實際的儲存體金鑰現在會儲存在 hello 使用者設定檔資料夾，所以可以控制其存取權。</span><span class="sxs-lookup"><span data-stu-id="75192-118">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="75192-119">Visual Studio 會從本機偵錯和發行程序的使用者設定檔資料夾讀取 hello 儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="75192-119">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="75192-120">在回應 toohello 變更上面所述，Visual Studio Online team 增強的 hello Azure 雲端服務部署工作範本讓使用者可以指定發佈 tooAzure 連續整合時，設定診斷延伸模組的 hello 儲存體金鑰與部署。</span><span class="sxs-lookup"><span data-stu-id="75192-120">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="75192-121">我們已經可能 toostore 安全的連接字串和 token 化的 Azure 診斷 (WAD)，toohelp 您跨 environements 解決組態問題。</span><span class="sxs-lookup"><span data-stu-id="75192-121">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="75192-122">Windows Server 2016 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="75192-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="75192-123">Visual Studio 現在支援部署雲端服務 tooOS 系列 5 (Windows Server 2016) 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="75192-123">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="75192-124">對於現有的雲端服務，您可以變更設定 tootarget hello 新的 OS 系列。</span><span class="sxs-lookup"><span data-stu-id="75192-124">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="75192-125">在建立新的雲端服務，如果您選擇使用.net 4.6 或更高的 toocreate hello 服務時，它將預設 hello 服務 toouse OS 系列 5。</span><span class="sxs-lookup"><span data-stu-id="75192-125">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="75192-126">如需詳細資訊，您可以檢閱 hello[客體作業系統系列支援資料表](../cloud-services/cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="75192-126">For more information, you can review hello [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="75192-127">已知問題</span><span class="sxs-lookup"><span data-stu-id="75192-127">Known issues</span></span>

- <span data-ttu-id="75192-128">Azure .NET SDK 3.0 中造成了在 Visual Studio 2015 的並存組態中移除 Visual Studio 2017 時的問題。</span><span class="sxs-lookup"><span data-stu-id="75192-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="75192-129">如果您擁有 hello Azure SDK for Visual Studio 2015 安裝，hello Microsoft Azure 儲存體模擬器與 Microsoft Azure 計算模擬器將會移除當您解除安裝 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="75192-129">If you have hello Azure SDK installed for Visual Studio 2015, hello Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="75192-130">這會在 Visual Studio 2015 建立和偵錯新雲端服務專案時產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="75192-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="75192-131">在排序 toofix 此問題，重新安裝 hello Web Platform Installer 從 hello Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="75192-131">In order toofix this issue,  reinstall hello Azure SDK from hello Web Platform Installer.</span></span>  <span data-ttu-id="75192-132">hello 問題將獲得解決在未來的 Visual Studio 2017 更新中。</span><span class="sxs-lookup"><span data-stu-id="75192-132">hello issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="75192-133">.</span><span class="sxs-lookup"><span data-stu-id="75192-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="75192-134">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="75192-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="75192-135">2016 年 11 月 30 日終止支援 Azure In-Role Cache。</span><span class="sxs-lookup"><span data-stu-id="75192-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="75192-136">如需詳細資訊，請按一下[這裡](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)。</span><span class="sxs-lookup"><span data-stu-id="75192-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>




