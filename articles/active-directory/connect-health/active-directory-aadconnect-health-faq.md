---
title: "Azure Active Directory Connect Health 常見問題集 - Azure | Microsoft Docs"
description: "此常見問題集會回答 Azure AD Connect Health 的相關問題。 這個常見問題集涵蓋使用服務的相關問題，包括計費模型、功能、限制及支援。"
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
ms.openlocfilehash: 902e5bdfbbf04ab70989be8c41e16eb69e475908
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a><span data-ttu-id="76be3-104">Azure AD Connect Health 常見問題集</span><span class="sxs-lookup"><span data-stu-id="76be3-104">Azure AD Connect Health frequently asked questions</span></span>
<span data-ttu-id="76be3-105">本文會回答有關 Azure Active Directory (Azure AD) Connect Health 的常見問題 (FAQ)。</span><span class="sxs-lookup"><span data-stu-id="76be3-105">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory (Azure AD) Connect Health.</span></span> <span data-ttu-id="76be3-106">這些常見問題涵蓋如何使用服務的相關問題，包括計費模型、功能、限制及支援。</span><span class="sxs-lookup"><span data-stu-id="76be3-106">These FAQs cover questions about how to use the service, which includes the billing model, capabilities, limitations, and support.</span></span>

## <a name="general-questions"></a><span data-ttu-id="76be3-107">一般問題</span><span class="sxs-lookup"><span data-stu-id="76be3-107">General questions</span></span>
<span data-ttu-id="76be3-108">**問：我管理多個 Azure AD 目錄。我如何切換到包含 Azure Active Directory Premium 的租用戶？**</span><span class="sxs-lookup"><span data-stu-id="76be3-108">**Q: I manage multiple Azure AD directories. How do I switch to the one that has Azure Active Directory Premium?**</span></span>

<span data-ttu-id="76be3-109">若要在不同的 Azure AD 租用戶之間切換，請在右上角選取目前登入的 [使用者名稱]，然後選擇適當的帳戶。</span><span class="sxs-lookup"><span data-stu-id="76be3-109">To switch between different Azure AD tenants, select the currently signed-in **User Name** on the upper-right corner, and then choose the appropriate account.</span></span> <span data-ttu-id="76be3-110">如果此處未列出帳戶，請選取 [登出]，然後使用已啟用 Azure Active Directory Premium 之目錄的全域系統管理員認證登入。</span><span class="sxs-lookup"><span data-stu-id="76be3-110">If the account is not listed here, select **Sign out**, and then use the global admin credentials of the directory that has Azure Active Directory Premium enabled to sign in.</span></span>

<span data-ttu-id="76be3-111">**問︰Azure AD Connect Health 支援哪個版本的身分識別角色？**</span><span class="sxs-lookup"><span data-stu-id="76be3-111">**Q: What version of identity roles are supported by Azure AD Connect Health?**</span></span>

<span data-ttu-id="76be3-112">下表列出各角色與支援的作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="76be3-112">The following table lists the roles and supported operating system versions.</span></span>

|<span data-ttu-id="76be3-113">角色</span><span class="sxs-lookup"><span data-stu-id="76be3-113">Role</span></span>| <span data-ttu-id="76be3-114">作業系統/版本</span><span class="sxs-lookup"><span data-stu-id="76be3-114">Operating system / Version</span></span>|
|--|--|
|<span data-ttu-id="76be3-115">Active Directory Federation Services (AD FS)</span><span class="sxs-lookup"><span data-stu-id="76be3-115">Active Directory Federation Services (AD FS)</span></span>| <ul> <li> <span data-ttu-id="76be3-116">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="76be3-116">Windows Server 2008 R2</span></span> </li><li> <span data-ttu-id="76be3-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="76be3-117">Windows Server 2012</span></span>  </li> <li><span data-ttu-id="76be3-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="76be3-118">Windows Server 2012 R2</span></span> </li> <li> <span data-ttu-id="76be3-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="76be3-119">Windows Server 2016</span></span>  </li> </ul>|
|<span data-ttu-id="76be3-120">Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="76be3-120">Azure AD Connect</span></span> | <span data-ttu-id="76be3-121">版本 1.0.9125 或更高版本</span><span class="sxs-lookup"><span data-stu-id="76be3-121">Version 1.0.9125 or higher</span></span>|
|<span data-ttu-id="76be3-122">Active Directory Domain Services (AD DS)</span><span class="sxs-lookup"><span data-stu-id="76be3-122">Active Directory Domain Services (AD DS)</span></span>| <ul> <li> <span data-ttu-id="76be3-123">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="76be3-123">Windows Server 2008 R2</span></span> </li><li> <span data-ttu-id="76be3-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="76be3-124">Windows Server 2012</span></span>  </li> <li><span data-ttu-id="76be3-125">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="76be3-125">Windows Server 2012 R2</span></span> </li> <li> <span data-ttu-id="76be3-126">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="76be3-126">Windows Server 2016</span></span>  </li> </ul>|

<span data-ttu-id="76be3-127">請注意，服務所提供的功能可能會因為角色和作業系統而有所不同。</span><span class="sxs-lookup"><span data-stu-id="76be3-127">Note that the features provided by the service may differ based on the role and the operating system.</span></span> <span data-ttu-id="76be3-128">換句話說，並非所有作業系統版本都能使用所有功能。</span><span class="sxs-lookup"><span data-stu-id="76be3-128">In other words, all the features may not be available for all operating system versions.</span></span> <span data-ttu-id="76be3-129">如需詳細資料，請參閱功能描述。</span><span class="sxs-lookup"><span data-stu-id="76be3-129">See the feature descriptions for details.</span></span>

<span data-ttu-id="76be3-130">**問︰我需要多少授權才能監視基礎結構？**</span><span class="sxs-lookup"><span data-stu-id="76be3-130">**Q: How many licenses do I need to monitor my infrastructure?**</span></span>

* <span data-ttu-id="76be3-131">第一個 Connect Health 代理程式至少需要一個 Azure AD Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="76be3-131">The first Connect Health Agent requires at least one Azure AD Premium license.</span></span>
* <span data-ttu-id="76be3-132">每多一個註冊代理程式，就需要再 25 個 Azure AD Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="76be3-132">Each additional registered agent requires 25 additional Azure AD Premium licenses.</span></span>
* <span data-ttu-id="76be3-133">代理程式計數等於所有受監視角色 (AD FS、Azure AD Connect 及/或 AD DS) 的註冊代理程式總數。</span><span class="sxs-lookup"><span data-stu-id="76be3-133">Agent count is equivalent to the total number of agents that are registered across all monitored roles (AD FS, Azure AD Connect, and/or AD DS).</span></span>

<span data-ttu-id="76be3-134">您也可以在 [Azure AD 定價頁面](https://aka.ms/aadpricing)找到授權資訊。</span><span class="sxs-lookup"><span data-stu-id="76be3-134">Licensing information is also found on the [Azure AD Pricing page](https://aka.ms/aadpricing).</span></span>

<span data-ttu-id="76be3-135">範例：</span><span class="sxs-lookup"><span data-stu-id="76be3-135">Example:</span></span>

| <span data-ttu-id="76be3-136">已註冊的代理程式</span><span class="sxs-lookup"><span data-stu-id="76be3-136">Registered agents</span></span> | <span data-ttu-id="76be3-137">需要的授權</span><span class="sxs-lookup"><span data-stu-id="76be3-137">Licenses needed</span></span> | <span data-ttu-id="76be3-138">監視組態範例</span><span class="sxs-lookup"><span data-stu-id="76be3-138">Example monitoring configuration</span></span> |
| ------ | --------------- | --- |
| <span data-ttu-id="76be3-139">1</span><span class="sxs-lookup"><span data-stu-id="76be3-139">1</span></span> | <span data-ttu-id="76be3-140">1</span><span class="sxs-lookup"><span data-stu-id="76be3-140">1</span></span> | <span data-ttu-id="76be3-141">1 個 Azure AD Connect 伺服器</span><span class="sxs-lookup"><span data-stu-id="76be3-141">1 Azure AD Connect server</span></span> |
| <span data-ttu-id="76be3-142">2</span><span class="sxs-lookup"><span data-stu-id="76be3-142">2</span></span> | <span data-ttu-id="76be3-143">26</span><span class="sxs-lookup"><span data-stu-id="76be3-143">26</span></span>| <span data-ttu-id="76be3-144">1 個 Azure AD Connect 伺服器、1 個網域控制站</span><span class="sxs-lookup"><span data-stu-id="76be3-144">1 Azure AD Connect server and 1 domain controller</span></span> |
| <span data-ttu-id="76be3-145">3</span><span class="sxs-lookup"><span data-stu-id="76be3-145">3</span></span> | <span data-ttu-id="76be3-146">51</span><span class="sxs-lookup"><span data-stu-id="76be3-146">51</span></span> | <span data-ttu-id="76be3-147">1 個 Active Directory Federation Services (AD FS) 伺服器、1 個 AD FS Proxy、1 個網域控制站</span><span class="sxs-lookup"><span data-stu-id="76be3-147">1 Active Directory Federation Services (AD FS) server, 1 AD FS proxy, and 1 domain controller</span></span> |
| <span data-ttu-id="76be3-148">4</span><span class="sxs-lookup"><span data-stu-id="76be3-148">4</span></span> | <span data-ttu-id="76be3-149">76</span><span class="sxs-lookup"><span data-stu-id="76be3-149">76</span></span> | <span data-ttu-id="76be3-150">1 個 AD FS 伺服器、1 個 AD FS Proxy、2 個網域控制站</span><span class="sxs-lookup"><span data-stu-id="76be3-150">1 AD FS server, 1 AD FS proxy, and 2 domain controllers</span></span> |
| <span data-ttu-id="76be3-151">5</span><span class="sxs-lookup"><span data-stu-id="76be3-151">5</span></span> | <span data-ttu-id="76be3-152">101</span><span class="sxs-lookup"><span data-stu-id="76be3-152">101</span></span> | <span data-ttu-id="76be3-153">1 個 Azure AD Connect 伺服器、1 個 AD FS 伺服器、1 個 AD FS Proxy、2 個網域控制站</span><span class="sxs-lookup"><span data-stu-id="76be3-153">1 Azure AD Connect server, 1 AD FS server, 1 AD FS proxy, and 2 domain controllers</span></span> |


## <a name="installation-questions"></a><span data-ttu-id="76be3-154">安裝問題</span><span class="sxs-lookup"><span data-stu-id="76be3-154">Installation questions</span></span>

<span data-ttu-id="76be3-155">**問：在個別的伺服器上安裝 Azure AD Connect Health 代理程式有什麼影響？**</span><span class="sxs-lookup"><span data-stu-id="76be3-155">**Q: What is the impact of installing the Azure AD Connect Health Agent on individual servers?**</span></span>

<span data-ttu-id="76be3-156">安裝 Microsoft Azure AD Connect Health 代理程式、AD FS、Web 應用程式 Proxy 伺服器、Azure AD Connect (同步處理) 伺服器、網域控制站，對於 CPU、記憶體耗用量、網路頻寬和儲存體的影響非常小。</span><span class="sxs-lookup"><span data-stu-id="76be3-156">The impact of installing the Microsoft Azure AD Connect Health Agent, AD FS, web application proxy servers, Azure AD Connect (sync) servers, domain controllers is minimal with respect to the CPU, memory consumption, network bandwidth, and storage.</span></span>

<span data-ttu-id="76be3-157">以下的數字是近似值：</span><span class="sxs-lookup"><span data-stu-id="76be3-157">The following numbers are an approximation:</span></span>

* <span data-ttu-id="76be3-158">CPU 耗用量：增加約 1-5%。</span><span class="sxs-lookup"><span data-stu-id="76be3-158">CPU consumption: ~1-5% increase.</span></span>
* <span data-ttu-id="76be3-159">記憶體耗用量：最多 10% 的系統總記憶體。</span><span class="sxs-lookup"><span data-stu-id="76be3-159">Memory consumption: Up to 10 % of the total system memory.</span></span>

> [!NOTE]
> <span data-ttu-id="76be3-160">如果代理程式無法與 Azure 通訊，則代理程式會在本機儲存資料，最多可達定義的上限。</span><span class="sxs-lookup"><span data-stu-id="76be3-160">If the agent cannot communicate with Azure, the agent stores the data locally for a defined maximum limit.</span></span> <span data-ttu-id="76be3-161">代理程式會根據「最近最少服務」的準則來覆寫「快取」資料。</span><span class="sxs-lookup"><span data-stu-id="76be3-161">The agent overwrites the “cached” data on a “least recently serviced” basis.</span></span>
>
>

* <span data-ttu-id="76be3-162">Azure AD Connect Health 代理程式的本機緩衝區儲存體：約 20 MB。</span><span class="sxs-lookup"><span data-stu-id="76be3-162">Local buffer storage for Azure AD Connect Health Agents: ~20 MB.</span></span>
* <span data-ttu-id="76be3-163">對於 AD FS 伺服器，建議您為 AD FS 稽核通道佈建 1024 MB (1 GB) 的磁碟空間，Azure AD Connect Health 代理程式才能在所有稽核資料遭到覆寫前加以處理。</span><span class="sxs-lookup"><span data-stu-id="76be3-163">For AD FS servers, we recommend that you provision a disk space of 1,024 MB (1 GB) for the AD FS audit channel for Azure AD Connect Health Agents to process all the audit data before it is overwritten.</span></span>

<span data-ttu-id="76be3-164">**問：在安裝 Azure AD Connect Health 代理程式期間，我是否需要重新啟動我的伺服器？**</span><span class="sxs-lookup"><span data-stu-id="76be3-164">**Q: Will I have to reboot my servers during the installation of the Azure AD Connect Health Agents?**</span></span>

<span data-ttu-id="76be3-165">否。</span><span class="sxs-lookup"><span data-stu-id="76be3-165">No.</span></span> <span data-ttu-id="76be3-166">安裝代理程式不需要您重新啟動伺服器。</span><span class="sxs-lookup"><span data-stu-id="76be3-166">The installation of the agents will not require you to reboot the server.</span></span> <span data-ttu-id="76be3-167">不過，安裝某些先決條件的步驟可能需要重新啟動伺服器。</span><span class="sxs-lookup"><span data-stu-id="76be3-167">However, installation of some prerequisite steps might require a reboot of the server.</span></span>

<span data-ttu-id="76be3-168">例如，在 Windows Server 2008 R2 上安裝 .NET 4.5 Framework 需要重新啟動伺服器。</span><span class="sxs-lookup"><span data-stu-id="76be3-168">For example, on Windows Server 2008 R2, installation of .NET 4.5 Framework requires a server reboot.</span></span>

<span data-ttu-id="76be3-169">**問：Azure AD Connect Health 是否透過傳遞 Http Proxy 運作？**</span><span class="sxs-lookup"><span data-stu-id="76be3-169">**Q: Does Azure AD Connect Health work through a pass-through HTTP proxy?**</span></span>

<span data-ttu-id="76be3-170">是。</span><span class="sxs-lookup"><span data-stu-id="76be3-170">Yes.</span></span> <span data-ttu-id="76be3-171">若是進行中的作業，您可以將 Health 代理程式設定為使用 HTTP Proxy 來轉送輸出 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="76be3-171">For ongoing operations, you can configure the Health Agent to use an HTTP proxy to forward outbound HTTP requests.</span></span>
<span data-ttu-id="76be3-172">深入了解[設定 Health 代理程式的 HTTP Proxy](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy)。</span><span class="sxs-lookup"><span data-stu-id="76be3-172">Read more about [configuring HTTP Proxy for Health Agents](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).</span></span>

<span data-ttu-id="76be3-173">如果需要在代理程式註冊期間設定 Proxy，您可能需要預先修改 Internet Explorer 的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="76be3-173">If you need to configure a proxy during agent registration, you might need to modify your Internet Explorer Proxy settings beforehand.</span></span>

1. <span data-ttu-id="76be3-174">開啟 Internet Explorer > [設定]  >  [網際網路選項]  >  [連線]  >  [LAN 設定]。</span><span class="sxs-lookup"><span data-stu-id="76be3-174">Open Internet Explorer > **Settings** > **Internet Options** > **Connections** > **LAN Settings**.</span></span>
2. <span data-ttu-id="76be3-175">選取 [在您的區域網路使用 Proxy 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="76be3-175">Select **Use a Proxy Server for your LAN**.</span></span>
3. <span data-ttu-id="76be3-176">如果您有不同的 Proxy 連接埠供 HTTP 和 HTTPS/安全使用，請選取 [進階]。</span><span class="sxs-lookup"><span data-stu-id="76be3-176">Select **Advanced** if you have different proxy ports for HTTP and HTTPS/Secure.</span></span>

<span data-ttu-id="76be3-177">**問：連線到 HTTP Proxy 時，Azure AD Connect Health 是否支援基本驗證？**</span><span class="sxs-lookup"><span data-stu-id="76be3-177">**Q: Does Azure AD Connect Health support Basic authentication when connecting to HTTP proxies?**</span></span>

<span data-ttu-id="76be3-178">否。</span><span class="sxs-lookup"><span data-stu-id="76be3-178">No.</span></span> <span data-ttu-id="76be3-179">目前不支援為基本驗證指定任意使用者名稱和密碼的機制。</span><span class="sxs-lookup"><span data-stu-id="76be3-179">A mechanism to specify an arbitrary user name and password for Basic authentication is not currently supported.</span></span>

<span data-ttu-id="76be3-180">**問：我需要開放哪些防火牆連接埠，Azure AD Connect Health 代理程式才能運作？**</span><span class="sxs-lookup"><span data-stu-id="76be3-180">**Q: What firewall ports do I need to open for the Azure AD Connect Health Agent to work?**</span></span>

<span data-ttu-id="76be3-181">請參閱[需求](active-directory-aadconnect-health-agent-install.md#requirements)一節，以取得防火牆連接埠清單與其他的連線需求。</span><span class="sxs-lookup"><span data-stu-id="76be3-181">See the [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for the list of firewall ports and other connectivity requirements.</span></span>

<span data-ttu-id="76be3-182">**問︰為什麼我會在 Azure AD Connect Health 入口網站中看到兩部名稱相同的伺服器？**</span><span class="sxs-lookup"><span data-stu-id="76be3-182">**Q: Why do I see two servers with the same name in the Azure AD Connect Health portal?**</span></span>

<span data-ttu-id="76be3-183">當您從伺服器移除代理程式時，系統不會自動從 Azure AD Connect Health 入口網站移除伺服器。</span><span class="sxs-lookup"><span data-stu-id="76be3-183">When you remove an agent from a server, the server is not automatically removed from the Azure AD Connect Health portal.</span></span> <span data-ttu-id="76be3-184">如果您以手動方式從伺服器移除代理程式，或移除伺服器本身，就需要以手動方式從 Azure AD Connect Health 入口網站中刪除伺服器項目。</span><span class="sxs-lookup"><span data-stu-id="76be3-184">If you manually remove an agent from a server or remove the server itself, you need to manually delete the server entry from the Azure AD Connect Health portal.</span></span>

<span data-ttu-id="76be3-185">您可能會重新安裝伺服器的映像，或以相同的細節 (例如電腦名稱) 建立新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="76be3-185">You might reimage a server or create a new server with the same details (such as machine name).</span></span> <span data-ttu-id="76be3-186">如果您並未從 Azure AD Connect Health 入口網站移除已經註冊的伺服器，就在新伺服器上安裝代理程式，您可能會看到兩個同名的項目。</span><span class="sxs-lookup"><span data-stu-id="76be3-186">If you did not remove the already registered server from the Azure AD Connect Health portal, and you installed the agent on the new server, you might see two entries with the same name.</span></span>

<span data-ttu-id="76be3-187">在此情況下，請手動刪除屬於舊伺服器的項目。</span><span class="sxs-lookup"><span data-stu-id="76be3-187">In this case, manually delete the entry that belongs to the older server.</span></span> <span data-ttu-id="76be3-188">此伺服器的資料應該已過時。</span><span class="sxs-lookup"><span data-stu-id="76be3-188">The data for this server should be out of date.</span></span>

## <a name="health-agent-registration-and-data-freshness"></a><span data-ttu-id="76be3-189">Health 代理程式註冊和資料有效性</span><span class="sxs-lookup"><span data-stu-id="76be3-189">Health Agent registration and data freshness</span></span>

<span data-ttu-id="76be3-190">**問︰Health 代理程式註冊失敗的常見原因為何？該如何解決問題？**</span><span class="sxs-lookup"><span data-stu-id="76be3-190">**Q: What are common reasons for the Health Agent registration failures and how do I troubleshoot issues?**</span></span>

<span data-ttu-id="76be3-191">Health 代理程式會因為下列可能原因而無法註冊：</span><span class="sxs-lookup"><span data-stu-id="76be3-191">The health agent can fail to register due to the following possible reasons:</span></span>

* <span data-ttu-id="76be3-192">因為防火牆封鎖流量，代理程式無法與所需端點通訊。</span><span class="sxs-lookup"><span data-stu-id="76be3-192">The agent cannot communicate with the required endpoints because a firewall is blocking traffic.</span></span> <span data-ttu-id="76be3-193">在 Web 應用程式 Proxy 伺服器上尤其常見。</span><span class="sxs-lookup"><span data-stu-id="76be3-193">This is particularly common on web application proxy servers.</span></span> <span data-ttu-id="76be3-194">請確定您已允許針對所需端點和連接埠的輸出通訊。</span><span class="sxs-lookup"><span data-stu-id="76be3-194">Make sure that you have allowed outbound communication to the required endpoints and ports.</span></span> <span data-ttu-id="76be3-195">如需詳細資訊，請參閱[需求](active-directory-aadconnect-health-agent-install.md#requirements)一節。</span><span class="sxs-lookup"><span data-stu-id="76be3-195">See the [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for details.</span></span>
* <span data-ttu-id="76be3-196">輸出通訊會在網路層遇到 SSL 檢查。</span><span class="sxs-lookup"><span data-stu-id="76be3-196">Outbound communication is subjected to an SSL inspection by the network layer.</span></span> <span data-ttu-id="76be3-197">這會導致代理程式所使用的憑證遭到檢查伺服器/實體所取代，完成代理程式註冊的步驟便會失敗。</span><span class="sxs-lookup"><span data-stu-id="76be3-197">This causes the certificate that the agent uses to be replaced by the inspection server/entity, and the steps to complete the agent registration fail.</span></span>
* <span data-ttu-id="76be3-198">使用者沒有執行代理程式註冊的存取權。</span><span class="sxs-lookup"><span data-stu-id="76be3-198">The user does not have access to perform the registration of the agent.</span></span> <span data-ttu-id="76be3-199">根據預設，全域系統管理員具有存取權。</span><span class="sxs-lookup"><span data-stu-id="76be3-199">Global admins have access by default.</span></span> <span data-ttu-id="76be3-200">您可以使用[角色型存取控制](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)將存取權委派給其他使用者。</span><span class="sxs-lookup"><span data-stu-id="76be3-200">You can use [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) to delegate access to other users.</span></span>

<span data-ttu-id="76be3-201">**問︰我收到有關「Health 服務資料不是最新狀態」的警示。我該如何進行解決這個問題？**</span><span class="sxs-lookup"><span data-stu-id="76be3-201">**Q: I am getting alerted that "Health Service data is not up to date." How do I troubleshoot the issue?**</span></span>

<span data-ttu-id="76be3-202">當 Azure AD Connect Health 在過去 2 小時沒有從伺服器收到所有資料點，就會產生此警示。</span><span class="sxs-lookup"><span data-stu-id="76be3-202">Azure AD Connect Health generates the alert when it does not receive all the data points from the server in the last two hours.</span></span> <span data-ttu-id="76be3-203">有很多原因都可能導致引發此警示。</span><span class="sxs-lookup"><span data-stu-id="76be3-203">There can be multiple reasons for this alert.</span></span>

* <span data-ttu-id="76be3-204">因為防火牆封鎖流量，代理程式無法與所需端點通訊。</span><span class="sxs-lookup"><span data-stu-id="76be3-204">The agent cannot communicate with the required endpoints because a firewall is blocking traffic.</span></span> <span data-ttu-id="76be3-205">在 Web 應用程式 Proxy 伺服器上尤其常見。</span><span class="sxs-lookup"><span data-stu-id="76be3-205">This is particularly common on web application proxy servers.</span></span> <span data-ttu-id="76be3-206">請確定您已允許針對所需端點和連接埠的輸出通訊。</span><span class="sxs-lookup"><span data-stu-id="76be3-206">Make sure that you have allowed outbound communication to the required end points and ports.</span></span> <span data-ttu-id="76be3-207">如需詳細資訊，請參閱[需求](active-directory-aadconnect-health-agent-install.md#requirements)一節。</span><span class="sxs-lookup"><span data-stu-id="76be3-207">See the [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for details.</span></span>
* <span data-ttu-id="76be3-208">輸出通訊會在網路層遇到 SSL 檢查。</span><span class="sxs-lookup"><span data-stu-id="76be3-208">Outbound communication is subjected to an SSL inspection by the network layer.</span></span> <span data-ttu-id="76be3-209">這會導致代理程式所使用的憑證遭到檢查伺服器/實體所取代，而無法將資料上傳至 Azure AD Connect Health 服務。</span><span class="sxs-lookup"><span data-stu-id="76be3-209">This causes the certificate that the agent uses to be replaced by the inspection server/entity, and the process fails to upload data to the Azure AD Connect Health service.</span></span>
* <span data-ttu-id="76be3-210">您可以使用代理程式內建的連線命令。</span><span class="sxs-lookup"><span data-stu-id="76be3-210">You can use the connectivity command built into the agent.</span></span> <span data-ttu-id="76be3-211">[閱讀更多資訊](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)。</span><span class="sxs-lookup"><span data-stu-id="76be3-211">[Read more](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).</span></span>
* <span data-ttu-id="76be3-212">代理程式也支援透過未經驗證之 HTTP Proxy 的輸出連線。</span><span class="sxs-lookup"><span data-stu-id="76be3-212">The agents also support outbound connectivity via an unauthenticated HTTP Proxy.</span></span> <span data-ttu-id="76be3-213">[閱讀更多資訊](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy)。</span><span class="sxs-lookup"><span data-stu-id="76be3-213">[Read more](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).</span></span>

## <a name="operations-questions"></a><span data-ttu-id="76be3-214">操作問題</span><span class="sxs-lookup"><span data-stu-id="76be3-214">Operations questions</span></span>
<span data-ttu-id="76be3-215">**問︰是否需要在 Web 應用程式 Proxy 伺服器上啟用稽核？**</span><span class="sxs-lookup"><span data-stu-id="76be3-215">**Q: Do I need to enable auditing on the web application proxy servers?**</span></span>

<span data-ttu-id="76be3-216">否，不需要在 Web 應用程式 Proxy 伺服器上啟用稽核。</span><span class="sxs-lookup"><span data-stu-id="76be3-216">No, auditing does not need to be enabled on the web application proxy servers.</span></span>

<span data-ttu-id="76be3-217">**問：Azure AD Connect Health 警示如何獲得解決？**</span><span class="sxs-lookup"><span data-stu-id="76be3-217">**Q: How do Azure AD Connect Health Alerts get resolved?**</span></span>

<span data-ttu-id="76be3-218">Azure AD Connect Health 警示會在成功情況下獲得解決。</span><span class="sxs-lookup"><span data-stu-id="76be3-218">Azure AD Connect Health alerts get resolved on a success condition.</span></span> <span data-ttu-id="76be3-219">Azure AD Connect Health 代理程式會定期偵測成功情況，並向服務回報。</span><span class="sxs-lookup"><span data-stu-id="76be3-219">Azure AD Connect Health Agents detect and report the success conditions to the service periodically.</span></span> <span data-ttu-id="76be3-220">對於少數幾個警示，隱藏是以時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="76be3-220">For a few alerts, the suppression is time-based.</span></span> <span data-ttu-id="76be3-221">也就是說，如果在警示產生的 72 小時內未觀察到相同的錯誤狀況，就會自動解決警示。</span><span class="sxs-lookup"><span data-stu-id="76be3-221">In other words, if the same error condition is not observed within 72 hours from alert generation, the alert is automatically resolved.</span></span>

<span data-ttu-id="76be3-222">**問：我收到下列警示：「測試驗證要求 (綜合交易) 無法取得權杖」。我該如何進行解決這個問題？**</span><span class="sxs-lookup"><span data-stu-id="76be3-222">**Q: I am getting alerted that "Test Authentication Request (Synthetic Transaction) failed to obtain a token." How do I troubleshoot the issue?**</span></span>

<span data-ttu-id="76be3-223">在健康狀態代理程式所起始的綜合交易期間，AD FS 伺服器上安裝的健康狀態代理程式無法取得權杖時，Azure AD Connect Health for AD FS 會產生警示。</span><span class="sxs-lookup"><span data-stu-id="76be3-223">Azure AD Connect Health for AD FS generates this alert when the Health Agent installed on an AD FS server fails to obtain a token as part of a synthetic transaction initiated by the Health Agent.</span></span> <span data-ttu-id="76be3-224">健康狀態代理程式使用本機系統內容，並嘗試取得自我信賴憑證者的權杖。</span><span class="sxs-lookup"><span data-stu-id="76be3-224">The Health agent uses the local system context and attempts to get a token for a self relying party.</span></span> <span data-ttu-id="76be3-225">這是 catch-all 測試，可確保 AD FS 處於發行權杖狀態。</span><span class="sxs-lookup"><span data-stu-id="76be3-225">This is a catch-all test to ensure that AD FS is in a state of issuing tokens.</span></span>

<span data-ttu-id="76be3-226">這項測試經常失敗，因為健康狀態代理程式無法解析 AD FS 伺服器陣列名稱。</span><span class="sxs-lookup"><span data-stu-id="76be3-226">Most often this test fails because the Health Agent is unable to resolve the AD FS farm name.</span></span> <span data-ttu-id="76be3-227">如果 AD FS 伺服器受到網路負載平衡器保護，並且從受到負載平衡器保護的節點起始要求 (相較於不受負載平衡器保護的一般用戶端)，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="76be3-227">This can happen if the AD FS servers are behind a network load balancers and the request gets initiated from a node that's behind the load balancer (as opposed to a regular client that is in front of the load balancer).</span></span> <span data-ttu-id="76be3-228">更新 "C:\Windows\System32\drivers\etc" 下的 "hosts" 檔案，使其包含 AD FS 伺服器的 IP 位址或 AD FS 伺服器陣列名稱 (例如 sts.contoso.com) 的迴圈 IP 位址 (127.0.0.1)，即可修正此問題。</span><span class="sxs-lookup"><span data-stu-id="76be3-228">This can be fixed by updating the "hosts" file located under "C:\Windows\System32\drivers\etc" to include the IP address of the AD FS server or a loopback IP address (127.0.0.1) for the AD FS farm name (such as sts.contoso.com).</span></span> <span data-ttu-id="76be3-229">新增主機檔案會讓網路呼叫短路，如此可讓健康狀態代理程式取得權杖。</span><span class="sxs-lookup"><span data-stu-id="76be3-229">Adding the host file will short-circuit the network call, thus allowing the Health Agent to get the token.</span></span>

<span data-ttu-id="76be3-230">**問：我收到一封電子郵件，指出未針對最近的勒索軟體攻擊修補我的電腦。我為什麼收到這封電子郵件？**</span><span class="sxs-lookup"><span data-stu-id="76be3-230">**Q: I got an email indicating my machines are NOT patched for the recent ransomeware attacks. Why did I receive this email?**</span></span>

<span data-ttu-id="76be3-231">Azure AD Connect Health 服務已掃描所有已監視的電腦，確保已安裝的必要修補程式。</span><span class="sxs-lookup"><span data-stu-id="76be3-231">Azure AD Connect Health service scanned all the machines it monitors to ensure the required patches were installed.</span></span> <span data-ttu-id="76be3-232">如果至少一部電腦沒有重大修補程式，則已將電子郵件傳送給租用戶系統管理員。</span><span class="sxs-lookup"><span data-stu-id="76be3-232">The email was sent to the tenant administrators if at least one machine did not have the critical patches.</span></span> <span data-ttu-id="76be3-233">下列邏輯已用來進行這項決定。</span><span class="sxs-lookup"><span data-stu-id="76be3-233">The following logic was used to make this determination.</span></span>
1. <span data-ttu-id="76be3-234">尋找電腦上安裝的所有 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="76be3-234">Find all the hotfixes installed on the machine.</span></span>
2. <span data-ttu-id="76be3-235">檢查定義的清單中是否有至少一個 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="76be3-235">Check if at least one of the HotFixes from the defined list is present.</span></span>
3. <span data-ttu-id="76be3-236">如果有，則電腦受到保護。</span><span class="sxs-lookup"><span data-stu-id="76be3-236">If Yes, the machine is protected.</span></span> <span data-ttu-id="76be3-237">如果沒有，則電腦會有受攻擊的風險。</span><span class="sxs-lookup"><span data-stu-id="76be3-237">If Not, the machine is at risk for the attack.</span></span>

<span data-ttu-id="76be3-238">您可以使用下列 PowerShell 指令碼手動執行這項檢查。</span><span class="sxs-lookup"><span data-stu-id="76be3-238">You can use the following PowerShell script to perform this check manually.</span></span> <span data-ttu-id="76be3-239">它會實作上述邏輯。</span><span class="sxs-lookup"><span data-stu-id="76be3-239">It implements the above logic.</span></span>

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks the computer it's run on if any of the listed hotfixes are present
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



## <a name="related-links"></a><span data-ttu-id="76be3-240">相關連結</span><span class="sxs-lookup"><span data-stu-id="76be3-240">Related links</span></span>
* [<span data-ttu-id="76be3-241">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="76be3-241">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="76be3-242">Azure AD Connect Health 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="76be3-242">Azure AD Connect Health Agent installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="76be3-243">Azure AD Connect Health 操作</span><span class="sxs-lookup"><span data-stu-id="76be3-243">Azure AD Connect Health operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="76be3-244">在 AD FS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="76be3-244">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="76be3-245">使用 Azure AD Connect Health 進行同步處理</span><span class="sxs-lookup"><span data-stu-id="76be3-245">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="76be3-246">在 AD DS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="76be3-246">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="76be3-247">Azure AD Connect Health 版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="76be3-247">Azure AD Connect Health version history</span></span>](active-directory-aadconnect-health-version-history.md)
