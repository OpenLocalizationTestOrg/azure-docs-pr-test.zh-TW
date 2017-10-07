---
title: "報告 aaaAccess-Azure rbac 進行 |Microsoft 文件"
description: "產生報告，列出所有變更中存取 tooyour hello 的角色型存取控制與 Azure 訂用帳戶過去 90 天內。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>建立角色型存取控制的存取報告
有人會授與或撤銷存取權，您的訂閱，在任何時間 hello 變更會記錄在 Azure 的事件。 您可以建立存取變更歷程記錄報表 toosee 所有變更的 hello 過去 90 天內。

## <a name="create-a-report-with-azure-powershell"></a>使用 Azure PowerShell 建立報告
toocreate 存取變更歷程記錄報表，在 PowerShell 中，使用 hello [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog)命令。

當您呼叫此命令時，您可以指定您想要列出，包括 hello 下列 hello 分派的哪一個屬性：

| 屬性 | 說明 |
| --- | --- |
| **Action** |已授與或已撤銷存取權 |
| **Caller** |負責 hello 存取 hello 擁有者變更 |
| **PrincipalId** | hello hello 使用者、 群組或指派 hello 角色的應用程式的唯一識別碼 |
| **PrincipalName** |hello 名稱的 hello 使用者、 群組或應用程式 |
| **PrincipalType** |Hello 分派是否針對使用者、 群組或應用程式 |
| **RoleDefinitionId** |hello hello 角色所授與或撤銷的 GUID |
| **RoleName** |已授與或撤銷 hello 角色 |
| **範圍** | hello hello 訂用帳戶、 資源群組或 hello 分派的資源的唯一識別項太適用於| 
| **ScopeName** |hello hello 訂用帳戶、 資源群組或資源的名稱 |
| **ScopeType** |Hello 分派是否在 hello 訂用帳戶、 資源群組或資源範圍 |
| **Timestamp** |hello 日期和時間的存取權已變更 |

此範例命令會列出過去七天內 hello 訂用帳戶中的所有存取變更：

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - 螢幕擷取畫面](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>使用 Azure CLI 建立報告
toocreate hello Azure 命令列介面 (CLI)，以存取變更歷程記錄報表使用 hello`azure role assignment changelog list`命令。

## <a name="export-tooa-spreadsheet"></a>匯出 tooa 試算表
toosave hello 報表，或操作 hello 資料、 匯出 hello 存取變成.csv 檔案。 然後，您就可以檢視試算表中檢視 hello 報表。

![以試算表形式來檢視的變更記錄 - 螢幕擷取畫面](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>後續步驟
* 使用 [Azure RBAC 中的自訂角色](role-based-access-control-custom-roles.md)
* 深入了解如何 toomanage [Azure rbac 進行使用 powershell](role-based-access-control-manage-access-powershell.md)

