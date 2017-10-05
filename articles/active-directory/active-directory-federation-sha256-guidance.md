---
title: "變更 Office 365 信賴憑證者信任的簽章雜湊演算法 | Microsoft Docs"
description: "本頁面提供變更與 Office 365 搭配運作之同盟信任的 SHA 演算法的指導方針"
keywords: "SHA1,SHA256,O365,同盟,aadconnect,adfs,ad fs,變更 sha,同盟信任,信賴憑證者信任"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: c581b1468630a9f28204592c936360b72f42f0d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="93f4c-104">變更 Office 365 信賴憑證者信任的簽章雜湊演算法</span><span class="sxs-lookup"><span data-stu-id="93f4c-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="93f4c-105">概觀</span><span class="sxs-lookup"><span data-stu-id="93f4c-105">Overview</span></span>
<span data-ttu-id="93f4c-106">Active Directory 同盟服務 (AD FS) 會將其權杖簽署到 Microsoft Azure Active Directory 以確保它們無法被竄改。</span><span class="sxs-lookup"><span data-stu-id="93f4c-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="93f4c-107">此簽章可以是以 SHA1 或 SHA256 為基礎。</span><span class="sxs-lookup"><span data-stu-id="93f4c-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="93f4c-108">Azure Active Directory 現在支援以 SHA256 演算法簽署的權杖，建議您將權杖簽署演算法設定為 SHA256 以獲得最高層級的安全性。</span><span class="sxs-lookup"><span data-stu-id="93f4c-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="93f4c-109">本文說明將權杖簽署演算法設定為更安全 SHA256 層級所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="93f4c-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="93f4c-110">Microsoft 建議使用 SHA256 作為簽署權杖的演算法，因為它比 SHA1 安全，但 SHA1 仍保留為支援的選項。</span><span class="sxs-lookup"><span data-stu-id="93f4c-110">Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="93f4c-111">變更權杖簽署演算法</span><span class="sxs-lookup"><span data-stu-id="93f4c-111">Change the token-signing algorithm</span></span>
<span data-ttu-id="93f4c-112">使用下列兩個程序之一設定簽章演算法之後，AD FS 會使用 SHA256 簽署 Office 365 信賴憑證者信任的權杖。</span><span class="sxs-lookup"><span data-stu-id="93f4c-112">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="93f4c-113">您不需要另外進行任何組態變更，而且這項變更不會影響您對 Office 365 或其他 Azure AD 應用程式的存取能力。</span><span class="sxs-lookup"><span data-stu-id="93f4c-113">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="93f4c-114">AD FS 管理主控台</span><span class="sxs-lookup"><span data-stu-id="93f4c-114">AD FS management console</span></span>
1. <span data-ttu-id="93f4c-115">在主要 AD FS 伺服器上，開啟 [AD FS 管理主控台]。</span><span class="sxs-lookup"><span data-stu-id="93f4c-115">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="93f4c-116">展開 AD FS 節點，然後按一下 [信賴憑證者信任] 。</span><span class="sxs-lookup"><span data-stu-id="93f4c-116">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="93f4c-117">在您的 Office 365/Azure 信賴憑證者信任上按一下滑鼠右鍵，然後選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="93f4c-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="93f4c-118">選取 [進階]  索引標籤，然後選取安全雜湊演算法 SHA256。</span><span class="sxs-lookup"><span data-stu-id="93f4c-118">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="93f4c-119">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="93f4c-119">Click **OK**.</span></span>

![SHA256 簽署演算法--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="93f4c-121">AD FS PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="93f4c-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="93f4c-122">在任何 AD FS 伺服器上，以系統管理員權限開啟 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="93f4c-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="93f4c-123">使用 **Set-AdfsRelyingPartyTrust** Cmdlet 來設定安全雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="93f4c-123">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="93f4c-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="93f4c-124">Also read</span></span>
* [<span data-ttu-id="93f4c-125">使用 Azure AD Connect 修復 Office 365 信任</span><span class="sxs-lookup"><span data-stu-id="93f4c-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

