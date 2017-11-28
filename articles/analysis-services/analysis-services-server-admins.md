---
title: "Azure Analysis Services 的伺服器管理員 aaaManage |Microsoft 文件"
description: "深入了解如何在 Azure 中的 Analysis Services 伺服器的 toomanage 伺服器管理員。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="d9fa3-103">管理伺服器管理員</span><span class="sxs-lookup"><span data-stu-id="d9fa3-103">Manage server administrators</span></span>
<span data-ttu-id="d9fa3-104">Hello 租用戶中的 hello 伺服器所在的伺服器系統管理員必須是有效的使用者或群組 hello Azure Active Directory (Azure AD) 中。</span><span class="sxs-lookup"><span data-stu-id="d9fa3-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="d9fa3-105">您可以使用**Analysis Services 系統管理員**在 Azure 入口網站中的伺服器或伺服器屬性，在 [伺服器管理員] SSMS toomanage hello 控制項刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="d9fa3-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="d9fa3-106">tooadd server 系統管理員使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d9fa3-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="d9fa3-107">在 hello 控制項刀鋒視窗中為您的伺服器，按一下  **Analysis Services 系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="d9fa3-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="d9fa3-108">在 hello **\<伺服器名稱 >-Analysis Services 系統管理員**刀鋒視窗中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="d9fa3-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="d9fa3-109">在 hello**新增伺服器管理員**刀鋒視窗中，選取從您的 Azure AD 的使用者帳戶，或外部使用者邀請電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="d9fa3-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Azure 入口網站的伺服器管理員](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="d9fa3-111">使用 SSMS tooadd server 系統管理員</span><span class="sxs-lookup"><span data-stu-id="d9fa3-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="d9fa3-112">以滑鼠右鍵按一下 hello 伺服器 >**屬性**。</span><span class="sxs-lookup"><span data-stu-id="d9fa3-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="d9fa3-113">在 [Analysis Server 屬性] 中，按一下 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="d9fa3-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="d9fa3-114">按一下**新增**，然後輸入 hello 電子郵件地址的使用者或群組您的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="d9fa3-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![在 SSMS 中新增伺服器管理員](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="d9fa3-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9fa3-116">Next steps</span></span> 
[<span data-ttu-id="d9fa3-117">驗證和使用者權限</span><span class="sxs-lookup"><span data-stu-id="d9fa3-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="d9fa3-118">管理資料庫角色和使用者</span><span class="sxs-lookup"><span data-stu-id="d9fa3-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="d9fa3-119">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="d9fa3-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

