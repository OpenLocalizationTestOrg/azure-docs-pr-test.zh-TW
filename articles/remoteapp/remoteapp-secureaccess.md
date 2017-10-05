---
title: "保護 Azure RemoteApp 的存取，且後續將會推出更多功能 | Microsoft Docs"
description: "了解如何透過使用 Azure Active Directory 中的條件式存取來安全存取 Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 28ee4698515d11964e5371628d21dbc00687c861
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="securing-access-to-azure-remoteapp-and-beyond"></a><span data-ttu-id="ba82d-103">保護 Azure RemoteApp 的存取，且後續將會推出更多功能</span><span class="sxs-lookup"><span data-stu-id="ba82d-103">Securing access to Azure RemoteApp, and beyond</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ba82d-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="ba82d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ba82d-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="ba82d-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ba82d-106">本文將概述系統管理員要如何設定安全存取通道，讓這條通道起自使用者、經過 Azure RemoteApp，並終止於 SQL 資料庫或另一個應用程式的後端等安全資源。</span><span class="sxs-lookup"><span data-stu-id="ba82d-106">In this article we will give an overview of how an administrator can set up a secure access channel starting from the end user, through Azure RemoteApp and ending with a secure resource such as a SQL database or another application back-end.</span></span> <span data-ttu-id="ba82d-107">其目標是要確定只有符合所需條件的授權使用者可以存取遠端應用程式，而且只能從受控制的 Azure RemoteApp 環境存取安全的後端，而無法從其他位置進行存取。</span><span class="sxs-lookup"><span data-stu-id="ba82d-107">The goal is to make sure that only authorized users meeting the desired conditions can access remote applications, and that the secure back-end can only be accessed from the controlled Azure RemoteApp environment and not from other locations.</span></span>

<span data-ttu-id="ba82d-108">系統管理員需要注意下列 3 個重點：</span><span class="sxs-lookup"><span data-stu-id="ba82d-108">There are 3 major areas the admin needs to look at:</span></span>

![Azure RemoteApp 條件式存取的考量](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

<span data-ttu-id="ba82d-110">請繼續閱讀後續內容以了解相關資訊和上述問題的解答。</span><span class="sxs-lookup"><span data-stu-id="ba82d-110">Read on for information and answers to these questions.</span></span>

## <a name="who-can-access-the-collection"></a><span data-ttu-id="ba82d-111">誰可以存取集合？</span><span class="sxs-lookup"><span data-stu-id="ba82d-111">Who can access the collection?</span></span>
<span data-ttu-id="ba82d-112">系統管理員必須選擇可存取集合中的遠端應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="ba82d-112">The administrator chooses the users that can access remote applications in the collection.</span></span> <span data-ttu-id="ba82d-113">您可以使用 Azure Active Directory (Azure AD) 的公司或學校帳戶 (先前稱為「組織帳戶」) 或 Microsoft 帳戶 (例如 @outlook.com)。</span><span class="sxs-lookup"><span data-stu-id="ba82d-113">You can use Azure Active Directory (Azure AD) work or school accounts (previously called, "organizational accounts") or Microsoft accounts (e.g. @outlook.com).</span></span> <span data-ttu-id="ba82d-114">大多數企業案例是使用 Azure AD 帳戶，此帳戶可讓您使用稍後會討論到的條件式存取功能，也是已加入網域之集合唯一能選擇的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ba82d-114">Most enterprise scenarios use Azure AD accounts; they let you use conditional access features discussed later and are also the only choice for domain-joined collections.</span></span> <span data-ttu-id="ba82d-115">本文其餘部分假設您使用 Azure AD 帳戶和 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ba82d-115">The rest of the article assumes you are using Azure AD accounts with Azure RemoteApp.</span></span>

<span data-ttu-id="ba82d-116">**我們已完成的工作：**</span><span class="sxs-lookup"><span data-stu-id="ba82d-116">**What we have accomplished:**</span></span>

<span data-ttu-id="ba82d-117">使用 Azure AD 帳戶來控制 Azure RemoteApp 的存取有兩個好處：</span><span class="sxs-lookup"><span data-stu-id="ba82d-117">Using Azure AD accounts to control access to Azure RemoteApp gives us two things:</span></span>

1. <span data-ttu-id="ba82d-118">我們永遠會知道誰可以存取已發行的應用程式以及這些應用程式所連接到的後端。</span><span class="sxs-lookup"><span data-stu-id="ba82d-118">We always know who can access the applications we have published and access any back-ends those applications connect to.</span></span>
2. <span data-ttu-id="ba82d-119">我們能控制基礎的 Azure AD，因此可以建立和刪除使用者帳戶、設定密碼原則，以及使用 Multi-Factor Authentication 等等。</span><span class="sxs-lookup"><span data-stu-id="ba82d-119">We control the underlying Azure AD so we can create and delete user accounts, set password policies, use multi-factor authentication, etc.</span></span> 

## <a name="how-is-the-collection-accessed-from-where"></a><span data-ttu-id="ba82d-120">集合的存取方式為何？</span><span class="sxs-lookup"><span data-stu-id="ba82d-120">How is the collection accessed?</span></span> <span data-ttu-id="ba82d-121">是從哪裡進行存取的？</span><span class="sxs-lookup"><span data-stu-id="ba82d-121">From where?</span></span>
<span data-ttu-id="ba82d-122">系統管理員通常會想要定義原則，來規範公用網際網路面向環境 (例如 Azure RemoteApp) 的存取。</span><span class="sxs-lookup"><span data-stu-id="ba82d-122">Commonly administrators want to define policies for accessing a public Internet-facing environment, such as Azure RemoteApp.</span></span> <span data-ttu-id="ba82d-123">比方說，他們想要確定從公司網路外部存取環境的使用者必須使用 Multi-Factor Authentication (MFA) 才能取得存取權，或者，應該全都遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="ba82d-123">For example, they want to ensure that users accessing the environment from outside of the corporate network have to use multi-factor authentication (MFA) to gain access; or perhaps they should be blocked altogether.</span></span>

<span data-ttu-id="ba82d-124">Azure RemoteApp 的系統管理員可以使用 Azure AD Premium 所提供的功能來設定其 Azure RemoteApp 環境的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="ba82d-124">Azure RemoteApp administrators can use the functionality available through Azure AD Premium to set conditional access policies for their Azure RemoteApp environment.</span></span> <span data-ttu-id="ba82d-125">他們也可以使用豐富的報告和警示功能來監控環境受到存取的情形。</span><span class="sxs-lookup"><span data-stu-id="ba82d-125">They can also use rich reporting and alerting features to monitor how the environment is being accessed.</span></span>

### <a name="how-to-set-up-conditional-access-for-azure-remoteapp"></a><span data-ttu-id="ba82d-126">如何設定 Azure RemoteApp 的條件式存取</span><span class="sxs-lookup"><span data-stu-id="ba82d-126">How to set up conditional access for Azure RemoteApp</span></span>
<span data-ttu-id="ba82d-127">我們要逐步解說一個範例案例，在此案例中，Azure RemoteApp 的系統管理員想要封鎖從公司網路外部存取環境的使用者。</span><span class="sxs-lookup"><span data-stu-id="ba82d-127">We are going to walk through an example scenario – the Azure RemoteApp administrator wants to block access to the environment when users are outside of the corporate network.</span></span>

> [!NOTE]
> <span data-ttu-id="ba82d-128">我們假設您已將 Azure AD 升級為「高階層」，並且您已建立至少一個 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="ba82d-128">We assume you have upgraded Azure AD to the Premium tier and that you have created at least one Azure RemoteApp collection.</span></span>
> 
> 

1. <span data-ttu-id="ba82d-129">在 Azure 入口網站中，按一下 [Active Directory]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ba82d-129">In Azure portal click the **Active Directory** tab.</span></span> <span data-ttu-id="ba82d-130">然後，按一下您想要設定的目錄。</span><span class="sxs-lookup"><span data-stu-id="ba82d-130">Then click the directory you want to configure.</span></span>
   
   <span data-ttu-id="ba82d-131">請記住：條件式存取是目錄的屬性，而非 Azure RemoteApp 的屬性，因此所有組態都是在目錄層級進行設定。</span><span class="sxs-lookup"><span data-stu-id="ba82d-131">Remember: Conditional access is a property of your directory and not of Azure RemoteApp, so all configuration is done at the directory level.</span></span> <span data-ttu-id="ba82d-132">這也表示您必須是目錄的系統管理員才能進行這些變更。</span><span class="sxs-lookup"><span data-stu-id="ba82d-132">This also means you need to be the directory administrator to make these changes.</span></span>
2. <span data-ttu-id="ba82d-133">按一下 [應用程式]，然後按一下 [Microsoft Azure RemoteApp] 來設定條件式存取。</span><span class="sxs-lookup"><span data-stu-id="ba82d-133">Click **Applications**, and then click **Microsoft Azure RemoteApp** to set up conditional access.</span></span> <span data-ttu-id="ba82d-134">請注意，您可以個別為目錄中的每個「軟體即服務」應用程式設定條件式存取。</span><span class="sxs-lookup"><span data-stu-id="ba82d-134">Note that you can set up conditional access for each "software as a service" application in your directory separately.</span></span>
   <span data-ttu-id="ba82d-135">![設定 Azure RemoteApp 的條件式存取](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)</span><span class="sxs-lookup"><span data-stu-id="ba82d-135">![Setting up conditional access for Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)</span></span>
3. <span data-ttu-id="ba82d-136">在 [設定] 索引標籤上，將 [啟用存取規則] 設為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="ba82d-136">On the **Configure** tab, set **Enable Access Rules** to ON.</span></span>
   <span data-ttu-id="ba82d-137">![啟用 Azure RemoteApp 的存取規則](./media/remoteapp-secureaccess/ra-enableaccessrules.png)</span><span class="sxs-lookup"><span data-stu-id="ba82d-137">![Enable access rules for Azure RemoteApp](./media/remoteapp-secureaccess/ra-enableaccessrules.png)</span></span>
4. <span data-ttu-id="ba82d-138">現在您可以設定不同的規則，並選擇要套用規則的人員：</span><span class="sxs-lookup"><span data-stu-id="ba82d-138">You can now configure various rules and choose who to apply them to:</span></span>
   
   1. <span data-ttu-id="ba82d-139">選擇 [不工作時封鎖存取]  以完全防止使用者從您指定的網路環境外部存取 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ba82d-139">Choose **Block access when not at work** to completely prevent users from accessing Azure RemoteApp outside of the network environment you specify.</span></span>
   2. <span data-ttu-id="ba82d-140">按一下下面的選項可定義構成「受信任網路」的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="ba82d-140">Click the option below to define the IP address ranges that constitute your "trusted network."</span></span> <span data-ttu-id="ba82d-141">此範圍以外的所有位址將會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="ba82d-141">Everything outside of those will be rejected.</span></span>
5. <span data-ttu-id="ba82d-142">從您指定的範圍之外的 IP 位址啟動 Azure RemoteApp 用戶端，來測試您的組態。</span><span class="sxs-lookup"><span data-stu-id="ba82d-142">Test your configuration by launching the Azure RemoteApp client from an IP address outside of the range you specified.</span></span> <span data-ttu-id="ba82d-143">在使用 Azure AD 認證登入之後，您應該會看到如下的訊息：</span><span class="sxs-lookup"><span data-stu-id="ba82d-143">After you sign in with your Azure AD credentials you should see a message like this:</span></span>

![拒絕 Azure RemoteApp 的存取](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a><span data-ttu-id="ba82d-145">未來的條件式存取功能</span><span class="sxs-lookup"><span data-stu-id="ba82d-145">Future conditional access features</span></span>
<span data-ttu-id="ba82d-146">Azure Active Directory 小組正著手開發條件式存取的新功能。</span><span class="sxs-lookup"><span data-stu-id="ba82d-146">The Azure Active Directory team is working on new capabilities in Conditional Access.</span></span> <span data-ttu-id="ba82d-147">系統管理員日後將可以建立網路位置型規則以外的新類型規則。</span><span class="sxs-lookup"><span data-stu-id="ba82d-147">Administrators will be able to create new types of rules beyond network location based rules.</span></span> <span data-ttu-id="ba82d-148">我們應該很快就會推出新功能的公開預覽。</span><span class="sxs-lookup"><span data-stu-id="ba82d-148">A public preview of the new functionality should be available soon.</span></span>

### <a name="how-to-monitor-access-to-azure-remoteapp"></a><span data-ttu-id="ba82d-149">如何監視 Azure RemoteApp 的存取</span><span class="sxs-lookup"><span data-stu-id="ba82d-149">How to monitor access to Azure RemoteApp</span></span>
<span data-ttu-id="ba82d-150">Azure Active Directory Premium 報告功能是能搭配條件式存取來使用的絕佳功能。</span><span class="sxs-lookup"><span data-stu-id="ba82d-150">A great feature to use alongside conditional access is the Azure Active Directory Premium reporting functionality.</span></span> <span data-ttu-id="ba82d-151">您可以使用報告來監視正在存取環境的人員，以及偵測任何可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="ba82d-151">You can use reports to monitor who is accessing your environment and detect any suspicious activity.</span></span>

<span data-ttu-id="ba82d-152">比方說，您可以查看存取 Azure RemoteApp 之使用者的名稱、存取次數和存取時間。</span><span class="sxs-lookup"><span data-stu-id="ba82d-152">For example, you can see the names of the users who accessed Azure RemoteApp, how many times they did it and when.</span></span>

1. <span data-ttu-id="ba82d-153">在 Azure 入口網站中，按一下 [Active Directory] ，然後按一下您的目錄。</span><span class="sxs-lookup"><span data-stu-id="ba82d-153">In Azure portal, click **Active Directory**, and then click your directory.</span></span>
2. <span data-ttu-id="ba82d-154">移至 [報告]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ba82d-154">Go to the **Reports** tab.</span></span>
3. <span data-ttu-id="ba82d-155">從報告清單中選取 [整合式應用程式] 底下的 [應用程式使用情況]。</span><span class="sxs-lookup"><span data-stu-id="ba82d-155">From the list of reports, select **Application usage** under **Integrated applications**.</span></span>
   
   <span data-ttu-id="ba82d-156">您會看到 Azure RemoteApp 的一些彙總統計資料。</span><span class="sxs-lookup"><span data-stu-id="ba82d-156">You'll see some aggregated statistics for Azure RemoteApp.</span></span> 
   <span data-ttu-id="ba82d-157">![彙總的 Azure RemoteApp 存取統計資料](./media/remoteapp-secureaccess/ra-accessstats.png)</span><span class="sxs-lookup"><span data-stu-id="ba82d-157">![Aggregated Azure RemoteApp access stats](./media/remoteapp-secureaccess/ra-accessstats.png)</span></span>
4. <span data-ttu-id="ba82d-158">按一下應用程式以顯示存取 Azure RemoteApp 之使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ba82d-158">Click the application to reveal information about users accessing Azure RemoteApp.</span></span>
   <span data-ttu-id="ba82d-159">![Azure RemoteApp 的使用者存取統計資料](./media/remoteapp-secureaccess/ra-userstats.png)</span><span class="sxs-lookup"><span data-stu-id="ba82d-159">![User access stats for Azure RemoteApp](./media/remoteapp-secureaccess/ra-userstats.png)</span></span>

### <a name="summary"></a><span data-ttu-id="ba82d-160">摘要</span><span class="sxs-lookup"><span data-stu-id="ba82d-160">Summary</span></span>
<span data-ttu-id="ba82d-161">使用 Azure Active Directory Premium，您就可以設定 Azure RemoteApp (以及其他可透過 Azure AD 取得的軟體即服務應用程式) 的存取規則。</span><span class="sxs-lookup"><span data-stu-id="ba82d-161">With Azure Active Directory Premium you can set up access rules to Azure RemoteApp (and other software as a service applications available through Azure AD).</span></span> <span data-ttu-id="ba82d-162">目前規則只有網路位置型原則，但未來將會延伸到其他企業管理層面。</span><span class="sxs-lookup"><span data-stu-id="ba82d-162">Rules are currently limited to network location based policies but will in the future be extended to other aspects of enterprise management.</span></span>

<span data-ttu-id="ba82d-163">Azure AD Premium 也提供相關報告和監視功能，可進一步延伸系統管理員對其 Azure RemoteApp 環境的控制能力。</span><span class="sxs-lookup"><span data-stu-id="ba82d-163">Azure AD Premium also offers reporting and monitoring capabilities that further extend the control the admin has over their Azure RemoteApp environment.</span></span>

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a><span data-ttu-id="ba82d-164">如何確定我的安全資源只能從 Azure RemoteApp 環境進行存取？</span><span class="sxs-lookup"><span data-stu-id="ba82d-164">How do I make sure my secure resource is accessible only from my Azure RemoteApp environment?</span></span>
<span data-ttu-id="ba82d-165">本文前幾節著重在保護 Azure RemoteApp 環境的存取。</span><span class="sxs-lookup"><span data-stu-id="ba82d-165">In previous sections of this article we focused on securing access to the Azure RemoteApp environment.</span></span> <span data-ttu-id="ba82d-166">透過選擇允許存取的使用者並設定存取規則以進一步控制使用者使用服務的方式，我們已經完成這個部分。</span><span class="sxs-lookup"><span data-stu-id="ba82d-166">We have accomplished that by choosing the users who are allowed access and setting up access rules to further control how they can use the service.</span></span>

<span data-ttu-id="ba82d-167">Azure RemoteApp 部署的常見案例是遠端應用程式需要與後端資源 (例如 SQL 資料庫) 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="ba82d-167">A common scenario for Azure RemoteApp deployments is that the remote applications need to communicate with a back-end resource, for example a SQL database.</span></span> <span data-ttu-id="ba82d-168">此資源裝載在內部部署環境中 (例如公司網路) 或雲端中 (例如 Azure IaaS)。</span><span class="sxs-lookup"><span data-stu-id="ba82d-168">This resource is hosted either on-premises (e.g. in a corporate network) or in the cloud (e.g. in Azure IaaS).</span></span> <span data-ttu-id="ba82d-169">系統管理員通常會想要確定，只有透過 Azure RemoteApp 部署的應用程式能夠存取後端資源，但 (舉例來說) 直接在使用者電腦上執行並透過公用網際網路存取的應用程式則不行。</span><span class="sxs-lookup"><span data-stu-id="ba82d-169">Administrators often want to make sure that the back-end resource can only be accessed by applications deployed via Azure RemoteApp and not for example by an application running directly on a user’s PC and accessing over public Internet.</span></span> <span data-ttu-id="ba82d-170">我們經常會將 Azure RemoteApp 視為受到集中管理的安全環境，且使用者只應該透過此途徑來與後端資源互動。</span><span class="sxs-lookup"><span data-stu-id="ba82d-170">Azure RemoteApp is often seen as the centrally-managed and secured environment and thus the only path through which users should interact with the back-end resource.</span></span>

<span data-ttu-id="ba82d-171">解決方法是將 Azure RemoteApp 環境和安全資源放在相同的 Azure 虛擬網路 (VNET) 中。</span><span class="sxs-lookup"><span data-stu-id="ba82d-171">The solution is to place both the Azure RemoteApp environment and the secure resource in the same Azure Virtual Network (VNET).</span></span> <span data-ttu-id="ba82d-172">如果資源位於不同網站，您可以建立站對站 VPN 連線，以便 (舉例來說) 建立一個橫跨 Azure 資料中心與客戶內部部署環境的 VNET。</span><span class="sxs-lookup"><span data-stu-id="ba82d-172">If the resource is in a different site, you can establish a site-to-site VPN connection, for example to create a VNet spanning the Azure data center and the customer on-premises environment.</span></span>

<span data-ttu-id="ba82d-173">Azure RemoteApp 支援兩種集合部署類型，您可以在其中提供您自己的 VNET：</span><span class="sxs-lookup"><span data-stu-id="ba82d-173">Azure RemoteApp supports two types of collection deployments where you can provide your own VNET:</span></span>

* <span data-ttu-id="ba82d-174">未加入網域：應用程式會有 VNET 中其他資源的「視線」。</span><span class="sxs-lookup"><span data-stu-id="ba82d-174">Non-domain-joined: the applications will have "line of sight" of the other resources in the VNET.</span></span> <span data-ttu-id="ba82d-175">比方說，這可以用來將應用程式連接至使用 SQL 驗證的 SQL 資料庫 (應用程式直接對資料庫驗證使用者)</span><span class="sxs-lookup"><span data-stu-id="ba82d-175">For example, this can be used to connect applications to a SQL database that uses SQL authentication (applications authenticate the user directly against the database)</span></span>
* <span data-ttu-id="ba82d-176">已加入網域：Azure RemoteApp 所使用的虛擬機器加入至 VNET 中的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="ba82d-176">Domain-joined: the virtual machines used by Azure RemoteApp are joined to a domain controller in the VNET.</span></span> <span data-ttu-id="ba82d-177">當應用程式需要對 Windows 網域控制站進行驗證以取得後端資源的存取權時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="ba82d-177">This is useful when the applications need to authenticate against a Windows Domain Controller in order to get access to a back-end resource.</span></span>
  <span data-ttu-id="ba82d-178">![Azure RemoteApp 中已加入網域的集合](./media/remoteapp-secureaccess/ra-domainjoined.png)</span><span class="sxs-lookup"><span data-stu-id="ba82d-178">![A domain-joined collection in Azure RemoteApp](./media/remoteapp-secureaccess/ra-domainjoined.png)</span></span>

### <a name="how-to-create-a-secure-connection-between-azure-and-my-on-premises-environment"></a><span data-ttu-id="ba82d-179">如何在 Azure 和內部部署環境之間建立安全連線</span><span class="sxs-lookup"><span data-stu-id="ba82d-179">How to create a secure connection between Azure and my on-premises environment</span></span>
<span data-ttu-id="ba82d-180">有數個組態選項可供用來連接 Azure 和內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="ba82d-180">There are several configuration options for connecting your Azure and on-premises environments.</span></span> <span data-ttu-id="ba82d-181">這裡有提供很好的選項概觀。</span><span class="sxs-lookup"><span data-stu-id="ba82d-181">A good overview of the options is available here.</span></span>

<span data-ttu-id="ba82d-182">在使用 Azure RemoteApp 時，您必須先設定 VNet，然後在集合的建立程序期間使用。</span><span class="sxs-lookup"><span data-stu-id="ba82d-182">With Azure RemoteApp you need to configure your VNet first, and then use it during the creation process of your collection.</span></span> 

## <a name="the-complete-solution"></a><span data-ttu-id="ba82d-183">完整解決方案</span><span class="sxs-lookup"><span data-stu-id="ba82d-183">The complete solution</span></span>
<span data-ttu-id="ba82d-184">下圖顯示完整的解決方案，我們在其中建置了起自使用者、經過 Azure RemoteApp (ARA)，並於最後進入後端資源的安全存取通道。</span><span class="sxs-lookup"><span data-stu-id="ba82d-184">The diagram below shows the complete solution where we have built a secure access channel from the end user, through Azure RemoteApp (ARA), into the backend resource.</span></span>
<span data-ttu-id="ba82d-185">![保護 Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png) 在階段 1 中，我們已選取使用者，並建立了控制 ARA 存取方式的存取規則。</span><span class="sxs-lookup"><span data-stu-id="ba82d-185">![Secure Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png) In Stage 1 we selected the users and created access rules that govern how ARA can be accessed.</span></span> <span data-ttu-id="ba82d-186">在下面的範例中，我們只允許從公司網路進行工作的使用者進行存取。</span><span class="sxs-lookup"><span data-stu-id="ba82d-186">In the example below we only allow access for users working from the corporate network.</span></span> <span data-ttu-id="ba82d-187">不符合此規定的使用者將完全無法存取 ARA 環境。</span><span class="sxs-lookup"><span data-stu-id="ba82d-187">Non-compliant users will not be able to access the ARA environment at all.</span></span>
<span data-ttu-id="ba82d-188">在「階段 2」中，我們公開了後端資源，但只能透過我們所控制的 VNet/VPN 組態來存取。</span><span class="sxs-lookup"><span data-stu-id="ba82d-188">In Stage 2 we have exposed the backend resource only through the VNet/VPN configuration which we control.</span></span> <span data-ttu-id="ba82d-189">Azure RemoteApp 已放置於相同的 VNet。</span><span class="sxs-lookup"><span data-stu-id="ba82d-189">Azure RemoteApp has been placed in the same VNet.</span></span> <span data-ttu-id="ba82d-190">最終結果是只能透過 ARA 環境存取資源。</span><span class="sxs-lookup"><span data-stu-id="ba82d-190">The end result is that the resource can only be accessed through the ARA environment.</span></span>

