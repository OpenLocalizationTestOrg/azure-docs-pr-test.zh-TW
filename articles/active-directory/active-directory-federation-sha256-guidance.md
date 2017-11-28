---
title: "Office 365 信賴憑證者信任 aaaChange 簽章雜湊演算法 |Microsoft 文件"
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
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="2a4a5-104">變更 Office 365 信賴憑證者信任的簽章雜湊演算法</span><span class="sxs-lookup"><span data-stu-id="2a4a5-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="2a4a5-105">概觀</span><span class="sxs-lookup"><span data-stu-id="2a4a5-105">Overview</span></span>
<span data-ttu-id="2a4a5-106">Active Directory Federation Services (AD FS) 會簽署它們無法竄改它語彙基元 tooMicrosoft Azure Active Directory tooensure。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-106">Active Directory Federation Services (AD FS) signs its tokens tooMicrosoft Azure Active Directory tooensure that they cannot be tampered with.</span></span> <span data-ttu-id="2a4a5-107">此簽章可以是以 SHA1 或 SHA256 為基礎。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="2a4a5-108">Azure Active Directory 現在支援使用 SHA256 演算法，簽章的權杖，我們建議您設定 hello hello 最高等級的安全性，權杖簽署演算法 tooSHA256。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting hello token-signing algorithm tooSHA256 for hello highest level of security.</span></span> <span data-ttu-id="2a4a5-109">本文說明 hello 步驟需要 tooset hello 權杖簽署演算法 toohello 更安全的 SHA256 層級。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-109">This article describes hello steps needed tooset hello token-signing algorithm toohello more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="2a4a5-110">Microsoft 建議使用 SHA256 做為 hello 演算法來簽署權杖，其會比 SHA1 更安全，但 SHA1 仍然是支援的選項。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-110">Microsoft recommends usage of SHA256 as hello algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-hello-token-signing-algorithm"></a><span data-ttu-id="2a4a5-111">變更 hello 權杖簽署演算法</span><span class="sxs-lookup"><span data-stu-id="2a4a5-111">Change hello token-signing algorithm</span></span>
<span data-ttu-id="2a4a5-112">設定 hello 簽章演算法，其中包含一個 hello 兩個下列程序之後，AD FS 會 for Office 365 信賴憑證者信任與 SHA256 簽署 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-112">After you have set hello signature algorithm with one of hello two processes below, AD FS signs hello tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="2a4a5-113">您不需要 toomake 任何額外的組態變更，且這項變更不會影響到您的能力 tooaccess Office 365 或其他 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-113">You don't need toomake any extra configuration changes, and this change has no impact on your ability tooaccess Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="2a4a5-114">AD FS 管理主控台</span><span class="sxs-lookup"><span data-stu-id="2a4a5-114">AD FS management console</span></span>
1. <span data-ttu-id="2a4a5-115">開啟 hello 主要 AD FS 伺服器上的 hello AD FS 管理主控台。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-115">Open hello AD FS management console on hello primary AD FS server.</span></span>
2. <span data-ttu-id="2a4a5-116">展開 hello AD FS 節點，然後按一下**信賴憑證者信任**。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-116">Expand hello AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="2a4a5-117">在您的 Office 365/Azure 信賴憑證者信任上按一下滑鼠右鍵，然後選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="2a4a5-118">選取 hello**進階** 索引標籤並選取 hello 安全雜湊演算法 SHA256。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-118">Select hello **Advanced** tab and select hello secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="2a4a5-119">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-119">Click **OK**.</span></span>

![SHA256 簽署演算法--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="2a4a5-121">AD FS PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="2a4a5-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="2a4a5-122">在任何 AD FS 伺服器上，以系統管理員權限開啟 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="2a4a5-123">使用 hello 組 hello 安全雜湊演算法**組 AdfsRelyingPartyTrust** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2a4a5-123">Set hello secure hash algorithm by using hello **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="2a4a5-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2a4a5-124">Also read</span></span>
* [<span data-ttu-id="2a4a5-125">使用 Azure AD Connect 修復 Office 365 信任</span><span class="sxs-lookup"><span data-stu-id="2a4a5-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

