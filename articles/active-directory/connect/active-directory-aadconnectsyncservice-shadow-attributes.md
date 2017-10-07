---
title: "aaaAzure AD Connect 同步處理服務陰影屬性 |Microsoft 文件"
description: "描述陰影屬性如何在 Azure AD Connect 同步處理服務中運作。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="60427-103">Azure AD Connect 同步處理服務陰影屬性</span><span class="sxs-lookup"><span data-stu-id="60427-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="60427-104">大部分屬性都表示相同 hello 在 Azure AD 和它們在您的內部部署 Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="60427-104">Most attributes are represented hello same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="60427-105">但某些屬性有一些特殊的處理和在 Azure AD 中的 hello 屬性值可能不同於 Azure AD Connect 同步處理。</span><span class="sxs-lookup"><span data-stu-id="60427-105">But some attributes have some special handling and hello attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="60427-106">簡介陰影屬性</span><span class="sxs-lookup"><span data-stu-id="60427-106">Introducing shadow attributes</span></span>
<span data-ttu-id="60427-107">某些屬性在 Azure AD 中有兩種表示法。</span><span class="sxs-lookup"><span data-stu-id="60427-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="60427-108">Hello 內部值和導出的值會儲存。</span><span class="sxs-lookup"><span data-stu-id="60427-108">Both hello on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="60427-109">這些額外的屬性稱為陰影屬性。</span><span class="sxs-lookup"><span data-stu-id="60427-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="60427-110">hello 兩個最常見屬性，您會看到這種行為是**userPrincipalName**和**proxyAddress**。</span><span class="sxs-lookup"><span data-stu-id="60427-110">hello two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="60427-111">這些屬性代表非已驗證網域中的值時，就會發生 hello 變更屬性值中。</span><span class="sxs-lookup"><span data-stu-id="60427-111">hello change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="60427-112">但在連接中的 hello 同步處理引擎讀取 hello 值 hello 陰影屬性中的，從其觀點來看，hello 屬性已確認 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="60427-112">But hello sync engine in Connect reads hello value in hello shadow attribute so from its perspective, hello attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="60427-113">您無法看到 hello 陰影屬性使用 hello Azure 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="60427-113">You cannot see hello shadow attributes using hello Azure portal or with PowerShell.</span></span> <span data-ttu-id="60427-114">但是了解 hello 概念可幫助您 tootroubleshoot 某些情況下 hello 屬性有不同的值在內部部署和雲端 hello。</span><span class="sxs-lookup"><span data-stu-id="60427-114">But understanding hello concept helps you tootroubleshoot certain scenarios where hello attribute has different values on-premises and in hello cloud.</span></span>

<span data-ttu-id="60427-115">toobetter 了解 hello 行為，看看這個範例來自 Fabrikam:</span><span class="sxs-lookup"><span data-stu-id="60427-115">toobetter understand hello behavior, look at this example from Fabrikam:</span></span>  
![網域](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="60427-117">它們在其內部部署 Active Directory 中有多個 UPN 尾碼，但是它們只驗證其中一個。</span><span class="sxs-lookup"><span data-stu-id="60427-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="60427-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="60427-118">userPrincipalName</span></span>
<span data-ttu-id="60427-119">使用者具有下列屬性值，在非驗證的網域中的 hello:</span><span class="sxs-lookup"><span data-stu-id="60427-119">A user has hello following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="60427-120">屬性</span><span class="sxs-lookup"><span data-stu-id="60427-120">Attribute</span></span> | <span data-ttu-id="60427-121">值</span><span class="sxs-lookup"><span data-stu-id="60427-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="60427-122">內部部署 userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="60427-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="60427-123">Azure AD shadowUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="60427-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="60427-124">Azure AD userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="60427-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="60427-125">hello userPrincipalName 屬性是使用 PowerShell 時，您所看到的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="60427-125">hello userPrincipalName attribute is hello value you see when using PowerShell.</span></span>

<span data-ttu-id="60427-126">因為 hello 實際在內部部署的屬性值會儲存在 Azure AD 中，當您驗證 hello fabrikam.com 網域，Azure AD 會更新與 hello shadowUserPrincipalName hello 值 hello userPrincipalName 屬性。</span><span class="sxs-lookup"><span data-stu-id="60427-126">Since hello real on-premises attribute value is stored in Azure AD, when you verify hello fabrikam.com domain, Azure AD updates hello userPrincipalName attribute with hello value from hello shadowUserPrincipalName.</span></span> <span data-ttu-id="60427-127">您沒有 toosynchronize 來自 Azure AD Connect 的更新這些值 toobe 的任何變更。</span><span class="sxs-lookup"><span data-stu-id="60427-127">You do not have toosynchronize any changes from Azure AD Connect for these values toobe updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="60427-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="60427-128">proxyAddresses</span></span>
<span data-ttu-id="60427-129">hello proxyAddresses，不過多了某些額外邏輯，也會發生相同的程序，只包含已驗證的網域。</span><span class="sxs-lookup"><span data-stu-id="60427-129">hello same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="60427-130">已驗證網域的 hello 檢查只會發生的信箱的使用者。</span><span class="sxs-lookup"><span data-stu-id="60427-130">hello check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="60427-131">擁有郵件功能的使用者或連絡人代表另一個 Exchange 組織中的使用者，並在 proxyAddresses toothese 物件，您可以加入任何值。</span><span class="sxs-lookup"><span data-stu-id="60427-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses toothese objects.</span></span>

<span data-ttu-id="60427-132">對於信箱使用者，內部部署或 Exchange Online，只會顯示已驗證網域的值。</span><span class="sxs-lookup"><span data-stu-id="60427-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="60427-133">它看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="60427-133">It could look like this:</span></span>

| <span data-ttu-id="60427-134">屬性</span><span class="sxs-lookup"><span data-stu-id="60427-134">Attribute</span></span> | <span data-ttu-id="60427-135">值</span><span class="sxs-lookup"><span data-stu-id="60427-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="60427-136">內部部署 proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="60427-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="60427-137">Exchange Online proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="60427-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="60427-138">在此情況下，**smtp:abbie.spencer@fabrikam.com ** 已移除，因為該網域尚未驗證。</span><span class="sxs-lookup"><span data-stu-id="60427-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="60427-139">但是 Exchange 也會新增 **SIP:abbie.spencer@fabrikamonline.com **。Fabrikam 不曾使用 Lync/Skype 內部部署，但是 Azure AD 和 Exchange Online 為它進行準備。</span><span class="sxs-lookup"><span data-stu-id="60427-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="60427-140">此邏輯 proxyAddresses 是參照的 tooas **ProxyCalc**。</span><span class="sxs-lookup"><span data-stu-id="60427-140">This logic for proxyAddresses is referred tooas **ProxyCalc**.</span></span> <span data-ttu-id="60427-141">ProxyCalc 在使用者每次變更時叫用，其時機為︰</span><span class="sxs-lookup"><span data-stu-id="60427-141">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="60427-142">hello 使用者已被指派包含 Exchange Online，即使 hello 使用者未獲得授權，適用於 Exchange 服務方案。</span><span class="sxs-lookup"><span data-stu-id="60427-142">hello user has been assigned a service plan that includes Exchange Online even if hello user was not licensed for Exchange.</span></span> <span data-ttu-id="60427-143">比方說，如果 hello 使用者被指派 hello Office E3 SKU，但只被指派 SharePoint Online。</span><span class="sxs-lookup"><span data-stu-id="60427-143">For example, if hello user is assigned hello Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="60427-144">即使您的信箱仍然是內部部署，也是如此。</span><span class="sxs-lookup"><span data-stu-id="60427-144">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="60427-145">hello 屬性 msExchRecipientTypeDetails 的值。</span><span class="sxs-lookup"><span data-stu-id="60427-145">hello attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="60427-146">您進行變更 tooproxyAddresses 或 userPrincipalName。</span><span class="sxs-lookup"><span data-stu-id="60427-146">You make a change tooproxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="60427-147">ProxyCalc 花一些時間 tooprocess 變更使用者，而且不同步與 hello Azure AD Connect 匯出程序。</span><span class="sxs-lookup"><span data-stu-id="60427-147">ProxyCalc might take some time tooprocess a change on a user and is not synchronous with hello Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="60427-148">hello ProxyCalc 邏輯都有某些進階案例中未記載於本主題的其他行為。</span><span class="sxs-lookup"><span data-stu-id="60427-148">hello ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="60427-149">本主題會提供您 toounderstand hello 行為和不文件內部的所有邏輯。</span><span class="sxs-lookup"><span data-stu-id="60427-149">This topic is provided for you toounderstand hello behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="60427-150">隔離的屬性值</span><span class="sxs-lookup"><span data-stu-id="60427-150">Quarantined attribute values</span></span>
<span data-ttu-id="60427-151">有重複的屬性值時，也會使用陰影屬性。</span><span class="sxs-lookup"><span data-stu-id="60427-151">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="60427-152">如需詳細資訊，請參閱[重複屬性恢復功能](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)。</span><span class="sxs-lookup"><span data-stu-id="60427-152">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="60427-153">另請參閱</span><span class="sxs-lookup"><span data-stu-id="60427-153">See also</span></span>
* [<span data-ttu-id="60427-154">Azure AD Connect 同步處理</span><span class="sxs-lookup"><span data-stu-id="60427-154">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="60427-155">[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="60427-155">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
