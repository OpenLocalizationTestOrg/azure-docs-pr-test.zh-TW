---
title: "當特定的使用者將能夠 tooaccess 應用程式外 aaaFind |Microsoft 文件"
description: "Toofind 出非常重要的使用者是無法 tooaccess 應用程式的當您設定的方式進行使用者佈建與 Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a><span data-ttu-id="e6121-103">找出特定的使用者將能夠 tooaccess 應用程式</span><span class="sxs-lookup"><span data-stu-id="e6121-103">Find out when a specific user will be able tooaccess an application</span></span>
<span data-ttu-id="e6121-104">透過應用程式使用自動使用者佈建時，Azure AD 會根據像是[使用者和群組指派](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)等事項，在定期排定的時間間隔內 (通常是每隔 10 分鐘)，自動佈建並更新應用程式中的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e6121-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="e6121-105">需要多久的時間？</span><span class="sxs-lookup"><span data-stu-id="e6121-105">How long does it take?</span></span>

<span data-ttu-id="e6121-106">指定的使用者 toobe 佈建所需的 hello 時間主要取決於已經發生初始的 「 完整 」 同步處理。</span><span class="sxs-lookup"><span data-stu-id="e6121-106">hello time it takes for a given user toobe provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="e6121-107">hello Azure AD 之間的第一個同步處理和應用程式可能需要 20 分鐘 tooseveral 小時，視 hello 大小 hello Azure AD 目錄與 hello 佈建的範圍中的使用者數目而定。</span><span class="sxs-lookup"><span data-stu-id="e6121-107">hello first sync between Azure AD and an app can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="e6121-108">Hello 初始同步處理之後的後續同步處理會比較快 （例如 10 分鐘內），因為佈建服務的 hello 儲存代表 hello 狀態，這兩個系統的 hello 初始同步處理之後，可改善效能的後續的同步處理的浮水印。</span><span class="sxs-lookup"><span data-stu-id="e6121-108">Subsequent syncs after hello initial sync be faster (e.g. within 10 minutes), as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-toocheck-hello-status-of-a-user"></a><span data-ttu-id="e6121-109">如何 toocheck hello 使用者的狀態</span><span class="sxs-lookup"><span data-stu-id="e6121-109">How toocheck hello status of a user</span></span>

<span data-ttu-id="e6121-110">toosee hello 佈建狀態為選取的使用者，請參閱稽核記錄，在 Azure AD 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e6121-110">toosee hello provisioning status for a selected user, consult hello Audit logs in Azure AD.</span></span>

<span data-ttu-id="e6121-111">佈建稽核記錄檔的 hello 可於 hello Azure 入口網站中 hello **Azure Active Directory&gt;企業應用程式&gt;\[應用程式名稱\]&gt;稽核記錄**] 索引標籤。篩選 hello 登入 hello**帳戶佈建**tooonly 類別目錄，請參閱 「 hello 佈建該應用程式的事件。</span><span class="sxs-lookup"><span data-stu-id="e6121-111">hello provisioning audit logs can be accessed in hello Azure portal, in hello **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter hello logs on hello **Account Provisioning** category tooonly see hello provisioning events for that app.</span></span> <span data-ttu-id="e6121-112">您可以根據 hello 「 比對識別碼 」 hello 屬性對應中為其設定為使用者進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="e6121-112">You can search for users based on hello “matching ID” that was configured for them in hello attribute mappings.</span></span> 

<span data-ttu-id="e6121-113">比方說，如果您設定 hello 「 使用者主體名稱 」 或 「 電子郵件地址 」 為 hello 比對一邊 hello Azure AD 的屬性和 hello 使用者未提供的值為"audrey@contoso.com"，然後搜尋 hello 稽核記錄檔中的"audrey@contoso.com」，然後檢閱傳回項目。</span><span class="sxs-lookup"><span data-stu-id="e6121-113">For example, if you configured hello “user principal name” or “email address” as hello matching attribute on hello Azure AD side, and hello user not being provisioning has a value of “audrey@contoso.com”, then search hello audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="e6121-114">hello 佈建稽核記錄檔的記錄所有 hello hello 佈建服務所執行的作業包括：</span><span class="sxs-lookup"><span data-stu-id="e6121-114">hello provisioning audit logs record all hello operations performed by hello provisioning service, including:</span></span>

* <span data-ttu-id="e6121-115">查詢位於佈建範圍內之已指派使用者的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6121-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="e6121-116">查詢 hello 目標應用程式，這些使用者的 hello 存在</span><span class="sxs-lookup"><span data-stu-id="e6121-116">Querying hello target app for hello existence of those users</span></span>
* <span data-ttu-id="e6121-117">比較 hello hello 系統之間的使用者物件</span><span class="sxs-lookup"><span data-stu-id="e6121-117">Comparing hello user objects between hello system</span></span>
* <span data-ttu-id="e6121-118">加入、 更新或停用根據 hello 比較 hello 目標系統中的 hello 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="e6121-118">Adding, updating, or disabling hello user account in hello target system based on hello comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6121-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6121-119">Next steps</span></span>
<span data-ttu-id="e6121-120">[自動化使用者佈建和取消佈建 tooSaaS 應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)'</span><span class="sxs-lookup"><span data-stu-id="e6121-120">[Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
