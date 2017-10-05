---
title: "針對應用程式 Proxy 應用程式找不到作用中的連接器群組 | Microsoft Docs"
description: "解決在具有 Azure AD 應用程式 Proxy 之應用程式的連接器群組中沒有作用中的連接器時可能會遇到問題"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4945958deedc8a1d9989ff901192c03a5363b4dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="859fc-103">針對應用程式 Proxy 應用程式找不到作用中的連接器群組</span><span class="sxs-lookup"><span data-stu-id="859fc-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="859fc-104">本文協助您解決針對與 Azure Active Directory 整合的應用程式 Proxy 應用程式無法偵測到連接器時所需面對的常見問題。</span><span class="sxs-lookup"><span data-stu-id="859fc-104">This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="859fc-105">步驟概觀</span><span class="sxs-lookup"><span data-stu-id="859fc-105">Overview of steps</span></span>
<span data-ttu-id="859fc-106">如果您應用程式的連接器群組中沒有作用中的連接器，有幾種方法可以解決此問題：</span><span class="sxs-lookup"><span data-stu-id="859fc-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span></span>

-   <span data-ttu-id="859fc-107">如果群組中沒有連接器，您可以：</span><span class="sxs-lookup"><span data-stu-id="859fc-107">If you have no connectors in the group, you can:</span></span>

    -   <span data-ttu-id="859fc-108">在正確的內部部署伺服器上下載新的連接器，然後將它指派到此群組</span><span class="sxs-lookup"><span data-stu-id="859fc-108">Download a new Connector on the right on-prem server, and assign it to this group</span></span>

    -   <span data-ttu-id="859fc-109">將作用中的連接器移至群組中</span><span class="sxs-lookup"><span data-stu-id="859fc-109">Move an active Connector into the group</span></span>

-   <span data-ttu-id="859fc-110">如果群組中沒有作用中的連接器，您可以：</span><span class="sxs-lookup"><span data-stu-id="859fc-110">If you have no active connectors in the group, you can:</span></span>

    -   <span data-ttu-id="859fc-111">找出連接器無法作用的原因並加以解決</span><span class="sxs-lookup"><span data-stu-id="859fc-111">Identify the reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="859fc-112">將作用中的連接器移至群組中</span><span class="sxs-lookup"><span data-stu-id="859fc-112">Move an active Connector into the group</span></span>

<span data-ttu-id="859fc-113">若要確認是哪一個問題，請在您的應用程式中開啟 [應用程式 Proxy] 功能表，然後查看連接器群組警告訊息。</span><span class="sxs-lookup"><span data-stu-id="859fc-113">To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span></span> <span data-ttu-id="859fc-114">它會指出群組至少需要一個連接器 (您在群組中完全沒有連接器)，或是沒有作用中的連接器 (不過您很可能有非作用中的連接器)。</span><span class="sxs-lookup"><span data-stu-id="859fc-114">It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Azure 入口網站中的連接器群組選項](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="859fc-116">如需每個選項的詳細資料，請參閱下列對應的小節。</span><span class="sxs-lookup"><span data-stu-id="859fc-116">For details on each of these options, see the corresponding section below.</span></span> <span data-ttu-id="859fc-117">這些小節都假設您是從連接器管理頁面開始。</span><span class="sxs-lookup"><span data-stu-id="859fc-117">Each of these assumes that you are starting from the Connector management page.</span></span> <span data-ttu-id="859fc-118">如果您看到上述的錯誤訊息，可以按一下警告訊息來移至此頁面。</span><span class="sxs-lookup"><span data-stu-id="859fc-118">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span></span> <span data-ttu-id="859fc-119">或者，您可以移至 [Azure Active Directory]，依序按一下 [企業應用程式]、[應用程式 Proxy] 來找到它。</span><span class="sxs-lookup"><span data-stu-id="859fc-119">Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Azure 入口網站中的連接器群組管理](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="859fc-121">下載新的連接器</span><span class="sxs-lookup"><span data-stu-id="859fc-121">Download a new Connector</span></span>

<span data-ttu-id="859fc-122">若要下載新的連接器，請使用頁面頂端的 [下載連接器] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="859fc-122">To download a new Connector, use the “Download Connector” button at the top of the page.</span></span>

<span data-ttu-id="859fc-123">請注意，連接器必須安裝在可直接看到後端應用程式的電腦上，而且通常會置於與應用程式相同的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="859fc-123">note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="859fc-124">下載之後，連接器應該會出現在此功能表中。</span><span class="sxs-lookup"><span data-stu-id="859fc-124">After downloading, the Connector should appear in this menu.</span></span> <span data-ttu-id="859fc-125">按一下連接器，然後使用 [連接器群組] 下拉式清單來確定它屬於正確的群組。</span><span class="sxs-lookup"><span data-stu-id="859fc-125">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span> <span data-ttu-id="859fc-126">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="859fc-126">Save the change.</span></span>

   ![從 Azure 入口網站下載連接器](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="859fc-128">移動作用中的連接器</span><span class="sxs-lookup"><span data-stu-id="859fc-128">Move an Active Connector</span></span>

<span data-ttu-id="859fc-129">如果您有應該屬於群組的作用中連接器，而且能直接看到目標後端應用程式，您可以將連接器移入指派的群組。</span><span class="sxs-lookup"><span data-stu-id="859fc-129">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="859fc-130">若要這麼做，請按一下連接器。</span><span class="sxs-lookup"><span data-stu-id="859fc-130">To do so, click the Connector.</span></span> <span data-ttu-id="859fc-131">在 [連接器群組] 欄位中，使用下拉式清單選取正確的群組，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="859fc-131">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="859fc-132">解決非作用中的連接器</span><span class="sxs-lookup"><span data-stu-id="859fc-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="859fc-133">如果在群組中唯一的連接器為非作用中，它們所在的電腦很可能未解除所有必要連接埠的封鎖。</span><span class="sxs-lookup"><span data-stu-id="859fc-133">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span></span>

<span data-ttu-id="859fc-134">請參閱《連接埠疑難排解》文件，以取得調查此問題的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="859fc-134">see the ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="859fc-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="859fc-135">Next steps</span></span>
[<span data-ttu-id="859fc-136">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="859fc-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


