---
title: "Azure Active Directory B2C：針對建立租用戶進行疑難排解 | Microsoft Docs"
description: "關於建立 Azure Active Directory 或 Azure Active Directory B2C 租用戶的問題與解決方法。"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="f5db7-103">針對建立 Azure Active Directory 或 Azure Active Directory B2C 租用戶進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f5db7-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="f5db7-104">建立 Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="f5db7-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="f5db7-105">如果您無法在 hello 第一次嘗試建立 Azure Active Directory (Azure AD) 租用戶，再試一次。</span><span class="sxs-lookup"><span data-stu-id="f5db7-105">If you can't create an Azure Active Directory (Azure AD) tenant on hello first attempt, try again.</span></span> <span data-ttu-id="f5db7-106">如果 hello 問題持續發生，請連絡 Azure 支援。</span><span class="sxs-lookup"><span data-stu-id="f5db7-106">If hello problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="f5db7-107">建立 Azure AD B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="f5db7-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="f5db7-108">如果您遇到問題時您[建立 Azure Active Directory B2C (Azure AD B2C) 租用戶](active-directory-b2c-get-started.md)，再試一次 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="f5db7-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try hello following options:</span></span>

* <span data-ttu-id="f5db7-109">如果您的租用戶的清單中，不會顯示 hello Azure AD B2C 租用戶，再試一次 toocreate hello 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f5db7-109">If hello Azure AD B2C tenant doesn't show up in your list of tenants, try again toocreate hello tenant.</span></span>
* <span data-ttu-id="f5db7-110">如果 hello Azure AD B2C 租用戶確實會顯示在您的租用戶的清單中，您會看到下列錯誤訊息的 hello 刪除 hello 租用戶，並重新建立它：</span><span class="sxs-lookup"><span data-stu-id="f5db7-110">If hello Azure AD B2C tenant does show up in your list of tenants and you see hello following  error message, delete hello tenant and create it again:</span></span>

    <span data-ttu-id="f5db7-111">"無法完成建立 hello B2C 租用戶 'contosob2c' hello。</span><span class="sxs-lookup"><span data-stu-id="f5db7-111">"Could not complete hello creation of hello B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="f5db7-112">如需詳細指引，請造訪此[連結](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409)。」</span><span class="sxs-lookup"><span data-stu-id="f5db7-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="f5db7-113">那里已知問題，當您刪除現有的 Azure AD B2C 租用戶，並使用 hello 重新建立相同的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="f5db7-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using hello same domain name.</span></span> <span data-ttu-id="f5db7-114">當您建立新的 Azure AD B2C 租用戶時，您必須使用不同的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="f5db7-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="f5db7-115">若這些解決方法無效，請連絡 Azure 支援中心。</span><span class="sxs-lookup"><span data-stu-id="f5db7-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="f5db7-116">如需詳細資訊，請參閱[提出 Azure AD B2C 的支援要求](active-directory-b2c-support.md)。</span><span class="sxs-lookup"><span data-stu-id="f5db7-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

