---
title: "內部部署資料閘道 | Microsoft Docs"
description: "如果 Azure 中的 Analysis Services 伺服器會連接到內部部署資料來源，則需要一個內部部署閘道。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: 514b5404e8cbfa0baa657eb41736e20cad502638
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connecting-to-on-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="ce70a-103">透過 Azure 內部部署資料閘道連線至內部部署資料來源</span><span class="sxs-lookup"><span data-stu-id="ce70a-103">Connecting to on-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="ce70a-104">內部部署資料閘道的角色如同橋接器，在內部部署資料來源和雲端中的 Azure Analysis Services 伺服器之間提供安全的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="ce70a-104">The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in the cloud.</span></span> <span data-ttu-id="ce70a-105">除了搭配相同區域中的多部 Azure Analysis Services 伺服器運作，最新版的閘道也可以搭配 Azure Logic Apps、Power BI、Power Apps 和 Microsoft Flow運作。</span><span class="sxs-lookup"><span data-stu-id="ce70a-105">In addition to working with multiple Azure Analysis Services servers in the same region, the latest version of the gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="ce70a-106">您可以讓相同區域中的多項服務與單一閘道建立關聯。</span><span class="sxs-lookup"><span data-stu-id="ce70a-106">You can associate multiple services in the same region with a single gateway.</span></span> 

 <span data-ttu-id="ce70a-107">Azure Analysis Services 需要相同區域中的閘道資源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-107">Azure Analysis Services requires a gateway resource in the same region.</span></span> <span data-ttu-id="ce70a-108">例如，如果您在美國東部 2 區域中有 Azure Analysis Services 伺服器，您就需要美國東部 2 區域中的閘道資源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-108">For example, if you have Azure Analysis Services servers in the East US 2 region, you need a gateway resource in the East US 2 region.</span></span> <span data-ttu-id="ce70a-109">美國東部 2 中的多部伺服器可以使用相同的閘道。</span><span class="sxs-lookup"><span data-stu-id="ce70a-109">Multiple servers in East US 2 can use the same gateway.</span></span>

<span data-ttu-id="ce70a-110">第一次設定閘道的程序有四部分：</span><span class="sxs-lookup"><span data-stu-id="ce70a-110">Getting setup with the gateway the first time is a four-part process:</span></span>

- <span data-ttu-id="ce70a-111">**下載並執行安裝程式** - 這個步驟會在您組織中的電腦上安裝閘道服務。</span><span class="sxs-lookup"><span data-stu-id="ce70a-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="ce70a-112">**註冊您的閘道** - 在此步驟中，您會為您的閘道指定名稱和復原金鑰，然後選取區域，並且向閘道雲端服務註冊您的閘道。</span><span class="sxs-lookup"><span data-stu-id="ce70a-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with the Gateway Cloud Service.</span></span>

- <span data-ttu-id="ce70a-113">**在 Azure 中建立閘道資源** - 在此步驟中，您會在您的 Azure 訂用帳戶中建立閘道資源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="ce70a-114">**將您的伺服器連線到閘道資源** - 您的訂用帳戶中一旦有閘道資源，您就可以開始將您的伺服器連線到它。</span><span class="sxs-lookup"><span data-stu-id="ce70a-114">**Connect your servers to your gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers to it.</span></span>

<span data-ttu-id="ce70a-115">為您的訂用帳戶設定閘道資源後，您就可以將多部伺服器和其他服務連線到它。</span><span class="sxs-lookup"><span data-stu-id="ce70a-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services to it.</span></span> <span data-ttu-id="ce70a-116">如果您在不同的區域中有伺服器或其他服務，您只需要安裝不同的閘道，並建立其他閘道資源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-116">You only need to install a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="ce70a-117">若要立即開始，請參閱[安裝及設定內部部署資料閘道](analysis-services-gateway-install.md)。</span><span class="sxs-lookup"><span data-stu-id="ce70a-117">To get started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="ce70a-118"><a name="how-it-works"> </a>運作方式</span><span class="sxs-lookup"><span data-stu-id="ce70a-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="ce70a-119">您在組織的電腦上安裝的閘道會以 Windows 服務 (**內部部署資料閘道**) 的形式執行。</span><span class="sxs-lookup"><span data-stu-id="ce70a-119">The gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="ce70a-120">此本機服務已透過 Azure 服務匯流排向閘道雲端服務註冊。</span><span class="sxs-lookup"><span data-stu-id="ce70a-120">This local service is registered with the Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="ce70a-121">您接著可為您的 Azure 訂用帳戶建立閘道資源 (閘道雲端服務)。</span><span class="sxs-lookup"><span data-stu-id="ce70a-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="ce70a-122">Azure Analysis Services 伺服器會接著連線至閘道資源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-122">Your Azure Analysis Services servers are then connected to your gateway resource.</span></span> <span data-ttu-id="ce70a-123">當您伺服器上的模型需要連線到內部部署資料來源進行查詢或處理時，查詢和資料流程會周遊閘道資源、Azure 服務匯流排、本機內部部署資料閘道服務以及您的資料來源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-123">When models on your server need to connect to your on-premises data sources for queries or processing, a query and data flow traverses the gateway resource, Azure Service Bus, the local on-premises data gateway service, and your data sources.</span></span> 

![運作方式](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="ce70a-125">查詢和資料流程：</span><span class="sxs-lookup"><span data-stu-id="ce70a-125">Queries and data flow:</span></span>

1. <span data-ttu-id="ce70a-126">雲端服務使用內部部署資料來源的加密認證建立查詢。</span><span class="sxs-lookup"><span data-stu-id="ce70a-126">A query is created by the cloud service with the encrypted credentials for the on-premises data source.</span></span> <span data-ttu-id="ce70a-127">查詢接著傳送至佇列供閘道處理。</span><span class="sxs-lookup"><span data-stu-id="ce70a-127">It's then sent to a queue for the gateway to process.</span></span>
2. <span data-ttu-id="ce70a-128">閘道雲端服務會分析該查詢，並將要求推送至 [Azure 服務匯流排](https://azure.microsoft.com/documentation/services/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="ce70a-128">The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="ce70a-129">內部部署資料閘道會輪詢 Azure 服務匯流排是否有待處理的要求。</span><span class="sxs-lookup"><span data-stu-id="ce70a-129">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="ce70a-130">閘道收到查詢、解密認證，並使用這些認證連接至資料來源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-130">The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.</span></span>
5. <span data-ttu-id="ce70a-131">閘道將查詢傳送至資料來源執行。</span><span class="sxs-lookup"><span data-stu-id="ce70a-131">The gateway sends the query to the data source for execution.</span></span>
6. <span data-ttu-id="ce70a-132">結果會從資料來源傳送回閘道，然後再到雲端服務和您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="ce70a-132">The results are sent from the data source, back to the gateway, and then onto the cloud service and your server.</span></span>

## <span data-ttu-id="ce70a-133"><a name="windows-service-account"> </a>Windows 服務帳戶</span><span class="sxs-lookup"><span data-stu-id="ce70a-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="ce70a-134">內部部署資料閘道設定為使用 *NT SERVICE\PBIEgwService* 做為 Windows 服務的登入認證。</span><span class="sxs-lookup"><span data-stu-id="ce70a-134">The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential.</span></span> <span data-ttu-id="ce70a-135">根據預設，它具有「以服務方式登入」的權限 (在您安裝閘道所在機器的環境中)。</span><span class="sxs-lookup"><span data-stu-id="ce70a-135">By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on.</span></span> <span data-ttu-id="ce70a-136">此認證不同於連接到內部部署資料來源使用的帳戶或您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce70a-136">This credential is not the same account used to connect to on-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="ce70a-137">如果您因為身分驗證面臨與 Proxy 服務器相關的問題，您可能需要將 Windows 服務帳戶變更為網域使用者或受管理的服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce70a-137">If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.</span></span>

## <span data-ttu-id="ce70a-138"><a name="ports"></a>連接埠</span><span class="sxs-lookup"><span data-stu-id="ce70a-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="ce70a-139">閘道會建立 Azure 服務匯流排的輸出連接。</span><span class="sxs-lookup"><span data-stu-id="ce70a-139">The gateway creates an outbound connection to Azure Service Bus.</span></span> <span data-ttu-id="ce70a-140">閘道會與下列輸出連接埠進行通訊︰TCP 443 (預設)、5671、5672、9350 到 9354。</span><span class="sxs-lookup"><span data-stu-id="ce70a-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="ce70a-141">閘道不需要輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="ce70a-141">The gateway does not require inbound ports.</span></span>

<span data-ttu-id="ce70a-142">建議您在防火牆中將您的資料區域 IP 位址列入白名單。</span><span class="sxs-lookup"><span data-stu-id="ce70a-142">We recommend you whitelist the IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="ce70a-143">您可以下載 [Microsoft Azure Datacenter IP 清單](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="ce70a-143">You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="ce70a-144">此清單每週更新。</span><span class="sxs-lookup"><span data-stu-id="ce70a-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="ce70a-145">Azure Datacenter IP 清單中列出的 IP 位址採用 CIDR 標記法。</span><span class="sxs-lookup"><span data-stu-id="ce70a-145">The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="ce70a-146">例如，10.0.0.0/24 並非 10.0.0.0 到 10.0.0.24。</span><span class="sxs-lookup"><span data-stu-id="ce70a-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="ce70a-147">深入了解 [CIDR 標記法](http://whatismyipaddress.com/cidr)。</span><span class="sxs-lookup"><span data-stu-id="ce70a-147">Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="ce70a-148">以下是閘道使用的完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ce70a-148">The following are the fully qualified domain names used by the gateway.</span></span>

| <span data-ttu-id="ce70a-149">網域名稱</span><span class="sxs-lookup"><span data-stu-id="ce70a-149">Domain names</span></span> | <span data-ttu-id="ce70a-150">輸出連接埠</span><span class="sxs-lookup"><span data-stu-id="ce70a-150">Outbound ports</span></span> | <span data-ttu-id="ce70a-151">說明</span><span class="sxs-lookup"><span data-stu-id="ce70a-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce70a-152">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="ce70a-152">*.powerbi.com</span></span> |<span data-ttu-id="ce70a-153">80</span><span class="sxs-lookup"><span data-stu-id="ce70a-153">80</span></span> |<span data-ttu-id="ce70a-154">用於下載安裝程式的 HTTP。</span><span class="sxs-lookup"><span data-stu-id="ce70a-154">HTTP used to download the installer.</span></span> |
| <span data-ttu-id="ce70a-155">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="ce70a-155">*.powerbi.com</span></span> |<span data-ttu-id="ce70a-156">443</span><span class="sxs-lookup"><span data-stu-id="ce70a-156">443</span></span> |<span data-ttu-id="ce70a-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ce70a-157">HTTPS</span></span> |
| <span data-ttu-id="ce70a-158">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="ce70a-158">*.analysis.windows.net</span></span> |<span data-ttu-id="ce70a-159">443</span><span class="sxs-lookup"><span data-stu-id="ce70a-159">443</span></span> |<span data-ttu-id="ce70a-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ce70a-160">HTTPS</span></span> |
| <span data-ttu-id="ce70a-161">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="ce70a-161">*.login.windows.net</span></span> |<span data-ttu-id="ce70a-162">443</span><span class="sxs-lookup"><span data-stu-id="ce70a-162">443</span></span> |<span data-ttu-id="ce70a-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ce70a-163">HTTPS</span></span> |
| <span data-ttu-id="ce70a-164">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="ce70a-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="ce70a-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="ce70a-165">5671-5672</span></span> |<span data-ttu-id="ce70a-166">進階訊息佇列通訊協定 (AMQP)</span><span class="sxs-lookup"><span data-stu-id="ce70a-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="ce70a-167">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="ce70a-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="ce70a-168">443、9350-9354</span><span class="sxs-lookup"><span data-stu-id="ce70a-168">443, 9350-9354</span></span> |<span data-ttu-id="ce70a-169">透過 TCP 之服務匯流排轉送上的接聽程式 (需要 443 才能取得「存取控制」權杖)</span><span class="sxs-lookup"><span data-stu-id="ce70a-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="ce70a-170">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="ce70a-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="ce70a-171">443</span><span class="sxs-lookup"><span data-stu-id="ce70a-171">443</span></span> |<span data-ttu-id="ce70a-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ce70a-172">HTTPS</span></span> |
| <span data-ttu-id="ce70a-173">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ce70a-173">*.core.windows.net</span></span> |<span data-ttu-id="ce70a-174">443</span><span class="sxs-lookup"><span data-stu-id="ce70a-174">443</span></span> |<span data-ttu-id="ce70a-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ce70a-175">HTTPS</span></span> |
| <span data-ttu-id="ce70a-176">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ce70a-176">login.microsoftonline.com</span></span> |<span data-ttu-id="ce70a-177">443</span><span class="sxs-lookup"><span data-stu-id="ce70a-177">443</span></span> |<span data-ttu-id="ce70a-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ce70a-178">HTTPS</span></span> |
| <span data-ttu-id="ce70a-179">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="ce70a-179">*.msftncsi.com</span></span> |<span data-ttu-id="ce70a-180">443</span><span class="sxs-lookup"><span data-stu-id="ce70a-180">443</span></span> |<span data-ttu-id="ce70a-181">如果 Power BI 服務無法連接至閘道，則用來測試網際網路連線能力。</span><span class="sxs-lookup"><span data-stu-id="ce70a-181">Used to test internet connectivity if the gateway is unreachable by the Power BI service.</span></span> |
| <span data-ttu-id="ce70a-182">*.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="ce70a-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="ce70a-183">443</span><span class="sxs-lookup"><span data-stu-id="ce70a-183">443</span></span> |<span data-ttu-id="ce70a-184">用於驗證 (視設定而定)。</span><span class="sxs-lookup"><span data-stu-id="ce70a-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="ce70a-185"><a name="force-https"></a>強制使用 Azure 服務匯流排進行 HTTPS 通訊</span><span class="sxs-lookup"><span data-stu-id="ce70a-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="ce70a-186">您可以強制閘道使用 HTTPS 取代直接 TCP 來與 Azure 服務匯流排通訊；但這樣會大幅降低效能。</span><span class="sxs-lookup"><span data-stu-id="ce70a-186">You can force the gateway to communicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="ce70a-187">您可以修改 *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* 檔案，方法是將值從 `AutoDetect` 變更為 `Https`。</span><span class="sxs-lookup"><span data-stu-id="ce70a-187">You can modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing the value from `AutoDetect` to `Https`.</span></span> <span data-ttu-id="ce70a-188">這個檔案通常位於 *C:\Program Files\On-premises data gateway*。</span><span class="sxs-lookup"><span data-stu-id="ce70a-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="ce70a-189"><a name="faq"></a>常見問題集</span><span class="sxs-lookup"><span data-stu-id="ce70a-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="ce70a-190">一般</span><span class="sxs-lookup"><span data-stu-id="ce70a-190">General</span></span>

<span data-ttu-id="ce70a-191">**問**︰我在雲端中的資料來源 (例如 Azure SQL Database) 是否需要閘道？</span><span class="sxs-lookup"><span data-stu-id="ce70a-191">**Q**: Do I need a gateway for data sources in the cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="ce70a-192">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="ce70a-192">
**A**: No.</span></span> <span data-ttu-id="ce70a-193">閘道只連接至內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-193">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="ce70a-194">**問**︰閘道必須安裝在與資料來源相同的電腦上嗎？</span><span class="sxs-lookup"><span data-stu-id="ce70a-194">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="ce70a-195">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="ce70a-195">
**A**: No.</span></span> <span data-ttu-id="ce70a-196">閘道會使用所提供的連線資訊連線至資料來源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-196">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="ce70a-197">在此請將閘道視為用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce70a-197">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="ce70a-198">閘道只需要能夠連線到所提供的伺服器名稱，通常是在相同網路上。</span><span class="sxs-lookup"><span data-stu-id="ce70a-198">The gateway just needs the capability to connect to the server name that was provided, typically on the same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="ce70a-199">**問︰**︰為何必須使用公司或學校帳戶進行登入？</span><span class="sxs-lookup"><span data-stu-id="ce70a-199">**Q**: Why do I need to use a work or school account to sign in?</span></span> <br/><span data-ttu-id="ce70a-200">
**答**︰安裝內部部署資料閘道時，您只能使用公司或學校的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce70a-200">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="ce70a-201">登入帳戶會儲存在由 Azure Active Directory (Azure AD) 所管理的租用戶中。</span><span class="sxs-lookup"><span data-stu-id="ce70a-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ce70a-202">Azure AD 帳戶的使用者主體名稱 (UPN) 通常會與電子郵件地址相符。</span><span class="sxs-lookup"><span data-stu-id="ce70a-202">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="ce70a-203">**問**︰我的認證儲存在哪裡？</span><span class="sxs-lookup"><span data-stu-id="ce70a-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="ce70a-204">
**答**：您針對資料來源輸入的認證會以加密方式儲存在閘道雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="ce70a-204">
**A**: The credentials that you enter for a data source are encrypted and stored in the Gateway Cloud Service.</span></span> <span data-ttu-id="ce70a-205">認證會在內部部署資料閘道進行解密。</span><span class="sxs-lookup"><span data-stu-id="ce70a-205">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="ce70a-206">**問**︰網路頻寬是否有任何需求？</span><span class="sxs-lookup"><span data-stu-id="ce70a-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="ce70a-207">
**答**︰建議您的網路連線要有良好的輸送量。</span><span class="sxs-lookup"><span data-stu-id="ce70a-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="ce70a-208">每個環境都是不同的，而且所傳送的資料量會影響結果。</span><span class="sxs-lookup"><span data-stu-id="ce70a-208">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="ce70a-209">使用 ExpressRoute 可以協助您確保在內部部署與 Azure 資料中心之間有一定的輸送量等級。</span><span class="sxs-lookup"><span data-stu-id="ce70a-209">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="ce70a-210">您可以使用第三方工具 Azure 速度測試應用程式，協助您量測輸送量。</span><span class="sxs-lookup"><span data-stu-id="ce70a-210">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="ce70a-211">**問**︰從閘道向資料來源執行查詢時的延遲為何？</span><span class="sxs-lookup"><span data-stu-id="ce70a-211">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="ce70a-212">最佳的架構為何？</span><span class="sxs-lookup"><span data-stu-id="ce70a-212">What is the best architecture?</span></span> <br/><span data-ttu-id="ce70a-213">
**答**：若要減少網路延遲，請盡可能靠近資料來源安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="ce70a-213">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="ce70a-214">如果您可以在實際的資料來源上安裝閘道，此鄰近程度就能將所產生的延遲降到最低。</span><span class="sxs-lookup"><span data-stu-id="ce70a-214">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="ce70a-215">請一併考量資料中心。</span><span class="sxs-lookup"><span data-stu-id="ce70a-215">Consider the datacenters too.</span></span> <span data-ttu-id="ce70a-216">例如，如果您的服務使用美國西部的資料中心，而您在 Azure VM 中裝載 SQL Server，Azure VM 也應該位於美國西部。</span><span class="sxs-lookup"><span data-stu-id="ce70a-216">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="ce70a-217">此鄰近程度能將延遲降到最低，並避免 Azure VM 的輸出費用。</span><span class="sxs-lookup"><span data-stu-id="ce70a-217">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="ce70a-218">**問**︰結果如何傳送回雲端？</span><span class="sxs-lookup"><span data-stu-id="ce70a-218">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="ce70a-219">
**答**︰結果會透過 Azure 服務匯流排傳送。</span><span class="sxs-lookup"><span data-stu-id="ce70a-219">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="ce70a-220">**問**︰是否有任何從雲端至閘道的輸入連線？</span><span class="sxs-lookup"><span data-stu-id="ce70a-220">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="ce70a-221">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="ce70a-221">
**A**: No.</span></span> <span data-ttu-id="ce70a-222">閘道使用連至 Azure 服務匯流排的輸出連接。</span><span class="sxs-lookup"><span data-stu-id="ce70a-222">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="ce70a-223">**問**︰如果我封鎖輸出連線會如何？</span><span class="sxs-lookup"><span data-stu-id="ce70a-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="ce70a-224">我需要開啟什麼嗎？</span><span class="sxs-lookup"><span data-stu-id="ce70a-224">What do I need to open?</span></span> <br/><span data-ttu-id="ce70a-225">
**答**：查看閘道使用的連接埠和主機。</span><span class="sxs-lookup"><span data-stu-id="ce70a-225">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="ce70a-226">**問**：實際的 Windows 服務名稱為何？</span><span class="sxs-lookup"><span data-stu-id="ce70a-226">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="ce70a-227">
**答**：在「服務」中，閘道稱為「內部部署資料閘道服務」。</span><span class="sxs-lookup"><span data-stu-id="ce70a-227">
**A**: In Services, the gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="ce70a-228">**問**︰閘道 Windows 服務可以使用 Azure Active Directory 帳戶執行嗎？</span><span class="sxs-lookup"><span data-stu-id="ce70a-228">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="ce70a-229">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="ce70a-229">
**A**: No.</span></span> <span data-ttu-id="ce70a-230">Windows 服務必須要有有效的 Windows 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce70a-230">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="ce70a-231">根據預設，此服務會使用服務 SID，NT SERVICE\PBIEgwService 執行。</span><span class="sxs-lookup"><span data-stu-id="ce70a-231">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="ce70a-232"><a name="high-availability"></a>高可用性和災害復原</span><span class="sxs-lookup"><span data-stu-id="ce70a-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="ce70a-233">**問**︰災害復原有哪些選項？</span><span class="sxs-lookup"><span data-stu-id="ce70a-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="ce70a-234">
**答**：您可以使用修復金鑰還原或移動閘道。</span><span class="sxs-lookup"><span data-stu-id="ce70a-234">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="ce70a-235">當您安裝閘道時，請指定修復金鑰。</span><span class="sxs-lookup"><span data-stu-id="ce70a-235">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="ce70a-236">**問**︰修復金鑰有什麼好處？</span><span class="sxs-lookup"><span data-stu-id="ce70a-236">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="ce70a-237">
**答**：修復金鑰可在災害發生後讓您有辦法移轉或復原閘道設定。</span><span class="sxs-lookup"><span data-stu-id="ce70a-237">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="ce70a-238"><a name="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="ce70a-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="ce70a-239">**問**︰如何查看有哪些查詢正要傳送至內部部署資料來源？</span><span class="sxs-lookup"><span data-stu-id="ce70a-239">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="ce70a-240">
**答**：您可以啟用查詢追蹤，其中包含要傳送的查詢。</span><span class="sxs-lookup"><span data-stu-id="ce70a-240">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="ce70a-241">完成疑難排解時，請務必將查詢追蹤變更回原始值。</span><span class="sxs-lookup"><span data-stu-id="ce70a-241">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="ce70a-242">讓查詢追蹤保持開啟會產生較大的記錄。</span><span class="sxs-lookup"><span data-stu-id="ce70a-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="ce70a-243">您也可以查看資料來源具備的工具是否有追蹤查詢。</span><span class="sxs-lookup"><span data-stu-id="ce70a-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="ce70a-244">例如，您可以使用 SQL Server 和 Analysis Services 的擴充事件或 SQL Profiler。</span><span class="sxs-lookup"><span data-stu-id="ce70a-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="ce70a-245">**問**︰閘道記錄在哪裡？</span><span class="sxs-lookup"><span data-stu-id="ce70a-245">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="ce70a-246">
**答**：請參閱本主題稍後的「記錄」。</span><span class="sxs-lookup"><span data-stu-id="ce70a-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="ce70a-247"><a name="update"></a>更新為最新版本</span><span class="sxs-lookup"><span data-stu-id="ce70a-247"><a name="update"></a>Update to the latest version</span></span>

<span data-ttu-id="ce70a-248">閘道版本過期時，可能會出現很多問題。</span><span class="sxs-lookup"><span data-stu-id="ce70a-248">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="ce70a-249">良好的一般作法是確實使用最新版本。</span><span class="sxs-lookup"><span data-stu-id="ce70a-249">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="ce70a-250">如果有一個月以上未更新閘道，您可以考慮安裝最新版的閘道，並看看是否能重現問題。</span><span class="sxs-lookup"><span data-stu-id="ce70a-250">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="ce70a-251">錯誤︰無法將使用者新增到群組。</span><span class="sxs-lookup"><span data-stu-id="ce70a-251">Error: Failed to add user to group.</span></span> <span data-ttu-id="ce70a-252">(-2147463168 PBIEgwService Performance Log Users)</span><span class="sxs-lookup"><span data-stu-id="ce70a-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="ce70a-253">如果您嘗試在不支援的網域控制站上安裝閘道，可能會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="ce70a-253">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="ce70a-254">請確定您是在非網域控制站的電腦上部署閘道。</span><span class="sxs-lookup"><span data-stu-id="ce70a-254">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="ce70a-255"><a name="logs"></a>記錄</span><span class="sxs-lookup"><span data-stu-id="ce70a-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="ce70a-256">進行疑難排解時，記錄檔是重要的資源。</span><span class="sxs-lookup"><span data-stu-id="ce70a-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="ce70a-257">企業閘道服務記錄檔</span><span class="sxs-lookup"><span data-stu-id="ce70a-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="ce70a-258">組態記錄檔</span><span class="sxs-lookup"><span data-stu-id="ce70a-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="ce70a-259">事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="ce70a-259">Event logs</span></span>

<span data-ttu-id="ce70a-260">您可以在 [應用程式及服務記錄] 底下找到資料管理閘道和 PowerBIGateway 記錄。</span><span class="sxs-lookup"><span data-stu-id="ce70a-260">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="ce70a-261"><a name="telemetry"></a>遙測</span><span class="sxs-lookup"><span data-stu-id="ce70a-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="ce70a-262">遙測可應用在監視和疑難排解上。</span><span class="sxs-lookup"><span data-stu-id="ce70a-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="ce70a-263">依照預設</span><span class="sxs-lookup"><span data-stu-id="ce70a-263">By default</span></span>

<span data-ttu-id="ce70a-264">**開啟遙測**</span><span class="sxs-lookup"><span data-stu-id="ce70a-264">**To turn on telemetry**</span></span>

1.  <span data-ttu-id="ce70a-265">檢查電腦上的內部部署資料閘道用戶端目錄。</span><span class="sxs-lookup"><span data-stu-id="ce70a-265">Check the On-premises data gateway client directory on the computer.</span></span> <span data-ttu-id="ce70a-266">此目錄通常是 **%systemdrive%\Program Files\內部部署資料閘道**。</span><span class="sxs-lookup"><span data-stu-id="ce70a-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="ce70a-267">或者，您可以開啟 [服務] 主控台並查看可執行檔的路徑：內部部署資料閘道服務的一個屬性。</span><span class="sxs-lookup"><span data-stu-id="ce70a-267">Or, you can open a Services console and check the Path to executable: A property of the On-premises data gateway service.</span></span>
2.  <span data-ttu-id="ce70a-268">在來自用戶端目錄的 Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config 檔案中，</span><span class="sxs-lookup"><span data-stu-id="ce70a-268">In the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="ce70a-269">將 SendTelemetry 設定變更為 true。</span><span class="sxs-lookup"><span data-stu-id="ce70a-269">Change the SendTelemetry setting to true.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="ce70a-270">儲存您的變更，然後重新啟動 Windows 服務：內部部署資料閘道服務。</span><span class="sxs-lookup"><span data-stu-id="ce70a-270">Save your changes and restart the Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="ce70a-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce70a-271">Next steps</span></span>
* [<span data-ttu-id="ce70a-272"> Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ce70a-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="ce70a-273">從 Azure Analysis Services 取得資料</span><span class="sxs-lookup"><span data-stu-id="ce70a-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
