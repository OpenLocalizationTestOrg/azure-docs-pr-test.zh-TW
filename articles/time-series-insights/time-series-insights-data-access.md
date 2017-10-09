---
title: "在 Azure 時間數列 Insights aaaData 存取原則 |Microsoft 文件"
description: "在本教學課程，了解時間序列 Insights 中的 toomanage 資料存取原則"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="f3d45-103">授與使用 Azure 入口網站的資料存取 tooa 時間數列 Insights 環境</span><span class="sxs-lookup"><span data-stu-id="f3d45-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="f3d45-104">Time Series Insights 環境有兩種獨立的存取原則︰</span><span class="sxs-lookup"><span data-stu-id="f3d45-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="f3d45-105">管理存取原則</span><span class="sxs-lookup"><span data-stu-id="f3d45-105">Management access policies</span></span>
* <span data-ttu-id="f3d45-106">資料存取原則</span><span class="sxs-lookup"><span data-stu-id="f3d45-106">Data access policies</span></span>

<span data-ttu-id="f3d45-107">這兩種原則可將特定環境的各種權限授與給 Azure Active Directory 主體 (使用者和應用程式)。</span><span class="sxs-lookup"><span data-stu-id="f3d45-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="f3d45-108">hello 主體 （使用者和應用程式） 必須屬於 toohello active directory （或 「 Azure 租用戶 「） 包含 hello 環境的 hello 訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="f3d45-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="f3d45-109">管理存取權原則授與 hello 環境的權限相關的 toohello 設定例如</span><span class="sxs-lookup"><span data-stu-id="f3d45-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="f3d45-110">建立和刪除 hello 環境中，事件來源的參考資料集和</span><span class="sxs-lookup"><span data-stu-id="f3d45-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="f3d45-111">Hello 資料存取原則的管理。</span><span class="sxs-lookup"><span data-stu-id="f3d45-111">Management of hello data access policies.</span></span>

<span data-ttu-id="f3d45-112">資料存取原則授與權限 tooissue 資料查詢、 處理 hello 環境中的參考資料和共用儲存的查詢和檢視方塊與 hello 環境相關聯。</span><span class="sxs-lookup"><span data-stu-id="f3d45-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="f3d45-113">hello 兩種原則允許存取 toohello hello 環境管理，以及存取 toohello hello 環境內的資料之間有清楚的區隔。</span><span class="sxs-lookup"><span data-stu-id="f3d45-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="f3d45-114">比方說，它是可能 toosetup 環境，使 hello 擁有者/的建立者 hello 環境移除 hello 資料存取。</span><span class="sxs-lookup"><span data-stu-id="f3d45-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="f3d45-115">使用者和服務可從 hello 環境 tooread 資料以及可能會被授與 hello 環境的任何存取 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="f3d45-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="f3d45-116">授與資料存取</span><span class="sxs-lookup"><span data-stu-id="f3d45-116">Grant data access</span></span>
<span data-ttu-id="f3d45-117">hello 下列步驟顯示如何 toogrant 資料存取的使用者主體：</span><span class="sxs-lookup"><span data-stu-id="f3d45-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="f3d45-118">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f3d45-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="f3d45-119">按一下 [所有資源] 功能表中的 hello 左邊 hello hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f3d45-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="f3d45-120">選取 Time Series Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="f3d45-120">Select your Time Series Insights environment.</span></span>

  ![管理 hello 時間數列 Insights 來源-環境](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="f3d45-122">選取 [資料層存取]，按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="f3d45-122">Select “Data Plane Access”, click “Add”</span></span>

  ![管理 hello 時間數列 Insights 來源-新增](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="f3d45-124">按一下 [選取使用者]。</span><span class="sxs-lookup"><span data-stu-id="f3d45-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="f3d45-125">搜尋並選取以 hello 電子郵件的使用者。</span><span class="sxs-lookup"><span data-stu-id="f3d45-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="f3d45-126">在 [選取使用者] 刀鋒視窗中按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="f3d45-126">Click “Select” in “Select User” blade.</span></span>

  ![管理 hello 時間數列 Insights 來源選取的使用者](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="f3d45-128">按一下 [選取角色]。</span><span class="sxs-lookup"><span data-stu-id="f3d45-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="f3d45-129">如果您想 tooallow 使用者 toochange 參考資料，並且與 hello 環境的其他使用者共用已儲存的查詢和檢視方塊，請選取 「 著作人 」。</span><span class="sxs-lookup"><span data-stu-id="f3d45-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="f3d45-130">否則選取 hello 環境中的 「 讀取 」 tooallow 使用者查詢資料並儲存在 hello 環境中的個人 （不共用） 的查詢。</span><span class="sxs-lookup"><span data-stu-id="f3d45-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="f3d45-131">在 hello 「 選取的角色 」 刀鋒視窗中，按一下 確定。</span><span class="sxs-lookup"><span data-stu-id="f3d45-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![管理 hello 時間數列 Insights 來源選取的角色](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="f3d45-133">在 hello 「 選取使用者角色 」 刀鋒視窗中，按一下 確定。</span><span class="sxs-lookup"><span data-stu-id="f3d45-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="f3d45-134">您應該會看到：</span><span class="sxs-lookup"><span data-stu-id="f3d45-134">You should see:</span></span>

  ![管理 hello 時間數列 Insights 來源結果](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="f3d45-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3d45-136">Next steps</span></span>

* [<span data-ttu-id="f3d45-137">建立事件來源</span><span class="sxs-lookup"><span data-stu-id="f3d45-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="f3d45-138">[傳送事件](time-series-insights-send-events.md)toohello 事件來源</span><span class="sxs-lookup"><span data-stu-id="f3d45-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="f3d45-139">在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中檢視您的環境</span><span class="sxs-lookup"><span data-stu-id="f3d45-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
