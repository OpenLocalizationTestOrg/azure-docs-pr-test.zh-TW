---
title: "Azure AD Connect 同步︰如何管理 Azure AD 服務帳戶 | Microsoft Docs"
description: "本主題將說明如何還原 Azure AD 服務帳戶。"
services: active-directory
keywords: "AADSTS70002, AADSTS50054, 如何重設 Azure AD Connect 同步處理連接器服務帳戶的密碼"
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
ms.openlocfilehash: 8e9e8192ee4fcb636b5be91d2616acbc9120c8c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="7ecff-104">Azure AD Connect 同步處理︰如何管理 Azure AD 服務帳戶</span><span class="sxs-lookup"><span data-stu-id="7ecff-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="7ecff-105">Azure AD 連接器所使用的服務帳戶應該是免費的服務。</span><span class="sxs-lookup"><span data-stu-id="7ecff-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="7ecff-106">如果您需要重設其認證，則這個主題適合您。</span><span class="sxs-lookup"><span data-stu-id="7ecff-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="7ecff-107">例如，如果全域管理員不小心使用 PowerShell 重設了服務帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="7ecff-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="7ecff-108">重設認證</span><span class="sxs-lookup"><span data-stu-id="7ecff-108">Reset the credentials</span></span>
<span data-ttu-id="7ecff-109">如果 Azure AD 連接器上定義的服務帳戶因驗證問題而無法連線至 Azure AD，就可以重設密碼。</span><span class="sxs-lookup"><span data-stu-id="7ecff-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="7ecff-110">登入 Azure AD Connect 同步處理伺服器，並啟動 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="7ecff-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="7ecff-111">執行 `Add-ADSyncAADServiceAccount`。</span><span class="sxs-lookup"><span data-stu-id="7ecff-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="7ecff-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="7ecff-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="7ecff-113">提供 Azure AD 全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="7ecff-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="7ecff-114">這個 Cmdlet 會重設服務帳戶的密碼，並在 Azure AD 和同步處理引擎中加以更新。</span><span class="sxs-lookup"><span data-stu-id="7ecff-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="7ecff-115">這些步驟可以解決的已知問題</span><span class="sxs-lookup"><span data-stu-id="7ecff-115">Known issues these steps can solve</span></span>
<span data-ttu-id="7ecff-116">本節是客戶回報的錯誤清單，這些錯誤已經透過重設 Azure AD 服務帳戶的認證來修正。</span><span class="sxs-lookup"><span data-stu-id="7ecff-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="7ecff-117">事件 6900</span><span class="sxs-lookup"><span data-stu-id="7ecff-117">Event 6900</span></span>  
<span data-ttu-id="7ecff-118">伺服器在處理密碼變更通知時發生未預期的錯誤︰</span><span class="sxs-lookup"><span data-stu-id="7ecff-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="7ecff-119">AADSTS70002︰驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecff-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="7ecff-120">AADSTS50054︰使用舊密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="7ecff-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="7ecff-121">事件 659</span><span class="sxs-lookup"><span data-stu-id="7ecff-121">Event 659</span></span>  
<span data-ttu-id="7ecff-122">擷取密碼原則同步處理設定時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecff-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="7ecff-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException：</span><span class="sxs-lookup"><span data-stu-id="7ecff-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="7ecff-124">AADSTS70002︰驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecff-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="7ecff-125">AADSTS50054︰使用舊密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="7ecff-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ecff-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ecff-126">Next steps</span></span>
<span data-ttu-id="7ecff-127">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="7ecff-127">**Overview topics**</span></span>

* [<span data-ttu-id="7ecff-128">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="7ecff-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="7ecff-129">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ecff-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

