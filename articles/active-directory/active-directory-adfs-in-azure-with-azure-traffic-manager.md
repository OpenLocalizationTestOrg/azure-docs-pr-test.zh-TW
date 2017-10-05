---
title: "使用 Azure 流量管理員在 Azure 中部署高可用性跨地區 AD FS | Microsoft Docs"
description: "在本文件中，您將了解如何在 Azure 中部署 AD FS 以獲得高可用性。"
keywords: "採用 Azure 流量管理員的 Ad fs, 採用 Azure 流量管理員的 adfs, 地理, 多重資料中心, 地理資料中心, 多重地理資料中心, 在 azure 中部署 AD FS, 部署 azure adfs, azure adfs, azure ad fs, 部署 adfs, 部署 ad fs, azure 中的 adfs, 在 azure 中部署 adfs, 在 azure 中部署 AD FS, adfs azure, AD FS 簡介, Azure, Azure 中的 AD FS, iaas, ADFS, 將 adfs 移至 azure"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: 077710049894d2690299ce0fcb0ead9911aa4bb6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a><span data-ttu-id="50a30-104">使用 Azure 流量管理員在 Azure 中部署高可用性跨地區 AD FS</span><span class="sxs-lookup"><span data-stu-id="50a30-104">High availability cross-geographic AD FS deployment in Azure with Azure Traffic Manager</span></span>
<span data-ttu-id="50a30-105">[Azure 中的 AD FS 部署](active-directory-aadconnect-azure-adfs.md) 提供有關如何在 Azure 中為您的組織部署簡單 AD FS 基礎結構的逐步指導方針。</span><span class="sxs-lookup"><span data-stu-id="50a30-105">[AD FS deployment in Azure](active-directory-aadconnect-azure-adfs.md) provides step-by-step guideline as to how you can deploy a simple AD FS infrastructure for your organization in Azure.</span></span> <span data-ttu-id="50a30-106">本文會提供後續的步驟，以使用 [Azure 流量管理員](../traffic-manager/traffic-manager-overview.md)在 Azure 中建立跨地區的 AD FS 部署。</span><span class="sxs-lookup"><span data-stu-id="50a30-106">This article provides the next steps to create a cross-geographic deployment of AD FS in Azure using [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="50a30-107">Azure 流量管理員會使用各種可用的路由方法來順應基礎結構的不同需求，而有助於為您的組織建立分散各地的高可用性和高效能 AD FS 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="50a30-107">Azure Traffic Manager helps create a geographically spread high availability and high-performance AD FS infrastructure for your organization by making use of range of routing methods available to suit different needs from the infrastructure.</span></span>

<span data-ttu-id="50a30-108">高可用性的跨地區 AD FS基礎結構能夠︰</span><span class="sxs-lookup"><span data-stu-id="50a30-108">A highly available cross-geographic AD FS infrastructure enables:</span></span>

* <span data-ttu-id="50a30-109">**消除單一失敗點︰** 利用 Azure 流量管理員的容錯移轉功能，即使全球其中一個資料中心無法使用，您仍可達到高可用性的 AD FS 基礎結構</span><span class="sxs-lookup"><span data-stu-id="50a30-109">**Elimination of single point of failure:** With failover capabilities of Azure Traffic Manager, you can achieve a highly available AD FS infrastructure even when one of the data centers in a part of the globe goes down</span></span>
* <span data-ttu-id="50a30-110">**的效能︰** 您可以使用本文中建議的部署，以提供高效能的 AD FS 基礎結構來協助使用者更快驗證。</span><span class="sxs-lookup"><span data-stu-id="50a30-110">**Improved performance:** You can use the suggested deployment in this article to provide a high-performance AD FS infrastructure that can help users authenticate faster.</span></span> 

## <a name="design-principles"></a><span data-ttu-id="50a30-111">設計原則</span><span class="sxs-lookup"><span data-stu-id="50a30-111">Design principles</span></span>
![整體設計](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

<span data-ttu-id="50a30-113">基本設計原則會與＜Azure 中的 AD FS 部署＞一文中所列的設計原則相同。</span><span class="sxs-lookup"><span data-stu-id="50a30-113">The basic design principles will be same as listed in Design principles in the article AD FS deployment in Azure.</span></span> <span data-ttu-id="50a30-114">上圖顯示的是將基本部署擴充至另一個地理區域的簡易延伸模組。</span><span class="sxs-lookup"><span data-stu-id="50a30-114">The diagram above shows a simple extension of the basic deployment to another geographical region.</span></span> <span data-ttu-id="50a30-115">以下是將您的部署擴充到新地理區域時所要考量的一些重點</span><span class="sxs-lookup"><span data-stu-id="50a30-115">Below are some points to consider when extending your deployment to new geographical region</span></span>

* <span data-ttu-id="50a30-116">**虛擬網路︰** 您應該在您要部署其他 AD FS 基礎結構的地理區域中建立新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="50a30-116">**Virtual network:** You should create a new virtual network in the geographical region you want to deploy additional AD FS infrastructure.</span></span> <span data-ttu-id="50a30-117">在上圖中，您會看到 Geo1 VNET 和 Geo2 VNET 顯示為每個地理區中的兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="50a30-117">In the diagram above you see Geo1 VNET and Geo2 VNET as the two virtual networks in each geographical region.</span></span>
* <span data-ttu-id="50a30-118">**新地區 VNET 中的網域控制站和 AD FS 伺服器︰** 建議在新的地理區域中部署網域控制站，在新區域中的 AD FS 伺服器就不需要連絡另一個遙遠網路中的網域控制站來完成驗證，因而改善效能。</span><span class="sxs-lookup"><span data-stu-id="50a30-118">**Domain controllers and AD FS servers in new geographical VNET:** It is recommended to deploy domain controllers in the new geographical region so that the AD FS servers in the new region do not have to contact a domain controller in another far away network to complete an authentication and thereby improving the performance.</span></span>
* <span data-ttu-id="50a30-119">**儲存體帳戶︰** 儲存體帳戶會與某個區域相關聯。</span><span class="sxs-lookup"><span data-stu-id="50a30-119">**Storage accounts:** Storage accounts are associated with a region.</span></span> <span data-ttu-id="50a30-120">因為您即將在新的地理區域中部署機器，所以您必須建立要在此區域中使用的新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="50a30-120">Since you will be deploying machines in a new geographic region, you will have to create new storage accounts to be used in the region.</span></span>  
* <span data-ttu-id="50a30-121">**網路安全性群組︰** 如同儲存體帳戶，在區域中建立的網路安全性群組不能用於另一個地理區域。</span><span class="sxs-lookup"><span data-stu-id="50a30-121">**Network Security Groups:** As storage accounts, Network Security Groups created in a region cannot be used in another geographical region.</span></span> <span data-ttu-id="50a30-122">因此，您必須為新地理區域中的 INT 和 DMZ 子網路，建立類似於第一個地理區域中的新網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="50a30-122">Therefore, you will need to create new network security groups similar to those in the first geographical region for INT and DMZ subnet in the new geographical region.</span></span>
* <span data-ttu-id="50a30-123">**公用 IP 位址的 DNS 標籤︰** Azure 流量管理員只能透過 DNS 標籤參考端點。</span><span class="sxs-lookup"><span data-stu-id="50a30-123">**DNS Labels for public IP addresses:** Azure Traffic Manager can refer to endpoints ONLY via DNS labels.</span></span> <span data-ttu-id="50a30-124">因此，您必須為外部負載平衡器的公用 IP 位址建立 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="50a30-124">Therefore, you are required to create DNS labels for the External Load Balancers’ public IP addresses.</span></span>
* <span data-ttu-id="50a30-125">**Azure 流量管理員** ：Microsoft Azure 流量管理員可讓您控制使用者流量，將流量分散到您在世界各地的不同資料中心執行的服務端點。</span><span class="sxs-lookup"><span data-stu-id="50a30-125">**Azure Traffic Manager:** Microsoft Azure Traffic Manager allows you to control the distribution of user traffic to your service endpoints running in different datacenters around the world.</span></span> <span data-ttu-id="50a30-126">Azure 流量管理員是在 DNS 層級上運作。</span><span class="sxs-lookup"><span data-stu-id="50a30-126">Azure Traffic Manager works at the DNS level.</span></span> <span data-ttu-id="50a30-127">它會使用 DNS 回應，將使用者流量導向全域散佈的端點。</span><span class="sxs-lookup"><span data-stu-id="50a30-127">It uses DNS responses to direct end-user traffic to globally-distributed endpoints.</span></span> <span data-ttu-id="50a30-128">接著用戶端會直接連接到這些端點。</span><span class="sxs-lookup"><span data-stu-id="50a30-128">Clients then connect to those endpoints directly.</span></span> <span data-ttu-id="50a30-129">效能、加權和優先順序均有不同的路由選項，您可以輕鬆地選擇最符合貴組織需求的路由選項。</span><span class="sxs-lookup"><span data-stu-id="50a30-129">With different routing options of Performance, Weighted and Priority, you can easily choose the routing option best suited for your organization’s needs.</span></span> 
* <span data-ttu-id="50a30-130">**兩個區域之間的 VNet 對 VNet 連線︰** 您不需要具備虛擬網路本身之間的連線。</span><span class="sxs-lookup"><span data-stu-id="50a30-130">**V-net to V-net connectivity between two regions:** You do not need to have connectivity between the virtual networks itself.</span></span> <span data-ttu-id="50a30-131">因為每個虛擬網路都可存取網域控制站，而且本身都有 AD FS 和 WAP 伺服器，所以不同區域中的虛擬網路之間不需要任何連線，即可運作。</span><span class="sxs-lookup"><span data-stu-id="50a30-131">Since each virtual network has access to domain controllers and has AD FS and WAP server in itself, they can work without any connectivity between the virtual networks in different regions.</span></span> 

## <a name="steps-to-integrate-azure-traffic-manager"></a><span data-ttu-id="50a30-132">整合 Azure 流量管理員的步驟</span><span class="sxs-lookup"><span data-stu-id="50a30-132">Steps to integrate Azure Traffic Manager</span></span>
### <a name="deploy-ad-fs-in-the-new-geographical-region"></a><span data-ttu-id="50a30-133">在新的地理區域中部署 AD FS</span><span class="sxs-lookup"><span data-stu-id="50a30-133">Deploy AD FS in the new geographical region</span></span>
<span data-ttu-id="50a30-134">請依照 [Azure 中的 AD FS 部署](active-directory-aadconnect-azure-adfs.md) 中的步驟和指導方針，在新的地理區域中部署相同的拓樸。</span><span class="sxs-lookup"><span data-stu-id="50a30-134">Follow the steps and guidelines in [AD FS deployment in Azure](active-directory-aadconnect-azure-adfs.md) to deploy the same topology in the new geographical region.</span></span>

### <a name="dns-labels-for-public-ip-addresses-of-the-internet-facing-public-load-balancers"></a><span data-ttu-id="50a30-135">網際網路對向 (公用) 負載平衡器中公用 IP 位址的 DNS 標籤</span><span class="sxs-lookup"><span data-stu-id="50a30-135">DNS labels for public IP addresses of the Internet Facing (public) Load Balancers</span></span>
<span data-ttu-id="50a30-136">如上所述，Azure 流量管理員只可以將 DNS 標籤當作端點參考，因此務必為外部負載平衡器的公用 IP 位址建立 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="50a30-136">As mentioned above, the Azure Traffic Manager can only refer to DNS labels as endpoints and therefore it is important to create DNS labels for the External Load Balancers’ public IP addresses.</span></span> <span data-ttu-id="50a30-137">以下螢幕擷取畫面顯示如何設定公用 IP 位址的 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="50a30-137">Below screenshot shows how you can configure your DNS label for the public IP address.</span></span> 

![DNS 標籤](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a><span data-ttu-id="50a30-139">部署 Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="50a30-139">Deploying Azure Traffic Manager</span></span>
<span data-ttu-id="50a30-140">依照以下步驟建立流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="50a30-140">Follow the steps below to create a traffic manager profile.</span></span> <span data-ttu-id="50a30-141">如需詳細資訊，您也可以參考 [管理 Azure 流量管理員設定檔](../traffic-manager/traffic-manager-manage-profiles.md)。</span><span class="sxs-lookup"><span data-stu-id="50a30-141">For more information, you can also refer to [Manage an Azure Traffic Manager profile](../traffic-manager/traffic-manager-manage-profiles.md).</span></span>

1. <span data-ttu-id="50a30-142">**建立流量管理員設定檔** ：為您的流量管理員設定檔提供一個唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="50a30-142">**Create a Traffic Manager profile:** Give your traffic manager profile a unique name.</span></span> <span data-ttu-id="50a30-143">設定檔的這個名稱是 DNS 名稱的一部分，並可做為流量管理員網域名稱標籤的前置詞。</span><span class="sxs-lookup"><span data-stu-id="50a30-143">This name of the profile is part of the DNS name and acts as a prefix for the Traffic Manager domain name label.</span></span> <span data-ttu-id="50a30-144">系統會將此名稱 / 前置詞新增至 .trafficmanager.net，以建立流量管理員的 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="50a30-144">The name / prefix is added to .trafficmanager.net to create a DNS label for your traffic manager.</span></span> <span data-ttu-id="50a30-145">以下螢幕擷取畫面顯示設定為 mysts 的流量管理員 DNS 前置詞，而產生的 DNS 標籤會是 mysts.trafficmanager.net。</span><span class="sxs-lookup"><span data-stu-id="50a30-145">The screenshot below shows the traffic manager DNS prefix being set as mysts and resulting DNS label will be mysts.trafficmanager.net.</span></span> 
   
    ![流量管理員設定檔建立](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. <span data-ttu-id="50a30-147">**流量路由方法：** 流量管理員中有三個可用的路由選項：</span><span class="sxs-lookup"><span data-stu-id="50a30-147">**Traffic routing method:** There are three routing options available in traffic manager:</span></span>
   
   * <span data-ttu-id="50a30-148">優先順序</span><span class="sxs-lookup"><span data-stu-id="50a30-148">Priority</span></span> 
   * <span data-ttu-id="50a30-149">效能</span><span class="sxs-lookup"><span data-stu-id="50a30-149">Performance</span></span>
   * <span data-ttu-id="50a30-150">加權</span><span class="sxs-lookup"><span data-stu-id="50a30-150">Weighted</span></span>
     
     <span data-ttu-id="50a30-151">**效能** 是達到高回應性 AD FS 基礎結構的建議選項。</span><span class="sxs-lookup"><span data-stu-id="50a30-151">**Performance** is the recommended option to achieve highly responsive AD FS infrastructure.</span></span> <span data-ttu-id="50a30-152">不過，您可以選擇任何最適合您的部署需求的路由方式。</span><span class="sxs-lookup"><span data-stu-id="50a30-152">However, you can choose any routing method best suited for your deployment needs.</span></span> <span data-ttu-id="50a30-153">AD FS 功能不會受到所選取的路由選項影響。</span><span class="sxs-lookup"><span data-stu-id="50a30-153">The AD FS functionality is not impacted by the routing option selected.</span></span> <span data-ttu-id="50a30-154">如需詳細資訊，請參閱 [流量管理員流量路由方法](../traffic-manager/traffic-manager-routing-methods.md) 。</span><span class="sxs-lookup"><span data-stu-id="50a30-154">See [Traffic Manager traffic routing methods](../traffic-manager/traffic-manager-routing-methods.md) for more information.</span></span> <span data-ttu-id="50a30-155">在上面的範例螢幕擷取畫面中，您可以看到已選取 **效能** 方法。</span><span class="sxs-lookup"><span data-stu-id="50a30-155">In the sample screenshot above you can see the **Performance** method selected.</span></span>
3. <span data-ttu-id="50a30-156">**設定端點︰** 在流量管理員頁面中，按一下端點並選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="50a30-156">**Configure endpoints:** In the traffic manager page, click on endpoints and select Add.</span></span> <span data-ttu-id="50a30-157">這會開啟類似以下螢幕擷取畫面的 [新增端點] 頁面</span><span class="sxs-lookup"><span data-stu-id="50a30-157">This will open an Add endpoint page similar to the screenshot below</span></span>
   
   ![設定端點](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   <span data-ttu-id="50a30-159">對於不同的輸入，請遵循下列指導方針︰</span><span class="sxs-lookup"><span data-stu-id="50a30-159">For the different inputs, follow the guideline below:</span></span>
   
   <span data-ttu-id="50a30-160">**類型︰** 選取 Azure 端點，因為我們即將指向 Azure 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="50a30-160">**Type:** Select Azure endpoint as we will be pointing to an Azure public IP address.</span></span>
   
   <span data-ttu-id="50a30-161">**名稱︰** 建立您想要與端點建立關聯的名稱。</span><span class="sxs-lookup"><span data-stu-id="50a30-161">**Name:** Create a name that you want to associate with the endpoint.</span></span> <span data-ttu-id="50a30-162">這不是 DNS 名稱，所以與 DNS 記錄沒有關聯。</span><span class="sxs-lookup"><span data-stu-id="50a30-162">This is not the DNS name and has no bearing on DNS records.</span></span>
   
   <span data-ttu-id="50a30-163">**目標資源類型︰** 選取公用 IP 位址做為這個屬性的值。</span><span class="sxs-lookup"><span data-stu-id="50a30-163">**Target resource type:** Select Public IP address as the value to this property.</span></span> 
   
   <span data-ttu-id="50a30-164">**目標資源︰** 這可讓您選擇不同於您訂用帳戶之下可用的 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="50a30-164">**Target resource:** This will give you an option to choose from the different DNS labels you have available under your subscription.</span></span> <span data-ttu-id="50a30-165">選擇對應到您要設定之端點的 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="50a30-165">Choose the DNS label corresponding to the endpoint you are configuring.</span></span>
   
   <span data-ttu-id="50a30-166">針對您希望 Azure 流量管理員路由傳送流量的每個地理區域，新增端點。</span><span class="sxs-lookup"><span data-stu-id="50a30-166">Add endpoint for each geographical region you want the Azure Traffic Manager to route traffic to.</span></span>
   <span data-ttu-id="50a30-167">如需有關如何在流量管理員中新增 / 設定端點的詳細資訊和詳細步驟，請參閱 [新增、停用、啟用或刪除端點](../traffic-manager/traffic-manager-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="50a30-167">For more information and detailed steps on how to add / configure endpoints in traffic manager, refer to [Add, disable, enable or delete endpoints](../traffic-manager/traffic-manager-endpoints.md)</span></span>
4. <span data-ttu-id="50a30-168">**設定探查︰** 在流量管理員頁面中，按一下 [組態]。</span><span class="sxs-lookup"><span data-stu-id="50a30-168">**Configure probe:** In the traffic manager page, click on Configuration.</span></span> <span data-ttu-id="50a30-169">在 [組態] 頁面中，您便需變更監視設定，以在 HTTP 連接埠 80 和相對路徑 /adfs/probe 探查</span><span class="sxs-lookup"><span data-stu-id="50a30-169">In the configuration page, you need to change the monitor settings to probe at HTTP port 80 and relative path /adfs/probe</span></span>
   
    ![設定探查](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > <span data-ttu-id="50a30-171">**確保在設定完成時，端點的狀態會處於線上狀態**。</span><span class="sxs-lookup"><span data-stu-id="50a30-171">**Ensure that the status of the endpoints is ONLINE once the configuration is complete**.</span></span> <span data-ttu-id="50a30-172">如果所有端點都處於「降級」狀態，則 Azure 流量管理員會盡力嘗試路由傳送流量，但前提是診斷不正確，而且所有端點均可觸達。</span><span class="sxs-lookup"><span data-stu-id="50a30-172">If all endpoints are in ‘degraded’ state, Azure Traffic Manager will do a best attempt to route the traffic assuming that the diagnostics is incorrect and all endpoints are reachable.</span></span>
   > 
   > 
5. <span data-ttu-id="50a30-173">**修改 Azure 流量管理員的 DNS 記錄︰** 您的同盟服務應該是 Azure 流量管理員 DNS 名稱的 CNAME。</span><span class="sxs-lookup"><span data-stu-id="50a30-173">**Modifying DNS records for Azure Traffic Manager:** Your federation service should be a CNAME to the Azure Traffic Manager DNS name.</span></span> <span data-ttu-id="50a30-174">在公用 DNS 記錄中建立 CNAME，以便正嘗試觸達同盟服務的人員實際觸達 Azure 流量管理員。</span><span class="sxs-lookup"><span data-stu-id="50a30-174">Create a CNAME in the public DNS records so that whoever is trying to reach the federation service actually reaches the Azure Traffic Manager.</span></span>
   
    <span data-ttu-id="50a30-175">例如，若要將同盟服務 fs.fabidentity.com 指向流量管理員，您需要將 DNS 資源記錄更新如下：</span><span class="sxs-lookup"><span data-stu-id="50a30-175">For example, to point the federation service fs.fabidentity.com to the Traffic Manager, you would need to update your DNS resource record to be the following:</span></span>
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-the-routing-and-ad-fs-sign-in"></a><span data-ttu-id="50a30-176">測試路由和 AD FS 登入</span><span class="sxs-lookup"><span data-stu-id="50a30-176">Test the routing and AD FS sign-in</span></span>
### <a name="routing-test"></a><span data-ttu-id="50a30-177">路由測試</span><span class="sxs-lookup"><span data-stu-id="50a30-177">Routing test</span></span>
<span data-ttu-id="50a30-178">路由的基本測試就是嘗試從每個地理區域中的機器 ping 同盟服務 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="50a30-178">A very basic test for the routing would be to try ping the federation service DNS name from a machine in each geographic region.</span></span> <span data-ttu-id="50a30-179">視所選的路由方法而定，其實際 ping 的端點將會反映在 ping 顯示中。</span><span class="sxs-lookup"><span data-stu-id="50a30-179">Depending on the routing method chosen, the endpoint it actually pings will be reflected in the ping display.</span></span> <span data-ttu-id="50a30-180">例如，如果您選取了效能路由，則會觸達最接近用戶端區域的端點。</span><span class="sxs-lookup"><span data-stu-id="50a30-180">For example, if you selected the performance routing, then the endpoint nearest to the region of the client will be reached.</span></span> <span data-ttu-id="50a30-181">以下是兩個來自兩個不同區域用戶端電腦的 ping 快照，一個位於 EastAsia 區域，一個位於美國西部。</span><span class="sxs-lookup"><span data-stu-id="50a30-181">Below is the snapshot of two pings from two different region client machines, one in EastAsia region and one in West US.</span></span> 

![路由測試](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a><span data-ttu-id="50a30-183">AD FS 登入測試</span><span class="sxs-lookup"><span data-stu-id="50a30-183">AD FS sign-in test</span></span>
<span data-ttu-id="50a30-184">若要測試 AD FS，最簡單的方法是使用 IdpInitiatedSignon.aspx 網頁。</span><span class="sxs-lookup"><span data-stu-id="50a30-184">The easiest way to test AD FS is by using the IdpInitiatedSignon.aspx page.</span></span> <span data-ttu-id="50a30-185">為了能夠執行此作業，必須在 AD FS 屬性上啟用 IdpInitiatedSignOn。</span><span class="sxs-lookup"><span data-stu-id="50a30-185">In order to be able to do that, it is required to enable the IdpInitiatedSignOn on the AD FS properties.</span></span> <span data-ttu-id="50a30-186">請遵循下列步驟來確認 AD FS 設定</span><span class="sxs-lookup"><span data-stu-id="50a30-186">Follow the steps below to verify your AD FS setup</span></span>

1. <span data-ttu-id="50a30-187">使用 PowerShell 在 AD FS 伺服器上執行以下 Cmdlet，將它設定為啟用。</span><span class="sxs-lookup"><span data-stu-id="50a30-187">Run the below cmdlet on the AD FS server, using PowerShell, to set it to enabled.</span></span> 
   <span data-ttu-id="50a30-188">Set-AdfsProperties -EnableIdPInitiatedSignonPage $true</span><span class="sxs-lookup"><span data-stu-id="50a30-188">Set-AdfsProperties -EnableIdPInitiatedSignonPage $true</span></span>
2. <span data-ttu-id="50a30-189">從任何外部電腦存取 https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx</span><span class="sxs-lookup"><span data-stu-id="50a30-189">From any external machine access https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx</span></span>
3. <span data-ttu-id="50a30-190">您應該會看到如下圖的 AD FS 網頁︰</span><span class="sxs-lookup"><span data-stu-id="50a30-190">You should see the AD FS page like below:</span></span>
   
    ![ADFS 測試 - 驗證挑戰](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    <span data-ttu-id="50a30-192">而成功登入時，它會提供您如下所示的成功訊息︰</span><span class="sxs-lookup"><span data-stu-id="50a30-192">and on successful sign-in, it will provide you with a success message as shown below:</span></span>
   
    ![ADFS 測試 - 驗證](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a><span data-ttu-id="50a30-194">相關連結</span><span class="sxs-lookup"><span data-stu-id="50a30-194">Related links</span></span>
* [<span data-ttu-id="50a30-195">Azure 中的基本 AD FS 部署</span><span class="sxs-lookup"><span data-stu-id="50a30-195">Basic AD FS deployment in Azure</span></span>](active-directory-aadconnect-azure-adfs.md)
* [<span data-ttu-id="50a30-196">Microsoft Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="50a30-196">Microsoft Azure Traffic Manager</span></span>](../traffic-manager/traffic-manager-overview.md)
* [<span data-ttu-id="50a30-197">流量管理員流量路由方法</span><span class="sxs-lookup"><span data-stu-id="50a30-197">Traffic Manager traffic routing methods</span></span>](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a><span data-ttu-id="50a30-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50a30-198">Next steps</span></span>
* [<span data-ttu-id="50a30-199">管理 Azure 流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="50a30-199">Manage an Azure Traffic Manager profile</span></span>](../traffic-manager/traffic-manager-manage-profiles.md)
* [<span data-ttu-id="50a30-200">加入、停用、啟用或刪除端點</span><span class="sxs-lookup"><span data-stu-id="50a30-200">Add, disable, enable or delete endpoints</span></span>](../traffic-manager/traffic-manager-endpoints.md) 

