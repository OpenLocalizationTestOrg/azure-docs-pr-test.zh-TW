---
title: "aaaUse Azure 自動化 tootrigger 作業 |Microsoft 文件"
description: "深入了解如何 toouse Azure 自動化觸發 StorSimple Data Manager 作業 （私人預覽中）"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>使用 Azure 自動化 tootrigger 作業 （私人預覽中）

此文章說明如何 toouse Azure 自動化 tootrigger StorSimple Data Manager 工作。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您有︰

*   已安裝 Azure Powershell。 [下載 Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。
*   組態設定 tooinitialize hello 資料轉換工作 （tooobtain 這些設定會包含在此處的指示）。
*   已在資源群組內的混合式資料資源中正確設定的工作定義。
*   下載`DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) hello github 儲存機制中的檔案。
*   下載`Get-ConfigurationParams.ps1`[指令碼](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1)hello github 儲存機制中。
*   下載`Trigger-DataTransformation-Job.ps1`[指令碼](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1)hello github 儲存機制中。

## <a name="step-by-step"></a>逐步說明

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>取得 Azure Active Directory hello 自動化工作 toorun hello 作業定義的權限

1. tooretrieve hello 組態參數，如 Active Directory 中，下列步驟 hello:

    1. 在本機電腦中開啟 Windows PowerShell。 確認 [Azure PowerShell](https://azure.microsoft.com/downloads/) 已安裝。
    1. 執行 hello `Get-ConfigurationParams.ps1` （在您下載上方 hello 資料夾） 的指令碼。 輸入下列命令在 hello PowerShell 視窗中的 hello:

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        hello ActiveDirectoryKey 是您稍後使用的密碼。 輸入您選擇的密碼。 AppName 可以是任何字串。

2. 此指令碼輸出 hello 觸發 hello 自動化 runbook 時，應該使用的值。 記下這些值。

    - 用戶端識別碼
    - 租用戶識別碼
    - Active Directory 金鑰 （相同 hello 上面輸入的其中一個）
    - 訂用帳戶識別碼

### <a name="set-up-hello-automation-account"></a>設定 hello 自動化帳戶

1. 登入 tooAzure，開啟您的自動化帳戶。
2. 按一下**資產**磚 tooopen hello 列出的資產清單。
3. 按一下**模組**磚 tooopen hello 模組的清單。
4. 按一下**+ 加入模組**啟動按鈕和 hello 新增模組 刀鋒視窗。

    ![自動化帳戶設定](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. 選取 hello 之後`DataTransformationApp.zip`檔案從本機電腦，請按一下**確定**tooimport hello 模組。

   當 Azure 自動化匯入模組 tooyour 帳戶時，它會擷取 hello 模組的相關中繼資料。 此作業可能需要幾分鐘的時間。

   ![自動化帳戶設定](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. 您會收到通知正在部署該 hello 模組和 hello 程序完成時的另一個通知。  您也可以檢查 hello 狀態**模組**磚。

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>tooimport hello runbook 觸發 hello 工作定義

1. 在 hello Azure 入口網站，開啟您的自動化帳戶。
2. 按一下**Runbook**磚 tooopen hello runbook 的清單。
3. 按一下 [+ 加入 Runbook]，然後按一下 [匯入現有 Runbook]。

   ![匯入現有 Runbook](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. 按一下**Runbook 檔案**和選取 hello 檔案 tooimport `Trigger-DataTransformation-Job.ps1`。
5. 按一下**建立**tooimport hello runbook。 hello 新的 runbook 會出現在 hello 清單 hello 自動化帳戶的 runbook。
7. 按一下 Trigger-DataTransformation-Job Runbook，然後按一下編輯。
8. 按一下 [發行]，並在系統提示您確認時按一下 [是]。


### <a name="toorun-hello-runbook"></a>toorun hello runbook:
1. 在 hello Azure 入口網站，開啟您的自動化帳戶。
2. 按一下 hello **Runbook**磚 tooopen hello runbook 的清單。
3. 按一下 [Trigger-DataTransformation-Job]。
4. 按一下**啟動**toostart hello runbook。

   ![啟動 Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. 在 hello**啟動 runbook**刀鋒視窗中，輸入所有 hello 參數。 按一下**確定**toosubmit hello 資料轉換作業。

   ![啟動 Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>後續步驟

[您的資料使用 StorSimple 資料管理員 UI tootransform](storsimple-data-manager-ui.md)。
