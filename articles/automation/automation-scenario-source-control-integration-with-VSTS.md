---
title: "與 Visual stuido 來 Team Services 原始檔控制的 Azure 自動化 aaaIntegrate |Microsoft 文件"
description: "案例將逐步引導您設定 Azure 自動化帳戶與 Visual Stuido Team Services 原始檔控制的整合。"
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "azure powershell, VSTS, 原始檔控制, 自動化"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Azure 自動化案例 - 自動化原始檔控制與 Visual Studio Team Services 的整合

在此案例中，您有 Visual Studio Team Services 專案，您會使用 toomanage Azure 自動化 runbook 或原始檔控制下的 DSC 設定。
本文說明如何與 Azure 自動化環境讓該持續整合就進行每次簽入 toointegrate VSTS。

## <a name="getting-hello-scenario"></a>取得 hello 案例

此案例包含兩個您可以直接從 hello 匯入的 PowerShell runbook [Runbook 庫](automation-runbook-gallery.md)在 hello Azure 入口網站，或從 hello 下載[PowerShell 資源庫](https://www.powershellgallery.com)。

### <a name="runbooks"></a>Runbook

Runbook | 說明| 
--------|------------|
Sync-VSTS | 完成簽入時，從 VSTS 原始檔控制匯入 Runbook 或組態。 如果以手動方式執行，它將會匯入及發行所有 runbook 或設定成 hello 自動化帳戶。| 
Sync-VSTSGit | 完成簽入時，從 Git 原始檔控制下的 VSTS 匯入 Runbook 或組態。 如果以手動方式執行，它將會匯入及發行所有 runbook 或設定成 hello 自動化帳戶。|

### <a name="variables"></a>變數

變數 | 說明|
-----------|------------|
VSToken | 保護變數將會建立包含的資產 hello VSTS 個人存取權杖。 您可以了解如何 toocreate VSTS 個人存取權杖上 hello [VSTS 驗證頁面](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)。 
## <a name="installing-and-configuring-this-scenario"></a>安裝和設定此案例

建立[個人存取權杖](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)VSTS 您將為您的自動化帳戶使用 toosync hello runbook 或組態中。

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

建立[secure 變數](automation-variables.md)在您的自動化帳戶 toohold hello 個人存取權杖，讓 hello runbook 可以驗證 tooVSTS 和同步處理 hello runbook 或設定成 hello 自動化帳戶。 您可以將此命名為 VSToken。 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

匯入 hello runbook 會同步您的 runbook 或設定成 hello 自動化帳戶。 您可以使用 hello [VSTS 範例 runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript)或 hello [VSTS 與 Git 範例 runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) 從 hello PowerShellGallery.com 視您使用 VSTS原始檔控制或 Git 與 VSTS 和部署 tooyour 自動化帳戶。

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

您現在可以[發佈](automation-creating-importing-runbook.md#publishing-a-runbook)此 Runbook，以便建立 Webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

建立[webhook](automation-webhooks.md)此同步 VSTS runbook 和填滿 hello 參數，如下所示。 請確定您複製 hello webhook url 將需於 VSTS 中的服務勾點。 hello VSAccessTokenVariableName 為您建立舊版 toohold hello 個人存取權杖的 hello 安全變數 hello 名稱 (VSToken)。 

整合與 VSTS (同步-VSTS.ps1) 需要下列參數的 hello。
### <a name="sync-vsts-parameters"></a>Sync-VSTS Parameters

參數 | 說明| 
--------|------------|
WebhookData | 這會包含從 hello VSTS 服務勾點傳送 hello 簽入資訊。 您應該將此參數保留為空白。| 
ResourceGroup | 這是 hello hello 資源群組中的 hello 自動化帳戶的名稱。|
AutomationAccountName | hello hello 與 VSTS 將同步的自動化帳戶名稱。|
VSFolder | VSTS 存在 hello runbook 和組態中的 hello 資料夾的名稱。|
VSAccount | hello hello Visual Studio Team Services 帳戶名稱。| 
VSAccessTokenVariableName | hello hello 安全的變數名稱 (VSToken) 保留 hello VSTS 個人存取權杖。| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

如果您使用 VSTS 含 GIT (同步-VSTSGit.ps1) 需要下列參數的 hello。

參數 | 說明|
--------|------------|
WebhookData | 這會包含從 hello VSTS 服務勾點傳送 hello 簽入資訊。 您應該將此參數保留為空白。| ResourceGroup | 這個 hello hello 資源群組的名稱中的 hello 自動化帳戶。|
AutomationAccountName | hello hello 與 VSTS 將同步的自動化帳戶名稱。|
VSAccount | hello hello Visual Studio Team Services 帳戶名稱。|
VSProject | hello VSTS 存在 hello runbook 和組態中的 hello 專案名稱。|
GitRepo | hello hello Git 儲存機制名稱。|
GitBranch | hello VSTS Git 儲存機制中的 hello 分支名稱。|
資料夾 | hello VSTS Git 分支中的 hello 資料夾名稱。|
VSAccessTokenVariableName | hello hello 安全的變數名稱 (VSToken) 保留 hello VSTS 個人存取權杖。|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

建立於 VSTS 中的服務勾點，此 webhook 在程式碼簽入觸發程序的簽入 toohello 資料夾。 選取 Web Hook 做為 hello 服務 toointegrate 與當您建立新的訂用帳戶。 您可以在 [VSTS 服務掛勾說明文件](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started)深入了解服務掛勾。
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

您應該要能 toodo 所有簽入您的 runbook 和 vsts 組態的並在這些自動現在會同步處理已為您的自動化帳戶。

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

如果您手動執行此 runbook，而不由 VSTS 被觸發，則可以是空白 hello webhookdata 參數，它會執行完整同步處理從指定的 hello VSTS 資料夾。

如果您想 toouninstall hello 案例中，從 VSTS 移除 hello 服務勾點，刪除 hello runbook 和 hello VSToken 變數。
