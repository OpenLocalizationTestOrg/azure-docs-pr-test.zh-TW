---
title: "aaaManage （服務系統管理員和租用戶） 的 Azure 堆疊中每位使用者的權限 tooresources |Microsoft 文件"
description: "身為服務系統管理員或租用戶，了解如何 toomanage RBAC 權限。"
services: azure-stack
documentationcenter: 
author: Heathl17
manager: byronr
editor: 
ms.assetid: cccac19a-e1bf-4e36-8ac8-2228e8487646
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 461feab12a4cb8b9402c6c61b721371c50f60559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control"></a><span data-ttu-id="8b954-103">管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="8b954-103">Manage Role-Based Access Control</span></span>
<span data-ttu-id="8b954-104">Azure Stack 中的使用者可以是訂用帳戶、資源群組或服務中每個執行個體的讀者、擁有者或參與者。</span><span class="sxs-lookup"><span data-stu-id="8b954-104">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span></span> <span data-ttu-id="8b954-105">例如，使用者 A 也許可以讀取器權限 tooSubscription 1，但卻有擁有者權限 tooVirtual 機器 7。</span><span class="sxs-lookup"><span data-stu-id="8b954-105">For example, User A might have reader permissions tooSubscription 1, but have owner permissions tooVirtual Machine 7.</span></span>

* <span data-ttu-id="8b954-106">讀者：使用者可以檢視所有項目，但無法進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="8b954-106">Reader: User can view everything, but can’t make any changes.</span></span>
* <span data-ttu-id="8b954-107">參與者： 使用者可以管理存取 tooresources 以外的所有內容。</span><span class="sxs-lookup"><span data-stu-id="8b954-107">Contributor: User can manage everything except access tooresources.</span></span>
* <span data-ttu-id="8b954-108">擁有者： 使用者可以管理任何項目，包括存取 tooresources。</span><span class="sxs-lookup"><span data-stu-id="8b954-108">Owner: User can manage everything, including access tooresources.</span></span>

## <a name="set-access-permissions-for-a-user"></a><span data-ttu-id="8b954-109">設定使用者的存取權限</span><span class="sxs-lookup"><span data-stu-id="8b954-109">Set access permissions for a user</span></span>
1. <span data-ttu-id="8b954-110">使用具有您想 toomanage 的擁有者權限 toohello 資源的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="8b954-110">Sign in with an account that has owner permissions toohello resource you want toomanage.</span></span>
2. <span data-ttu-id="8b954-111">在 hello hello 資源刀鋒視窗中按一下 hello**存取**圖示![](media/azure-stack-manage-permissions/image1.png)。</span><span class="sxs-lookup"><span data-stu-id="8b954-111">In hello blade for hello resource, click hello **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span></span>
3. <span data-ttu-id="8b954-112">在 hello**使用者**刀鋒視窗中，按一下 **角色**。</span><span class="sxs-lookup"><span data-stu-id="8b954-112">In hello **Users** blade, click **Roles**.</span></span>
4. <span data-ttu-id="8b954-113">在 hello**角色**刀鋒視窗中，按一下 **新增**tooadd hello 使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="8b954-113">In hello **Roles** blade, click **Add** tooadd permissions for hello user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b954-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b954-114">Next steps</span></span>
[<span data-ttu-id="8b954-115">新增 Azure Stack 租用戶</span><span class="sxs-lookup"><span data-stu-id="8b954-115">Add an Azure Stack tenant</span></span>](azure-stack-add-new-user-aad.md)

