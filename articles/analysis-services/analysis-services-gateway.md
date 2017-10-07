---
title: "aaaOn 內部部署資料閘道 |Microsoft 文件"
description: "如果您在 Azure 中的 Analysis Services 伺服器將連線 tooon 內部部署資料來源，必須在內部部署閘道。"
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
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="6ae7b-103">使用 Azure 的內部部署資料閘道連接 tooon 內部部署資料來源</span><span class="sxs-lookup"><span data-stu-id="6ae7b-103">Connecting tooon-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="6ae7b-104">hello 在內部部署資料閘道作為橋接器，提供在內部部署資料來源與 hello 雲端中的您 Azure Analysis Services 伺服器之間的安全資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-104">hello on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in hello cloud.</span></span> <span data-ttu-id="6ae7b-105">在多個 Azure Analysis Services 中的伺服器 hello 加法 tooworking 相同的區域，hello hello 閘道最新版本也可以搭配 Azure 邏輯應用程式、 Power BI、 電源應用程式和 Microsoft Flow。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-105">In addition tooworking with multiple Azure Analysis Services servers in hello same region, hello latest version of hello gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="6ae7b-106">您可以將多個服務在 hello 與單一閘道相同的區域。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-106">You can associate multiple services in hello same region with a single gateway.</span></span> 

 <span data-ttu-id="6ae7b-107">Azure Analysis Services 需要在 hello 閘道資源相同的區域。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-107">Azure Analysis Services requires a gateway resource in hello same region.</span></span> <span data-ttu-id="6ae7b-108">例如，如果您有 Azure Analysis Services 伺服器 hello 美國東部 2 區域中，您會需要 hello 美國東部 2 區域中的閘道資源。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-108">For example, if you have Azure Analysis Services servers in hello East US 2 region, you need a gateway resource in hello East US 2 region.</span></span> <span data-ttu-id="6ae7b-109">美國東部 2 中的多部伺服器可以使用 hello 相同閘道器。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-109">Multiple servers in East US 2 can use hello same gateway.</span></span>

<span data-ttu-id="6ae7b-110">讓安裝程式以 hello 閘道 hello 第一次是四部分的程序：</span><span class="sxs-lookup"><span data-stu-id="6ae7b-110">Getting setup with hello gateway hello first time is a four-part process:</span></span>

- <span data-ttu-id="6ae7b-111">**下載並執行安裝程式** - 這個步驟會在您組織中的電腦上安裝閘道服務。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="6ae7b-112">**註冊您的閘道**-在此步驟中，您指定的名稱和復原您的閘道金鑰，然後選取區域，以 hello 閘道器雲端服務中註冊您的閘道。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with hello Gateway Cloud Service.</span></span>

- <span data-ttu-id="6ae7b-113">**在 Azure 中建立閘道資源** - 在此步驟中，您會在您的 Azure 訂用帳戶中建立閘道資源。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="6ae7b-114">**連接您的伺服器 tooyour 閘道資源**-一旦您訂用帳戶中有閘道資源，您就可以開始連接伺服器 tooit。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-114">**Connect your servers tooyour gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers tooit.</span></span>

<span data-ttu-id="6ae7b-115">訂用帳戶設定閘道資源之後，您可以連接多部伺服器和其他服務 tooit。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services tooit.</span></span> <span data-ttu-id="6ae7b-116">您只需要 tooinstall 不同的閘道，並建立其他閘道資源，如果您的伺服器或其他服務在不同的區域。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-116">You only need tooinstall a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="6ae7b-117">tooget 立即，請參閱[安裝和設定內部部署資料閘道](analysis-services-gateway-install.md)。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-117">tooget started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="6ae7b-118"><a name="how-it-works"> </a>運作方式</span><span class="sxs-lookup"><span data-stu-id="6ae7b-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="6ae7b-119">您的電腦安裝在組織中的 hello 閘道會當做 Windows 服務，來執行**在內部部署資料閘道**。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-119">hello gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="6ae7b-120">這個本機服務已向 hello 透過 Azure 服務匯流排閘道器雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-120">This local service is registered with hello Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="6ae7b-121">您接著可為您的 Azure 訂用帳戶建立閘道資源 (閘道雲端服務)。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="6ae7b-122">您 Azure 的 Analysis Services 伺服器接著會連接 tooyour 閘道資源。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-122">Your Azure Analysis Services servers are then connected tooyour gateway resource.</span></span> <span data-ttu-id="6ae7b-123">當您伺服器需要 tooconnect tooyour 模型內部的查詢或處理資料來源時，查詢和資料流量會周遊 hello 閘道資源時，Azure 服務匯流排，hello 本機內部部署資料閘道服務，以及您的資料來源。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-123">When models on your server need tooconnect tooyour on-premises data sources for queries or processing, a query and data flow traverses hello gateway resource, Azure Service Bus, hello local on-premises data gateway service, and your data sources.</span></span> 

![運作方式](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="6ae7b-125">查詢和資料流程：</span><span class="sxs-lookup"><span data-stu-id="6ae7b-125">Queries and data flow:</span></span>

1. <span data-ttu-id="6ae7b-126">Hello 雲端服務所使用的認證加密的 hello hello 在內部部署資料來源建立查詢。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-126">A query is created by hello cloud service with hello encrypted credentials for hello on-premises data source.</span></span> <span data-ttu-id="6ae7b-127">然後已傳送嗨閘道 tooprocess tooa 佇列。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-127">It's then sent tooa queue for hello gateway tooprocess.</span></span>
2. <span data-ttu-id="6ae7b-128">hello 閘道器雲端服務會分析 hello 查詢，並將推送 hello 要求 toohello [Azure 服務匯流排](https://azure.microsoft.com/documentation/services/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-128">hello gateway cloud service analyzes hello query and pushes hello request toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="6ae7b-129">hello 在內部部署資料閘道會輪詢 hello 適用於 Azure 服務匯流排擱置的要求。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-129">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="6ae7b-130">hello 閘道取得 hello 查詢、 解密 hello 認證，並利用這些認證連接 toohello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-130">hello gateway gets hello query, decrypts hello credentials, and connects toohello data sources with those credentials.</span></span>
5. <span data-ttu-id="6ae7b-131">hello 閘道會傳送 hello 查詢 toohello 資料來源執行。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-131">hello gateway sends hello query toohello data source for execution.</span></span>
6. <span data-ttu-id="6ae7b-132">hello 結果會傳送 hello 資料來源，回復 toohello 閘道，然後拖曳 hello 雲端服務和您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-132">hello results are sent from hello data source, back toohello gateway, and then onto hello cloud service and your server.</span></span>

## <span data-ttu-id="6ae7b-133"><a name="windows-service-account"> </a>Windows 服務帳戶</span><span class="sxs-lookup"><span data-stu-id="6ae7b-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="6ae7b-134">hello 在內部部署資料閘道已設定的 toouse *NT SERVICE\PBIEgwService* hello Windows 服務登入認證。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-134">hello on-premises data gateway is configured toouse *NT SERVICE\PBIEgwService* for hello Windows service logon credential.</span></span> <span data-ttu-id="6ae7b-135">根據預設，其具有作為服務; hello 登入的權限hello 在內容中您要安裝 hello 閘道的 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-135">By default, it has hello right of Logon as a service; in hello context of hello machine that you are installing hello gateway on.</span></span> <span data-ttu-id="6ae7b-136">此認證不是 hello 相同的帳戶使用 tooconnect tooon 內部部署資料來源或您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-136">This credential is not hello same account used tooconnect tooon-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="6ae7b-137">如果您遇到的問題與您的 proxy 伺服器，因為 tooauthentication，您可能會想的 toochange hello Windows 服務帳戶 tooa 網域使用者或受管理服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-137">If you encounter issues with your proxy server due tooauthentication, you may want toochange hello Windows service account tooa domain user or managed service account.</span></span>

## <span data-ttu-id="6ae7b-138"><a name="ports"></a>連接埠</span><span class="sxs-lookup"><span data-stu-id="6ae7b-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="6ae7b-139">hello 閘道建立服務匯流排的輸出連線 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-139">hello gateway creates an outbound connection tooAzure Service Bus.</span></span> <span data-ttu-id="6ae7b-140">閘道會與下列輸出連接埠進行通訊︰TCP 443 (預設)、5671、5672、9350 到 9354。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="6ae7b-141">hello 閘道不需要輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-141">hello gateway does not require inbound ports.</span></span>

<span data-ttu-id="6ae7b-142">我們建議您在防火牆中的資料區域的白名單 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-142">We recommend you whitelist hello IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="6ae7b-143">您可以下載 hello [Microsoft Azure Datacenter IP 清單](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-143">You can download hello [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="6ae7b-144">此清單每週更新。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="6ae7b-145">hello hello Azure Datacenter IP 清單中列出的 IP 位址是以 CIDR 標記法。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-145">hello IP Addresses listed in hello Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="6ae7b-146">例如，10.0.0.0/24 並非 10.0.0.0 到 10.0.0.24。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="6ae7b-147">深入了解 hello [CIDR 標記法](http://whatismyipaddress.com/cidr)。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-147">Learn more about hello [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="6ae7b-148">hello 如下 hello 閘道所使用的 hello 完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-148">hello following are hello fully qualified domain names used by hello gateway.</span></span>

| <span data-ttu-id="6ae7b-149">網域名稱</span><span class="sxs-lookup"><span data-stu-id="6ae7b-149">Domain names</span></span> | <span data-ttu-id="6ae7b-150">輸出連接埠</span><span class="sxs-lookup"><span data-stu-id="6ae7b-150">Outbound ports</span></span> | <span data-ttu-id="6ae7b-151">說明</span><span class="sxs-lookup"><span data-stu-id="6ae7b-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ae7b-152">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="6ae7b-152">*.powerbi.com</span></span> |<span data-ttu-id="6ae7b-153">80</span><span class="sxs-lookup"><span data-stu-id="6ae7b-153">80</span></span> |<span data-ttu-id="6ae7b-154">Toodownload hello 安裝程式會使用 HTTP。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-154">HTTP used toodownload hello installer.</span></span> |
| <span data-ttu-id="6ae7b-155">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="6ae7b-155">*.powerbi.com</span></span> |<span data-ttu-id="6ae7b-156">443</span><span class="sxs-lookup"><span data-stu-id="6ae7b-156">443</span></span> |<span data-ttu-id="6ae7b-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6ae7b-157">HTTPS</span></span> |
| <span data-ttu-id="6ae7b-158">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="6ae7b-158">*.analysis.windows.net</span></span> |<span data-ttu-id="6ae7b-159">443</span><span class="sxs-lookup"><span data-stu-id="6ae7b-159">443</span></span> |<span data-ttu-id="6ae7b-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6ae7b-160">HTTPS</span></span> |
| <span data-ttu-id="6ae7b-161">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="6ae7b-161">*.login.windows.net</span></span> |<span data-ttu-id="6ae7b-162">443</span><span class="sxs-lookup"><span data-stu-id="6ae7b-162">443</span></span> |<span data-ttu-id="6ae7b-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6ae7b-163">HTTPS</span></span> |
| <span data-ttu-id="6ae7b-164">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="6ae7b-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="6ae7b-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="6ae7b-165">5671-5672</span></span> |<span data-ttu-id="6ae7b-166">進階訊息佇列通訊協定 (AMQP)</span><span class="sxs-lookup"><span data-stu-id="6ae7b-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="6ae7b-167">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="6ae7b-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="6ae7b-168">443、9350-9354</span><span class="sxs-lookup"><span data-stu-id="6ae7b-168">443, 9350-9354</span></span> |<span data-ttu-id="6ae7b-169">透過 TCP 之服務匯流排轉送上的接聽程式 (需要 443 才能取得「存取控制」權杖)</span><span class="sxs-lookup"><span data-stu-id="6ae7b-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="6ae7b-170">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="6ae7b-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="6ae7b-171">443</span><span class="sxs-lookup"><span data-stu-id="6ae7b-171">443</span></span> |<span data-ttu-id="6ae7b-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6ae7b-172">HTTPS</span></span> |
| <span data-ttu-id="6ae7b-173">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="6ae7b-173">*.core.windows.net</span></span> |<span data-ttu-id="6ae7b-174">443</span><span class="sxs-lookup"><span data-stu-id="6ae7b-174">443</span></span> |<span data-ttu-id="6ae7b-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6ae7b-175">HTTPS</span></span> |
| <span data-ttu-id="6ae7b-176">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6ae7b-176">login.microsoftonline.com</span></span> |<span data-ttu-id="6ae7b-177">443</span><span class="sxs-lookup"><span data-stu-id="6ae7b-177">443</span></span> |<span data-ttu-id="6ae7b-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6ae7b-178">HTTPS</span></span> |
| <span data-ttu-id="6ae7b-179">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="6ae7b-179">*.msftncsi.com</span></span> |<span data-ttu-id="6ae7b-180">443</span><span class="sxs-lookup"><span data-stu-id="6ae7b-180">443</span></span> |<span data-ttu-id="6ae7b-181">如果無法連到 hello Power BI 服務的 hello 閘道，請使用 tootest 網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-181">Used tootest internet connectivity if hello gateway is unreachable by hello Power BI service.</span></span> |
| <span data-ttu-id="6ae7b-182">*.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="6ae7b-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="6ae7b-183">443</span><span class="sxs-lookup"><span data-stu-id="6ae7b-183">443</span></span> |<span data-ttu-id="6ae7b-184">用於驗證 (視設定而定)。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="6ae7b-185"><a name="force-https"></a>強制使用 Azure 服務匯流排進行 HTTPS 通訊</span><span class="sxs-lookup"><span data-stu-id="6ae7b-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="6ae7b-186">您可以使用 HTTPS 而不是直接 TCP; 強制 hello 閘道 toocommunicate 搭配 Azure Service Bus不過，這樣做，可以大幅降低效能。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-186">You can force hello gateway toocommunicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="6ae7b-187">您可以修改 hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config*藉由變更 hello 值從檔案`AutoDetect`太`Https`。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-187">You can modify hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing hello value from `AutoDetect` too`Https`.</span></span> <span data-ttu-id="6ae7b-188">這個檔案通常位於 *C:\Program Files\On-premises data gateway*。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="6ae7b-189"><a name="faq"></a>常見問題集</span><span class="sxs-lookup"><span data-stu-id="6ae7b-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="6ae7b-190">一般</span><span class="sxs-lookup"><span data-stu-id="6ae7b-190">General</span></span>

<span data-ttu-id="6ae7b-191">**問：**： 我需要閘道 hello 雲端，例如 Azure SQL Database 中的資料來源嗎？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-191">**Q**: Do I need a gateway for data sources in hello cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="6ae7b-192">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-192">
**A**: No.</span></span> <span data-ttu-id="6ae7b-193">閘道正在連接只 tooon 內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-193">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="6ae7b-194">**問：**: hello 閘道是否有 toobe hello 做 hello 資料來源相同電腦上安裝？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-194">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="6ae7b-195">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-195">
**A**: No.</span></span> <span data-ttu-id="6ae7b-196">hello 閘道正在連接 toohello 資料來源使用所提供的 hello 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-196">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="6ae7b-197">Hello 閘道視為用戶端應用程式，這方面。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-197">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="6ae7b-198">hello 閘道只需要 hello 功能 tooconnect toohello 伺服器所提供名稱，通常在 hello 相同網路。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-198">hello gateway just needs hello capability tooconnect toohello server name that was provided, typically on hello same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="6ae7b-199">**問：**： 為什麼需要 toouse 工作或學校帳戶 toosign 中的？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-199">**Q**: Why do I need toouse a work or school account toosign in?</span></span> <br/><span data-ttu-id="6ae7b-200">
**A**： 您只能使用 Azure 的工作或學校帳戶，當您安裝 hello 在內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-200">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="6ae7b-201">登入帳戶會儲存在由 Azure Active Directory (Azure AD) 所管理的租用戶中。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6ae7b-202">通常，您的 Azure AD 帳戶的使用者主要名稱 (UPN) 符合 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-202">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="6ae7b-203">**問**︰我的認證儲存在哪裡？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="6ae7b-204">
**A**： 您輸入的資料來源的 hello 認證會加密並儲存在 hello 閘道器雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-204">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello Gateway Cloud Service.</span></span> <span data-ttu-id="6ae7b-205">hello 認證會在 hello 在內部部署資料閘道進行解密。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-205">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="6ae7b-206">**問**︰網路頻寬是否有任何需求？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="6ae7b-207">
**答**︰建議您的網路連線要有良好的輸送量。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="6ae7b-208">每個環境都不同，並傳送資料的 hello 數量會影響 hello 的結果。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-208">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="6ae7b-209">使用 ExpressRoute 有利於 tooguarantee 的內部部署與 hello Azure 資料中心之間的輸送量層級。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-209">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="6ae7b-210">您可以使用您的輸送量 hello 協力廠商工具 Azure Speed Test 應用程式 toohelp 量測計。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-210">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="6ae7b-211">**問：**: hello 延遲執行查詢 tooa 資料來源，從 hello 閘道是什麼？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-211">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="6ae7b-212">Hello 最佳架構為何？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-212">What is hello best architecture?</span></span> <br/><span data-ttu-id="6ae7b-213">
**A**: tooreduce 網路延遲，安裝 hello 閘道為盡可能關閉 toohello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-213">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="6ae7b-214">您可以安裝 hello 閘道 hello 實際的資料來源上，如果此相近延遲降至最低 hello 導入。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-214">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="6ae7b-215">太考慮 hello 資料中心。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-215">Consider hello datacenters too.</span></span> <span data-ttu-id="6ae7b-216">例如，如果您的服務會使用 hello 美國西部的資料中心，而且您的 Azure VM 中裝載 SQL Server，Azure VM 應該在 hello 美國西部太。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-216">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="6ae7b-217">此接近延遲降至最低，並避免 hello Azure VM 的輸出流量費用。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-217">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="6ae7b-218">**問：**： 的結果傳送後 toohello 雲端方式？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-218">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="6ae7b-219">
**A**: hello Azure Service Bus 透過傳送結果。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-219">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="6ae7b-220">**問：**： 是否有任何輸入的連線 toohello 閘道在 hello 雲端？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-220">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="6ae7b-221">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-221">
**A**: No.</span></span> <span data-ttu-id="6ae7b-222">hello 閘道會使用輸出連線 tooAzure Service Bus。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-222">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="6ae7b-223">**問**︰如果我封鎖輸出連線會如何？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="6ae7b-224">怎麼我需要 tooopen？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-224">What do I need tooopen?</span></span> <br/><span data-ttu-id="6ae7b-225">
**A**: hello 連接埠和主控件以 hello 閘道使用，請參閱。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-225">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="6ae7b-226">**問：**: hello 實際的 Windows 服務稱為？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-226">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="6ae7b-227">
**A**: hello 閘道在服務中，呼叫在內部部署資料閘道服務。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-227">
**A**: In Services, hello gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="6ae7b-228">**問：**： 可以 hello 使用 Azure Active Directory 帳戶來執行閘道 Windows 服務嗎？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-228">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="6ae7b-229">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-229">
**A**: No.</span></span> <span data-ttu-id="6ae7b-230">hello Windows 服務必須有有效的 Windows 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-230">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="6ae7b-231">根據預設，hello 服務會以 hello 服務 SID NT SERVICE\PBIEgwService 執行。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-231">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="6ae7b-232"><a name="high-availability"></a>高可用性和災害復原</span><span class="sxs-lookup"><span data-stu-id="6ae7b-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="6ae7b-233">**問**︰災害復原有哪些選項？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="6ae7b-234">
**A**： 您可以使用 hello 修復金鑰 toorestore 或移動閘道。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-234">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="6ae7b-235">當您安裝 hello 閘道時，指定 hello 修復金鑰。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-235">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="6ae7b-236">**問：**: hello hello 修復金鑰的優點為何？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-236">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="6ae7b-237">
**A**: hello 修復金鑰提供方式 toomigrate 或損毀狀況之後復原您的閘道設定。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-237">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="6ae7b-238"><a name="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="6ae7b-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="6ae7b-239">**問：**： 如何查看哪些查詢會傳送 toohello 在內部部署資料來源嗎？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-239">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="6ae7b-240">
**A**： 您可以啟用查詢追蹤，其中包括傳送嗨查詢。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-240">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="6ae7b-241">請記住 toochange 查詢後追蹤 toohello 完成疑難排解後的原始值。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-241">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="6ae7b-242">讓查詢追蹤保持開啟會產生較大的記錄。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="6ae7b-243">您也可以查看資料來源具備的工具是否有追蹤查詢。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="6ae7b-244">例如，您可以使用 SQL Server 和 Analysis Services 的擴充事件或 SQL Profiler。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="6ae7b-245">**問：**： 所在 hello 閘道記錄檔？</span><span class="sxs-lookup"><span data-stu-id="6ae7b-245">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="6ae7b-246">
**答**：請參閱本主題稍後的「記錄」。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="6ae7b-247"><a name="update"></a>更新 toohello 最新版本</span><span class="sxs-lookup"><span data-stu-id="6ae7b-247"><a name="update"></a>Update toohello latest version</span></span>

<span data-ttu-id="6ae7b-248">Hello 閘道器版本過期時，就會出現許多問題。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-248">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="6ae7b-249">良好一般做法，請確定您使用 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-249">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="6ae7b-250">如果您超過一個月或更久沒有更新 hello 閘道，您可能會考慮安裝 hello hello 閘道最新版本，並查看可否重現 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-250">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="6ae7b-251">錯誤： 無法 tooadd 使用者 toogroup。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-251">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="6ae7b-252">(-2147463168 PBIEgwService Performance Log Users)</span><span class="sxs-lookup"><span data-stu-id="6ae7b-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="6ae7b-253">如果您嘗試 tooinstall hello 閘道不支援的網域控制站上，您可能會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-253">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="6ae7b-254">請確定您部署的 hello 閘道不是網域控制站的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-254">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="6ae7b-255"><a name="logs"></a>記錄</span><span class="sxs-lookup"><span data-stu-id="6ae7b-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="6ae7b-256">進行疑難排解時，記錄檔是重要的資源。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="6ae7b-257">企業閘道服務記錄檔</span><span class="sxs-lookup"><span data-stu-id="6ae7b-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="6ae7b-258">組態記錄檔</span><span class="sxs-lookup"><span data-stu-id="6ae7b-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="6ae7b-259">事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="6ae7b-259">Event logs</span></span>

<span data-ttu-id="6ae7b-260">您可以找到 hello 下的資料管理閘道器和 PowerBIGateway 記錄**Application and Services Logs**。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-260">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="6ae7b-261"><a name="telemetry"></a>遙測</span><span class="sxs-lookup"><span data-stu-id="6ae7b-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="6ae7b-262">遙測可應用在監視和疑難排解上。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="6ae7b-263">依照預設</span><span class="sxs-lookup"><span data-stu-id="6ae7b-263">By default</span></span>

<span data-ttu-id="6ae7b-264">**tooturn 遙測**</span><span class="sxs-lookup"><span data-stu-id="6ae7b-264">**tooturn on telemetry**</span></span>

1.  <span data-ttu-id="6ae7b-265">請檢查 hello 在內部部署資料閘道用戶端電腦上的目錄 hello。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-265">Check hello On-premises data gateway client directory on hello computer.</span></span> <span data-ttu-id="6ae7b-266">此目錄通常是 **%systemdrive%\Program Files\內部部署資料閘道**。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="6ae7b-267">或者，您可以開啟 [服務] 主控台，並檢查 hello 路徑 tooexecutable: hello 在內部部署資料閘道服務的屬性。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-267">Or, you can open a Services console and check hello Path tooexecutable: A property of hello On-premises data gateway service.</span></span>
2.  <span data-ttu-id="6ae7b-268">在用戶端目錄中的 hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-268">In hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="6ae7b-269">變更 hello SendTelemetry 設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-269">Change hello SendTelemetry setting tootrue.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="6ae7b-270">儲存變更並重新啟動 hello Windows 服務： 在內部部署資料閘道服務。</span><span class="sxs-lookup"><span data-stu-id="6ae7b-270">Save your changes and restart hello Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="6ae7b-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ae7b-271">Next steps</span></span>
* [<span data-ttu-id="6ae7b-272"> Analysis Services</span><span class="sxs-lookup"><span data-stu-id="6ae7b-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="6ae7b-273">從 Azure Analysis Services 取得資料</span><span class="sxs-lookup"><span data-stu-id="6ae7b-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
