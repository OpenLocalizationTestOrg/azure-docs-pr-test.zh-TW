---
title: "aaaAzure 角色型存取控制 (RBAC) toocontrol 存取權限 toocreate 及管理支援要求 |Microsoft 文件"
description: "Azure 角色型存取控制 (RBAC) toocontrol 存取權限 toocreate 及管理支援要求"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a>Azure 角色型存取控制 (RBAC) toocontrol 存取權限 toocreate 及管理支援要求

[角色型存取控制 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) 提供適用於 Azure 的詳細存取權管理。
支援 hello Azure 入口網站中的要求建立[portal.azure.com](https://portal.azure.com)，使用 Azure RBAC 模型 toodefine 可以建立和管理的支援要求。
指派適當 RBAC 角色 toousers hello、 群組和應用程式在特定範圍，它可以是訂用帳戶、 資源群組或資源授與的存取。

讓我們來看一個範例： 為具有 hello 訂用帳戶範圍的讀取權限的資源群組擁有者，您可以管理在 hello 資源群組下，例如網站、 虛擬機器，以及子網路的所有 hello 資源。
不過，當您嘗試 toocreate 針對 hello 虛擬機器資源的支援要求時，您遇到下列錯誤 hello

![訂用帳戶錯誤](./media/create-manage-support-requests-using-access-control/subscription-error.png)

在支援要求的管理，您需要寫入權限，或具有 hello 的角色，可支援在 hello 訂用帳戶範圍 toobe 無法 toocreate 動作 Microsoft.Support/* 及管理支援要求。

hello 下列文章說明如何使用 Azure 的自訂角色型存取控制 (RBAC) toocreate，及管理在 hello Azure 入口網站的支援要求。

## <a name="getting-started"></a>開始使用

使用 hello 上述範例中，您將無法 toocreate 支援要求您為資源如果您已由 hello 訂用帳戶擁有者指派自訂 RBAC 角色 hello 訂用帳戶。
[自訂 RBAC 角色](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/)可以使用 Azure PowerShell、 Azure 命令列介面 (CLI) 和 hello REST API 來建立。

hello 動作屬性的自訂安全性角色指定 hello Azure 操作 toowhich hello 角色會授與的存取。
toocreate 支援要求管理自訂的角色，hello 角色必須擁有 hello 動作 Microsoft.Support/*

以下是範例，您可以使用 toocreate 和管理自訂安全性角色的支援要求。
我們已經名為 「 支援要求著作人 」 這個角色，且我們 toohello 本文章中的自訂角色的方式。

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

中所述步驟 hello[這段影片](https://www.youtube.com/watch?v=-PaBaDmfwKI)toolearn 如何 toocreate 訂用帳戶自訂安全性角色。

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a>建立及管理在 hello Azure 入口網站的支援要求

讓我們來看一個範例-您是 hello 擁有者的訂用帳戶 「 Visual Studio MSDN 訂閱。 」
Joe 是您對等的此訂用帳戶中的 hello 資源群組資源擁有者 toosome 並具有讀取權限 toohello 訂用帳戶。
您想 toogive 存取 tooyour 等 Joe，hello 能力 toocreate 和管理此訂用帳戶下的 hello 資源的支援票證。

1. hello 第一個步驟是 toogo toohello 訂用帳戶，並在 [設定] 下會看見使用者清單。 按一下 hello 使用者 Joe 上 hello 訂用帳戶擁有讀取器存取權限，讓我們來指派新的自訂角色 toohim。

    ![新增角色](./media/create-manage-support-requests-using-access-control/add-role.png)

2. 按一下 [新增] 底下 hello 「 使用者 」 刀鋒視窗。 從 hello 角色清單中選取 hello 自訂角色 「 支援要求著作人 」

    ![新增支援參與者角色](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. 選取之後 hello 角色名稱，請按一下 [加入使用者] 並輸入 hello Joe 的電子郵件憑證。 按一下 [選取]

    ![新增使用者](./media/create-manage-support-requests-using-access-control/add-users.png)

4. 按一下 「 確定 」 tooproceed

    ![新增存取](./media/create-manage-support-requests-using-access-control/add-access.png)

5. 現在您會看見 hello 與 hello 新增自訂角色 「 支援要求著作人 」 hello 的 hello 擁有者的訂用帳戶底下的使用者

    ![新增的使用者](./media/create-manage-support-requests-using-access-control/user-added.png)

    Joe 登入時 hello 入口網站，他會看見 hello 訂用帳戶 toowhich 他已加入。

7. Joe 從 hello 「 說明及支援 」 刀鋒視窗中按一下 「 新的支援要求 」，而且可以建立支援要求的"Visual Studio Ultimate 與 MSDN"

    ![新增支援要求](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. 按一下 「 所有支援的要求 」 Joe 可以檢視針對此訂用帳戶建立支援要求 hello 清單![案例詳細資料檢視](./media/create-manage-support-requests-using-access-control/case-details-view.png)

## <a name="remove-support-request-access-in-hello-azure-portal"></a>移除 hello Azure 入口網站支援要求的存取權

就如同它是可能 toogrant 存取 tooa 使用者 toocreate 及管理支援要求時，它會使用 hello 使用者也可能 tooremove 存取。
tooremove hello 能力 toocreate 和管理的支援要求，請 toohello 訂用帳戶中，按一下 [設定]，按一下 hello 使用者 （在此情況下，是 Joe）。
以滑鼠右鍵按一下 「 支援要求著作人 」 hello 角色名稱，然後按一下 [移除]

![移除支援要求存取權](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

當 Joe 登入 toohello 入口網站，並嘗試 toocreate 支援要求時，他會遇到下列錯誤 hello

![訂用帳戶錯誤-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

當 Joe 按一下 [所有支援要求] 時，他不會看到任何支援要求

![案例詳細資料檢視-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
