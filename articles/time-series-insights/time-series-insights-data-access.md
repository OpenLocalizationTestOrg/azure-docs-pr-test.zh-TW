---
title: "Azure Time Series Insights 中的資料存取原則 | Microsoft Docs"
description: "在本教學課程中，您會了解如何在 Time Series Insights 中管理資料存取原則"
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
ms.openlocfilehash: e975c6d8f217bc73948c0c046204b16b1a742bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="grant-data-access-to-a-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="7ba95-103">使用 Azure 入口網站授與 Time Series Insights 環境的資料存取權</span><span class="sxs-lookup"><span data-stu-id="7ba95-103">Grant data access to a Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="7ba95-104">Time Series Insights 環境有兩種獨立的存取原則︰</span><span class="sxs-lookup"><span data-stu-id="7ba95-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="7ba95-105">管理存取原則</span><span class="sxs-lookup"><span data-stu-id="7ba95-105">Management access policies</span></span>
* <span data-ttu-id="7ba95-106">資料存取原則</span><span class="sxs-lookup"><span data-stu-id="7ba95-106">Data access policies</span></span>

<span data-ttu-id="7ba95-107">這兩種原則可將特定環境的各種權限授與給 Azure Active Directory 主體 (使用者和應用程式)。</span><span class="sxs-lookup"><span data-stu-id="7ba95-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="7ba95-108">主體 (使用者和應用程式) 必須屬於與含有此環境之訂用帳戶相關聯的 Active Directory (或「Azure 租用戶」)。</span><span class="sxs-lookup"><span data-stu-id="7ba95-108">The principals (users and apps) must belong to the active directory (or “Azure tenant”) associated with the subscription containing the environment.</span></span>

<span data-ttu-id="7ba95-109">管理存取原則可授與環境設定相關權限，例如</span><span class="sxs-lookup"><span data-stu-id="7ba95-109">Management access policies grant permissions related to the configuration of the environment, such as</span></span>
*   <span data-ttu-id="7ba95-110">建立和刪除環境、事件來源、參考資料集，以及</span><span class="sxs-lookup"><span data-stu-id="7ba95-110">Creation and deletion of the environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="7ba95-111">管理資料存取原則。</span><span class="sxs-lookup"><span data-stu-id="7ba95-111">Management of the data access policies.</span></span>

<span data-ttu-id="7ba95-112">資料存取原則可授與下列權限：發出資料查詢、在環境中操作參考資料，以及共用與環境相關聯的已儲存查詢和檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="7ba95-112">Data access policies grant permissions to issue data queries, manipulate reference data in the environment, and share saved queries and perspectives associated with the environment.</span></span>

<span data-ttu-id="7ba95-113">這兩種原則能夠清楚區隔環境管理存取權與環境內資料存取權。</span><span class="sxs-lookup"><span data-stu-id="7ba95-113">The two kinds of policies allow clear separation between access to the management of the environment and access to the data inside the environment.</span></span> <span data-ttu-id="7ba95-114">比方說，可以設定環境，以便移除環境擁有者/建立者的資料存取權。</span><span class="sxs-lookup"><span data-stu-id="7ba95-114">For example, it is possible to setup an environment such that the owner/creator of the environment is removed from the data access.</span></span> <span data-ttu-id="7ba95-115">獲准讀取環境中資料的使用者與服務，可能無法存取環境的組態。</span><span class="sxs-lookup"><span data-stu-id="7ba95-115">As well as users and services that are allowed to read data from the environment may be granted no access to the configuration of the environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="7ba95-116">授與資料存取</span><span class="sxs-lookup"><span data-stu-id="7ba95-116">Grant data access</span></span>
<span data-ttu-id="7ba95-117">下列步驟示範如何授與使用者主體的資料存取權︰</span><span class="sxs-lookup"><span data-stu-id="7ba95-117">The following steps show how to grant data access for a user principal:</span></span>

1.  <span data-ttu-id="7ba95-118">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7ba95-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="7ba95-119">按一下 Azure 入口網站左側功能表中的 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="7ba95-119">Click “All resources” in the menu on the left side of the Azure portal.</span></span>
3.  <span data-ttu-id="7ba95-120">選取 Time Series Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="7ba95-120">Select your Time Series Insights environment.</span></span>

  ![管理 Time Series Insights 來源 - 環境](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="7ba95-122">選取 [資料層存取]，按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="7ba95-122">Select “Data Plane Access”, click “Add”</span></span>

  ![管理 Time Series Insights 來源 - 新增](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="7ba95-124">按一下 [選取使用者]。</span><span class="sxs-lookup"><span data-stu-id="7ba95-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="7ba95-125">依照電子郵件搜尋並選取使用者。</span><span class="sxs-lookup"><span data-stu-id="7ba95-125">Search and select user by the email.</span></span>
7.  <span data-ttu-id="7ba95-126">在 [選取使用者] 刀鋒視窗中按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="7ba95-126">Click “Select” in “Select User” blade.</span></span>

  ![管理 Time Series Insights 來源 - 選取使用者](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="7ba95-128">按一下 [選取角色]。</span><span class="sxs-lookup"><span data-stu-id="7ba95-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="7ba95-129">如果您要允許使用者變更參考資料，並與其他環境使用者共用已儲存的查詢和觀點，請選取 [參與者]。</span><span class="sxs-lookup"><span data-stu-id="7ba95-129">Select “Contributor” if you want to allow user to change reference data and share saved queries and perspectives with other users of the environment.</span></span> <span data-ttu-id="7ba95-130">否則選取 [讀取者]，允許使用者查詢環境中的資料並且在環境中儲存個人 (非共用) 查詢。</span><span class="sxs-lookup"><span data-stu-id="7ba95-130">Otherwise select “Reader” to allow user query data in the environment and save personal (not shared) queries in the environment.</span></span>
10. <span data-ttu-id="7ba95-131">在 [選取角色] 刀鋒視窗中按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7ba95-131">Click “Ok” in the “Select Role” blade.</span></span>

  ![管理 Time Series Insights 來源 - 選取角色](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="7ba95-133">在 [選取使用者角色] 刀鋒視窗中按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7ba95-133">Click “Ok” in the “Select User Role” blade.</span></span>
12. <span data-ttu-id="7ba95-134">您應該會看到：</span><span class="sxs-lookup"><span data-stu-id="7ba95-134">You should see:</span></span>

  ![管理 Time Series Insights 來源 - 結果](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="7ba95-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ba95-136">Next steps</span></span>

* [<span data-ttu-id="7ba95-137">建立事件來源</span><span class="sxs-lookup"><span data-stu-id="7ba95-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="7ba95-138">[將事件傳送](time-series-insights-send-events.md)到事件來源</span><span class="sxs-lookup"><span data-stu-id="7ba95-138">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="7ba95-139">在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中檢視您的環境</span><span class="sxs-lookup"><span data-stu-id="7ba95-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
