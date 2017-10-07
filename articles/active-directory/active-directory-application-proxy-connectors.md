---
title: "aaaClassic 入口網站的 Azure AD 應用程式 Proxy 連接器 |Microsoft 文件"
description: "涵蓋如何 toocreate 和管理的 Azure AD 應用程式 Proxy 連接器群組。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="57392-103">使用連接器群組在個別的網路和位置上發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="57392-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57392-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="57392-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="57392-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="57392-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="57392-106">連接器群組可用於多種不同狀況，包括：</span><span class="sxs-lookup"><span data-stu-id="57392-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="57392-107">具有多個互連資料中心的網站。</span><span class="sxs-lookup"><span data-stu-id="57392-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="57392-108">在此情況下，您想讓 tookeep 盡流量 hello 資料中心內儘可能因為跨資料中心的連結是高度耗費資源而變慢。</span><span class="sxs-lookup"><span data-stu-id="57392-108">In this case, you want tookeep as much traffic within hello datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="57392-109">您可以部署中每個資料中心 tooserve 只有 hello 應用程式位於 hello 資料中心內的連接器。</span><span class="sxs-lookup"><span data-stu-id="57392-109">You can deploy connectors in each datacenter tooserve only hello applications that reside within hello datacenter.</span></span> <span data-ttu-id="57392-110">這種方式跨資料中心連結降到最低，並提供完全透明的經驗 tooyour 使用者。</span><span class="sxs-lookup"><span data-stu-id="57392-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience tooyour users.</span></span>
* <span data-ttu-id="57392-111">管理不屬於 hello 主要公司網路的隔離網路上安裝的應用程式。</span><span class="sxs-lookup"><span data-stu-id="57392-111">Managing applications installed on isolated networks that are not part of hello main corporate network.</span></span> <span data-ttu-id="57392-112">您可以使用連接器群組 tooinstall 專用連接器隔離的網路 tooalso 隔離的應用程式 toohello 網路上。</span><span class="sxs-lookup"><span data-stu-id="57392-112">You can use connector groups tooinstall dedicated connectors on isolated networks tooalso isolate applications toohello network.</span></span>
* <span data-ttu-id="57392-113">對於應用程式安裝在 IaaS 雲端存取，連接器群組提供常見服務 toosecure hello 存取 tooall hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57392-113">For applications installed on IaaS for cloud access, connector groups provide a common service toosecure hello access tooall hello apps.</span></span> <span data-ttu-id="57392-114">連接器群組不在您的公司網路上建立其他相依性或片段 hello 應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="57392-114">Connector groups don't create additional dependency on your corporate network, or fragment hello app experience.</span></span> <span data-ttu-id="57392-115">連接器可安裝在每個雲端資料中心，而且只為此網路中的應用程式提供服務。</span><span class="sxs-lookup"><span data-stu-id="57392-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="57392-116">您可以安裝數個連接器 tooachieve 高可用性。</span><span class="sxs-lookup"><span data-stu-id="57392-116">You can install several connectors tooachieve high availability.</span></span>
* <span data-ttu-id="57392-117">多樹系環境中特定連接器部署每個樹系及設定 tooserve 特定應用程式的支援。</span><span class="sxs-lookup"><span data-stu-id="57392-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set tooserve specific applications.</span></span>
* <span data-ttu-id="57392-118">連接器群組可用於災害復原站台 tooeither 偵測容錯移轉，或做為備份的 hello 主要站台。</span><span class="sxs-lookup"><span data-stu-id="57392-118">Connector groups can be used in Disaster Recovery sites tooeither detect failover or as backup for hello main site.</span></span>
* <span data-ttu-id="57392-119">連接器群組也可以是使用的 tooserve 來自單一租用戶的多個公司。</span><span class="sxs-lookup"><span data-stu-id="57392-119">Connector groups can also be used tooserve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="57392-120">必要條件︰建立連接器</span><span class="sxs-lookup"><span data-stu-id="57392-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="57392-121">toogroup 的連接器，[安裝多個連接器](active-directory-application-proxy-enable.md)，然後將其命名並將它們群組。</span><span class="sxs-lookup"><span data-stu-id="57392-121">toogroup your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="57392-122">最後您擁有 tooassign 它們 toospecific 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57392-122">Finally you have tooassign them toospecific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="57392-123">步驟 1：建立連接器群組</span><span class="sxs-lookup"><span data-stu-id="57392-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="57392-124">您可以建立任意數量的連接器群組。</span><span class="sxs-lookup"><span data-stu-id="57392-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="57392-125">連接器群組建立為 hello Azure 傳統入口網站中完成。</span><span class="sxs-lookup"><span data-stu-id="57392-125">Connector group creation is accomplished in hello Azure classic portal.</span></span>

1. <span data-ttu-id="57392-126">選取您的目錄，然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="57392-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="57392-127">![應用程式 Proxy [設定] 螢幕擷取畫面 - 按一下 [管理連接器群組]](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="57392-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="57392-128">在應用程式 Proxy 下按一下**管理連接器群組**並建立連接器群組為 hello 群組指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="57392-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving hello group a name.</span></span>  
    <span data-ttu-id="57392-129">![應用程式 Proxy 連接器群組螢幕擷取畫面 - 為新群組命名](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="57392-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-tooyour-groups"></a><span data-ttu-id="57392-130">步驟 2： 指派連接器 tooyour 群組</span><span class="sxs-lookup"><span data-stu-id="57392-130">Step 2: Assign connectors tooyour groups</span></span>
<span data-ttu-id="57392-131">一旦建立 hello 連接器群組時，移動 hello 連接器 toohello 適當的群組。</span><span class="sxs-lookup"><span data-stu-id="57392-131">Once hello connector groups are created, move hello connectors toohello appropriate group.</span></span>

1. <span data-ttu-id="57392-132">在 [應用程式 Proxy] 底下，按一下 [管理連接器]。</span><span class="sxs-lookup"><span data-stu-id="57392-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="57392-133">在下**群組**，選取您想要針對每個連接器的 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="57392-133">Under **Group**, select hello group you want for each connector.</span></span> <span data-ttu-id="57392-134">可能需要向上 too10 分鐘 toobecome hello 連接器 hello 新群組中的使用中。</span><span class="sxs-lookup"><span data-stu-id="57392-134">It might take hello connectors up too10 minutes toobecome active in hello new group.</span></span>  
    <span data-ttu-id="57392-135">![應用程式 Proxy 連接器螢幕擷取畫面 - 從下拉式功能表中選取群組](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="57392-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-tooyour-connector-groups"></a><span data-ttu-id="57392-136">步驟 3： 將應用程式指派 tooyour 連接器群組</span><span class="sxs-lookup"><span data-stu-id="57392-136">Step 3: Assign applications tooyour connector groups</span></span>
<span data-ttu-id="57392-137">hello 最後一個步驟是 tooset 提供每個應用程式 toohello 連接器群組。</span><span class="sxs-lookup"><span data-stu-id="57392-137">hello last step is tooset each application toohello connector group that serves it.</span></span>

1. <span data-ttu-id="57392-138">在 hello Azure 傳統入口網站，在您目錄中，選取 hello 應用程式，您要讓 tooassign toohello 群組，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="57392-138">In hello Azure classic portal, in your directory, select hello Application you want tooassign toohello group and click **Configure**.</span></span>
2. <span data-ttu-id="57392-139">在下**連接器群組**，選取您想在 hello 應用程式 toouse hello 群組。</span><span class="sxs-lookup"><span data-stu-id="57392-139">Under **Connector group**, select hello group you want hello application toouse.</span></span> <span data-ttu-id="57392-140">這項變更會立即套用。</span><span class="sxs-lookup"><span data-stu-id="57392-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="57392-141">![應用程式 Proxy 連接器群組螢幕擷取畫面 - 從下拉式功能表中選取群組](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="57392-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="57392-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="57392-142">See also</span></span>
* [<span data-ttu-id="57392-143">啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="57392-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="57392-144">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="57392-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="57392-145">啟用條件式存取</span><span class="sxs-lookup"><span data-stu-id="57392-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="57392-146">使用應用程式 Proxy 疑難排解您遇到的問題</span><span class="sxs-lookup"><span data-stu-id="57392-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="57392-147">如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="57392-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
