---
title: "在 Azure Active Directory aaaNamed 位置 |Microsoft 文件"
description: "藉由設定名為位置，您可以避免 IP 位址，您的組織所擁有的產生誤判 hello 不可能的旅遊 tooatypical 位置風險事件類型。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="ef863-103">Azure Active Directory 中的具名位置</span><span class="sxs-lookup"><span data-stu-id="ef863-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="ef863-104">以 hello 名為位置的 Azure Active Directory 的功能，您可以在您的組織中標籤受信任的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="ef863-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="ef863-105">在您的環境，您可以使用具名的位置 hello 內容中的 hello 偵測[風險事件](active-directory-reporting-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="ef863-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="ef863-106">hello 功能有助於減少 hello hello 報告誤判數目*不可能的旅遊 tooatypical 位置*風險事件類型。</span><span class="sxs-lookup"><span data-stu-id="ef863-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="ef863-107">組態</span><span class="sxs-lookup"><span data-stu-id="ef863-107">Configuration</span></span>

<span data-ttu-id="ef863-108">tooconfigure 具名的位置：</span><span class="sxs-lookup"><span data-stu-id="ef863-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="ef863-109">登入 toohello [Azure 入口網站](https://portal.azure.com)全域系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="ef863-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="ef863-110">在 [hello] 左窗格中，按一下 [ **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="ef863-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![hello 左窗格中的 hello Azure Active Directory 連結](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="ef863-112">在 [hello **Azure Active Directory**刀鋒視窗中的，在 hello**安全性**區段中，按一下**條件式存取**。</span><span class="sxs-lookup"><span data-stu-id="ef863-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![hello 條件式存取命令](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="ef863-114">在 [hello**條件式存取**刀鋒視窗中的，在 hello**管理**區段中，按一下**名為位置**。</span><span class="sxs-lookup"><span data-stu-id="ef863-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![hello 具名位置命令](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="ef863-116">在 [hello**名為位置**刀鋒視窗中，按一下 [**新位置**。</span><span class="sxs-lookup"><span data-stu-id="ef863-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![hello 新位置的命令](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="ef863-118">在 hello**新增**刀鋒視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="ef863-118">On hello **New** blade, do hello following:</span></span>

    ![hello 新刀鋒視窗](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="ef863-120">a.</span><span class="sxs-lookup"><span data-stu-id="ef863-120">a.</span></span> <span data-ttu-id="ef863-121">在 [hello**名稱**方塊中，輸入您的具名位置的名稱。</span><span class="sxs-lookup"><span data-stu-id="ef863-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="ef863-122">b.</span><span class="sxs-lookup"><span data-stu-id="ef863-122">b.</span></span> <span data-ttu-id="ef863-123">在 [hello **IP 範圍**方塊中，輸入 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="ef863-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="ef863-124">hello IP 範圍必須在 hello toobe*無類別網域間路由*(選擇 CIDR) 格式。</span><span class="sxs-lookup"><span data-stu-id="ef863-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="ef863-125">c.</span><span class="sxs-lookup"><span data-stu-id="ef863-125">c.</span></span> <span data-ttu-id="ef863-126">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ef863-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="ef863-127">您應該知道的事情</span><span class="sxs-lookup"><span data-stu-id="ef863-127">What you should know</span></span>

<span data-ttu-id="ef863-128">**大量更新**： 當您建立或更新具名的位置，大量更新，您可以上傳或下載 CSV 檔案與 hello IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="ef863-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="ef863-129">上傳 hello 檔案 toohello 清單，而非覆寫 hello 清單中加入 hello IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="ef863-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![hello 上傳和下載連結](./media/active-directory-named-locations/09.png)


<span data-ttu-id="ef863-131">**限制**： 您可以定義最多 60 具名的位置，請使用其中一個 IP 範圍指派 tooeach。</span><span class="sxs-lookup"><span data-stu-id="ef863-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="ef863-132">如果您有一個具名的位置設定時，您可以為它定義總 too500 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="ef863-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ef863-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef863-133">Next steps</span></span>

<span data-ttu-id="ef863-134">toolearn 詳細資料的風險事件，請參閱[Azure Active Directory 風險事件](active-directory-reporting-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="ef863-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

