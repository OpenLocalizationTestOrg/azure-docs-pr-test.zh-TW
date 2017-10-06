---
title: "aaaManage 存取和使用 RBAC-Azure rbac 進行的權限 |Microsoft 文件"
description: "快速入門中存取管理 hello Azure 入口網站中的 Azure 角色型存取控制。 使用您的目錄中的角色指派 tooassign 權限。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>開始使用 hello Azure 入口網站中的 角色型存取控制
安全性導向公司應該專注於讓員工 hello 所需的確切權限。 太多權限可以公開帳戶 tooattackers。 權限太少則會讓員工無法有效率地完成工作。 Azure「角色型存取控制」(RBAC) 可以為 Azure 提供更細緻的存取管理來協助解決這個問題。

使用 RBAC 時，您可以隔離您的小組內的責任，並授與存取 toousers 只 hello 量他們需要 tooperform 他們的工作。 您可以不授與每個人 Azure 訂用帳戶或資源中無限制的權限，而是只允許執行特定的動作。 例如，使用 RBAC toolet 一位員工管理訂用帳戶中的虛擬機器，而另一個可以管理 SQL 資料庫內 hello 相同訂用帳戶。

## <a name="basics-of-access-management-in-azure"></a>Azure 存取權管理的基礎
每個 Azure 訂用帳戶都會與一個 Azure Active Directory (AD) 目錄相關聯。 使用者、 群組和從該目錄的應用程式可以管理 hello Azure 訂用帳戶中的資源。 指派這些使用 hello Azure 入口網站、 Azure 命令列工具，以及 Azure 管理 Api 的存取權限。

藉由指派 hello 適當 RBAC 角色 toousers、 群組和應用程式在特定範圍授與存取權。 訂用帳戶、 資源群組或單一資源，可以是 hello 範圍的角色指派。 在父範圍中指派的角色也會授與存取內含 toohello 子系。 例如，具有存取 tooa 資源群組的使用者可以管理其中的內容，例如網站、 虛擬機器，以及子網路的所有 hello 資源。

![Azure Active Directory 元素之間的關聯性 - 圖表](./media/role-based-access-control-what-is/rbac_aad.png)

hello RBAC 角色指派會規定哪些資源 hello 使用者、 群組或應用程式可以管理該範圍內。

## <a name="built-in-roles"></a>內建角色
Azure RBAC 具有三個套用 tooall 資源類型的基本角色：

* **擁有者**具有完整存取 tooall 資源，包括 hello 右 toodelegate 存取 tooothers。
* **參與者**可以建立及管理 Azure 資源的所有類型，但無法授與存取 tooothers。
* **讀者** 可以檢視現有的 Azure 資源。

hello RBAC 角色在 Azure 中的 hello rest 允許特定的 Azure 資源管理。 例如，hello 虛擬機器參與者角色可讓 hello 使用者 toocreate 及管理虛擬機器。 它沒有提供這些存取 toohello 虛擬網路或 hello hello 虛擬機器的子網路連線到。 

[RBAC 內建角色](role-based-access-built-in-roles.md)清單 hello Azure 中可用的角色。 它會指定 hello 作業和每個內建的角色會授與 toousers 的範圍。 如果您要尋找 toodefine 您自己的角色的更多控制，請參閱如何 toobuild [Azure rbac 進行中的自訂角色](role-based-access-control-custom-roles.md)。

## <a name="resource-hierarchy-and-access-inheritance"></a>資源階層和存取繼承
* 每個**訂用帳戶**所屬 Azure tooonly 一個目錄。 (但每個目錄可以有多個訂用帳戶)。
* 每個**資源群組**所屬 tooonly 一個訂用帳戶。
* 每個**資源**所屬 tooonly 一個資源群組。

您在父範圍授與的存取權會在子範圍繼承。 例如：

* 您指派 hello 讀取器角色 tooan Azure AD 群組在 hello 訂用帳戶範圍。 hello 該群組的成員可以檢視每個資源群組和資源 hello 訂用帳戶中。
* 您指派 hello 參與者角色 tooan 應用程式在 hello 資源群組範圍。 它可以管理該資源群組，但沒有其他 hello 訂用帳戶中的資源群組中的所有類型的資源。

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>Azure RBAC 與傳統訂用帳戶系統管理員
傳統的訂用帳戶管理員和共同管理員具有完整存取 toohello Azure 訂用帳戶。 他們可以管理資源使用 hello [Azure 入口網站](https://portal.azure.com)與 Azure 資源管理員 Api 或 hello [Azure 傳統入口網站](https://manage.windowsazure.com)和 Azure 傳統部署模型。 在 hello RBAC 模型中，傳統的系統管理員會指派 hello 擁有者角色在 hello 訂用帳戶範圍。

只有 hello Azure 入口網站和 hello 新的 Azure 資源管理員 Api 支援 Azure rbac 進行。 使用者和指派 RBAC 角色的應用程式無法使用 hello 傳統管理入口網站和 hello Azure 傳統部署模型。

## <a name="authorization-for-management-vs-data-operations"></a>管理與資料作業的授權
Azure RBAC 僅支援管理操作的 hello Azure 中的資源 hello Azure 入口網站和 Azure 資源管理員 Api。 它無法授權 Azure 資源的所有資料層級作業。 例如，您可以授權其他人 toomanage 儲存體帳戶，但不是 toohello blob 或資料表儲存體帳戶內。 同樣地，SQL database 的管理、 但不是 hello 資料表內。

## <a name="next-steps"></a>後續步驟
* 開始使用[hello Azure 入口網站中的 角色型存取控制](role-based-access-control-configure.md)。
* 請參閱 hello [RBAC 內建的角色](role-based-access-built-in-roles.md)
* 定義您自己的 [Azure RBAC 中的自訂角色](role-based-access-control-custom-roles.md)
