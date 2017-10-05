---
title: "連接到 Azure Analysis Services 所需的用戶端程式庫 | Microsoft Docs"
description: "說明用戶端應用程式和工具連接到 Azure Analysis Services 所需的用戶端程式庫"
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
ms.openlocfilehash: a96e7fe671dc051da35168fa7b49ecba53b4c4a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a><span data-ttu-id="4ff4d-103">可供連接到 Azure Analysis Services 的用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="4ff4d-103">Client libraries for connecting to Azure Analysis Services</span></span>

<span data-ttu-id="4ff4d-104">用戶端程式庫是用戶端應用程式和工具連接到 Analysis Services 伺服器的必備條件。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span></span> 

<span data-ttu-id="4ff4d-105">Analysis Services 會利用三個用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="4ff4d-106">ADOMD.NET 和「Analysis Services 管理物件」(AMO) 是受管理的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="4ff4d-107">Analysis Services OLE DB 提供者 (MSOLAP DLL) 是原生用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="4ff4d-108">通常會同時安裝這所有三個程式庫。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-108">Typically, all three are installed at the same time.</span></span> <span data-ttu-id="4ff4d-109">Azure Analysis Services 需要的是最新版本。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-109">Azure Analysis Services requires the latest versions.</span></span> 

<span data-ttu-id="4ff4d-110">Microsoft 用戶端應用程式 (例如 Power BI Desktop 和 Excel) 會安裝這所有三個用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="4ff4d-111">不過，用戶端程式庫可能不是 Azure Analysis Services 所需的最新版本，需依更新的版本或頻率而定。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-111">However, depending on the version or frequency of updates, client libraries may not be the latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="4ff4d-112">同樣適用於自訂應用程式或其他介面，例如 AsCmd、TOM、ADOMD.NET。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="4ff4d-113">這些應用程式需要手動安裝程式庫。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-113">These applications require manually installing the libraries.</span></span> <span data-ttu-id="4ff4d-114">手動安裝的用戶端程式庫會以可散發的套件形式包含在 SQL Server 功能套件中。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="4ff4d-115">不過，這些會用戶端程式庫與 SQL Server 版本繫結，而可能不是最新版本。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-115">However, these client libraries are tied to the SQL Server version and may not be the latest.</span></span>  

<span data-ttu-id="4ff4d-116">用於用戶端連線的用戶端程式庫，與從 Azure Analysis Services 伺服器連接到資料來源所需的資料提供者不同。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-116">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span></span> <span data-ttu-id="4ff4d-117">若要深入了解資料來源連接，請參閱[資料來源連接](analysis-services-datasource.md)。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-117">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-the-latest-client-libraries"></a><span data-ttu-id="4ff4d-118">下載最新的用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="4ff4d-118">Download the latest client libraries</span></span>  
<span data-ttu-id="4ff4d-119">如果您處於生產環境並需要完整發行且受支援的版本，請使用下列用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="4ff4d-119">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="4ff4d-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="4ff4d-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="4ff4d-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="4ff4d-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="4ff4d-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="4ff4d-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="4ff4d-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="4ff4d-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="4ff4d-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ff4d-124">Next steps</span></span>
<span data-ttu-id="4ff4d-125">[使用 Excel 進行連接](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="4ff4d-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="4ff4d-126">與 Power BI 連線</span><span class="sxs-lookup"><span data-stu-id="4ff4d-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
