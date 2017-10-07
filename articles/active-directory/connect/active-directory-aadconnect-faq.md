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
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="23c35-103">Azure Active Directory Connect 的常見問題集</span><span class="sxs-lookup"><span data-stu-id="23c35-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="23c35-104">一般安裝</span><span class="sxs-lookup"><span data-stu-id="23c35-104">General installation</span></span>
<span data-ttu-id="23c35-105">**問： 是否會安裝運作 hello Azure AD 全域管理員是否已啟用的 2FA？**</span><span class="sxs-lookup"><span data-stu-id="23c35-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="23c35-106">從 2016 年 2 月 hello 組建，以支援此功能。</span><span class="sxs-lookup"><span data-stu-id="23c35-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="23c35-107">**問： 是否有方法 tooinstall 無人看管的 Azure AD Connect？**</span><span class="sxs-lookup"><span data-stu-id="23c35-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="23c35-108">它是只支援的 tooinstall Azure AD Connect 使用 hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="23c35-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="23c35-109">不支援自動和無訊息安裝。</span><span class="sxs-lookup"><span data-stu-id="23c35-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="23c35-110">**問：我有一個樹系，但無法連線到其中的網域。如何安裝 Azure AD Connect？**</span><span class="sxs-lookup"><span data-stu-id="23c35-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="23c35-111">從 2016 年 2 月 hello 組建，以支援此功能。</span><span class="sxs-lookup"><span data-stu-id="23c35-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="23c35-112">**問： 沒有 hello 在 server core 上的 AD DS 健全狀況代理程式工作嗎？**</span><span class="sxs-lookup"><span data-stu-id="23c35-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="23c35-113">是。</span><span class="sxs-lookup"><span data-stu-id="23c35-113">Yes.</span></span> <span data-ttu-id="23c35-114">在安裝之後 hello 代理程式，您可以完成 hello 註冊程序使用下列 PowerShell cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="23c35-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="23c35-115">網路</span><span class="sxs-lookup"><span data-stu-id="23c35-115">Network</span></span>
<span data-ttu-id="23c35-116">**問： 我有防火牆、 網路裝置或其他項目，以限制 hello 最大時間連接可以維持開啟我的網路上。使用 Azure AD Connect 時，用戶端逾時閥值時間應該多長？**</span><span class="sxs-lookup"><span data-stu-id="23c35-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="23c35-117">所有的網路軟體、 實體裝置，或其他任何項目 hello 連接可以保持開啟的最長時間應該使用至少 5 分鐘 （300 秒） 的臨界值之間的連線限制 hello hello Azure AD Connect 的用戶端安裝所在的伺服器與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="23c35-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="23c35-118">這也適用於先前發行的 tooall Microsoft 身分識別同步處理工具。</span><span class="sxs-lookup"><span data-stu-id="23c35-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="23c35-119">**問：是否支援 SLD (單一標籤網域)？**</span><span class="sxs-lookup"><span data-stu-id="23c35-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="23c35-120"> 否，Azure AD Connect 不支援使用 SLD 的內部部署樹系/網域。</span><span class="sxs-lookup"><span data-stu-id="23c35-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="23c35-121">**問：是否支援有句點的 NetBios 名稱？**</span><span class="sxs-lookup"><span data-stu-id="23c35-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="23c35-122">否，Azure AD 連接不支援在內部部署樹系/網域 hello NetBios 名稱包含句點的位置 」。 「 hello 名稱中。</span><span class="sxs-lookup"><span data-stu-id="23c35-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="23c35-123">同盟</span><span class="sxs-lookup"><span data-stu-id="23c35-123">Federation</span></span>
<span data-ttu-id="23c35-124">**問： 我該怎麼辦如果我收到一封電子郵件，詢問 toorenew 我的 Office 365 憑證**</span><span class="sxs-lookup"><span data-stu-id="23c35-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="23c35-125">使用 hello 指南所述 hello[更新憑證](active-directory-aadconnect-o365-certs.md)上 toorenew hello 憑證的如何主題。</span><span class="sxs-lookup"><span data-stu-id="23c35-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="23c35-126">**問：我已經針對 O365 信賴憑證者設定「自動更新信賴憑證者」。我是否必須 tootake 任何動作時我的權杖簽署憑證會自動彙總？**</span><span class="sxs-lookup"><span data-stu-id="23c35-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="23c35-127">使用 hello 文件中所述的 hello 指引[更新憑證](active-directory-aadconnect-o365-certs.md)。</span><span class="sxs-lookup"><span data-stu-id="23c35-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="23c35-128">Environment</span><span class="sxs-lookup"><span data-stu-id="23c35-128">Environment</span></span>
<span data-ttu-id="23c35-129">**問： 是否支援 it toorename hello 伺服器在安裝 Azure AD Connect 之後？**</span><span class="sxs-lookup"><span data-stu-id="23c35-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="23c35-130">否。</span><span class="sxs-lookup"><span data-stu-id="23c35-130">No.</span></span> <span data-ttu-id="23c35-131">變更 hello 伺服器名稱將原因 hello 同步處理引擎 toonot 會無法 tooconnect toohello SQL database 和 hello 服務將不能 toostart。</span><span class="sxs-lookup"><span data-stu-id="23c35-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="23c35-132">身分識別資料</span><span class="sxs-lookup"><span data-stu-id="23c35-132">Identity data</span></span>
<span data-ttu-id="23c35-133">**問： hello UPN (userPrincipalName) 屬性，在 Azure AD 中的不符合 hello 由內部部署 UPN-為何？**</span><span class="sxs-lookup"><span data-stu-id="23c35-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="23c35-134"> 請參閱以下文章：</span><span class="sxs-lookup"><span data-stu-id="23c35-134">See these articles:</span></span>

* [<span data-ttu-id="23c35-135">使用者名稱不符合在 Office 365、 Azure 或 Intune hello 在內部部署 UPN 或替代登入識別碼</span><span class="sxs-lookup"><span data-stu-id="23c35-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="23c35-136">變更未同步處理 hello Azure Active Directory 同步作業工具之後變更 hello 的使用者帳戶 toouse 不同的同盟網域 UPN</span><span class="sxs-lookup"><span data-stu-id="23c35-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="23c35-137">您也可以如所述設定 Azure AD tooallow hello 同步處理引擎 tooupdate hello userPrincipalName [Azure AD Connect 同步處理服務功能](active-directory-aadconnectsyncservice-features.md)。</span><span class="sxs-lookup"><span data-stu-id="23c35-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="23c35-138">**問： 是否支援 it toosoft 比對內部部署 AD 群組/連絡人物件，與現有的 Azure AD 群組/連絡人物件？**</span><span class="sxs-lookup"><span data-stu-id="23c35-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="23c35-139">否，目前不支援。</span><span class="sxs-lookup"><span data-stu-id="23c35-139">No, this is currently not supported.</span></span>

<span data-ttu-id="23c35-140">**問： 是否支援 it toomanually 設定 ImmutableId 屬性上的現有 Azure AD 群組/連絡人物件 toohard 使其符合 tooon 內部部署 AD 群組/連絡人物件嗎？**</span><span class="sxs-lookup"><span data-stu-id="23c35-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="23c35-141">否，目前不支援。</span><span class="sxs-lookup"><span data-stu-id="23c35-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="23c35-142">自訂組態</span><span class="sxs-lookup"><span data-stu-id="23c35-142">Custom configuration</span></span>
<span data-ttu-id="23c35-143">**問： 哪裡適記載的 Azure AD Connect hello PowerShell 指令程式？**</span><span class="sxs-lookup"><span data-stu-id="23c35-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="23c35-144">記載此站台上的 hello cmdlet 的 hello 例外狀況，以供客戶使用不支援在 Azure AD Connect 中找到其他 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="23c35-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="23c35-145">**問： 是否可以使用 「 伺服器伺服器匯出/匯入 」 中找到*同步處理服務管理員*toomove 伺服器之間的組態？**</span><span class="sxs-lookup"><span data-stu-id="23c35-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="23c35-146">否。</span><span class="sxs-lookup"><span data-stu-id="23c35-146">No.</span></span> <span data-ttu-id="23c35-147">此選項將不會擷取所有組態設定，因此不應使用。</span><span class="sxs-lookup"><span data-stu-id="23c35-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="23c35-148">您應該改為使用 hello 精靈 toocreate hello 基底組態 hello 第二部伺服器上並使用 hello 同步處理規則編輯器 toogenerate PowerShell 指令碼 toomove 伺服器之間的任何自訂規則。</span><span class="sxs-lookup"><span data-stu-id="23c35-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="23c35-149">請參閱[變換移轉](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)。</span><span class="sxs-lookup"><span data-stu-id="23c35-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="23c35-150">**問： 是否可以密碼快取 hello Azure 登入頁面上，且可以這避免因為它包含了密碼 input 的元素與 hello autocomplete ="false"的屬性？**</span><span class="sxs-lookup"><span data-stu-id="23c35-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="23c35-151">我們目前不支援修改 hello HTML 屬性的 hello 密碼輸入欄位，包括 hello 自動完成標記。</span><span class="sxs-lookup"><span data-stu-id="23c35-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="23c35-152">我們目前使用中的功能，可讓您自訂的 Javascript，這可讓您 tooadd 任何屬性 toohello 密碼欄位。</span><span class="sxs-lookup"><span data-stu-id="23c35-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="23c35-153">應可在 2017 年下半年使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="23c35-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="23c35-154">**問： 在 hello Azure 登入頁面，會顯示先前登入成功的使用者的使用者名稱。可以關閉此行為嗎？**</span><span class="sxs-lookup"><span data-stu-id="23c35-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="23c35-155">我們目前不支援修改 hello HTML 屬性的 hello 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="23c35-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="23c35-156">我們目前使用中的功能，可讓您自訂的 Javascript，這可讓您 tooadd 任何屬性 toohello 密碼欄位。</span><span class="sxs-lookup"><span data-stu-id="23c35-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="23c35-157">應可在 2017 年下半年使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="23c35-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="23c35-158">**問： 是否有方法 tooprevent 並行工作階段？**</span><span class="sxs-lookup"><span data-stu-id="23c35-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="23c35-159">否。</span><span class="sxs-lookup"><span data-stu-id="23c35-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="23c35-160">疑難排解</span><span class="sxs-lookup"><span data-stu-id="23c35-160">Troubleshooting</span></span>
<span data-ttu-id="23c35-161">**問：如何取得 Azure AD Connect 的說明？**</span><span class="sxs-lookup"><span data-stu-id="23c35-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="23c35-162">搜尋 hello Microsoft 知識庫 (KB)</span><span class="sxs-lookup"><span data-stu-id="23c35-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="23c35-163">支援 Azure AD Connect 的相關技術解決方案 toocommon 中斷的修復問題的搜尋 hello Microsoft 知識庫 (KB)。</span><span class="sxs-lookup"><span data-stu-id="23c35-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="23c35-164">Microsoft Azure Active Directory 論壇</span><span class="sxs-lookup"><span data-stu-id="23c35-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="23c35-165">您可以搜尋和瀏覽的技術問題和解答的 hello 社群成員或詢問您自己的問題，依序按一下[這裡](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required)。</span><span class="sxs-lookup"><span data-stu-id="23c35-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="23c35-166">Azure AD Connect 客戶支援</span><span class="sxs-lookup"><span data-stu-id="23c35-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="23c35-167">使用此連結 tooget 支援透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="23c35-167">Use this link tooget support through hello Azure portal.</span></span>

