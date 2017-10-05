---
title: "我的 ASP.NET 5 專案 (Visual Studio Azure 儲存體連接的服務) 發生什麼狀況 | Microsoft Docs"
description: "說明使用 Visual Studio 已連接服務連接到 Visual Studio ASP.NET 5 專案中的 Azure 儲存體帳戶後，會發生什麼事"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4390993772eaf35516e48ad7adcdcec5f1df8d71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="bf961-103">我的 ASP.NET 5 專案 (Visual Studio Azure 儲存體連接的服務) 發生什麼狀況？</span><span class="sxs-lookup"><span data-stu-id="bf961-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="bf961-104">加入參考</span><span class="sxs-lookup"><span data-stu-id="bf961-104">References added</span></span>
<span data-ttu-id="bf961-105">Azure 儲存體 NuGet 封裝已加入至 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="bf961-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="bf961-106">這個封裝會加入下列 .NET 參考：</span><span class="sxs-lookup"><span data-stu-id="bf961-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="bf961-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="bf961-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="bf961-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="bf961-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="bf961-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="bf961-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="bf961-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="bf961-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="bf961-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="bf961-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="bf961-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="bf961-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="bf961-113">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="bf961-113">**System.Data**</span></span>
* <span data-ttu-id="bf961-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="bf961-114">**System.Spatial**</span></span>

<span data-ttu-id="bf961-115">另外也加入了 NuGet 封裝 **Microsoft.Framework.Configuration.Json** 。</span><span class="sxs-lookup"><span data-stu-id="bf961-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="bf961-116">加入 Azure 儲存體的連接字串</span><span class="sxs-lookup"><span data-stu-id="bf961-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="bf961-117">在專案的 config.json 檔案中，已使用所選儲存體帳戶的連接字串和金鑰建立一個元素。</span><span class="sxs-lookup"><span data-stu-id="bf961-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="bf961-118">如需詳細資訊，請參閱 [ASP.NET 5](http://www.asp.net/vnext)。</span><span class="sxs-lookup"><span data-stu-id="bf961-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>
