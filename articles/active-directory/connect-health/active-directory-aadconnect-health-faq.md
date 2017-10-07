---
title: "aaaAzure Active Directory 連線健全狀況常見問題集-Azure |Microsoft 文件"
description: "此常見問題集會回答 Azure AD Connect Health 的相關問題。 此常見問題集涵蓋使用 hello 服務，包括 hello 計費模型、 功能、 限制，以及支援的相關問題。"
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a><span data-ttu-id="f830a-104">Azure AD Connect Health 常見問題集</span><span class="sxs-lookup"><span data-stu-id="f830a-104">Azure AD Connect Health frequently asked questions</span></span>
<span data-ttu-id="f830a-105">這篇文章包含有關 Azure Active Directory (Azure AD) 連線的健康情況集 (faq) 解答 toofrequently。</span><span class="sxs-lookup"><span data-stu-id="f830a-105">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory (Azure AD) Connect Health.</span></span> <span data-ttu-id="f830a-106">這些常見問題集涵蓋疑問 toouse hello 服務，其中包括 hello 計費模型、 功能、 限制，以及支援的方式。</span><span class="sxs-lookup"><span data-stu-id="f830a-106">These FAQs cover questions about how toouse hello service, which includes hello billing model, capabilities, limitations, and support.</span></span>

## <a name="general-questions"></a><span data-ttu-id="f830a-107">一般問題</span><span class="sxs-lookup"><span data-stu-id="f830a-107">General questions</span></span>
<span data-ttu-id="f830a-108">**問：我管理多個 Azure AD 目錄。我要如何切換 toohello 具有 Azure Active Directory Premium？**</span><span class="sxs-lookup"><span data-stu-id="f830a-108">**Q: I manage multiple Azure AD directories. How do I switch toohello one that has Azure Active Directory Premium?**</span></span>

<span data-ttu-id="f830a-109">tooswitch 不同 Azure AD 租用戶，選取 hello 目前登入的**使用者名**在 hello 右上角，然後選擇 hello 適當的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f830a-109">tooswitch between different Azure AD tenants, select hello currently signed-in **User Name** on hello upper-right corner, and then choose hello appropriate account.</span></span> <span data-ttu-id="f830a-110">如果此處未列出 hello 帳戶，請選取**登出**，然後再使用 hello 全域系統管理員認證具有 Azure Active Directory Premium 的 hello 目錄啟用 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="f830a-110">If hello account is not listed here, select **Sign out**, and then use hello global admin credentials of hello directory that has Azure Active Directory Premium enabled toosign in.</span></span>

<span data-ttu-id="f830a-111">**問︰Azure AD Connect Health 支援哪個版本的身分識別角色？**</span><span class="sxs-lookup"><span data-stu-id="f830a-111">**Q: What version of identity roles are supported by Azure AD Connect Health?**</span></span>

<span data-ttu-id="f830a-112">hello 下表列出 hello 角色，並支援的作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="f830a-112">hello following table lists hello roles and supported operating system versions.</span></span>

|<span data-ttu-id="f830a-113">角色</span><span class="sxs-lookup"><span data-stu-id="f830a-113">Role</span></span>| <span data-ttu-id="f830a-114">作業系統/版本</span><span class="sxs-lookup"><span data-stu-id="f830a-114">Operating system / Version</span></span>|
|--|--|
|<span data-ttu-id="f830a-115">Active Directory Federation Services (AD FS)</span><span class="sxs-lookup"><span data-stu-id="f830a-115">Active Directory Federation Services (AD FS)</span></span>| <ul> <li> <span data-ttu-id="f830a-116">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="f830a-116">Windows Server 2008 R2</span></span> </li><li> <span data-ttu-id="f830a-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f830a-117">Windows Server 2012</span></span>  </li> <li><span data-ttu-id="f830a-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f830a-118">Windows Server 2012 R2</span></span> </li> <li> <span data-ttu-id="f830a-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f830a-119">Windows Server 2016</span></span>  </li> </ul>|
|<span data-ttu-id="f830a-120">Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f830a-120">Azure AD Connect</span></span> | <span data-ttu-id="f830a-121">版本 1.0.9125 或更高版本</span><span class="sxs-lookup"><span data-stu-id="f830a-121">Version 1.0.9125 or higher</span></span>|
|<span data-ttu-id="f830a-122">Active Directory Domain Services (AD DS)</span><span class="sxs-lookup"><span data-stu-id="f830a-122">Active Directory Domain Services (AD DS)</span></span>| <ul> <li> <span data-ttu-id="f830a-123">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="f830a-123">Windows Server 2008 R2</span></span> </li><li> <span data-ttu-id="f830a-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f830a-124">Windows Server 2012</span></span>  </li> <li><span data-ttu-id="f830a-125">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f830a-125">Windows Server 2012 R2</span></span> </li> <li> <span data-ttu-id="f830a-126">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f830a-126">Windows Server 2016</span></span>  </li> </ul>|

<span data-ttu-id="f830a-127">請注意 hello hello 服務所提供的功能可能不同，根據 hello 角色和 hello 作業系統而不同。</span><span class="sxs-lookup"><span data-stu-id="f830a-127">Note that hello features provided by hello service may differ based on hello role and hello operating system.</span></span> <span data-ttu-id="f830a-128">換句話說，所有 hello 功能可能無法供所有作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="f830a-128">In other words, all hello features may not be available for all operating system versions.</span></span> <span data-ttu-id="f830a-129">請參閱 hello 功能描述，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f830a-129">See hello feature descriptions for details.</span></span>

<span data-ttu-id="f830a-130">**問： 如何授權執行我的基礎結構需要 toomonitor？**</span><span class="sxs-lookup"><span data-stu-id="f830a-130">**Q: How many licenses do I need toomonitor my infrastructure?**</span></span>

* <span data-ttu-id="f830a-131">hello 第一個 Connect Health 代理程式需要至少一個 Azure AD Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="f830a-131">hello first Connect Health Agent requires at least one Azure AD Premium license.</span></span>
* <span data-ttu-id="f830a-132">每多一個註冊代理程式，就需要再 25 個 Azure AD Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="f830a-132">Each additional registered agent requires 25 additional Azure AD Premium licenses.</span></span>
* <span data-ttu-id="f830a-133">代理程式計數是跨越所有受監視的角色 （AD FS、 Azure AD Connect，及/或 AD DS） 中註冊的代理程式的對等 toohello 總數。</span><span class="sxs-lookup"><span data-stu-id="f830a-133">Agent count is equivalent toohello total number of agents that are registered across all monitored roles (AD FS, Azure AD Connect, and/or AD DS).</span></span>

<span data-ttu-id="f830a-134">授權資訊也可以找到上 hello [Azure AD 定價頁面](https://aka.ms/aadpricing)。</span><span class="sxs-lookup"><span data-stu-id="f830a-134">Licensing information is also found on hello [Azure AD Pricing page](https://aka.ms/aadpricing).</span></span>

<span data-ttu-id="f830a-135">範例：</span><span class="sxs-lookup"><span data-stu-id="f830a-135">Example:</span></span>

| <span data-ttu-id="f830a-136">已註冊的代理程式</span><span class="sxs-lookup"><span data-stu-id="f830a-136">Registered agents</span></span> | <span data-ttu-id="f830a-137">需要的授權</span><span class="sxs-lookup"><span data-stu-id="f830a-137">Licenses needed</span></span> | <span data-ttu-id="f830a-138">監視組態範例</span><span class="sxs-lookup"><span data-stu-id="f830a-138">Example monitoring configuration</span></span> |
| ------ | --------------- | --- |
| <span data-ttu-id="f830a-139">1</span><span class="sxs-lookup"><span data-stu-id="f830a-139">1</span></span> | <span data-ttu-id="f830a-140">1</span><span class="sxs-lookup"><span data-stu-id="f830a-140">1</span></span> | <span data-ttu-id="f830a-141">1 個 Azure AD Connect 伺服器</span><span class="sxs-lookup"><span data-stu-id="f830a-141">1 Azure AD Connect server</span></span> |
| <span data-ttu-id="f830a-142">2</span><span class="sxs-lookup"><span data-stu-id="f830a-142">2</span></span> | <span data-ttu-id="f830a-143">26</span><span class="sxs-lookup"><span data-stu-id="f830a-143">26</span></span>| <span data-ttu-id="f830a-144">1 個 Azure AD Connect 伺服器、1 個網域控制站</span><span class="sxs-lookup"><span data-stu-id="f830a-144">1 Azure AD Connect server and 1 domain controller</span></span> |
| <span data-ttu-id="f830a-145">3</span><span class="sxs-lookup"><span data-stu-id="f830a-145">3</span></span> | <span data-ttu-id="f830a-146">51</span><span class="sxs-lookup"><span data-stu-id="f830a-146">51</span></span> | <span data-ttu-id="f830a-147">1 個 Active Directory Federation Services (AD FS) 伺服器、1 個 AD FS Proxy、1 個網域控制站</span><span class="sxs-lookup"><span data-stu-id="f830a-147">1 Active Directory Federation Services (AD FS) server, 1 AD FS proxy, and 1 domain controller</span></span> |
| <span data-ttu-id="f830a-148">4</span><span class="sxs-lookup"><span data-stu-id="f830a-148">4</span></span> | <span data-ttu-id="f830a-149">76</span><span class="sxs-lookup"><span data-stu-id="f830a-149">76</span></span> | <span data-ttu-id="f830a-150">1 個 AD FS 伺服器、1 個 AD FS Proxy、2 個網域控制站</span><span class="sxs-lookup"><span data-stu-id="f830a-150">1 AD FS server, 1 AD FS proxy, and 2 domain controllers</span></span> |
| <span data-ttu-id="f830a-151">5</span><span class="sxs-lookup"><span data-stu-id="f830a-151">5</span></span> | <span data-ttu-id="f830a-152">101</span><span class="sxs-lookup"><span data-stu-id="f830a-152">101</span></span> | <span data-ttu-id="f830a-153">1 個 Azure AD Connect 伺服器、1 個 AD FS 伺服器、1 個 AD FS Proxy、2 個網域控制站</span><span class="sxs-lookup"><span data-stu-id="f830a-153">1 Azure AD Connect server, 1 AD FS server, 1 AD FS proxy, and 2 domain controllers</span></span> |


## <a name="installation-questions"></a><span data-ttu-id="f830a-154">安裝問題</span><span class="sxs-lookup"><span data-stu-id="f830a-154">Installation questions</span></span>

<span data-ttu-id="f830a-155">**問： hello 的 hello Azure AD Connect Health 代理程式安裝在個別伺服器上的影響為何？**</span><span class="sxs-lookup"><span data-stu-id="f830a-155">**Q: What is hello impact of installing hello Azure AD Connect Health Agent on individual servers?**</span></span>

<span data-ttu-id="f830a-156">與尊重 toohello CPU、 記憶體耗用量、 網路頻寬和儲存體最小的 hello 影響安裝 hello Microsoft Azure AD Connect Health 代理程式，AD FS web 應用程式 proxy 伺服器，Azure AD Connect （同步） 伺服器、 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="f830a-156">hello impact of installing hello Microsoft Azure AD Connect Health Agent, AD FS, web application proxy servers, Azure AD Connect (sync) servers, domain controllers is minimal with respect toohello CPU, memory consumption, network bandwidth, and storage.</span></span>

<span data-ttu-id="f830a-157">下列數字的 hello 是近似值：</span><span class="sxs-lookup"><span data-stu-id="f830a-157">hello following numbers are an approximation:</span></span>

* <span data-ttu-id="f830a-158">CPU 耗用量：增加約 1-5%。</span><span class="sxs-lookup"><span data-stu-id="f830a-158">CPU consumption: ~1-5% increase.</span></span>
* <span data-ttu-id="f830a-159">記憶體耗用量： too10%的 hello 系統總記憶體。</span><span class="sxs-lookup"><span data-stu-id="f830a-159">Memory consumption: Up too10 % of hello total system memory.</span></span>

> [!NOTE]
> <span data-ttu-id="f830a-160">如果 hello 代理程式無法與 Azure 通訊，hello 代理程式會儲存 hello 資料在本機定義的最大限制。</span><span class="sxs-lookup"><span data-stu-id="f830a-160">If hello agent cannot communicate with Azure, hello agent stores hello data locally for a defined maximum limit.</span></span> <span data-ttu-id="f830a-161">hello 代理程式會覆寫 hello 「 快取 」 的資料，「 最近最少服務 」 為基礎。</span><span class="sxs-lookup"><span data-stu-id="f830a-161">hello agent overwrites hello “cached” data on a “least recently serviced” basis.</span></span>
>
>

* <span data-ttu-id="f830a-162">Azure AD Connect Health 代理程式的本機緩衝區儲存體：約 20 MB。</span><span class="sxs-lookup"><span data-stu-id="f830a-162">Local buffer storage for Azure AD Connect Health Agents: ~20 MB.</span></span>
* <span data-ttu-id="f830a-163">AD FS 伺服器，我們建議，您佈建 Azure AD Connect Health 代理程式 tooprocess 的 hello AD FS 稽核通道 1024 MB (1 GB) 的磁碟空間 hello 的所有稽核資料之前會覆寫。</span><span class="sxs-lookup"><span data-stu-id="f830a-163">For AD FS servers, we recommend that you provision a disk space of 1,024 MB (1 GB) for hello AD FS audit channel for Azure AD Connect Health Agents tooprocess all hello audit data before it is overwritten.</span></span>

<span data-ttu-id="f830a-164">**問： 我可以 tooreboot 我的伺服器 hello hello Azure AD Connect Health 代理程式安裝期間嗎？**</span><span class="sxs-lookup"><span data-stu-id="f830a-164">**Q: Will I have tooreboot my servers during hello installation of hello Azure AD Connect Health Agents?**</span></span>

<span data-ttu-id="f830a-165">否。</span><span class="sxs-lookup"><span data-stu-id="f830a-165">No.</span></span> <span data-ttu-id="f830a-166">hello 安裝 hello 代理程式不會要求您 tooreboot hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f830a-166">hello installation of hello agents will not require you tooreboot hello server.</span></span> <span data-ttu-id="f830a-167">不過，某些先決條件步驟的安裝可能需要 hello 伺服器重新的開機。</span><span class="sxs-lookup"><span data-stu-id="f830a-167">However, installation of some prerequisite steps might require a reboot of hello server.</span></span>

<span data-ttu-id="f830a-168">例如，在 Windows Server 2008 R2 上安裝 .NET 4.5 Framework 需要重新啟動伺服器。</span><span class="sxs-lookup"><span data-stu-id="f830a-168">For example, on Windows Server 2008 R2, installation of .NET 4.5 Framework requires a server reboot.</span></span>

<span data-ttu-id="f830a-169">**問：Azure AD Connect Health 是否透過傳遞 Http Proxy 運作？**</span><span class="sxs-lookup"><span data-stu-id="f830a-169">**Q: Does Azure AD Connect Health work through a pass-through HTTP proxy?**</span></span>

<span data-ttu-id="f830a-170">是。</span><span class="sxs-lookup"><span data-stu-id="f830a-170">Yes.</span></span> <span data-ttu-id="f830a-171">針對進行中操作，您可以設定 hello 健康情況代理程式 toouse HTTP proxy tooforward 傳出 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="f830a-171">For ongoing operations, you can configure hello Health Agent toouse an HTTP proxy tooforward outbound HTTP requests.</span></span>
<span data-ttu-id="f830a-172">深入了解[設定 Health 代理程式的 HTTP Proxy](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy)。</span><span class="sxs-lookup"><span data-stu-id="f830a-172">Read more about [configuring HTTP Proxy for Health Agents](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).</span></span>

<span data-ttu-id="f830a-173">如果您需要 tooconfigure proxy 代理程式註冊期間，您可能需要 toomodify Internet Explorer Proxy 設定事先。</span><span class="sxs-lookup"><span data-stu-id="f830a-173">If you need tooconfigure a proxy during agent registration, you might need toomodify your Internet Explorer Proxy settings beforehand.</span></span>

1. <span data-ttu-id="f830a-174">開啟 Internet Explorer > [設定]  >  [網際網路選項]  >  [連線]  >  [LAN 設定]。</span><span class="sxs-lookup"><span data-stu-id="f830a-174">Open Internet Explorer > **Settings** > **Internet Options** > **Connections** > **LAN Settings**.</span></span>
2. <span data-ttu-id="f830a-175">選取 [在您的區域網路使用 Proxy 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="f830a-175">Select **Use a Proxy Server for your LAN**.</span></span>
3. <span data-ttu-id="f830a-176">如果您有不同的 Proxy 連接埠供 HTTP 和 HTTPS/安全使用，請選取 [進階]。</span><span class="sxs-lookup"><span data-stu-id="f830a-176">Select **Advanced** if you have different proxy ports for HTTP and HTTPS/Secure.</span></span>

<span data-ttu-id="f830a-177">**問： 沒有 Azure AD Connect Health 支援基本驗證連接 tooHTTP proxy 時？**</span><span class="sxs-lookup"><span data-stu-id="f830a-177">**Q: Does Azure AD Connect Health support Basic authentication when connecting tooHTTP proxies?**</span></span>

<span data-ttu-id="f830a-178">否。</span><span class="sxs-lookup"><span data-stu-id="f830a-178">No.</span></span> <span data-ttu-id="f830a-179">機制 toospecify 任意使用者名稱和密碼進行基本驗證目前不支援。</span><span class="sxs-lookup"><span data-stu-id="f830a-179">A mechanism toospecify an arbitrary user name and password for Basic authentication is not currently supported.</span></span>

<span data-ttu-id="f830a-180">**問： 哪些防火牆連接埠是否需要 hello Azure AD Connect Health 代理程式 toowork tooopen 嗎？**</span><span class="sxs-lookup"><span data-stu-id="f830a-180">**Q: What firewall ports do I need tooopen for hello Azure AD Connect Health Agent toowork?**</span></span>

<span data-ttu-id="f830a-181">請參閱 hello[需求 > 一節](active-directory-aadconnect-health-agent-install.md#requirements)hello 清單的防火牆連接埠與其他連線的需求。</span><span class="sxs-lookup"><span data-stu-id="f830a-181">See hello [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for hello list of firewall ports and other connectivity requirements.</span></span>

<span data-ttu-id="f830a-182">**問： 為什麼看兩部伺服器以相同的名稱，在 hello Azure AD Connect Health 入口網站中的 hello？**</span><span class="sxs-lookup"><span data-stu-id="f830a-182">**Q: Why do I see two servers with hello same name in hello Azure AD Connect Health portal?**</span></span>

<span data-ttu-id="f830a-183">當您從伺服器移除代理程式時，hello 伺服器是不會自動移除 hello Azure AD Connect Health 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f830a-183">When you remove an agent from a server, hello server is not automatically removed from hello Azure AD Connect Health portal.</span></span> <span data-ttu-id="f830a-184">如果您以手動方式從伺服器移除代理程式，或移除 hello 伺服器本身，您會需要 toomanually 刪除 hello 伺服器項目從 hello Azure AD Connect Health 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f830a-184">If you manually remove an agent from a server or remove hello server itself, you need toomanually delete hello server entry from hello Azure AD Connect Health portal.</span></span>

<span data-ttu-id="f830a-185">您可能會在伺服器重新製作映像，或建立新的伺服器 hello 與相同的詳細資訊 （例如電腦名稱）。</span><span class="sxs-lookup"><span data-stu-id="f830a-185">You might reimage a server or create a new server with hello same details (such as machine name).</span></span> <span data-ttu-id="f830a-186">如果您並未從 hello Azure AD Connect Health 入口網站中，移除 hello 已註冊的伺服器，而且您 hello 新的伺服器上安裝 hello 代理程式，您可能會看到兩個項目以 hello 相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="f830a-186">If you did not remove hello already registered server from hello Azure AD Connect Health portal, and you installed hello agent on hello new server, you might see two entries with hello same name.</span></span>

<span data-ttu-id="f830a-187">在此情況下，手動刪除屬於 toohello 舊伺服器 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="f830a-187">In this case, manually delete hello entry that belongs toohello older server.</span></span> <span data-ttu-id="f830a-188">此伺服器 hello 資料應過期。</span><span class="sxs-lookup"><span data-stu-id="f830a-188">hello data for this server should be out of date.</span></span>

## <a name="health-agent-registration-and-data-freshness"></a><span data-ttu-id="f830a-189">Health 代理程式註冊和資料有效性</span><span class="sxs-lookup"><span data-stu-id="f830a-189">Health Agent registration and data freshness</span></span>

<span data-ttu-id="f830a-190">**問： 什麼是 hello 健全狀況代理程式註冊失敗的常見原因，以及如何疑難排解問題？**</span><span class="sxs-lookup"><span data-stu-id="f830a-190">**Q: What are common reasons for hello Health Agent registration failures and how do I troubleshoot issues?**</span></span>

<span data-ttu-id="f830a-191">hello 健康情況代理程式可能會失敗 tooregister 到期 toohello 下列可能的原因：</span><span class="sxs-lookup"><span data-stu-id="f830a-191">hello health agent can fail tooregister due toohello following possible reasons:</span></span>

* <span data-ttu-id="f830a-192">hello 代理程式無法與所需的 hello 端點通訊，因為防火牆封鎖流量。</span><span class="sxs-lookup"><span data-stu-id="f830a-192">hello agent cannot communicate with hello required endpoints because a firewall is blocking traffic.</span></span> <span data-ttu-id="f830a-193">在 Web 應用程式 Proxy 伺服器上尤其常見。</span><span class="sxs-lookup"><span data-stu-id="f830a-193">This is particularly common on web application proxy servers.</span></span> <span data-ttu-id="f830a-194">請確定您已允許連出通訊所需的 toohello 端點及連接埠。</span><span class="sxs-lookup"><span data-stu-id="f830a-194">Make sure that you have allowed outbound communication toohello required endpoints and ports.</span></span> <span data-ttu-id="f830a-195">請參閱 hello[需求 > 一節](active-directory-aadconnect-health-agent-install.md#requirements)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f830a-195">See hello [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for details.</span></span>
* <span data-ttu-id="f830a-196">連出通訊是由 hello 網路層膨脹 tooan SSL 檢查。</span><span class="sxs-lookup"><span data-stu-id="f830a-196">Outbound communication is subjected tooan SSL inspection by hello network layer.</span></span> <span data-ttu-id="f830a-197">這會導致 hello 憑證 hello 代理程式會使用 toobe 取代 hello 檢查伺服器/實體，然後 hello 步驟 toocomplete hello 代理程式註冊失敗。</span><span class="sxs-lookup"><span data-stu-id="f830a-197">This causes hello certificate that hello agent uses toobe replaced by hello inspection server/entity, and hello steps toocomplete hello agent registration fail.</span></span>
* <span data-ttu-id="f830a-198">hello 使用者沒有存取 tooperform hello 登錄 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="f830a-198">hello user does not have access tooperform hello registration of hello agent.</span></span> <span data-ttu-id="f830a-199">根據預設，全域系統管理員具有存取權。</span><span class="sxs-lookup"><span data-stu-id="f830a-199">Global admins have access by default.</span></span> <span data-ttu-id="f830a-200">您可以使用[Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate 存取 tooother 使用者。</span><span class="sxs-lookup"><span data-stu-id="f830a-200">You can use [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate access tooother users.</span></span>

<span data-ttu-id="f830a-201">**問： 我已開始收到警示，「 健全狀況服務的資料不是向上 toodate。 」如何疑難排解 hello 問題？**</span><span class="sxs-lookup"><span data-stu-id="f830a-201">**Q: I am getting alerted that "Health Service data is not up toodate." How do I troubleshoot hello issue?**</span></span>

<span data-ttu-id="f830a-202">它不會收到 hello 的所有資料點 hello 伺服器 hello 中最後兩小時時，azure AD Connect Health 便會產生 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="f830a-202">Azure AD Connect Health generates hello alert when it does not receive all hello data points from hello server in hello last two hours.</span></span> <span data-ttu-id="f830a-203">有很多原因都可能導致引發此警示。</span><span class="sxs-lookup"><span data-stu-id="f830a-203">There can be multiple reasons for this alert.</span></span>

* <span data-ttu-id="f830a-204">hello 代理程式無法與所需的 hello 端點通訊，因為防火牆封鎖流量。</span><span class="sxs-lookup"><span data-stu-id="f830a-204">hello agent cannot communicate with hello required endpoints because a firewall is blocking traffic.</span></span> <span data-ttu-id="f830a-205">在 Web 應用程式 Proxy 伺服器上尤其常見。</span><span class="sxs-lookup"><span data-stu-id="f830a-205">This is particularly common on web application proxy servers.</span></span> <span data-ttu-id="f830a-206">請確定您已允許連出通訊所需的 toohello 結束點及連接埠。</span><span class="sxs-lookup"><span data-stu-id="f830a-206">Make sure that you have allowed outbound communication toohello required end points and ports.</span></span> <span data-ttu-id="f830a-207">請參閱 hello[需求 > 一節](active-directory-aadconnect-health-agent-install.md#requirements)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f830a-207">See hello [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for details.</span></span>
* <span data-ttu-id="f830a-208">連出通訊是由 hello 網路層膨脹 tooan SSL 檢查。</span><span class="sxs-lookup"><span data-stu-id="f830a-208">Outbound communication is subjected tooan SSL inspection by hello network layer.</span></span> <span data-ttu-id="f830a-209">這會導致 hello 憑證 hello 代理程式會使用 toobe 取代 hello 檢查伺服器/實體，然後 hello 程序失敗 tooupload 資料 toohello Azure AD Connect Health 服務。</span><span class="sxs-lookup"><span data-stu-id="f830a-209">This causes hello certificate that hello agent uses toobe replaced by hello inspection server/entity, and hello process fails tooupload data toohello Azure AD Connect Health service.</span></span>
* <span data-ttu-id="f830a-210">您可以使用內建 hello 代理程式的 hello 連線命令。</span><span class="sxs-lookup"><span data-stu-id="f830a-210">You can use hello connectivity command built into hello agent.</span></span> <span data-ttu-id="f830a-211">[閱讀更多資訊](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)。</span><span class="sxs-lookup"><span data-stu-id="f830a-211">[Read more](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).</span></span>
* <span data-ttu-id="f830a-212">hello 代理程式也支援透過未經驗證的 HTTP Proxy 的傳出連線。</span><span class="sxs-lookup"><span data-stu-id="f830a-212">hello agents also support outbound connectivity via an unauthenticated HTTP Proxy.</span></span> <span data-ttu-id="f830a-213">[閱讀更多資訊](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy)。</span><span class="sxs-lookup"><span data-stu-id="f830a-213">[Read more](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).</span></span>

## <a name="operations-questions"></a><span data-ttu-id="f830a-214">操作問題</span><span class="sxs-lookup"><span data-stu-id="f830a-214">Operations questions</span></span>
<span data-ttu-id="f830a-215">**問： 我需要 tooenable hello web 應用程式 proxy 伺服器上的稽核嗎？**</span><span class="sxs-lookup"><span data-stu-id="f830a-215">**Q: Do I need tooenable auditing on hello web application proxy servers?**</span></span>

<span data-ttu-id="f830a-216">否，稽核不需要 toobe hello web 應用程式 proxy 伺服器上啟用。</span><span class="sxs-lookup"><span data-stu-id="f830a-216">No, auditing does not need toobe enabled on hello web application proxy servers.</span></span>

<span data-ttu-id="f830a-217">**問：Azure AD Connect Health 警示如何獲得解決？**</span><span class="sxs-lookup"><span data-stu-id="f830a-217">**Q: How do Azure AD Connect Health Alerts get resolved?**</span></span>

<span data-ttu-id="f830a-218">Azure AD Connect Health 警示會在成功情況下獲得解決。</span><span class="sxs-lookup"><span data-stu-id="f830a-218">Azure AD Connect Health alerts get resolved on a success condition.</span></span> <span data-ttu-id="f830a-219">Azure AD Connect Health 代理程式偵測，並定期報告 hello 成功條件 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="f830a-219">Azure AD Connect Health Agents detect and report hello success conditions toohello service periodically.</span></span> <span data-ttu-id="f830a-220">有幾項警示的 hello 隱藏項目是以時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="f830a-220">For a few alerts, hello suppression is time-based.</span></span> <span data-ttu-id="f830a-221">換句話說，如果 hello 相同錯誤狀況未觀察到的警示產生 72 個小時內，會自動解決 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="f830a-221">In other words, if hello same error condition is not observed within 72 hours from alert generation, hello alert is automatically resolved.</span></span>

<span data-ttu-id="f830a-222">**問： 我已開始收到警示，「 測試驗證要求 （綜合交易） 無法 tooobtain 語彙基元。 」如何疑難排解 hello 問題？**</span><span class="sxs-lookup"><span data-stu-id="f830a-222">**Q: I am getting alerted that "Test Authentication Request (Synthetic Transaction) failed tooobtain a token." How do I troubleshoot hello issue?**</span></span>

<span data-ttu-id="f830a-223">Hello 安裝 AD FS 伺服器上的健全狀況代理程式失敗 tooobtain 權杖做為起始的 hello 健康情況代理程式的綜合交易的一部分時，azure AD Connect Health 的 AD FS 會產生此警示。</span><span class="sxs-lookup"><span data-stu-id="f830a-223">Azure AD Connect Health for AD FS generates this alert when hello Health Agent installed on an AD FS server fails tooobtain a token as part of a synthetic transaction initiated by hello Health Agent.</span></span> <span data-ttu-id="f830a-224">hello 健康情況代理程式會使用 hello 本機系統內容，並嘗試本身的信賴憑證者合作對象 tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f830a-224">hello Health agent uses hello local system context and attempts tooget a token for a self relying party.</span></span> <span data-ttu-id="f830a-225">這是所有測試 tooensure AD FS 已發行權杖的狀態。</span><span class="sxs-lookup"><span data-stu-id="f830a-225">This is a catch-all test tooensure that AD FS is in a state of issuing tokens.</span></span>

<span data-ttu-id="f830a-226">通常這項測試失敗，因為 hello 健康情況代理程式是無法 tooresolve hello AD FS 伺服器陣列名稱。</span><span class="sxs-lookup"><span data-stu-id="f830a-226">Most often this test fails because hello Health Agent is unable tooresolve hello AD FS farm name.</span></span> <span data-ttu-id="f830a-227">這種情況 hello AD FS 伺服器是網路負載平衡器後方，而且 hello 要求取得初始化的節點為 hello 負載平衡器後方 （相對於的 tooa 一般用戶端 hello 負載平衡器前面）。</span><span class="sxs-lookup"><span data-stu-id="f830a-227">This can happen if hello AD FS servers are behind a network load balancers and hello request gets initiated from a node that's behind hello load balancer (as opposed tooa regular client that is in front of hello load balancer).</span></span> <span data-ttu-id="f830a-228">這可以藉由修復更新 hello"hosts"檔案位於"C:\Windows\System32\drivers\etc"tooinclude hello 的 hello AD FS 伺服器的 IP 位址或回送 IP 位址 (127.0.0.1) hello AD FS 伺服器陣列名稱 （例如，sts.contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="f830a-228">This can be fixed by updating hello "hosts" file located under "C:\Windows\System32\drivers\etc" tooinclude hello IP address of hello AD FS server or a loopback IP address (127.0.0.1) for hello AD FS farm name (such as sts.contoso.com).</span></span> <span data-ttu-id="f830a-229">加入 hello 主機檔案，將會最少運算 hello 的網路呼叫，進而 hello 健康情況代理程式 tooget hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f830a-229">Adding hello host file will short-circuit hello network call, thus allowing hello Health Agent tooget hello token.</span></span>

<span data-ttu-id="f830a-230">**問： 我收到一封電子郵件，指出 我的電腦不修補 hello 最近 ransomeware 攻擊。我為什麼收到這封電子郵件？**</span><span class="sxs-lookup"><span data-stu-id="f830a-230">**Q: I got an email indicating my machines are NOT patched for hello recent ransomeware attacks. Why did I receive this email?**</span></span>

<span data-ttu-id="f830a-231">Azure AD Connect Health 服務掃描它會監視 tooensure hello 所需的修補程式的電腦已安裝的所有 hello。</span><span class="sxs-lookup"><span data-stu-id="f830a-231">Azure AD Connect Health service scanned all hello machines it monitors tooensure hello required patches were installed.</span></span> <span data-ttu-id="f830a-232">hello 電子郵件已傳送 toohello 租用戶系統管理員，如果至少一部電腦沒有 hello 的重大修補程式。</span><span class="sxs-lookup"><span data-stu-id="f830a-232">hello email was sent toohello tenant administrators if at least one machine did not have hello critical patches.</span></span> <span data-ttu-id="f830a-233">下列邏輯 hello 已使用的 toomake 這項判斷。</span><span class="sxs-lookup"><span data-stu-id="f830a-233">hello following logic was used toomake this determination.</span></span>
1. <span data-ttu-id="f830a-234">尋找所有 hello hotfix 安裝在 hello 電腦上。</span><span class="sxs-lookup"><span data-stu-id="f830a-234">Find all hello hotfixes installed on hello machine.</span></span>
2. <span data-ttu-id="f830a-235">檢查是否至少一個從 hello hello Hotfix 定義清單會出現。</span><span class="sxs-lookup"><span data-stu-id="f830a-235">Check if at least one of hello HotFixes from hello defined list is present.</span></span>
3. <span data-ttu-id="f830a-236">如果是，hello 機器已受保護。</span><span class="sxs-lookup"><span data-stu-id="f830a-236">If Yes, hello machine is protected.</span></span> <span data-ttu-id="f830a-237">如果沒有，hello 機器位於 hello 攻擊的風險。</span><span class="sxs-lookup"><span data-stu-id="f830a-237">If Not, hello machine is at risk for hello attack.</span></span>

<span data-ttu-id="f830a-238">您可以使用下列 PowerShell 指令碼 tooperform hello 這個核取以手動方式。</span><span class="sxs-lookup"><span data-stu-id="f830a-238">You can use hello following PowerShell script tooperform this check manually.</span></span> <span data-ttu-id="f830a-239">它會實作 hello 上方邏輯。</span><span class="sxs-lookup"><span data-stu-id="f830a-239">It implements hello above logic.</span></span>

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a><span data-ttu-id="f830a-240">相關連結</span><span class="sxs-lookup"><span data-stu-id="f830a-240">Related links</span></span>
* [<span data-ttu-id="f830a-241">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="f830a-241">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="f830a-242">Azure AD Connect Health 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="f830a-242">Azure AD Connect Health Agent installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="f830a-243">Azure AD Connect Health 操作</span><span class="sxs-lookup"><span data-stu-id="f830a-243">Azure AD Connect Health operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="f830a-244">在 AD FS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="f830a-244">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="f830a-245">使用 Azure AD Connect Health 進行同步處理</span><span class="sxs-lookup"><span data-stu-id="f830a-245">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="f830a-246">在 AD DS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="f830a-246">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="f830a-247">Azure AD Connect Health 版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="f830a-247">Azure AD Connect Health version history</span></span>](active-directory-aadconnect-health-version-history.md)
