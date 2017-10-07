---
title: "aaaScale Azure 雲端服務中 Windows PowerShell |Microsoft 文件"
description: "（傳統）深入了解如何 toouse PowerShell tooscale web 角色或背景工作角色或縮小在 Azure 中。"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a>在 PowerShell 中 tooscale 雲端服務的方式

可以使用 Windows PowerShell tooscale web 角色或背景工作角色或縮小，藉由新增或移除執行個體。  

## <a name="log-in-tooazure"></a>登入 tooAzure

您必須先登入，才能透過 PowerShell 在訂用帳戶上執行任何作業︰

```powershell
Add-AzureAccount
```

如果您有多個與您的帳戶相關聯的訂用帳戶，您可能需要 toochange hello 目前訂用帳戶根據您的雲端服務所在的位置。 toocheck hello 目前訂用帳戶，執行：

```powershell
Get-AzureSubscription -Current
```

如果您需要 toochange hello 目前訂用帳戶，請執行：

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a>請檢查您的角色 hello 目前執行個體計數

toocheck hello 的目前狀態執行您的角色：

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

您應該取得 hello 角色，包括其目前的作業系統版本和執行個體計數的相關資訊。 在此情況下，hello 角色都有單一執行個體。

![Hello 角色的相關資訊](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a>藉由新增更多執行個體擴展 hello 角色

tooscale 出您的角色，傳遞 hello 預期的執行個體的數目為 hello**計數**參數 toohello**組 AzureRole** cmdlet:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

hello cmdlet 區塊 hello 的新執行個體時的短暫地佈建與已啟動。 在此期間，如果您開啟新的 PowerShell 視窗並呼叫**Get-azurerole**稍早所示，您會看到 hello 新目標執行個體計數。 如果您檢查 hello hello 入口網站中的角色狀態，您應該會看到 hello 啟動的新執行個體：

![VM instance starting in portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

一旦啟動 hello 的新執行個體，就會成功傳回 hello cmdlet:

![角色執行個體成功增加](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a>縮放 hello 角色中移除執行個體

您可以藉由移除執行個體在 hello 調整角色中相同的方式。 設定 hello**計數**參數**組 AzureRole** toohello 數目的執行個體之後您想要 toohave hello 延展作業已完成。

## <a name="next-steps"></a>後續步驟

不可能 tooconfigure-用於自動調整規模雲端服務從 PowerShell。 請參閱 toodo [tooauto 調整雲端服務的規模](cloud-services-how-to-scale-portal.md)。
