---
title: "aaaAzure SDK for.NET 2.9 版本資訊"
description: "Azure SDK for .NET 2.9 版本資訊"
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
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="2670b-103">Azure SDK for .NET 2.9 版本資訊</span><span class="sxs-lookup"><span data-stu-id="2670b-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="2670b-104">本主題包含 Azure SDK for .NET 2.9 和 2.9.6 版的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="2670b-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="2670b-105">Azure SDK for .NET 2.9.6 發行摘要</span><span class="sxs-lookup"><span data-stu-id="2670b-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="2670b-106">發行日期︰2016/11/16</span><span class="sxs-lookup"><span data-stu-id="2670b-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="2670b-107">在此版本中引進了沒有重大變更 toohello Azure SDK 2.9 中。</span><span class="sxs-lookup"><span data-stu-id="2670b-107">No breaking changes toohello Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="2670b-108">沒有也需要升級的程序 tooleverage 此 SDK 與現有的雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="2670b-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="2670b-109">Visual Studio 2017 候選版</span><span class="sxs-lookup"><span data-stu-id="2670b-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="2670b-110">在 Visual Studio 2017 RC 中，這一版的 hello Azure SDK for.NET 是內建在 hello Azure 工作負載。</span><span class="sxs-lookup"><span data-stu-id="2670b-110">In Visual Studio 2017 RC, this release of hello Azure SDK for .NET is built in in hello Azure Workload.</span></span> <span data-ttu-id="2670b-111">Toodo Azure 開發所需的所有 hello 工具將會都是 Visual Studio 2017 RC 往後的一部分。</span><span class="sxs-lookup"><span data-stu-id="2670b-111">All hello tools you need toodo Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="2670b-112">Visual Studio 2015 和 Visual Studio 2013，hello SDK 仍可透過 WebPI。</span><span class="sxs-lookup"><span data-stu-id="2670b-112">For Visual Studio 2015 and Visual Studio 2013, hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="2670b-113">當 Visual Studio 2017 以最終產品發行時，我們就不再提供適用於 Visual Studio 2013 的 Azure SDK for .NET 版本。</span><span class="sxs-lookup"><span data-stu-id="2670b-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="2670b-114">請依照此連結 toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="2670b-114">Follow this link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="2670b-115">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="2670b-115">Azure Diagnostics</span></span>

- <span data-ttu-id="2670b-116">已變更的 hello 行為 tooonly 儲存部分連接字串與 hello 索引鍵的雲端服務診斷儲存體連接字串語彙基元所取代。</span><span class="sxs-lookup"><span data-stu-id="2670b-116">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="2670b-117">hello 實際的儲存體金鑰現在會儲存在 hello 使用者設定檔資料夾，所以可以控制其存取權。</span><span class="sxs-lookup"><span data-stu-id="2670b-117">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="2670b-118">Visual Studio 會從本機偵錯和發行程序的使用者設定檔資料夾讀取 hello 儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="2670b-118">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="2670b-119">在回應 toohello 變更上面所述，Visual Studio Online team 增強的 hello Azure 雲端服務部署工作範本讓使用者可以指定發佈 tooAzure 連續整合時，設定診斷延伸模組的 hello 儲存體金鑰與部署。</span><span class="sxs-lookup"><span data-stu-id="2670b-119">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="2670b-120">我們已經可能 toostore 安全的連接字串和 token 化的 Azure 診斷 (WAD)，toohelp 您跨 environements 解決組態問題。</span><span class="sxs-lookup"><span data-stu-id="2670b-120">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="2670b-121">Windows Server 2016 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2670b-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="2670b-122">Visual Studio 現在支援部署雲端服務 tooOS 系列 5 (Windows Server 2016) 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2670b-122">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="2670b-123">對於現有的雲端服務，您可以變更設定 tootarget hello 新的 OS 系列。</span><span class="sxs-lookup"><span data-stu-id="2670b-123">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="2670b-124">在建立新的雲端服務，如果您選擇使用.net 4.6 或更高的 toocreate hello 服務時，它將預設 hello 服務 toouse OS 系列 5。</span><span class="sxs-lookup"><span data-stu-id="2670b-124">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="2670b-125">如需詳細資訊，您可以檢閱 hello[客體作業系統系列支援資料表](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/)。</span><span class="sxs-lookup"><span data-stu-id="2670b-125">For more information, you can review hello [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="2670b-126">已知問題</span><span class="sxs-lookup"><span data-stu-id="2670b-126">Known issues</span></span>

- <span data-ttu-id="2670b-127">Azure.NET SDK 2.9.6 引入的限制，會封鎖部署的專案使用不支援的.NET 架構 （例如.NET 4.6) tooany OS 系列 < 5。</span><span class="sxs-lookup"><span data-stu-id="2670b-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) tooany OS Family < 5.</span></span> <span data-ttu-id="2670b-128">因應措施提供於[這裡](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9)。</span><span class="sxs-lookup"><span data-stu-id="2670b-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="2670b-129">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="2670b-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="2670b-130">2016 年 11 月 30 日終止支援 Azure In-Role Cache。</span><span class="sxs-lookup"><span data-stu-id="2670b-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="2670b-131">如需詳細資訊，請按一下[這裡](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)。</span><span class="sxs-lookup"><span data-stu-id="2670b-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="2670b-132">適用於 Azure Stack 的 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="2670b-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="2670b-133">我們已引進 Azure Stack 做為 Azure Resource Manager 範本的部署目標。</span><span class="sxs-lookup"><span data-stu-id="2670b-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="2670b-134">Azure SDK for .NET 2.9 摘要</span><span class="sxs-lookup"><span data-stu-id="2670b-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="2670b-135">概觀</span><span class="sxs-lookup"><span data-stu-id="2670b-135">Overview</span></span>
<span data-ttu-id="2670b-136">本文件包含 hello hello Azure SDK for.NET 2.9 版的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="2670b-136">This document contains hello release notes for hello Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="2670b-137">如需此版本中更新的詳細資訊，請參閱 hello [Azure SDK 2.9 公告文章](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)。</span><span class="sxs-lookup"><span data-stu-id="2670b-137">For detailed information about updates in this release, see hello [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="2670b-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 和 Visual Studio "15" 預覽</span><span class="sxs-lookup"><span data-stu-id="2670b-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="2670b-139">此更新包含下列錯誤修正 hello:</span><span class="sxs-lookup"><span data-stu-id="2670b-139">This update includes hello following bug fixes:</span></span>

* <span data-ttu-id="2670b-140">發出相關的 tooREST API 產生用戶端中的 hello 字串中 「 未知的型別 」 會顯示成 hello hello 產生程式碼資料夾名稱和/或 hello hello 放入 hello 產生程式碼的命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="2670b-140">Issue related tooREST API Client Generation in in which hello string "Unknown Type” would appear as hello name of hello code-gen folder and/or hello name of hello namespace dropped into hello generated code.</span></span>
* <span data-ttu-id="2670b-141">發出的驗證資訊失敗 toobe 傳遞 toohello 排程器佈建程序中的 hello 相關的 tooScheduled WebJobs。</span><span class="sxs-lookup"><span data-stu-id="2670b-141">Issue related tooScheduled WebJobs in which hello authentication information was failing toobe passed toohello Scheduler provisioning process.</span></span>

<span data-ttu-id="2670b-142">此更新包含下列新功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="2670b-142">This update includes hello following new feature:</span></span>

* <span data-ttu-id="2670b-143">Hello App Service 佈建對話方塊 hello 「 服務 」 索引標籤中的第二個應用程式服務的支援。</span><span class="sxs-lookup"><span data-stu-id="2670b-143">Support for secondary App Services in hello "Services" tab of hello App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="2670b-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="2670b-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="2670b-145">此更新包含下列 hello:</span><span class="sxs-lookup"><span data-stu-id="2670b-145">This updates includes hello following:</span></span>

* <span data-ttu-id="2670b-146">**Azure Data Lake Tools** Visual Studio 現在合併成 hello Azure SDK for.NET 版本。</span><span class="sxs-lookup"><span data-stu-id="2670b-146">**Azure Data Lake Tools** for Visual Studio is now merged into hello Azure SDK for .NET release.</span></span> <span data-ttu-id="2670b-147">當您安裝 Azure SDK，hello 工具會自動安裝。</span><span class="sxs-lookup"><span data-stu-id="2670b-147">hello tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="2670b-148">hello 工具經常更新，請移[這裡](http://aka.ms/datalaketool)tooget hello 更新。</span><span class="sxs-lookup"><span data-stu-id="2670b-148">hello tool is updated frequently, go [here](http://aka.ms/datalaketool) tooget hello updates.</span></span>
* <span data-ttu-id="2670b-149">**伺服器總管**現在可讓您 tooview 所有，並建立一些 U-SQL 中繼資料實體。</span><span class="sxs-lookup"><span data-stu-id="2670b-149">**Server Explorer** now enables you tooview all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="2670b-150">如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/documentation/services/data-lake-analytics/) 。</span><span class="sxs-lookup"><span data-stu-id="2670b-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="2670b-151">HDInsight 工具</span><span class="sxs-lookup"><span data-stu-id="2670b-151">HDInsight Tools</span></span>
<span data-ttu-id="2670b-152">**HDInsight Tools** for Visual Studio 現在支援 HDInsight 3.3 版，包括顯示 Tez 圖形和其他語言修正。</span><span class="sxs-lookup"><span data-stu-id="2670b-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="2670b-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2670b-153">Azure Resource Manager</span></span>
<span data-ttu-id="2670b-154">此版本為 Resource Manager 範本新增[金鑰保存庫](../azure-resource-manager/resource-manager-keyvault-parameter.md)支援。</span><span class="sxs-lookup"><span data-stu-id="2670b-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="2670b-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2670b-155">See also</span></span>
[<span data-ttu-id="2670b-156">Azure SDK 2.9 公告文章</span><span class="sxs-lookup"><span data-stu-id="2670b-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

