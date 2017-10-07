---
title: "資源原則的 aaaAzure 入口網站 |Microsoft 文件"
description: "描述如何 toouse Azure 入口網站 toocreate 和管理資源管理員原則。 原則可以套用在 hello 訂用帳戶或資源群組。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>使用 Azure 入口網站 tooassign 和管理資源原則
hello Azure 入口網站可讓您 tooassign 資源原則 tooresource 群組和訂閱。 hello 使用者介面可讓您輕鬆 tooselect hello 原則 tooassign，並指定該原則 toocustomize hello 原則設定的參數值。 

tooassign 透過 hello 入口網站的原則，hello 原則定義必須存在於訂用帳戶。 您的訂用帳戶已準備好讓您 tooassign tooresource 群組或訂用帳戶的數個內建的原則定義。 您會看到這些內建的原則和任何使用 hello 入口 tooassign 原則時，您已定義的自訂原則。 簡介 toopolicies 及 toodefine 自訂原則的方式，請參閱[資源原則概觀](resource-manager-policy.md)。

原則會由所有子資源繼承。 因此，如果原則已套用的 tooa 資源群組，則該資源群組中的適用 tooall hello 資源。 在本文中 hello 詞彙**範圍**參考 toohello 資源群組或指派 hello 原則的訂用帳戶。 

建立和更新資源 (PUT 和 PATCH 作業) 時，會評估原則。

## <a name="assign-a-policy"></a>指派原則

1. tooassign 原則 tooeither 資源群組或訂用帳戶，請選取該資源群組或訂用帳戶。 在 hello 設定選取**原則**。

   ![選取原則](./media/resource-manager-policy-portal/select-policies.png)

2. toocreate 原則指派為此範圍中，選取**加入指派**。

   ![新增指派](./media/resource-manager-policy-portal/add-assignment.png)

3. 選取您想要 tooassign hello 原則。 即使您尚未加入任何原則定義 tooyour 訂用帳戶，您會看到 hello 內建原則，可供指派。 這些內建原則涵蓋許多常見的案例。

   ![選取定義](./media/resource-manager-policy-portal/select-definition.png)

4. 選取原則之後, 您會看到 hello 原則的描述，以及該原則的任何參數。 例如，hello 下列影像顯示 hello**允許位置**限制 hello 可用位置的 hello 原則而言是必要的參數。

   ![顯示參數](./media/resource-manager-policy-portal/show-parameters.png)

5. 透過 hello 使用者介面中，選取 hello 值 toospecify hello 原則參數 （例如，用於部署的 hello 位置）。

   ![選取參數值](./media/resource-manager-policy-portal/select-parameters.png)

6. 提供 hello 其他參數值。 根據您選取 hello 原則指派要在啟動時的 hello 刀鋒視窗，自動指派 hello 範圍。 完成時選取 [確定]  。

   ![定義參數](./media/resource-manager-policy-portal/define-parameters.png)

  您已指派 hello 原則 toohello 指定範圍。

## <a name="view-policy-assignments"></a>檢視原則指派

在指派原則之後, 您看到它 hello 針對該領域的原則清單中。 hello**詳細資料**索引標籤會顯示 hello 原則指派的摘要。

![顯示詳細資料](./media/resource-manager-policy-portal/show-details.png)

hello**指派規則**索引標籤會顯示 hello JSON hello 原則定義。

![顯示指派規則](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>變更現有的原則指派

toochange 原則，選取**編輯指派**或**刪除**

![編輯或刪除指派](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>指派自訂的原則

如果您已經在您的訂用帳戶中定義的自訂原則，這些原則是透過 hello 入口網站指派的可用。 這些原則前面會加上 [自訂]

![自訂原則](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>後續步驟
* toolearn 有關 hello JSON 語法定義原則，請參閱[資源原則概觀](resource-manager-policy.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。
* 發行位置 hello 原則結構描述是在[http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)。 

