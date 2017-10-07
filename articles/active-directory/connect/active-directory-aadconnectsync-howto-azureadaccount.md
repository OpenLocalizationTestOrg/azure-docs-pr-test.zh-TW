---
title: "Azure AD Connect 同步： 如何 toomanage hello Azure AD 服務帳戶 |Microsoft 文件"
description: "本主題將說明如何 toorestore hello Azure AD 服務帳戶。"
services: active-directory
keywords: "如何 tooreset hello 密碼 AADSTS70002、 AADSTS50054，hello Azure AD Connect 同步處理連接器服務帳戶"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="39065-104">Azure AD Connect 同步： 如何 toomanage hello Azure AD 服務帳戶</span><span class="sxs-lookup"><span data-stu-id="39065-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="39065-105">hello hello Azure AD 連接器所使用的服務帳戶應該 toobe 服務可用。</span><span class="sxs-lookup"><span data-stu-id="39065-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="39065-106">如果您需要 tooreset 其認證，本主題是供您。</span><span class="sxs-lookup"><span data-stu-id="39065-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="39065-107">例如，如果錯誤重設 hello 密碼 hello 服務帳戶使用 PowerShell，在具有全域管理員。</span><span class="sxs-lookup"><span data-stu-id="39065-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="39065-108">重設 hello 認證</span><span class="sxs-lookup"><span data-stu-id="39065-108">Reset hello credentials</span></span>
<span data-ttu-id="39065-109">如果 hello hello Azure AD 連接器上定義的服務帳戶無法聯繫 tooauthentication 問題原因的 Azure AD，hello 密碼可以重設。</span><span class="sxs-lookup"><span data-stu-id="39065-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="39065-110">登入 toohello Azure AD Connect 同步處理伺服器，並啟動 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="39065-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="39065-111">執行 `Add-ADSyncAADServiceAccount`。</span><span class="sxs-lookup"><span data-stu-id="39065-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="39065-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="39065-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="39065-113">提供 Azure AD 全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="39065-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="39065-114">此 cmdlet 會重設 hello hello 服務帳戶的密碼，並在 Azure AD 和 hello 同步處理引擎中更新它。</span><span class="sxs-lookup"><span data-stu-id="39065-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="39065-115">這些步驟可以解決的已知問題</span><span class="sxs-lookup"><span data-stu-id="39065-115">Known issues these steps can solve</span></span>
<span data-ttu-id="39065-116">本節是一份 hello Azure AD 服務帳戶上重設認證已修正客戶所報告的錯誤。</span><span class="sxs-lookup"><span data-stu-id="39065-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="39065-117">事件 6900</span><span class="sxs-lookup"><span data-stu-id="39065-117">Event 6900</span></span>  
<span data-ttu-id="39065-118">hello 伺服器處理密碼變更通知時發生未預期的錯誤：</span><span class="sxs-lookup"><span data-stu-id="39065-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="39065-119">AADSTS70002︰驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="39065-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="39065-120">AADSTS50054︰使用舊密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="39065-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="39065-121">事件 659</span><span class="sxs-lookup"><span data-stu-id="39065-121">Event 659</span></span>  
<span data-ttu-id="39065-122">擷取密碼原則同步處理設定時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="39065-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="39065-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException：</span><span class="sxs-lookup"><span data-stu-id="39065-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="39065-124">AADSTS70002︰驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="39065-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="39065-125">AADSTS50054︰使用舊密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="39065-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39065-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39065-126">Next steps</span></span>
<span data-ttu-id="39065-127">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="39065-127">**Overview topics**</span></span>

* [<span data-ttu-id="39065-128">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="39065-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="39065-129">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39065-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

