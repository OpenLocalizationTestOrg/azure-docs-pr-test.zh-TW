---
title: "aaaTroubleshoot Azure Data Factory 問題"
description: "了解如何使用 Azure Data Factory tootroubleshoot 問題。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a>資料處理站的疑難排解
這篇文章提供使用 Azure Data Factory 時的問題疑難排解提示。 本文使用 hello 服務時不會列出所有的 hello 可能的問題，但涵蓋了某些問題和一般的疑難排解秘訣。   

## <a name="troubleshooting-tips"></a>疑難排解秘訣
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>錯誤： hello 訂用帳戶不是已註冊的 toouse 命名空間 'Microsoft.DataFactory'
如果您收到這個錯誤，hello Azure Data Factory 的資源提供者尚未註冊您的電腦上。 請勿 hello 遵循：

1. 啟動 Azure PowerShell。
2. 使用下列命令的 hello 的 Azure 帳戶登入 tooyour 中。

    ```powershell
    Login-AzureRmAccount
    ```
3. 執行下列命令 tooregister hello Azure Data Factory 提供者的 hello。

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>問題：執行 Data Factory Cmdlet 時發生未授權錯誤
您可能不會使用 hello 右邊的 Azure 帳戶或訂用帳戶以 hello Azure PowerShell。 使用下列 cmdlet tooselect hello 權限以 hello Azure PowerShell 的 Azure 帳戶和訂用帳戶 toouse hello。

1. 登入-AzureRmAccount-使用 hello 權限的使用者識別碼和密碼
2. Get AzureRmSubscription-檢視所有 hello hello 帳戶的訂用帳戶。
3. 選取 AzureRmSubscription&lt;訂用帳戶名稱&gt;-選取 hello 右訂用帳戶。 使用 hello 同一個您可以使用 data factory toocreate hello Azure 入口網站上。

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>問題： 無法從 Azure 入口網站的 toolaunch 資料管理閘道 Express 安裝程式
資料管理閘道器 hello Express 安裝程式需要 Internet Explorer 或與 Microsoft ClickOnce 相容的 web 瀏覽器。 Toostart hello Express 安裝程式時，執行 hello 下列其中一種動作：

* 使用 Internet Explorer 或 Microsoft ClickOnce 相容的 Web 瀏覽器。

    如果您使用 Chrome，請移至 toohello [Chrome web store](https://chrome.google.com/webstore/)、 搜尋與"ClickOnce"關鍵字、 選擇其中一個 hello ClickOnce 擴充功能，及安裝它。

    請勿 hello 相同 Firefox （安裝增益集）。 按一下 hello 工具列 （三條水平線 hello 右上角） 上的開啟功能表按鈕、 按一下 附加元件、 搜尋與"ClickOnce"關鍵字，選擇其中一個 hello ClickOnce 擴充功能，並安裝它。
* 使用 hello**手動安裝**連結顯示 hello hello 入口網站中的相同刀鋒視窗。 您可以使用此方法 toodownload 安裝檔案，並手動執行它。 Hello 安裝成功之後，您會看到 hello 資料管理閘道組態對話方塊。 複製 hello**金鑰**防止 hello 入口網站畫面並在 hello configuration manager toomanually hello 閘道註冊 hello 服務的使用。  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>問題： 失敗 tooconnect tooon 內部部署 SQL Server
啟動**資料管理閘道組態管理員**hello 閘道電腦且使用 hello**疑難排解**tootest hello 連接 tooSQL hello 閘道電腦從伺服器索引標籤上。 如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>問題：輸入配量永遠處於 Waiting 狀態
hello 配量可能處於**等候**到期 toovarious 原因的狀態。 其中一個 hello 的常見原因是該 hello**外部**屬性未設定太**true**。 Azure Data Factory 外部產生的 hello 範圍的任何資料集應該用來標記**外部**屬性。 此屬性會指出 hello 資料的外部和任何管線內 hello 資料處理站不支援。 hello 資料配量會標示為**準備**一旦 hello 資料可在 hello 個別存放區中。

請參閱下列範例 hello 使用量的 hello hello**外部**屬性。 您可以選擇性地指定**externalData*** 當您將外部 tootrue。

如需此屬性的詳細資訊，請參閱 [資料集](data-factory-create-datasets.md) 文章。

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

tooresolve hello 錯誤、 新增 hello**外部**屬性和選用的 hello **externalData**區段 toohello JSON 定義的 hello 輸入資料表，並重新建立 hello 資料表。

### <a name="problem-hybrid-copy-operation-fails"></a>問題：混合式複製作業失敗
請參閱[閘道問題的疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues)的 tootroubleshoot 問題複製至 azure 或從內部部署資料存放區使用的步驟 hello 資料管理閘道器。

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>問題：隨選 HDInsight 佈建失敗
使用型別 HDInsightOnDemand 連結的服務時，您會需要 toospecify linkedServiceName 指向 tooan Azure Blob 儲存體。 資料 Factory 服務會隨 HDInsight 叢集使用此儲存體 toostore 記錄並支援檔案。  有時在隨選 HDInsight 叢集的佈建失敗並 hello 下列錯誤：

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

此錯誤通常表示 hello hello hello linkedServiceName 中指定的儲存體帳戶的位置不在 hello 相同資料中心位置發生 hello HDInsight 佈建的位置。 範例： 如果您的 data factory 是在美國西部且 hello Azure 儲存體位於美國東部、 hello 美國西部的依需求佈建失敗。

此外，還有第二個的 JSON 屬性 additionalLinkedServiceNames，可供隨選 HDInsight 中指定其他儲存體帳戶。 這些額外的連結儲存體帳戶應為 hello 的 hello 相同 hello HDInsight 叢集，或它的位置失敗時相同的錯誤。

### <a name="problem-custom-net-activity-fails"></a>問題：自訂 .NET 活動失敗
如需詳細步驟，請參閱 [偵錯具有自訂活動的管線](data-factory-use-custom-activities.md#troubleshoot-failures) 。

## <a name="use-azure-portal-tootroubleshoot"></a>使用 Azure 入口網站 tootroubleshoot
### <a name="using-portal-blades"></a>使用入口網站刀鋒視窗
請參閱 [監視管線](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) 以取得步驟。

### <a name="using-monitor-and-manage-app"></a>使用監視及管理應用程式
如需詳細資訊，請參閱 [使用監視及管理應用程式，來監視及管理 Data Factory 管線](data-factory-monitor-manage-app.md) 。

## <a name="use-azure-powershell-tootroubleshoot"></a>使用 Azure PowerShell tootroubleshoot
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>使用 Azure PowerShell tootroubleshoot 錯誤
如需詳細資料，請參閱 [使用 Azure PowerShell 監視 Data Factory 管線](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) 。

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
