---
title: "Azure Active Directory Connect 常見問題集 - | Microsoft Docs"
description: "此頁面包含有關 Azure AD Connect 的常見問題集。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="e674d-103">Azure Active Directory Connect 的常見問題集</span><span class="sxs-lookup"><span data-stu-id="e674d-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="e674d-104">一般安裝</span><span class="sxs-lookup"><span data-stu-id="e674d-104">General installation</span></span>
<span data-ttu-id="e674d-105">**問：如果 Azure AD 全域管理員已啟用 2FA，安裝是否能夠運作？**</span><span class="sxs-lookup"><span data-stu-id="e674d-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="e674d-106">從 2016 年 2 月的組建開始便提供這項支援。</span><span class="sxs-lookup"><span data-stu-id="e674d-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="e674d-107">**問：是否有方法可自動安裝 Azure AD Connect？**</span><span class="sxs-lookup"><span data-stu-id="e674d-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="e674d-108">它僅支援使用安裝精靈來安裝 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="e674d-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="e674d-109">不支援自動和無訊息安裝。</span><span class="sxs-lookup"><span data-stu-id="e674d-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="e674d-110">**問：我有一個樹系，但無法連線到其中的網域。如何安裝 Azure AD Connect？**</span><span class="sxs-lookup"><span data-stu-id="e674d-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="e674d-111">從 2016 年 2 月的組建開始便提供這項支援。</span><span class="sxs-lookup"><span data-stu-id="e674d-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="e674d-112">**問︰AD DS 健康情況代理程式是否是在伺服器核心上運作？**</span><span class="sxs-lookup"><span data-stu-id="e674d-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="e674d-113">是。</span><span class="sxs-lookup"><span data-stu-id="e674d-113">Yes.</span></span> <span data-ttu-id="e674d-114">安裝代理程式之後，您可以使用下列 PowerShell Cmdlet 來完成註冊程序︰</span><span class="sxs-lookup"><span data-stu-id="e674d-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="e674d-115">網路</span><span class="sxs-lookup"><span data-stu-id="e674d-115">Network</span></span>
<span data-ttu-id="e674d-116">**問：我的防火牆、網路裝置或其他軟硬體會限制在網路上開啟連線的時間上限。使用 Azure AD Connect 時，用戶端逾時閥值時間應該多長？**</span><span class="sxs-lookup"><span data-stu-id="e674d-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="e674d-117">所有網路軟體、實體裝置或其他軟硬體限制連線開啟時間上限的閥值應該至少為 5 分鐘 (300 秒)，以便讓安裝 Azure AD Connect 用戶端的伺服器與 Azure Active Directory 連線。</span><span class="sxs-lookup"><span data-stu-id="e674d-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="e674d-118">這也適用於所有先前發行的  Microsoft Identity 同步處理工具。</span><span class="sxs-lookup"><span data-stu-id="e674d-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="e674d-119">**問：是否支援 SLD (單一標籤網域)？**</span><span class="sxs-lookup"><span data-stu-id="e674d-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="e674d-120">否，Azure AD Connect 不支援使用 SLD 的內部部署樹系/網域。</span><span class="sxs-lookup"><span data-stu-id="e674d-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="e674d-121">**問：是否支援有句點的 NetBios 名稱？**</span><span class="sxs-lookup"><span data-stu-id="e674d-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="e674d-122">否，Azure AD Connect 不支援 NetBios 名稱包含句點的內部部署樹系/網域。</span><span class="sxs-lookup"><span data-stu-id="e674d-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="e674d-123">同盟</span><span class="sxs-lookup"><span data-stu-id="e674d-123">Federation</span></span>
<span data-ttu-id="e674d-124">**問：如果我收到一封電子郵件，要求我更新我的 Office 365 憑證，該怎麼辦？**</span><span class="sxs-lookup"><span data-stu-id="e674d-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="e674d-125">請參考 [更新憑證](active-directory-aadconnect-o365-certs.md) 主題中概述的指導方針來了解如何更新憑證。</span><span class="sxs-lookup"><span data-stu-id="e674d-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="e674d-126">**問：我已經針對 O365 信賴憑證者設定「自動更新信賴憑證者」。當我的權杖簽署憑證自動換用時，需要採取任何動作嗎？**</span><span class="sxs-lookup"><span data-stu-id="e674d-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="e674d-127">請參考 [更新憑證](active-directory-aadconnect-o365-certs.md)一文中概述的指導方針。</span><span class="sxs-lookup"><span data-stu-id="e674d-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="e674d-128">Environment</span><span class="sxs-lookup"><span data-stu-id="e674d-128">Environment</span></span>
<span data-ttu-id="e674d-129">**問：安裝 Azure AD Connect 之後，是否支援重新命名伺服器？**</span><span class="sxs-lookup"><span data-stu-id="e674d-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="e674d-130">否。</span><span class="sxs-lookup"><span data-stu-id="e674d-130">No.</span></span> <span data-ttu-id="e674d-131">變更伺服器名稱將會導致同步處理引擎無法連接到 SQL 資料庫，服務將無法啟動。</span><span class="sxs-lookup"><span data-stu-id="e674d-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="e674d-132">身分識別資料</span><span class="sxs-lookup"><span data-stu-id="e674d-132">Identity data</span></span>
<span data-ttu-id="e674d-133">**問：Azure AD 中的 UPN (userPrincipalName) 屬性不符合內部部署的 UPN，為什麼？**</span><span class="sxs-lookup"><span data-stu-id="e674d-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="e674d-134">請參閱以下文章：</span><span class="sxs-lookup"><span data-stu-id="e674d-134">See these articles:</span></span>

* [<span data-ttu-id="e674d-135">Office 365、Azure 或 Intune 中的使用者名稱不符合內部部署的 UPN 或替代登入識別碼</span><span class="sxs-lookup"><span data-stu-id="e674d-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="e674d-136">在您將使用者帳戶的 UPN 變更為使用不同的同盟網域後，Azure Active Directory 同步作業工具未同步處理變更</span><span class="sxs-lookup"><span data-stu-id="e674d-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="e674d-137">您也可以將 Azure AD 設定為允許同步處理引擎更新 userPrincipalName，如 [Azure AD Connect 同步處理服務功能](active-directory-aadconnectsyncservice-features.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="e674d-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="e674d-138">**問：是否支援將內部部署 AD「群組/連絡人」物件與現有的 Azure AD「群組/連絡人」物件進行大致相符比對？**</span><span class="sxs-lookup"><span data-stu-id="e674d-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="e674d-139">否，目前不支援。</span><span class="sxs-lookup"><span data-stu-id="e674d-139">No, this is currently not supported.</span></span>

<span data-ttu-id="e674d-140">**問：是否支援將現有 Azure AD「群組/連絡人」物件上的 ImmutableId 屬性手動設定成與內部部署 AD「群組/連絡人」物件完全相符？**</span><span class="sxs-lookup"><span data-stu-id="e674d-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="e674d-141">否，目前不支援。</span><span class="sxs-lookup"><span data-stu-id="e674d-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="e674d-142">自訂組態</span><span class="sxs-lookup"><span data-stu-id="e674d-142">Custom configuration</span></span>
<span data-ttu-id="e674d-143">**問：Azure AD Connect 適用的 PowerShell Cmdlet 記載於何處？**</span><span class="sxs-lookup"><span data-stu-id="e674d-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="e674d-144">除了記載於本網站上的 Cmdlet，在 Azure AD Connect 中找到的其他 PowerShell Cmdlet 不支援客戶使用。</span><span class="sxs-lookup"><span data-stu-id="e674d-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="e674d-145">**問：我是否可以使用在 Synchronization Service Manager 中找到的「伺服器匯出/伺服器匯入」，在伺服器之間移動組態？**</span><span class="sxs-lookup"><span data-stu-id="e674d-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="e674d-146">否。</span><span class="sxs-lookup"><span data-stu-id="e674d-146">No.</span></span> <span data-ttu-id="e674d-147">此選項將不會擷取所有組態設定，因此不應使用。</span><span class="sxs-lookup"><span data-stu-id="e674d-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="e674d-148">您應該改用精靈在第二部伺服器上建立基底組態，並使用同步處理規則編輯器產生 PowerShell 指令碼，以在伺服器之間移動任何自訂規則。</span><span class="sxs-lookup"><span data-stu-id="e674d-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="e674d-149">請參閱[變換移轉](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)。</span><span class="sxs-lookup"><span data-stu-id="e674d-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="e674d-150">**問︰是否可針對 Azure 登入頁面密碼快取，而且是否可以因為它包含自動完成 ="false" 屬性的密碼輸入元素而避免此行為？**</span><span class="sxs-lookup"><span data-stu-id="e674d-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="e674d-151">我們目前不支援修改密碼輸入欄位的 HTML 屬性，包括自動完成標記。</span><span class="sxs-lookup"><span data-stu-id="e674d-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="e674d-152">我們目前正在開發適用於自訂 javascript 的功能，可讓您將任何屬性新增密碼欄位。</span><span class="sxs-lookup"><span data-stu-id="e674d-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="e674d-153">應可在 2017 年下半年使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="e674d-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="e674d-154">**問︰在 Azure 登入頁面上，會顯示先前登入成功之使用者的使用者名稱。可以關閉此行為嗎？**</span><span class="sxs-lookup"><span data-stu-id="e674d-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="e674d-155">我們目前不支援修改登入頁面的 HTML 屬性。</span><span class="sxs-lookup"><span data-stu-id="e674d-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="e674d-156">我們目前正在開發適用於自訂 javascript 的功能，可讓您將任何屬性新增密碼欄位。</span><span class="sxs-lookup"><span data-stu-id="e674d-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="e674d-157">應可在 2017 年下半年使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="e674d-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="e674d-158">**問︰是否辦法避免並行的工作階段？**</span><span class="sxs-lookup"><span data-stu-id="e674d-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="e674d-159">否。</span><span class="sxs-lookup"><span data-stu-id="e674d-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="e674d-160">疑難排解</span><span class="sxs-lookup"><span data-stu-id="e674d-160">Troubleshooting</span></span>
<span data-ttu-id="e674d-161">**問：如何取得 Azure AD Connect 的說明？**</span><span class="sxs-lookup"><span data-stu-id="e674d-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="e674d-162">搜尋 Microsoft 知識庫 (KB)</span><span class="sxs-lookup"><span data-stu-id="e674d-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="e674d-163">在 Microsoft 知識庫 (KB) 中搜尋有關 Azure AD Connect 支援的常見協助修正問題的技術解決方案。</span><span class="sxs-lookup"><span data-stu-id="e674d-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="e674d-164">Microsoft Azure Active Directory 論壇</span><span class="sxs-lookup"><span data-stu-id="e674d-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="e674d-165">按一下 [這裡](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required)，即可在社群中搜尋和瀏覽技術問題和答案，或提出自己的問題。</span><span class="sxs-lookup"><span data-stu-id="e674d-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="e674d-166">Azure AD Connect 客戶支援</span><span class="sxs-lookup"><span data-stu-id="e674d-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="e674d-167">使用此連結透過 Azure 入口網站取得支援。</span><span class="sxs-lookup"><span data-stu-id="e674d-167">Use this link to get support through the Azure portal.</span></span>

