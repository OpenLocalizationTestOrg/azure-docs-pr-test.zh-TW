---
title: "Azure SDK for .NET 3.0 版本資訊 | Microsoft 文件"
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
ms.openlocfilehash: eea4e569ac2d0192ed7872d2fcb9bed03614832b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="86884-103">Azure SDK for .NET 3.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="86884-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="86884-104">本主題包含 Azure SDK for .NET 3.0 版的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="86884-104">This topic includes release notes for version 3.0 of the Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="86884-105">Azure SDK for .NET 3.0 發行摘要</span><span class="sxs-lookup"><span data-stu-id="86884-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="86884-106">發行日期︰2017/03/07</span><span class="sxs-lookup"><span data-stu-id="86884-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="86884-107">Azure SDK 3.0 在此版本中沒有重大變更。</span><span class="sxs-lookup"><span data-stu-id="86884-107">No breaking changes to the Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="86884-108">在現有的雲端服務專案上使用這套 SDK 也不需要升級程序。</span><span class="sxs-lookup"><span data-stu-id="86884-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="86884-109">為了在無需升級程序的情況下允許使用 Azure SDK 3.0，Azure SDK 3.0 會安裝至與 Azure SDK 2.9 相同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="86884-109">To allow use of the Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs to the same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="86884-110">大部分元件的主要版本並未自 2.9 變更，而是只更新組建編號。</span><span class="sxs-lookup"><span data-stu-id="86884-110">Most the components did not change the major version from 2.9 but instead just updated the build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="86884-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="86884-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="86884-112">在 Visual Studio 2017 中，這個版本的 Azure SDK for .NET 內建於 Azure 工作負載。</span><span class="sxs-lookup"><span data-stu-id="86884-112">In Visual Studio 2017, this release of the Azure SDK for .NET is built in to the Azure Workload.</span></span> <span data-ttu-id="86884-113">未來將會在 Visual Studio 2017 中提供您開發 Azure 所需的一切工具。</span><span class="sxs-lookup"><span data-stu-id="86884-113">All the tools you need to do Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="86884-114">在 Visual Studio 2015 中，將仍然可以透過 WebPI 使用這套 SDK。</span><span class="sxs-lookup"><span data-stu-id="86884-114">For Visual Studio 2015 the SDK will still be available through WebPI.</span></span> <span data-ttu-id="86884-115">現在既然已釋出 Visual Studio 2017，我們已不再提供 Visual Studio 2013 適用的 Azure SDK .NET 版本。</span><span class="sxs-lookup"><span data-stu-id="86884-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="86884-116">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="86884-116">Azure Diagnostics</span></span>

- <span data-ttu-id="86884-117">已變更為只儲存部分連接字串，並以雲端服務儲存體連接字串的權杖取代金鑰。</span><span class="sxs-lookup"><span data-stu-id="86884-117">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="86884-118">實際的儲存體金鑰現在儲存在使用者設定檔資料夾中，方便控制其存取權。</span><span class="sxs-lookup"><span data-stu-id="86884-118">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="86884-119">Visual Studio 會從使用者設定檔資料夾中讀取儲存體金鑰，以執行本機偵錯和發佈程序。</span><span class="sxs-lookup"><span data-stu-id="86884-119">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="86884-120">為了因應上述變更，Visual Studio Online 小組已增強 Azure 雲端服務部署工作範本，當使用者在持續整合及部署中發佈至 Azure 時，可以指定儲存體金鑰來設定診斷擴充。</span><span class="sxs-lookup"><span data-stu-id="86884-120">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="86884-121">我們已可讓您儲存安全連接字串和 Azure 診斷 (WAD) 的 Token 化，協助您解決跨環境組態的問題。</span><span class="sxs-lookup"><span data-stu-id="86884-121">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="86884-122">Windows Server 2016 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="86884-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="86884-123">Visual Studio 現在支援將雲端服務部署到作業系統系列 5 (Windows Server 2016) 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="86884-123">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="86884-124">對於現有的雲端服務，您可以變更設定，以新的作業系統系列為目標。</span><span class="sxs-lookup"><span data-stu-id="86884-124">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="86884-125">建立新的雲端服務時，如果您選擇使用 .net 4.6 或更高版本建立服務，服務會預設為使用作業系統系列 5。</span><span class="sxs-lookup"><span data-stu-id="86884-125">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="86884-126">如需詳細資訊，您可以檢閱[客體 OS 系列支援資料表](../cloud-services/cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="86884-126">For more information, you can review the [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="86884-127">已知問題</span><span class="sxs-lookup"><span data-stu-id="86884-127">Known issues</span></span>

- <span data-ttu-id="86884-128">Azure .NET SDK 3.0 中造成了在 Visual Studio 2015 的並存組態中移除 Visual Studio 2017 時的問題。</span><span class="sxs-lookup"><span data-stu-id="86884-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="86884-129">如果已安裝 Visual Studio 2015 的 Azure SDK，如果解除安裝 Visual Studio 2017，將會移除 Microsoft Azure 儲存體模擬器和 Microsoft Azure 計算模擬器。</span><span class="sxs-lookup"><span data-stu-id="86884-129">If you have the Azure SDK installed for Visual Studio 2015, the Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="86884-130">這會在 Visual Studio 2015 建立和偵錯新雲端服務專案時產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="86884-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="86884-131">若要修正這個問題，請透過 Web Platform Installer 重新安裝 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="86884-131">In order to fix this issue,  reinstall the Azure SDK from the Web Platform Installer.</span></span>  <span data-ttu-id="86884-132">此問題將在未來的 Visual Studio 2017 更新中獲得解決。</span><span class="sxs-lookup"><span data-stu-id="86884-132">The issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="86884-133">。</span><span class="sxs-lookup"><span data-stu-id="86884-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="86884-134">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="86884-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="86884-135">2016 年 11 月 30 日終止支援 Azure In-Role Cache。</span><span class="sxs-lookup"><span data-stu-id="86884-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="86884-136">如需詳細資訊，請按一下[這裡](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)。</span><span class="sxs-lookup"><span data-stu-id="86884-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>




