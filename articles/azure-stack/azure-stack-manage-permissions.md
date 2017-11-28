---
title: "在 Azure Stack 中針對每位使用者管理資源的權限 (服務系統管理員與租用戶) | Microsoft Docs"
description: "您身為服務系統管理員或租用戶，應了解如何管理 RBAC 權限。"
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
ms.openlocfilehash: 95bdc83351acdec352620feaea3b1e50c0dabad4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-role-based-access-control"></a><span data-ttu-id="a61af-103">管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="a61af-103">Manage Role-Based Access Control</span></span>
<span data-ttu-id="a61af-104">Azure Stack 中的使用者可以是訂用帳戶、資源群組或服務中每個執行個體的讀者、擁有者或參與者。</span><span class="sxs-lookup"><span data-stu-id="a61af-104">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span></span> <span data-ttu-id="a61af-105">例如，使用者 A 對於訂用帳戶 1 可能擁有讀者權限，但對於虛擬機器 7 則具備擁有者權限。</span><span class="sxs-lookup"><span data-stu-id="a61af-105">For example, User A might have reader permissions to Subscription 1, but have owner permissions to Virtual Machine 7.</span></span>

* <span data-ttu-id="a61af-106">讀者：使用者可以檢視所有項目，但無法進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="a61af-106">Reader: User can view everything, but can’t make any changes.</span></span>
* <span data-ttu-id="a61af-107">參與者：使用者可以管理除了存取以外的所有項目</span><span class="sxs-lookup"><span data-stu-id="a61af-107">Contributor: User can manage everything except access to resources.</span></span>
* <span data-ttu-id="a61af-108">擁有者：使用者可以管理所有項目，包括存取資源。</span><span class="sxs-lookup"><span data-stu-id="a61af-108">Owner: User can manage everything, including access to resources.</span></span>

## <a name="set-access-permissions-for-a-user"></a><span data-ttu-id="a61af-109">設定使用者的存取權限</span><span class="sxs-lookup"><span data-stu-id="a61af-109">Set access permissions for a user</span></span>
1. <span data-ttu-id="a61af-110">使用具備擁有者權限的帳戶登入您想要管理的資源。</span><span class="sxs-lookup"><span data-stu-id="a61af-110">Sign in with an account that has owner permissions to the resource you want to manage.</span></span>
2. <span data-ttu-id="a61af-111">在 [資源] 刀鋒視窗中，按一下 [存取] 圖示 ![](media/azure-stack-manage-permissions/image1.png)。</span><span class="sxs-lookup"><span data-stu-id="a61af-111">In the blade for the resource, click the **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span></span>
3. <span data-ttu-id="a61af-112">在 [使用者] 刀鋒視窗中，按一下 [角色]。</span><span class="sxs-lookup"><span data-stu-id="a61af-112">In the **Users** blade, click **Roles**.</span></span>
4. <span data-ttu-id="a61af-113">在 [角色] 刀鋒視窗中，按一下 [新增] 即可加入使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="a61af-113">In the **Roles** blade, click **Add** to add permissions for the user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a61af-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a61af-114">Next steps</span></span>
[<span data-ttu-id="a61af-115">新增 Azure Stack 租用戶</span><span class="sxs-lookup"><span data-stu-id="a61af-115">Add an Azure Stack tenant</span></span>](azure-stack-add-new-user-aad.md)

