---
title: "aaaUpdate Azure 在 Azure 自動化模組 |Microsoft 文件"
description: "本文說明現在要如何更新 Azure 自動化中預設提供的通用 Azure PowerShell 模組。"
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>如何在 Azure 自動化中的 tooupdate Azure PowerShell 模組

hello 最常見的 Azure PowerShell 模組會提供預設會在每個自動化帳戶。  hello Azure 團隊更新定期 hello Azure 模組，以便在 hello 自動化帳戶中我們提供一種您 tooupdate hello 帳戶中的 hello 模組從 hello 入口網站的新版本可用時。  

模組會定期更新 hello 產品群組，因為變更可能會發生與 hello 包含 cmdlet，這可能會對您的 runbook，根據 hello 類型變更，例如重新命名的參數，或完全淘汰 cmdlet 產生負面影響。 影響您的 runbook 和 hello tooavoid 自動化程序，強烈建議您測試和驗證，然後再繼續。  如果您沒有適用於此用途的專用的自動化帳戶，請考慮建立一個，以便您可以測試許多不同的案例和排列您的 runbook，加法 tooiterative 變更，例如更新 hello hello 開發期間PowerShell 模組。  Hello 結果會進行驗證，而且您已套用所需的任何變更之後，繼續進行協調 hello 移轉的需要修改任何 runbook，並執行 hello 更新，如下所述在生產環境中。     

## <a name="updating-azure-modules"></a>更新 Azure 模組

1. Hello 模組中您的自動化帳戶有刀鋒視窗是選項呼叫**更新 Azure 模組**。  它一律為啟用狀態。<br><br> ![[模組] 刀鋒視窗中的 [更新 Azure 模組] 選項](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. 按一下**更新 Azure 模組**，您將會出現詢問您是否 toocontinue 確認通知。<br><br> ![更新 Azure 模組通知](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. 按一下**是**hello 模組更新程序會開始。  hello 更新程序，大約需要 15 20 分鐘 tooupdate hello 下列模組：

  * Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    如果 hello 模組已經註冊 toodate，hello 程序將會完成在幾秒鐘的時間。  Hello 更新程序完成時將會通知您。<br><br> ![更新 Azure 模組更新狀態](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Azure 自動化會使用 hello 最新的模組，您的自動化帳戶中，新的排程的工作執行時。    

如果您使用 cmdlet 從您的 runbook toomanage Azure 在這些 Azure PowerShell 模組的資源，則您會想 tooperform 這個更新程序每月或您擁有的 tooassure 因此 hello 最新的模組。

## <a name="next-steps"></a>後續步驟

* toolearn 深入了解整合模組和 toocreate 自訂模組 toofurther 如何整合自動化與其他系統、 服務或方案，請參閱[整合模組](automation-integration-modules.md)。

* 請考慮使用的原始檔控制整合[GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md)或[Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally 管理和控制自動化 runbook 及設定組合的版本。  
