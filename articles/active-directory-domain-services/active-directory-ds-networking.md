---
title: "Azure AD Domain Services︰網路指導方針 | Microsoft Docs"
description: "Azure Active Directory Domain Services 的網路考量"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 8306c1ff72d348f5f327b79617e1422a78e26bdb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a><span data-ttu-id="ba28d-103">Azure AD 網域服務的網路考量</span><span class="sxs-lookup"><span data-stu-id="ba28d-103">Networking considerations for Azure AD Domain Services</span></span>
## <a name="how-to-select-an-azure-virtual-network"></a><span data-ttu-id="ba28d-104">如何選取 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="ba28d-104">How to select an Azure virtual network</span></span>
<span data-ttu-id="ba28d-105">下列指導方針可協助您選取要與 Azure AD 網域服務搭配使用的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-105">The following guidelines help you select a virtual network to use with Azure AD Domain Services.</span></span>

### <a name="type-of-azure-virtual-network"></a><span data-ttu-id="ba28d-106">Azure 虛擬網路類型</span><span class="sxs-lookup"><span data-stu-id="ba28d-106">Type of Azure virtual network</span></span>
* <span data-ttu-id="ba28d-107">您可以啟用傳統 Azure 虛擬網路中的 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="ba28d-107">You can enable Azure AD Domain Services in a classic Azure virtual network.</span></span>
* <span data-ttu-id="ba28d-108">**使用 Azure Resource Manager 建立的虛擬網路無法啟用**Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="ba28d-108">Azure AD Domain Services **cannot be enabled in virtual networks created using Azure Resource Manager**.</span></span>
* <span data-ttu-id="ba28d-109">您可以將以資源管理員為基礎的虛擬網路連接到啟用 Azure AD 網域服務的傳統虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-109">You can connect a Resource Manager-based virtual network to a classic virtual network in which Azure AD Domain Services is enabled.</span></span> <span data-ttu-id="ba28d-110">此後，您就能夠在以資源管理員為基礎的虛擬網路中使用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="ba28d-110">Thereafter, you can use Azure AD Domain Services in the Resource Manager-based virtual network.</span></span> <span data-ttu-id="ba28d-111">如需詳細資訊，請參閱[網路連線](active-directory-ds-networking.md#network-connectivity)。</span><span class="sxs-lookup"><span data-stu-id="ba28d-111">For more information, see the [Network connectivity](active-directory-ds-networking.md#network-connectivity) section.</span></span>
* <span data-ttu-id="ba28d-112">**區域虛擬網路**：如果您計劃使用現有的虛擬網路，請確定它是區域虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-112">**Regional Virtual Networks**: If you plan to use an existing virtual network, ensure that it is a regional virtual network.</span></span>

  * <span data-ttu-id="ba28d-113">使用舊版同質群組機制的虛擬網路不能與 Azure AD 網域服務搭配使用。</span><span class="sxs-lookup"><span data-stu-id="ba28d-113">Virtual networks that use the legacy affinity groups mechanism cannot be used with Azure AD Domain Services.</span></span>
  * <span data-ttu-id="ba28d-114">若要使用 Azure AD 網域服務， [請將傳統的虛擬網路移轉到區域虛擬網路](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="ba28d-114">To use Azure AD Domain Services, [migrate legacy virtual networks to regional virtual networks](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span></span>

### <a name="azure-region-for-the-virtual-network"></a><span data-ttu-id="ba28d-115">虛擬網路的 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="ba28d-115">Azure region for the virtual network</span></span>
* <span data-ttu-id="ba28d-116">您的 Azure AD 網域服務受管理網域已部署在與您選擇用來啟用該服務的虛擬網路所在的同一 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="ba28d-116">Your Azure AD Domain Services managed domain is deployed in the same Azure region as the virtual network you choose to enable the service in.</span></span>
* <span data-ttu-id="ba28d-117">選取虛擬網路，其位於 Azure AD 網域服務支援的 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="ba28d-117">Select a virtual network in an Azure region supported by Azure AD Domain Services.</span></span>
* <span data-ttu-id="ba28d-118">請參閱 [依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services/) 頁面，以了解可使用 Azure AD 網域服務的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="ba28d-118">See the [Azure services by region](https://azure.microsoft.com/regions/#services/) page to know the Azure regions in which Azure AD Domain Services is available.</span></span>

### <a name="requirements-for-the-virtual-network"></a><span data-ttu-id="ba28d-119">虛擬網路需求</span><span class="sxs-lookup"><span data-stu-id="ba28d-119">Requirements for the virtual network</span></span>
* <span data-ttu-id="ba28d-120">**Azure 工作負載的近接感測**：選取需要存取 Azure AD 網域服務的目前主控/即將主控的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-120">**Proximity to your Azure workloads**: Select the virtual network that currently hosts/will host virtual machines that need access to Azure AD Domain Services.</span></span>
* <span data-ttu-id="ba28d-121">**自訂/自備 DNS 伺服器**：請確定沒有針對虛擬網路設定的自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ba28d-121">**Custom/bring-your-own DNS servers**: Ensure that there are no custom DNS servers configured for the virtual network.</span></span>
* <span data-ttu-id="ba28d-122">**網域名稱相同的現有網域**：請確定現有網域的名稱並未與該虛擬網路上可用的網域名稱相同。</span><span class="sxs-lookup"><span data-stu-id="ba28d-122">**Existing domains with the same domain name**: Ensure that you do not have an existing domain with the same domain name available on that virtual network.</span></span> <span data-ttu-id="ba28d-123">例如，假設您有名為 'contoso.com' 的網域已可用於選取的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-123">For instance, assume you have a domain called 'contoso.com' already available on the selected virtual network.</span></span> <span data-ttu-id="ba28d-124">接著，您可嘗試在該虛擬網路上啟用具有相同網域名稱 (即 'contoso.com') 的 Azure AD 網域服務受管理網域。</span><span class="sxs-lookup"><span data-stu-id="ba28d-124">Later, you try to enable an Azure AD Domain Services managed domain with the same domain name (that is 'contoso.com') on that virtual network.</span></span> <span data-ttu-id="ba28d-125">您在嘗試啟用 Azure AD 網域服務時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ba28d-125">You encounter a failure when trying to enable Azure AD Domain Services.</span></span> <span data-ttu-id="ba28d-126">這個錯誤是因為名稱與該虛擬網路上的網域名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="ba28d-126">This failure is due to name conflicts for the domain name on that virtual network.</span></span> <span data-ttu-id="ba28d-127">在此情況下，您必須使用不同的名稱來設定 Azure AD 網域服務受管理網域。</span><span class="sxs-lookup"><span data-stu-id="ba28d-127">In this situation, you must use a different name to set up your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="ba28d-128">或者，您可以解除佈建現有的網域，然後繼續啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="ba28d-128">Alternately, you can de-provision the existing domain and then proceed to enable Azure AD Domain Services.</span></span>

> [!WARNING]
> <span data-ttu-id="ba28d-129">在您啟用網域服務之後，便無法將該服務移到不同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-129">You cannot move Domain Services to a different virtual network after you have enabled the service.</span></span>
>
>

## <a name="network-security-groups-and-subnet-design"></a><span data-ttu-id="ba28d-130">網路安全性群組與子網路設計</span><span class="sxs-lookup"><span data-stu-id="ba28d-130">Network Security Groups and subnet design</span></span>
<span data-ttu-id="ba28d-131">[網路安全性群組 (NSG)](../virtual-network/virtual-networks-nsg.md) 包含存取控制清單 (ACL) 規則的清單，可允許或拒絕虛擬網路中 VM 執行個體的網路流量。</span><span class="sxs-lookup"><span data-stu-id="ba28d-131">A [Network Security Group (NSG)](../virtual-network/virtual-networks-nsg.md) contains a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="ba28d-132">NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。</span><span class="sxs-lookup"><span data-stu-id="ba28d-132">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="ba28d-133">當 NSG 與子網路相關聯時，ACL 規則便會套用至該子網路中的所有 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ba28d-133">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="ba28d-134">此外，將 NSG 直接關聯至該 VM，即可進一步限制個別 VM 的流量。</span><span class="sxs-lookup"><span data-stu-id="ba28d-134">In addition, traffic to an individual VM can be restricted further by associating an NSG directly to that VM.</span></span>

![建議的子網路設計](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a><span data-ttu-id="ba28d-136">選擇子網路的最佳作法</span><span class="sxs-lookup"><span data-stu-id="ba28d-136">Best practices for choosing a subnet</span></span>
* <span data-ttu-id="ba28d-137">將 Azure AD 網域服務部署到 Azure 虛擬網路中**不同的專用子網路**。</span><span class="sxs-lookup"><span data-stu-id="ba28d-137">Deploy Azure AD Domain Services to a **separate dedicated subnet** within your Azure virtual network.</span></span>
* <span data-ttu-id="ba28d-138">請勿將 NSG 套用至受管理網域的專用子網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-138">Do not apply NSGs to the dedicated subnet for your managed domain.</span></span> <span data-ttu-id="ba28d-139">如果您必須將 NSG 套用至專用子網路，請確保**不會封鎖服務及管理您的網域所需的連接埠**。</span><span class="sxs-lookup"><span data-stu-id="ba28d-139">If you must apply NSGs to the dedicated subnet, ensure you **do not block the ports required to service and manage your domain**.</span></span>
* <span data-ttu-id="ba28d-140">請勿過度限制受管理網域的專用子網路內可用的 IP 位址數目。</span><span class="sxs-lookup"><span data-stu-id="ba28d-140">Do not overly restrict the number of IP addresses available within the dedicated subnet for your managed domain.</span></span> <span data-ttu-id="ba28d-141">此限制會使服務無法將兩個網域控制站提供給受管理的網域使用。</span><span class="sxs-lookup"><span data-stu-id="ba28d-141">This restriction prevents the service from making two domain controllers available for your managed domain.</span></span>
* <span data-ttu-id="ba28d-142">**請勿在虛擬網路的閘道子網路中啟用 Azure AD 網域服務**。</span><span class="sxs-lookup"><span data-stu-id="ba28d-142">**Do not enable Azure AD Domain Services in the gateway subnet** of your virtual network.</span></span>

> [!WARNING]
> <span data-ttu-id="ba28d-143">當您讓 NSG 與已啟用 Azure AD 網域服務的子網路產生關聯時，可能會中斷 Microsoft 服務及管理網域的功能。</span><span class="sxs-lookup"><span data-stu-id="ba28d-143">When you associate an NSG with a subnet in which Azure AD Domain Services is enabled, you may disrupt Microsoft's ability to service and manage the domain.</span></span> <span data-ttu-id="ba28d-144">此外，Azure AD 租用戶與受管理網域之間的同步處理已中斷。</span><span class="sxs-lookup"><span data-stu-id="ba28d-144">Additionally, synchronization between your Azure AD tenant and your managed domain is disrupted.</span></span> <span data-ttu-id="ba28d-145">**SLA 不適用於已套用 NSG 的部署，因為 NSG 會阻止 Azure AD 網域服務更新和管理您的網域。**</span><span class="sxs-lookup"><span data-stu-id="ba28d-145">**The SLA does not apply to deployments where an NSG has been applied that blocks Azure AD Domain Services from updating and managing your domain.**</span></span>
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a><span data-ttu-id="ba28d-146">Azure AD 網域服務所需的連接埠</span><span class="sxs-lookup"><span data-stu-id="ba28d-146">Ports required for Azure AD Domain Services</span></span>
<span data-ttu-id="ba28d-147">下列是 Azure AD 網域服務維護及服務受管理網域所需的連接埠。</span><span class="sxs-lookup"><span data-stu-id="ba28d-147">The following ports are required for Azure AD Domain Services to service and maintain your managed domain.</span></span> <span data-ttu-id="ba28d-148">請確保未針對已啟用受管理網域的子網路封鎖這些連接埠。</span><span class="sxs-lookup"><span data-stu-id="ba28d-148">Ensure that these ports are not blocked for the subnet in which you have enabled your managed domain.</span></span>

| <span data-ttu-id="ba28d-149">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="ba28d-149">Port number</span></span> | <span data-ttu-id="ba28d-150">目的</span><span class="sxs-lookup"><span data-stu-id="ba28d-150">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="ba28d-151">443</span><span class="sxs-lookup"><span data-stu-id="ba28d-151">443</span></span> |<span data-ttu-id="ba28d-152">與 Azure AD 租用戶同步處理</span><span class="sxs-lookup"><span data-stu-id="ba28d-152">Synchronization with your Azure AD tenant</span></span> |
| <span data-ttu-id="ba28d-153">3389</span><span class="sxs-lookup"><span data-stu-id="ba28d-153">3389</span></span> |<span data-ttu-id="ba28d-154">管理您的網域</span><span class="sxs-lookup"><span data-stu-id="ba28d-154">Management of your domain</span></span> |
| <span data-ttu-id="ba28d-155">5986</span><span class="sxs-lookup"><span data-stu-id="ba28d-155">5986</span></span> |<span data-ttu-id="ba28d-156">管理您的網域</span><span class="sxs-lookup"><span data-stu-id="ba28d-156">Management of your domain</span></span> |
| <span data-ttu-id="ba28d-157">636</span><span class="sxs-lookup"><span data-stu-id="ba28d-157">636</span></span> |<span data-ttu-id="ba28d-158">保護受管理網域的 LDAP (LDAPS) 存取</span><span class="sxs-lookup"><span data-stu-id="ba28d-158">Secure LDAP (LDAPS) access to your managed domain</span></span> |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a><span data-ttu-id="ba28d-159">具有 Azure AD Domain Services 之虛擬網路的範例 NSG</span><span class="sxs-lookup"><span data-stu-id="ba28d-159">Sample NSG for virtual networks with Azure AD Domain Services</span></span>
<span data-ttu-id="ba28d-160">下表說明您可以針對具有 Azure AD Domain Services 受管理網域之虛擬網路設定的範例 NSG。</span><span class="sxs-lookup"><span data-stu-id="ba28d-160">The following table illustrates a sample NSG you can configure for a virtual network with an Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="ba28d-161">這個規則允許從上述指定的連接埠輸入流量，以確保您受管理的網域保持修補、更新，並且可由 Microsoft 監視。</span><span class="sxs-lookup"><span data-stu-id="ba28d-161">This rule allows inbound traffic from the above specified ports to ensure your managed domain stays patched, updated and can be monitored by Microsoft.</span></span> <span data-ttu-id="ba28d-162">預設 'DenyAll' 規則適用於來自網際網路的所有其他輸入流量。</span><span class="sxs-lookup"><span data-stu-id="ba28d-162">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span>

<span data-ttu-id="ba28d-163">此外，NSG 也會說明如何透過網際網路來鎖定安全 LDAP 存取。</span><span class="sxs-lookup"><span data-stu-id="ba28d-163">Additionally, the NSG also illustrates how to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="ba28d-164">如果您尚未透過網際網路啟用安全 LDAP 存取至受管理的網域，請跳過此規則。</span><span class="sxs-lookup"><span data-stu-id="ba28d-164">Skip this rule if you have not enabled secure LDAP access to your managed domain over the internet.</span></span> <span data-ttu-id="ba28d-165">NSG 包含一組規則，允許僅從一組指定 IP 位址透過 TCP 連接埠 636 的輸入 LDAPS 存取。</span><span class="sxs-lookup"><span data-stu-id="ba28d-165">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="ba28d-166">允許從指定的 IP 位址透過網際網路之 LDAPS 存取的 NSG 規則，其優先順序高於 DenyAll NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="ba28d-166">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![透過網際網路之安全 LDAP 存取的範例 NSG](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="ba28d-168">**更多資訊** - [建立網路安全性群組](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="ba28d-168">**More information** - [Create a Network Security Group](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>


## <a name="network-connectivity"></a><span data-ttu-id="ba28d-169">網路連線</span><span class="sxs-lookup"><span data-stu-id="ba28d-169">Network connectivity</span></span>
<span data-ttu-id="ba28d-170">Azure AD 網域服務受管理網域只可在Azure 的單一傳統虛擬網路中啟用。</span><span class="sxs-lookup"><span data-stu-id="ba28d-170">An Azure AD Domain Services managed domain can be enabled only within a single classic virtual network in Azure.</span></span> <span data-ttu-id="ba28d-171">不支援使用 Azure Resource Manager 建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-171">Virtual networks created using Azure Resource Manager are not supported.</span></span>

### <a name="scenarios-for-connecting-azure-networks"></a><span data-ttu-id="ba28d-172">Azure 網路連線的案例</span><span class="sxs-lookup"><span data-stu-id="ba28d-172">Scenarios for connecting Azure networks</span></span>
<span data-ttu-id="ba28d-173">在下列各部署案例中，連接 Azure 虛擬網路來使用受管理的網域︰</span><span class="sxs-lookup"><span data-stu-id="ba28d-173">Connect Azure virtual networks to use the managed domain in any of the following deployment scenarios:</span></span>

#### <a name="use-the-managed-domain-in-more-than-one-azure-classic-virtual-network"></a><span data-ttu-id="ba28d-174">在多個 Azure 傳統虛擬網路中使用受管理的網域</span><span class="sxs-lookup"><span data-stu-id="ba28d-174">Use the managed domain in more than one Azure classic virtual network</span></span>
<span data-ttu-id="ba28d-175">您可以將其他 Azure 傳統虛擬網路連接到已啟用 Azure AD 網域服務的 Azure 傳統虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-175">You can connect other Azure classic virtual networks to the Azure classic virtual network in which you have enabled Azure AD Domain Services.</span></span> <span data-ttu-id="ba28d-176">此 VPN 連線可讓您使用受管理的網域，而您的工作負載已部署在其他虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="ba28d-176">This VPN connection enables you to use the managed domain with your workloads deployed in other virtual networks.</span></span>

![傳統的虛擬網路連線](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-the-managed-domain-in-a-resource-manager-based-virtual-network"></a><span data-ttu-id="ba28d-178">在以資源管理員為基礎的虛擬網路中，使用受管理的網域</span><span class="sxs-lookup"><span data-stu-id="ba28d-178">Use the managed domain in a Resource Manager-based virtual network</span></span>
<span data-ttu-id="ba28d-179">您可以將以資源管理員為基礎的虛擬網路連接到已啟用 Azure AD 網域服務的 Azure 傳統虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba28d-179">You can connect a Resource Manager-based virtual network to the Azure classic virtual network in which you have enabled Azure AD Domain Services.</span></span> <span data-ttu-id="ba28d-180">此連線可讓您使用受管理的網域，而您的工作負載已部署在以資源管理員為基礎的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="ba28d-180">This connection enables you to use the managed domain with your workloads deployed in the Resource Manager-based virtual network.</span></span>

![傳統虛擬網路連線的資源管理員](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a><span data-ttu-id="ba28d-182">網路連線選項</span><span class="sxs-lookup"><span data-stu-id="ba28d-182">Network connection options</span></span>
* <span data-ttu-id="ba28d-183">**使用站對站 VPN 連線的 VNet 對 VNet 連線**：將一個虛擬網路連接到另一個虛擬網路 (VNet 對 VNet) 類似於將虛擬網路連接到內部部署網站位置。</span><span class="sxs-lookup"><span data-stu-id="ba28d-183">**VNet-to-VNet connections using site-to-site VPN connections**: Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a virtual network to an on-premises site location.</span></span> <span data-ttu-id="ba28d-184">這兩種連線類型都使用 VPN 閘道提供使用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="ba28d-184">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span>

    ![使用 VPN 閘道的虛擬網路連線](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [<span data-ttu-id="ba28d-186">詳細資訊 - 使用 VPN 閘道連接虛擬網路</span><span class="sxs-lookup"><span data-stu-id="ba28d-186">More information - connect virtual networks using VPN gateway</span></span>](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* <span data-ttu-id="ba28d-187">**使用虛擬網路對等互連的 VNet 對 VNet 連線**：虛擬網路對等互連是透過 Azure 骨幹網路來連接同一區域中兩個虛擬網路的機制。</span><span class="sxs-lookup"><span data-stu-id="ba28d-187">**VNet-to-VNet connections using virtual network peering**: Virtual network peering is a mechanism that connects two virtual networks in the same region through the Azure backbone network.</span></span> <span data-ttu-id="ba28d-188">一旦對等互連，針對用作連線而言兩個虛擬網路看起來就像一個。</span><span class="sxs-lookup"><span data-stu-id="ba28d-188">Once peered, the two virtual networks appear as one for all connectivity purposes.</span></span> <span data-ttu-id="ba28d-189">它們仍做為不同的資源進行管理，但這些虛擬網路中的虛擬機器可以使用私人 IP 位址彼此直接通訊。</span><span class="sxs-lookup"><span data-stu-id="ba28d-189">They are still managed as separate resources, but virtual machines in these virtual networks can communicate with each other directly by using private IP addresses.</span></span>

    ![使用對等互連的虛擬網路連線](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [<span data-ttu-id="ba28d-191">詳細資訊 - 虛擬網路對等互連</span><span class="sxs-lookup"><span data-stu-id="ba28d-191">More information - virtual network peering</span></span>](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a><span data-ttu-id="ba28d-192">相關內容</span><span class="sxs-lookup"><span data-stu-id="ba28d-192">Related Content</span></span>
* [<span data-ttu-id="ba28d-193">Azure 虛擬網路對等互連</span><span class="sxs-lookup"><span data-stu-id="ba28d-193">Azure virtual network peering</span></span>](../virtual-network/virtual-network-peering-overview.md)
* [<span data-ttu-id="ba28d-194">設定傳統部署模型的 VNet 對 VNet 連接</span><span class="sxs-lookup"><span data-stu-id="ba28d-194">Configure a VNet-to-VNet connection for the classic deployment model</span></span>](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [<span data-ttu-id="ba28d-195">Azure 網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ba28d-195">Azure Network Security Groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="ba28d-196">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ba28d-196">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
