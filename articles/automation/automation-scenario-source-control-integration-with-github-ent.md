---
title: "aaaAzure 自動化原始檔控制整合與 GitHub Enterprise |Microsoft 文件"
description: "Hello 詳細說明的方式使用 GitHub Enterprise tooconfigure 整合原始檔控制的自動化 runbook。"
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Azure 自動化案例 - 自動化原始檔控制與 GitHub Enterprise 的整合

自動化目前支援原始檔控制整合，可讓您 tooassociate 您自動化帳戶 tooa GitHub 原始檔控制儲存機制中的 runbook。  不過，部署的客戶[GitHub Enterprise](https://enterprise.github.com/home) toosupport 其 DevOps 做法，也會想 toouse 它 toomanage hello 生命週期的 runbook 會開發 tooautomate 商務程序和服務管理作業。  

在此案例中，您在 Windows 電腦設定為 Hybrid Runbook Worker 安裝 Git 工具 hello Azure 資源管理員模組與您資料中心。  hello 混合式背景工作電腦有 hello 本機 Git 儲存機制的複製品。  Hello runbook hello 混合式背景工作上執行時，hello Git 目錄同步處理和 hello runbook 檔案內容匯入至 hello 自動化帳戶。

本文說明如何註冊您的 Azure 自動化環境中的此設定 tooset。 我們一開始設定自動化以 hello 安全性認證，runbook 必須 toosupport 此案例中，且部署的混合式 Runbook Worker 在您的資料中心 toorun hello runbook 及存取您的企業 GitHub 儲存機制 toosynchronizerunbook 與您的自動化帳戶。  


## <a name="getting-hello-scenario"></a>取得 hello 案例

此案例包含兩個您可以直接從 hello 匯入的 PowerShell runbook [Runbook 庫](automation-runbook-gallery.md)在 hello Azure 入口網站，或從 hello 下載[PowerShell 資源庫](https://www.powershellgallery.com)。

### <a name="runbooks"></a>Runbook

Runbook | 說明| 
--------|------------|
Export-RunAsCertificateToHybridWorker | Runbook 會從自動化帳戶 tooa hybrid worker 匯出 RunAs 認證，讓 runbook 在 hello 背景工作上的可以驗證搭配 Azure 順序 tooimport runbook 中到 hello 自動化帳戶。| 
Sync-LocalGitFolderToAutomationAccount | Runbook 的同步 hello hello 混合式電腦上的本機 Git 資料夾，然後再將 hello runbook 檔案 (*.ps1) 匯入 hello 自動化帳戶。|

### <a name="credentials"></a>認證

認證 | 說明|
-----------|------------|
GitHRWCredential | 認證資產建立 toocontain hello 使用者名稱和密碼的使用者與權限 toohello 混合式背景工作。|

## <a name="installing-and-configuring-this-scenario"></a>安裝和設定此案例

### <a name="prerequisites"></a>必要條件

1. hello 同步 LocalGitFolderToAutomationAccount runbook 會驗證使用 hello [Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)。 

2. Microsoft Operations Management Suite (OMS) 工作區以 hello Azure 自動化方案已啟用和設定也是必要的。  如果沒有一個 hello 自動化帳戶使用 tooinstall 相關聯，並且設定此案例中，則會建立並為您設定，當您執行 hello**新增 OnPremiseHybridWorker.ps1**從 hello 混合式的指令碼runbook worker。        

    > [!NOTE]
    > 目前 hello 下列區域只支援自動化整合與 OMS-**澳洲東南部**，**美國東部 2**，**東南亞**，和**西歐洲**。 

3. 電腦可做為專用的混合式 Runbook 背景工作，也會裝載 hello GitHub 軟體並維護 hello runbook 檔案 (*runbook*.ps1) hello 檔案系統 toosynchronize 之間 GitHub 上的來源目錄中，您自動化帳戶。

### <a name="import-and-publish-hello-runbooks"></a>匯入及發行 runbook hello

tooimport hello*匯出 RunAsCertificateToHybridWorker*和*同步 LocalGitFolderToAutomationAccount* hello Runbook 資源庫，從您的自動化帳戶 hello Azure 入口網站中的 runbook請依照下列中的 hello 程序[hello Runbook 庫匯入 Runbook](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal)。 它們已成功匯入您的自動化帳戶之後，請發佈 hello runbook。

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>部署和設定 Hybrid Runbook Worker

如果您沒有已部署在您的資料中心 Hybrid Runbook Worker，您應該檢閱 hello 需求，並遵循 hello 自動化的安裝步驟，使用中的 hello 程序[Azure 自動化 Hybrid Runbook Worker-自動安裝和組態](automation-hybrid-runbook-worker.md#automated-deployment)。  一旦您已順利安裝 hello 混合式背景工作，在電腦上，執行 hello 下列步驟 toocomplete 其組態 toosupport 這種情況。

1. Toohello 電腦主控 hello 混合式 Runbook 背景工作角色上使用具有本機系統管理權限的帳戶登入，並建立目錄 toohold hello Git runbook 檔。  複製 hello 內部 Git 儲存機制 toohello 目錄。
2. 如果您沒有建立 RunAs 帳戶或您想要 toocreate 新建一個專門用於此用途，從 hello Azure 入口網站瀏覽 tooAutomation 帳戶中，選取您的自動化帳戶並建立[認證資產](automation-credentials.md)，包含 hello 使用者名稱和密碼之使用者的權限 toohello 混合式背景工作。  
3. 從您的自動化帳戶[編輯 hello runbook](automation-edit-textual-runbook.md)**匯出 RunAsCertificateToHybridWorker**和修改 hello hello 變數值*$Password*具有強式密碼。    修改 hello 值之後，請按一下**發行**hello runbook toohave hello 草稿版本發行。 
5. 啟動 hello runbook**匯出 RunAsCertificateToHybridWorker**，並在 hello**啟動 Runbook**刀鋒視窗中的，在 hello 選項**回合設定**選取 hello 選項**Hybrid Worker**在 hello 下拉式清單選取 hello Hybrid worker 群組您稍早在此案例建立。  

    這會匯出憑證 toohello 混合式背景工作，讓 runbook 在 hello 背景工作上的可以驗證搭配 Azure 使用中訂單 toomanage hello 執行身分連接 （在此案例-匯入 runbook toohello 自動化帳戶的特定） 的 Azure 資源。

4. 從您的自動化帳戶選取 hello 稍早建立的 Hybrid worker 群組和[指定的 RunAs 帳戶](automation-hrw-run-runbooks.md#runas-account)hello Hybrid worker 群組，以及選擇您剛或已建立的 hello 認證資產。  如此可確保該 hello 同步 runbook 可以執行 Git 命令。 
5. 啟動 hello runbook**同步 LocalGitFolderToAutomationAccount**，提供 hello 下列必要的輸入的參數值在 hello**啟動 Runbook**刀鋒視窗中的，在 hello 選項**執行設定**選取 hello 選項**Hybrid Worker**和 hello 下拉式清單選取 hello Hybrid worker 群組您稍早建立此案例中：
    * *ResourceGroup* -hello 您與您的自動化帳戶相關聯的資源群組的名稱
    * *AutomationAccountName* -hello 的自動化帳戶名稱
    * *GitPath* -hello 本機資料夾或 hello Hybrid Runbook Worker Git 設定 toopull 最新變更的位置上的檔案

    將同步 hello 上的本機 Git 資料夾 hello 混合式背景工作電腦，並從 hello 來源目錄 toohello 自動化帳戶，然後匯入 hello.ps1 檔案。

    ![Start Sync-LocalGitFolderToAutomationAccount Runbook](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Hello runbook 工作摘要詳細資料檢視選取從 hello **Runbook**刀鋒視窗，然後選取 hello 與自動化帳戶中的**作業**磚。  確認已成功完成選取 hello**所有記錄檔**磚和檢閱 hello 詳細的記錄檔資料流。  

## <a name="next-steps"></a>後續步驟

-  tooknow 深入了解 runbook 類型、 其優點和限制，請參閱[Azure 自動化 runbook 類型](automation-runbook-types.md)
-  如需 PowerShell 指令碼支援功能的詳細資訊，請參閱 [Azure 自動化中的原生 PowerShell 指令碼支援](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
