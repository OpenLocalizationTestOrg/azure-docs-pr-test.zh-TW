---
title: "傳統入口網站 Azure AD 應用程式 Proxy 連接器 | Microsoft Docs"
description: "涵蓋如何建立和管理「Azure AD 應用程式 Proxy」中的連接器群組。"
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
ms.openlocfilehash: fc65c4053c45d9c16c62ee0fe65924133a4bb94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="c35e6-103">使用連接器群組在個別的網路和位置上發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="c35e6-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c35e6-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c35e6-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="c35e6-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="c35e6-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="c35e6-106">連接器群組可用於多種不同狀況，包括：</span><span class="sxs-lookup"><span data-stu-id="c35e6-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="c35e6-107">具有多個互連資料中心的網站。</span><span class="sxs-lookup"><span data-stu-id="c35e6-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="c35e6-108">在此情況下，您會希望儘量將流量保留在資料中心內，因為跨資料中心的連結既昂貴、速度又慢。</span><span class="sxs-lookup"><span data-stu-id="c35e6-108">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="c35e6-109">您可以在每個資料中心都部署連接器，來只為資料中心內的應用程式提供服務。</span><span class="sxs-lookup"><span data-stu-id="c35e6-109">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="c35e6-110">這種方法可將跨資料中心的連結減到最少，讓使用者體驗完全的流暢性。</span><span class="sxs-lookup"><span data-stu-id="c35e6-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>
* <span data-ttu-id="c35e6-111">管理安裝在隔離網路 (不是主要的公司網路的一部分) 上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c35e6-111">Managing applications installed on isolated networks that are not part of the main corporate network.</span></span> <span data-ttu-id="c35e6-112">您可以使用連接器群組將專用連接器安裝在隔離網路上，以同時將應用程式與網路隔離。</span><span class="sxs-lookup"><span data-stu-id="c35e6-112">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span>
* <span data-ttu-id="c35e6-113">對於安裝在 IaaS 上以供雲端存取的應用程式，連接器群組提供通用的服務來保護對所有應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="c35e6-113">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="c35e6-114">連接器群組不會對公司網路產生額外的相依性，或是造成不完整的應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="c35e6-114">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="c35e6-115">連接器可安裝在每個雲端資料中心，而且只為此網路中的應用程式提供服務。</span><span class="sxs-lookup"><span data-stu-id="c35e6-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="c35e6-116">您可以安裝數個連接器以獲得高可用性。</span><span class="sxs-lookup"><span data-stu-id="c35e6-116">You can install several connectors to achieve high availability.</span></span>
* <span data-ttu-id="c35e6-117">支援多樹系環境，其中可以依樹系部署特定連接器，並設定為針對特定應用程式提供服務。</span><span class="sxs-lookup"><span data-stu-id="c35e6-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set to serve specific applications.</span></span>
* <span data-ttu-id="c35e6-118">連接器群組可用於災害復原網站，以偵測容錯移轉或做為主要網站的備份。</span><span class="sxs-lookup"><span data-stu-id="c35e6-118">Connector groups can be used in Disaster Recovery sites to either detect failover or as backup for the main site.</span></span>
* <span data-ttu-id="c35e6-119">連接器群組也可用來為單一租用戶的多家公司提供服務。</span><span class="sxs-lookup"><span data-stu-id="c35e6-119">Connector groups can also be used to serve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="c35e6-120">必要條件︰建立連接器</span><span class="sxs-lookup"><span data-stu-id="c35e6-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="c35e6-121">若要將連接器設為群組，請[安裝多個連接器](active-directory-application-proxy-enable.md)，然後命名並組合它們。</span><span class="sxs-lookup"><span data-stu-id="c35e6-121">To group your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="c35e6-122">最後，您必須將它們指派給特定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c35e6-122">Finally you have to assign them to specific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="c35e6-123">步驟 1：建立連接器群組</span><span class="sxs-lookup"><span data-stu-id="c35e6-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="c35e6-124">您可以建立任意數量的連接器群組。</span><span class="sxs-lookup"><span data-stu-id="c35e6-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="c35e6-125">連接器群組的建立是在 Azure 傳統入口網站中完成。</span><span class="sxs-lookup"><span data-stu-id="c35e6-125">Connector group creation is accomplished in the Azure classic portal.</span></span>

1. <span data-ttu-id="c35e6-126">選取您的目錄，然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="c35e6-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="c35e6-127">![應用程式 Proxy [設定] 螢幕擷取畫面 - 按一下 [管理連接器群組]](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="c35e6-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="c35e6-128">在 [應用程式 Proxy] 底下，按一下 [管理連接器群組]，然後提供一個群組名稱來建立連接器群組。</span><span class="sxs-lookup"><span data-stu-id="c35e6-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving the group a name.</span></span>  
    <span data-ttu-id="c35e6-129">![應用程式 Proxy 連接器群組螢幕擷取畫面 - 為新群組命名](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="c35e6-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-to-your-groups"></a><span data-ttu-id="c35e6-130">步驟 2：將連接器指派給您的群組</span><span class="sxs-lookup"><span data-stu-id="c35e6-130">Step 2: Assign connectors to your groups</span></span>
<span data-ttu-id="c35e6-131">建立連接器群組之後，請將連接器移到適當的群組。</span><span class="sxs-lookup"><span data-stu-id="c35e6-131">Once the connector groups are created, move the connectors to the appropriate group.</span></span>

1. <span data-ttu-id="c35e6-132">在 [應用程式 Proxy] 底下，按一下 [管理連接器]。</span><span class="sxs-lookup"><span data-stu-id="c35e6-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="c35e6-133">在 [群組] 底下，選取要用於每個連接器的群組。</span><span class="sxs-lookup"><span data-stu-id="c35e6-133">Under **Group**, select the group you want for each connector.</span></span> <span data-ttu-id="c35e6-134">連接器可能最多需要 10 分鐘才會在新群組中變成作用中。</span><span class="sxs-lookup"><span data-stu-id="c35e6-134">It might take the connectors up to 10 minutes to become active in the new group.</span></span>  
    <span data-ttu-id="c35e6-135">![應用程式 Proxy 連接器螢幕擷取畫面 - 從下拉式功能表中選取群組](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="c35e6-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-to-your-connector-groups"></a><span data-ttu-id="c35e6-136">步驟 3：將應用程式指派給您的連接器群組</span><span class="sxs-lookup"><span data-stu-id="c35e6-136">Step 3: Assign applications to your connector groups</span></span>
<span data-ttu-id="c35e6-137">最後一個步驟是將每個應用程式設定給適合的連接器群組。</span><span class="sxs-lookup"><span data-stu-id="c35e6-137">The last step is to set each application to the connector group that serves it.</span></span>

1. <span data-ttu-id="c35e6-138">在 Azure 傳統入口網站中，於您的目錄中選取要指派給群組的應用程式，然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="c35e6-138">In the Azure classic portal, in your directory, select the Application you want to assign to the group and click **Configure**.</span></span>
2. <span data-ttu-id="c35e6-139">在 [連接器群組] 底下，選取應用程式要使用的群組。</span><span class="sxs-lookup"><span data-stu-id="c35e6-139">Under **Connector group**, select the group you want the application to use.</span></span> <span data-ttu-id="c35e6-140">這項變更會立即套用。</span><span class="sxs-lookup"><span data-stu-id="c35e6-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="c35e6-141">![應用程式 Proxy 連接器群組螢幕擷取畫面 - 從下拉式功能表中選取群組](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="c35e6-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="c35e6-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c35e6-142">See also</span></span>
* [<span data-ttu-id="c35e6-143">啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="c35e6-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="c35e6-144">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="c35e6-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="c35e6-145">啟用條件式存取</span><span class="sxs-lookup"><span data-stu-id="c35e6-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="c35e6-146">使用應用程式 Proxy 疑難排解您遇到的問題</span><span class="sxs-lookup"><span data-stu-id="c35e6-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="c35e6-147">如需最新消息，請查閱 [應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="c35e6-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
