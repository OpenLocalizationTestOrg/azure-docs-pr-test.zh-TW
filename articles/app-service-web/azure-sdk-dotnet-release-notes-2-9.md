---
title: "Azure SDK for .NET 2.9 版本資訊"
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
ms.openlocfilehash: 199f0906f73d693d7cd4b73c928f23ae83b99596
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="4cea5-103">Azure SDK for .NET 2.9 版本資訊</span><span class="sxs-lookup"><span data-stu-id="4cea5-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="4cea5-104">本主題包含 Azure SDK for .NET 2.9 和 2.9.6 版的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="4cea5-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="4cea5-105">Azure SDK for .NET 2.9.6 發行摘要</span><span class="sxs-lookup"><span data-stu-id="4cea5-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="4cea5-106">發行日期︰2016/11/16</span><span class="sxs-lookup"><span data-stu-id="4cea5-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="4cea5-107">Azure SDK 2.9 在此版本中沒有重大變更。</span><span class="sxs-lookup"><span data-stu-id="4cea5-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="4cea5-108">在現有的雲端服務專案上使用這套 SDK 也不需要升級程序。</span><span class="sxs-lookup"><span data-stu-id="4cea5-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="4cea5-109">Visual Studio 2017 候選版</span><span class="sxs-lookup"><span data-stu-id="4cea5-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="4cea5-110">在 Visual Studio 2017 RC 中，這個版本的 Azure SDK for .NET 內建於 Azure 工作負載。</span><span class="sxs-lookup"><span data-stu-id="4cea5-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span></span> <span data-ttu-id="4cea5-111">未來將會在 Visual Studio 2017 RC 中提供您開發 Azure 所需的一切工具。</span><span class="sxs-lookup"><span data-stu-id="4cea5-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="4cea5-112">在 Visual Studio 2015 和 Visual Studio 2013 中，將仍然可以透過 WebPI 使用這套 SDK。</span><span class="sxs-lookup"><span data-stu-id="4cea5-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span></span> <span data-ttu-id="4cea5-113">當 Visual Studio 2017 以最終產品發行時，我們就不再提供適用於 Visual Studio 2013 的 Azure SDK for .NET 版本。</span><span class="sxs-lookup"><span data-stu-id="4cea5-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="4cea5-114">請透過此連結來下載 Visual Studio 2017 RC：https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="4cea5-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="4cea5-115">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="4cea5-115">Azure Diagnostics</span></span>

- <span data-ttu-id="4cea5-116">已變更為只儲存部分連接字串，並以雲端服務儲存體連接字串的權杖取代金鑰。</span><span class="sxs-lookup"><span data-stu-id="4cea5-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="4cea5-117">實際的儲存體金鑰現在儲存在使用者設定檔資料夾中，方便控制其存取權。</span><span class="sxs-lookup"><span data-stu-id="4cea5-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="4cea5-118">Visual Studio 會從使用者設定檔資料夾中讀取儲存體金鑰，以執行本機偵錯和發佈程序。</span><span class="sxs-lookup"><span data-stu-id="4cea5-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="4cea5-119">為了因應上述變更，Visual Studio Online 小組已增強 Azure 雲端服務部署工作範本，當使用者在持續整合及部署中發佈至 Azure 時，可以指定儲存體金鑰來設定診斷擴充。</span><span class="sxs-lookup"><span data-stu-id="4cea5-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="4cea5-120">我們已可讓您儲存安全連接字串和 Azure 診斷 (WAD) 的 Token 化，協助您解決跨環境組態的問題。</span><span class="sxs-lookup"><span data-stu-id="4cea5-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="4cea5-121">Windows Server 2016 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4cea5-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="4cea5-122">Visual Studio 現在支援將雲端服務部署到作業系統系列 5 (Windows Server 2016) 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4cea5-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="4cea5-123">對於現有的雲端服務，您可以變更設定，以新的作業系統系列為目標。</span><span class="sxs-lookup"><span data-stu-id="4cea5-123">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="4cea5-124">建立新的雲端服務時，如果您選擇使用 .net 4.6 或更高版本建立服務，服務會預設為使用作業系統系列 5。</span><span class="sxs-lookup"><span data-stu-id="4cea5-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="4cea5-125">如需詳細資訊，您可以檢閱[客體 OS 系列支援資料表](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/)。</span><span class="sxs-lookup"><span data-stu-id="4cea5-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4cea5-126">已知問題</span><span class="sxs-lookup"><span data-stu-id="4cea5-126">Known issues</span></span>

- <span data-ttu-id="4cea5-127">Azure.NET SDK 2.9.6 引進了一項限制，會使用不支援的 .NET Framework (例如 .NET 4.6) 至任何 < 5 的作業系統系列封鎖專案的部署。</span><span class="sxs-lookup"><span data-stu-id="4cea5-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span></span> <span data-ttu-id="4cea5-128">因應措施提供於[這裡](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9)。</span><span class="sxs-lookup"><span data-stu-id="4cea5-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="4cea5-129">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="4cea5-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="4cea5-130">2016 年 11 月 30 日終止支援 Azure In-Role Cache。</span><span class="sxs-lookup"><span data-stu-id="4cea5-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="4cea5-131">如需詳細資訊，請按一下[這裡](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)。</span><span class="sxs-lookup"><span data-stu-id="4cea5-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="4cea5-132">適用於 Azure Stack 的 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="4cea5-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="4cea5-133">我們已引進 Azure Stack 做為 Azure Resource Manager 範本的部署目標。</span><span class="sxs-lookup"><span data-stu-id="4cea5-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="4cea5-134">Azure SDK for .NET 2.9 摘要</span><span class="sxs-lookup"><span data-stu-id="4cea5-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="4cea5-135">概觀</span><span class="sxs-lookup"><span data-stu-id="4cea5-135">Overview</span></span>
<span data-ttu-id="4cea5-136">本文包含 Azure SDK for .NET 2.9 版的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="4cea5-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="4cea5-137">如需此版本之更新內容的詳細資訊，請參閱 [Azure SDK 2.9 公告文章](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)。</span><span class="sxs-lookup"><span data-stu-id="4cea5-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="4cea5-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 和 Visual Studio "15" 預覽</span><span class="sxs-lookup"><span data-stu-id="4cea5-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="4cea5-139">此更新包含下列錯誤修正：</span><span class="sxs-lookup"><span data-stu-id="4cea5-139">This update includes the following bug fixes:</span></span>

* <span data-ttu-id="4cea5-140">與 REST API 用戶端產生有關的問題，在此問題中，字串「未知類型」會出現成為 code-gen 資料夾的名稱和/或放入所產生程式碼之命名空間的名稱。</span><span class="sxs-lookup"><span data-stu-id="4cea5-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span></span>
* <span data-ttu-id="4cea5-141">與排程的 WebJobs 有關的問題，在此問題中，驗證資訊無法傳遞給排程器佈建程序。</span><span class="sxs-lookup"><span data-stu-id="4cea5-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span></span>

<span data-ttu-id="4cea5-142">此更新包含下列新功能：</span><span class="sxs-lookup"><span data-stu-id="4cea5-142">This update includes the following new feature:</span></span>

* <span data-ttu-id="4cea5-143">在 App Service 佈建對話方塊的 [服務] 索引標籤中支援第二個 App Service。</span><span class="sxs-lookup"><span data-stu-id="4cea5-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="4cea5-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="4cea5-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="4cea5-145">此更新包含下列工具：</span><span class="sxs-lookup"><span data-stu-id="4cea5-145">This updates includes the following:</span></span>

* <span data-ttu-id="4cea5-146">**Azure Data Lake Tools** for Visual Studio 現在已合併到 Azure SDK for .NET 版本。</span><span class="sxs-lookup"><span data-stu-id="4cea5-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span></span> <span data-ttu-id="4cea5-147">當您安裝 Azure SDK 時，便會自動安裝此工具。</span><span class="sxs-lookup"><span data-stu-id="4cea5-147">The tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="4cea5-148">此工具會經常更新，請前往 [這裡](http://aka.ms/datalaketool) 取得更新。</span><span class="sxs-lookup"><span data-stu-id="4cea5-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span></span>
* <span data-ttu-id="4cea5-149">**伺服器總管** 現在可讓您全部檢視，並建立一些 U-SQL 中繼資料實體。</span><span class="sxs-lookup"><span data-stu-id="4cea5-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="4cea5-150">如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/documentation/services/data-lake-analytics/) 。</span><span class="sxs-lookup"><span data-stu-id="4cea5-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="4cea5-151">HDInsight 工具</span><span class="sxs-lookup"><span data-stu-id="4cea5-151">HDInsight Tools</span></span>
<span data-ttu-id="4cea5-152">**HDInsight Tools** for Visual Studio 現在支援 HDInsight 3.3 版，包括顯示 Tez 圖形和其他語言修正。</span><span class="sxs-lookup"><span data-stu-id="4cea5-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="4cea5-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4cea5-153">Azure Resource Manager</span></span>
<span data-ttu-id="4cea5-154">此版本為 Resource Manager 範本新增[金鑰保存庫](../azure-resource-manager/resource-manager-keyvault-parameter.md)支援。</span><span class="sxs-lookup"><span data-stu-id="4cea5-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="4cea5-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4cea5-155">See also</span></span>
[<span data-ttu-id="4cea5-156">Azure SDK 2.9 公告文章</span><span class="sxs-lookup"><span data-stu-id="4cea5-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

