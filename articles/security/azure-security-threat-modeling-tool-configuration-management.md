---
title: "Azure 管理-Microsoft 威脅模型化工具-aaaConfiguration |Microsoft 文件"
description: "hello 威脅模型化工具中公開的威脅防護功能"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a><span data-ttu-id="7ec21-103">安全框架︰組態管理 | 緩和措施</span><span class="sxs-lookup"><span data-stu-id="7ec21-103">Security Frame: Configuration Management | Mitigations</span></span> 
| <span data-ttu-id="7ec21-104">產品/服務</span><span class="sxs-lookup"><span data-stu-id="7ec21-104">Product/Service</span></span> | <span data-ttu-id="7ec21-105">文章</span><span class="sxs-lookup"><span data-stu-id="7ec21-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="7ec21-106">**Web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="7ec21-106">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="7ec21-107">實作內容安全性原則 (CSP)，並停用內嵌 javascript</span><span class="sxs-lookup"><span data-stu-id="7ec21-107">Implement Content Security Policy (CSP), and disable inline javascript</span></span>](#csp-js)</li><li>[<span data-ttu-id="7ec21-108">啟用瀏覽器的 XSS 篩選器</span><span class="sxs-lookup"><span data-stu-id="7ec21-108">Enable browser's XSS filter</span></span>](#xss-filter)</li><li>[<span data-ttu-id="7ec21-109">追蹤和偵錯先前 toodeployment，必須先停用 ASP.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-109">ASP.NET applications must disable tracing and debugging prior toodeployment</span></span>](#trace-deploy)</li><li>[<span data-ttu-id="7ec21-110">僅從信任的來源存取第三方 javascript</span><span class="sxs-lookup"><span data-stu-id="7ec21-110">Access third-party javascripts from trusted sources only</span></span>](#js-trusted)</li><li>[<span data-ttu-id="7ec21-111">確保已驗證的 ASP.NET 頁面納入 UI 偽裝或點擊劫持防禦功能</span><span class="sxs-lookup"><span data-stu-id="7ec21-111">Ensure that authenticated ASP.NET pages incorporate UI Redressing or click-jacking defenses</span></span>](#ui-defenses)</li><li>[<span data-ttu-id="7ec21-112">確保在 ASP.NET Web 應用程式上啟用 CORS 的情況下只允許信任的原始來源</span><span class="sxs-lookup"><span data-stu-id="7ec21-112">Ensure that only trusted origins are allowed if CORS is enabled on ASP.NET Web Applications</span></span>](#cors-aspnet)</li><li>[<span data-ttu-id="7ec21-113">在 ASP.NET 頁面上啟用 ValidateRequest 屬性</span><span class="sxs-lookup"><span data-stu-id="7ec21-113">Enable ValidateRequest attribute on ASP.NET Pages</span></span>](#validate-aspnet)</li><li>[<span data-ttu-id="7ec21-114">使用在本機裝載的最新 JavaScript 程式庫版本</span><span class="sxs-lookup"><span data-stu-id="7ec21-114">Use locally-hosted latest versions of JavaScript libraries</span></span>](#local-js)</li><li>[<span data-ttu-id="7ec21-115">停用自動 MIME 探查</span><span class="sxs-lookup"><span data-stu-id="7ec21-115">Disable automatic MIME sniffing</span></span>](#mime-sniff)</li><li>[<span data-ttu-id="7ec21-116">移除 standard 的伺服器上 Windows Azure Web Sites tooavoid 指紋識別的標頭</span><span class="sxs-lookup"><span data-stu-id="7ec21-116">Remove standard server headers on Windows Azure Web Sites tooavoid fingerprinting</span></span>](#standard-finger)</li></ul> |
| <span data-ttu-id="7ec21-117">**資料庫**</span><span class="sxs-lookup"><span data-stu-id="7ec21-117">**Database**</span></span> | <ul><li>[<span data-ttu-id="7ec21-118">設定用於 Database Engine 存取的 Windows 防火牆</span><span class="sxs-lookup"><span data-stu-id="7ec21-118">Configure a Windows Firewall for Database Engine Access</span></span>](#firewall-db)</li></ul> |
| <span data-ttu-id="7ec21-119">**Web API**</span><span class="sxs-lookup"><span data-stu-id="7ec21-119">**Web API**</span></span> | <ul><li>[<span data-ttu-id="7ec21-120">確保在 ASP.NET Web API 上啟用 CORS 的情況下只允許信任的原始來源</span><span class="sxs-lookup"><span data-stu-id="7ec21-120">Ensure that only trusted origins are allowed if CORS is enabled on ASP.NET Web API</span></span>](#cors-api)</li><li>[<span data-ttu-id="7ec21-121">加密包含敏感性資料的 Web API 組態檔區段</span><span class="sxs-lookup"><span data-stu-id="7ec21-121">Encrypt sections of Web API's configuration files that contain sensitive data</span></span>](#config-sensitive)</li></ul> |
| <span data-ttu-id="7ec21-122">**IoT 裝置**</span><span class="sxs-lookup"><span data-stu-id="7ec21-122">**IoT Device**</span></span> | <ul><li>[<span data-ttu-id="7ec21-123">確保使用強式認證保護所有系統管理介面</span><span class="sxs-lookup"><span data-stu-id="7ec21-123">Ensure that all admin interfaces are secured with strong credentials</span></span>](#admin-strong)</li><li>[<span data-ttu-id="7ec21-124">確保無法在裝置上執行不明的程式碼</span><span class="sxs-lookup"><span data-stu-id="7ec21-124">Ensure that unknown code cannot execute on devices</span></span>](#unknown-exe)</li><li>[<span data-ttu-id="7ec21-125">使用 Bitlocker 將 IoT 裝置的 OS 和其他磁碟分割加密</span><span class="sxs-lookup"><span data-stu-id="7ec21-125">Encrypt OS and additional partitions of IoT Device with bit-locker</span></span>](#partition-iot)</li><li>[<span data-ttu-id="7ec21-126">確定只有 hello 最少服務/功能已啟用裝置上</span><span class="sxs-lookup"><span data-stu-id="7ec21-126">Ensure that only hello minimum services/features are enabled on devices</span></span>](#min-enable)</li></ul> |
| <span data-ttu-id="7ec21-127">**IoT 現場閘道**</span><span class="sxs-lookup"><span data-stu-id="7ec21-127">**IoT Field Gateway**</span></span> | <ul><li>[<span data-ttu-id="7ec21-128">使用 Bitlocker 將 IoT 現場閘道的 OS 和其他磁碟分割加密</span><span class="sxs-lookup"><span data-stu-id="7ec21-128">Encrypt OS and additional partitions of IoT Field Gateway with bit-locker</span></span>](#field-bit-locker)</li><li>[<span data-ttu-id="7ec21-129">請確定在安裝期間，會變更的 hello 欄位閘道 hello 預設登入認證</span><span class="sxs-lookup"><span data-stu-id="7ec21-129">Ensure that hello default login credentials of hello field gateway are changed during installation</span></span>](#default-change)</li></ul> |
| <span data-ttu-id="7ec21-130">**IoT 雲端閘道**</span><span class="sxs-lookup"><span data-stu-id="7ec21-130">**IoT Cloud Gateway**</span></span> | <ul><li>[<span data-ttu-id="7ec21-131">確定該 hello 雲端閘道實作 toodate 註冊程序 tookeep hello 連接裝置韌體</span><span class="sxs-lookup"><span data-stu-id="7ec21-131">Ensure that hello Cloud Gateway implements a process tookeep hello connected devices firmware up toodate</span></span>](#cloud-firmware)</li></ul> |
| <span data-ttu-id="7ec21-132">**電腦信任邊界**</span><span class="sxs-lookup"><span data-stu-id="7ec21-132">**Machine Trust Boundary**</span></span> | <ul><li>[<span data-ttu-id="7ec21-133">確保裝置已根據組織的原則設定端點安全性控制項</span><span class="sxs-lookup"><span data-stu-id="7ec21-133">Ensure that devices have end-point security controls configured as per organizational policies</span></span>](#controls-policies)</li></ul> |
| <span data-ttu-id="7ec21-134">**Azure 儲存體**</span><span class="sxs-lookup"><span data-stu-id="7ec21-134">**Azure Storage**</span></span> | <ul><li>[<span data-ttu-id="7ec21-135">確保 Azure 儲存體存取金鑰的安全管理</span><span class="sxs-lookup"><span data-stu-id="7ec21-135">Ensure secure management of Azure storage access keys</span></span>](#secure-keys)</li><li>[<span data-ttu-id="7ec21-136">確保在 Azure 儲存體上啟用 CORS 的情況下只允許信任的原始來源</span><span class="sxs-lookup"><span data-stu-id="7ec21-136">Ensure that only trusted origins are allowed if CORS is enabled on Azure storage</span></span>](#cors-storage)</li></ul> |
| <span data-ttu-id="7ec21-137">**WCF**</span><span class="sxs-lookup"><span data-stu-id="7ec21-137">**WCF**</span></span> | <ul><li>[<span data-ttu-id="7ec21-138">啟用 WCF 的服務節流功能</span><span class="sxs-lookup"><span data-stu-id="7ec21-138">Enable WCF's service throttling feature</span></span>](#throttling)</li><li>[<span data-ttu-id="7ec21-139">WCF-透過中繼資料的資訊洩漏</span><span class="sxs-lookup"><span data-stu-id="7ec21-139">WCF-Information disclosure through metadata</span></span>](#info-metadata)</li></ul> | 

## <span data-ttu-id="7ec21-140"><a id="csp-js"></a>實作內容安全性原則 (CSP)，並停用內嵌 javascript</span><span class="sxs-lookup"><span data-stu-id="7ec21-140"><a id="csp-js"></a>Implement Content Security Policy (CSP), and disable inline javascript</span></span>

| <span data-ttu-id="7ec21-141">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-141">Title</span></span>                   | <span data-ttu-id="7ec21-142">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-142">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-143">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-143">**Component**</span></span>               | <span data-ttu-id="7ec21-144">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-144">Web Application</span></span> | 
| <span data-ttu-id="7ec21-145">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-145">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-146">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-146">Build</span></span> |  
| <span data-ttu-id="7ec21-147">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-147">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-148">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-148">Generic</span></span> |
| <span data-ttu-id="7ec21-149">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-149">**Attributes**</span></span>              | <span data-ttu-id="7ec21-150">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-150">N/A</span></span>  |
| <span data-ttu-id="7ec21-151">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-151">**References**</span></span>              | <span data-ttu-id="7ec21-152">[簡介 tooContent 安全性原則](http://www.html5rocks.com/en/tutorials/security/content-security-policy/)，[內容安全性原則參照](http://content-security-policy.com/)，[安全性功能](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/)，[簡介 toocontent 安全性原則](https://docs.webplatform.org/wiki/tutorials/content-security-policy)，[我可以使用 CSP 嗎？](http://caniuse.com/#feat=contentsecuritypolicy)</span><span class="sxs-lookup"><span data-stu-id="7ec21-152">[An Introduction tooContent Security Policy](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [Content Security Policy Reference](http://content-security-policy.com/), [Security features](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [Introduction toocontent security policy](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [Can I use CSP?](http://caniuse.com/#feat=contentsecuritypolicy)</span></span> |
| <span data-ttu-id="7ec21-153">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-153">**Steps**</span></span> | <p><span data-ttu-id="7ec21-154">內容安全性原則 (CSP) 為深度防禦的安全性機制，W3C 標準，可讓 web 應用程式擁有者 toohave 控制項 hello 內容內嵌在其站台上。</span><span class="sxs-lookup"><span data-stu-id="7ec21-154">Content Security Policy (CSP) is a defense-in-depth security mechanism, a W3C standard, that enables web application owners toohave control on hello content embedded in their site.</span></span> <span data-ttu-id="7ec21-155">CSP 會加入成為 hello web 伺服器上的 HTTP 回應標頭，並且在 hello 用戶端瀏覽器會強制執行。</span><span class="sxs-lookup"><span data-stu-id="7ec21-155">CSP is added as an HTTP response header on hello web server and is enforced on hello client side by browsers.</span></span> <span data-ttu-id="7ec21-156">這是以白名單為基礎的原則 - 網站可以宣告一組可從中載入主動式內容 (例如 JavaScript) 的受信任網域。</span><span class="sxs-lookup"><span data-stu-id="7ec21-156">It is a whitelist-based policy - a website can declare a set of trusted domains from which active content such as JavaScript can be loaded.</span></span></p><p><span data-ttu-id="7ec21-157">CSP 提供下列安全性優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ec21-157">CSP provides hello following security benefits:</span></span></p><ul><li><span data-ttu-id="7ec21-158">**防止 XSS:**如果分頁是很容易遭受 tooXSS，攻擊者可以利用它 2 的方式：</span><span class="sxs-lookup"><span data-stu-id="7ec21-158">**Protection against XSS:** If a page is vulnerable tooXSS, an attacker can exploit it in 2 ways:</span></span><ul><li><span data-ttu-id="7ec21-159">插入 `<script>malicious code</script>`。</span><span class="sxs-lookup"><span data-stu-id="7ec21-159">Inject `<script>malicious code</script>`.</span></span> <span data-ttu-id="7ec21-160">此利用將無法運作到期 tooCSP 的限制-1 為基底</span><span class="sxs-lookup"><span data-stu-id="7ec21-160">This exploit will not work due tooCSP’s Base Restriction-1</span></span></li><li><span data-ttu-id="7ec21-161">插入 `<script src=”http://attacker.com/maliciousCode.js”/>`。</span><span class="sxs-lookup"><span data-stu-id="7ec21-161">Inject `<script src=”http://attacker.com/maliciousCode.js”/>`.</span></span> <span data-ttu-id="7ec21-162">Hello 攻擊者控制網域都不會在網域的 CSP 的允許清單中，此利用將無法運作</span><span class="sxs-lookup"><span data-stu-id="7ec21-162">This exploit will not work since hello attacker controlled domain will not be in CSP’s whitelist of domains</span></span></li></ul></li><li><span data-ttu-id="7ec21-163">**控制資料滲透：** CSP 如果網頁上的任何惡意內容嘗試 tooconnect tooan 外部網站，並竊取資料，將會中止 hello 的連接。</span><span class="sxs-lookup"><span data-stu-id="7ec21-163">**Control over data exfiltration:** If any malicious content on a webpage attempts tooconnect tooan external website and steal data, hello connection will be aborted by CSP.</span></span> <span data-ttu-id="7ec21-164">這是因為 hello 目標網域，都不會在 CSP 的白名單</span><span class="sxs-lookup"><span data-stu-id="7ec21-164">This is because hello target domain will not be in CSP’s whitelist</span></span></li><li><span data-ttu-id="7ec21-165">**防禦機制以防止按一下 jacking:**按一下 jacking 是一種攻擊技巧使用敵人可以框架正版的網站，並強制使用者 tooclick UI 項目上。</span><span class="sxs-lookup"><span data-stu-id="7ec21-165">**Defense against click-jacking:** click-jacking is an attack technique using which an adversary can frame a genuine website and force users tooclick on UI elements.</span></span> <span data-ttu-id="7ec21-166">目前可藉由設定回應標頭- X-Frame-Options 來防禦點擊劫持。</span><span class="sxs-lookup"><span data-stu-id="7ec21-166">Currently defense against click-jacking is achieved by configuring a response header- X-Frame-Options.</span></span> <span data-ttu-id="7ec21-167">並非所有瀏覽器尊重此標頭，並將正向 CSP 會針對按一下 jacking 標準方式 toodefend</span><span class="sxs-lookup"><span data-stu-id="7ec21-167">Not all browsers respect this header and going forward CSP will be a standard way toodefend against click-jacking</span></span></li><li><span data-ttu-id="7ec21-168">**即時攻擊 reporting:** CSP 啟用網站的資料隱碼攻擊時，瀏覽器將會自動觸發 hello 網頁伺服器上設定的通知 tooan 端點。</span><span class="sxs-lookup"><span data-stu-id="7ec21-168">**Real-time attack reporting:** If there is an injection attack on a CSP-enabled website, browsers will automatically trigger a notification tooan endpoint configured on hello webserver.</span></span> <span data-ttu-id="7ec21-169">如此一來，CSP 可當作即時警告系統。</span><span class="sxs-lookup"><span data-stu-id="7ec21-169">This way, CSP serves as a real-time warning system.</span></span></li></ul> |

### <a name="example"></a><span data-ttu-id="7ec21-170">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-170">Example</span></span>
<span data-ttu-id="7ec21-171">範例原則︰</span><span class="sxs-lookup"><span data-stu-id="7ec21-171">Example policy:</span></span> 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
<span data-ttu-id="7ec21-172">此原則可讓指令碼 tooload 只能從 hello web 應用程式的伺服器和 google analytics 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7ec21-172">This policy allows scripts tooload only from hello web application’s server and google analytics server.</span></span> <span data-ttu-id="7ec21-173">將會拒絕從任何其他網站載入的指令碼。</span><span class="sxs-lookup"><span data-stu-id="7ec21-173">Scripts loaded from any other site will be rejected.</span></span> <span data-ttu-id="7ec21-174">CSP 是在網站上啟用，hello 下列功能會自動停用的 toomitigate XSS 攻擊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-174">When CSP is enabled on a website, hello following features are automatically disabled toomitigate XSS attacks.</span></span> 

### <a name="example"></a><span data-ttu-id="7ec21-175">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-175">Example</span></span>
<span data-ttu-id="7ec21-176">將不會執行內嵌指令碼。</span><span class="sxs-lookup"><span data-stu-id="7ec21-176">Inline scripts will not execute.</span></span> <span data-ttu-id="7ec21-177">以下是內嵌指令碼的範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-177">Following are examples of inline scripts</span></span> 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a><span data-ttu-id="7ec21-178">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-178">Example</span></span>
<span data-ttu-id="7ec21-179">字串不會評估為程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ec21-179">Strings will not be evaluated as code.</span></span> 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <span data-ttu-id="7ec21-180"><a id="xss-filter"></a>啟用瀏覽器的 XSS 篩選器</span><span class="sxs-lookup"><span data-stu-id="7ec21-180"><a id="xss-filter"></a>Enable browser's XSS filter</span></span>

| <span data-ttu-id="7ec21-181">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-181">Title</span></span>                   | <span data-ttu-id="7ec21-182">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-182">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-183">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-183">**Component**</span></span>               | <span data-ttu-id="7ec21-184">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-184">Web Application</span></span> | 
| <span data-ttu-id="7ec21-185">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-185">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-186">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-186">Build</span></span> |  
| <span data-ttu-id="7ec21-187">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-187">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-188">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-188">Generic</span></span> |
| <span data-ttu-id="7ec21-189">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-189">**Attributes**</span></span>              | <span data-ttu-id="7ec21-190">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-190">N/A</span></span>  |
| <span data-ttu-id="7ec21-191">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-191">**References**</span></span>              | [<span data-ttu-id="7ec21-192">XSS 防護篩選器</span><span class="sxs-lookup"><span data-stu-id="7ec21-192">XSS Protection Filter</span></span>](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection) |
| <span data-ttu-id="7ec21-193">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-193">**Steps**</span></span> | <p><span data-ttu-id="7ec21-194">X XSS 保護回應標頭設定控制項 hello 瀏覽器的跨網站指令碼的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7ec21-194">X-XSS-Protection response header configuration controls hello browser's cross site script filter.</span></span> <span data-ttu-id="7ec21-195">此回應標頭可以有下列值︰</span><span class="sxs-lookup"><span data-stu-id="7ec21-195">This response header can have following values:</span></span></p><ul><li><span data-ttu-id="7ec21-196">`0:`這會停用 hello 篩選</span><span class="sxs-lookup"><span data-stu-id="7ec21-196">`0:` This will disable hello filter</span></span></li><li><span data-ttu-id="7ec21-197">`1: Filter enabled`Hello 瀏覽器偵測到跨網站指令碼的攻擊時，在訂單 toostop hello 攻擊中，將會處理 hello 頁面</span><span class="sxs-lookup"><span data-stu-id="7ec21-197">`1: Filter enabled` If a cross-site scripting attack is detected, in order toostop hello attack, hello browser will sanitize hello page</span></span></li><li><span data-ttu-id="7ec21-198">`1: mode=block : Filter enabled`。</span><span class="sxs-lookup"><span data-stu-id="7ec21-198">`1: mode=block : Filter enabled`.</span></span> <span data-ttu-id="7ec21-199">Hello 瀏覽器而非淨化 hello 頁面上，，偵測到 XSS 攻擊時，會防止 hello 頁面的轉譯</span><span class="sxs-lookup"><span data-stu-id="7ec21-199">Rather than sanitize hello page, when a XSS attack is detected, hello browser will prevent rendering of hello page</span></span></li><li><span data-ttu-id="7ec21-200">`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`。</span><span class="sxs-lookup"><span data-stu-id="7ec21-200">`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`.</span></span> <span data-ttu-id="7ec21-201">hello 瀏覽器將會處理 hello 頁面和報表 hello 違規。</span><span class="sxs-lookup"><span data-stu-id="7ec21-201">hello browser will sanitize hello page and report hello violation.</span></span></li></ul><p><span data-ttu-id="7ec21-202">這是利用 CSP 違規報告 toosend 詳細資料 tooa 您選擇的 URI Chromium 函式。</span><span class="sxs-lookup"><span data-stu-id="7ec21-202">This is a Chromium function utilizing CSP violation reports toosend details tooa URI of your choice.</span></span> <span data-ttu-id="7ec21-203">hello 最後 2 個選項會視為安全的值。</span><span class="sxs-lookup"><span data-stu-id="7ec21-203">hello last 2 options are considered safe values.</span></span></p>|

## <span data-ttu-id="7ec21-204"><a id="trace-deploy"></a>追蹤和偵錯先前 toodeployment，必須先停用 ASP.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-204"><a id="trace-deploy"></a>ASP.NET applications must disable tracing and debugging prior toodeployment</span></span>

| <span data-ttu-id="7ec21-205">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-205">Title</span></span>                   | <span data-ttu-id="7ec21-206">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-206">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-207">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-207">**Component**</span></span>               | <span data-ttu-id="7ec21-208">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-208">Web Application</span></span> | 
| <span data-ttu-id="7ec21-209">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-209">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-210">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-210">Build</span></span> |  
| <span data-ttu-id="7ec21-211">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-211">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-212">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-212">Generic</span></span> |
| <span data-ttu-id="7ec21-213">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-213">**Attributes**</span></span>              | <span data-ttu-id="7ec21-214">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-214">N/A</span></span>  |
| <span data-ttu-id="7ec21-215">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-215">**References**</span></span>              | <span data-ttu-id="7ec21-216">[ASP.NET 偵錯概觀](http://msdn2.microsoft.com/library/ms227556.aspx)、[ASP.NET 追蹤概觀](http://msdn2.microsoft.com/library/bb386420.aspx)、[作法：對 ASP.NET 應用程式啟用追蹤](http://msdn2.microsoft.com/library/0x5wc973.aspx)、[作法：對 ASP.NET 應用程式啟用偵錯](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="7ec21-216">[ASP.NET Debugging Overview](http://msdn2.microsoft.com/library/ms227556.aspx), [ASP.NET Tracing Overview](http://msdn2.microsoft.com/library/bb386420.aspx), [How to: Enable Tracing for an ASP.NET Application](http://msdn2.microsoft.com/library/0x5wc973.aspx), [How to: Enable Debugging for ASP.NET Applications](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx)</span></span> |
| <span data-ttu-id="7ec21-217">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-217">**Steps**</span></span> | <span data-ttu-id="7ec21-218">Hello 頁面啟用追蹤時，每個瀏覽器要求的方式也會取得包含內部伺服器狀態和工作流程的相關資料的 hello 追蹤資訊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-218">When tracing is enabled for hello page, every browser requesting it also obtains hello trace information that contains data about internal server state and workflow.</span></span> <span data-ttu-id="7ec21-219">這項資訊可能是安全性相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-219">That information could be security sensitive.</span></span> <span data-ttu-id="7ec21-220">Hello 頁面啟用偵錯時，完整的堆疊追蹤資料中的 hello 伺服器結果上發生的錯誤會呈現 toohello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7ec21-220">When debugging is enabled for hello page, errors happening on hello server result in a full stack trace data presented toohello browser.</span></span> <span data-ttu-id="7ec21-221">該資料可能會公開有關伺服器 hello 的工作流程的敏感的安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-221">That data may expose security-sensitive information about hello server's workflow.</span></span> |

## <span data-ttu-id="7ec21-222"><a id="js-trusted"></a>僅從信任的來源存取第三方 javascript</span><span class="sxs-lookup"><span data-stu-id="7ec21-222"><a id="js-trusted"></a>Access third-party javascripts from trusted sources only</span></span>

| <span data-ttu-id="7ec21-223">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-223">Title</span></span>                   | <span data-ttu-id="7ec21-224">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-224">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-225">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-225">**Component**</span></span>               | <span data-ttu-id="7ec21-226">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-226">Web Application</span></span> | 
| <span data-ttu-id="7ec21-227">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-227">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-228">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-228">Build</span></span> |  
| <span data-ttu-id="7ec21-229">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-229">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-230">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-230">Generic</span></span> |
| <span data-ttu-id="7ec21-231">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-231">**Attributes**</span></span>              | <span data-ttu-id="7ec21-232">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-232">N/A</span></span>  |
| <span data-ttu-id="7ec21-233">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-233">**References**</span></span>              | <span data-ttu-id="7ec21-234">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-234">N/A</span></span>  |
| <span data-ttu-id="7ec21-235">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-235">**Steps**</span></span> | <span data-ttu-id="7ec21-236">僅能從信任的來源參照第三方 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="7ec21-236">third-party JavaScripts should be referenced only from trusted sources.</span></span> <span data-ttu-id="7ec21-237">hello 參考端點應該一律是在 SSL 上。</span><span class="sxs-lookup"><span data-stu-id="7ec21-237">hello reference endpoints should always be on SSL.</span></span> |

## <span data-ttu-id="7ec21-238"><a id="ui-defenses"></a>確保已驗證的 ASP.NET 頁面納入 UI 偽裝或點擊劫持防禦功能</span><span class="sxs-lookup"><span data-stu-id="7ec21-238"><a id="ui-defenses"></a>Ensure that authenticated ASP.NET pages incorporate UI Redressing or click-jacking defenses</span></span>

| <span data-ttu-id="7ec21-239">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-239">Title</span></span>                   | <span data-ttu-id="7ec21-240">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-240">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-241">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-241">**Component**</span></span>               | <span data-ttu-id="7ec21-242">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-242">Web Application</span></span> | 
| <span data-ttu-id="7ec21-243">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-243">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-244">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-244">Build</span></span> |  
| <span data-ttu-id="7ec21-245">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-245">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-246">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-246">Generic</span></span> |
| <span data-ttu-id="7ec21-247">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-247">**Attributes**</span></span>              | <span data-ttu-id="7ec21-248">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-248">N/A</span></span>  |
| <span data-ttu-id="7ec21-249">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-249">**References**</span></span>              | <span data-ttu-id="7ec21-250">[OWASP 點擊劫持防禦功能提要](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet)、[IE 內部 - 使用 X-Frame-Options 對抗點擊劫持](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/)</span><span class="sxs-lookup"><span data-stu-id="7ec21-250">[OWASP click-jacking Defense Cheat Sheet](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet), [IE Internals - Combating click-jacking With X-Frame-Options](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/)</span></span> |
| <span data-ttu-id="7ec21-251">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-251">**Steps**</span></span> | <p><span data-ttu-id="7ec21-252">按一下 jacking 也稱為 「 UI 賠償攻擊 」，是當攻擊者會使用多個透明或不透明的層級 tootrick 使用者按一下按鈕或連結在另一個頁面上，當它們所想 tooclick hello 最上層頁面上。</span><span class="sxs-lookup"><span data-stu-id="7ec21-252">click-jacking, also known as a "UI redress attack", is when an attacker uses multiple transparent or opaque layers tootrick a user into clicking on a button or link on another page when they were intending tooclick on hello top-level page.</span></span></p><p><span data-ttu-id="7ec21-253">這個分層達成製作惡意的頁面上，使用 iframe，載入 hello 受害者的頁面。</span><span class="sxs-lookup"><span data-stu-id="7ec21-253">This layering is achieved by crafting a malicious page with an iframe, which loads hello victim's page.</span></span> <span data-ttu-id="7ec21-254">因此，hello 攻擊者 「 攔截 」 按一下適用於其頁面，進行路由 tooanother 頁面上，最有可能擁有的另一個應用程式、 網域，或兩者。</span><span class="sxs-lookup"><span data-stu-id="7ec21-254">Thus, hello attacker is "hijacking" clicks meant for their page and routing them tooanother page, most likely owned by another application, domain, or both.</span></span> <span data-ttu-id="7ec21-255">tooprevent 按一下 jacking 攻擊組 hello 適當 X 框架選項 HTTP 回應標頭，以指示 hello 瀏覽器 toonot 允許從其他網域的框架</span><span class="sxs-lookup"><span data-stu-id="7ec21-255">tooprevent click-jacking attacks, set hello proper X-Frame-Options HTTP response headers that instruct hello browser toonot allow framing from other domains</span></span></p>|

### <a name="example"></a><span data-ttu-id="7ec21-256">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-256">Example</span></span>
<span data-ttu-id="7ec21-257">可以透過 IIS 的 web.config 設定 hello X 框架選項標頭。決不能進行框架處理之網站的 Web.config 程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="7ec21-257">hello X-FRAME-OPTIONS header can be set via IIS web.config. Web.config code snippet for sites that should never be framed:</span></span> 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a><span data-ttu-id="7ec21-258">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-258">Example</span></span>
<span data-ttu-id="7ec21-259">只有所包覆的網站的 Web.config 程式碼中的分頁 hello 相同網域：</span><span class="sxs-lookup"><span data-stu-id="7ec21-259">Web.config code for sites that should only be framed by pages in hello same domain:</span></span> 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <span data-ttu-id="7ec21-260"><a id="cors-aspnet"></a>確保在 ASP.NET Web 應用程式上啟用 CORS 的情況下只允許信任的原始來源</span><span class="sxs-lookup"><span data-stu-id="7ec21-260"><a id="cors-aspnet"></a>Ensure that only trusted origins are allowed if CORS is enabled on ASP.NET Web Applications</span></span>

| <span data-ttu-id="7ec21-261">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-261">Title</span></span>                   | <span data-ttu-id="7ec21-262">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-262">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-263">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-263">**Component**</span></span>               | <span data-ttu-id="7ec21-264">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-264">Web Application</span></span> | 
| <span data-ttu-id="7ec21-265">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-265">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-266">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-266">Build</span></span> |  
| <span data-ttu-id="7ec21-267">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-267">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-268">Web Form、MVC5</span><span class="sxs-lookup"><span data-stu-id="7ec21-268">Web Forms, MVC5</span></span> |
| <span data-ttu-id="7ec21-269">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-269">**Attributes**</span></span>              | <span data-ttu-id="7ec21-270">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-270">N/A</span></span>  |
| <span data-ttu-id="7ec21-271">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-271">**References**</span></span>              | <span data-ttu-id="7ec21-272">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-272">N/A</span></span>  |
| <span data-ttu-id="7ec21-273">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-273">**Steps**</span></span> | <p><span data-ttu-id="7ec21-274">瀏覽器安全性可防止網頁進行 AJAX 要求 tooanother 網域。</span><span class="sxs-lookup"><span data-stu-id="7ec21-274">Browser security prevents a web page from making AJAX requests tooanother domain.</span></span> <span data-ttu-id="7ec21-275">這項限制稱為 hello 相同來源原則，並防止惡意網站從其他站台讀取的機密資料。</span><span class="sxs-lookup"><span data-stu-id="7ec21-275">This restriction is called hello same-origin policy, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="7ec21-276">不過，有時可能需要的 tooexpose Api 安全地其他站台也適用。</span><span class="sxs-lookup"><span data-stu-id="7ec21-276">However, sometimes it might be required tooexpose APIs securely which other sites can consume.</span></span> <span data-ttu-id="7ec21-277">跨原始資源共用 (CORS) 是 toorelax hello 相同來源原則，可讓伺服器 W3C 標準。</span><span class="sxs-lookup"><span data-stu-id="7ec21-277">Cross Origin Resource Sharing (CORS) is a W3C standard that allows a server toorelax hello same-origin policy.</span></span> <span data-ttu-id="7ec21-278">使用 CORS，伺服器可以明確允許某些跨源要求，然而拒絕其他要求。</span><span class="sxs-lookup"><span data-stu-id="7ec21-278">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span></p><p><span data-ttu-id="7ec21-279">相較於早期技術 (例如 JSONP)，CORS 較為安全且更具彈性。</span><span class="sxs-lookup"><span data-stu-id="7ec21-279">CORS is safer and more flexible than earlier techniques such as JSONP.</span></span> <span data-ttu-id="7ec21-280">基本上，啟用 CORS 轉譯 tooadding 少數的 HTTP 回應標頭 (存取控制-*) 完成 toohello web 應用程式，而這幾種方式。</span><span class="sxs-lookup"><span data-stu-id="7ec21-280">At its core, enabling CORS translates tooadding a few HTTP response headers (Access-Control-*) toohello web application and this can be done in a couple of ways.</span></span></p>|

### <a name="example"></a><span data-ttu-id="7ec21-281">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-281">Example</span></span>
<span data-ttu-id="7ec21-282">是否可存取 tooWeb.config，CORS 可以加入下列程式碼的 hello 透過：</span><span class="sxs-lookup"><span data-stu-id="7ec21-282">If access tooWeb.config is available, then CORS can be added through hello following code:</span></span> 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a><span data-ttu-id="7ec21-283">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-283">Example</span></span>
<span data-ttu-id="7ec21-284">如果找不到存取 tooweb.config，則可設定 CORS 加 hello 遵循 CSharp 程式碼：</span><span class="sxs-lookup"><span data-stu-id="7ec21-284">If access tooweb.config is not available, then CORS can be configured by adding hello following CSharp code:</span></span> 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

<span data-ttu-id="7ec21-285">請注意，它是關鍵 tooensure hello 的 「 存取控制-允許-原始 」 屬性中的原始來源清單，請將設定 tooa 有限且受信任組的來源。</span><span class="sxs-lookup"><span data-stu-id="7ec21-285">Please note that it is critical tooensure that hello list of origins in "Access-Control-Allow-Origin" attribute is set tooa finite and trusted set of origins.</span></span> <span data-ttu-id="7ec21-286">這不適當地失敗 tooconfigure (例如，設定 hello 值做為 ' *') 可讓惡意網站 tootrigger 跨原始要求 toohello web 應用程式 > 沒有任何限制，因而讓 hello 應用程式容易遭受 tooCSRF 攻擊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-286">Failing tooconfigure this inappropriately (e.g., setting hello value as '*') will allow malicious sites tootrigger cross origin requests toohello web application >without any restrictions, thereby making hello application vulnerable tooCSRF attacks.</span></span> 

## <span data-ttu-id="7ec21-287"><a id="validate-aspnet"></a>在 ASP.NET 頁面上啟用 ValidateRequest 屬性</span><span class="sxs-lookup"><span data-stu-id="7ec21-287"><a id="validate-aspnet"></a>Enable ValidateRequest attribute on ASP.NET Pages</span></span>

| <span data-ttu-id="7ec21-288">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-288">Title</span></span>                   | <span data-ttu-id="7ec21-289">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-289">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-290">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-290">**Component**</span></span>               | <span data-ttu-id="7ec21-291">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-291">Web Application</span></span> | 
| <span data-ttu-id="7ec21-292">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-292">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-293">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-293">Build</span></span> |  
| <span data-ttu-id="7ec21-294">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-294">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-295">Web Form、MVC5</span><span class="sxs-lookup"><span data-stu-id="7ec21-295">Web Forms, MVC5</span></span> |
| <span data-ttu-id="7ec21-296">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-296">**Attributes**</span></span>              | <span data-ttu-id="7ec21-297">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-297">N/A</span></span>  |
| <span data-ttu-id="7ec21-298">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-298">**References**</span></span>              | [<span data-ttu-id="7ec21-299">要求驗證 - 預防指令碼攻擊</span><span class="sxs-lookup"><span data-stu-id="7ec21-299">Request Validation - Preventing Script Attacks</span></span>](http://www.asp.net/whitepapers/request-validation) |
| <span data-ttu-id="7ec21-300">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-300">**Steps**</span></span> | <p><span data-ttu-id="7ec21-301">要求驗證，自 1.1 版的 ASP.NET 功能防止 hello 伺服器接受內容包含未編碼的 HTML。</span><span class="sxs-lookup"><span data-stu-id="7ec21-301">Request validation, a feature of ASP.NET since version 1.1, prevents hello server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="7ec21-302">此功能設計 toohelp 避免讓用戶端指令碼或 HTML 可以不知情的情況下送出的 tooa 伺服器、 儲存，並接著呈現 tooother 使用者部分指令碼資料隱碼攻擊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-302">This feature is designed toohelp prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted tooa server, stored, and then presented tooother users.</span></span> <span data-ttu-id="7ec21-303">我們仍強烈建議您驗證所有輸入資料，而且適時進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="7ec21-303">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span></p><p><span data-ttu-id="7ec21-304">藉由比較有潛在危險的值的所有輸入的資料 tooa 清單執行要求驗證。</span><span class="sxs-lookup"><span data-stu-id="7ec21-304">Request validation is performed by comparing all input data tooa list of potentially dangerous values.</span></span> <span data-ttu-id="7ec21-305">如果相符，ASP.NET 會引發 `HttpRequestValidationException`。</span><span class="sxs-lookup"><span data-stu-id="7ec21-305">If a match occurs, ASP.NET raises an `HttpRequestValidationException`.</span></span> <span data-ttu-id="7ec21-306">預設會啟用要求驗證功能。</span><span class="sxs-lookup"><span data-stu-id="7ec21-306">By default, Request Validation feature is enabled.</span></span></p>|

### <a name="example"></a><span data-ttu-id="7ec21-307">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-307">Example</span></span>
<span data-ttu-id="7ec21-308">不過，這項功能可以在頁面層級停用︰</span><span class="sxs-lookup"><span data-stu-id="7ec21-308">However, this feature can be disabled at page level:</span></span> 
```XML
<%@ Page validateRequest="false" %> 
```
<span data-ttu-id="7ec21-309">或在應用程式層級停用</span><span class="sxs-lookup"><span data-stu-id="7ec21-309">or, at application level</span></span> 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
<span data-ttu-id="7ec21-310">請注意，要求驗證功能不受支援，而且不是 MVC6 管線的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ec21-310">Please note that Request Validation feature is not supported, and is not part of MVC6 pipeline.</span></span> 

## <span data-ttu-id="7ec21-311"><a id="local-js"></a>使用在本機裝載的最新 JavaScript 程式庫版本</span><span class="sxs-lookup"><span data-stu-id="7ec21-311"><a id="local-js"></a>Use locally-hosted latest versions of JavaScript libraries</span></span>

| <span data-ttu-id="7ec21-312">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-312">Title</span></span>                   | <span data-ttu-id="7ec21-313">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-313">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-314">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-314">**Component**</span></span>               | <span data-ttu-id="7ec21-315">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-315">Web Application</span></span> | 
| <span data-ttu-id="7ec21-316">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-316">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-317">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-317">Build</span></span> |  
| <span data-ttu-id="7ec21-318">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-318">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-319">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-319">Generic</span></span> |
| <span data-ttu-id="7ec21-320">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-320">**Attributes**</span></span>              | <span data-ttu-id="7ec21-321">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-321">N/A</span></span>  |
| <span data-ttu-id="7ec21-322">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-322">**References**</span></span>              | <span data-ttu-id="7ec21-323">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-323">N/A</span></span>  |
| <span data-ttu-id="7ec21-324">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-324">**Steps**</span></span> | <p><span data-ttu-id="7ec21-325">使用 JQuery 之類標準 JavaScript 程式庫的開發人員必須使用已核准且不包含已知安全性缺陷的通用 JavaScript 程式庫版本。</span><span class="sxs-lookup"><span data-stu-id="7ec21-325">Developers using standard JavaScript libraries like JQuery must use approved versions of common JavaScript libraries that do not contain known security flaws.</span></span> <span data-ttu-id="7ec21-326">最好的作法是 toouse hello 最新版的 hello 程式庫，因為它們包含其較舊版本中的已知弱點的安全性修正程式。</span><span class="sxs-lookup"><span data-stu-id="7ec21-326">A good practice is toouse hello most latest version of hello libraries, since they contain security fixes for known vulnerabilities in their older versions.</span></span></p><p><span data-ttu-id="7ec21-327">如果因為 toocompatibility 原因無法使用 hello 最新版本，就應該使用 hello 最低版本如下。</span><span class="sxs-lookup"><span data-stu-id="7ec21-327">If hello most recent release cannot be used due toocompatibility reasons, hello below minimum versions should be used.</span></span></p><p><span data-ttu-id="7ec21-328">可接受的最小版本︰</span><span class="sxs-lookup"><span data-stu-id="7ec21-328">Acceptable minimum versions:</span></span></p><ul><li><span data-ttu-id="7ec21-329">**JQuery**</span><span class="sxs-lookup"><span data-stu-id="7ec21-329">**JQuery**</span></span><ul><li><span data-ttu-id="7ec21-330">JQuery 1.7.1</span><span class="sxs-lookup"><span data-stu-id="7ec21-330">JQuery 1.7.1</span></span></li><li><span data-ttu-id="7ec21-331">JQueryUI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="7ec21-331">JQueryUI 1.10.0</span></span></li><li><span data-ttu-id="7ec21-332">JQuery Validate 1.9</span><span class="sxs-lookup"><span data-stu-id="7ec21-332">JQuery Validate 1.9</span></span></li><li><span data-ttu-id="7ec21-333">JQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="7ec21-333">JQuery Mobile 1.0.1</span></span></li><li><span data-ttu-id="7ec21-334">JQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="7ec21-334">JQuery Cycle 2.99</span></span></li><li><span data-ttu-id="7ec21-335">JQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="7ec21-335">JQuery DataTables 1.9.0</span></span></li></ul></li><li><span data-ttu-id="7ec21-336">**Ajax Control Toolkit**</span><span class="sxs-lookup"><span data-stu-id="7ec21-336">**Ajax Control Toolkit**</span></span><ul><li><span data-ttu-id="7ec21-337">Ajax Control Toolkit 40412</span><span class="sxs-lookup"><span data-stu-id="7ec21-337">Ajax Control Toolkit 40412</span></span></li></ul></li><li><span data-ttu-id="7ec21-338">**ASP.NET Web Form 和 Ajax**</span><span class="sxs-lookup"><span data-stu-id="7ec21-338">**ASP.NET Web Forms and Ajax**</span></span><ul><li><span data-ttu-id="7ec21-339">ASP.NET Web Form 和 Ajax 4</span><span class="sxs-lookup"><span data-stu-id="7ec21-339">ASP.NET Web Forms and Ajax 4</span></span></li><li><span data-ttu-id="7ec21-340">ASP.NET Ajax 3.5</span><span class="sxs-lookup"><span data-stu-id="7ec21-340">ASP.NET Ajax 3.5</span></span></li></ul></li><li><span data-ttu-id="7ec21-341">**ASP.NET MVC**</span><span class="sxs-lookup"><span data-stu-id="7ec21-341">**ASP.NET MVC**</span></span><ul><li><span data-ttu-id="7ec21-342">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="7ec21-342">ASP.NET MVC 3.0</span></span></li></ul></li></ul><p><span data-ttu-id="7ec21-343">決不會從外部網站 (例如 public CDN) 載入任何 JavaScript 程式庫</span><span class="sxs-lookup"><span data-stu-id="7ec21-343">Never load any JavaScript library from external sites such as public CDNs</span></span></p>|

## <span data-ttu-id="7ec21-344"><a id="mime-sniff"></a>停用自動 MIME 探查</span><span class="sxs-lookup"><span data-stu-id="7ec21-344"><a id="mime-sniff"></a>Disable automatic MIME sniffing</span></span>

| <span data-ttu-id="7ec21-345">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-345">Title</span></span>                   | <span data-ttu-id="7ec21-346">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-346">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-347">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-347">**Component**</span></span>               | <span data-ttu-id="7ec21-348">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-348">Web Application</span></span> | 
| <span data-ttu-id="7ec21-349">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-349">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-350">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-350">Build</span></span> |  
| <span data-ttu-id="7ec21-351">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-351">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-352">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-352">Generic</span></span> |
| <span data-ttu-id="7ec21-353">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-353">**Attributes**</span></span>              | <span data-ttu-id="7ec21-354">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-354">N/A</span></span>  |
| <span data-ttu-id="7ec21-355">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-355">**References**</span></span>              | <span data-ttu-id="7ec21-356">[IE8 Security Part V：完善的保護](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)、[MIME 類型](http://en.wikipedia.org/wiki/Mime_type)</span><span class="sxs-lookup"><span data-stu-id="7ec21-356">[IE8 Security Part V: Comprehensive Protection](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx), [MIME type](http://en.wikipedia.org/wiki/Mime_type)</span></span> |
| <span data-ttu-id="7ec21-357">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-357">**Steps**</span></span> | <span data-ttu-id="7ec21-358">hello X 內容-類型選項標頭是可讓開發人員的 HTTP 標頭，其內容不應為 MIME 探查 toospecify。</span><span class="sxs-lookup"><span data-stu-id="7ec21-358">hello X-Content-Type-Options header is an HTTP header that allows developers toospecify that their content should not be MIME-sniffed.</span></span> <span data-ttu-id="7ec21-359">此標頭是設計的 toomitigate MIME 探查攻擊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-359">This header is designed toomitigate MIME-Sniffing attacks.</span></span> <span data-ttu-id="7ec21-360">針對可包含使用者可控制內容的每個頁面上，您必須使用 hello HTTP 標頭 X-內容-類型的選項： nosniff。</span><span class="sxs-lookup"><span data-stu-id="7ec21-360">For each page that could contain user controllable content, you must use hello HTTP Header X-Content-Type-Options:nosniff.</span></span> <span data-ttu-id="7ec21-361">tooenable hello 必要的標頭全域的 hello 應用程式中的所有頁面，您可以 hello 下列其中一種</span><span class="sxs-lookup"><span data-stu-id="7ec21-361">tooenable hello required header globally for all pages in hello application, you can do one of hello following</span></span>|

### <a name="example"></a><span data-ttu-id="7ec21-362">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-362">Example</span></span>
<span data-ttu-id="7ec21-363">如果 hello 應用程式裝載在由網際網路資訊服務 (IIS) 7 及更新版本，請在 hello web.config 檔案中加入 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="7ec21-363">Add hello header in hello web.config file if hello application is hosted by Internet Information Services (IIS) 7 onwards.</span></span> 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a><span data-ttu-id="7ec21-364">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-364">Example</span></span>
<span data-ttu-id="7ec21-365">加入透過 hello hello 標頭全域應用程式\_BeginRequest</span><span class="sxs-lookup"><span data-stu-id="7ec21-365">Add hello header through hello global Application\_BeginRequest</span></span> 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a><span data-ttu-id="7ec21-366">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-366">Example</span></span>
<span data-ttu-id="7ec21-367">實作自訂 HTTP 模組</span><span class="sxs-lookup"><span data-stu-id="7ec21-367">Implement custom HTTP module</span></span> 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a><span data-ttu-id="7ec21-368">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-368">Example</span></span>
<span data-ttu-id="7ec21-369">您可以將它加入 tooindividual 回應啟用 hello 必要的標頭標記僅適用於特定頁面：</span><span class="sxs-lookup"><span data-stu-id="7ec21-369">You can enable hello required header only for specific pages by adding it tooindividual responses:</span></span> 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <span data-ttu-id="7ec21-370"><a id="standard-finger"></a>移除 standard 的伺服器上 Windows Azure Web Sites tooavoid 指紋識別的標頭</span><span class="sxs-lookup"><span data-stu-id="7ec21-370"><a id="standard-finger"></a>Remove standard server headers on Windows Azure Web Sites tooavoid fingerprinting</span></span>

| <span data-ttu-id="7ec21-371">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-371">Title</span></span>                   | <span data-ttu-id="7ec21-372">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-372">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-373">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-373">**Component**</span></span>               | <span data-ttu-id="7ec21-374">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-374">Web Application</span></span> | 
| <span data-ttu-id="7ec21-375">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-375">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-376">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-376">Build</span></span> |  
| <span data-ttu-id="7ec21-377">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-377">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-378">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-378">Generic</span></span> |
| <span data-ttu-id="7ec21-379">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-379">**Attributes**</span></span>              | <span data-ttu-id="7ec21-380">EnvironmentType - Azure</span><span class="sxs-lookup"><span data-stu-id="7ec21-380">EnvironmentType - Azure</span></span> |
| <span data-ttu-id="7ec21-381">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-381">**References**</span></span>              | [<span data-ttu-id="7ec21-382">移除 Windows Azure 網站上的標準伺服器標頭</span><span class="sxs-lookup"><span data-stu-id="7ec21-382">Removing standard server headers on Windows Azure Web Sites</span></span>](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) |
| <span data-ttu-id="7ec21-383">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-383">**Steps**</span></span> | <span data-ttu-id="7ec21-384">標頭，例如伺服器、 X-電源-，X AspNet 版本顯示 hello 伺服器和 hello 基礎技術相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-384">Headers such as Server, X-Powered-By, X-AspNet-Version reveal information about hello server and hello underlying technologies.</span></span> <span data-ttu-id="7ec21-385">建議 toosuppress 這些標頭，因此可以防止 指紋 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec21-385">It is recommended toosuppress these headers thereby preventing fingerprinting hello application</span></span> |

## <span data-ttu-id="7ec21-386"><a id="firewall-db"></a>設定用於 Database Engine 存取的 Windows 防火牆</span><span class="sxs-lookup"><span data-stu-id="7ec21-386"><a id="firewall-db"></a>Configure a Windows Firewall for Database Engine Access</span></span>

| <span data-ttu-id="7ec21-387">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-387">Title</span></span>                   | <span data-ttu-id="7ec21-388">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-388">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-389">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-389">**Component**</span></span>               | <span data-ttu-id="7ec21-390">資料庫</span><span class="sxs-lookup"><span data-stu-id="7ec21-390">Database</span></span> | 
| <span data-ttu-id="7ec21-391">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-391">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-392">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-392">Build</span></span> |  
| <span data-ttu-id="7ec21-393">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-393">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-394">SQL Azure、OnPrem</span><span class="sxs-lookup"><span data-stu-id="7ec21-394">SQL Azure, OnPrem</span></span> |
| <span data-ttu-id="7ec21-395">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-395">**Attributes**</span></span>              | <span data-ttu-id="7ec21-396">N/A、SQL 版本 - V12</span><span class="sxs-lookup"><span data-stu-id="7ec21-396">N/A, SQL Version - V12</span></span> |
| <span data-ttu-id="7ec21-397">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-397">**References**</span></span>              | <span data-ttu-id="7ec21-398">[如何 tooconfigure Azure SQL database 防火牆](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)，[設定用於 Database Engine 存取的 Windows 防火牆](https://msdn.microsoft.com/library/ms175043)</span><span class="sxs-lookup"><span data-stu-id="7ec21-398">[How tooconfigure an Azure SQL database firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [Configure a Windows Firewall for Database Engine Access](https://msdn.microsoft.com/library/ms175043)</span></span> |
| <span data-ttu-id="7ec21-399">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-399">**Steps**</span></span> | <span data-ttu-id="7ec21-400">防火牆系統有助於預防未經授權的存取 toocomputer 資源。</span><span class="sxs-lookup"><span data-stu-id="7ec21-400">Firewall systems help prevent unauthorized access toocomputer resources.</span></span> <span data-ttu-id="7ec21-401">tooaccess 透過防火牆 hello SQL Server Database Engine 的執行個體，您必須執行 SQL Server tooallow 存取 hello 電腦上設定 hello 防火牆</span><span class="sxs-lookup"><span data-stu-id="7ec21-401">tooaccess an instance of hello SQL Server Database Engine through a firewall, you must configure hello firewall on hello computer running SQL Server tooallow access</span></span> |

## <span data-ttu-id="7ec21-402"><a id="cors-api"></a>確保在 ASP.NET Web API 上啟用 CORS 的情況下只允許信任的原始來源</span><span class="sxs-lookup"><span data-stu-id="7ec21-402"><a id="cors-api"></a>Ensure that only trusted origins are allowed if CORS is enabled on ASP.NET Web API</span></span>

| <span data-ttu-id="7ec21-403">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-403">Title</span></span>                   | <span data-ttu-id="7ec21-404">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-404">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-405">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-405">**Component**</span></span>               | <span data-ttu-id="7ec21-406">Web API</span><span class="sxs-lookup"><span data-stu-id="7ec21-406">Web API</span></span> | 
| <span data-ttu-id="7ec21-407">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-407">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-408">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-408">Build</span></span> |  
| <span data-ttu-id="7ec21-409">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-409">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-410">MVC 5</span><span class="sxs-lookup"><span data-stu-id="7ec21-410">MVC 5</span></span> |
| <span data-ttu-id="7ec21-411">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-411">**Attributes**</span></span>              | <span data-ttu-id="7ec21-412">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-412">N/A</span></span>  |
| <span data-ttu-id="7ec21-413">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-413">**References**</span></span>              | <span data-ttu-id="7ec21-414">[在 ASP.NET Web API 2 中啟用跨源要求](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)、[ASP.NET Web API - ASP.NET Web API 2 中的 CORS 支援](https://msdn.microsoft.com/magazine/dn532203.aspx)</span><span class="sxs-lookup"><span data-stu-id="7ec21-414">[Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api), [ASP.NET Web API - CORS Support in ASP.NET Web API 2](https://msdn.microsoft.com/magazine/dn532203.aspx)</span></span> |
| <span data-ttu-id="7ec21-415">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-415">**Steps**</span></span> | <p><span data-ttu-id="7ec21-416">瀏覽器安全性可防止網頁進行 AJAX 要求 tooanother 網域。</span><span class="sxs-lookup"><span data-stu-id="7ec21-416">Browser security prevents a web page from making AJAX requests tooanother domain.</span></span> <span data-ttu-id="7ec21-417">這項限制稱為 hello 相同來源原則，並防止惡意網站從其他站台讀取的機密資料。</span><span class="sxs-lookup"><span data-stu-id="7ec21-417">This restriction is called hello same-origin policy, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="7ec21-418">不過，有時可能需要的 tooexpose Api 安全地其他站台也適用。</span><span class="sxs-lookup"><span data-stu-id="7ec21-418">However, sometimes it might be required tooexpose APIs securely which other sites can consume.</span></span> <span data-ttu-id="7ec21-419">跨原始資源共用 (CORS) 是 toorelax hello 相同來源原則，可讓伺服器 W3C 標準。</span><span class="sxs-lookup"><span data-stu-id="7ec21-419">Cross Origin Resource Sharing (CORS) is a W3C standard that allows a server toorelax hello same-origin policy.</span></span></p><p><span data-ttu-id="7ec21-420">使用 CORS，伺服器可以明確允許某些跨源要求，然而拒絕其他要求。</span><span class="sxs-lookup"><span data-stu-id="7ec21-420">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="7ec21-421">相較於早期技術 (例如 JSONP)，CORS 較為安全且更具彈性。</span><span class="sxs-lookup"><span data-stu-id="7ec21-421">CORS is safer and more flexible than earlier techniques such as JSONP.</span></span></p>|

### <a name="example"></a><span data-ttu-id="7ec21-422">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-422">Example</span></span>
<span data-ttu-id="7ec21-423">在 hello App_Start/WebApiConfig.cs，加入下列程式碼 toohello WebApiConfig.Register 方法 hello</span><span class="sxs-lookup"><span data-stu-id="7ec21-423">In hello App_Start/WebApiConfig.cs, add hello following code toohello WebApiConfig.Register method</span></span> 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a><span data-ttu-id="7ec21-424">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-424">Example</span></span>
<span data-ttu-id="7ec21-425">EnableCors 屬性可以套用的 tooaction 控制器中的方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7ec21-425">EnableCors attribute can be applied tooaction methods in a controller as follows:</span></span> 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

<span data-ttu-id="7ec21-426">請注意，它是關鍵 tooensure hello EnableCors 屬性中的原始來源的清單，請將設定 tooa 有限且受信任組的來源。</span><span class="sxs-lookup"><span data-stu-id="7ec21-426">Please note that it is critical tooensure that hello list of origins in EnableCors attribute is set tooa finite and trusted set of origins.</span></span> <span data-ttu-id="7ec21-427">這不適當地失敗 tooconfigure (例如，設定 hello 值做為 ' *') 可讓惡意網站 tootrigger 跨原始要求 toohello API 沒有任何限制，> 因此 hello API tooCSRF 容易遭受攻擊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-427">Failing tooconfigure this inappropriately (e.g., setting hello value as '*') will allow malicious sites tootrigger cross origin requests toohello API without any restrictions, >thereby making hello API vulnerable tooCSRF attacks.</span></span> <span data-ttu-id="7ec21-428">可以在控制器層級裝飾 EnableCors。</span><span class="sxs-lookup"><span data-stu-id="7ec21-428">EnableCors can be decorated at controller level.</span></span> 

### <a name="example"></a><span data-ttu-id="7ec21-429">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-429">Example</span></span>
<span data-ttu-id="7ec21-430">在類別中的特定方法的 toodisable CORS hello 的 DisableCors 屬性可以使用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7ec21-430">toodisable CORS on a particular method in a class, hello DisableCors attribute can be used as shown below:</span></span> 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| <span data-ttu-id="7ec21-431">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-431">Title</span></span>                   | <span data-ttu-id="7ec21-432">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-432">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-433">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-433">**Component**</span></span>               | <span data-ttu-id="7ec21-434">Web API</span><span class="sxs-lookup"><span data-stu-id="7ec21-434">Web API</span></span> | 
| <span data-ttu-id="7ec21-435">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-435">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-436">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-436">Build</span></span> |  
| <span data-ttu-id="7ec21-437">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-437">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-438">MVC 6</span><span class="sxs-lookup"><span data-stu-id="7ec21-438">MVC 6</span></span> |
| <span data-ttu-id="7ec21-439">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-439">**Attributes**</span></span>              | <span data-ttu-id="7ec21-440">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-440">N/A</span></span>  |
| <span data-ttu-id="7ec21-441">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-441">**References**</span></span>              | <span data-ttu-id="7ec21-442">[在 ASP.NET Core 1.0 中啟用跨源要求](https://docs.asp.net/en/latest/security/cors.html)。</span><span class="sxs-lookup"><span data-stu-id="7ec21-442">[Enabling Cross-Origin Requests (CORS) in ASP.NET Core 1.0](https://docs.asp.net/en/latest/security/cors.html)</span></span> |
| <span data-ttu-id="7ec21-443">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-443">**Steps**</span></span> | <p><span data-ttu-id="7ec21-444">在 ASP.NET Core 1.0 中，可以使用中介軟體或使用 MVC 啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="7ec21-444">In ASP.NET Core 1.0, CORS can be enabled either using middleware or using MVC.</span></span> <span data-ttu-id="7ec21-445">當使用 MVC tooenable CORS hello 相同 CORS 服務使用，但 hello CORS 中介軟體不是。</span><span class="sxs-lookup"><span data-stu-id="7ec21-445">When using MVC tooenable CORS hello same CORS services are used, but hello CORS middleware is not.</span></span></p>|

<span data-ttu-id="7ec21-446">**方法 1**啟用 CORS 中介軟體： hello 整個應用程式的 CORS tooenable 新增 hello CORS 中介軟體 toohello 要求管線 hello UseCors 擴充方法。</span><span class="sxs-lookup"><span data-stu-id="7ec21-446">**Approach-1** Enabling CORS with middleware: tooenable CORS for hello entire application add hello CORS middleware toohello request pipeline using hello UseCors extension method.</span></span> <span data-ttu-id="7ec21-447">新增使用 hello CorsPolicyBuilder 類別 hello CORS 中介軟體時，就可以指定跨原始原則。</span><span class="sxs-lookup"><span data-stu-id="7ec21-447">A cross-origin policy can be specified when adding hello CORS middleware using hello CorsPolicyBuilder class.</span></span> <span data-ttu-id="7ec21-448">有兩種方式 toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="7ec21-448">There are two ways toodo this:</span></span>

### <a name="example"></a><span data-ttu-id="7ec21-449">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-449">Example</span></span>
<span data-ttu-id="7ec21-450">hello 第一個是 toocall UseCors 與 lambda。</span><span class="sxs-lookup"><span data-stu-id="7ec21-450">hello first is toocall UseCors with a lambda.</span></span> <span data-ttu-id="7ec21-451">hello lambda 採用 CorsPolicyBuilder 物件：</span><span class="sxs-lookup"><span data-stu-id="7ec21-451">hello lambda takes a CorsPolicyBuilder object:</span></span> 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a><span data-ttu-id="7ec21-452">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-452">Example</span></span>
<span data-ttu-id="7ec21-453">hello 第二種是 toodefine 其中一個或多個具名 CORS 原則，然後選取 hello 原則依名稱執行階段。</span><span class="sxs-lookup"><span data-stu-id="7ec21-453">hello second is toodefine one or more named CORS policies, and then select hello policy by name at run time.</span></span> 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

<span data-ttu-id="7ec21-454">**方法 2** MVC 中的啟用 CORS： 開發人員可以使用 MVC tooapply 特定的 CORS，每個動作，每個控制站，或全域的所有控制站。</span><span class="sxs-lookup"><span data-stu-id="7ec21-454">**Approach-2** Enabling CORS in MVC: Developers can alternatively use MVC tooapply specific CORS per action, per controller, or globally for all controllers.</span></span>

### <a name="example"></a><span data-ttu-id="7ec21-455">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-455">Example</span></span>
<span data-ttu-id="7ec21-456">每個動作： toospecify CORS 原則特定的動作加入 hello [EnableCors] 屬性 toohello 動作。</span><span class="sxs-lookup"><span data-stu-id="7ec21-456">Per action: toospecify a CORS policy for a specific action add hello [EnableCors] attribute toohello action.</span></span> <span data-ttu-id="7ec21-457">指定 hello 原則名稱。</span><span class="sxs-lookup"><span data-stu-id="7ec21-457">Specify hello policy name.</span></span> 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a><span data-ttu-id="7ec21-458">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-458">Example</span></span>
<span data-ttu-id="7ec21-459">每個控制站︰</span><span class="sxs-lookup"><span data-stu-id="7ec21-459">Per controller:</span></span> 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a><span data-ttu-id="7ec21-460">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-460">Example</span></span>
<span data-ttu-id="7ec21-461">全域︰</span><span class="sxs-lookup"><span data-stu-id="7ec21-461">Globally:</span></span> 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
<span data-ttu-id="7ec21-462">請注意，它是關鍵 tooensure hello EnableCors 屬性中的原始來源的清單，請將設定 tooa 有限且受信任組的來源。</span><span class="sxs-lookup"><span data-stu-id="7ec21-462">Please note that it is critical tooensure that hello list of origins in EnableCors attribute is set tooa finite and trusted set of origins.</span></span> <span data-ttu-id="7ec21-463">這不適當地失敗 tooconfigure (例如，設定 hello 值做為 ' *') 可讓惡意網站 tootrigger 跨原始要求 toohello API 沒有任何限制，> 因此 hello API tooCSRF 容易遭受攻擊。</span><span class="sxs-lookup"><span data-stu-id="7ec21-463">Failing tooconfigure this inappropriately (e.g., setting hello value as '*') will allow malicious sites tootrigger cross origin requests toohello API without any restrictions, >thereby making hello API vulnerable tooCSRF attacks.</span></span> 

### <a name="example"></a><span data-ttu-id="7ec21-464">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-464">Example</span></span>
<span data-ttu-id="7ec21-465">toodisable CORS 控制器或動作，使用 hello [DisableCors] 屬性。</span><span class="sxs-lookup"><span data-stu-id="7ec21-465">toodisable CORS for a controller or action, use hello [DisableCors] attribute.</span></span> 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <span data-ttu-id="7ec21-466"><a id="config-sensitive"></a>加密包含敏感性資料的 Web API 組態檔區段</span><span class="sxs-lookup"><span data-stu-id="7ec21-466"><a id="config-sensitive"></a>Encrypt sections of Web API's configuration files that contain sensitive data</span></span>

| <span data-ttu-id="7ec21-467">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-467">Title</span></span>                   | <span data-ttu-id="7ec21-468">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-468">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-469">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-469">**Component**</span></span>               | <span data-ttu-id="7ec21-470">Web API</span><span class="sxs-lookup"><span data-stu-id="7ec21-470">Web API</span></span> | 
| <span data-ttu-id="7ec21-471">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-471">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-472">部署</span><span class="sxs-lookup"><span data-stu-id="7ec21-472">Deployment</span></span> |  
| <span data-ttu-id="7ec21-473">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-473">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-474">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-474">Generic</span></span> |
| <span data-ttu-id="7ec21-475">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-475">**Attributes**</span></span>              | <span data-ttu-id="7ec21-476">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-476">N/A</span></span>  |
| <span data-ttu-id="7ec21-477">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-477">**References**</span></span>              | <span data-ttu-id="7ec21-478">[如何： 加密組態區段，在 ASP.NET 2.0 使用 DPAPI](https://msdn.microsoft.com/library/ff647398.aspx)，[指定受保護的組態提供者](https://msdn.microsoft.com/library/68ze1hb2.aspx)，[使用 Azure 金鑰保存庫 tooprotect 應用程式密碼](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/)</span><span class="sxs-lookup"><span data-stu-id="7ec21-478">[How To: Encrypt Configuration Sections in ASP.NET 2.0 Using DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [Specifying a Protected Configuration Provider](https://msdn.microsoft.com/library/68ze1hb2.aspx), [Using Azure Key Vault tooprotect application secrets](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/)</span></span> |
| <span data-ttu-id="7ec21-479">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-479">**Steps**</span></span> | <span data-ttu-id="7ec21-480">例如 hello Web.config 組態檔，appsettings.json 通常會使用 toohold 機密資訊，包括使用者名稱、 密碼、 資料庫連接字串，以及加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="7ec21-480">Configuration files such as hello Web.config, appsettings.json are often used toohold sensitive information, including user names, passwords, database connection strings, and encryption keys.</span></span> <span data-ttu-id="7ec21-481">如果不保護這項資訊，您的應用程式是很容易遭受 tooattackers 或惡意使用者取得敏感性資訊，例如帳戶使用者名稱和密碼、 資料庫名稱和伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="7ec21-481">If you do not protect this information, your application is vulnerable tooattackers or malicious users obtaining sensitive information such as account user names and passwords, database names and server names.</span></span> <span data-ttu-id="7ec21-482">根據 hello 部署類型 （azure/內部），加密 hello 機密使用 DPAPI 或服務，例如 Azure 金鑰保存庫的組態檔區段。</span><span class="sxs-lookup"><span data-stu-id="7ec21-482">Based on hello deployment type (azure/on-prem), encrypt hello sensitive sections of config files using DPAPI or services like Azure Key Vault.</span></span> |

## <span data-ttu-id="7ec21-483"><a id="admin-strong"></a>確保使用強式認證保護所有系統管理介面</span><span class="sxs-lookup"><span data-stu-id="7ec21-483"><a id="admin-strong"></a>Ensure that all admin interfaces are secured with strong credentials</span></span>

| <span data-ttu-id="7ec21-484">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-484">Title</span></span>                   | <span data-ttu-id="7ec21-485">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-485">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-486">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-486">**Component**</span></span>               | <span data-ttu-id="7ec21-487">IoT 裝置</span><span class="sxs-lookup"><span data-stu-id="7ec21-487">IoT Device</span></span> | 
| <span data-ttu-id="7ec21-488">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-488">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-489">部署</span><span class="sxs-lookup"><span data-stu-id="7ec21-489">Deployment</span></span> |  
| <span data-ttu-id="7ec21-490">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-490">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-491">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-491">Generic</span></span> |
| <span data-ttu-id="7ec21-492">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-492">**Attributes**</span></span>              | <span data-ttu-id="7ec21-493">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-493">N/A</span></span>  |
| <span data-ttu-id="7ec21-494">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-494">**References**</span></span>              | <span data-ttu-id="7ec21-495">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-495">N/A</span></span>  |
| <span data-ttu-id="7ec21-496">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-496">**Steps**</span></span> | <span data-ttu-id="7ec21-497">任何系統管理介面 hello 裝置或欄位閘道會公開應該使用強式認證保護。</span><span class="sxs-lookup"><span data-stu-id="7ec21-497">Any administrative interfaces that hello device or field gateway exposes should be secured using strong credentials.</span></span> <span data-ttu-id="7ec21-498">此外，對於任何公開的介面 (如 WiFi、SSH、檔案共用)，應使用強式認證保護 FTP。</span><span class="sxs-lookup"><span data-stu-id="7ec21-498">Also, any other exposed interfaces like WiFi, SSH, File shares, FTP should be secured with strong credentials.</span></span> <span data-ttu-id="7ec21-499">不得使用預設弱式密碼。</span><span class="sxs-lookup"><span data-stu-id="7ec21-499">Default weak passwords should not be used.</span></span> |

## <span data-ttu-id="7ec21-500"><a id="unknown-exe"></a>確保無法在裝置上執行不明的程式碼</span><span class="sxs-lookup"><span data-stu-id="7ec21-500"><a id="unknown-exe"></a>Ensure that unknown code cannot execute on devices</span></span>

| <span data-ttu-id="7ec21-501">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-501">Title</span></span>                   | <span data-ttu-id="7ec21-502">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-502">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-503">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-503">**Component**</span></span>               | <span data-ttu-id="7ec21-504">IoT 裝置</span><span class="sxs-lookup"><span data-stu-id="7ec21-504">IoT Device</span></span> | 
| <span data-ttu-id="7ec21-505">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-505">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-506">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-506">Build</span></span> |  
| <span data-ttu-id="7ec21-507">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-507">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-508">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-508">Generic</span></span> |
| <span data-ttu-id="7ec21-509">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-509">**Attributes**</span></span>              | <span data-ttu-id="7ec21-510">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-510">N/A</span></span>  |
| <span data-ttu-id="7ec21-511">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-511">**References**</span></span>              | [<span data-ttu-id="7ec21-512">在 Windows 10 IoT Core 上啟用安全開機和 BitLocker 裝置加密</span><span class="sxs-lookup"><span data-stu-id="7ec21-512">Enabling Secure Boot and bit-locker Device Encryption on Windows 10 IoT Core</span></span>](https://developer.microsoft.com/windows/iot/win10/sb_bl) |
| <span data-ttu-id="7ec21-513">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-513">**Steps**</span></span> | <span data-ttu-id="7ec21-514">UEFI 安全開機限制 hello 系統 tooonly 允許執行指定的授權單位簽署的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="7ec21-514">UEFI Secure Boot restricts hello system tooonly allow execution of binaries signed by a specified authority.</span></span> <span data-ttu-id="7ec21-515">這項功能會讓不明的程式碼 hello 平台上執行，而且可能會降低它的 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="7ec21-515">This feature prevents unknown code from being executed on hello platform and potentially weakening hello security posture of it.</span></span> <span data-ttu-id="7ec21-516">啟用 UEFI 安全開機，並限制 hello 的受信任程式碼簽章的憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="7ec21-516">Enable UEFI Secure Boot and restrict hello list of certificate authorities that are trusted for signing code.</span></span> <span data-ttu-id="7ec21-517">登入使用一個 hello 信任授權單位的 hello 裝置部署的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ec21-517">Sign all code that is deployed on hello device using one of hello trusted authorities.</span></span> |

## <span data-ttu-id="7ec21-518"><a id="partition-iot"></a>使用 Bitlocker 將 IoT 裝置的 OS 和其他磁碟分割加密</span><span class="sxs-lookup"><span data-stu-id="7ec21-518"><a id="partition-iot"></a>Encrypt OS and additional partitions of IoT Device with bit-locker</span></span>

| <span data-ttu-id="7ec21-519">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-519">Title</span></span>                   | <span data-ttu-id="7ec21-520">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-520">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-521">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-521">**Component**</span></span>               | <span data-ttu-id="7ec21-522">IoT 裝置</span><span class="sxs-lookup"><span data-stu-id="7ec21-522">IoT Device</span></span> | 
| <span data-ttu-id="7ec21-523">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-523">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-524">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-524">Build</span></span> |  
| <span data-ttu-id="7ec21-525">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-525">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-526">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-526">Generic</span></span> |
| <span data-ttu-id="7ec21-527">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-527">**Attributes**</span></span>              | <span data-ttu-id="7ec21-528">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-528">N/A</span></span>  |
| <span data-ttu-id="7ec21-529">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-529">**References**</span></span>              | <span data-ttu-id="7ec21-530">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-530">N/A</span></span>  |
| <span data-ttu-id="7ec21-531">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-531">**Steps**</span></span> | <span data-ttu-id="7ec21-532">Windows 10 IoT 核心實作元保險箱裝置加密，它具有強式相依性的 TPM hello 平台上，包括 hello 必要 preOS 通訊協定進行 hello 必要度量的 UEFI 中的 hello 存在輕量版。</span><span class="sxs-lookup"><span data-stu-id="7ec21-532">Windows 10 IoT Core implements a lightweight version of bit-locker Device Encryption, which has a strong dependency on hello presence of a TPM on hello platform, including hello necessary preOS protocol in UEFI that conducts hello necessary measurements.</span></span> <span data-ttu-id="7ec21-533">這些 preOS 度量，請確定該作業系統稍後所最終記錄的方式啟動 hello OS 的 hello。加密作業系統使用的資料分割元保險箱和任何額外的資料分割也以防它們會儲存任何機密資料。</span><span class="sxs-lookup"><span data-stu-id="7ec21-533">These preOS measurements ensure that hello OS later has a definitive record of how hello OS was launched.Encrypt OS partitions using bit-locker and any additional partitions also in case they store any sensitive data.</span></span> |

## <span data-ttu-id="7ec21-534"><a id="min-enable"></a>確定只有 hello 最少服務/功能已啟用裝置上</span><span class="sxs-lookup"><span data-stu-id="7ec21-534"><a id="min-enable"></a>Ensure that only hello minimum services/features are enabled on devices</span></span>

| <span data-ttu-id="7ec21-535">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-535">Title</span></span>                   | <span data-ttu-id="7ec21-536">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-536">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-537">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-537">**Component**</span></span>               | <span data-ttu-id="7ec21-538">IoT 裝置</span><span class="sxs-lookup"><span data-stu-id="7ec21-538">IoT Device</span></span> | 
| <span data-ttu-id="7ec21-539">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-539">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-540">部署</span><span class="sxs-lookup"><span data-stu-id="7ec21-540">Deployment</span></span> |  
| <span data-ttu-id="7ec21-541">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-541">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-542">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-542">Generic</span></span> |
| <span data-ttu-id="7ec21-543">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-543">**Attributes**</span></span>              | <span data-ttu-id="7ec21-544">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-544">N/A</span></span>  |
| <span data-ttu-id="7ec21-545">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-545">**References**</span></span>              | <span data-ttu-id="7ec21-546">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-546">N/A</span></span>  |
| <span data-ttu-id="7ec21-547">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-547">**Steps**</span></span> | <span data-ttu-id="7ec21-548">請勿啟用或關閉的任何功能或服務在 hello 的 hello 運作 hello 方案不需要的作業系統。</span><span class="sxs-lookup"><span data-stu-id="7ec21-548">Do not enable or turn off any features or services in hello OS that is not required for hello functioning of hello solution.</span></span> <span data-ttu-id="7ec21-549">如例如如果 hello 裝置不需要部署 UI toobe，安裝 Windows IoT 核心版中遠端控制的模式。</span><span class="sxs-lookup"><span data-stu-id="7ec21-549">For e.g. if hello device does not require a UI toobe deployed, install Windows IoT Core in headless mode.</span></span> |

## <span data-ttu-id="7ec21-550"><a id="field-bit-locker"></a>使用 Bitlocker 將 IoT 現場閘道的 OS 和其他磁碟分割加密</span><span class="sxs-lookup"><span data-stu-id="7ec21-550"><a id="field-bit-locker"></a>Encrypt OS and additional partitions of IoT Field Gateway with bit-locker</span></span>

| <span data-ttu-id="7ec21-551">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-551">Title</span></span>                   | <span data-ttu-id="7ec21-552">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-552">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-553">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-553">**Component**</span></span>               | <span data-ttu-id="7ec21-554">IoT 現場閘道</span><span class="sxs-lookup"><span data-stu-id="7ec21-554">IoT Field Gateway</span></span> | 
| <span data-ttu-id="7ec21-555">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-555">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-556">部署</span><span class="sxs-lookup"><span data-stu-id="7ec21-556">Deployment</span></span> |  
| <span data-ttu-id="7ec21-557">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-557">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-558">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-558">Generic</span></span> |
| <span data-ttu-id="7ec21-559">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-559">**Attributes**</span></span>              | <span data-ttu-id="7ec21-560">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-560">N/A</span></span>  |
| <span data-ttu-id="7ec21-561">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-561">**References**</span></span>              | <span data-ttu-id="7ec21-562">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-562">N/A</span></span>  |
| <span data-ttu-id="7ec21-563">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-563">**Steps**</span></span> | <span data-ttu-id="7ec21-564">Windows 10 IoT 核心實作元保險箱裝置加密，它具有強式相依性的 TPM hello 平台上，包括 hello 必要 preOS 通訊協定進行 hello 必要度量的 UEFI 中的 hello 存在輕量版。</span><span class="sxs-lookup"><span data-stu-id="7ec21-564">Windows 10 IoT Core implements a lightweight version of bit-locker Device Encryption, which has a strong dependency on hello presence of a TPM on hello platform, including hello necessary preOS protocol in UEFI that conducts hello necessary measurements.</span></span> <span data-ttu-id="7ec21-565">這些 preOS 度量，請確定該作業系統稍後所最終記錄的方式啟動 hello OS 的 hello。加密作業系統使用的資料分割元保險箱和任何額外的資料分割也以防它們會儲存任何機密資料。</span><span class="sxs-lookup"><span data-stu-id="7ec21-565">These preOS measurements ensure that hello OS later has a definitive record of how hello OS was launched.Encrypt OS partitions using bit-locker and any additional partitions also in case they store any sensitive data.</span></span> |

## <span data-ttu-id="7ec21-566"><a id="default-change"></a>請確定在安裝期間，會變更的 hello 欄位閘道 hello 預設登入認證</span><span class="sxs-lookup"><span data-stu-id="7ec21-566"><a id="default-change"></a>Ensure that hello default login credentials of hello field gateway are changed during installation</span></span>

| <span data-ttu-id="7ec21-567">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-567">Title</span></span>                   | <span data-ttu-id="7ec21-568">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-568">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-569">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-569">**Component**</span></span>               | <span data-ttu-id="7ec21-570">IoT 現場閘道</span><span class="sxs-lookup"><span data-stu-id="7ec21-570">IoT Field Gateway</span></span> | 
| <span data-ttu-id="7ec21-571">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-571">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-572">部署</span><span class="sxs-lookup"><span data-stu-id="7ec21-572">Deployment</span></span> |  
| <span data-ttu-id="7ec21-573">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-573">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-574">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-574">Generic</span></span> |
| <span data-ttu-id="7ec21-575">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-575">**Attributes**</span></span>              | <span data-ttu-id="7ec21-576">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-576">N/A</span></span>  |
| <span data-ttu-id="7ec21-577">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-577">**References**</span></span>              | <span data-ttu-id="7ec21-578">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-578">N/A</span></span>  |
| <span data-ttu-id="7ec21-579">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-579">**Steps**</span></span> | <span data-ttu-id="7ec21-580">請確定在安裝期間，會變更的 hello 欄位閘道 hello 預設登入認證</span><span class="sxs-lookup"><span data-stu-id="7ec21-580">Ensure that hello default login credentials of hello field gateway are changed during installation</span></span> |

## <span data-ttu-id="7ec21-581"><a id="cloud-firmware"></a>確定該 hello 雲端閘道實作 toodate 註冊程序 tookeep hello 連接裝置韌體</span><span class="sxs-lookup"><span data-stu-id="7ec21-581"><a id="cloud-firmware"></a>Ensure that hello Cloud Gateway implements a process tookeep hello connected devices firmware up toodate</span></span>

| <span data-ttu-id="7ec21-582">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-582">Title</span></span>                   | <span data-ttu-id="7ec21-583">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-583">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-584">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-584">**Component**</span></span>               | <span data-ttu-id="7ec21-585">IoT 雲端閘道</span><span class="sxs-lookup"><span data-stu-id="7ec21-585">IoT Cloud Gateway</span></span> | 
| <span data-ttu-id="7ec21-586">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-586">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-587">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-587">Build</span></span> |  
| <span data-ttu-id="7ec21-588">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-588">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-589">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-589">Generic</span></span> |
| <span data-ttu-id="7ec21-590">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-590">**Attributes**</span></span>              | <span data-ttu-id="7ec21-591">閘道選擇 - Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="7ec21-591">Gateway choice - Azure IoT Hub</span></span> |
| <span data-ttu-id="7ec21-592">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-592">**References**</span></span>              | <span data-ttu-id="7ec21-593">[IoT 中樞裝置管理概觀](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/)，[如何 tooupdate 裝置韌體](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/)</span><span class="sxs-lookup"><span data-stu-id="7ec21-593">[IoT Hub Device Management Overview](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [How tooupdate Device Firmware](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/)</span></span> |
| <span data-ttu-id="7ec21-594">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-594">**Steps**</span></span> | <span data-ttu-id="7ec21-595">LWM2M 是從 hello 開放行動聯盟 IoT 裝置管理通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7ec21-595">LWM2M is a protocol from hello Open Mobile Alliance for IoT Device Management.</span></span> <span data-ttu-id="7ec21-596">Azure IoT 裝置管理入口允許 toointeract 與使用裝置作業的實體裝置。</span><span class="sxs-lookup"><span data-stu-id="7ec21-596">Azure IoT device management allows toointeract with physical devices using device jobs.</span></span> <span data-ttu-id="7ec21-597">請確定該 hello 雲端閘道實作處理程序 tooroutinely 保持 hello 裝置和其他組態資料 toodate 使用 Azure IoT 中樞裝置管理設定。</span><span class="sxs-lookup"><span data-stu-id="7ec21-597">Ensure that hello Cloud Gateway implements a process tooroutinely keep hello device and other configuration data up toodate using Azure IoT Hub Device Management.</span></span> |

## <span data-ttu-id="7ec21-598"><a id="controls-policies"></a>確保裝置已根據組織的原則設定端點安全性控制項</span><span class="sxs-lookup"><span data-stu-id="7ec21-598"><a id="controls-policies"></a>Ensure that devices have end-point security controls configured as per organizational policies</span></span>

| <span data-ttu-id="7ec21-599">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-599">Title</span></span>                   | <span data-ttu-id="7ec21-600">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-600">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-601">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-601">**Component**</span></span>               | <span data-ttu-id="7ec21-602">電腦信任邊界</span><span class="sxs-lookup"><span data-stu-id="7ec21-602">Machine Trust Boundary</span></span> | 
| <span data-ttu-id="7ec21-603">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-603">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-604">部署</span><span class="sxs-lookup"><span data-stu-id="7ec21-604">Deployment</span></span> |  
| <span data-ttu-id="7ec21-605">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-605">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-606">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-606">Generic</span></span> |
| <span data-ttu-id="7ec21-607">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-607">**Attributes**</span></span>              | <span data-ttu-id="7ec21-608">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-608">N/A</span></span>  |
| <span data-ttu-id="7ec21-609">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-609">**References**</span></span>              | <span data-ttu-id="7ec21-610">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-610">N/A</span></span>  |
| <span data-ttu-id="7ec21-611">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-611">**Steps**</span></span> | <span data-ttu-id="7ec21-612">確保裝置有根據組織安全性原則設定的端點安全性控制項，例如適用於磁碟層級加密的 bitlocker、採用更新後簽章的防毒軟體、主機型防火牆、OS 升級、群組原則等。</span><span class="sxs-lookup"><span data-stu-id="7ec21-612">Ensure that devices have end-point security controls such as bit-locker for disk-level encryption, anti-virus with updated signatures, host based firewall, OS upgrades, group policies etc. are configured as per organizational security policies.</span></span> |

## <span data-ttu-id="7ec21-613"><a id="secure-keys"></a>確保 Azure 儲存體存取金鑰的安全管理</span><span class="sxs-lookup"><span data-stu-id="7ec21-613"><a id="secure-keys"></a>Ensure secure management of Azure storage access keys</span></span>

| <span data-ttu-id="7ec21-614">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-614">Title</span></span>                   | <span data-ttu-id="7ec21-615">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-615">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-616">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-616">**Component**</span></span>               | <span data-ttu-id="7ec21-617">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="7ec21-617">Azure Storage</span></span> | 
| <span data-ttu-id="7ec21-618">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-618">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-619">部署</span><span class="sxs-lookup"><span data-stu-id="7ec21-619">Deployment</span></span> |  
| <span data-ttu-id="7ec21-620">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-620">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-621">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-621">Generic</span></span> |
| <span data-ttu-id="7ec21-622">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-622">**Attributes**</span></span>              | <span data-ttu-id="7ec21-623">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-623">N/A</span></span>  |
| <span data-ttu-id="7ec21-624">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-624">**References**</span></span>              | [<span data-ttu-id="7ec21-625">Azure 儲存體安全性指南 - 管理儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="7ec21-625">Azure Storage security guide - Managing Your Storage Account Keys</span></span>](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| <span data-ttu-id="7ec21-626">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-626">**Steps**</span></span> | <p><span data-ttu-id="7ec21-627">金鑰儲存： 它建議 toostore hello Azure 儲存體存取金鑰做為密碼的 Azure 金鑰保存庫中，且有 hello 擷取 hello 金鑰從金鑰保存庫的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ec21-627">Key Storage: It is recommended toostore hello Azure Storage access keys in Azure Key Vault as a secret and have hello applications retrieve hello key from key vault.</span></span> <span data-ttu-id="7ec21-628">這因為 toohello 下列建議的原因：</span><span class="sxs-lookup"><span data-stu-id="7ec21-628">This is recommended due toohello following reasons:</span></span></p><ul><li><span data-ttu-id="7ec21-629">hello 應用程式組態檔中，代表要移除的人取得存取 toohello 金鑰沒有特定的權限途徑絕對不會有 hello 儲存體金鑰的硬式編碼</span><span class="sxs-lookup"><span data-stu-id="7ec21-629">hello application will never have hello storage key hardcoded in a configuration file, which removes that avenue of somebody getting access toohello keys without specific permission</span></span></li><li><span data-ttu-id="7ec21-630">可以使用 Azure Active Directory 來控制存取 toohello 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7ec21-630">Access toohello keys can be controlled using Azure Active Directory.</span></span> <span data-ttu-id="7ec21-631">這表示帳戶擁有者可以授與存取 toohello 少數需要 tooretrieve hello 索引鍵，從 Azure 金鑰保存庫的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ec21-631">This means an account owner can grant access toohello handful of applications that need tooretrieve hello keys from Azure Key Vault.</span></span> <span data-ttu-id="7ec21-632">其他應用程式不會無法 tooaccess hello 機碼，不必授與他們權限特別</span><span class="sxs-lookup"><span data-stu-id="7ec21-632">Other applications will not be able tooaccess hello keys without granting them permission specifically</span></span></li><li><span data-ttu-id="7ec21-633">重新產生金鑰： 建議 toohave 處理程序中的位置 tooregenerate Azure 儲存體存取金鑰基於安全性考量。</span><span class="sxs-lookup"><span data-stu-id="7ec21-633">Key Regeneration: It is recommended toohave a process in place tooregenerate Azure storage access keys for security reasons.</span></span> <span data-ttu-id="7ec21-634">有關原因和方式 tooplan 重新產生金鑰所述的 hello Azure 儲存體安全性指南 》 參考文件</span><span class="sxs-lookup"><span data-stu-id="7ec21-634">Details on why and how tooplan for key regeneration are documented in hello Azure Storage Security Guide reference article</span></span></li></ul>|

## <span data-ttu-id="7ec21-635"><a id="cors-storage"></a>確保在 Azure 儲存體上啟用 CORS 的情況下只允許信任的來源</span><span class="sxs-lookup"><span data-stu-id="7ec21-635"><a id="cors-storage"></a>Ensure that only trusted origins are allowed if CORS is enabled on Azure storage</span></span>

| <span data-ttu-id="7ec21-636">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-636">Title</span></span>                   | <span data-ttu-id="7ec21-637">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-637">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-638">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-638">**Component**</span></span>               | <span data-ttu-id="7ec21-639">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="7ec21-639">Azure Storage</span></span> | 
| <span data-ttu-id="7ec21-640">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-640">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-641">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-641">Build</span></span> |  
| <span data-ttu-id="7ec21-642">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-642">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-643">泛型</span><span class="sxs-lookup"><span data-stu-id="7ec21-643">Generic</span></span> |
| <span data-ttu-id="7ec21-644">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-644">**Attributes**</span></span>              | <span data-ttu-id="7ec21-645">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-645">N/A</span></span>  |
| <span data-ttu-id="7ec21-646">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-646">**References**</span></span>              | [<span data-ttu-id="7ec21-647">Hello Azure 儲存體服務的 CORS 支援</span><span class="sxs-lookup"><span data-stu-id="7ec21-647">CORS Support for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| <span data-ttu-id="7ec21-648">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-648">**Steps**</span></span> | <span data-ttu-id="7ec21-649">Azure 儲存體可讓您 tooenable CORS – 跨原始資源共用。</span><span class="sxs-lookup"><span data-stu-id="7ec21-649">Azure Storage allows you tooenable CORS – Cross Origin Resource Sharing.</span></span> <span data-ttu-id="7ec21-650">每個儲存體帳戶，您可以指定可存取該儲存體帳戶中的 hello 資源的網域。</span><span class="sxs-lookup"><span data-stu-id="7ec21-650">For each storage account, you can specify domains that can access hello resources in that storage account.</span></span> <span data-ttu-id="7ec21-651">根據預設，所有服務上都會停用 CORS。</span><span class="sxs-lookup"><span data-stu-id="7ec21-651">By default, CORS is disabled on all services.</span></span> <span data-ttu-id="7ec21-652">您可以使用 hello REST API 或 hello 儲存體用戶端程式庫 toocall 其中 hello 方法 tooset hello 服務原則，以啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="7ec21-652">You can enable CORS by using hello REST API or hello storage client library toocall one of hello methods tooset hello service policies.</span></span> |

## <span data-ttu-id="7ec21-653"><a id="throttling"></a>啟用 WCF 的服務節流功能</span><span class="sxs-lookup"><span data-stu-id="7ec21-653"><a id="throttling"></a>Enable WCF's service throttling feature</span></span>

| <span data-ttu-id="7ec21-654">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-654">Title</span></span>                   | <span data-ttu-id="7ec21-655">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-655">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-656">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-656">**Component**</span></span>               | <span data-ttu-id="7ec21-657">WCF</span><span class="sxs-lookup"><span data-stu-id="7ec21-657">WCF</span></span> | 
| <span data-ttu-id="7ec21-658">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-658">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-659">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-659">Build</span></span> |  
| <span data-ttu-id="7ec21-660">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-660">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-661">.NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="7ec21-661">.NET Framework 3</span></span> |
| <span data-ttu-id="7ec21-662">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-662">**Attributes**</span></span>              | <span data-ttu-id="7ec21-663">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-663">N/A</span></span>  |
| <span data-ttu-id="7ec21-664">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-664">**References**</span></span>              | <span data-ttu-id="7ec21-665">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="7ec21-665">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="7ec21-666">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-666">**Steps**</span></span> | <p><span data-ttu-id="7ec21-667">不在 hello 中放置限制使用的系統資源可能會導致資源耗盡，最後阻絕服務。</span><span class="sxs-lookup"><span data-stu-id="7ec21-667">Not placing a limit on hello use of system resources could result in resource exhaustion and ultimately a denial of service.</span></span></p><ul><li><span data-ttu-id="7ec21-668">**說明：** Windows Communication Foundation (WCF) 提供 hello 能力 toothrottle 服務要求。</span><span class="sxs-lookup"><span data-stu-id="7ec21-668">**EXPLANATION:** Windows Communication Foundation (WCF) offers hello ability toothrottle service requests.</span></span> <span data-ttu-id="7ec21-669">允許太多的用戶端要求可能會淹沒系統及耗盡其資源。</span><span class="sxs-lookup"><span data-stu-id="7ec21-669">Allowing too many client requests can flood a system and exhaust its resources.</span></span> <span data-ttu-id="7ec21-670">Hello 上另一方面，讓只有少數要求 tooa 服務可讓合法使用者無法使用 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="7ec21-670">On hello other hand, allowing only a small number of requests tooa service can prevent legitimate users from using hello service.</span></span> <span data-ttu-id="7ec21-671">每個服務應該設定的個別微調的 tooand tooallow hello 適當的資源數量。</span><span class="sxs-lookup"><span data-stu-id="7ec21-671">Each service should be individually tuned tooand configured tooallow hello appropriate amount of resources.</span></span></li><li><span data-ttu-id="7ec21-672">**建議** 啟用 WCF 的服務節流功能以及為應用程式設定適當的限制。</span><span class="sxs-lookup"><span data-stu-id="7ec21-672">**RECOMMENDATIONS** Enable WCF's service throttling feature and set limits appropriate for your application.</span></span></li></ul>|

### <a name="example"></a><span data-ttu-id="7ec21-673">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-673">Example</span></span>
<span data-ttu-id="7ec21-674">hello 以下是範例設定以啟用節流設定：</span><span class="sxs-lookup"><span data-stu-id="7ec21-674">hello following is an example configuration with throttling enabled:</span></span>
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <span data-ttu-id="7ec21-675"><a id="info-metadata"></a>WCF-透過中繼資料的資訊洩漏</span><span class="sxs-lookup"><span data-stu-id="7ec21-675"><a id="info-metadata"></a>WCF-Information disclosure through metadata</span></span>

| <span data-ttu-id="7ec21-676">Title</span><span class="sxs-lookup"><span data-stu-id="7ec21-676">Title</span></span>                   | <span data-ttu-id="7ec21-677">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-677">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7ec21-678">**元件**</span><span class="sxs-lookup"><span data-stu-id="7ec21-678">**Component**</span></span>               | <span data-ttu-id="7ec21-679">WCF</span><span class="sxs-lookup"><span data-stu-id="7ec21-679">WCF</span></span> | 
| <span data-ttu-id="7ec21-680">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="7ec21-680">**SDL Phase**</span></span>               | <span data-ttu-id="7ec21-681">建置</span><span class="sxs-lookup"><span data-stu-id="7ec21-681">Build</span></span> |  
| <span data-ttu-id="7ec21-682">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="7ec21-682">**Applicable Technologies**</span></span> | <span data-ttu-id="7ec21-683">.NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="7ec21-683">.NET Framework 3</span></span> |
| <span data-ttu-id="7ec21-684">**屬性**</span><span class="sxs-lookup"><span data-stu-id="7ec21-684">**Attributes**</span></span>              | <span data-ttu-id="7ec21-685">N/A</span><span class="sxs-lookup"><span data-stu-id="7ec21-685">N/A</span></span>  |
| <span data-ttu-id="7ec21-686">**參考**</span><span class="sxs-lookup"><span data-stu-id="7ec21-686">**References**</span></span>              | <span data-ttu-id="7ec21-687">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="7ec21-687">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="7ec21-688">**步驟**</span><span class="sxs-lookup"><span data-stu-id="7ec21-688">**Steps**</span></span> | <span data-ttu-id="7ec21-689">中繼資料，有助於深入了解 hello 系統，並規劃一種攻擊，攻擊者。</span><span class="sxs-lookup"><span data-stu-id="7ec21-689">Metadata can help attackers learn about hello system and plan a form of attack.</span></span> <span data-ttu-id="7ec21-690">WCF 服務可以設定的 tooexpose 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7ec21-690">WCF services can be configured tooexpose metadata.</span></span> <span data-ttu-id="7ec21-691">中繼資料可提供詳細的服務描述資訊，且不得在生產環境中廣播。</span><span class="sxs-lookup"><span data-stu-id="7ec21-691">Metadata gives detailed service description information and should not be broadcast in production environments.</span></span> <span data-ttu-id="7ec21-692">hello `HttpGetEnabled`  /  `HttpsGetEnabled` hello ServiceMetaData 類別的屬性定義服務是否會公開 hello 中繼資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-692">hello `HttpGetEnabled` / `HttpsGetEnabled` properties of hello ServiceMetaData class defines whether a service will expose hello metadata</span></span> | 

### <a name="example"></a><span data-ttu-id="7ec21-693">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-693">Example</span></span>
<span data-ttu-id="7ec21-694">hello 的下列程式碼會指示 WCF toobroadcast 服務的中繼資料</span><span class="sxs-lookup"><span data-stu-id="7ec21-694">hello code below instructs WCF toobroadcast a service's metadata</span></span>
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
<span data-ttu-id="7ec21-695">不要在生產環境中廣播服務中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7ec21-695">Do not broadcast service metadata in a production environment.</span></span> <span data-ttu-id="7ec21-696">設定 hello HttpGetEnabled / hello ServiceMetaData HttpsGetEnabled 屬性類別 toofalse。</span><span class="sxs-lookup"><span data-stu-id="7ec21-696">Set hello HttpGetEnabled / HttpsGetEnabled properties of hello ServiceMetaData class toofalse.</span></span> 

### <a name="example"></a><span data-ttu-id="7ec21-697">範例</span><span class="sxs-lookup"><span data-stu-id="7ec21-697">Example</span></span>
<span data-ttu-id="7ec21-698">hello 的下列程式碼會指示 WCF toonot 廣播服務的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7ec21-698">hello code below instructs WCF toonot broadcast a service's metadata.</span></span> 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
