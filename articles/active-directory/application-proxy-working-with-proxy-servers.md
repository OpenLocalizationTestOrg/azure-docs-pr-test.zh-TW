---
title: "aaaWork 與現有的內部 proxy 伺服器與 Azure AD |Microsoft 文件"
description: "涵蓋如何 toowork 與現有的內部 proxy 伺服器。"
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
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="6824f-103">使用現有的內部部署 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="6824f-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="6824f-104">這篇文章說明如何 tooconfigure Azure Active Directory (Azure AD) 應用程式 Proxy 連接器 toowork 與連出 proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6824f-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="6824f-105">它適用於具有現有 Proxy 之網路環境的客戶。</span><span class="sxs-lookup"><span data-stu-id="6824f-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="6824f-106">我們先來看看這些主要部署案例︰</span><span class="sxs-lookup"><span data-stu-id="6824f-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="6824f-107">設定連接器 toobypass 您在內部部署輸出 proxy。</span><span class="sxs-lookup"><span data-stu-id="6824f-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="6824f-108">設定連接器 toouse 連出 proxy tooaccess Azure AD Application Proxy。</span><span class="sxs-lookup"><span data-stu-id="6824f-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="6824f-109">如需連接器運作方式的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="6824f-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="6824f-110">設定 hello 連出 proxy</span><span class="sxs-lookup"><span data-stu-id="6824f-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="6824f-111">如果您的環境中有輸出 proxy，請使用適當的權限 tooconfigure hello 連出 proxy 使用的帳戶。</span><span class="sxs-lookup"><span data-stu-id="6824f-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="6824f-112">因為 hello 安裝程式會執行 hello 負責 hello 安裝 hello 使用者內容中，您可以使用 Microsoft Edge 或其他網際網路瀏覽器檢查 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="6824f-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="6824f-113">在 Microsoft Edge tooconfigure hello proxy 設定：</span><span class="sxs-lookup"><span data-stu-id="6824f-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="6824f-114">跳過**設定** > **檢視進階設定** > **開啟的 Proxy 設定** > **手動 Proxy 安裝**.</span><span class="sxs-lookup"><span data-stu-id="6824f-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="6824f-115">設定**使用 proxy 伺服器**太**上**，選取 hello **（內部網路） 的本機位址不要使用 hello proxy 伺服器**核取方塊，然後按一下 變更 hello 位址和連接埠 tooreflect您的本機 proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6824f-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="6824f-116">填入 hello 必要的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="6824f-116">Fill in hello necessary proxy settings.</span></span>

   ![Proxy 設定的對話方塊](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="6824f-118">略過輸出 Proxy</span><span class="sxs-lookup"><span data-stu-id="6824f-118">Bypass outbound proxies</span></span>

<span data-ttu-id="6824f-119">連接器有會發出輸出要求的基礎作業系統元件。</span><span class="sxs-lookup"><span data-stu-id="6824f-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="6824f-120">這些元件會自動嘗試 toolocate hello 網路上的 proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6824f-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="6824f-121">如果啟用 hello 環境中，他們會使用 Web Proxy 自動探索 (WPAD)。</span><span class="sxs-lookup"><span data-stu-id="6824f-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="6824f-122">hello OS 元件嘗試一波波的 wpad.domainsuffix 的 DNS 查閱 toolocate proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6824f-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="6824f-123">如果此解析在 DNS 中，HTTP 要求接著會 toohello IP wpad.dat 的位址。</span><span class="sxs-lookup"><span data-stu-id="6824f-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="6824f-124">此要求會變成您的環境中的 hello proxy 組態指令碼。</span><span class="sxs-lookup"><span data-stu-id="6824f-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="6824f-125">hello 連接器會使用這個指令碼 tooselect 連出 proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6824f-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="6824f-126">不過，連接器流量可能仍然不經過，由於在 hello proxy 所需的其他組態設定。</span><span class="sxs-lookup"><span data-stu-id="6824f-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="6824f-127">您可以設定它使用您在內部部署 proxy tooensure 直接連線 toohello Azure hello 連接器 toobypass 服務。</span><span class="sxs-lookup"><span data-stu-id="6824f-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="6824f-128">我們建議您使用這種方法 （如果它允許您的網路原則），因為這表示您有一個較少的組態 toomaintain。</span><span class="sxs-lookup"><span data-stu-id="6824f-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="6824f-129">hello 連接器 toodisable 連出 proxy 使用方式編輯 hello C:\Program Files\Microsoft AAD 應用程式 Proxy Connector\ApplicationProxyConnectorService.exe.config 檔案，並新增 hello *system.net*此程式碼範例所示的區段:</span><span class="sxs-lookup"><span data-stu-id="6824f-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

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
<span data-ttu-id="6824f-130">tooensure hello 連接器更新程式服務也會略過 hello proxy，使類似變更 toohello ApplicationProxyConnectorUpdaterService.exe.config 檔案位於 C:\Program Files\Microsoft AAD 應用程式 Proxy 連接器更新程式。</span><span class="sxs-lookup"><span data-stu-id="6824f-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="6824f-131">是 hello 原始檔，確定 toomake 副本，以防您需要 toorevert toohello 預設.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="6824f-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="6824f-132">使用 hello 連出 proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="6824f-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="6824f-133">某些環境中需要所有的輸出流量 toogo 透過輸出 proxy，而沒有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6824f-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="6824f-134">如此一來，略過 hello proxy 不是選項。</span><span class="sxs-lookup"><span data-stu-id="6824f-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="6824f-135">您可以設定透過 hello 輸出 proxy，hello 連接器流量 toogo hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="6824f-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![設定連接器流量 toogo 透過連出 proxy tooAzure AD 應用程式 Proxy](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="6824f-137">因此只有輸出流量的沒有任何需要 tooconfigure 輸入通過防火牆的存取。</span><span class="sxs-lookup"><span data-stu-id="6824f-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="6824f-138">步驟 1： 設定 hello 連接器和相關服務 toogo 透過 hello 連出 proxy</span><span class="sxs-lookup"><span data-stu-id="6824f-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="6824f-139">Hello 連接器就如同舊版中，如果 WPAD hello 環境中啟用並適當地設定，會自動探索 hello 連出 proxy 伺服器，並嘗試 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="6824f-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="6824f-140">不過，您可以明確地設定 hello 連接器 toogo 透過輸出的 proxy。</span><span class="sxs-lookup"><span data-stu-id="6824f-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="6824f-141">toodo 因此編輯 hello C:\Program Files\Microsoft AAD 應用程式 Proxy Connector\ApplicationProxyConnectorService.exe.config 檔案，然後新增 hello *system.net* > 一節，此程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="6824f-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="6824f-142">變更*proxyserver:8080* tooreflect 您本機 proxy 伺服器名稱或 IP 位址與 hello 連接埠會接聽。</span><span class="sxs-lookup"><span data-stu-id="6824f-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

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

<span data-ttu-id="6824f-143">接下來，進行類似的變更 toohello 檔案位於 C:\Program Files\Microsoft AAD 應用程式 Proxy 連接器 Updater\ApplicationProxyConnectorUpdaterService.exe.config 設定 hello 連接器更新程式服務 toouse hello proxy。</span><span class="sxs-lookup"><span data-stu-id="6824f-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="6824f-144">步驟 2： 設定從 hello 連接器和相關的服務 tooflow 透過 hello proxy tooallow 流量</span><span class="sxs-lookup"><span data-stu-id="6824f-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="6824f-145">在 hello 連出 proxy 有四個層面 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="6824f-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="6824f-146">Proxy 輸出規則</span><span class="sxs-lookup"><span data-stu-id="6824f-146">Proxy outbound rules</span></span>
* <span data-ttu-id="6824f-147">Proxy 驗證</span><span class="sxs-lookup"><span data-stu-id="6824f-147">Proxy authentication</span></span>
* <span data-ttu-id="6824f-148">Proxy 連接埠</span><span class="sxs-lookup"><span data-stu-id="6824f-148">Proxy ports</span></span>
* <span data-ttu-id="6824f-149">SSL 審查</span><span class="sxs-lookup"><span data-stu-id="6824f-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="6824f-150">Proxy 輸出規則</span><span class="sxs-lookup"><span data-stu-id="6824f-150">Proxy outbound rules</span></span>
<span data-ttu-id="6824f-151">允許存取 toohello 下列連接器服務存取的端點：</span><span class="sxs-lookup"><span data-stu-id="6824f-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="6824f-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="6824f-152">*.msappproxy.net</span></span>
* <span data-ttu-id="6824f-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="6824f-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="6824f-154">初始的註冊，允許存取 toohello 下列端點：</span><span class="sxs-lookup"><span data-stu-id="6824f-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="6824f-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="6824f-155">login.windows.net</span></span>
* <span data-ttu-id="6824f-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6824f-156">login.microsoftonline.com</span></span>

<span data-ttu-id="6824f-157">如果您不允許連線的 FQDN，而且需要 toospecify IP 範圍相反地，使用這些選項：</span><span class="sxs-lookup"><span data-stu-id="6824f-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="6824f-158">允許 hello 連接器對外存取 tooall 目的地。</span><span class="sxs-lookup"><span data-stu-id="6824f-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="6824f-159">允許 hello 連接器對外存取太[Azure 資料中心 IP 範圍](https://www.microsoft.com/en-gb/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="6824f-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="6824f-160">使用 hello Azure 資料中心 IP 範圍清單的 hello 挑戰是每週更新。</span><span class="sxs-lookup"><span data-stu-id="6824f-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="6824f-161">您需要 tooput 位置 tooensure 據以更新您的存取規則中的處理序。</span><span class="sxs-lookup"><span data-stu-id="6824f-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="6824f-162">Proxy 驗證</span><span class="sxs-lookup"><span data-stu-id="6824f-162">Proxy authentication</span></span>

<span data-ttu-id="6824f-163">目前不支援 Proxy 驗證。</span><span class="sxs-lookup"><span data-stu-id="6824f-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="6824f-164">我們目前建議 tooallow hello 連接器匿名存取 toohello 網際網路目的地。</span><span class="sxs-lookup"><span data-stu-id="6824f-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="6824f-165">Proxy 連接埠</span><span class="sxs-lookup"><span data-stu-id="6824f-165">Proxy ports</span></span>

<span data-ttu-id="6824f-166">hello 連接器可藉由使用 hello CONNECT 方法的輸出的 ssl 連線。</span><span class="sxs-lookup"><span data-stu-id="6824f-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="6824f-167">這個方法基本上穿過 hello 連出 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="6824f-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="6824f-168">設定 hello proxy 伺服器 tooallow 通道 tooports 443 和 80。</span><span class="sxs-lookup"><span data-stu-id="6824f-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="6824f-169">當服務匯流排在 HTTPS 上執行時，它會使用連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="6824f-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="6824f-170">不過，根據預設，服務匯流排嘗試直接 TCP 連線，而且會回復 tooHTTPS 只有直接連線失敗時。</span><span class="sxs-lookup"><span data-stu-id="6824f-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="6824f-171">hello 流量也會傳送 hello 連出 proxy 伺服器透過服務匯流排，請確認該 hello 連接器無法直接連線 toohello tooensure Azure 服務的連接埠 9350、 9352 和 5671。</span><span class="sxs-lookup"><span data-stu-id="6824f-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="6824f-172">SSL 審查</span><span class="sxs-lookup"><span data-stu-id="6824f-172">SSL inspection</span></span>
<span data-ttu-id="6824f-173">請勿用於 SSL 檢查 hello 連接器流量，因為這會導致 hello 連接器流量的問題。</span><span class="sxs-lookup"><span data-stu-id="6824f-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="6824f-174">針對連接器 Proxy 問題和服務連線問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="6824f-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="6824f-175">現在您應該會看到所有流量流經 hello proxy。</span><span class="sxs-lookup"><span data-stu-id="6824f-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="6824f-176">如果您有問題，應該有助於 hello 下列疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="6824f-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="6824f-177">hello 最佳方式 tooidentify 和連接器連線問題疑難排解的問題是的 tootake 啟動 hello 連接器服務時擷取 hello 連接器服務的網路。</span><span class="sxs-lookup"><span data-stu-id="6824f-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="6824f-178">這可能是令人怯步的工作，因此讓我們看看關於擷取及篩選網路追蹤的快速提示。</span><span class="sxs-lookup"><span data-stu-id="6824f-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="6824f-179">您可以使用 hello 監視您所選擇的工具。</span><span class="sxs-lookup"><span data-stu-id="6824f-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="6824f-180">針對 hello 本文的目的，我們會使用 Microsoft 網路監視器 3.4。</span><span class="sxs-lookup"><span data-stu-id="6824f-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="6824f-181">您可以[從 Microsoft 下載](https://www.microsoft.com/download/details.aspx?id=4865)。</span><span class="sxs-lookup"><span data-stu-id="6824f-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="6824f-182">hello 範例和我們在 hello 下列各節中使用的篩選特定 tooNetwork 監視器，但 hello 原則可以套用的 tooany 分析工具。</span><span class="sxs-lookup"><span data-stu-id="6824f-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="6824f-183">使用網路監視器進行擷取</span><span class="sxs-lookup"><span data-stu-id="6824f-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="6824f-184">toostart 擷取：</span><span class="sxs-lookup"><span data-stu-id="6824f-184">toostart a capture:</span></span>

1. <span data-ttu-id="6824f-185">開啟網路監視器，並按一下 [新增擷取]。</span><span class="sxs-lookup"><span data-stu-id="6824f-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="6824f-186">按一下 hello**啟動** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6824f-186">Click hello **Start** button.</span></span>

   ![網路監視器視窗](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="6824f-188">完成擷取之後，請按一下 hello**停止**按鈕 tooend 它。</span><span class="sxs-lookup"><span data-stu-id="6824f-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="6824f-189">擷取連接器流量</span><span class="sxs-lookup"><span data-stu-id="6824f-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="6824f-190">初始疑難排解時，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6824f-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="6824f-191">從 services.msc，停止 hello Azure AD 應用程式 Proxy 連接器服務。</span><span class="sxs-lookup"><span data-stu-id="6824f-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="6824f-192">啟動 hello 網路擷取。</span><span class="sxs-lookup"><span data-stu-id="6824f-192">Start hello network capture.</span></span>
3. <span data-ttu-id="6824f-193">啟動 hello Azure AD 應用程式 Proxy 連接器服務。</span><span class="sxs-lookup"><span data-stu-id="6824f-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="6824f-194">停止 hello 網路擷取。</span><span class="sxs-lookup"><span data-stu-id="6824f-194">Stop hello network capture.</span></span>

   ![services.msc 中的 Azure AD 應用程式 Proxy 連接器服務](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="6824f-196">查看 hello 要求從 hello 連接器 toohello proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="6824f-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="6824f-197">現在您有網路擷取，您已準備好 toofilter 它。</span><span class="sxs-lookup"><span data-stu-id="6824f-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="6824f-198">hello 金鑰 toolooking hello 追蹤在了解如何 toofilter hello 擷取。</span><span class="sxs-lookup"><span data-stu-id="6824f-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="6824f-199">一個篩選條件如下所示 （其中 8080 是 hello proxy 服務連接埠）：</span><span class="sxs-lookup"><span data-stu-id="6824f-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="6824f-200">**(http.Request or http.Response) and tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="6824f-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="6824f-201">如果您輸入此篩選條件在 hello**顯示篩選**視窗，然後選取**套用**，它會篩選根據 hello 篩選 hello 擷取流量。</span><span class="sxs-lookup"><span data-stu-id="6824f-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="6824f-202">hello 上述篩選條件會顯示只 hello HTTP 要求和回應從 hello proxy 連接埠。</span><span class="sxs-lookup"><span data-stu-id="6824f-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="6824f-203">連接器啟動，其中 hello 連接器是設定的 toouse proxy 伺服器，會顯示 hello 篩選結果類似這樣：</span><span class="sxs-lookup"><span data-stu-id="6824f-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![篩選之 HTTP 要求和回應的範例清單](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="6824f-205">您想要現在特別尋求的 hello 連線要求，顯示與 hello proxy 伺服器的通訊。</span><span class="sxs-lookup"><span data-stu-id="6824f-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="6824f-206">成功時，您會收到 HTTP OK (200) 回應。</span><span class="sxs-lookup"><span data-stu-id="6824f-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="6824f-207">如果您看到其他回應碼，例如 407 或 502，hello proxy 需要驗證，或因其他原因而禁止 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="6824f-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="6824f-208">此時您會與您的 Proxy 伺服器支援團隊合作。</span><span class="sxs-lookup"><span data-stu-id="6824f-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="6824f-209">識別失敗的 TCP 連線嘗試</span><span class="sxs-lookup"><span data-stu-id="6824f-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="6824f-210">hello 其他常見的案例，您可能會想要時 hello 連接器嘗試 tooconnect 直接，但它失敗。</span><span class="sxs-lookup"><span data-stu-id="6824f-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="6824f-211">另一個網路監視器篩選，可協助您 tooeasily 識別這個問題是：</span><span class="sxs-lookup"><span data-stu-id="6824f-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="6824f-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="6824f-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="6824f-213">SYN 封包是 hello 第一個封包傳送 tooestablish TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="6824f-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="6824f-214">如果這個封包不會傳回回應，hello SYN 重試失敗。</span><span class="sxs-lookup"><span data-stu-id="6824f-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="6824f-215">您可以使用任何重新傳輸的 Syn 之前篩選 toosee hello。</span><span class="sxs-lookup"><span data-stu-id="6824f-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="6824f-216">然後，您可以檢查這些 Syn 是否對應 tooany 連接器相關的資料流。</span><span class="sxs-lookup"><span data-stu-id="6824f-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="6824f-217">hello 下例示範失敗的連線嘗試 tooService 匯流排連接埠則為 9352:</span><span class="sxs-lookup"><span data-stu-id="6824f-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![失敗連線嘗試的範例回應](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="6824f-219">如果您看到類似前面回應 hello，hello 連接器正嘗試 toocommunicate 直接與 hello Azure 服務匯流排服務。</span><span class="sxs-lookup"><span data-stu-id="6824f-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="6824f-220">如果您預期 hello 連接器 toomake 直接連接 toohello Azure 服務，此回應是清楚知道您是否有網路或防火牆問題。</span><span class="sxs-lookup"><span data-stu-id="6824f-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="6824f-221">如果您是設定的 toouse proxy 伺服器，可能表示這個回應，Service Bus 嘗試直接 TCP 連線之後，才能透過 HTTPS 切換 tooattempting 連接。</span><span class="sxs-lookup"><span data-stu-id="6824f-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="6824f-222">網路追蹤分析並非適合每個人。</span><span class="sxs-lookup"><span data-stu-id="6824f-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="6824f-223">但它可以是與您的網路狀況有關的寶貴工具 tooget 快速資訊。</span><span class="sxs-lookup"><span data-stu-id="6824f-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="6824f-224">如果您繼續 toostruggle 與連接器連線問題，請使用我們支援小組建立票證。</span><span class="sxs-lookup"><span data-stu-id="6824f-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="6824f-225">hello 小組可協助您進行進一步的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="6824f-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="6824f-226">如需有關解決應用程式 Proxy 連接器錯誤的相關資訊，請參閱[疑難排解應用程式 Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot)。</span><span class="sxs-lookup"><span data-stu-id="6824f-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6824f-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6824f-227">Next steps</span></span>

[<span data-ttu-id="6824f-228">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="6824f-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="6824f-229">
[Toosilently hello Azure AD 應用程式 Proxy 連接器的安裝方式](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="6824f-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
