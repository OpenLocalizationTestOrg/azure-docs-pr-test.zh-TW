---
title: "Azure Active Directory Domain Services：啟用對 SharePoint User Profile Service 的支援 | Microsoft Docs"
description: "設定 Azure Active Directory 網域服務受管理的網域 toosupport 設定檔同步處理 SharePoint 伺服器"
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
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="0133c-103">設定 SharePoint 伺服器的受管理的網域 toosupport 設定檔同步處理</span><span class="sxs-lookup"><span data-stu-id="0133c-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="0133c-104">SharePoint Server 包含用來同步處理使用者設定檔的 User Profile Service。</span><span class="sxs-lookup"><span data-stu-id="0133c-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="0133c-105">註冊使用者設定檔服務的 hello tooset，適當的權限需要 toobe 授與 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="0133c-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="0133c-106">如需詳細資訊，請參閱[授與 Active Directory Domain Services 權限以供 SharePoint Server 2013 中的設定檔同步處理使用](https://technet.microsoft.com/library/hh296982.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0133c-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="0133c-107">本文說明如何設定 Azure AD 網域服務受管理的網域 toodeploy hello SharePoint 伺服器使用者設定檔同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="0133c-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="0133c-108">hello ' AAD DC Service Accounts' 群組</span><span class="sxs-lookup"><span data-stu-id="0133c-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="0133c-109">安全性群組呼叫 '**AAD DC 的服務帳戶**' hello '的使用者 」 組織單位上受管理的網域內可供使用。</span><span class="sxs-lookup"><span data-stu-id="0133c-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="0133c-110">您可以看到這個群組中 hello **Active Directory 使用者和電腦**MMC 嵌入式管理單元在受管理的網域上。</span><span class="sxs-lookup"><span data-stu-id="0133c-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![AAD DC Service Accounts 安全性群組](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="0133c-112">此安全性群組的成員會委派下列權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="0133c-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="0133c-113">hello 根目錄 DSE 的 hello 上 hello 複寫目錄變更權限管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0133c-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="0133c-114">hello hello 設定命名內容上的複寫目錄變更權限 (cn = configuration 容器) 的 hello 受管理網域。</span><span class="sxs-lookup"><span data-stu-id="0133c-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="0133c-115">此安全性群組也是 hello 內建群組成員**Pre-Windows 2000 Compatible Access**。</span><span class="sxs-lookup"><span data-stu-id="0133c-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![AAD DC Service Accounts 安全性群組](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="0133c-117">啟用您的受管理的網域 toosupport SharePoint 伺服器使用者設定檔同步處理</span><span class="sxs-lookup"><span data-stu-id="0133c-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="0133c-118">您可以新增 hello 服務帳戶使用的 SharePoint 使用者設定檔同步處理 toohello **AAD DC 的服務帳戶**群組。</span><span class="sxs-lookup"><span data-stu-id="0133c-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="0133c-119">如此一來，hello 同步處理帳戶取得足夠的權限 tooreplicate 變更 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="0133c-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="0133c-120">此組態步驟可讓 SharePoint 伺服器的使用者設定檔同步 toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="0133c-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![AAD DC Service Accounts - 新增成員](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC Service Accounts - 新增成員](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="0133c-123">相關內容</span><span class="sxs-lookup"><span data-stu-id="0133c-123">Related Content</span></span>
* [<span data-ttu-id="0133c-124">技術參考 - 授與 Active Directory Domain Services 權限以供 SharePoint Server 2013 中的設定檔同步處理使用</span><span class="sxs-lookup"><span data-stu-id="0133c-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
