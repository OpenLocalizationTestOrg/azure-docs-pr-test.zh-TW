---
title: "應用程式 Proxy 應用程式找到 aaaNo 工作連接器群組 |Microsoft 文件"
description: "在您的應用程式以 hello Azure AD 應用程式 Proxy 連接器群組的連接器沒有工作時，可能會遇到的問題"
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
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="2d555-103">針對應用程式 Proxy 應用程式找不到作用中的連接器群組</span><span class="sxs-lookup"><span data-stu-id="2d555-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="2d555-104">此文章說明您 tooresolve hello 常見的問題不是偵測到應用程式的應用程式 Proxy 連接器時所面對整合與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="2d555-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="2d555-105">步驟概觀</span><span class="sxs-lookup"><span data-stu-id="2d555-105">Overview of steps</span></span>
<span data-ttu-id="2d555-106">如果沒有任何工作在您的應用程式連接器群組的連接器，有幾種方式 tooresolve hello 問題：</span><span class="sxs-lookup"><span data-stu-id="2d555-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="2d555-107">如果您不有任何連接器 hello 群組中，您可以：</span><span class="sxs-lookup"><span data-stu-id="2d555-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="2d555-108">下載新的連接器，在 hello 右由內部部署伺服器上，並將它指派 toothis 群組</span><span class="sxs-lookup"><span data-stu-id="2d555-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="2d555-109">將 active 的連接器移到 hello 群組</span><span class="sxs-lookup"><span data-stu-id="2d555-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="2d555-110">如果您不有任何作用中連接器 hello 群組中，您可以：</span><span class="sxs-lookup"><span data-stu-id="2d555-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="2d555-111">識別您的連接器為非使用中的 hello 原因和解決</span><span class="sxs-lookup"><span data-stu-id="2d555-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="2d555-112">將 active 的連接器移到 hello 群組</span><span class="sxs-lookup"><span data-stu-id="2d555-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="2d555-113">其中是 hello 問題 tooknow 開啟應用程式中的 hello"應用程式 Proxy 」 功能表，並查看 hello 連接器群組的警告訊息。</span><span class="sxs-lookup"><span data-stu-id="2d555-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="2d555-114">它會指定其中一個該 hello 群組必須至少一個連接器 （有無 hello 群組中） 或它有沒有作用中的連接線，（雖然您可能會有非作用中連接器）。</span><span class="sxs-lookup"><span data-stu-id="2d555-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Azure 入口網站中的連接器群組選項](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="2d555-116">如需上述各選項的詳細資訊，請參閱 hello 對應下一節。</span><span class="sxs-lookup"><span data-stu-id="2d555-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="2d555-117">每一種會假設您從 hello 連接器管理 頁面上啟動。</span><span class="sxs-lookup"><span data-stu-id="2d555-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="2d555-118">如果您看到上述的 hello 錯誤訊息，您可以移 toothis 頁面按一下 hello 警告訊息。</span><span class="sxs-lookup"><span data-stu-id="2d555-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="2d555-119">否則找到此太移**Azure Active Directory**、 按一下**企業應用程式**，然後**應用程式 Proxy。**</span><span class="sxs-lookup"><span data-stu-id="2d555-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Azure 入口網站中的連接器群組管理](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="2d555-121">下載新的連接器</span><span class="sxs-lookup"><span data-stu-id="2d555-121">Download a new Connector</span></span>

<span data-ttu-id="2d555-122">toodownload 新連接器，使用 hello 「 下載連接器 」 按鈕，在 hello hello 頁面最上方。</span><span class="sxs-lookup"><span data-stu-id="2d555-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="2d555-123">請注意 hello 連接器需求 toobe 直接視線 toohello 後端應用程式的電腦上安裝，且通常會放在 hello 與 hello 應用程式相同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="2d555-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="2d555-124">下載之後，應該會出現在這個功能表中的 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="2d555-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="2d555-125">按一下 hello 連接器，並使用 hello 「 連接器群組 」 下拉式 toomake 確定其所屬 toohello 正確的群組。</span><span class="sxs-lookup"><span data-stu-id="2d555-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="2d555-126">儲存 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="2d555-126">Save hello change.</span></span>

   ![從 hello Azure 入口網站下載 hello 連接器](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="2d555-128">移動作用中的連接器</span><span class="sxs-lookup"><span data-stu-id="2d555-128">Move an Active Connector</span></span>

<span data-ttu-id="2d555-129">如果您有使用中的連接器應隸屬於 toohello 群組且具有的視野 toohello 目標後端應用程式，您可以將 hello 連接器移到 hello 分派群組中。</span><span class="sxs-lookup"><span data-stu-id="2d555-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="2d555-130">toodo，請按一下 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="2d555-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="2d555-131">在 hello 「 連接器群組 」 欄位中，使用 hello 下拉式 tooselect hello 正確的群組，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="2d555-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="2d555-132">解決非作用中的連接器</span><span class="sxs-lookup"><span data-stu-id="2d555-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="2d555-133">如果 hello 只有連接器 hello 群組中的非使用中，他們可能並不會在機器上有所有 hello 必要的連接埠已解除都封鎖。</span><span class="sxs-lookup"><span data-stu-id="2d555-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="2d555-134">請參閱 hello 連接埠上調查此問題的詳細資料的疑難排解文件。</span><span class="sxs-lookup"><span data-stu-id="2d555-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d555-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d555-135">Next steps</span></span>
[<span data-ttu-id="2d555-136">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="2d555-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


