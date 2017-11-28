---
title: "aaaUnlicensed 使用量] 報表 |Microsoft 文件"
description: "hello 未經授權的使用方式報告可協助您識別未經授權的使用者正在使用付費型 Azure AD 的功能。"
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
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="18361-103">未經授權的使用報告</span><span class="sxs-lookup"><span data-stu-id="18361-103">Unlicensed usage report</span></span>
<span data-ttu-id="18361-104">hello 未經授權的使用方式報告可協助您識別未經授權的使用者正在使用付費型 Azure AD 的功能。</span><span class="sxs-lookup"><span data-stu-id="18361-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="18361-105">這可讓您 toomake 更妥善運用您購買的授權和 tooidentify 您知道何時您可能需要額外的授權。</span><span class="sxs-lookup"><span data-stu-id="18361-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="18361-106">hello 報告會顯示作用中的 hello 付費功能在 hello 過去 30 天的使用方式。</span><span class="sxs-lookup"><span data-stu-id="18361-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="18361-107">報告結構</span><span class="sxs-lookup"><span data-stu-id="18361-107">Report structure</span></span>
| <span data-ttu-id="18361-108">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="18361-108">Column name</span></span> | <span data-ttu-id="18361-109">說明</span><span class="sxs-lookup"><span data-stu-id="18361-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18361-110">未經授權的使用者</span><span class="sxs-lookup"><span data-stu-id="18361-110">Unlicensed User</span></span> |<span data-ttu-id="18361-111">Hello 使用者名稱</span><span class="sxs-lookup"><span data-stu-id="18361-111">Name of hello user</span></span> |
| <span data-ttu-id="18361-112">功能</span><span class="sxs-lookup"><span data-stu-id="18361-112">Feature</span></span> |<span data-ttu-id="18361-113">hello 的功能名稱。</span><span class="sxs-lookup"><span data-stu-id="18361-113">hello feature name.</span></span> <span data-ttu-id="18361-114">例如：條件式存取</span><span class="sxs-lookup"><span data-stu-id="18361-114">For example: conditional access</span></span> |
| <span data-ttu-id="18361-115">存取的應用程式</span><span class="sxs-lookup"><span data-stu-id="18361-115">Application Accessed</span></span> |<span data-ttu-id="18361-116">hello 與 hello 功能正在存取的 hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="18361-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="18361-117">例如︰Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="18361-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="18361-118">如果使用者帳戶已被刪除 hello '未經授權使用者' 將會填入資料行識別碼，例如 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="18361-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="18361-119">條件式存取功能</span><span class="sxs-lookup"><span data-stu-id="18361-119">Conditional access feature</span></span>
<span data-ttu-id="18361-120">未經授權的使用者如果沒有 Azure AD Premium 授權，則會在存取已套用條件式存取原則的服務時遭到標示。</span><span class="sxs-lookup"><span data-stu-id="18361-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="18361-121">這適用於 tooMFA/位置原則，以及裝置原則，使用 Intune。</span><span class="sxs-lookup"><span data-stu-id="18361-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="18361-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="18361-122">See also</span></span>
* [<span data-ttu-id="18361-123">搭配使用條件式存取與 Office 365 和其他 Azure Active Directory 連線應用程式</span><span class="sxs-lookup"><span data-stu-id="18361-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="18361-124">開始使用條件式存取 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="18361-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

