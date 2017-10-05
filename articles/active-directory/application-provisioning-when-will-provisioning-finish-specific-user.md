---
title: "查明特定使用者何時將能存取應用程式 | Microsoft Docs"
description: "如何查明非常重要的使用者何時能夠存取您已設定的應用程式，以透過 Azure AD 進行使用者佈建"
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
ms.openlocfilehash: fcefb31904cfb77022db0358e9feee6a0479db81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a><span data-ttu-id="60175-103">查明特定使用者何時將能存取應用程式</span><span class="sxs-lookup"><span data-stu-id="60175-103">Find out when a specific user will be able to access an application</span></span>
<span data-ttu-id="60175-104">透過應用程式使用自動使用者佈建時，Azure AD 會根據像是[使用者和群組指派](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)等事項，在定期排定的時間間隔內 (通常是每隔 10 分鐘)，自動佈建並更新應用程式中的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="60175-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="60175-105">需要多久的時間？</span><span class="sxs-lookup"><span data-stu-id="60175-105">How long does it take?</span></span>

<span data-ttu-id="60175-106">針對要佈建的特定使用者所花費的時間，主要是根據初始的「完整」同步處理是否已經發生而定。</span><span class="sxs-lookup"><span data-stu-id="60175-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="60175-107">根據 Azure AD 目錄大小和佈建範圍中的使用者數目而定，Azure AD 和應用程式之間的第一次同步處理可能會花費 20 分鐘到數小時。</span><span class="sxs-lookup"><span data-stu-id="60175-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="60175-108">初始同步處理之後的後續同步處理會更快 (例如，在 10 分鐘內)，因為佈建服務會儲存浮水印，代表兩個系統在初始同步處理之後的狀態，所以會改善後續同步處理的效能。</span><span class="sxs-lookup"><span data-stu-id="60175-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-check-the-status-of-a-user"></a><span data-ttu-id="60175-109">如何檢查使用者的狀態</span><span class="sxs-lookup"><span data-stu-id="60175-109">How to check the status of a user</span></span>

<span data-ttu-id="60175-110">若要查看所選使用者的佈建狀態，請參閱 Azure AD 中的稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="60175-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span></span>

<span data-ttu-id="60175-111">您可以在 Azure 入口網站的 [Azure Active Directory]&gt;[企業應用程式]&gt;[\[應用程式名稱\]]&gt;[稽核記錄] 索引標籤中存取佈建稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="60175-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab.</span></span> <span data-ttu-id="60175-112">基於 [帳戶佈建] 類別來篩選記錄，只顯示該應用程式的佈建事件。</span><span class="sxs-lookup"><span data-stu-id="60175-112">Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span></span> <span data-ttu-id="60175-113">您可以根據「比對識別碼」來搜尋使用者，此識別碼是在屬性對應中針對使用者所設定。</span><span class="sxs-lookup"><span data-stu-id="60175-113">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span></span> 

<span data-ttu-id="60175-114">例如，如果您設定了「使用者主體名稱」或「電子郵件地址」做為 Azure AD 端的比對屬性，而且未佈建的使用者具有 "audrey@contoso.com" 的值，接著搜尋 “audrey@contoso.com” 的稽核記錄，然後檢閱傳回的項目。</span><span class="sxs-lookup"><span data-stu-id="60175-114">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="60175-115">佈建的稽核記錄會記錄佈建服務所執行的所有作業，包括：</span><span class="sxs-lookup"><span data-stu-id="60175-115">The provisioning audit logs record all the operations performed by the provisioning service, including:</span></span>

* <span data-ttu-id="60175-116">查詢位於佈建範圍內之已指派使用者的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="60175-116">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="60175-117">查詢目標應用程式以確定那些使用者是否存在</span><span class="sxs-lookup"><span data-stu-id="60175-117">Querying the target app for the existence of those users</span></span>
* <span data-ttu-id="60175-118">比較系統之間的使用者物件</span><span class="sxs-lookup"><span data-stu-id="60175-118">Comparing the user objects between the system</span></span>
* <span data-ttu-id="60175-119">根據比較，在目標系統中新增、更新或停用使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="60175-119">Adding, updating, or disabling the user account in the target system based on the comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="60175-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60175-120">Next steps</span></span>
<span data-ttu-id="60175-121">[自動化使用 Azure Active Directory 對於 SaaS 應用程式的使用者佈建和解除佈建](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)</span><span class="sxs-lookup"><span data-stu-id="60175-121">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
