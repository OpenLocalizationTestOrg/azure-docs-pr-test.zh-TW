---
title: "我的 WebJob 專案 (Visual Studio Azure 儲存體連接的服務) 發生什麼狀況？ | Microsoft Docs"
description: "說明使用 Visual Studio 已連接服務連接到儲存體帳戶後，會在 Azure WebJob 專案中發生什麼事"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3b28ddeadc87937941d60b16fae817e59a220b22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="f994f-104">我的 WebJob 專案 (Visual Studio Azure 儲存體連接的服務) 發生什麼狀況？</span><span class="sxs-lookup"><span data-stu-id="f994f-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="f994f-105">加入參考</span><span class="sxs-lookup"><span data-stu-id="f994f-105">References Added</span></span>
<span data-ttu-id="f994f-106">Azure 儲存體 NuGet 封裝已加入至 Visual Studio 專案或在其中更新。</span><span class="sxs-lookup"><span data-stu-id="f994f-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="f994f-107">這個封裝會加入下列 .NET 參考：</span><span class="sxs-lookup"><span data-stu-id="f994f-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="f994f-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="f994f-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="f994f-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="f994f-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="f994f-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="f994f-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="f994f-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="f994f-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="f994f-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="f994f-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="f994f-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="f994f-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="f994f-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="f994f-114">**System.Data**</span></span>
* <span data-ttu-id="f994f-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="f994f-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="f994f-116">加入 Azure 儲存體的連接字串</span><span class="sxs-lookup"><span data-stu-id="f994f-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="f994f-117">在專案的 App.config 檔案中，已使用所選儲存體帳戶的連接字串和金鑰更新 **AzureWebJobsStorage** 和 **AzureWebJobsDashboard** 項目。</span><span class="sxs-lookup"><span data-stu-id="f994f-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="f994f-118">如需詳細資訊，請參閱 [Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="f994f-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

