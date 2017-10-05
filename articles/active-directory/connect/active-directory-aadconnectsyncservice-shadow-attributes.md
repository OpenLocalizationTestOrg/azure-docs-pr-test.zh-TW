---
title: "Azure AD Connect 同步處理服務陰影屬性 | Microsoft Docs"
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
ms.openlocfilehash: 0b6a7f22d744480a40a878c979986cdd7667109c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="e8633-103">Azure AD Connect 同步處理服務陰影屬性</span><span class="sxs-lookup"><span data-stu-id="e8633-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="e8633-104">大部分屬性是以它們在內部部署 Active Directory 中的相同方式，在 Azure AD 中表示。</span><span class="sxs-lookup"><span data-stu-id="e8633-104">Most attributes are represented the same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="e8633-105">但是某些屬性有一些特殊處理，而且在 Azure AD 中的屬性值可能不同於 Azure AD Connect 同步處理。</span><span class="sxs-lookup"><span data-stu-id="e8633-105">But some attributes have some special handling and the attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="e8633-106">簡介陰影屬性</span><span class="sxs-lookup"><span data-stu-id="e8633-106">Introducing shadow attributes</span></span>
<span data-ttu-id="e8633-107">某些屬性在 Azure AD 中有兩種表示法。</span><span class="sxs-lookup"><span data-stu-id="e8633-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="e8633-108">會儲存內部部署值和計算值。</span><span class="sxs-lookup"><span data-stu-id="e8633-108">Both the on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="e8633-109">這些額外的屬性稱為陰影屬性。</span><span class="sxs-lookup"><span data-stu-id="e8633-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="e8633-110">您會在其中看到此行為的兩個最常見屬性是 **userPrincipalName** 和 **proxyAddress**。</span><span class="sxs-lookup"><span data-stu-id="e8633-110">The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="e8633-111">這些屬性中有值代表未驗證網域時，就會發生屬性值的變更。</span><span class="sxs-lookup"><span data-stu-id="e8633-111">The change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="e8633-112">但是，連接中的同步處理引擎會讀取陰影屬性中的值，所以從其角度來看，屬性已由 Azure AD 確認。</span><span class="sxs-lookup"><span data-stu-id="e8633-112">But the sync engine in Connect reads the value in the shadow attribute so from its perspective, the attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="e8633-113">您無法使用 Azure 入口網站或 PowerShell 看到陰影屬性。</span><span class="sxs-lookup"><span data-stu-id="e8633-113">You cannot see the shadow attributes using the Azure portal or with PowerShell.</span></span> <span data-ttu-id="e8633-114">但是，了解概念可協助您針對特定案例進行疑難排解，其中屬性在內部部署和雲端中有不同的值。</span><span class="sxs-lookup"><span data-stu-id="e8633-114">But understanding the concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.</span></span>

<span data-ttu-id="e8633-115">若要進一步了解行為，請參閱來自 Fabrikam 的這個範例：</span><span class="sxs-lookup"><span data-stu-id="e8633-115">To better understand the behavior, look at this example from Fabrikam:</span></span>  
![網域](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="e8633-117">它們在其內部部署 Active Directory 中有多個 UPN 尾碼，但是它們只驗證其中一個。</span><span class="sxs-lookup"><span data-stu-id="e8633-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="e8633-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="e8633-118">userPrincipalName</span></span>
<span data-ttu-id="e8633-119">使用者在未驗證網域中具有下列屬性值︰</span><span class="sxs-lookup"><span data-stu-id="e8633-119">A user has the following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="e8633-120">屬性</span><span class="sxs-lookup"><span data-stu-id="e8633-120">Attribute</span></span> | <span data-ttu-id="e8633-121">值</span><span class="sxs-lookup"><span data-stu-id="e8633-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e8633-122">內部部署 userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="e8633-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="e8633-123">Azure AD shadowUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="e8633-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="e8633-124">Azure AD userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="e8633-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="e8633-125">userPrincipalName 屬性是您使用 PowerShell 時看到的值。</span><span class="sxs-lookup"><span data-stu-id="e8633-125">The userPrincipalName attribute is the value you see when using PowerShell.</span></span>

<span data-ttu-id="e8633-126">因為實際內部部署屬性值會儲存在 Azure AD 中，當您確認 fabrikam.com 網域時，Azure AD 會以 shadowUserPrincipalName 的值更新 userPrincipalName 屬性。</span><span class="sxs-lookup"><span data-stu-id="e8633-126">Since the real on-premises attribute value is stored in Azure AD, when you verify the fabrikam.com domain, Azure AD updates the userPrincipalName attribute with the value from the shadowUserPrincipalName.</span></span> <span data-ttu-id="e8633-127">您不需要同步處理 Azure AD Connect 的任何變更，讓這些值進行更新。</span><span class="sxs-lookup"><span data-stu-id="e8633-127">You do not have to synchronize any changes from Azure AD Connect for these values to be updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="e8633-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="e8633-128">proxyAddresses</span></span>
<span data-ttu-id="e8633-129">僅包含已驗證網域的相同程序也會針對 proxyAddresses 發生，但是具有某些額外邏輯。</span><span class="sxs-lookup"><span data-stu-id="e8633-129">The same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="e8633-130">針對已驗證網域的檢查只會對信箱使用者發生。</span><span class="sxs-lookup"><span data-stu-id="e8633-130">The check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="e8633-131">擁有郵件功能的使用者或連絡人代表另一個 Exchange 組織中的使用者，您可以將 proxyAddresses 中的任何值新增至這些物件。</span><span class="sxs-lookup"><span data-stu-id="e8633-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.</span></span>

<span data-ttu-id="e8633-132">對於信箱使用者，內部部署或 Exchange Online，只會顯示已驗證網域的值。</span><span class="sxs-lookup"><span data-stu-id="e8633-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="e8633-133">它看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="e8633-133">It could look like this:</span></span>

| <span data-ttu-id="e8633-134">屬性</span><span class="sxs-lookup"><span data-stu-id="e8633-134">Attribute</span></span> | <span data-ttu-id="e8633-135">值</span><span class="sxs-lookup"><span data-stu-id="e8633-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e8633-136">內部部署 proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="e8633-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="e8633-137">Exchange Online proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="e8633-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="e8633-138">在此情況下，**smtp:abbie.spencer@fabrikam.com**  已移除，因為該網域尚未驗證。</span><span class="sxs-lookup"><span data-stu-id="e8633-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="e8633-139">但是 Exchange 也會新增 **SIP:abbie.spencer@fabrikamonline.com** 。</span><span class="sxs-lookup"><span data-stu-id="e8633-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**.</span></span> <span data-ttu-id="e8633-140">Fabrikam 不曾使用 Lync/Skype 內部部署，但是 Azure AD 和 Exchange Online 為它進行準備。</span><span class="sxs-lookup"><span data-stu-id="e8633-140">Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="e8633-141">proxyAddresses 的此邏輯稱為 **ProxyCalc**。</span><span class="sxs-lookup"><span data-stu-id="e8633-141">This logic for proxyAddresses is referred to as **ProxyCalc**.</span></span> <span data-ttu-id="e8633-142">ProxyCalc 在使用者每次變更時叫用，其時機為︰</span><span class="sxs-lookup"><span data-stu-id="e8633-142">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="e8633-143">使用者已指派服務方案，該方案包含 Exchange Online，即使使用者沒有使用 Exchange 的授權。</span><span class="sxs-lookup"><span data-stu-id="e8633-143">The user has been assigned a service plan that includes Exchange Online even if the user was not licensed for Exchange.</span></span> <span data-ttu-id="e8633-144">例如，如果使用者已指派 Office E3 SKU，但是只指派 SharePoint Online。</span><span class="sxs-lookup"><span data-stu-id="e8633-144">For example, if the user is assigned the Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="e8633-145">即使您的信箱仍然是內部部署，也是如此。</span><span class="sxs-lookup"><span data-stu-id="e8633-145">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="e8633-146">屬性 msExchRecipientTypeDetails 具有值。</span><span class="sxs-lookup"><span data-stu-id="e8633-146">The attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="e8633-147">您對 proxyAddresses 或 userPrincipalName 進行變更。</span><span class="sxs-lookup"><span data-stu-id="e8633-147">You make a change to proxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="e8633-148">ProxyCalc 可能需要一些時間來處理使用者的變更，並且與 Azure AD Connect 匯出程序不是同步的。</span><span class="sxs-lookup"><span data-stu-id="e8633-148">ProxyCalc might take some time to process a change on a user and is not synchronous with the Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="e8633-149">ProxyCalc 邏輯具有本主題中未提及之進階案例的一些額外行為。</span><span class="sxs-lookup"><span data-stu-id="e8633-149">The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="e8633-150">本主題是讓您了解行為，而未記載所有內部邏輯。</span><span class="sxs-lookup"><span data-stu-id="e8633-150">This topic is provided for you to understand the behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="e8633-151">隔離的屬性值</span><span class="sxs-lookup"><span data-stu-id="e8633-151">Quarantined attribute values</span></span>
<span data-ttu-id="e8633-152">有重複的屬性值時，也會使用陰影屬性。</span><span class="sxs-lookup"><span data-stu-id="e8633-152">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="e8633-153">如需詳細資訊，請參閱[重複屬性恢復功能](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)。</span><span class="sxs-lookup"><span data-stu-id="e8633-153">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e8633-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e8633-154">See also</span></span>
* [<span data-ttu-id="e8633-155">Azure AD Connect 同步處理</span><span class="sxs-lookup"><span data-stu-id="e8633-155">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="e8633-156">[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="e8633-156">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
