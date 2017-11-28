---
title: "aaaAzure AD 連接多個網域"
description: "本文件說明如何使用 O365 與 Azure AD 安裝及設定多個最上層網域。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="5bc8f-103">與 Azure AD 同盟的多網域支援</span><span class="sxs-lookup"><span data-stu-id="5bc8f-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="5bc8f-104">hello 下列文件指引如何 toouse 多個最上層網域和子網域時將與 Office 365 或 Azure AD 網域加入同盟。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="5bc8f-105">多個最上層網域支援</span><span class="sxs-lookup"><span data-stu-id="5bc8f-105">Multiple top-level domain support</span></span>
<span data-ttu-id="5bc8f-106">若要讓多個最上層網域與 Azure AD 同盟，您需要一些讓單一最上層網域同盟時不需要的額外組態。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="5bc8f-107">當使用 Azure AD 同盟網域時，在 Azure 中的 hello 網域會設定數個屬性。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="5bc8f-108">其中一個重要屬性是 IssuerUri。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="5bc8f-109">這是 URI，會使用 Azure AD tooidentify hello 語彙基元的 hello 網域是與相關聯。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="5bc8f-110">hello URI 不需要 tooresolve tooanything，但它必須是有效的 URI。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="5bc8f-111">根據預設，Azure AD 設定此 toohello hello federation service 識別碼中值您內部部署 AD FS 組態。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="5bc8f-112">hello federation service 識別碼是可唯一識別同盟服務的 URI。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="5bc8f-113">hello federation service 是 AD FS 該函式的執行個體，為 hello 安全性權杖服務。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="5bc8f-114">您可以使用 hello PowerShell 命令檢視 IssuerUri `Get-MsolDomainFederationSettings -DomainName <your domain>`。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="5bc8f-116">當我們想 tooadd 最上層的網域不止一個，就會發生問題。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="5bc8f-117">例如，假設您已設定 Azure AD 和內部部署環境之間的同盟。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="5bc8f-118">在本文中我使用 bmcontoso.com。現在我已加入第二個最上層網域 bmfabrikam.com。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![網域](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="5bc8f-120">當我們嘗試的 tooconvert 我們 bmfabrikam.com 網域 toobe 同盟時，我們會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="5bc8f-121">hello 原因是，Azure AD 包含不允許 hello IssuerUri 屬性 toohave hello 相同值的多個網域的條件約束。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![同盟錯誤](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="5bc8f-123">SupportMultipleDomain 參數</span><span class="sxs-lookup"><span data-stu-id="5bc8f-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="5bc8f-124">tooworkaround，我們需要能夠使用 hello 完成不同 IssuerUri tooadd`-SupportMultipleDomain`參數。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="5bc8f-125">這個參數會搭配 hello 下列 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5bc8f-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="5bc8f-126">這個參數可讓 Azure AD 設定 hello IssuerUri，讓它基礎 hello hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="5bc8f-127">它將會成為 Azure AD 中所有目錄的唯一項目。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="5bc8f-128">使用 hello 參數允許 hello PowerShell 命令 toocomplete 成功。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="5bc8f-130">看看我們新 bmfabrikam.com 網域的 hello 設定，可以看到 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5bc8f-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="5bc8f-132">請注意，`-SupportMultipleDomain`不會變更 hello adfs.bmcontoso.com 上其他端點，也就是仍設定的 toopoint tooour 同盟服務。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="5bc8f-133">另一項，`-SupportMultipleDomain`沒有可確保 hello AD FS 系統將 hello 正確的簽發者值包含在 Azure ad 簽發的權杖中。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="5bc8f-134">它會 hello 網域一部分 hello 使用者 UPN，以及將此設定為在 hello IssuerUri，也就是 https://{upn 尾碼 hello 網域} / adfs/services/信任。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="5bc8f-135">因此在驗證 tooAzure AD 或 Office 365 時，hello 使用者的權杖中的 hello IssuerUri 項目會是在 Azure AD 中使用的 toolocate hello 網域。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="5bc8f-136">如果相符項目找不到 hello 驗證將會失敗。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="5bc8f-137">例如，如果使用者的 UPN 是bsimon@bmcontoso.com，toohttp://bmcontoso.com/adfs/services/trust 會集中 hello 語彙基元的 AD FS 問題的 hello IssuerUri 項目。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="5bc8f-138">這會符合 hello Azure AD 組態，並驗證將會成功。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="5bc8f-139">hello 下面是 hello 實作此邏輯的自訂的宣告規則：</span><span class="sxs-lookup"><span data-stu-id="5bc8f-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="5bc8f-140">在順序 toouse hello-SupportMultipleDomain 切換嘗試 tooadd 新時，或轉換已加入網域，您需要 toohave 設定同盟的信任 toosupport 它們原本。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="5bc8f-141">Tooupdate hello 信任 AD FS 與 Azure AD 之間的方式</span><span class="sxs-lookup"><span data-stu-id="5bc8f-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="5bc8f-142">如果您並未設定 AD FS 與 Azure AD 執行個體之間的 hello 同盟信任，您可能需要 toore-建立信任。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="5bc8f-143">這是因為時最初設定，而不 hello`-SupportMultipleDomain`參數，hello IssuerUri 設 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="5bc8f-144">在 hello 低於您的螢幕擷取畫面可以看到 hello IssuerUri 設定 toohttps://adfs.bmcontoso.com/adfs/services/trust。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="5bc8f-145">因此現在，如果我們已成功地在 hello Azure AD 入口網站中加入新的網域，然後嘗試 tooconvert 使用`Convert-MsolDomaintoFederated -DomainName <your domain>`，得到下列錯誤 hello。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="5bc8f-147">如果您嘗試 tooadd hello`-SupportMultipleDomain`交換器我們將會收到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="5bc8f-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="5bc8f-149">只嘗試 toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` hello 上原始網域也會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="5bc8f-151">使用下列 tooadd 額外的最上層網域的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="5bc8f-152">如果您已加入網域並不是使用 hello`-SupportMultipleDomain`參數開頭 hello 移除和更新您的原始網域的步驟。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="5bc8f-153">如果您尚未新增最上層網域尚未就可以開始新增網域，使用 PowerShell 的 Azure AD Connect 的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="5bc8f-154">使用下列步驟 tooremove hello Microsoft Online 信任 hello，並更新您的原始網域。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="5bc8f-155">在 AD FS 同盟伺服器上，開啟 [AD FS 管理] </span><span class="sxs-lookup"><span data-stu-id="5bc8f-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="5bc8f-156">Hello 左側展開**信任關係**和**信賴憑證者信任**</span><span class="sxs-lookup"><span data-stu-id="5bc8f-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="5bc8f-157">在右邊的 hello，刪除 hello **Microsoft Office 365 識別平台**項目。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="5bc8f-158">![移除 Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="5bc8f-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="5bc8f-159">已在機器上[Azure Active Directory 的 Windows PowerShell 模組](https://msdn.microsoft.com/library/azure/jj151815.aspx)上面執行 hello 下列安裝： `$cred=Get-Credential`。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="5bc8f-160">輸入您正在同盟與 hello Azure AD 網域 hello 使用者名稱和密碼的全域管理員</span><span class="sxs-lookup"><span data-stu-id="5bc8f-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="5bc8f-161">在 PowerShell 中輸入 `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="5bc8f-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="5bc8f-162">在 PowerShell 中輸入 `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="5bc8f-163">這是 hello 原始網域。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-163">This is for hello original domain.</span></span>  <span data-ttu-id="5bc8f-164">上述網域會使用 hello:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="5bc8f-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="5bc8f-165">使用下列步驟 tooadd hello 新增最上層網域使用 PowerShell 的 hello</span><span class="sxs-lookup"><span data-stu-id="5bc8f-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="5bc8f-166">已在機器上[Azure Active Directory 的 Windows PowerShell 模組](https://msdn.microsoft.com/library/azure/jj151815.aspx)上面執行 hello 下列安裝： `$cred=Get-Credential`。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="5bc8f-167">輸入您正在同盟與 hello Azure AD 網域 hello 使用者名稱和密碼的全域管理員</span><span class="sxs-lookup"><span data-stu-id="5bc8f-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="5bc8f-168">在 PowerShell 中輸入 `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="5bc8f-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="5bc8f-169">在 PowerShell 中輸入 `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="5bc8f-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="5bc8f-170">使用下列步驟 tooadd hello 新增最上層網域使用 Azure AD Connect 的 hello。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="5bc8f-171">啟動 Azure AD Connect 從 hello 桌面或 [開始] 功能表</span><span class="sxs-lookup"><span data-stu-id="5bc8f-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="5bc8f-172">選擇 [新增其他 Azure AD 網域] ![新增其他 Azure AD 網域](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="5bc8f-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="5bc8f-173">輸入您的 Azure AD 和 Active Directory 認證</span><span class="sxs-lookup"><span data-stu-id="5bc8f-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="5bc8f-174">選取您想為同盟 tooconfigure hello 第二個網域。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="5bc8f-175">![新增其他 Azure AD 網域](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="5bc8f-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="5bc8f-176">按一下 [安裝]</span><span class="sxs-lookup"><span data-stu-id="5bc8f-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="5bc8f-177">確認 hello 新增最上層網域</span><span class="sxs-lookup"><span data-stu-id="5bc8f-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="5bc8f-178">使用 hello PowerShell 命令`Get-MsolDomainFederationSettings -DomainName <your domain>`您可以檢視 hello 更新 IssuerUri。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="5bc8f-179">hello 以下螢幕擷取畫面顯示 hello 同盟設定在我們的原始網域 http://bmcontoso.com/adfs/services/trust 更新</span><span class="sxs-lookup"><span data-stu-id="5bc8f-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="5bc8f-181">而且 hello IssuerUri 我們新的網域上已設定 toohttps://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="5bc8f-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="5bc8f-183">子網域的支援</span><span class="sxs-lookup"><span data-stu-id="5bc8f-183">Support for Sub-domains</span></span>
<span data-ttu-id="5bc8f-184">當您新增子網域時，由於 hello 方式 Azure AD 會處理網域，它會繼承 hello hello 父項設定。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="5bc8f-185">這表示該 hello IssuerUri 需要 toomatch hello 父代。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="5bc8f-186">因此，假設我有 bmcontoso.com，後來再加入 corp.bmcontoso.com。這表示該 hello IssuerUri corp.bmcontoso.com 的使用者將需要 toobe **http://bmcontoso.com/adfs/services/trust。**</span><span class="sxs-lookup"><span data-stu-id="5bc8f-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="5bc8f-187">Azure AD 實作上述 hello 標準規則，但是會產生為簽發者的語彙基元**http://corp.bmcontoso.com/adfs/services/trust。**</span><span class="sxs-lookup"><span data-stu-id="5bc8f-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="5bc8f-188">這不會符合 hello 網域的必要的值，驗證將會失敗。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="5bc8f-189">Tooenable 支援子網域的方式</span><span class="sxs-lookup"><span data-stu-id="5bc8f-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="5bc8f-190">這個 hello 周圍的順序 toowork 中 AD FS 信賴憑證者信任的 Microsoft Online 需要 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="5bc8f-191">toodo，您必須設定自訂宣告規則，使它剝 hello 使用者的 UPN 尾碼從任何子網域時建構 hello 自訂簽發者值。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="5bc8f-192">hello 下列宣告會這樣做：</span><span class="sxs-lookup"><span data-stu-id="5bc8f-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="5bc8f-193">hello hello 規則運算式中的最後一個號碼設定 hello 多少沒有根網域中的父網域。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="5bc8f-194">此處我所擁有的是 bmcontoso.com，因此必須有 2 個父網域。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="5bc8f-195">如果三個父網域已保留 toobe (也就是： corp.bmcontoso.com)，然後 hello 數目已經三個。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="5bc8f-196">可看出 Eventualy 範圍、 hello 相符項目一律都會 toomatch hello 的定義域的最大值。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="5bc8f-197">"{2，3}"會比對兩個 toothree 網域 (也就是： bmfabrikam.com 和 corp.bmcontoso.com)。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="5bc8f-198">使用下列步驟 tooadd hello 自訂宣告 toosupport 子網域。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="5bc8f-199">開啟 [AD FS 管理]</span><span class="sxs-lookup"><span data-stu-id="5bc8f-199">Open AD FS Management</span></span>
2. <span data-ttu-id="5bc8f-200">以滑鼠右鍵按一下 hello Microsoft 線上 RP trust，然後選擇 編輯宣告規則</span><span class="sxs-lookup"><span data-stu-id="5bc8f-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="5bc8f-201">選取 hello 第三個宣告規則，並取代![宣告編輯](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="5bc8f-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="5bc8f-202">取代 hello 目前宣告：</span><span class="sxs-lookup"><span data-stu-id="5bc8f-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![取代宣告](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="5bc8f-204">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-204">Click Ok.</span></span>  <span data-ttu-id="5bc8f-205">按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-205">Click Apply.</span></span>  <span data-ttu-id="5bc8f-206">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-206">Click Ok.</span></span>  <span data-ttu-id="5bc8f-207">關閉 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="5bc8f-207">Close AD FS Management.</span></span>

