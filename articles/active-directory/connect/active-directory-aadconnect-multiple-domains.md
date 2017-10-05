---
title: "Azure AD Connect 多個網域"
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
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="8f47b-103">與 Azure AD 同盟的多網域支援</span><span class="sxs-lookup"><span data-stu-id="8f47b-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="8f47b-104">以下文件提供與 Office 365 或 Azure AD 網域同盟時，如何使用多個最上層網域和子網域的指引。</span><span class="sxs-lookup"><span data-stu-id="8f47b-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="8f47b-105">多個最上層網域支援</span><span class="sxs-lookup"><span data-stu-id="8f47b-105">Multiple top-level domain support</span></span>
<span data-ttu-id="8f47b-106">若要讓多個最上層網域與 Azure AD 同盟，您需要一些讓單一最上層網域同盟時不需要的額外組態。</span><span class="sxs-lookup"><span data-stu-id="8f47b-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="8f47b-107">當網域與 Azure AD 同盟時，系統會在 Azure 中的網域上設定幾個屬性。</span><span class="sxs-lookup"><span data-stu-id="8f47b-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span></span>  <span data-ttu-id="8f47b-108">其中一個重要屬性是 IssuerUri。</span><span class="sxs-lookup"><span data-stu-id="8f47b-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="8f47b-109">這是 Azure AD 用來識別與權杖相關聯之網域的 URI。</span><span class="sxs-lookup"><span data-stu-id="8f47b-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span></span>  <span data-ttu-id="8f47b-110">該 URI 不需要解析為任何內容，不過它必須是有效的 URI。</span><span class="sxs-lookup"><span data-stu-id="8f47b-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span></span>  <span data-ttu-id="8f47b-111">根據預設，Azure AD 會在內部部署 AD FS 組態中將其設定為同盟服務識別碼的值。</span><span class="sxs-lookup"><span data-stu-id="8f47b-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="8f47b-112">同盟服務識別碼是可唯一識別同盟服務的 URI。</span><span class="sxs-lookup"><span data-stu-id="8f47b-112">The federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="8f47b-113">同盟服務是能做為 Security Token Service 的 AD FS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="8f47b-113">The federation service is an instance of AD FS that functions as the security token service.</span></span> 
> 
> 

<span data-ttu-id="8f47b-114">您可以使用 PowerShell 命令 `Get-MsolDomainFederationSettings -DomainName <your domain>`檢視 IssuerUri。</span><span class="sxs-lookup"><span data-stu-id="8f47b-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="8f47b-116">當我們想要加入多個最上層網域時，問題便油然而生。</span><span class="sxs-lookup"><span data-stu-id="8f47b-116">A problem arises when we want to add more than one top-level domain.</span></span>  <span data-ttu-id="8f47b-117">例如，假設您已設定 Azure AD 和內部部署環境之間的同盟。</span><span class="sxs-lookup"><span data-stu-id="8f47b-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="8f47b-118">在本文中我使用 bmcontoso.com。</span><span class="sxs-lookup"><span data-stu-id="8f47b-118">For this document I am using bmcontoso.com.</span></span>  <span data-ttu-id="8f47b-119">現在我已加入第二個最上層網域 bmfabrikam.com。</span><span class="sxs-lookup"><span data-stu-id="8f47b-119">Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![網域](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="8f47b-121">當我們嘗試將 bmfabrikam.com 網域轉換為同盟時，會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="8f47b-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span></span>  <span data-ttu-id="8f47b-122">這個錯誤的原因在於，Azure AD 有一項限制，這項限制不允許多個網域的 IssuerURI 屬性擁有相同的值。</span><span class="sxs-lookup"><span data-stu-id="8f47b-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span></span>  

![同盟錯誤](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="8f47b-124">SupportMultipleDomain 參數</span><span class="sxs-lookup"><span data-stu-id="8f47b-124">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="8f47b-125">若要解決這個問題，我們需要使用 `-SupportMultipleDomain` 參數來加入不同的 IssuerUri。</span><span class="sxs-lookup"><span data-stu-id="8f47b-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="8f47b-126">這個參數可搭配下列 Cmdlet 使用：</span><span class="sxs-lookup"><span data-stu-id="8f47b-126">This parameter is used with the following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="8f47b-127">這個參數可讓 Azure AD 根據網域名稱設定 IssuerUri。</span><span class="sxs-lookup"><span data-stu-id="8f47b-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span></span>  <span data-ttu-id="8f47b-128">它將會成為 Azure AD 中所有目錄的唯一項目。</span><span class="sxs-lookup"><span data-stu-id="8f47b-128">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="8f47b-129">使用參數可讓 PowerShell 命令順利完成。</span><span class="sxs-lookup"><span data-stu-id="8f47b-129">Using the parameter allows the PowerShell command to complete successfully.</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="8f47b-131">從新 bmfabrikam.com 網域的設定中，您可以發現以下內容︰</span><span class="sxs-lookup"><span data-stu-id="8f47b-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="8f47b-133">請注意， `-SupportMultipleDomain` 不會變更依然設定為指向 adfs.bmcontoso.com 上之同盟服務的其他端點。</span><span class="sxs-lookup"><span data-stu-id="8f47b-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="8f47b-134">`-SupportMultipleDomain` 的另一個功用是確保 AD FS 系統在簽發給 Azure AD 之權杖中包含正確的簽發者值。</span><span class="sxs-lookup"><span data-stu-id="8f47b-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="8f47b-135">它會透過取用使用者 UPN 的網域部分並將其設定為 IssuerUri 中的網域 (即 https://{upn suffix}/adfs/services/trust)，以完成此動作。</span><span class="sxs-lookup"><span data-stu-id="8f47b-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="8f47b-136">因此在 Azure AD 或 Office 365 驗證期間，系統會以使用者權杖的 IssuerUri 項目來尋找 Azure AD 中的網域。</span><span class="sxs-lookup"><span data-stu-id="8f47b-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span></span>  <span data-ttu-id="8f47b-137">如果找不到相符項目，驗證將會失敗。</span><span class="sxs-lookup"><span data-stu-id="8f47b-137">If a match cannot be found the authentication will fail.</span></span> 

<span data-ttu-id="8f47b-138">例如，如果使用者的 UPN 是bsimon@bmcontoso.com，IssuerUri 中的項目語彙基元 AD FS 問題將會設定為 http://bmcontoso.com/adfs/services/trust。</span><span class="sxs-lookup"><span data-stu-id="8f47b-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="8f47b-139">這會比對 Azure AD 組態，且驗證將會成功。</span><span class="sxs-lookup"><span data-stu-id="8f47b-139">This will match the Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="8f47b-140">以下是實作此邏輯的自訂宣告規則：</span><span class="sxs-lookup"><span data-stu-id="8f47b-140">The following is the customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="8f47b-141">若要在嘗試加入新網域或轉換已加入的網域時使用 -SupportMultipleDomain 參數，您需要先設定同盟信任才能以原生方式支援。</span><span class="sxs-lookup"><span data-stu-id="8f47b-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span></span>  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="8f47b-142">如何更新 AD FS 與 Azure AD 之間的信任</span><span class="sxs-lookup"><span data-stu-id="8f47b-142">How to update the trust between AD FS and Azure AD</span></span>
<span data-ttu-id="8f47b-143">如果您未設定 AD FS 與 Azure AD 執行個體之間的同盟信任，可能需要重新建立此信任。</span><span class="sxs-lookup"><span data-stu-id="8f47b-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span></span>  <span data-ttu-id="8f47b-144">這是因為當我們最初未使用 `-SupportMultipleDomain` 參數進行設定時，系統會將 IssuerUri 設定為預設值。</span><span class="sxs-lookup"><span data-stu-id="8f47b-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span></span>  <span data-ttu-id="8f47b-145">在以下螢幕擷取畫面中，您可以看到 IssuerUri 的設定為 https://adfs.bmcontoso.com/adfs/services/trust。</span><span class="sxs-lookup"><span data-stu-id="8f47b-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="8f47b-146">回過頭來，如果我們已成功地在 Azure AD 入口網站中加入新網域，然後再嘗試使用 `Convert-MsolDomaintoFederated -DomainName <your domain>`轉換，我們會收到下列錯誤。</span><span class="sxs-lookup"><span data-stu-id="8f47b-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="8f47b-148">如果您嘗試加入 `-SupportMultipleDomain` 參數，我們將會收到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="8f47b-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="8f47b-150">單單嘗試針對原始網域執行 `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` ，也會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="8f47b-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span></span>

![同盟錯誤](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="8f47b-152">使用下列步驟來加入其他最上層網域。</span><span class="sxs-lookup"><span data-stu-id="8f47b-152">Use the steps below to add an additional top-level domain.</span></span>  <span data-ttu-id="8f47b-153">如果您已加入網域且未使用 `-SupportMultipleDomain` 參數，請從移除及更新原始網域的步驟開始。</span><span class="sxs-lookup"><span data-stu-id="8f47b-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span></span>  <span data-ttu-id="8f47b-154">如果您尚未加入最上層網域，可以從使用 Azure AD Connect 的 PowerShell 來加入網域開始。</span><span class="sxs-lookup"><span data-stu-id="8f47b-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="8f47b-155">請使用下列步驟來移除 Microsoft Online 信任，然後更新您的原始網域。</span><span class="sxs-lookup"><span data-stu-id="8f47b-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="8f47b-156">在 AD FS 同盟伺服器上，開啟 [AD FS 管理] </span><span class="sxs-lookup"><span data-stu-id="8f47b-156">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="8f47b-157">展開左側的 [信任關係] 和 [信賴憑證者信任]</span><span class="sxs-lookup"><span data-stu-id="8f47b-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="8f47b-158">刪除右側的 **Microsoft Office 365 身分識別平台** 項目。</span><span class="sxs-lookup"><span data-stu-id="8f47b-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="8f47b-159">![移除 Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="8f47b-159">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="8f47b-160">在已安裝[適用於 Windows PowerShell 的 Microsoft Azure Active Directory 模組](https://msdn.microsoft.com/library/azure/jj151815.aspx)的機器上執行下列命令：`$cred=Get-Credential`。</span><span class="sxs-lookup"><span data-stu-id="8f47b-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="8f47b-161">輸入欲同盟之 Azure AD 網域的全域管理員使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="8f47b-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="8f47b-162">在 PowerShell 中輸入 `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="8f47b-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="8f47b-163">在 PowerShell 中輸入 `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`。</span><span class="sxs-lookup"><span data-stu-id="8f47b-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="8f47b-164">這是針對原始網域。</span><span class="sxs-lookup"><span data-stu-id="8f47b-164">This is for the original domain.</span></span>  <span data-ttu-id="8f47b-165">所以使用上述網域後，它將會成為：`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="8f47b-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="8f47b-166">使用下列步驟以透過 PowerShell 加入新的最上層網域</span><span class="sxs-lookup"><span data-stu-id="8f47b-166">Use the following steps to add the new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="8f47b-167">在已安裝[適用於 Windows PowerShell 的 Microsoft Azure Active Directory 模組](https://msdn.microsoft.com/library/azure/jj151815.aspx)的機器上執行下列命令：`$cred=Get-Credential`。</span><span class="sxs-lookup"><span data-stu-id="8f47b-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="8f47b-168">輸入欲同盟之 Azure AD 網域的全域管理員使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="8f47b-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="8f47b-169">在 PowerShell 中輸入 `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="8f47b-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="8f47b-170">在 PowerShell 中輸入 `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="8f47b-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="8f47b-171">使用下列步驟以透過 Azure AD Connect 加入新的最上層網域。</span><span class="sxs-lookup"><span data-stu-id="8f47b-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="8f47b-172">從桌面或 [開始] 功能表啟動 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="8f47b-172">Launch Azure AD Connect from the desktop or start menu</span></span>
2. <span data-ttu-id="8f47b-173">選擇 [新增其他 Azure AD 網域] ![新增其他 Azure AD 網域](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="8f47b-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="8f47b-174">輸入您的 Azure AD 和 Active Directory 認證</span><span class="sxs-lookup"><span data-stu-id="8f47b-174">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="8f47b-175">選取要設定同盟的第二個網域。</span><span class="sxs-lookup"><span data-stu-id="8f47b-175">Select the second domain you wish to configure for federation.</span></span>
   <span data-ttu-id="8f47b-176">![新增其他 Azure AD 網域](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="8f47b-176">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="8f47b-177">按一下 [安裝]</span><span class="sxs-lookup"><span data-stu-id="8f47b-177">Click Install</span></span>

### <a name="verify-the-new-top-level-domain"></a><span data-ttu-id="8f47b-178">確認新的最上層網域</span><span class="sxs-lookup"><span data-stu-id="8f47b-178">Verify the new top-level domain</span></span>
<span data-ttu-id="8f47b-179">藉由使用 PowerShell 命令 `Get-MsolDomainFederationSettings -DomainName <your domain>`，您可以檢視更新的 IssuerUri。</span><span class="sxs-lookup"><span data-stu-id="8f47b-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span></span>  <span data-ttu-id="8f47b-180">以下螢幕擷取畫面顯示原始網域上的同盟設定已更新 http://bmcontoso.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="8f47b-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="8f47b-182">而新網域上的 IssuerUri 已設定為 https://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="8f47b-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="8f47b-184">子網域的支援</span><span class="sxs-lookup"><span data-stu-id="8f47b-184">Support for Sub-domains</span></span>
<span data-ttu-id="8f47b-185">在加入子網域時，因為 Azure AD 處理網域的方式，導致子網域會繼承父項的設定。</span><span class="sxs-lookup"><span data-stu-id="8f47b-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span></span>  <span data-ttu-id="8f47b-186">這表示 IssuerUri 需要與父項相符。</span><span class="sxs-lookup"><span data-stu-id="8f47b-186">This means that the IssuerUri needs to match the parents.</span></span>

<span data-ttu-id="8f47b-187">因此，假設我有 bmcontoso.com，後來再加入 corp.bmcontoso.com。</span><span class="sxs-lookup"><span data-stu-id="8f47b-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span></span>  <span data-ttu-id="8f47b-188">這表示來自 corp.bmcontoso.com 使用者的 IssuerUri 必須是 **http://bmcontoso.com/adfs/services/trust**。</span><span class="sxs-lookup"><span data-stu-id="8f47b-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="8f47b-189">不過，以上針對 Azure AD 實作的標準規則，會以為簽發者 **http://corp.bmcontoso.com/adfs/services/trust** 產生權杖。</span><span class="sxs-lookup"><span data-stu-id="8f47b-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="8f47b-190">的權杖，這與網域所需的值不符，因此驗證將會失敗。</span><span class="sxs-lookup"><span data-stu-id="8f47b-190">which will not match the domain's required value and authentication will fail.</span></span>

### <a name="how-to-enable-support-for-sub-domains"></a><span data-ttu-id="8f47b-191">如何啟用子網域的支援</span><span class="sxs-lookup"><span data-stu-id="8f47b-191">How To enable support for sub-domains</span></span>
<span data-ttu-id="8f47b-192">若要解決這個問題，您需要更新 Microsoft Online 的 AD FS 信賴憑證者信任。</span><span class="sxs-lookup"><span data-stu-id="8f47b-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span></span>  <span data-ttu-id="8f47b-193">若要這樣做，您必須設定自訂宣告規則，以使其在建構自訂簽發者值時能夠從使用者的 UPN 尾碼移除任何子網域。</span><span class="sxs-lookup"><span data-stu-id="8f47b-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span></span> 

<span data-ttu-id="8f47b-194">下列宣告將會執行這項操作︰</span><span class="sxs-lookup"><span data-stu-id="8f47b-194">The following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="8f47b-195">規則運算式中的最後一個數字設定了您根網域中的父網域數目。</span><span class="sxs-lookup"><span data-stu-id="8f47b-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span></span> <span data-ttu-id="8f47b-196">此處我所擁有的是 bmcontoso.com，因此必須有 2 個父網域。</span><span class="sxs-lookup"><span data-stu-id="8f47b-196">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="8f47b-197">如果要保留 3 個父網域 (亦即 corp.bmcontoso.com)，則數字就會是 3。</span><span class="sxs-lookup"><span data-stu-id="8f47b-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span></span> <span data-ttu-id="8f47b-198">最後可以指出一個範圍，系統一律會進行比對來符合網域數目上限。</span><span class="sxs-lookup"><span data-stu-id="8f47b-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span></span> <span data-ttu-id="8f47b-199">"{2,3}" 會比對出 2 到 3 個網域 (亦即 bmfabrikam.com 和 corp.bmcontoso.com)。</span><span class="sxs-lookup"><span data-stu-id="8f47b-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="8f47b-200">請使用下列步驟來加入自訂宣告，以支援子網域。</span><span class="sxs-lookup"><span data-stu-id="8f47b-200">Use the following steps to add a custom claim to support sub-domains.</span></span>

1. <span data-ttu-id="8f47b-201">開啟 [AD FS 管理]</span><span class="sxs-lookup"><span data-stu-id="8f47b-201">Open AD FS Management</span></span>
2. <span data-ttu-id="8f47b-202">以滑鼠右鍵按一下 Microsoft Online RP 信任，然後選擇 [編輯宣告規則]</span><span class="sxs-lookup"><span data-stu-id="8f47b-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="8f47b-203">選取第三個宣告規則並取代![編輯宣告](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="8f47b-203">Select the third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="8f47b-204">取代目前的宣告︰</span><span class="sxs-lookup"><span data-stu-id="8f47b-204">Replace the current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![取代宣告](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="8f47b-206">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8f47b-206">Click Ok.</span></span>  <span data-ttu-id="8f47b-207">按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="8f47b-207">Click Apply.</span></span>  <span data-ttu-id="8f47b-208">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8f47b-208">Click Ok.</span></span>  <span data-ttu-id="8f47b-209">關閉 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="8f47b-209">Close AD FS Management.</span></span>

