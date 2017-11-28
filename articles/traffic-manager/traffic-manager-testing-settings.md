---
title: "aaaVerify Azure Traffic Manager 設定 |Microsoft 文件"
description: "此文章將協助您驗證流量管理員設定"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a><span data-ttu-id="ba119-103">驗證流量管理員設定</span><span class="sxs-lookup"><span data-stu-id="ba119-103">Verify Traffic Manager settings</span></span>

<span data-ttu-id="ba119-104">tootest Traffic Manager 設定，您需要 toohave 多個用戶端，在不同的位置，您可以從中執行測試。</span><span class="sxs-lookup"><span data-stu-id="ba119-104">tootest your Traffic Manager settings, you need toohave multiple clients, in various locations, from which you can run your tests.</span></span> <span data-ttu-id="ba119-105">然後，將下一次在 Traffic Manager 設定檔中的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="ba119-105">Then, bring hello endpoints in your Traffic Manager profile down one at a time.</span></span>

* <span data-ttu-id="ba119-106">設定 DNS TTL 值 hello 低，使變更傳播快速 （例如，30 秒為單位）。</span><span class="sxs-lookup"><span data-stu-id="ba119-106">Set hello DNS TTL value low so that changes propagate quickly (for example, 30 seconds).</span></span>
* <span data-ttu-id="ba119-107">知道 hello Azure 雲端服務和網站中您所測試的 hello 設定檔的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ba119-107">Know hello IP addresses of your Azure cloud services and websites in hello profile you are testing.</span></span>
* <span data-ttu-id="ba119-108">使用工具，可讓您解析 DNS 名稱 tooan IP 位址，並顯示該位址。</span><span class="sxs-lookup"><span data-stu-id="ba119-108">Use tools that let you resolve a DNS name tooan IP address and display that address.</span></span>

<span data-ttu-id="ba119-109">您檢查 toosee hello DNS 名稱解析 tooIP hello 設定檔中的端點位址。</span><span class="sxs-lookup"><span data-stu-id="ba119-109">You are checking toosee that hello DNS names resolve tooIP addresses of hello endpoints in your profile.</span></span> <span data-ttu-id="ba119-110">解析 hello 名稱應該與 hello Traffic Manager 設定檔中定義的 hello 流量路由方式一致的方式。</span><span class="sxs-lookup"><span data-stu-id="ba119-110">hello names should resolve in a manner consistent with hello traffic routing method defined in hello Traffic Manager profile.</span></span> <span data-ttu-id="ba119-111">您可以使用類似的 hello 工具**nslookup**或**繼續深入了解**tooresolve DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="ba119-111">You can use hello tools like **nslookup** or **dig** tooresolve DNS names.</span></span>

<span data-ttu-id="ba119-112">hello 以下範例將協助您測試 Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="ba119-112">hello following examples help you test your Traffic Manager profile.</span></span>

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a><span data-ttu-id="ba119-113">使用 Windows 中的 nslookup 和 ipconfig 檢查流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="ba119-113">Check Traffic Manager profile using nslookup and ipconfig in Windows</span></span>

1. <span data-ttu-id="ba119-114">以系統管理員的身分開啟命令或 Windows PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="ba119-114">Open a command or Windows PowerShell prompt as an administrator.</span></span>
2. <span data-ttu-id="ba119-115">型別`ipconfig /flushdns`tooflush hello DNS 解析程式快取。</span><span class="sxs-lookup"><span data-stu-id="ba119-115">Type `ipconfig /flushdns` tooflush hello DNS resolver cache.</span></span>
3. <span data-ttu-id="ba119-116">輸入 `nslookup <your Traffic Manager domain name>`。</span><span class="sxs-lookup"><span data-stu-id="ba119-116">Type `nslookup <your Traffic Manager domain name>`.</span></span> <span data-ttu-id="ba119-117">例如，下列命令檢查 hello hello 前置詞的網域名稱來 hello *myapp.contoso*</span><span class="sxs-lookup"><span data-stu-id="ba119-117">For example, hello following command checks hello domain name with hello prefix *myapp.contoso*</span></span>

        nslookup myapp.contoso.trafficmanager.net

    <span data-ttu-id="ba119-118">典型的結果會顯示下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="ba119-118">A typical result shows hello following information:</span></span>

    + <span data-ttu-id="ba119-119">hello DNS 名稱和 IP 位址的 hello DNS 伺服器正在存取 tooresolve 此 Traffic Manager 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ba119-119">hello DNS name and IP address of hello DNS server being accessed tooresolve this Traffic Manager domain name.</span></span>
    + <span data-ttu-id="ba119-120">hello Traffic Manager 網域名稱輸入 hello 命令列上之後"nslookup"後面，而且 hello IP 位址 toowhich hello Traffic Manager 網域解析。</span><span class="sxs-lookup"><span data-stu-id="ba119-120">hello Traffic Manager domain name you typed on hello command line after "nslookup" and hello IP address toowhich hello Traffic Manager domain resolves.</span></span> <span data-ttu-id="ba119-121">hello 第二個 IP 位址是 hello 重要的一個 toocheck。</span><span class="sxs-lookup"><span data-stu-id="ba119-121">hello second IP address is hello important one toocheck.</span></span> <span data-ttu-id="ba119-122">其值必須符合其中一個 hello 雲端服務或網站 hello 所測試的 Traffic Manager 設定檔中的公用虛擬 IP (VIP) 位址。</span><span class="sxs-lookup"><span data-stu-id="ba119-122">It should match a public virtual IP (VIP) address for one of hello cloud services or websites in hello Traffic Manager profile you are testing.</span></span>

## <a name="how-tootest-hello-failover-traffic-routing-method"></a><span data-ttu-id="ba119-123">Tootest hello 容錯移轉如何流量路由方法</span><span class="sxs-lookup"><span data-stu-id="ba119-123">How tootest hello failover traffic routing method</span></span>

1. <span data-ttu-id="ba119-124">保持所有端點運作。</span><span class="sxs-lookup"><span data-stu-id="ba119-124">Leave all endpoints up.</span></span>
2. <span data-ttu-id="ba119-125">在單一用戶端，使用 nslookup 或類似的公用程式要求公司網域名稱的 DNS 解析。</span><span class="sxs-lookup"><span data-stu-id="ba119-125">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="ba119-126">請確定該 hello 解析 IP 位址符合 hello 主要端點。</span><span class="sxs-lookup"><span data-stu-id="ba119-126">Ensure that hello resolved IP address matches hello primary endpoint.</span></span>
4. <span data-ttu-id="ba119-127">將您的主要端點關機，或移除監視檔案，以便 Traffic Manager 認為服務的 hello 應用程式已關閉的 hello。</span><span class="sxs-lookup"><span data-stu-id="ba119-127">Bring down your primary endpoint or remove hello monitoring file so that Traffic Manager thinks that hello application is down.</span></span>
5. <span data-ttu-id="ba119-128">等候 hello Traffic Manager 設定檔的 hello DNS--存留時間 (TTL) 再加上兩分鐘。</span><span class="sxs-lookup"><span data-stu-id="ba119-128">Wait for hello DNS Time-to-Live (TTL) of hello Traffic Manager profile plus an additional two minutes.</span></span> <span data-ttu-id="ba119-129">例如，若您的 DNS TTL 為 300 秒 (5 分鐘)，則您必須等待 7 分鐘。</span><span class="sxs-lookup"><span data-stu-id="ba119-129">For example, if your DNS TTL is 300 seconds (5 minutes), you must wait for seven minutes.</span></span>
6. <span data-ttu-id="ba119-130">排清您的 DNS 用戶端快取，使用 nslookup 要求 DNS 解析。</span><span class="sxs-lookup"><span data-stu-id="ba119-130">Flush your DNS client cache and request DNS resolution using nslookup.</span></span> <span data-ttu-id="ba119-131">在 Windows 中，您可以清除 DNS 快取與 hello ipconfig /flushdns 命令。</span><span class="sxs-lookup"><span data-stu-id="ba119-131">In Windows, you can flush your DNS cache with hello ipconfig /flushdns command.</span></span>
7. <span data-ttu-id="ba119-132">請確定該 hello 解析 IP 位址是否符合您的次要端點。</span><span class="sxs-lookup"><span data-stu-id="ba119-132">Ensure that hello resolved IP address matches your secondary endpoint.</span></span>
8. <span data-ttu-id="ba119-133">重複 hello 程序，接著垮每個端點。</span><span class="sxs-lookup"><span data-stu-id="ba119-133">Repeat hello process, bringing down each endpoint in turn.</span></span> <span data-ttu-id="ba119-134">請確認該 hello DNS 傳回 hello 清單中的 hello 的 hello 下一個端點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ba119-134">Verify that hello DNS returns hello IP address of hello next endpoint in hello list.</span></span> <span data-ttu-id="ba119-135">當所有端點都皆停止後時，您應該再次取得 hello hello 主要端點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ba119-135">When all endpoints are down, you should obtain hello IP address of hello primary endpoint again.</span></span>

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a><span data-ttu-id="ba119-136">如何 tootest hello 加權流量路由方法</span><span class="sxs-lookup"><span data-stu-id="ba119-136">How tootest hello weighted traffic routing method</span></span>

1. <span data-ttu-id="ba119-137">保持所有端點運作。</span><span class="sxs-lookup"><span data-stu-id="ba119-137">Leave all endpoints up.</span></span>
2. <span data-ttu-id="ba119-138">在單一用戶端，使用 nslookup 或類似的公用程式要求公司網域名稱的 DNS 解析。</span><span class="sxs-lookup"><span data-stu-id="ba119-138">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="ba119-139">請確定該 hello 解析 IP 位址是否符合其中一個端點。</span><span class="sxs-lookup"><span data-stu-id="ba119-139">Ensure that hello resolved IP address matches one of your endpoints.</span></span>
4. <span data-ttu-id="ba119-140">排清 DNS 用戶端快取，然後對每個端點重複步驟 2 和 3。</span><span class="sxs-lookup"><span data-stu-id="ba119-140">Flush your DNS client cache and repeat steps 2 and 3 for each endpoint.</span></span> <span data-ttu-id="ba119-141">您應該可看到為每個端點傳回不同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ba119-141">You should see different IP addresses returned for each of your endpoints.</span></span>

## <a name="how-tootest-hello-performance-traffic-routing-method"></a><span data-ttu-id="ba119-142">如何 tootest hello 效能流量路由方法</span><span class="sxs-lookup"><span data-stu-id="ba119-142">How tootest hello performance traffic routing method</span></span>

<span data-ttu-id="ba119-143">tooeffectively 測試效能流量路由方式中，您必須有遍佈各地的 hello world 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="ba119-143">tooeffectively test a performance traffic routing method, you must have clients located in different parts of hello world.</span></span> <span data-ttu-id="ba119-144">您可以建立用戶端可以使用的 tootest 不同 Azure 區域中您的服務。</span><span class="sxs-lookup"><span data-stu-id="ba119-144">You can create clients in different Azure regions that can be used tootest your services.</span></span> <span data-ttu-id="ba119-145">如果您有全球網路，您可以從遠端登入 tooclients 中其他部分的 hello world 方法，並可以從該處執行測試。</span><span class="sxs-lookup"><span data-stu-id="ba119-145">If you have a global network, you can remotely sign in tooclients in other parts of hello world and run your tests from there.</span></span>

<span data-ttu-id="ba119-146">或者，您可以找到免費的 Web 型 DNS 查閱和挖掘服務。</span><span class="sxs-lookup"><span data-stu-id="ba119-146">Alternatively, there are free web-based DNS lookup and dig services available.</span></span> <span data-ttu-id="ba119-147">這些工具提供 hello 能力 toocheck DNS 名稱解析從 hello 世界各地的不同位置。</span><span class="sxs-lookup"><span data-stu-id="ba119-147">Some of these tools give you hello ability toocheck DNS name resolution from various locations around hello world.</span></span> <span data-ttu-id="ba119-148">例如，搜尋 "DNS lookup" 相關資料。</span><span class="sxs-lookup"><span data-stu-id="ba119-148">Do a search on "DNS lookup" for examples.</span></span> <span data-ttu-id="ba119-149">如 Gomez 或 Keynote 協力廠商服務可以使用的 tooconfirm 您的設定檔會依預期分配流量。</span><span class="sxs-lookup"><span data-stu-id="ba119-149">Third-party services like Gomez or Keynote can be used tooconfirm that your profiles are distributing traffic as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba119-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba119-150">Next steps</span></span>

* [<span data-ttu-id="ba119-151">關於流量管理員流量路由方法</span><span class="sxs-lookup"><span data-stu-id="ba119-151">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="ba119-152">流量管理員的效能考量</span><span class="sxs-lookup"><span data-stu-id="ba119-152">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="ba119-153">疑難排解流量管理員的已降級狀態</span><span class="sxs-lookup"><span data-stu-id="ba119-153">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
