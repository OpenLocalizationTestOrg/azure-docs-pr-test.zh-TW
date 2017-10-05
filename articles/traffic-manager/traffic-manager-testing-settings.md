---
title: "驗證 Azure 流量管理員設定 | Microsoft Docs"
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
ms.openlocfilehash: aadff1806a7cb22347283143563467366e857569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="verify-traffic-manager-settings"></a><span data-ttu-id="949e0-103">驗證流量管理員設定</span><span class="sxs-lookup"><span data-stu-id="949e0-103">Verify Traffic Manager settings</span></span>

<span data-ttu-id="949e0-104">若要測試您的流量管理員設定，您需要有在不同位置的多個用戶端，讓您可以從中執行測試。</span><span class="sxs-lookup"><span data-stu-id="949e0-104">To test your Traffic Manager settings, you need to have multiple clients, in various locations, from which you can run your tests.</span></span> <span data-ttu-id="949e0-105">然後，在流量管理員設定檔中一次關閉一個端點。</span><span class="sxs-lookup"><span data-stu-id="949e0-105">Then, bring the endpoints in your Traffic Manager profile down one at a time.</span></span>

* <span data-ttu-id="949e0-106">設定低的 DNS TTL，方便快速傳播變更，例如 30 秒。</span><span class="sxs-lookup"><span data-stu-id="949e0-106">Set the DNS TTL value low so that changes propagate quickly (for example, 30 seconds).</span></span>
* <span data-ttu-id="949e0-107">知道正在測試的設定檔中您 Azure 雲端服務和網站的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="949e0-107">Know the IP addresses of your Azure cloud services and websites in the profile you are testing.</span></span>
* <span data-ttu-id="949e0-108">使用可讓您解析 IP 位址之 DNS 名稱的工具並顯示該位址。</span><span class="sxs-lookup"><span data-stu-id="949e0-108">Use tools that let you resolve a DNS name to an IP address and display that address.</span></span>

<span data-ttu-id="949e0-109">您要查看設定檔中 DNS 名稱是否解析成端點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="949e0-109">You are checking to see that the DNS names resolve to IP addresses of the endpoints in your profile.</span></span> <span data-ttu-id="949e0-110">名稱的解析方法應與流量管理員設定檔中定義的流量路由方法一致。</span><span class="sxs-lookup"><span data-stu-id="949e0-110">The names should resolve in a manner consistent with the traffic routing method defined in the Traffic Manager profile.</span></span> <span data-ttu-id="949e0-111">您可以使用像是 **nslookup** 或 **dig** 等工具來解析 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="949e0-111">You can use the tools like **nslookup** or **dig** to resolve DNS names.</span></span>

<span data-ttu-id="949e0-112">下列範例可協助您測試流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="949e0-112">The following examples help you test your Traffic Manager profile.</span></span>

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a><span data-ttu-id="949e0-113">使用 Windows 中的 nslookup 和 ipconfig 檢查流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="949e0-113">Check Traffic Manager profile using nslookup and ipconfig in Windows</span></span>

1. <span data-ttu-id="949e0-114">以系統管理員的身分開啟命令或 Windows PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="949e0-114">Open a command or Windows PowerShell prompt as an administrator.</span></span>
2. <span data-ttu-id="949e0-115">輸入 `ipconfig /flushdns` 以排清 DNS 解析程式快取。</span><span class="sxs-lookup"><span data-stu-id="949e0-115">Type `ipconfig /flushdns` to flush the DNS resolver cache.</span></span>
3. <span data-ttu-id="949e0-116">輸入 `nslookup <your Traffic Manager domain name>`。</span><span class="sxs-lookup"><span data-stu-id="949e0-116">Type `nslookup <your Traffic Manager domain name>`.</span></span> <span data-ttu-id="949e0-117">例如，下列命令會檢查包含 myapp.contoso 前置詞的網域名稱</span><span class="sxs-lookup"><span data-stu-id="949e0-117">For example, the following command checks the domain name with the prefix *myapp.contoso*</span></span>

        nslookup myapp.contoso.trafficmanager.net

    <span data-ttu-id="949e0-118">典型的結果會顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="949e0-118">A typical result shows the following information:</span></span>

    + <span data-ttu-id="949e0-119">正在存取 DNS 伺服器的 DNS 名稱和 IP 位址，藉此解析此流量管理員網域名稱。</span><span class="sxs-lookup"><span data-stu-id="949e0-119">The DNS name and IP address of the DNS server being accessed to resolve this Traffic Manager domain name.</span></span>
    + <span data-ttu-id="949e0-120">您在命令行上輸入在 "nslookup" 之後的流量管理員網域名稱，和流量管理員網域名稱解析的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="949e0-120">The Traffic Manager domain name you typed on the command line after "nslookup" and the IP address to which the Traffic Manager domain resolves.</span></span> <span data-ttu-id="949e0-121">第二個 IP 位址是要檢查的重點。</span><span class="sxs-lookup"><span data-stu-id="949e0-121">The second IP address is the important one to check.</span></span> <span data-ttu-id="949e0-122">它應符合正在測試流量管理員設定檔中其中一個雲端服務或網站的 虛擬 IP (VIP)。</span><span class="sxs-lookup"><span data-stu-id="949e0-122">It should match a public virtual IP (VIP) address for one of the cloud services or websites in the Traffic Manager profile you are testing.</span></span>

## <a name="how-to-test-the-failover-traffic-routing-method"></a><span data-ttu-id="949e0-123">如何測試容錯移轉流量路由方法</span><span class="sxs-lookup"><span data-stu-id="949e0-123">How to test the failover traffic routing method</span></span>

1. <span data-ttu-id="949e0-124">保持所有端點運作。</span><span class="sxs-lookup"><span data-stu-id="949e0-124">Leave all endpoints up.</span></span>
2. <span data-ttu-id="949e0-125">在單一用戶端，使用 nslookup 或類似的公用程式要求公司網域名稱的 DNS 解析。</span><span class="sxs-lookup"><span data-stu-id="949e0-125">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="949e0-126">確定解析後的 IP 位址與您的主要端點相符。</span><span class="sxs-lookup"><span data-stu-id="949e0-126">Ensure that the resolved IP address matches the primary endpoint.</span></span>
4. <span data-ttu-id="949e0-127">關閉您的主要端點或移除監視檔案，所以流量管理員會認為應用程式已關閉。</span><span class="sxs-lookup"><span data-stu-id="949e0-127">Bring down your primary endpoint or remove the monitoring file so that Traffic Manager thinks that the application is down.</span></span>
5. <span data-ttu-id="949e0-128">等待時間為流量管理員設定檔的 DNS 存留時間 (TTL) 再加上 2 分鐘。</span><span class="sxs-lookup"><span data-stu-id="949e0-128">Wait for the DNS Time-to-Live (TTL) of the Traffic Manager profile plus an additional two minutes.</span></span> <span data-ttu-id="949e0-129">例如，若您的 DNS TTL 為 300 秒 (5 分鐘)，則您必須等待 7 分鐘。</span><span class="sxs-lookup"><span data-stu-id="949e0-129">For example, if your DNS TTL is 300 seconds (5 minutes), you must wait for seven minutes.</span></span>
6. <span data-ttu-id="949e0-130">排清您的 DNS 用戶端快取，使用 nslookup 要求 DNS 解析。</span><span class="sxs-lookup"><span data-stu-id="949e0-130">Flush your DNS client cache and request DNS resolution using nslookup.</span></span> <span data-ttu-id="949e0-131">在 Windows 中，您可以使用 ipconfig/flushdns 命令排清 DNS 快取。</span><span class="sxs-lookup"><span data-stu-id="949e0-131">In Windows, you can flush your DNS cache with the ipconfig /flushdns command.</span></span>
7. <span data-ttu-id="949e0-132">確定解析後的 IP 位址與您的次要端點相符。</span><span class="sxs-lookup"><span data-stu-id="949e0-132">Ensure that the resolved IP address matches your secondary endpoint.</span></span>
8. <span data-ttu-id="949e0-133">重複此程序，依序關閉每個端點。</span><span class="sxs-lookup"><span data-stu-id="949e0-133">Repeat the process, bringing down each endpoint in turn.</span></span> <span data-ttu-id="949e0-134">請確定 DNS 傳回清單中下一個端點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="949e0-134">Verify that the DNS returns the IP address of the next endpoint in the list.</span></span> <span data-ttu-id="949e0-135">關閉所有端點之後，您應可再次取得主要端點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="949e0-135">When all endpoints are down, you should obtain the IP address of the primary endpoint again.</span></span>

## <a name="how-to-test-the-weighted-traffic-routing-method"></a><span data-ttu-id="949e0-136">如何測試加權流量路由方法</span><span class="sxs-lookup"><span data-stu-id="949e0-136">How to test the weighted traffic routing method</span></span>

1. <span data-ttu-id="949e0-137">保持所有端點運作。</span><span class="sxs-lookup"><span data-stu-id="949e0-137">Leave all endpoints up.</span></span>
2. <span data-ttu-id="949e0-138">在單一用戶端，使用 nslookup 或類似的公用程式要求公司網域名稱的 DNS 解析。</span><span class="sxs-lookup"><span data-stu-id="949e0-138">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="949e0-139">確定解析後的 IP 位址與您的端點之一相符。</span><span class="sxs-lookup"><span data-stu-id="949e0-139">Ensure that the resolved IP address matches one of your endpoints.</span></span>
4. <span data-ttu-id="949e0-140">排清 DNS 用戶端快取，然後對每個端點重複步驟 2 和 3。</span><span class="sxs-lookup"><span data-stu-id="949e0-140">Flush your DNS client cache and repeat steps 2 and 3 for each endpoint.</span></span> <span data-ttu-id="949e0-141">您應該可看到為每個端點傳回不同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="949e0-141">You should see different IP addresses returned for each of your endpoints.</span></span>

## <a name="how-to-test-the-performance-traffic-routing-method"></a><span data-ttu-id="949e0-142">如何測試效能流量路由方法</span><span class="sxs-lookup"><span data-stu-id="949e0-142">How to test the performance traffic routing method</span></span>

<span data-ttu-id="949e0-143">若要有效地測試效能流量路由方法，您必須有個在位於世界上不同位置的用戶端。</span><span class="sxs-lookup"><span data-stu-id="949e0-143">To effectively test a performance traffic routing method, you must have clients located in different parts of the world.</span></span> <span data-ttu-id="949e0-144">您可以在不同 Azure 區域中建立用戶端以用來測試您的服務。</span><span class="sxs-lookup"><span data-stu-id="949e0-144">You can create clients in different Azure regions that can be used to test your services.</span></span> <span data-ttu-id="949e0-145">如果您有全域網路，可以從世界上的其他地方遠端登入用戶端，並從該處執行測試。</span><span class="sxs-lookup"><span data-stu-id="949e0-145">If you have a global network, you can remotely sign in to clients in other parts of the world and run your tests from there.</span></span>

<span data-ttu-id="949e0-146">或者，您可以找到免費的 Web 型 DNS 查閱和挖掘服務。</span><span class="sxs-lookup"><span data-stu-id="949e0-146">Alternatively, there are free web-based DNS lookup and dig services available.</span></span> <span data-ttu-id="949e0-147">其中一些工具提供您從全球不同位置檢查 DNS 名稱解析的能力。</span><span class="sxs-lookup"><span data-stu-id="949e0-147">Some of these tools give you the ability to check DNS name resolution from various locations around the world.</span></span> <span data-ttu-id="949e0-148">例如，搜尋 "DNS lookup" 相關資料。</span><span class="sxs-lookup"><span data-stu-id="949e0-148">Do a search on "DNS lookup" for examples.</span></span> <span data-ttu-id="949e0-149">協力廠商服務 (如 Gomez、Keynote) 可用於確認您的設定檔正如預期般分配流量。</span><span class="sxs-lookup"><span data-stu-id="949e0-149">Third-party services like Gomez or Keynote can be used to confirm that your profiles are distributing traffic as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="949e0-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="949e0-150">Next steps</span></span>

* [<span data-ttu-id="949e0-151">關於流量管理員流量路由方法</span><span class="sxs-lookup"><span data-stu-id="949e0-151">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="949e0-152">流量管理員的效能考量</span><span class="sxs-lookup"><span data-stu-id="949e0-152">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="949e0-153">疑難排解流量管理員的已降級狀態</span><span class="sxs-lookup"><span data-stu-id="949e0-153">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
