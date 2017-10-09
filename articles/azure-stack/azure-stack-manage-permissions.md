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
# <a name="manage-role-based-access-control"></a>管理角色型存取控制
Azure Stack 中的使用者可以是訂用帳戶、資源群組或服務中每個執行個體的讀者、擁有者或參與者。 例如，使用者 A 也許可以讀取器權限 tooSubscription 1，但卻有擁有者權限 tooVirtual 機器 7。

* 讀者：使用者可以檢視所有項目，但無法進行任何變更。
* 參與者： 使用者可以管理存取 tooresources 以外的所有內容。
* 擁有者： 使用者可以管理任何項目，包括存取 tooresources。

## <a name="set-access-permissions-for-a-user"></a>設定使用者的存取權限
1. 使用具有您想 toomanage 的擁有者權限 toohello 資源的帳戶登入。
2. 在 hello hello 資源刀鋒視窗中按一下 hello**存取**圖示![](media/azure-stack-manage-permissions/image1.png)。
3. 在 hello**使用者**刀鋒視窗中，按一下 **角色**。
4. 在 hello**角色**刀鋒視窗中，按一下 **新增**tooadd hello 使用者的權限。

## <a name="next-steps"></a>後續步驟
[新增 Azure Stack 租用戶](azure-stack-add-new-user-aad.md)

