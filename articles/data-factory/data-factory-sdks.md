---
title: "aaaAzure Data Factory 開發人員參考"
description: "深入了解不同的方式 toocreate 監視和管理 Azure data factory"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: dc752fa1-a6c3-4753-904e-9f32d0a940b7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2017
ms.author: spelluru
redirect_url: https://azure.microsoft.com/services/data-factory/
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 5384f2209ff0f788527542ddd400c1d163d587c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-developer-reference"></a><span data-ttu-id="db561-103">Azure Data Factory 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="db561-103">Azure Data Factory Developer Reference</span></span>
<span data-ttu-id="db561-104">您可以建立、 監視和管理使用 Azure 入口網站、 Azure PowerShell、.NET 類別庫或 REST API 的 hello 處理站。</span><span class="sxs-lookup"><span data-stu-id="db561-104">You can create, monitor, and manage hello factories using either Azure portal, Azure PowerShell, .NET Class Library, or REST API.</span></span>

| <span data-ttu-id="db561-105">方法</span><span class="sxs-lookup"><span data-stu-id="db561-105">Method</span></span> | <span data-ttu-id="db561-106">資源位置</span><span class="sxs-lookup"><span data-stu-id="db561-106">Resource Location</span></span> | <span data-ttu-id="db561-107">開發人員參考</span><span class="sxs-lookup"><span data-stu-id="db561-107">Developer References</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db561-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="db561-108">Azure portal</span></span> |[<span data-ttu-id="db561-109">https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="db561-109">https://portal.azure.com/</span></span>](https://portal.azure.com) |[<span data-ttu-id="db561-110">開始使用 Azure Data Factory (Azure 入口網站)</span><span class="sxs-lookup"><span data-stu-id="db561-110">Get started with Azure Data Factory (Azure portal)</span></span>](data-factory-build-your-first-pipeline-using-editor.md) |
| <span data-ttu-id="db561-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="db561-111">Azure PowerShell</span></span> |<span data-ttu-id="db561-112">下載最新的 hello [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="db561-112">Download hello latest [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span></span> |[<span data-ttu-id="db561-113">Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="db561-113">Cmdlet reference</span></span>](https://msdn.microsoft.com/library/dn820234.aspx) |
| <span data-ttu-id="db561-114">.NET 類別庫</span><span class="sxs-lookup"><span data-stu-id="db561-114">.NET Class Library</span></span> |<span data-ttu-id="db561-115">hello Azure Data Factory.NET SDK 可讓您 toocreate 監視和管理 Azure data factory 和擴充使用.NET 活動的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="db561-115">hello Azure Data Factory .NET SDK enables you toocreate, monitor, and manage Azure data factories and extend Data Factory using a .NET activity.</span></span> <span data-ttu-id="db561-116">請參閱[Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md)和[建立、 監視和管理 Azure data factory 使用 Data Factory.NET SDK](data-factory-create-data-factories-programmatically.md)文章 toohelp 您立即開始。</span><span class="sxs-lookup"><span data-stu-id="db561-116">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) and [Create, monitor, and manage Azure data factories using Data Factory .NET SDK](data-factory-create-data-factories-programmatically.md) articles toohelp you get started.</span></span><br/><br/><span data-ttu-id="db561-117"><b>下載 hello 最新的 Nuget</b></span><span class="sxs-lookup"><span data-stu-id="db561-117"><b>Downloading hello latest Nuget</b></span></span><br/><span data-ttu-id="db561-118">您可以下載從 hello 最新 Azure Data Factory 管理程式庫 Nuget 封裝： [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span><span class="sxs-lookup"><span data-stu-id="db561-118">You can download hello latest Azure Data Factory Management Library Nuget package from: [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span></span><br/><br/><span data-ttu-id="db561-119">**在 Visual Studio 中使用封裝管理員主控台**</span><span class="sxs-lookup"><span data-stu-id="db561-119">**Using Package Manager Console in Visual Studio**</span></span><br/><span data-ttu-id="db561-120">您可以執行 hello 下列命令，在 Visual Studio Package Manager Console tooget hello 最新 Azure 資料 Factory 管理程式庫</span><span class="sxs-lookup"><span data-stu-id="db561-120">You can run hello following command in Visual Studio’s Package Manager Console tooget hello latest Azure Data Factory Management Library</span></span><br/><br/><span data-ttu-id="db561-121">Install-Package Microsoft.Azure.Management.DataFactories</span><span class="sxs-lookup"><span data-stu-id="db561-121">Install-Package Microsoft.Azure.Management.DataFactories</span></span> |[<span data-ttu-id="db561-122">.NET SDK 參考</span><span class="sxs-lookup"><span data-stu-id="db561-122">.NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt415893.aspx) |
| <span data-ttu-id="db561-123">REST API</span><span class="sxs-lookup"><span data-stu-id="db561-123">REST API</span></span> |<span data-ttu-id="db561-124">您可以使用 hello Data Factory REST API toocreate、 監視和管理 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="db561-124">You can use hello Data Factory REST API toocreate, monitor, and manage Azure data factories.</span></span> |[<span data-ttu-id="db561-125">REST API 參考</span><span class="sxs-lookup"><span data-stu-id="db561-125">REST API Reference</span></span>](https://msdn.microsoft.com/library/dn906738.aspx) |

