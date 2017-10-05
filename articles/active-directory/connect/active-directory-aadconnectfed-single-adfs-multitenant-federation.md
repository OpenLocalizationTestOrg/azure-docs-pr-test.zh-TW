---
title: "將多個 Azure AD 和單一 AD FS 建立同盟關係 | Microsoft Docs"
description: "在本文件中，您將學習如何使用多個 Azure AD 和單一 AD FS 建立同盟。"
keywords: "聯盟, ADFS, AD FS, 多個租用戶, 單一 AD FS, 一個 ADFS, 多個租用戶同盟, 多樹系 adfs, aad 連線, 同盟, 跨租用戶同盟"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 436bf5905d2b203dc4cceea97f4fb90593df7111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="f8657-104">將多個 Azure AD 執行個體和單一 AD FS 執行個體建立同盟</span><span class="sxs-lookup"><span data-stu-id="f8657-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="f8657-105">如果樹系之間有雙向信任，單一高可用 AD FS 伺服器陣列就可以聯合多個樹系。</span><span class="sxs-lookup"><span data-stu-id="f8657-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="f8657-106">這些樹系可能會也可能不會對應到相同的 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="f8657-106">These multiple forests may or may not correspond to the same Azure Active Directory.</span></span> <span data-ttu-id="f8657-107">本文提供有關如何在單一 AD FS 部署和同步至不同 Azure AD 的多個樹系之間建立同盟的指示。</span><span class="sxs-lookup"><span data-stu-id="f8657-107">This article provides instructions on how to configure federation between a single AD FS deployment and more than one forests that sync to different Azure AD.</span></span>

![多租用戶與單一 AD FS 的同盟關係](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="f8657-109">在此案例中不支援裝置回寫和自動加入裝置。</span><span class="sxs-lookup"><span data-stu-id="f8657-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="f8657-110">Azure AD Connect 無法用來設定此案例中的同盟關係，因為 Azure AD Connect 可以在單一 Azure AD 中設定網域的同盟關係。</span><span class="sxs-lookup"><span data-stu-id="f8657-110">Azure AD Connect cannot be used to configure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="f8657-111">將 AD FS 和多個 Azure AD 建立同盟的步驟</span><span class="sxs-lookup"><span data-stu-id="f8657-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="f8657-112">請將 Azure Active Directory contoso.onmicrosoft.com 中的網域 contoso.com 已經與 contoso.com 內部部署 Active Directory 環境中安裝的 AD FS 內部部署建立同盟這點列入考慮。</span><span class="sxs-lookup"><span data-stu-id="f8657-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with the AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="f8657-113">Fabrikam.com 是 fabrikam.onmicrosoft.com Azure Active Directory 中的網域。</span><span class="sxs-lookup"><span data-stu-id="f8657-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="f8657-114">步驟 1︰建立雙向信任</span><span class="sxs-lookup"><span data-stu-id="f8657-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="f8657-115">若要 contoso.com 中的 AD FS 能夠驗證 fabrikam.com 中的使用者，需要 contoso.com 和 fabrikam.com 之間的雙向信任。</span><span class="sxs-lookup"><span data-stu-id="f8657-115">For AD FS in contoso.com to be able to authenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com.</span></span> <span data-ttu-id="f8657-116">請依照本[文章](https://technet.microsoft.com/library/cc816590.aspx)的指導方針建立雙向信任。</span><span class="sxs-lookup"><span data-stu-id="f8657-116">Follow the guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) to create the two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="f8657-117">步驟 2︰修改 contoso.com 同盟設定</span><span class="sxs-lookup"><span data-stu-id="f8657-117">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="f8657-118">與 AD FS 建立同盟的單一網域的預設簽發者為 "http://ADFSServiceFQDN/adfs/services/trust"，例如 “http://fs.contoso.com/adfs/services/trust”。</span><span class="sxs-lookup"><span data-stu-id="f8657-118">The default issuer set for a single domain federated to AD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="f8657-119">Azure Active Directory 要求每個同盟網域都需要擁有唯一簽發者。</span><span class="sxs-lookup"><span data-stu-id="f8657-119">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="f8657-120">由於相同的 AD FS 會建立兩個網域的同盟，因此必須修改簽發者值，所以該值對於 AD FS 與 Azure Active Directory 同盟的每個網域而言是唯一的值。</span><span class="sxs-lookup"><span data-stu-id="f8657-120">Since the same AD FS is going to federate two domains, the issuer value needs to be modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="f8657-121">在 AD FS 伺服器上，開啟 Azure AD PowerShell 並執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="f8657-121">On the AD FS server, open Azure AD PowerShell and perform the following steps:</span></span>
 
<span data-ttu-id="f8657-122">連線至 Azure Active Directory，其中包含網域 contoso.com Connect-MsolService Update contoso.com 的同盟設定 Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="f8657-122">Connect to the Azure Active Directory that contains the domain contoso.com Connect-MsolService Update the federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="f8657-123">在網域同盟設定中的簽發者會變更為 "http://contoso.com/adfs/services/trust"，並會針對 Azure AD 信賴憑證者信任新增發行宣告規則，以根據 UPN 尾碼發出正確的 issuerId 值。</span><span class="sxs-lookup"><span data-stu-id="f8657-123">Issuer in the domain federation setting will be changed to "http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for the Azure AD Relying Party Trust to issue the correct issuerId value based on the UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="f8657-124">步驟 3︰建立 fabrikam.com 與 AD FS 的同盟</span><span class="sxs-lookup"><span data-stu-id="f8657-124">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="f8657-125">在 Azure AD powershell 工作階段中執行下列步驟︰連線至包含網域 fabrikam.com 的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8657-125">In Azure AD powershell session perform the following steps: Connect to Azure Active Directory that contains the domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="f8657-126">將 fabrikam.com 受管理的網域轉換為同盟︰</span><span class="sxs-lookup"><span data-stu-id="f8657-126">Convert the fabrikam.com managed domain to federated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="f8657-127">上述作業會建立網域 fabrikam.com 與相同 AD FS 的同盟。</span><span class="sxs-lookup"><span data-stu-id="f8657-127">The above operation will federate the domain fabrikam.com with the same AD FS.</span></span> <span data-ttu-id="f8657-128">您可以使用兩個網域的 Get-msoldomainfederationsettings 確認網域設定。</span><span class="sxs-lookup"><span data-stu-id="f8657-128">You can verify the domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8657-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8657-129">Next steps</span></span>
[<span data-ttu-id="f8657-130">使用 Azure Active Directory 與 Active Directory 連線</span><span class="sxs-lookup"><span data-stu-id="f8657-130">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
