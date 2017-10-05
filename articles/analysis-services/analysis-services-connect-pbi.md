---
title: "使用 Power BI 來連接到 Azure Analysis Services | Microsoft Docs"
description: "了解如何使用 Power BI 來連接到 Azure Analysis Services 伺服器。"
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
ms.openlocfilehash: 3a2af043feddb4a1d6d63f50e838c8a39035449f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="447ce-103">使用 Power BI 進行連接</span><span class="sxs-lookup"><span data-stu-id="447ce-103">Connect with Power BI</span></span>

<span data-ttu-id="447ce-104">您在 Azure 中建立一個伺服器，並將表格式模型部署至該伺服器後，您組織中的使用者便可以連線與開始瀏覽資料。</span><span class="sxs-lookup"><span data-stu-id="447ce-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="447ce-105">請務必使用最新版的 [Power BI Desktop](https://powerbi.microsoft.com/desktop/)。</span><span class="sxs-lookup"><span data-stu-id="447ce-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="447ce-106">在 Power BI Desktop 中連線</span><span class="sxs-lookup"><span data-stu-id="447ce-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="447ce-107">在 Power BI Desktop 中，按一下 [取得資料] > [Azure] > [Azure Analysis Services 資料庫]。</span><span class="sxs-lookup"><span data-stu-id="447ce-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="447ce-108">在 [伺服器] 中，輸入伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="447ce-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="447ce-109">請務必包含完整的 URL。</span><span class="sxs-lookup"><span data-stu-id="447ce-109">Be sure to include the full URL.</span></span> <span data-ttu-id="447ce-110">例如 asazure://westcentralus.asazure.windows.net/advworks。</span><span class="sxs-lookup"><span data-stu-id="447ce-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="447ce-111">在 [資料庫] 中，如果您知道所要連線表格式模型資料庫或檢視方塊的名稱，請在此貼上。</span><span class="sxs-lookup"><span data-stu-id="447ce-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="447ce-112">否則，您可以將此欄位保留空白，然後稍後選取資料庫或檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="447ce-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="447ce-113">保留預設的 [即時連接] 選項，然後按 [連接]。</span><span class="sxs-lookup"><span data-stu-id="447ce-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="447ce-114">如果出現提示，請輸入您的登入認證。</span><span class="sxs-lookup"><span data-stu-id="447ce-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="447ce-115">在 [導覽器] 中展開伺服器，然後選取您要連線的模型或檢視方塊，再按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="447ce-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="447ce-116">按一下某個模型或檢視方塊，即可顯示該檢視的所有物件。</span><span class="sxs-lookup"><span data-stu-id="447ce-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="447ce-117">模型會在 Power BI Desktop 中開啟，其中會在 [報表] 檢視下顯示一個空白報表。</span><span class="sxs-lookup"><span data-stu-id="447ce-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="447ce-118">[欄位] 清單會顯示所有非隱藏的模型物件。</span><span class="sxs-lookup"><span data-stu-id="447ce-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="447ce-119">連線狀態會顯示在右下角。</span><span class="sxs-lookup"><span data-stu-id="447ce-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="447ce-120">在 Power BI Desktop 中連線 (服務)</span><span class="sxs-lookup"><span data-stu-id="447ce-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="447ce-121">建立與您伺服器上模型即時連線的 Power BI Desktop 檔案。</span><span class="sxs-lookup"><span data-stu-id="447ce-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="447ce-122">在 [Power BI](https://powerbi.microsoft.com) 中，按一下 [取得資料]  >  [檔案]。</span><span class="sxs-lookup"><span data-stu-id="447ce-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="447ce-123">找到並選取您的檔案。</span><span class="sxs-lookup"><span data-stu-id="447ce-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="447ce-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="447ce-124">See also</span></span>
<span data-ttu-id="447ce-125">[連接到 Azure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="447ce-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="447ce-126">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="447ce-126">Client libraries</span></span>](analysis-services-data-providers.md)

