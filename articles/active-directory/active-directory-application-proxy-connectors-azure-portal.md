---
title: "在 Azure AD 應用程式 Proxy 中使用連接器群組在個別的網路和位置上發佈應用程式 | Microsoft Docs"
description: "涵蓋如何建立和管理「Azure AD 應用程式 Proxy」中的連接器群組。"
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
ms.openlocfilehash: 1b08a0b376cbcae8522364c9b6ef22e9c0176438
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="1da0b-103">使用連接器群組在個別的網路和位置上發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="1da0b-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1da0b-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1da0b-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="1da0b-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="1da0b-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>

<span data-ttu-id="1da0b-106">客戶在越來越多的案例和應用程式中利用 Azure AD 的應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="1da0b-106">Customers utilize Azure AD's Application Proxy for more and more scenarios and applications.</span></span> <span data-ttu-id="1da0b-107">因此我們啟用更多的拓撲使應用程式 Proxy 更具彈性。</span><span class="sxs-lookup"><span data-stu-id="1da0b-107">So we've made App Proxy even more flexible by enabling more topologies.</span></span> <span data-ttu-id="1da0b-108">您可以建立應用程式 Proxy 連接器群組，如此便可以指派特定連接器以提供特定應用程式。</span><span class="sxs-lookup"><span data-stu-id="1da0b-108">You can create Application Proxy connector groups so that you can assign specific connectors to serve specific applications.</span></span> <span data-ttu-id="1da0b-109">此功能讓您有更多的控制能力與方法來最佳化應用程式 Proxy 部署。</span><span class="sxs-lookup"><span data-stu-id="1da0b-109">This capability gives you more control and ways to optimize your Application Proxy deployment.</span></span> 

<span data-ttu-id="1da0b-110">每個應用程式 Proxy 連接器都會指派給連接器群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-110">Each Application Proxy connector is assigned to a connector group.</span></span> <span data-ttu-id="1da0b-111">隸屬於相同連接器群組的所有連接器會做為高可用性及負載平衡的個別單位。</span><span class="sxs-lookup"><span data-stu-id="1da0b-111">All the connectors that belong to the same connector group act as a separate unit for high-availability and load balancing.</span></span> <span data-ttu-id="1da0b-112">所有的連接器皆屬於連接器群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-112">All connectors belong to a connector group.</span></span> <span data-ttu-id="1da0b-113">如果您未建立群組，則所有的連接器皆會在預設群組中。</span><span class="sxs-lookup"><span data-stu-id="1da0b-113">If you don't create groups, then all your connectors are in a default group.</span></span> <span data-ttu-id="1da0b-114">系統管理員可以建立新的群組，並在 Azure 入口網站中將連接器指派給群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-114">Your admin can create new groups and assign connectors to them in the Azure portal.</span></span> 

<span data-ttu-id="1da0b-115">所有應用程式均會指派給連接器群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-115">All applications are assigned to a connector group.</span></span> <span data-ttu-id="1da0b-116">如果您未建立群組，則所有的連接器皆會指派給預設群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-116">If you don't create groups, then all your applications are assigned to a default group.</span></span> <span data-ttu-id="1da0b-117">但是，如果您將連接器組織成群組，可以設定每個應用程式使用特定連接器群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-117">But if you organize your connectors into groups, you can set each application to work with a specific connector group.</span></span> <span data-ttu-id="1da0b-118">在此情況下，只有該群組中的連接器會在收到要求時為應用程式提供服務。</span><span class="sxs-lookup"><span data-stu-id="1da0b-118">In this case, only the connectors in that group serve the application upon request.</span></span> <span data-ttu-id="1da0b-119">如果您的應用程式裝載在不同的位置中，這是個很有用的功能。</span><span class="sxs-lookup"><span data-stu-id="1da0b-119">This feature is useful if your applications are hosted in different locations.</span></span> <span data-ttu-id="1da0b-120">您可以根據位置來建立連接器群組，讓應用程式一律由實體位置相近的連接器提供服務。</span><span class="sxs-lookup"><span data-stu-id="1da0b-120">You can create connector groups based on location, so that applications are always served by connectors that are physically close to them.</span></span>

>[!TIP] 
><span data-ttu-id="1da0b-121">如果您有大規模的應用程式 Proxy 部署，請勿將任何應用程式指派給預設連接器群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-121">If you have a large Application Proxy deployment, don't assign any applications to the default connector group.</span></span> <span data-ttu-id="1da0b-122">如此一來，新的連接器便不會收到任何即時流量，除非您將新連接器指派給作用中的連接器群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-122">That way, new connectors don't receive any live traffic until you assign them to an active connector group.</span></span> <span data-ttu-id="1da0b-123">此設定也可以將連接器移回預設群組的方式，藉此讓連接器進入閒置模式，如此您便可以在不影響使用者的情況下執行維護。</span><span class="sxs-lookup"><span data-stu-id="1da0b-123">This configuration also enables you to put connectors in an idle mode by moving them back to the default group, so that you can perform maintenance without impacting your users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1da0b-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="1da0b-124">Prerequisites</span></span>
<span data-ttu-id="1da0b-125">若要將連接器組成群組，您必須確定 [已安裝多個連接器](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="1da0b-125">To group your connectors, you have to make sure you [installed multiple connectors](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="1da0b-126">當您安裝新的連接器時，它會自動加入「預設」  連接器群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-126">When you install a new connector, it automatically joins the **Default** connector group.</span></span>

## <a name="create-connector-groups"></a><span data-ttu-id="1da0b-127">建立連接器群組</span><span class="sxs-lookup"><span data-stu-id="1da0b-127">Create connector groups</span></span>
<span data-ttu-id="1da0b-128">使用以下步驟建立您所要的連接器群組，數量不拘。</span><span class="sxs-lookup"><span data-stu-id="1da0b-128">Use these steps to create as many connector groups as you want.</span></span> 

1. <span data-ttu-id="1da0b-129">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1da0b-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="1da0b-130">選取 [Azure Active Directory]  >  [企業應用程式]  >  [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="1da0b-130">Select **Azure Active Directory** > **Enterprise applications** > **Application proxy**.</span></span>
2. <span data-ttu-id="1da0b-131">選取 [新增連接器群組]。</span><span class="sxs-lookup"><span data-stu-id="1da0b-131">Select **New connector group**.</span></span> <span data-ttu-id="1da0b-132">[新增連接器群組] 刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1da0b-132">The New Connector Group blade appears.</span></span>

   ![選取新的連接器群組](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. <span data-ttu-id="1da0b-134">指定新連接器群組的名稱，然後使用下拉式功能表來選取哪些連接器屬於此群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-134">Give your new connector group a name, then use the dropdown menu to select which connectors belong in this group.</span></span>
4. <span data-ttu-id="1da0b-135">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="1da0b-135">Select **Save**.</span></span>

## <a name="assign-applications-to-your-connector-groups"></a><span data-ttu-id="1da0b-136">將應用程式指派給您的連接器群組</span><span class="sxs-lookup"><span data-stu-id="1da0b-136">Assign applications to your connector groups</span></span>
<span data-ttu-id="1da0b-137">已透過應用程式 Proxy 發佈的每個應用程式均按照這些步驟處理。</span><span class="sxs-lookup"><span data-stu-id="1da0b-137">Use these steps for each application that you've published with Application Proxy.</span></span> <span data-ttu-id="1da0b-138">您可以在首次發佈應用程式時，將應用程式指派給連接器群組，也可以隨時使用這些步驟變更指派。</span><span class="sxs-lookup"><span data-stu-id="1da0b-138">You can assign an application to a connector group when you first publish it, or you can use these steps to change the assignment whenever you want.</span></span>   

1. <span data-ttu-id="1da0b-139">從您目錄的管理儀表板中，選取 [企業應用程式] > [所有應用程式] > 您想要指派給連接器群組的應用程式 > [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="1da0b-139">From the management dashboard for your directory, select **Enterprise applications** > **All applications** > the application you want to assign to a connector group > **Application Proxy**.</span></span>
2. <span data-ttu-id="1da0b-140">使用 [連接器群組] 下拉式功能表來選取應用程式所要使用的群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-140">Use the **Connector Group** dropdown menu to select the group you want the application to use.</span></span>
3. <span data-ttu-id="1da0b-141">按一下 [儲存]  以套用變更。</span><span class="sxs-lookup"><span data-stu-id="1da0b-141">Select **Save** to apply the change.</span></span>

## <a name="use-cases-for-connector-groups"></a><span data-ttu-id="1da0b-142">連接器群組的使用案例</span><span class="sxs-lookup"><span data-stu-id="1da0b-142">Use cases for connector groups</span></span> 

<span data-ttu-id="1da0b-143">連接器群組可用於多種不同狀況，包括：</span><span class="sxs-lookup"><span data-stu-id="1da0b-143">Connector groups are useful for various scenarios, including:</span></span>

### <a name="sites-with-multiple-interconnected-datacenters"></a><span data-ttu-id="1da0b-144">具有多個互連資料中心的網站</span><span class="sxs-lookup"><span data-stu-id="1da0b-144">Sites with multiple interconnected datacenters</span></span>

<span data-ttu-id="1da0b-145">許多組織都有數個彼此連接的資料中心。</span><span class="sxs-lookup"><span data-stu-id="1da0b-145">Many organizations have a number of interconnected datacenters.</span></span> <span data-ttu-id="1da0b-146">在此情況下，您會希望儘量將流量保留在資料中心內，因為跨資料中心的連結既昂貴、速度又慢。</span><span class="sxs-lookup"><span data-stu-id="1da0b-146">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="1da0b-147">您可以在每個資料中心都部署連接器，來只為資料中心內的應用程式提供服務。</span><span class="sxs-lookup"><span data-stu-id="1da0b-147">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="1da0b-148">這種方法可將跨資料中心的連結減到最少，讓使用者體驗完全的流暢性。</span><span class="sxs-lookup"><span data-stu-id="1da0b-148">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>

### <a name="applications-installed-on-isolated-networks"></a><span data-ttu-id="1da0b-149">安裝在隔離網路上的應用程式</span><span class="sxs-lookup"><span data-stu-id="1da0b-149">Applications installed on isolated networks</span></span>

<span data-ttu-id="1da0b-150">應用程式可以在不是主要的公司網路一部分的網路上託管。</span><span class="sxs-lookup"><span data-stu-id="1da0b-150">Applications can be hosted in networks that are not part of the main corporate network.</span></span> <span data-ttu-id="1da0b-151">您可以使用連接器群組將專用連接器安裝在隔離網路上，以同時將應用程式與網路隔離。</span><span class="sxs-lookup"><span data-stu-id="1da0b-151">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span> <span data-ttu-id="1da0b-152">當協力廠商為您的組織維護特定應用程式時，就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="1da0b-152">This usually happens when a third-party vendor maintains a specific application for your organization.</span></span> 

<span data-ttu-id="1da0b-153">連接器群組可讓您安裝僅發佈特定應用程式之網路的專用連接器，使外包應用程式管理給協力廠商更輕鬆且更安全。</span><span class="sxs-lookup"><span data-stu-id="1da0b-153">Connector groups allow you to install dedicated connectors for those networks that publish only specific applications, making it easier and more secure to outsource application management to third-party vendors.</span></span>

### <a name="applications-installed-on-iaas"></a><span data-ttu-id="1da0b-154">IaaS 上已安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="1da0b-154">Applications installed on IaaS</span></span> 

<span data-ttu-id="1da0b-155">對於安裝在 IaaS 上以供雲端存取的應用程式，連接器群組提供通用的服務來保護對所有應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="1da0b-155">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="1da0b-156">連接器群組不會對公司網路產生額外的相依性，或是造成不完整的應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="1da0b-156">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="1da0b-157">連接器可安裝在每個雲端資料中心，而且只為該網路中的應用程式提供服務。</span><span class="sxs-lookup"><span data-stu-id="1da0b-157">Connectors can be installed on every cloud datacenter and serve only applications that reside in that network.</span></span> <span data-ttu-id="1da0b-158">您可以安裝數個連接器以獲得高可用性。</span><span class="sxs-lookup"><span data-stu-id="1da0b-158">You can install several connectors to achieve high availability.</span></span>

<span data-ttu-id="1da0b-159">以擁有數個虛擬機器連線到本身 IaaS 主控之虛擬網路的組織為例。</span><span class="sxs-lookup"><span data-stu-id="1da0b-159">Take as an example an organization that has several virtual machines connected to their own IaaS hosted virtual network.</span></span> <span data-ttu-id="1da0b-160">若要允許員工使用這些應用程式，這些私人網路會使用站台對站 VPN 連線到公司網路。</span><span class="sxs-lookup"><span data-stu-id="1da0b-160">To allow employees to use these applications, these private networks are connected to the corporate network using site-to-site VPN.</span></span> <span data-ttu-id="1da0b-161">針對位於內部部署的員工，這會提供良好的體驗。</span><span class="sxs-lookup"><span data-stu-id="1da0b-161">This provides a good experience for employees that are located on-premises.</span></span> <span data-ttu-id="1da0b-162">但是，它可能不適合遠端員工，因為它需要額外內部部署基礎結構來路由存取權，如您所見下圖顯示︰</span><span class="sxs-lookup"><span data-stu-id="1da0b-162">But, it may not be ideal for remote employees, because it requires additional on-premises infrastructure to route access, as you can see in the diagram below:</span></span>

![AzureAD Iaas 網路](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
<span data-ttu-id="1da0b-164">使用 Azure AD 應用程式 Proxy 連接器群組，您可以啟用一般服務來保護所有應用程式，而無須在您的公司網路上建立其他相依性︰</span><span class="sxs-lookup"><span data-stu-id="1da0b-164">With Azure AD Application Proxy connector groups, you can enable a common service to secure the access to all applications without creating additional dependency on your corporate network:</span></span>

![AzureAD Iaas 多雲端廠商](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a><span data-ttu-id="1da0b-166">多樹系 – 每個樹系不同的連接器群組</span><span class="sxs-lookup"><span data-stu-id="1da0b-166">Multi-forest – different connector groups for each forest</span></span>

<span data-ttu-id="1da0b-167">大部分已部署應用程式 Proxy 的客戶會執行 Kerberos 限制委派 (KCD) 來使用單一登入 (SSO) 功能。</span><span class="sxs-lookup"><span data-stu-id="1da0b-167">Most customers who have deployed Application Proxy are using its single-sign-on (SSO) capabilities by performing Kerberos Constrained Delegation (KCD).</span></span> <span data-ttu-id="1da0b-168">若要達到此目的，連接器的電腦需要加入可將使用者委派至應用程式的網域。</span><span class="sxs-lookup"><span data-stu-id="1da0b-168">To achieve this, the connector’s machines need to be joined to a domain that can delegate the users toward the application.</span></span> <span data-ttu-id="1da0b-169">KCD 支援跨樹系功能。</span><span class="sxs-lookup"><span data-stu-id="1da0b-169">KCD supports cross-forest capabilities.</span></span> <span data-ttu-id="1da0b-170">但對於擁有不同的多樹系環境且它們之間沒有信任的公司來說，單一連接器無法用於所有的樹系。</span><span class="sxs-lookup"><span data-stu-id="1da0b-170">But for companies who have distinct multi-forest environments with no trust between them, a single connector cannot be used for all forests.</span></span> 

<span data-ttu-id="1da0b-171">在此情況下，每個樹系可以部署特定連接器，並設定為僅為該特定樹系使用者提供服務所發佈的應用程式提供服務。</span><span class="sxs-lookup"><span data-stu-id="1da0b-171">In this case, specific connectors can be deployed per forest, and set to serve applications that were published to serve only the users of that specific forest.</span></span> <span data-ttu-id="1da0b-172">每個連接器群組代表不同的樹系。</span><span class="sxs-lookup"><span data-stu-id="1da0b-172">Each connector group represents a different forest.</span></span> <span data-ttu-id="1da0b-173">雖然租用戶和大部分的體驗會針對所有樹系進行整合，使用者可以使用 Azure AD 群組指派給其樹系的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1da0b-173">While the tenant and most of the experience is unified for all forests, users can be assigned to their forest applications using Azure AD groups.</span></span>
 
### <a name="disaster-recovery-sites"></a><span data-ttu-id="1da0b-174">災害復原網站</span><span class="sxs-lookup"><span data-stu-id="1da0b-174">Disaster Recovery sites</span></span>

<span data-ttu-id="1da0b-175">您可以根據您站台的實作方式，使用災害復原 (DR) 網站採用兩種不同的方法︰</span><span class="sxs-lookup"><span data-stu-id="1da0b-175">There are two different approaches you can take with a disaster recovery (DR) site, depending on how your sites are implemented:</span></span>

* <span data-ttu-id="1da0b-176">如果您的 DR 網站是在主動-主動模式中建置，其中與主要站台完全相同，且具有相同的網路與 AD 設定，您可以在與主要站台相同的連接器群組中，在 DR 網站上建立連接器。</span><span class="sxs-lookup"><span data-stu-id="1da0b-176">If your DR site is built in active-active mode where it is exactly like the main site and has the same networking and AD settings, you can create the connectors on the DR site in the same connector group as the main site.</span></span> <span data-ttu-id="1da0b-177">這可讓 Azure AD 為您偵測容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1da0b-177">This enables Azure AD to detect failovers for you.</span></span>
* <span data-ttu-id="1da0b-178">如果 DR 網站是獨立於主要網站，您可以在 DR 網站中建立不同的連接器群組，並且 1) 擁有備份應用程式，或 2) 視需要手動將現有的應用程式轉向至 DR 連接器群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-178">If your DR site is separate from the main site, you can create a different connector group in the DR site, and either 1) have backup applications or 2) manually divert the existing application to the DR connector group as needed.</span></span>
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a><span data-ttu-id="1da0b-179">從單一租用戶為多家公司提供服務</span><span class="sxs-lookup"><span data-stu-id="1da0b-179">Serve multiple companies from a single tenant</span></span>

<span data-ttu-id="1da0b-180">有許多不同的方式可實作模型，其中單一服務提供者可部署及為多家公司維護 Azure AD 的相關服務。</span><span class="sxs-lookup"><span data-stu-id="1da0b-180">There are many different ways to implement a model in which a single service provider deploys and maintains Azure AD related services for multiple companies.</span></span> <span data-ttu-id="1da0b-181">連接器群組可協助系統管理員將連接器和應用程式分成不同的群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-181">Connector groups help the admin segregate the connectors and applications into different groups.</span></span> <span data-ttu-id="1da0b-182">適合小型公司的一個方法是擁有單一 Azure AD 租用戶，同時不同公司都有自己的網域名稱和網路。</span><span class="sxs-lookup"><span data-stu-id="1da0b-182">One way, which is suitable for small companies, is to have a single Azure AD tenant while the different companies have their own domain name and networks.</span></span> <span data-ttu-id="1da0b-183">M&A 案例和情況也是如此，其中單一 IT 部門會針對規範或企業原因為幾家公司提供服務。</span><span class="sxs-lookup"><span data-stu-id="1da0b-183">This is also true for M&A scenarios and situations where a single IT division serves several companies for regulatory or business reasons.</span></span> 

## <a name="sample-configurations"></a><span data-ttu-id="1da0b-184">範例組態</span><span class="sxs-lookup"><span data-stu-id="1da0b-184">Sample configurations</span></span>

<span data-ttu-id="1da0b-185">您可以實作一些範例，包括下列連接器群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-185">Some examples that you can implement, include the following connector groups.</span></span>
 
### <a name="default-configuration--no-use-for-connector-groups"></a><span data-ttu-id="1da0b-186">預設組態 – 不使用連接器群組</span><span class="sxs-lookup"><span data-stu-id="1da0b-186">Default configuration – no use for connector groups</span></span>

<span data-ttu-id="1da0b-187">如果您不使用連接器群組，您的組態會看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="1da0b-187">If you don’t use connector groups, your configuration would look like this:</span></span>

![AzureAD 沒有連接器群組](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
<span data-ttu-id="1da0b-189">這個組態就對小型部署和測試就已足夠。</span><span class="sxs-lookup"><span data-stu-id="1da0b-189">This configuration is sufficient for small deployments and tests.</span></span> <span data-ttu-id="1da0b-190">如果您的組織具有平面網路拓撲，則它也會正常運作。</span><span class="sxs-lookup"><span data-stu-id="1da0b-190">It will also work well if your organization has a flat network topology.</span></span>
 
### <a name="default-configuration-and-an-isolated-network"></a><span data-ttu-id="1da0b-191">預設組態和隔離的網路</span><span class="sxs-lookup"><span data-stu-id="1da0b-191">Default configuration and an isolated network</span></span>

<span data-ttu-id="1da0b-192">此組態是預設的演化，其中有在隔離網路 (例如 IaaS 虛擬網路) 中執行的特定應用程式︰</span><span class="sxs-lookup"><span data-stu-id="1da0b-192">This configuration is an evolution of the default one, in which there is a specific app that runs in an isolated network such as IaaS virtual network:</span></span> 

![AzureAD 沒有連接器群組](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a><span data-ttu-id="1da0b-194">建議的組態 – 幾個特定的群組和預設的閒置群組</span><span class="sxs-lookup"><span data-stu-id="1da0b-194">Recommended configuration – several specific groups and a default group for idle</span></span>

<span data-ttu-id="1da0b-195">大型及複雜組織的建議組態是具有預設連接器群組做為不提供任何應用程式服務並用於閒置或新安裝連接器的群組。</span><span class="sxs-lookup"><span data-stu-id="1da0b-195">The recommended configuration for large and complex organizations is to have the default connector group as a group that doesn’t serve any applications and is used for idle or newly installed connectors.</span></span> <span data-ttu-id="1da0b-196">所有應用程式會使用自訂的連接器群組來提供服務。</span><span class="sxs-lookup"><span data-stu-id="1da0b-196">All applications are served using customized connector groups.</span></span> <span data-ttu-id="1da0b-197">這可啟用上述案例的所有複雜度。</span><span class="sxs-lookup"><span data-stu-id="1da0b-197">This enables all the complexity of the scenarios described above.</span></span>

<span data-ttu-id="1da0b-198">下列範例中，公司有兩個資料中心 (A 和 B)，並具有兩個連接器可為每個站台提供服務。</span><span class="sxs-lookup"><span data-stu-id="1da0b-198">In the example below, the company has two datacenters, A and B, with two connectors that serve each site.</span></span> <span data-ttu-id="1da0b-199">每個網站都有不同的應用程式在其上執行。</span><span class="sxs-lookup"><span data-stu-id="1da0b-199">Each site has different applications that run on it.</span></span> 

![AzureAD 沒有連接器群組](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a><span data-ttu-id="1da0b-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1da0b-201">Next steps</span></span>

* [<span data-ttu-id="1da0b-202">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="1da0b-202">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
* [<span data-ttu-id="1da0b-203">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="1da0b-203">Enable single-sign on</span></span>](application-proxy-sso-overview.md)


