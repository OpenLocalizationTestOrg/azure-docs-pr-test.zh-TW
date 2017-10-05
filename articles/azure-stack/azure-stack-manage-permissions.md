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
# <a name="manage-role-based-access-control"></a>管理角色型存取控制
Azure Stack 中的使用者可以是訂用帳戶、資源群組或服務中每個執行個體的讀者、擁有者或參與者。 例如，使用者 A 對於訂用帳戶 1 可能擁有讀者權限，但對於虛擬機器 7 則具備擁有者權限。

* 讀者：使用者可以檢視所有項目，但無法進行任何變更。
* 參與者：使用者可以管理除了存取以外的所有項目
* 擁有者：使用者可以管理所有項目，包括存取資源。

## <a name="set-access-permissions-for-a-user"></a>設定使用者的存取權限
1. 使用具備擁有者權限的帳戶登入您想要管理的資源。
2. 在 [資源] 刀鋒視窗中，按一下 [存取] 圖示 ![](media/azure-stack-manage-permissions/image1.png)。
3. 在 [使用者] 刀鋒視窗中，按一下 [角色]。
4. 在 [角色] 刀鋒視窗中，按一下 [新增] 即可加入使用者的權限。

## <a name="next-steps"></a>後續步驟
[新增 Azure Stack 租用戶](azure-stack-add-new-user-aad.md)

