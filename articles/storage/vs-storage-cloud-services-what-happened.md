---
title: "我的雲端服務專案發生什麼狀況？ | Microsoft Docs"
description: "說明使用 Visual Studio 已連接服務連接至 Azure 儲存體帳戶後，雲端服務專案發生的狀況"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4e0d4864c2fad624fbde39080146dc62ebebff09
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="d7be5-104">我的雲端服務專案發生什麼狀況 (Visual Studio Azure 儲存體已連接服務)？</span><span class="sxs-lookup"><span data-stu-id="d7be5-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="d7be5-105">加入參考</span><span class="sxs-lookup"><span data-stu-id="d7be5-105">References added</span></span>
<span data-ttu-id="d7be5-106">Azure 儲存體 NuGet 封裝已加入至 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="d7be5-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="d7be5-107">這個封裝會加入下列 .NET 參考：</span><span class="sxs-lookup"><span data-stu-id="d7be5-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="d7be5-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="d7be5-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="d7be5-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="d7be5-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="d7be5-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="d7be5-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="d7be5-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="d7be5-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="d7be5-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="d7be5-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="d7be5-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="d7be5-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="d7be5-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="d7be5-114">**System.Data**</span></span>
* <span data-ttu-id="d7be5-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="d7be5-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="d7be5-116">加入 Azure 儲存體的連接字串</span><span class="sxs-lookup"><span data-stu-id="d7be5-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="d7be5-117">已使用所選儲存體帳戶的連接字串和金鑰建立元素。</span><span class="sxs-lookup"><span data-stu-id="d7be5-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="d7be5-118">已修改下列檔案：</span><span class="sxs-lookup"><span data-stu-id="d7be5-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="d7be5-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="d7be5-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="d7be5-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="d7be5-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="d7be5-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="d7be5-121">**ServiceConfiguration.Local.cscfg**</span></span>

