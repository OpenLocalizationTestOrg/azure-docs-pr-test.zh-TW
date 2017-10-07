---
title: "aaaPublishing 不同網路與使用 Azure AD 應用程式 Proxy 連接器群組的位置上的應用程式 |Microsoft 文件"
description: "涵蓋如何 toocreate 和管理的 Azure AD 應用程式 Proxy 連接器群組。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="bb597-103">使用連接器群組在個別的網路和位置上發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="bb597-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb597-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bb597-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="bb597-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="bb597-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>

<span data-ttu-id="bb597-106">客戶在越來越多的案例和應用程式中利用 Azure AD 的應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="bb597-106">Customers utilize Azure AD's Application Proxy for more and more scenarios and applications.</span></span> <span data-ttu-id="bb597-107">因此我們啟用更多的拓撲使應用程式 Proxy 更具彈性。</span><span class="sxs-lookup"><span data-stu-id="bb597-107">So we've made App Proxy even more flexible by enabling more topologies.</span></span> <span data-ttu-id="bb597-108">如此您可以指定特定連接器 tooserve 特定應用程式，您可以建立應用程式 Proxy 連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-108">You can create Application Proxy connector groups so that you can assign specific connectors tooserve specific applications.</span></span> <span data-ttu-id="bb597-109">這項功能可讓您更多的控制和方式 toooptimize 您應用程式 Proxy 的部署。</span><span class="sxs-lookup"><span data-stu-id="bb597-109">This capability gives you more control and ways toooptimize your Application Proxy deployment.</span></span> 

<span data-ttu-id="bb597-110">每個應用程式 Proxy 連接器會被指派 tooa 連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-110">Each Application Proxy connector is assigned tooa connector group.</span></span> <span data-ttu-id="bb597-111">所有 hello 屬於相同的連接器群組做為高可用性和負載平衡的個別單位 toohello 的連接器。</span><span class="sxs-lookup"><span data-stu-id="bb597-111">All hello connectors that belong toohello same connector group act as a separate unit for high-availability and load balancing.</span></span> <span data-ttu-id="bb597-112">所有的連接器隸屬 tooa 連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-112">All connectors belong tooa connector group.</span></span> <span data-ttu-id="bb597-113">如果您未建立群組，則所有的連接器皆會在預設群組中。</span><span class="sxs-lookup"><span data-stu-id="bb597-113">If you don't create groups, then all your connectors are in a default group.</span></span> <span data-ttu-id="bb597-114">您的系統管理員可以建立新的群組，並指派連接器 toothem hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="bb597-114">Your admin can create new groups and assign connectors toothem in hello Azure portal.</span></span> 

<span data-ttu-id="bb597-115">所有應用程式會指派 tooa 連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-115">All applications are assigned tooa connector group.</span></span> <span data-ttu-id="bb597-116">如果您不要建立群組，所有的應用程式會指派 tooa 預設群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-116">If you don't create groups, then all your applications are assigned tooa default group.</span></span> <span data-ttu-id="bb597-117">但是，如果您組織成群組的連接器，您可以設定每個應用程式 toowork 與特定連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-117">But if you organize your connectors into groups, you can set each application toowork with a specific connector group.</span></span> <span data-ttu-id="bb597-118">在此情況下，只有該群組中的 hello 連接器服務收到要求時的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb597-118">In this case, only hello connectors in that group serve hello application upon request.</span></span> <span data-ttu-id="bb597-119">如果您的應用程式裝載在不同的位置中，這是個很有用的功能。</span><span class="sxs-lookup"><span data-stu-id="bb597-119">This feature is useful if your applications are hosted in different locations.</span></span> <span data-ttu-id="bb597-120">您可以建立連接器群組的位置，以便應用程式一律會由實際關閉 toothem 的接點。</span><span class="sxs-lookup"><span data-stu-id="bb597-120">You can create connector groups based on location, so that applications are always served by connectors that are physically close toothem.</span></span>

>[!TIP] 
><span data-ttu-id="bb597-121">如果您有大規模的應用程式 Proxy 部署，則不會指派任何應用程式 toohello 預設連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-121">If you have a large Application Proxy deployment, don't assign any applications toohello default connector group.</span></span> <span data-ttu-id="bb597-122">這樣一來，新的連接器沒有收到任何即時流量之前指派 tooan active 連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-122">That way, new connectors don't receive any live traffic until you assign them tooan active connector group.</span></span> <span data-ttu-id="bb597-123">這項設定也可讓您 tooput 連接器處於閒置模式將其移動後 toohello 預設群組，以便您可以執行維護，而不會影響您的使用者。</span><span class="sxs-lookup"><span data-stu-id="bb597-123">This configuration also enables you tooput connectors in an idle mode by moving them back toohello default group, so that you can perform maintenance without impacting your users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb597-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="bb597-124">Prerequisites</span></span>
<span data-ttu-id="bb597-125">toogroup 的連接器，您必須確定 toomake 您[安裝多個連接器](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="bb597-125">toogroup your connectors, you have toomake sure you [installed multiple connectors](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="bb597-126">當您安裝新的連接器時，它也會自動加入 hello**預設**連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-126">When you install a new connector, it automatically joins hello **Default** connector group.</span></span>

## <a name="create-connector-groups"></a><span data-ttu-id="bb597-127">建立連接器群組</span><span class="sxs-lookup"><span data-stu-id="bb597-127">Create connector groups</span></span>
<span data-ttu-id="bb597-128">使用這些步驟 toocreate 您想要的多個連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-128">Use these steps toocreate as many connector groups as you want.</span></span> 

1. <span data-ttu-id="bb597-129">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="bb597-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="bb597-130">選取 [Azure Active Directory]  >  [企業應用程式]  >  [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="bb597-130">Select **Azure Active Directory** > **Enterprise applications** > **Application proxy**.</span></span>
2. <span data-ttu-id="bb597-131">選取 [新增連接器群組]。</span><span class="sxs-lookup"><span data-stu-id="bb597-131">Select **New connector group**.</span></span> <span data-ttu-id="bb597-132">hello 新連接器群組刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="bb597-132">hello New Connector Group blade appears.</span></span>

   ![選取新的連接器群組](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. <span data-ttu-id="bb597-134">指定新的連接器群組的名稱，然後使用 hello 下拉功能表 tooselect 連接器屬於此群組中。</span><span class="sxs-lookup"><span data-stu-id="bb597-134">Give your new connector group a name, then use hello dropdown menu tooselect which connectors belong in this group.</span></span>
4. <span data-ttu-id="bb597-135">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="bb597-135">Select **Save**.</span></span>

## <a name="assign-applications-tooyour-connector-groups"></a><span data-ttu-id="bb597-136">指派應用程式 tooyour 連接器群組</span><span class="sxs-lookup"><span data-stu-id="bb597-136">Assign applications tooyour connector groups</span></span>
<span data-ttu-id="bb597-137">已透過應用程式 Proxy 發佈的每個應用程式均按照這些步驟處理。</span><span class="sxs-lookup"><span data-stu-id="bb597-137">Use these steps for each application that you've published with Application Proxy.</span></span> <span data-ttu-id="bb597-138">當您第一次發行，或在需要時，您可以使用這些步驟 toochange hello 分派，您可以指派應用程式 tooa 連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-138">You can assign an application tooa connector group when you first publish it, or you can use these steps toochange hello assignment whenever you want.</span></span>   

1. <span data-ttu-id="bb597-139">從 hello 管理儀表板為您的目錄，選取**企業應用程式** > **所有應用程式**> hello 想 tooassign tooa 連接器群組的應用程式 > **應用程式 Proxy**。</span><span class="sxs-lookup"><span data-stu-id="bb597-139">From hello management dashboard for your directory, select **Enterprise applications** > **All applications** > hello application you want tooassign tooa connector group > **Application Proxy**.</span></span>
2. <span data-ttu-id="bb597-140">使用 hello**連接器群組**想 hello toouse 應用程式的下拉式清單中功能表 tooselect hello 群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-140">Use hello **Connector Group** dropdown menu tooselect hello group you want hello application toouse.</span></span>
3. <span data-ttu-id="bb597-141">選取**儲存**tooapply hello 變更。</span><span class="sxs-lookup"><span data-stu-id="bb597-141">Select **Save** tooapply hello change.</span></span>

## <a name="use-cases-for-connector-groups"></a><span data-ttu-id="bb597-142">連接器群組的使用案例</span><span class="sxs-lookup"><span data-stu-id="bb597-142">Use cases for connector groups</span></span> 

<span data-ttu-id="bb597-143">連接器群組可用於多種不同狀況，包括：</span><span class="sxs-lookup"><span data-stu-id="bb597-143">Connector groups are useful for various scenarios, including:</span></span>

### <a name="sites-with-multiple-interconnected-datacenters"></a><span data-ttu-id="bb597-144">具有多個互連資料中心的網站</span><span class="sxs-lookup"><span data-stu-id="bb597-144">Sites with multiple interconnected datacenters</span></span>

<span data-ttu-id="bb597-145">許多組織都有數個彼此連接的資料中心。</span><span class="sxs-lookup"><span data-stu-id="bb597-145">Many organizations have a number of interconnected datacenters.</span></span> <span data-ttu-id="bb597-146">在此情況下，您想讓 tookeep 盡流量 hello 資料中心內儘可能因為跨資料中心的連結是高度耗費資源而變慢。</span><span class="sxs-lookup"><span data-stu-id="bb597-146">In this case, you want tookeep as much traffic within hello datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="bb597-147">您可以部署中每個資料中心 tooserve 只有 hello 應用程式位於 hello 資料中心內的連接器。</span><span class="sxs-lookup"><span data-stu-id="bb597-147">You can deploy connectors in each datacenter tooserve only hello applications that reside within hello datacenter.</span></span> <span data-ttu-id="bb597-148">這種方式跨資料中心連結降到最低，並提供完全透明的經驗 tooyour 使用者。</span><span class="sxs-lookup"><span data-stu-id="bb597-148">This approach minimizes cross-datacenter links and provides an entirely transparent experience tooyour users.</span></span>

### <a name="applications-installed-on-isolated-networks"></a><span data-ttu-id="bb597-149">安裝在隔離網路上的應用程式</span><span class="sxs-lookup"><span data-stu-id="bb597-149">Applications installed on isolated networks</span></span>

<span data-ttu-id="bb597-150">應用程式可以裝載於不屬於 hello 主要公司網路的網路。</span><span class="sxs-lookup"><span data-stu-id="bb597-150">Applications can be hosted in networks that are not part of hello main corporate network.</span></span> <span data-ttu-id="bb597-151">您可以使用連接器群組 tooinstall 專用連接器隔離的網路 tooalso 隔離的應用程式 toohello 網路上。</span><span class="sxs-lookup"><span data-stu-id="bb597-151">You can use connector groups tooinstall dedicated connectors on isolated networks tooalso isolate applications toohello network.</span></span> <span data-ttu-id="bb597-152">當協力廠商為您的組織維護特定應用程式時，就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="bb597-152">This usually happens when a third-party vendor maintains a specific application for your organization.</span></span> 

<span data-ttu-id="bb597-153">連接器群組可讓您 tooinstall 專用的網路發佈只有特定應用程式，以更輕鬆的連接器和更安全的 toooutsource 應用程式管理 toothird 廠商所提供。</span><span class="sxs-lookup"><span data-stu-id="bb597-153">Connector groups allow you tooinstall dedicated connectors for those networks that publish only specific applications, making it easier and more secure toooutsource application management toothird-party vendors.</span></span>

### <a name="applications-installed-on-iaas"></a><span data-ttu-id="bb597-154">IaaS 上已安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="bb597-154">Applications installed on IaaS</span></span> 

<span data-ttu-id="bb597-155">對於應用程式安裝在 IaaS 雲端存取，連接器群組提供常見服務 toosecure hello 存取 tooall hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb597-155">For applications installed on IaaS for cloud access, connector groups provide a common service toosecure hello access tooall hello apps.</span></span> <span data-ttu-id="bb597-156">連接器群組不在您的公司網路上建立其他相依性或片段 hello 應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="bb597-156">Connector groups don't create additional dependency on your corporate network, or fragment hello app experience.</span></span> <span data-ttu-id="bb597-157">連接器可安裝在每個雲端資料中心，而且只為該網路中的應用程式提供服務。</span><span class="sxs-lookup"><span data-stu-id="bb597-157">Connectors can be installed on every cloud datacenter and serve only applications that reside in that network.</span></span> <span data-ttu-id="bb597-158">您可以安裝數個連接器 tooachieve 高可用性。</span><span class="sxs-lookup"><span data-stu-id="bb597-158">You can install several connectors tooachieve high availability.</span></span>

<span data-ttu-id="bb597-159">取得做為範例的組織有數個虛擬機器連線 tootheir 自己主控的 IaaS 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bb597-159">Take as an example an organization that has several virtual machines connected tootheir own IaaS hosted virtual network.</span></span> <span data-ttu-id="bb597-160">tooallow 員工 toouse 這些應用程式，這些私人網路會使用站對站 VPN 連線的 toohello 公司網路。</span><span class="sxs-lookup"><span data-stu-id="bb597-160">tooallow employees toouse these applications, these private networks are connected toohello corporate network using site-to-site VPN.</span></span> <span data-ttu-id="bb597-161">針對位於內部部署的員工，這會提供良好的體驗。</span><span class="sxs-lookup"><span data-stu-id="bb597-161">This provides a good experience for employees that are located on-premises.</span></span> <span data-ttu-id="bb597-162">但是，它可能不適合用來遠端員工，因為它需要額外的內部部署基礎結構 tooroute 存取，您可以看到在 hello 圖中：</span><span class="sxs-lookup"><span data-stu-id="bb597-162">But, it may not be ideal for remote employees, because it requires additional on-premises infrastructure tooroute access, as you can see in hello diagram below:</span></span>

![AzureAD Iaas 網路](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
<span data-ttu-id="bb597-164">與 Azure AD 應用程式 Proxy 連接器群組，您可以啟用一般服務 toosecure hello 存取 tooall 應用程式，而不需要在您的公司網路上建立其他相依性：</span><span class="sxs-lookup"><span data-stu-id="bb597-164">With Azure AD Application Proxy connector groups, you can enable a common service toosecure hello access tooall applications without creating additional dependency on your corporate network:</span></span>

![AzureAD Iaas 多雲端廠商](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a><span data-ttu-id="bb597-166">多樹系 – 每個樹系不同的連接器群組</span><span class="sxs-lookup"><span data-stu-id="bb597-166">Multi-forest – different connector groups for each forest</span></span>

<span data-ttu-id="bb597-167">大部分已部署應用程式 Proxy 的客戶會執行 Kerberos 限制委派 (KCD) 來使用單一登入 (SSO) 功能。</span><span class="sxs-lookup"><span data-stu-id="bb597-167">Most customers who have deployed Application Proxy are using its single-sign-on (SSO) capabilities by performing Kerberos Constrained Delegation (KCD).</span></span> <span data-ttu-id="bb597-168">tooachieve 這 hello 連接器的電腦需要 toobe 聯結的 tooa 網域，可以委派 hello 朝 hello 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="bb597-168">tooachieve this, hello connector’s machines need toobe joined tooa domain that can delegate hello users toward hello application.</span></span> <span data-ttu-id="bb597-169">KCD 支援跨樹系功能。</span><span class="sxs-lookup"><span data-stu-id="bb597-169">KCD supports cross-forest capabilities.</span></span> <span data-ttu-id="bb597-170">但對於擁有不同的多樹系環境且它們之間沒有信任的公司來說，單一連接器無法用於所有的樹系。</span><span class="sxs-lookup"><span data-stu-id="bb597-170">But for companies who have distinct multi-forest environments with no trust between them, a single connector cannot be used for all forests.</span></span> 

<span data-ttu-id="bb597-171">在此情況下，每個樹系，可部署特定連接器，且已發行的 tooserve 組 tooserve 應用程式只 hello 該特定樹系的使用者。</span><span class="sxs-lookup"><span data-stu-id="bb597-171">In this case, specific connectors can be deployed per forest, and set tooserve applications that were published tooserve only hello users of that specific forest.</span></span> <span data-ttu-id="bb597-172">每個連接器群組代表不同的樹系。</span><span class="sxs-lookup"><span data-stu-id="bb597-172">Each connector group represents a different forest.</span></span> <span data-ttu-id="bb597-173">雖然 hello 租用戶和大部分的 hello 體驗有統一適用於所有樹系中，使用者可以指派 tootheir 樹系的應用程式使用 Azure AD 群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-173">While hello tenant and most of hello experience is unified for all forests, users can be assigned tootheir forest applications using Azure AD groups.</span></span>
 
### <a name="disaster-recovery-sites"></a><span data-ttu-id="bb597-174">災害復原網站</span><span class="sxs-lookup"><span data-stu-id="bb597-174">Disaster Recovery sites</span></span>

<span data-ttu-id="bb597-175">您可以根據您站台的實作方式，使用災害復原 (DR) 網站採用兩種不同的方法︰</span><span class="sxs-lookup"><span data-stu-id="bb597-175">There are two different approaches you can take with a disaster recovery (DR) site, depending on how your sites are implemented:</span></span>

* <span data-ttu-id="bb597-176">如果您的 DR 網站內建於主動 / 主動模式，其中與 hello 主要站台完全相同而且 hello 相同網路和 AD 設定，您可以在 hello hello DR 網站上建立 hello 連接器相同 hello 主要站台連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-176">If your DR site is built in active-active mode where it is exactly like hello main site and has hello same networking and AD settings, you can create hello connectors on hello DR site in hello same connector group as hello main site.</span></span> <span data-ttu-id="bb597-177">這樣可以為您的 Azure AD toodetect 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="bb597-177">This enables Azure AD toodetect failovers for you.</span></span>
* <span data-ttu-id="bb597-178">如果您的 DR 網站是分開 hello 主要站台，您可以在 hello DR 網站中，建立不同的連接器群組 1） 必須備份應用程式或 2） 手動將視轉向至 hello 現有應用程式 toohello DR 連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-178">If your DR site is separate from hello main site, you can create a different connector group in hello DR site, and either 1) have backup applications or 2) manually divert hello existing application toohello DR connector group as needed.</span></span>
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a><span data-ttu-id="bb597-179">從單一租用戶為多家公司提供服務</span><span class="sxs-lookup"><span data-stu-id="bb597-179">Serve multiple companies from a single tenant</span></span>

<span data-ttu-id="bb597-180">有許多不同的方式 tooimplement 單一服務提供者會將部署和維護 Azure AD 的模型相關的多個公司的服務。</span><span class="sxs-lookup"><span data-stu-id="bb597-180">There are many different ways tooimplement a model in which a single service provider deploys and maintains Azure AD related services for multiple companies.</span></span> <span data-ttu-id="bb597-181">連接器群組可協助 hello 系統管理員隔離 hello 連接器和應用程式分成不同的群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-181">Connector groups help hello admin segregate hello connectors and applications into different groups.</span></span> <span data-ttu-id="bb597-182">其中一個方法，這是適用於小型公司，是 toohave 單一雖然 hello 不同公司都有自己的網域名稱和網路的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bb597-182">One way, which is suitable for small companies, is toohave a single Azure AD tenant while hello different companies have their own domain name and networks.</span></span> <span data-ttu-id="bb597-183">M&A 案例和情況也是如此，其中單一 IT 部門會針對規範或企業原因為幾家公司提供服務。</span><span class="sxs-lookup"><span data-stu-id="bb597-183">This is also true for M&A scenarios and situations where a single IT division serves several companies for regulatory or business reasons.</span></span> 

## <a name="sample-configurations"></a><span data-ttu-id="bb597-184">範例組態</span><span class="sxs-lookup"><span data-stu-id="bb597-184">Sample configurations</span></span>

<span data-ttu-id="bb597-185">您可以實作，一些範例包括 hello 下列連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-185">Some examples that you can implement, include hello following connector groups.</span></span>
 
### <a name="default-configuration--no-use-for-connector-groups"></a><span data-ttu-id="bb597-186">預設組態 – 不使用連接器群組</span><span class="sxs-lookup"><span data-stu-id="bb597-186">Default configuration – no use for connector groups</span></span>

<span data-ttu-id="bb597-187">如果您不使用連接器群組，您的組態會看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="bb597-187">If you don’t use connector groups, your configuration would look like this:</span></span>

![AzureAD 沒有連接器群組](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
<span data-ttu-id="bb597-189">這個組態就對小型部署和測試就已足夠。</span><span class="sxs-lookup"><span data-stu-id="bb597-189">This configuration is sufficient for small deployments and tests.</span></span> <span data-ttu-id="bb597-190">如果您的組織具有平面網路拓撲，則它也會正常運作。</span><span class="sxs-lookup"><span data-stu-id="bb597-190">It will also work well if your organization has a flat network topology.</span></span>
 
### <a name="default-configuration-and-an-isolated-network"></a><span data-ttu-id="bb597-191">預設組態和隔離的網路</span><span class="sxs-lookup"><span data-stu-id="bb597-191">Default configuration and an isolated network</span></span>

<span data-ttu-id="bb597-192">此組態是 hello 預設值，這在沒有執行例如 IaaS 虛擬網路隔離網路中的特定應用程式的演進而來：</span><span class="sxs-lookup"><span data-stu-id="bb597-192">This configuration is an evolution of hello default one, in which there is a specific app that runs in an isolated network such as IaaS virtual network:</span></span> 

![AzureAD 沒有連接器群組](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a><span data-ttu-id="bb597-194">建議的組態 – 幾個特定的群組和預設的閒置群組</span><span class="sxs-lookup"><span data-stu-id="bb597-194">Recommended configuration – several specific groups and a default group for idle</span></span>

<span data-ttu-id="bb597-195">hello 建議組態的大型且複雜的組織為群組，不做任何應用程式，使用閒置或新安裝的連接器是 toohave hello 預設連接器群組。</span><span class="sxs-lookup"><span data-stu-id="bb597-195">hello recommended configuration for large and complex organizations is toohave hello default connector group as a group that doesn’t serve any applications and is used for idle or newly installed connectors.</span></span> <span data-ttu-id="bb597-196">所有應用程式會使用自訂的連接器群組來提供服務。</span><span class="sxs-lookup"><span data-stu-id="bb597-196">All applications are served using customized connector groups.</span></span> <span data-ttu-id="bb597-197">這可讓所有 hello 複雜度 hello 上面所述的案例。</span><span class="sxs-lookup"><span data-stu-id="bb597-197">This enables all hello complexity of hello scenarios described above.</span></span>

<span data-ttu-id="bb597-198">Hello 下列範例中，在 hello 公司會有兩個資料中心，A 和 B，以提供每個站台的兩個連接器。</span><span class="sxs-lookup"><span data-stu-id="bb597-198">In hello example below, hello company has two datacenters, A and B, with two connectors that serve each site.</span></span> <span data-ttu-id="bb597-199">每個網站都有不同的應用程式在其上執行。</span><span class="sxs-lookup"><span data-stu-id="bb597-199">Each site has different applications that run on it.</span></span> 

![AzureAD 沒有連接器群組](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a><span data-ttu-id="bb597-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb597-201">Next steps</span></span>

* [<span data-ttu-id="bb597-202">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="bb597-202">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
* [<span data-ttu-id="bb597-203">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="bb597-203">Enable single-sign on</span></span>](application-proxy-sso-overview.md)


