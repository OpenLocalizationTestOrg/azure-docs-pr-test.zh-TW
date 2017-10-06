---
title: "在 Azure API 管理角色型存取控制的 aaaHow tooUse |Microsoft 文件"
description: "了解 toouse hello 內建的角色，並在 Azure API 管理中建立自訂角色"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>TooUse 角色型存取控制的方式在 Azure API 管理
Azure API 管理會依賴的 API 管理服務和實體 （例如，應用程式開發介面，原則） 的所有存取控制 (RBAC) tooenable 精細存取管理。 這篇文章提供您的 hello 內建和自訂角色概觀 API 管理中。 如果您想需 hello Azure 入口網站中存取管理的詳細資訊，請參閱[hello Azure 入口網站中存取管理使用者入門](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>內建角色
API 管理目前提供 3 內建的角色，並將在未來附近 hello 中加入 2 個角色。 這些角色可以指派到不同的範圍，包括訂用帳戶、資源群組，以及個別 API 管理執行個體。 比方說，如果 hello"Azure API 管理服務讀取器 」 角色被指派 tooan hello 資源群組層級的使用者，則 hello 使用者將有 hello 資源群組內的讀取權限 tooall API 管理執行個體。 

hello 下表提供的 hello 的簡短說明內建的角色。 您可以指派這些角色使用 hello Azure 入口網站或其他工具，包括 Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell)，Azure[命令列介面](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli)，和[REST API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest)。 如需詳細資訊，關於如何 tooassign 內建的角色，請參閱[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)。

| 角色          | 讀取權限<sup>[1]</sup> | 寫入權限<sup>[2]</sup> | 服務建立、刪除、調整，VPN 及自訂網域設定 | 存取 toolegacy Publsiher 入口網站 | 說明
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Azure API 管理服務參與者 | ✓ | ✓  | ✓  | ✓ | 進階使用者。 具有完整的 CRUD 存取 tooAPI 管理服務和實體 （例如，應用程式開發介面、 原則）。 具有存取 toohello 舊版發行者入口網站。 |
| Azure API 管理服務讀者 | ✓  | | || 具有唯讀存取 tooAPI 管理服務和實體。 |
| Azure API 管理服務操作員 | ✓ | | ✓ | | 可以管理 API 管理服務，但無法管理實體。|
| Azure API 管理服務編輯者<sup>*</sup> | ✓ | ✓ | |  | 可以管理 API 管理實體，但無法管理服務。|
| Azure API 管理內容管理員<sup>*</sup> | ✓ | | | ✓ | 可以管理開發人員入口網站。 唯讀存取 tooservices 和實體。|

<sup>[1] 的讀取權限 tooAPI 管理服務和實體 （例如，應用程式開發介面，原則）</sup>

<sup>[2] 寫入權限 tooAPI 管理服務和實體，除了下列 opeartions: 1） 執行個體建立、 刪除和調整 2) VPN 組態 3） 自訂網域名稱設定</sup>

<sup>\*hello 服務編輯器角色後才能我們移轉所有 admin UI 中從 hello 現有發行者入口網站 toohello Azure 入口網站。hello 內容管理員角色可 tooonly hello 發行者入口網站，將會重構之後包含功能相關的 toomanaging hello 開發人員入口網站。</sup>  


## <a name="custom-roles"></a>自訂角色
如果 hello 內建角色都不符合您的特定需求，自訂角色可以建立 tooprovide 更精細存取管理 API 管理的實體。 例如，您可以建立自訂安全性角色的唯讀存取 tooan API 管理服務，但僅有寫入權限 tooone 特定 API。 toolearn 更多詳細的自訂角色，請參閱[Azure rbac 進行中的自訂角色](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)。 

當您建立自訂安全性角色時，很容易 toostart 與其中一個 hello 內建角色。 編輯 hello 屬性 tooadd hello 動作、 NotActions 或 AssignableScopes，然後儲存 hello 變更為新的角色。 hello 下列範例會開始與 hello"Azure API 管理服務讀取器 」 角色並建立自訂安全性角色稱為 「 計算機 API 編輯器 」。 只有 tooa 特定 API 因此將只具有存取 toothat API hello 自訂角色指派。 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>觀看影片概觀

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>後續步驟

* 深入了解 Azure 中的角色型存取控制
  * [開始使用 hello Azure 入口網站中存取管理](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Azure RBAC 中的自訂角色](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
