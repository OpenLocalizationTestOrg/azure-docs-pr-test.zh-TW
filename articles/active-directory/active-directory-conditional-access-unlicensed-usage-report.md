---
title: "未經授權的使用報告 | Microsoft Docs"
description: "未經授權的使用報告可協助您識別使用 Azure AD 付費功能的未經授權使用者。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c0b4f455f067e825362bdecc02ea62d7984f0d31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="6b26b-103">未經授權的使用報告</span><span class="sxs-lookup"><span data-stu-id="6b26b-103">Unlicensed usage report</span></span>
<span data-ttu-id="6b26b-104">未經授權的使用報告可協助您識別使用 Azure AD 付費功能的未經授權使用者。</span><span class="sxs-lookup"><span data-stu-id="6b26b-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="6b26b-105">這可讓您充分利用您已購買的授權，以及確認您知道何時可能需要額外的授權。</span><span class="sxs-lookup"><span data-stu-id="6b26b-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="6b26b-106">此報告會顯示過去 30 天內有使用付費功能的情形。</span><span class="sxs-lookup"><span data-stu-id="6b26b-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="6b26b-107">報告結構</span><span class="sxs-lookup"><span data-stu-id="6b26b-107">Report structure</span></span>
| <span data-ttu-id="6b26b-108">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="6b26b-108">Column name</span></span> | <span data-ttu-id="6b26b-109">說明</span><span class="sxs-lookup"><span data-stu-id="6b26b-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6b26b-110">未經授權的使用者</span><span class="sxs-lookup"><span data-stu-id="6b26b-110">Unlicensed User</span></span> |<span data-ttu-id="6b26b-111">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="6b26b-111">Name of the user</span></span> |
| <span data-ttu-id="6b26b-112">功能</span><span class="sxs-lookup"><span data-stu-id="6b26b-112">Feature</span></span> |<span data-ttu-id="6b26b-113">功能名稱。</span><span class="sxs-lookup"><span data-stu-id="6b26b-113">The feature name.</span></span> <span data-ttu-id="6b26b-114">例如：條件式存取</span><span class="sxs-lookup"><span data-stu-id="6b26b-114">For example: conditional access</span></span> |
| <span data-ttu-id="6b26b-115">存取的應用程式</span><span class="sxs-lookup"><span data-stu-id="6b26b-115">Application Accessed</span></span> |<span data-ttu-id="6b26b-116">使用功能存取的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="6b26b-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="6b26b-117">例如︰Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6b26b-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="6b26b-118">如果使用者帳戶已遭刪除，「未經授權的使用者」資料行將會填入識別碼，例如 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="6b26b-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="6b26b-119">條件式存取功能</span><span class="sxs-lookup"><span data-stu-id="6b26b-119">Conditional access feature</span></span>
<span data-ttu-id="6b26b-120">未經授權的使用者如果沒有 Azure AD Premium 授權，則會在存取已套用條件式存取原則的服務時遭到標示。</span><span class="sxs-lookup"><span data-stu-id="6b26b-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="6b26b-121">這適用於 MFA/位置原則以及使用 Intune 的裝置原則。</span><span class="sxs-lookup"><span data-stu-id="6b26b-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="6b26b-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6b26b-122">See also</span></span>
* [<span data-ttu-id="6b26b-123">搭配使用條件式存取與 Office 365 和其他 Azure Active Directory 連線應用程式</span><span class="sxs-lookup"><span data-stu-id="6b26b-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="6b26b-124">開始使用 Azure AD 的條件式存取</span><span class="sxs-lookup"><span data-stu-id="6b26b-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

