---
title: "我的 ASP.NET 專案發生什麼情形？ | Microsoft Docs"
description: "說明使用 Visual Studio 已連接服務將 Azure 儲存體新增至 ASP.NET 專案後，會發生什麼事"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: e1fe1b6d-4e3d-476d-8b2f-f7ade050515e
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e2cdc2ff4df85f0224352bd32a3ec62480c3e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-aspnet-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="c00fe-104">我的 ASP.NET 專案 (Visual Studio Azure 儲存體連接的服務) 發生什麼狀況？</span><span class="sxs-lookup"><span data-stu-id="c00fe-104">What happened to my ASP.NET project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="c00fe-105">加入參考</span><span class="sxs-lookup"><span data-stu-id="c00fe-105">References added</span></span>
<span data-ttu-id="c00fe-106">Azure 儲存體 NuGet 封裝已加入至 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="c00fe-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="c00fe-107">這個封裝會加入下列 .NET 參考：</span><span class="sxs-lookup"><span data-stu-id="c00fe-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="c00fe-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="c00fe-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="c00fe-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="c00fe-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="c00fe-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="c00fe-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="c00fe-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="c00fe-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="c00fe-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="c00fe-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="c00fe-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="c00fe-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="c00fe-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="c00fe-114">**System.Data**</span></span>
* <span data-ttu-id="c00fe-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="c00fe-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="c00fe-116">加入 Azure 儲存體的連接字串</span><span class="sxs-lookup"><span data-stu-id="c00fe-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="c00fe-117">在專案的 web.config 檔案中，已使用所選儲存體帳戶的連接字串和金鑰建立一個元素。</span><span class="sxs-lookup"><span data-stu-id="c00fe-117">In the web.config file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="c00fe-118">如需詳細資訊，請參閱 [ASP.NET](http://www.asp.net)。</span><span class="sxs-lookup"><span data-stu-id="c00fe-118">For more information, see [ASP.NET](http://www.asp.net).</span></span>

