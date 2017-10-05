---
title: "使用現有的內部部署 Proxy 伺服器與 Azure AD | Microsoft Docs"
description: "涵蓋如何使用現有的內部部署 Proxy 伺服器。"
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
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="cb32f-103">使用現有的內部部署 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="cb32f-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="cb32f-104">本文說明如何設定 Azure Active Directory (Azure AD) 應用程式 Proxy 連接器以使用輸出 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cb32f-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="cb32f-105">它適用於具有現有 Proxy 之網路環境的客戶。</span><span class="sxs-lookup"><span data-stu-id="cb32f-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="cb32f-106">我們先來看看這些主要部署案例︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="cb32f-107">設定連接器以略過您的內部部署輸出 Proxy。</span><span class="sxs-lookup"><span data-stu-id="cb32f-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="cb32f-108">設定要使用輸出 Proxy 來存取 Azure AD 應用程式 Proxy 的連接器。</span><span class="sxs-lookup"><span data-stu-id="cb32f-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="cb32f-109">如需連接器運作方式的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="cb32f-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="cb32f-110">設定輸出 Proxy</span><span class="sxs-lookup"><span data-stu-id="cb32f-110">Configure the outbound proxy</span></span>

<span data-ttu-id="cb32f-111">如果您的環境中有輸出 Proxy，請使用具有適當權限的帳戶來設定輸出 Proxy。</span><span class="sxs-lookup"><span data-stu-id="cb32f-111">If you have an outbound proxy in your environment, use an account with appropriate permissions to configure the outbound proxy.</span></span> <span data-ttu-id="cb32f-112">安裝程式會在進行安裝的使用者內容中執行，因此您可以使用 Microsoft Edge 或其他網際網路瀏覽器來檢查組態。</span><span class="sxs-lookup"><span data-stu-id="cb32f-112">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="cb32f-113">若要在 Microsoft Edge 中設定 Proxy 的設定︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-113">To configure the proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="cb32f-114">移至 [設定] > [檢視進階設定] > [開啟 Proxy 設定] > [手動 Proxy 設定]。</span><span class="sxs-lookup"><span data-stu-id="cb32f-114">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="cb32f-115">將 [使用 Proxy 伺服器] 設定為 [開啟]，選取 [不要為近端 (內部網路) 位址使用 Proxy 伺服器] 核取方塊，然後變更位址和連接埠以反映您的本機 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cb32f-115">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="cb32f-116">填寫必要的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="cb32f-116">Fill in the necessary proxy settings.</span></span>

   ![Proxy 設定的對話方塊](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="cb32f-118">略過輸出 Proxy</span><span class="sxs-lookup"><span data-stu-id="cb32f-118">Bypass outbound proxies</span></span>

<span data-ttu-id="cb32f-119">連接器有會發出輸出要求的基礎作業系統元件。</span><span class="sxs-lookup"><span data-stu-id="cb32f-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="cb32f-120">這些元件會自動嘗試在網路上找出 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cb32f-120">These components automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="cb32f-121">然後使用 Web Proxy 自動探索 (WPAD) (如果已在環境中啟用)。</span><span class="sxs-lookup"><span data-stu-id="cb32f-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="cb32f-122">OS 元件會嘗試藉由對 wpad.domainsuffix 執行 DNS 查閱來尋找 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cb32f-122">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="cb32f-123">如果這在 DNS 中解決，則會對 wpad.dat 的 IP 位址提出 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="cb32f-123">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="cb32f-124">此要求會成為您環境中的 Proxy 組態指令碼。</span><span class="sxs-lookup"><span data-stu-id="cb32f-124">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="cb32f-125">連接器會使用這個指令碼來選取輸出 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cb32f-125">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="cb32f-126">不過，連接器流量可能會因為 Proxy 上所需的其他組態設定而仍然不會通過。</span><span class="sxs-lookup"><span data-stu-id="cb32f-126">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="cb32f-127">您可以將連接器設定為略過內部部署 Proxy，以確保它會使用與 Azure 服務的直接連線。</span><span class="sxs-lookup"><span data-stu-id="cb32f-127">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="cb32f-128">我們之所以建議這種方式 (若您的網路原則允許)，是因為這表示您有一個要維護的較少組態。</span><span class="sxs-lookup"><span data-stu-id="cb32f-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="cb32f-129">若要停用連接器的輸出 Proxy 使用，請編輯 C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config 檔案，並新增此程式碼範例中所示的 system.net 區段︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-129">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="cb32f-130">若要確保連接器更新程式服務也會略過 Proxy，對位於 C:\Program Files\Microsoft AAD App Proxy Connector Updater 的 ApplicationProxyConnectorUpdaterService.exe.config 檔案進行類似的變更。</span><span class="sxs-lookup"><span data-stu-id="cb32f-130">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="cb32f-131">請務必複製原始檔案，以免您需要還原為預設 .config 檔案。</span><span class="sxs-lookup"><span data-stu-id="cb32f-131">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="cb32f-132">使用輸出 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="cb32f-132">Use the outbound proxy server</span></span>

<span data-ttu-id="cb32f-133">某些環境會要求所有輸出流量通過輸出 Proxy，無一例外。</span><span class="sxs-lookup"><span data-stu-id="cb32f-133">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="cb32f-134">如此一來，略過 Proxy 不是選項。</span><span class="sxs-lookup"><span data-stu-id="cb32f-134">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="cb32f-135">您可以設定連接器流量通過輸出 Proxy，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="cb32f-135">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![設定讓連接器流量通過輸出 Proxy 來到達 Azure AD 應用程式 Proxy](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="cb32f-137">由於僅有輸出流量，因此您不需要設定透過防火牆來進行的輸入存取。</span><span class="sxs-lookup"><span data-stu-id="cb32f-137">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="cb32f-138">步驟 1：設定連接器和相關服務以通過輸出 Proxy</span><span class="sxs-lookup"><span data-stu-id="cb32f-138">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="cb32f-139">如先前所述，若 WPAD 在環境中啟用並正確地設定，連接器會自動探索輸出 Proxy 伺服器，並嘗試使用它。</span><span class="sxs-lookup"><span data-stu-id="cb32f-139">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="cb32f-140">不過，您可以明確地設定連接器以通過輸出 Proxy。</span><span class="sxs-lookup"><span data-stu-id="cb32f-140">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="cb32f-141">若要這樣做，請編輯 C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config 檔案，並新增此程式碼範例中所示的 system.net 區段。</span><span class="sxs-lookup"><span data-stu-id="cb32f-141">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="cb32f-142">變更 proxyserver:8080 以反映您的本機 Proxy 伺服器名稱或 IP 位址與其正在接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="cb32f-142">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="cb32f-143">接著，設定連接器更新程式服務來使用 Proxy，方法為對位於 C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config 的檔案進行類似變更。</span><span class="sxs-lookup"><span data-stu-id="cb32f-143">Next, configure the Connector Updater service to use the proxy by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="cb32f-144">步驟 2︰設定 Proxy 以允許來自連接器與相關服務的流量通過</span><span class="sxs-lookup"><span data-stu-id="cb32f-144">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="cb32f-145">在輸出 Proxy 有 4 個層面需要考量：</span><span class="sxs-lookup"><span data-stu-id="cb32f-145">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="cb32f-146">Proxy 輸出規則</span><span class="sxs-lookup"><span data-stu-id="cb32f-146">Proxy outbound rules</span></span>
* <span data-ttu-id="cb32f-147">Proxy 驗證</span><span class="sxs-lookup"><span data-stu-id="cb32f-147">Proxy authentication</span></span>
* <span data-ttu-id="cb32f-148">Proxy 連接埠</span><span class="sxs-lookup"><span data-stu-id="cb32f-148">Proxy ports</span></span>
* <span data-ttu-id="cb32f-149">SSL 審查</span><span class="sxs-lookup"><span data-stu-id="cb32f-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="cb32f-150">Proxy 輸出規則</span><span class="sxs-lookup"><span data-stu-id="cb32f-150">Proxy outbound rules</span></span>
<span data-ttu-id="cb32f-151">允許存取下列端點以取得連接器服務的存取權︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-151">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="cb32f-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="cb32f-152">*.msappproxy.net</span></span>
* <span data-ttu-id="cb32f-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="cb32f-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="cb32f-154">針對初始註冊，允許存取下列端點︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-154">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="cb32f-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="cb32f-155">login.windows.net</span></span>
* <span data-ttu-id="cb32f-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="cb32f-156">login.microsoftonline.com</span></span>

<span data-ttu-id="cb32f-157">如果您不允許 FQDN 連線且需要改為指定 IP 範圍，請使用下列選項：</span><span class="sxs-lookup"><span data-stu-id="cb32f-157">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="cb32f-158">允許連接器輸出存取所有目的地。</span><span class="sxs-lookup"><span data-stu-id="cb32f-158">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="cb32f-159">允許連接器輸出存取 [Azure 資料中心 IP 範圍](https://www.microsoft.com/en-gb/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="cb32f-159">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="cb32f-160">Azure 資料中心 IP 範圍清單在使用上的麻煩在於此清單是每週更新。</span><span class="sxs-lookup"><span data-stu-id="cb32f-160">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="cb32f-161">您必須制定程序，以確保存取規則會跟著更新。</span><span class="sxs-lookup"><span data-stu-id="cb32f-161">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="cb32f-162">Proxy 驗證</span><span class="sxs-lookup"><span data-stu-id="cb32f-162">Proxy authentication</span></span>

<span data-ttu-id="cb32f-163">目前不支援 Proxy 驗證。</span><span class="sxs-lookup"><span data-stu-id="cb32f-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="cb32f-164">目前的建議是允許連接器匿名存取網際網路目的地。</span><span class="sxs-lookup"><span data-stu-id="cb32f-164">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="cb32f-165">Proxy 連接埠</span><span class="sxs-lookup"><span data-stu-id="cb32f-165">Proxy ports</span></span>

<span data-ttu-id="cb32f-166">連接器可使用 CONNECT 方法進行輸出 SSL 型連線。</span><span class="sxs-lookup"><span data-stu-id="cb32f-166">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="cb32f-167">此方法基本上會透過輸出 Proxy 設定通道。</span><span class="sxs-lookup"><span data-stu-id="cb32f-167">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="cb32f-168">設定 Proxy 伺服器以允許連接埠 443 和 80 通道。</span><span class="sxs-lookup"><span data-stu-id="cb32f-168">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="cb32f-169">當服務匯流排在 HTTPS 上執行時，它會使用連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="cb32f-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="cb32f-170">不過，根據預設，服務匯流排會嘗試導向 TCP 連線，且僅在直接連線失敗時，才會改為使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="cb32f-170">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="cb32f-171">若要確認服務匯流排流量也會傳送輸出 Proxy 伺服器，請確定連接器無法直接連接到連接埠 9350、9352 和 5671 的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="cb32f-171">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="cb32f-172">SSL 審查</span><span class="sxs-lookup"><span data-stu-id="cb32f-172">SSL inspection</span></span>
<span data-ttu-id="cb32f-173">請勿對連接器流量使用 SSL 審查，因為這樣會導致連接器流量發生問題。</span><span class="sxs-lookup"><span data-stu-id="cb32f-173">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="cb32f-174">針對連接器 Proxy 問題和服務連線問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="cb32f-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="cb32f-175">現在您應該會看到所有的流量通過 Proxy。</span><span class="sxs-lookup"><span data-stu-id="cb32f-175">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="cb32f-176">如果您有問題，下列疑難排解資訊應該會有幫助。</span><span class="sxs-lookup"><span data-stu-id="cb32f-176">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="cb32f-177">找出連接器連線問題並進行疑難排解的最佳方式，是在啟動連接器服務時，在連接器服務上進行網路擷取。</span><span class="sxs-lookup"><span data-stu-id="cb32f-177">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="cb32f-178">這可能是令人怯步的工作，因此讓我們看看關於擷取及篩選網路追蹤的快速提示。</span><span class="sxs-lookup"><span data-stu-id="cb32f-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="cb32f-179">您可以使用您選擇的監視工具。</span><span class="sxs-lookup"><span data-stu-id="cb32f-179">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="cb32f-180">基於本文的目的，我們使用了 Microsoft Network Monitor 3.4。</span><span class="sxs-lookup"><span data-stu-id="cb32f-180">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="cb32f-181">您可以[從 Microsoft 下載](https://www.microsoft.com/download/details.aspx?id=4865)。</span><span class="sxs-lookup"><span data-stu-id="cb32f-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="cb32f-182">我們在後續章節所使用的範例與篩選器僅限網路監視器，但這些原則可以套用到任何分析工具。</span><span class="sxs-lookup"><span data-stu-id="cb32f-182">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="cb32f-183">使用網路監視器進行擷取</span><span class="sxs-lookup"><span data-stu-id="cb32f-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="cb32f-184">若要開始擷取︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-184">To start a capture:</span></span>

1. <span data-ttu-id="cb32f-185">開啟網路監視器，並按一下 [新增擷取]。</span><span class="sxs-lookup"><span data-stu-id="cb32f-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="cb32f-186">按一下 [啟動] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb32f-186">Click the **Start** button.</span></span>

   ![網路監視器視窗](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="cb32f-188">完成擷取之後，按一下 [停止] 按鈕予以結束。</span><span class="sxs-lookup"><span data-stu-id="cb32f-188">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="cb32f-189">擷取連接器流量</span><span class="sxs-lookup"><span data-stu-id="cb32f-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="cb32f-190">如需初始的疑難排解，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-190">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="cb32f-191">從 services.msc 停止 Azure AD 應用程式 Proxy 連接器服務。</span><span class="sxs-lookup"><span data-stu-id="cb32f-191">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="cb32f-192">啟動網路擷取。</span><span class="sxs-lookup"><span data-stu-id="cb32f-192">Start the network capture.</span></span>
3. <span data-ttu-id="cb32f-193">啟動 Azure AD 應用程式 Proxy 連接器服務。</span><span class="sxs-lookup"><span data-stu-id="cb32f-193">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="cb32f-194">停止網路擷取。</span><span class="sxs-lookup"><span data-stu-id="cb32f-194">Stop the network capture.</span></span>

   ![services.msc 中的 Azure AD 應用程式 Proxy 連接器服務](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="cb32f-196">查看連接器對 Proxy 伺服器的要求</span><span class="sxs-lookup"><span data-stu-id="cb32f-196">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="cb32f-197">現在，您有網路擷取，準備好要進行篩選。</span><span class="sxs-lookup"><span data-stu-id="cb32f-197">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="cb32f-198">查看追蹤的關鍵在於了解如何篩選擷取。</span><span class="sxs-lookup"><span data-stu-id="cb32f-198">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="cb32f-199">其中一個篩選條件如下所示 (其中 8080 是 Proxy 服務連接埠)︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-199">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="cb32f-200">**(http.Request or http.Response) and tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="cb32f-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="cb32f-201">如果您在 [顯示篩選器] 視窗中輸入此篩選器並選取 [套用]，它會根據篩選條件篩選擷取的流量。</span><span class="sxs-lookup"><span data-stu-id="cb32f-201">If you enter this filter in the **Display Filter** window and select **Apply**, it filters the captured traffic based on the filter.</span></span>

<span data-ttu-id="cb32f-202">上述篩選條件只會顯示 HTTP 要求和往返 Proxy 連接埠的回應。</span><span class="sxs-lookup"><span data-stu-id="cb32f-202">The preceding filter shows just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="cb32f-203">針對連接器設定為使用 Proxy 伺服器的連接器啟動，篩選條件會顯示如下︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-203">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![篩選之 HTTP 要求和回應的範例清單](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="cb32f-205">您現在要特別尋找顯示與 Proxy 伺服器通訊的 CONNECT 要求。</span><span class="sxs-lookup"><span data-stu-id="cb32f-205">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="cb32f-206">成功時，您會收到 HTTP OK (200) 回應。</span><span class="sxs-lookup"><span data-stu-id="cb32f-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="cb32f-207">如果您看到其他回應碼，例如 407 或 502，則表示 Proxy 需要驗證或由於某些其他原因不允許流量。</span><span class="sxs-lookup"><span data-stu-id="cb32f-207">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="cb32f-208">此時您會與您的 Proxy 伺服器支援團隊合作。</span><span class="sxs-lookup"><span data-stu-id="cb32f-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="cb32f-209">識別失敗的 TCP 連線嘗試</span><span class="sxs-lookup"><span data-stu-id="cb32f-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="cb32f-210">您可能感興趣的其他常見案例是當連接器嘗試直接連線但是失敗。</span><span class="sxs-lookup"><span data-stu-id="cb32f-210">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="cb32f-211">另一個可協助您更容易找出這個問題的網路監視器篩選條件是︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-211">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="cb32f-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="cb32f-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="cb32f-213">SYN 封包是傳送到建立 TCP 連線的第一個封包。</span><span class="sxs-lookup"><span data-stu-id="cb32f-213">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="cb32f-214">如果此封包未傳回回應，則會重新嘗試 SYN。</span><span class="sxs-lookup"><span data-stu-id="cb32f-214">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="cb32f-215">您可以使用上述篩選條件來查看任何重新傳輸的 SYN。</span><span class="sxs-lookup"><span data-stu-id="cb32f-215">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="cb32f-216">然後，您可以檢查這些 SYN 是否對應至任何與連接器相關的流量。</span><span class="sxs-lookup"><span data-stu-id="cb32f-216">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="cb32f-217">下列範例會示範失敗的服務匯流排連接埠 9352 連線嘗試︰</span><span class="sxs-lookup"><span data-stu-id="cb32f-217">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![失敗連線嘗試的範例回應](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="cb32f-219">如果您看到類似上述的回應，則表示連接器嘗試直接與 Azure 服務匯流排服務通訊。</span><span class="sxs-lookup"><span data-stu-id="cb32f-219">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="cb32f-220">如果您希望該連接器直接連線至 Azure 服務，則此回應清楚表示您有網路或防火牆問題。</span><span class="sxs-lookup"><span data-stu-id="cb32f-220">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="cb32f-221">如果您已設定為使用 Proxy 伺服器，此回應可能表示服務匯流排在改為嘗試透過 HTTPS 連線之前，會先嘗試直接 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="cb32f-221">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="cb32f-222">網路追蹤分析並非適合每個人。</span><span class="sxs-lookup"><span data-stu-id="cb32f-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="cb32f-223">但它會是可用來快速取得您網路運作情況相關資訊的寶貴工具。</span><span class="sxs-lookup"><span data-stu-id="cb32f-223">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="cb32f-224">如果您繼續遭遇連接器連線問題，請向我們的支援小組建立票證。</span><span class="sxs-lookup"><span data-stu-id="cb32f-224">If you continue to struggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="cb32f-225">該小組能協助您進行進一步疑難排解。</span><span class="sxs-lookup"><span data-stu-id="cb32f-225">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="cb32f-226">如需有關解決應用程式 Proxy 連接器錯誤的相關資訊，請參閱[疑難排解應用程式 Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot)。</span><span class="sxs-lookup"><span data-stu-id="cb32f-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb32f-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb32f-227">Next steps</span></span>

[<span data-ttu-id="cb32f-228">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="cb32f-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="cb32f-229">
[如何以無訊息方式安裝 Azure AD 應用程式 Proxy 連接器](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="cb32f-229">
[How to silently install the Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
