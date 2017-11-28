---
title: "連接 tooAzure Analysis Services 所需的 aaaClient 程式庫 |Microsoft 文件"
description: "描述所需的用戶端應用程式和工具 tooconnect Azure Analysis Services 的用戶端程式庫"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="5c42f-103">連接 tooAzure Analysis Services 的用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="5c42f-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="5c42f-104">用戶端程式庫所需的用戶端應用程式和工具 tooconnect tooAnalysis 服務伺服器。</span><span class="sxs-lookup"><span data-stu-id="5c42f-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="5c42f-105">Analysis Services 會利用三個用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="5c42f-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="5c42f-106">ADOMD.NET 和「Analysis Services 管理物件」(AMO) 是受管理的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="5c42f-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="5c42f-107">hello Analysis Services OLE DB 提供者 (MSOLAP DLL) 是原生用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="5c42f-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="5c42f-108">一般來說，這三個可安裝在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="5c42f-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="5c42f-109">Azure Analysis Services 需要 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="5c42f-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="5c42f-110">Microsoft 用戶端應用程式 (例如 Power BI Desktop 和 Excel) 會安裝這所有三個用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="5c42f-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="5c42f-111">不過，根據 hello 版本或更新的頻率，用戶端程式庫可能無法 hello Azure Analysis Services 所需的最新版本。</span><span class="sxs-lookup"><span data-stu-id="5c42f-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="5c42f-112">hello 一樣 toocustom 應用程式或其他介面，例如 AsCmd，TOM，ADOMD.NET。</span><span class="sxs-lookup"><span data-stu-id="5c42f-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="5c42f-113">這些應用程式需要以手動方式安裝 hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="5c42f-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="5c42f-114">hello 進行手動安裝的用戶端程式庫隨附的 SQL Server 功能套件散發的封裝。</span><span class="sxs-lookup"><span data-stu-id="5c42f-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="5c42f-115">不過，這些用戶端程式庫會繫結的 toohello SQL Server 版本，可能無法 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="5c42f-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="5c42f-116">用戶端連線的用戶端程式庫會與不同的資料提供者需要 tooconnect 從 Azure Analysis Services 伺服器 tooa 資料來源。</span><span class="sxs-lookup"><span data-stu-id="5c42f-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="5c42f-117">toolearn 進一步了解資料來源連接，請參閱[資料來源連接](analysis-services-datasource.md)。</span><span class="sxs-lookup"><span data-stu-id="5c42f-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="5c42f-118">下載最新用戶端程式庫 hello</span><span class="sxs-lookup"><span data-stu-id="5c42f-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="5c42f-119">使用下列用戶端程式庫，如果您是在生產環境中，而且需要完整發行和支援版本的 hello。</span><span class="sxs-lookup"><span data-stu-id="5c42f-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="5c42f-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="5c42f-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="5c42f-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="5c42f-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="5c42f-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="5c42f-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="5c42f-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="5c42f-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="5c42f-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c42f-124">Next steps</span></span>
<span data-ttu-id="5c42f-125">[使用 Excel 進行連接](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="5c42f-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="5c42f-126">與 Power BI 連線</span><span class="sxs-lookup"><span data-stu-id="5c42f-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
