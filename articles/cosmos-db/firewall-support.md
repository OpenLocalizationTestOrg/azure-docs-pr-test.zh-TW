---
title: "Azure Cosmos DB 防火牆支援和 IP 存取控制 | Microsoft Docs"
description: "了解如何使用 IP 存取控制原則進行 Azure Cosmos DB 資料庫帳戶上的防火牆支援。"
keywords: "IP 存取控制，防火牆支援"
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: e08c0ba9c1fc0bab72ae8c1158aafaad4f66920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-firewall-support"></a><span data-ttu-id="acc79-104">Azure Cosmos DB 防火牆支援</span><span class="sxs-lookup"><span data-stu-id="acc79-104">Azure Cosmos DB firewall support</span></span>
<span data-ttu-id="acc79-105">為了保護 Azure Cosmos DB 資料庫帳戶中所儲存的資料，Azure Cosmos DB 已支援利用強式雜湊式訊息驗證碼 (HMAC) 的密碼型[授權模型](https://msdn.microsoft.com/library/azure/dn783368.aspx)。</span><span class="sxs-lookup"><span data-stu-id="acc79-105">To secure data stored in an Azure Cosmos DB database account, Azure Cosmos DB has provided support for a secret based [authorization model](https://msdn.microsoft.com/library/azure/dn783368.aspx) that utilizes a strong Hash-based message authentication code (HMAC).</span></span> <span data-ttu-id="acc79-106">現在，除了密碼型授權模型之外，Azure Cosmos DB 還支援使用原則驅動的 IP 型存取控制來進行輸入防火牆支援。</span><span class="sxs-lookup"><span data-stu-id="acc79-106">Now, in addition to the secret based authorization model, Azure Cosmos DB supports policy driven IP-based access controls for inbound firewall support.</span></span> <span data-ttu-id="acc79-107">這個模型與傳統資料庫系統的防火牆規則十分類似，並提供 Azure Cosmos DB 資料庫帳戶的額外安全性層級。</span><span class="sxs-lookup"><span data-stu-id="acc79-107">This model is very similar to the firewall rules of a traditional database system and provides an additional level of security to the Azure Cosmos DB database account.</span></span> <span data-ttu-id="acc79-108">您現在可以使用這個模型，設定只能從一組核准的電腦和 (或) 雲端服務存取 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="acc79-108">With this model, you can now configure an Azure Cosmos DB database account to be accessible only from an approved set of machines and/or cloud services.</span></span> <span data-ttu-id="acc79-109">透過這些核准的電腦和服務組合來存取 Azure Cosmos DB 資源，仍然需要呼叫者呈現有效的授權權杖。</span><span class="sxs-lookup"><span data-stu-id="acc79-109">Access to Azure Cosmos DB resources from these approved sets of machines and services still require the caller to present a valid authorization token.</span></span>

## <a name="ip-access-control-overview"></a><span data-ttu-id="acc79-110">IP 存取控制概觀</span><span class="sxs-lookup"><span data-stu-id="acc79-110">IP access control overview</span></span>
<span data-ttu-id="acc79-111">只要要求伴隨有效的授權權杖，預設就可以從公用網際網路存取 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="acc79-111">By default, an Azure Cosmos DB database account is accessible from public internet as long as the request is accompanied by a valid authorization token.</span></span> <span data-ttu-id="acc79-112">若要設定 IP 原則型存取控制，使用者必須以 CIDR 形式提供這組 IP 位址或 IP 位址範圍，以作為指定資料庫帳戶的允許用戶端 IP 清單。</span><span class="sxs-lookup"><span data-stu-id="acc79-112">To configure IP policy-based access control, the user must provide the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="acc79-113">套用這個組態之後，伺服器將會封鎖源自此允許清單外部之電腦的所有要求。</span><span class="sxs-lookup"><span data-stu-id="acc79-113">Once this configuration is applied, all requests originating from machines outside this allowed list will be blocked by the server.</span></span>  <span data-ttu-id="acc79-114">下圖說明 IP 型存取控制的連接處理流程。</span><span class="sxs-lookup"><span data-stu-id="acc79-114">The connection processing flow for the IP-based access control is described in the following diagram.</span></span>

![顯示 IP 型存取控制之連接程序的圖表](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a><span data-ttu-id="acc79-116">從雲端服務的連接</span><span class="sxs-lookup"><span data-stu-id="acc79-116">Connections from cloud services</span></span>
<span data-ttu-id="acc79-117">在 Azure 中，雲端服務是使用 Azure Cosmos DB 裝載中介層服務邏輯的極常見方式。</span><span class="sxs-lookup"><span data-stu-id="acc79-117">In Azure, cloud services are a very common way for hosting middle tier service logic using Azure Cosmos DB.</span></span> <span data-ttu-id="acc79-118">若要從雲端服務存取 Azure Cosmos DB 資料庫帳戶，必須[設定 IP 存取控制原則](#configure-ip-policy)，以將雲端服務的公用 IP 位址新增至與 Azure Cosmos DB 資料庫帳戶相關聯的允許 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="acc79-118">To enable access to an Azure Cosmos DB database account from a cloud service, the public IP address of the cloud service must be added to the allowed list of IP addresses associated with your Azure Cosmos DB database account by [configuring the IP access control policy](#configure-ip-policy).</span></span>  <span data-ttu-id="acc79-119">這確保雲端服務的所有角色執行個體都能存取您的 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="acc79-119">This ensures that all role instances of cloud services have access to your Azure Cosmos DB database account.</span></span> <span data-ttu-id="acc79-120">您可以在 Azure 入口網站中擷取雲端服務的 IP 位址，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="acc79-120">You can retrieve IP addresses for your cloud services in the Azure portal, as shown in the following screenshot.</span></span>

![這個螢幕擷取畫面顯示 Azure 入口網站中所顯示雲端服務的公用 IP 位址](./media/firewall-support/public-ip-addresses.png)

<span data-ttu-id="acc79-122">當您新增其他角色執行個體來相應放大雲端服務時，那些新的執行個體將可自動存取 Azure Cosmos DB 資料庫帳戶，因為它們是相同雲端服務的一部分。</span><span class="sxs-lookup"><span data-stu-id="acc79-122">When you scale out your cloud service by adding additional role instance(s), those new instances will automatically have access to the Azure Cosmos DB database account since they are part of the same cloud service.</span></span>

## <a name="connections-from-virtual-machines"></a><span data-ttu-id="acc79-123">從虛擬機器的連接</span><span class="sxs-lookup"><span data-stu-id="acc79-123">Connections from virtual machines</span></span>
<span data-ttu-id="acc79-124">您也可以使用[虛擬機器](https://azure.microsoft.com/services/virtual-machines/)或[虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)，透過 Azure Cosmos DB 裝載中介層服務。</span><span class="sxs-lookup"><span data-stu-id="acc79-124">[Virtual machines](https://azure.microsoft.com/services/virtual-machines/) or [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) can also be used to host middle tier services using Azure Cosmos DB.</span></span>  <span data-ttu-id="acc79-125">若要設定允許從虛擬機器存取 Azure Cosmos DB 資料庫帳戶，必須[設定 IP 存取控制原則](#configure-ip-policy)，以將虛擬機器和 (或) 虛擬機器擴展集的公用 IP 位址設定為 Azure Cosmos DB 資料庫帳戶的其中一個允許 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="acc79-125">To configure the Azure Cosmos DB database account to allow access from virtual machines, public IP addresses of virtual machine and/or virtual machine scale set must be configured as one of the allowed IP addresses for your Azure Cosmos DB database account by [configuring the IP access control policy](#configure-ip-policy).</span></span> <span data-ttu-id="acc79-126">您可以在 Azure 入口網站中擷取虛擬機器的 IP 位址，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="acc79-126">You can retrieve IP addresses for virtual machines in the Azure portal, as shown in the following screenshot.</span></span>

![這個螢幕擷取畫面顯示 Azure 入口網站中所顯示虛擬機器的公用 IP 位址](./media/firewall-support/public-ip-addresses-dns.png)

<span data-ttu-id="acc79-128">當您將其他虛擬機器執行個體新增至群組時，它們即可自動存取您的 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="acc79-128">When you add additional virtual machine instances to the group, they are automatically provided access to your Azure Cosmos DB database account.</span></span>

## <a name="connections-from-the-internet"></a><span data-ttu-id="acc79-129">從網際網路的連接</span><span class="sxs-lookup"><span data-stu-id="acc79-129">Connections from the internet</span></span>
<span data-ttu-id="acc79-130">從網際網路上的電腦存取 Azure Cosmos DB 資料庫帳戶時，必須將電腦的用戶端 IP 位址或 IP 位址範圍新增至 Azure Cosmos DB 資料庫帳戶的允許 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="acc79-130">When you access an Azure Cosmos DB database account from a computer on the internet, the client IP address or IP address range of the machine must be added to the allowed list of IP address for the Azure Cosmos DB database account.</span></span> 

## <span data-ttu-id="acc79-131"><a id="configure-ip-policy"></a> 設定 IP 存取控制原則</span><span class="sxs-lookup"><span data-stu-id="acc79-131"><a id="configure-ip-policy"></a> Configuring the IP access control policy</span></span>
<span data-ttu-id="acc79-132">您可以在 Azure 入口網站中設定 IP 存取控制原則，也可以透過 [Azure CLI](cli-samples.md)、[Azure Powershell](powershell-samples.md) 或 [REST API](/rest/api/documentdb/)，以程式設計方式更新 `ipRangeFilter` 屬性來設定。</span><span class="sxs-lookup"><span data-stu-id="acc79-132">The IP access control policy can be set in the Azure portal, or programmatically through [Azure CLI](cli-samples.md), [Azure Powershell](powershell-samples.md), or the [REST API](/rest/api/documentdb/) by updating the `ipRangeFilter` property.</span></span> <span data-ttu-id="acc79-133">IP 位址/範圍必須以逗號分隔，而且不得包含任何空格。</span><span class="sxs-lookup"><span data-stu-id="acc79-133">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="acc79-134">範例："13.91.6.132,13.91.6.1/24"。</span><span class="sxs-lookup"><span data-stu-id="acc79-134">Example: "13.91.6.132,13.91.6.1/24".</span></span> <span data-ttu-id="acc79-135">透過這些方法更新資料庫帳戶時，請務必填入所有屬性，以避免重設為預設設定。</span><span class="sxs-lookup"><span data-stu-id="acc79-135">When updating your database account through these methods, be sure to populate all of the properties to prevent resetting to default settings.</span></span>

> [!NOTE]
> <span data-ttu-id="acc79-136">啟用 Azure Cosmos DB 資料庫帳戶的 IP 存取控制原則，即會封鎖所設定之允許 IP 位址範圍清單外部的電腦對您 Azure Cosmos DB 資料庫帳戶的所有存取。</span><span class="sxs-lookup"><span data-stu-id="acc79-136">By enabling an IP access control policy for your Azure Cosmos DB database account, all access to your Azure Cosmos DB database account from machines outside the configured allowed list of IP address ranges are blocked.</span></span> <span data-ttu-id="acc79-137">透過這個模型，也會封鎖從入口網站瀏覽資料平面作業，確保存取控制的完整性。</span><span class="sxs-lookup"><span data-stu-id="acc79-137">By virtue of this model, browsing the data plane operation from the portal will also be blocked to ensure the integrity of access control.</span></span>

<span data-ttu-id="acc79-138">為了簡化開發工作，Azure 入口網站可協助您識別用戶端電腦的 IP 並新增至允許清單，讓您電腦上執行的應用程式可以存取 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="acc79-138">To simplify development, the Azure portal helps you identify and add the IP of your client machine to the allowed list, so that apps running your machine can access the Azure Cosmos DB account.</span></span> <span data-ttu-id="acc79-139">請注意，此處的用戶端 IP 位址是由入口網站偵測到。</span><span class="sxs-lookup"><span data-stu-id="acc79-139">Note that the client IP address here is detected as seen by the portal.</span></span> <span data-ttu-id="acc79-140">它可能是您電腦的用戶端 IP 位址，但也可能是網路閘道的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="acc79-140">It may be the client IP address of your machine, but it could also be the IP address of your network gateway.</span></span> <span data-ttu-id="acc79-141">移至生產環境之前，別忘記移除它。</span><span class="sxs-lookup"><span data-stu-id="acc79-141">Do not forget to remove it before going to production.</span></span>

<span data-ttu-id="acc79-142">若要在 Azure 入口網站中設定 IP 存取控制原則，請瀏覽至 [Azure Cosmos DB 帳戶] 刀鋒視窗、按一下導覽功能表中的 [防火牆]，然後按一下 [開啟]</span><span class="sxs-lookup"><span data-stu-id="acc79-142">To set the IP access control policy in the Azure portal, navigate to the Azure Cosmos DB account blade, click **Firewall** in the navigation menu, then click **ON**</span></span> 

![顯示如何在 Azure 入口網站中開啟 [防火牆] 刀鋒視窗的螢幕擷取畫面](./media/firewall-support/azure-portal-firewall.png)

<span data-ttu-id="acc79-144">在新窗格中，指定 Azure 入口網站是否可以存取帳戶，並適當地新增其他地址和範圍，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="acc79-144">In the new pane, specify whether the Azure portal can access the account, and add other addresses and ranges as appropriate, then click **Save**.</span></span>  

> [!NOTE]
> <span data-ttu-id="acc79-145">當您啟用 IP 存取控制原則時，您必須加入您 Azure 入口網站的 IP 位址以維持存取權。</span><span class="sxs-lookup"><span data-stu-id="acc79-145">When you enable an IP access control policy, you need to add the IP address for the Azure portal to maintain access.</span></span> <span data-ttu-id="acc79-146">入口網站 IP 位址是：</span><span class="sxs-lookup"><span data-stu-id="acc79-146">The portal IP addresses are:</span></span>
> |<span data-ttu-id="acc79-147">區域</span><span class="sxs-lookup"><span data-stu-id="acc79-147">Region</span></span>|<span data-ttu-id="acc79-148">IP 位址</span><span class="sxs-lookup"><span data-stu-id="acc79-148">IP address</span></span>|
> |------|----------|
> |<span data-ttu-id="acc79-149">所有區域 (下面指定的區域除外)</span><span class="sxs-lookup"><span data-stu-id="acc79-149">All regions except those specified below</span></span>| <span data-ttu-id="acc79-150">104.42.195.92</span><span class="sxs-lookup"><span data-stu-id="acc79-150">104.42.195.92</span></span>|
> |<span data-ttu-id="acc79-151">德國</span><span class="sxs-lookup"><span data-stu-id="acc79-151">Germany</span></span>|<span data-ttu-id="acc79-152">51.4.229.218</span><span class="sxs-lookup"><span data-stu-id="acc79-152">51.4.229.218</span></span>|
> |<span data-ttu-id="acc79-153">中國</span><span class="sxs-lookup"><span data-stu-id="acc79-153">China</span></span>|<span data-ttu-id="acc79-154">139.217.8.252</span><span class="sxs-lookup"><span data-stu-id="acc79-154">139.217.8.252</span></span>|
> |<span data-ttu-id="acc79-155">美國政府亞利桑那州</span><span class="sxs-lookup"><span data-stu-id="acc79-155">US Gov Arizona</span></span>|<span data-ttu-id="acc79-156">52.244.48.71</span><span class="sxs-lookup"><span data-stu-id="acc79-156">52.244.48.71</span></span>|
>

![顯示如何在 Azure 入口網站中進行防火牆設定的螢幕擷取畫面](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-the-ip-access-control-policy"></a><span data-ttu-id="acc79-158">針對 IP 存取控制原則進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="acc79-158">Troubleshooting the IP access control policy</span></span>
### <a name="portal-operations"></a><span data-ttu-id="acc79-159">入口網站作業</span><span class="sxs-lookup"><span data-stu-id="acc79-159">Portal operations</span></span>
<span data-ttu-id="acc79-160">啟用 Azure Cosmos DB 資料庫帳戶的 IP 存取控制原則，即會封鎖所設定之允許 IP 位址範圍清單外部的電腦對您 Azure Cosmos DB 資料庫帳戶的所有存取。</span><span class="sxs-lookup"><span data-stu-id="acc79-160">By enabling an IP access control policy for your Azure Cosmos DB database account, all access to your Azure Cosmos DB database account from machines outside the configured allowed list of IP address ranges are blocked.</span></span> <span data-ttu-id="acc79-161">因此，如果您想要啟用資料層面作業，例如瀏覽集合和查詢文件，您需要在入口網站使用 [防火牆] 刀鋒視窗，明確允許存取 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="acc79-161">Therefore if you want to enable portal data plane operations like browsing collections and query documents, you need to explicitly allow Azure portal access using the **Firewall** blade in the portal.</span></span> 

![顯示如何允許存取 Azure 入口網站的螢幕擷取畫面](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a><span data-ttu-id="acc79-163">SDK & Rest API</span><span class="sxs-lookup"><span data-stu-id="acc79-163">SDK & Rest API</span></span>
<span data-ttu-id="acc79-164">基於安全性考量，如果從電腦透過 SDK 或 REST API 的存取不在允許清單上，則會傳回沒有其他詳細資料的一般「404 找不到」回應。</span><span class="sxs-lookup"><span data-stu-id="acc79-164">For security reasons, access via SDK or REST API from machines not on the allowed list will return a generic 404 Not Found response with no additional details.</span></span> <span data-ttu-id="acc79-165">請確認已針對您 Azure Cosmos DB 資料庫帳戶設定的 IP 允許清單，以確保會將正確的原則組態套用至您的 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="acc79-165">Please verify the IP allowed list configured for your Azure Cosmos DB database account to ensure the correct policy configuration is applied to your Azure Cosmos DB database account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acc79-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acc79-166">Next steps</span></span>
<span data-ttu-id="acc79-167">如需網路相關效能秘訣的相關資訊，請參閱[效能秘訣](performance-tips.md)。</span><span class="sxs-lookup"><span data-stu-id="acc79-167">For information about network related performance tips, see [Performance tips](performance-tips.md).</span></span>

