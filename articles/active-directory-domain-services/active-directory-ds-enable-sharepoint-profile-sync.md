---
title: "Azure Active Directory Domain Services：啟用對 SharePoint User Profile Service 的支援 | Microsoft Docs"
description: "設定 Azure Active Directory Domain Services 受管理網域以支援 SharePoint Server 的設定檔同步處理"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: c3c923b5c9cd652f0c5b0ec98c1cda740f180122
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="c53d6-103">設定受管理網域以支援 SharePoint Server 的設定檔同步處理</span><span class="sxs-lookup"><span data-stu-id="c53d6-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="c53d6-104">SharePoint Server 包含用來同步處理使用者設定檔的 User Profile Service。</span><span class="sxs-lookup"><span data-stu-id="c53d6-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="c53d6-105">若要設定 User Profile Service，必須在 Active Directory 網域授與適當的權限。</span><span class="sxs-lookup"><span data-stu-id="c53d6-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="c53d6-106">如需詳細資訊，請參閱[授與 Active Directory Domain Services 權限以供 SharePoint Server 2013 中的設定檔同步處理使用](https://technet.microsoft.com/library/hh296982.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c53d6-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="c53d6-107">本文說明如何設定 Azure AD Domain Services 受管理網域，以部署「SharePoint Server 使用者設定檔同步處理」服務。</span><span class="sxs-lookup"><span data-stu-id="c53d6-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="c53d6-108">'AAD DC Service Accounts' 群組</span><span class="sxs-lookup"><span data-stu-id="c53d6-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="c53d6-109">受管理網域上的 'Users' 組織單位內有一個名為 '**AAD DC Service Accounts**' 的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="c53d6-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="c53d6-110">您可以在 [Active Directory 使用者和電腦] MMC 嵌入式管理單元中的受管理網域上，看到這個群組。</span><span class="sxs-lookup"><span data-stu-id="c53d6-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![AAD DC Service Accounts 安全性群組](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="c53d6-112">下列權限會委派給此安全性群組的成員：</span><span class="sxs-lookup"><span data-stu-id="c53d6-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="c53d6-113">受管理網域之根 DSE 上的「複寫目錄變更」權限。</span><span class="sxs-lookup"><span data-stu-id="c53d6-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="c53d6-114">受管理網域之組態命名內容 (cn=組態容器) 上的「複寫目錄變更」權限。</span><span class="sxs-lookup"><span data-stu-id="c53d6-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="c53d6-115">此安全性群組也是內建群組 **Pre-Windows 2000 Compatible Access** 的成員。</span><span class="sxs-lookup"><span data-stu-id="c53d6-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![AAD DC Service Accounts 安全性群組](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="c53d6-117">可讓您的受管理網域支援 SharePoint Server 使用者設定檔同步處理</span><span class="sxs-lookup"><span data-stu-id="c53d6-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="c53d6-118">您可以將用於 SharePoint 使用者設定檔同步處理的服務帳戶新增到 **AAD DC Service Accounts** 群組。</span><span class="sxs-lookup"><span data-stu-id="c53d6-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="c53d6-119">如此一來，同步處理帳戶就會獲得可將變更複寫到目錄的適當權限。</span><span class="sxs-lookup"><span data-stu-id="c53d6-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="c53d6-120">此組態步驟可讓 SharePoint Server 使用者設定檔同步處理正確運作。</span><span class="sxs-lookup"><span data-stu-id="c53d6-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![AAD DC Service Accounts - 新增成員](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC Service Accounts - 新增成員](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="c53d6-123">相關內容</span><span class="sxs-lookup"><span data-stu-id="c53d6-123">Related Content</span></span>
* [<span data-ttu-id="c53d6-124">技術參考 - 授與 Active Directory Domain Services 權限以供 SharePoint Server 2013 中的設定檔同步處理使用</span><span class="sxs-lookup"><span data-stu-id="c53d6-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
