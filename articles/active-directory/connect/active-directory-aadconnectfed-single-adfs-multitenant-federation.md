---
title: "aaaFederating 與單一 AD FS 的多個 Azure AD |Microsoft 文件"
description: "本文件中，您將學習如何 toofederate 與單一的 AD FS 的多個 Azure AD。"
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
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="3bb6f-104">將多個 Azure AD 執行個體和單一 AD FS 執行個體建立同盟</span><span class="sxs-lookup"><span data-stu-id="3bb6f-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="3bb6f-105">如果樹系之間有雙向信任，單一高可用 AD FS 伺服器陣列就可以聯合多個樹系。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="3bb6f-106">這些多個樹系可能或可能無法對應 toohello 相同的 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-106">These multiple forests may or may not correspond toohello same Azure Active Directory.</span></span> <span data-ttu-id="3bb6f-107">這篇文章提供如何 tooconfigure 同盟與單一 AD FS 部署多個樹系，同步處理 toodifferent Azure AD 的指示。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-107">This article provides instructions on how tooconfigure federation between a single AD FS deployment and more than one forests that sync toodifferent Azure AD.</span></span>

![多租用戶與單一 AD FS 的同盟關係](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="3bb6f-109">在此案例中不支援裝置回寫和自動加入裝置。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="3bb6f-110">Azure AD Connect 不能使用的 tooconfigure 同盟，在此案例中，與 Azure AD Connect 可以在單一的 Azure AD 中設定同盟網域。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-110">Azure AD Connect cannot be used tooconfigure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="3bb6f-111">將 AD FS 和多個 Azure AD 建立同盟的步驟</span><span class="sxs-lookup"><span data-stu-id="3bb6f-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="3bb6f-112">請考慮在 Azure Active Directory contoso.onmicrosoft.com 網域 contoso.com 已經同盟與 hello AD FS 內部 contoso.com 在內部部署 Active Directory 環境中安裝。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with hello AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="3bb6f-113">Fabrikam.com 是 fabrikam.onmicrosoft.com Azure Active Directory 中的網域。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="3bb6f-114">步驟 1︰建立雙向信任</span><span class="sxs-lookup"><span data-stu-id="3bb6f-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="3bb6f-115">中的 AD FS 中 fabrikam.com contoso.com toobe 無法 tooauthenticate 使用者，contoso.com 和 fabrikam.com 之間需要雙向信任關係。請依照下列中的 hello 指導方針[文章](https://technet.microsoft.com/library/cc816590.aspx)toocreate hello 雙向信任關係。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-115">For AD FS in contoso.com toobe able tooauthenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com. Follow hello guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="3bb6f-116">步驟 2︰修改 contoso.com 同盟設定</span><span class="sxs-lookup"><span data-stu-id="3bb6f-116">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="3bb6f-117">hello 預設簽發者為單一網域同盟 tooAD FS"http://ADFSServiceFQDN/adfs/services/trust"，例如，"http://fs.contoso.com/adfs/services/trust 」 設定。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-117">hello default issuer set for a single domain federated tooAD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="3bb6f-118">Azure Active Directory 要求每個同盟網域都需要擁有唯一簽發者。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-118">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="3bb6f-119">Hello 相同 AD FS 會成為 toofederate 兩個網域，必須修改，使它是唯一的 AD FS 同盟與 Azure Active Directory 的每個網域的 toobe hello 簽發者值。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-119">Since hello same AD FS is going toofederate two domains, hello issuer value needs toobe modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="3bb6f-120">Hello AD FS 伺服器上，開啟 Azure AD PowerShell 並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3bb6f-120">On hello AD FS server, open Azure AD PowerShell and perform hello following steps:</span></span>
 
<span data-ttu-id="3bb6f-121">連接 toohello 包含 hello 網域 contoso.com Connect-msolservice 更新 hello de federación de contoso.com Update-msolfederateddomain-DomainName contoso.com 的 Azure Active Directory – SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="3bb6f-121">Connect toohello Azure Active Directory that contains hello domain contoso.com Connect-MsolService Update hello federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="3bb6f-122">將變更 hello 網域同盟設定中的簽發者太"http://contoso.com/adfs/services/trust 」 和發行宣告規則將會新增 hello Azure AD 信賴憑證者信任 tooissue hello 正確 issuerId 值根據 hello UPN 尾碼。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-122">Issuer in hello domain federation setting will be changed too"http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for hello Azure AD Relying Party Trust tooissue hello correct issuerId value based on hello UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="3bb6f-123">步驟 3︰建立 fabrikam.com 與 AD FS 的同盟</span><span class="sxs-lookup"><span data-stu-id="3bb6f-123">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="3bb6f-124">在 Azure AD powershell 工作階段執行下列步驟的 hello： 連接 tooAzure 包含 hello 網域 fabrikam.com 的 Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bb6f-124">In Azure AD powershell session perform hello following steps: Connect tooAzure Active Directory that contains hello domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="3bb6f-125">轉換 hello 管理 fabrikam.com 網域 toofederated:</span><span class="sxs-lookup"><span data-stu-id="3bb6f-125">Convert hello fabrikam.com managed domain toofederated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="3bb6f-126">上述操作的 hello 將同盟 hello 網域 fabrikam.com 以 hello 相同 AD FS。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-126">hello above operation will federate hello domain fabrikam.com with hello same AD FS.</span></span> <span data-ttu-id="3bb6f-127">您可以使用這兩個網域 Get-msoldomainfederationsettings 確認 hello 網域設定。</span><span class="sxs-lookup"><span data-stu-id="3bb6f-127">You can verify hello domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bb6f-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bb6f-128">Next steps</span></span>
[<span data-ttu-id="3bb6f-129">使用 Azure Active Directory 與 Active Directory 連線</span><span class="sxs-lookup"><span data-stu-id="3bb6f-129">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
