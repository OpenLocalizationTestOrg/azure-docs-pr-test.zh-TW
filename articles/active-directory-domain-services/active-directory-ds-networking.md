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
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a><span data-ttu-id="0a94f-103">Azure AD 網域服務的網路考量</span><span class="sxs-lookup"><span data-stu-id="0a94f-103">Networking considerations for Azure AD Domain Services</span></span>
## <a name="how-tooselect-an-azure-virtual-network"></a><span data-ttu-id="0a94f-104">如何 tooselect Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="0a94f-104">How tooselect an Azure virtual network</span></span>
<span data-ttu-id="0a94f-105">hello 下列方針可協助您選取的虛擬網路 toouse 與 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="0a94f-105">hello following guidelines help you select a virtual network toouse with Azure AD Domain Services.</span></span>

### <a name="type-of-azure-virtual-network"></a><span data-ttu-id="0a94f-106">Azure 虛擬網路類型</span><span class="sxs-lookup"><span data-stu-id="0a94f-106">Type of Azure virtual network</span></span>
* <span data-ttu-id="0a94f-107">您可以啟用傳統 Azure 虛擬網路中的 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="0a94f-107">You can enable Azure AD Domain Services in a classic Azure virtual network.</span></span>
* <span data-ttu-id="0a94f-108">**使用 Azure Resource Manager 建立的虛擬網路無法啟用**Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="0a94f-108">Azure AD Domain Services **cannot be enabled in virtual networks created using Azure Resource Manager**.</span></span>
* <span data-ttu-id="0a94f-109">您可以將資源管理員為基礎的虛擬網路 tooa 傳統虛擬網路連線 Azure AD 網域服務已啟用。</span><span class="sxs-lookup"><span data-stu-id="0a94f-109">You can connect a Resource Manager-based virtual network tooa classic virtual network in which Azure AD Domain Services is enabled.</span></span> <span data-ttu-id="0a94f-110">之後，您可以使用 Azure AD 網域服務中 hello 資源管理員為基礎的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-110">Thereafter, you can use Azure AD Domain Services in hello Resource Manager-based virtual network.</span></span> <span data-ttu-id="0a94f-111">如需詳細資訊，請參閱 hello[網路連線](active-directory-ds-networking.md#network-connectivity)> 一節。</span><span class="sxs-lookup"><span data-stu-id="0a94f-111">For more information, see hello [Network connectivity](active-directory-ds-networking.md#network-connectivity) section.</span></span>
* <span data-ttu-id="0a94f-112">**地區虛擬網路**： 如果您計劃 toouse 現有的虛擬網路，請確定它是區域虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-112">**Regional Virtual Networks**: If you plan toouse an existing virtual network, ensure that it is a regional virtual network.</span></span>

  * <span data-ttu-id="0a94f-113">使用 hello 舊版同質群組機制的虛擬網路不能與 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="0a94f-113">Virtual networks that use hello legacy affinity groups mechanism cannot be used with Azure AD Domain Services.</span></span>
  * <span data-ttu-id="0a94f-114">Azure AD 網域服務、 toouse[移轉繼承的虛擬網路 tooregional 虛擬網路](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="0a94f-114">toouse Azure AD Domain Services, [migrate legacy virtual networks tooregional virtual networks](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span></span>

### <a name="azure-region-for-hello-virtual-network"></a><span data-ttu-id="0a94f-115">Hello 虛擬網路的 azure 地區</span><span class="sxs-lookup"><span data-stu-id="0a94f-115">Azure region for hello virtual network</span></span>
* <span data-ttu-id="0a94f-116">您的 Azure AD 網域服務受管理的網域部署在 hello 與 hello 選擇 tooenable hello 服務中的虛擬網路相同的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-116">Your Azure AD Domain Services managed domain is deployed in hello same Azure region as hello virtual network you choose tooenable hello service in.</span></span>
* <span data-ttu-id="0a94f-117">選取虛擬網路，其位於 Azure AD 網域服務支援的 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="0a94f-117">Select a virtual network in an Azure region supported by Azure AD Domain Services.</span></span>
* <span data-ttu-id="0a94f-118">請參閱 hello[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)頁面 tooknow hello Azure AD 網域服務可用的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-118">See hello [Azure services by region](https://azure.microsoft.com/regions/#services/) page tooknow hello Azure regions in which Azure AD Domain Services is available.</span></span>

### <a name="requirements-for-hello-virtual-network"></a><span data-ttu-id="0a94f-119">Hello 虛擬網路需求</span><span class="sxs-lookup"><span data-stu-id="0a94f-119">Requirements for hello virtual network</span></span>
* <span data-ttu-id="0a94f-120">**鄰近 tooyour Azure 工作負載**： 選取 hello 目前裝載/將裝載虛擬機器需要存取 tooAzure AD 網域服務的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-120">**Proximity tooyour Azure workloads**: Select hello virtual network that currently hosts/will host virtual machines that need access tooAzure AD Domain Services.</span></span>
* <span data-ttu-id="0a94f-121">**自訂/使-您-擁有 DNS 伺服器**： 請確認沒有任何自訂的 DNS 伺服器 hello 虛擬網路設定。</span><span class="sxs-lookup"><span data-stu-id="0a94f-121">**Custom/bring-your-own DNS servers**: Ensure that there are no custom DNS servers configured for hello virtual network.</span></span>
* <span data-ttu-id="0a94f-122">**現有網域與 hello 相同的網域名稱**： 請確定您沒有現有的網域 hello 與該虛擬網路上可用的相同網域名稱。</span><span class="sxs-lookup"><span data-stu-id="0a94f-122">**Existing domains with hello same domain name**: Ensure that you do not have an existing domain with hello same domain name available on that virtual network.</span></span> <span data-ttu-id="0a94f-123">比方說，假設您擁有 hello 選取的虛擬網路上呼叫 'contoso.com' 已存在的網域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-123">For instance, assume you have a domain called 'contoso.com' already available on hello selected virtual network.</span></span> <span data-ttu-id="0a94f-124">您嘗試 tooenable hello 與 Azure AD 網域服務受管理網域的更新版本中，相同的網域名稱 （亦即 'contoso.com'） 上的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-124">Later, you try tooenable an Azure AD Domain Services managed domain with hello same domain name (that is 'contoso.com') on that virtual network.</span></span> <span data-ttu-id="0a94f-125">嘗試 tooenable Azure AD 網域服務時發生失敗。</span><span class="sxs-lookup"><span data-stu-id="0a94f-125">You encounter a failure when trying tooenable Azure AD Domain Services.</span></span> <span data-ttu-id="0a94f-126">此失敗是由於 tooname hello 網域名稱，該虛擬網路上的衝突。</span><span class="sxs-lookup"><span data-stu-id="0a94f-126">This failure is due tooname conflicts for hello domain name on that virtual network.</span></span> <span data-ttu-id="0a94f-127">在此情況下，您必須使用不同的名稱 tooset 註冊您 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-127">In this situation, you must use a different name tooset up your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="0a94f-128">或者，可以解除佈建 hello 現有網域，然後繼續 tooenable Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="0a94f-128">Alternately, you can de-provision hello existing domain and then proceed tooenable Azure AD Domain Services.</span></span>

> [!WARNING]
> <span data-ttu-id="0a94f-129">Hello 服務啟用後，您無法移動網域服務 tooa 不同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-129">You cannot move Domain Services tooa different virtual network after you have enabled hello service.</span></span>
>
>

## <a name="network-security-groups-and-subnet-design"></a><span data-ttu-id="0a94f-130">網路安全性群組與子網路設計</span><span class="sxs-lookup"><span data-stu-id="0a94f-130">Network Security Groups and subnet design</span></span>
<span data-ttu-id="0a94f-131">A[網路安全性群組 (NSG)](../virtual-network/virtual-networks-nsg.md)包含存取控制清單 (ACL) 規則，允許或拒絕網路流量 tooyour 虛擬網路中的 VM 執行個體的清單。</span><span class="sxs-lookup"><span data-stu-id="0a94f-131">A [Network Security Group (NSG)](../virtual-network/virtual-networks-nsg.md) contains a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="0a94f-132">NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。</span><span class="sxs-lookup"><span data-stu-id="0a94f-132">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="0a94f-133">NSG 與子網路產生關聯時，hello ACL 規則適用於 tooall hello VM 執行個體中子網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-133">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="0a94f-134">此外，流量 tooan 個別 VM 可能會限制進一步將 NSG 直接 toothat VM。</span><span class="sxs-lookup"><span data-stu-id="0a94f-134">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span>

![建議的子網路設計](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a><span data-ttu-id="0a94f-136">選擇子網路的最佳作法</span><span class="sxs-lookup"><span data-stu-id="0a94f-136">Best practices for choosing a subnet</span></span>
* <span data-ttu-id="0a94f-137">部署 Azure AD 網域服務 tooa**分隔專用子網路**Azure 虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="0a94f-137">Deploy Azure AD Domain Services tooa **separate dedicated subnet** within your Azure virtual network.</span></span>
* <span data-ttu-id="0a94f-138">不會套用 Nsg toohello 專用子網路的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-138">Do not apply NSGs toohello dedicated subnet for your managed domain.</span></span> <span data-ttu-id="0a94f-139">如果您必須先套用 Nsg toohello 專用子網路，請確定您**進行封鎖 hello 連接埠需要的 tooservice 及管理您的網域**。</span><span class="sxs-lookup"><span data-stu-id="0a94f-139">If you must apply NSGs toohello dedicated subnet, ensure you **do not block hello ports required tooservice and manage your domain**.</span></span>
* <span data-ttu-id="0a94f-140">不要過度限制 hello hello 專用子網路的受管理的網域內可用的 IP 位址數目。</span><span class="sxs-lookup"><span data-stu-id="0a94f-140">Do not overly restrict hello number of IP addresses available within hello dedicated subnet for your managed domain.</span></span> <span data-ttu-id="0a94f-141">這項限制防止 hello 服務兩個網域控制站可供受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-141">This restriction prevents hello service from making two domain controllers available for your managed domain.</span></span>
* <span data-ttu-id="0a94f-142">**請勿啟用 hello 閘道子網路中的 Azure AD 網域服務**的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-142">**Do not enable Azure AD Domain Services in hello gateway subnet** of your virtual network.</span></span>

> [!WARNING]
> <span data-ttu-id="0a94f-143">當您建立關聯 NSG 與 Azure AD 網域服務中的子網路已啟用，您可能會中斷 Microsoft 的能力 tooservice 和管理 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-143">When you associate an NSG with a subnet in which Azure AD Domain Services is enabled, you may disrupt Microsoft's ability tooservice and manage hello domain.</span></span> <span data-ttu-id="0a94f-144">此外，Azure AD 租用戶與受管理網域之間的同步處理已中斷。</span><span class="sxs-lookup"><span data-stu-id="0a94f-144">Additionally, synchronization between your Azure AD tenant and your managed domain is disrupted.</span></span> <span data-ttu-id="0a94f-145">**hello SLA 不適用的 toodeployments 其中 NSG 已套用該區塊的 Azure AD 網域服務更新與管理您的網域。**</span><span class="sxs-lookup"><span data-stu-id="0a94f-145">**hello SLA does not apply toodeployments where an NSG has been applied that blocks Azure AD Domain Services from updating and managing your domain.**</span></span>
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a><span data-ttu-id="0a94f-146">Azure AD 網域服務所需的連接埠</span><span class="sxs-lookup"><span data-stu-id="0a94f-146">Ports required for Azure AD Domain Services</span></span>
<span data-ttu-id="0a94f-147">hello 下列連接埠所需的 Azure AD 網域服務 tooservice 並維護受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-147">hello following ports are required for Azure AD Domain Services tooservice and maintain your managed domain.</span></span> <span data-ttu-id="0a94f-148">請確定這些連接埠不會封鎖 hello 子網路已啟用受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-148">Ensure that these ports are not blocked for hello subnet in which you have enabled your managed domain.</span></span>

| <span data-ttu-id="0a94f-149">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="0a94f-149">Port number</span></span> | <span data-ttu-id="0a94f-150">目的</span><span class="sxs-lookup"><span data-stu-id="0a94f-150">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="0a94f-151">443</span><span class="sxs-lookup"><span data-stu-id="0a94f-151">443</span></span> |<span data-ttu-id="0a94f-152">與 Azure AD 租用戶同步處理</span><span class="sxs-lookup"><span data-stu-id="0a94f-152">Synchronization with your Azure AD tenant</span></span> |
| <span data-ttu-id="0a94f-153">3389</span><span class="sxs-lookup"><span data-stu-id="0a94f-153">3389</span></span> |<span data-ttu-id="0a94f-154">管理您的網域</span><span class="sxs-lookup"><span data-stu-id="0a94f-154">Management of your domain</span></span> |
| <span data-ttu-id="0a94f-155">5986</span><span class="sxs-lookup"><span data-stu-id="0a94f-155">5986</span></span> |<span data-ttu-id="0a94f-156">管理您的網域</span><span class="sxs-lookup"><span data-stu-id="0a94f-156">Management of your domain</span></span> |
| <span data-ttu-id="0a94f-157">636</span><span class="sxs-lookup"><span data-stu-id="0a94f-157">636</span></span> |<span data-ttu-id="0a94f-158">安全 LDAP (LDAPS) 存取 tooyour 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="0a94f-158">Secure LDAP (LDAPS) access tooyour managed domain</span></span> |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a><span data-ttu-id="0a94f-159">具有 Azure AD Domain Services 之虛擬網路的範例 NSG</span><span class="sxs-lookup"><span data-stu-id="0a94f-159">Sample NSG for virtual networks with Azure AD Domain Services</span></span>
<span data-ttu-id="0a94f-160">下表中的 hello 說明範例 NSG，您可以設定虛擬網路與 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-160">hello following table illustrates a sample NSG you can configure for a virtual network with an Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="0a94f-161">此規則可讓您受管理的網域會保持修補、 更新和監視 Microsoft 以上面指定的連接埠 tooensure hello 的輸入的流量。</span><span class="sxs-lookup"><span data-stu-id="0a94f-161">This rule allows inbound traffic from hello above specified ports tooensure your managed domain stays patched, updated and can be monitored by Microsoft.</span></span> <span data-ttu-id="0a94f-162">hello 預設 'DenyAll' 規則套用 tooall 其他輸入的流量的 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-162">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span>

<span data-ttu-id="0a94f-163">此外，hello NSG 也說明如何透過安全 LDAP 存取 toolock hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-163">Additionally, hello NSG also illustrates how toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="0a94f-164">如果您沒有透過啟用安全 LDAP 存取 tooyour 受管理的網域，hello 網際網路，略過此規則。</span><span class="sxs-lookup"><span data-stu-id="0a94f-164">Skip this rule if you have not enabled secure LDAP access tooyour managed domain over hello internet.</span></span> <span data-ttu-id="0a94f-165">hello NSG 包含一組規則，允許對內的 LDAPS 存取透過 TCP 連接埠 636 只能從一組指定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0a94f-165">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="0a94f-166">hello NSG 規則 tooallow LDAPS 存取 hello 透過網際網路從指定的 IP 位址的優先順序高於 hello DenyAll NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="0a94f-166">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![透過範例 NSG toosecure LDAPS 存取 hello 網際網路](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="0a94f-168">**更多資訊** - [建立網路安全性群組](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="0a94f-168">**More information** - [Create a Network Security Group](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>


## <a name="network-connectivity"></a><span data-ttu-id="0a94f-169">網路連線</span><span class="sxs-lookup"><span data-stu-id="0a94f-169">Network connectivity</span></span>
<span data-ttu-id="0a94f-170">Azure AD 網域服務受管理網域只可在Azure 的單一傳統虛擬網路中啟用。</span><span class="sxs-lookup"><span data-stu-id="0a94f-170">An Azure AD Domain Services managed domain can be enabled only within a single classic virtual network in Azure.</span></span> <span data-ttu-id="0a94f-171">不支援使用 Azure Resource Manager 建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a94f-171">Virtual networks created using Azure Resource Manager are not supported.</span></span>

### <a name="scenarios-for-connecting-azure-networks"></a><span data-ttu-id="0a94f-172">Azure 網路連線的案例</span><span class="sxs-lookup"><span data-stu-id="0a94f-172">Scenarios for connecting Azure networks</span></span>
<span data-ttu-id="0a94f-173">連接 Azure 虛擬網路 toouse hello 受管理的網域中任何 hello 下列部署案例：</span><span class="sxs-lookup"><span data-stu-id="0a94f-173">Connect Azure virtual networks toouse hello managed domain in any of hello following deployment scenarios:</span></span>

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a><span data-ttu-id="0a94f-174">使用 hello 管理多個 Azure 傳統虛擬網路中的網域</span><span class="sxs-lookup"><span data-stu-id="0a94f-174">Use hello managed domain in more than one Azure classic virtual network</span></span>
<span data-ttu-id="0a94f-175">您可以連接其他傳統的 Azure 虛擬網路 toohello Azure 傳統的虛擬網路已啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="0a94f-175">You can connect other Azure classic virtual networks toohello Azure classic virtual network in which you have enabled Azure AD Domain Services.</span></span> <span data-ttu-id="0a94f-176">此 VPN 連線可讓您 toouse hello 受管理的網域與您在其他虛擬網路中部署的工作負載。</span><span class="sxs-lookup"><span data-stu-id="0a94f-176">This VPN connection enables you toouse hello managed domain with your workloads deployed in other virtual networks.</span></span>

![傳統的虛擬網路連線](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a><span data-ttu-id="0a94f-178">使用資源管理員為基礎的虛擬網路中的 hello 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="0a94f-178">Use hello managed domain in a Resource Manager-based virtual network</span></span>
<span data-ttu-id="0a94f-179">您可以連接的資源管理員為基礎的虛擬網路 toohello Azure 傳統的虛擬網路已啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="0a94f-179">You can connect a Resource Manager-based virtual network toohello Azure classic virtual network in which you have enabled Azure AD Domain Services.</span></span> <span data-ttu-id="0a94f-180">此連線可讓您 toouse hello 受管理的網域擁有 hello 資源管理員為基礎的虛擬網路中部署您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="0a94f-180">This connection enables you toouse hello managed domain with your workloads deployed in hello Resource Manager-based virtual network.</span></span>

![資源管理員 tooclassic 虛擬網路連線](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a><span data-ttu-id="0a94f-182">網路連線選項</span><span class="sxs-lookup"><span data-stu-id="0a94f-182">Network connection options</span></span>
* <span data-ttu-id="0a94f-183">**使用站對站 VPN 連線的 VNet 對 VNet 連線**： 連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting 虛擬網路 tooan 在內部部署站台位置。</span><span class="sxs-lookup"><span data-stu-id="0a94f-183">**VNet-to-VNet connections using site-to-site VPN connections**: Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a virtual network tooan on-premises site location.</span></span> <span data-ttu-id="0a94f-184">這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="0a94f-184">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span>

    ![使用 VPN 閘道的虛擬網路連線](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [<span data-ttu-id="0a94f-186">詳細資訊 - 使用 VPN 閘道連接虛擬網路</span><span class="sxs-lookup"><span data-stu-id="0a94f-186">More information - connect virtual networks using VPN gateway</span></span>](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* <span data-ttu-id="0a94f-187">**VNet 對 VNet 連線使用虛擬網路對等互連**： 虛擬網路對等互連是一套機制 hello 中的兩個虛擬網路連接在一起，透過網路 hello Azure 中樞相同的區域。</span><span class="sxs-lookup"><span data-stu-id="0a94f-187">**VNet-to-VNet connections using virtual network peering**: Virtual network peering is a mechanism that connects two virtual networks in hello same region through hello Azure backbone network.</span></span> <span data-ttu-id="0a94f-188">所以，一旦 hello 兩個虛擬網路會顯示為一個供所有連接。</span><span class="sxs-lookup"><span data-stu-id="0a94f-188">Once peered, hello two virtual networks appear as one for all connectivity purposes.</span></span> <span data-ttu-id="0a94f-189">它們仍做為不同的資源進行管理，但這些虛擬網路中的虛擬機器可以使用私人 IP 位址彼此直接通訊。</span><span class="sxs-lookup"><span data-stu-id="0a94f-189">They are still managed as separate resources, but virtual machines in these virtual networks can communicate with each other directly by using private IP addresses.</span></span>

    ![使用對等互連的虛擬網路連線](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [<span data-ttu-id="0a94f-191">詳細資訊 - 虛擬網路對等互連</span><span class="sxs-lookup"><span data-stu-id="0a94f-191">More information - virtual network peering</span></span>](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a><span data-ttu-id="0a94f-192">相關內容</span><span class="sxs-lookup"><span data-stu-id="0a94f-192">Related Content</span></span>
* [<span data-ttu-id="0a94f-193">Azure 虛擬網路對等互連</span><span class="sxs-lookup"><span data-stu-id="0a94f-193">Azure virtual network peering</span></span>](../virtual-network/virtual-network-peering-overview.md)
* [<span data-ttu-id="0a94f-194">設定 VNet 對 VNet 連線以 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="0a94f-194">Configure a VNet-to-VNet connection for hello classic deployment model</span></span>](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [<span data-ttu-id="0a94f-195">Azure 網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="0a94f-195">Azure Network Security Groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="0a94f-196">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="0a94f-196">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
