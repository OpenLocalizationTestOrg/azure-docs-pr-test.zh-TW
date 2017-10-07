---
title: "Azure 堆疊 aaaUse 範本驗證程式 toocheck 範本 |Microsoft 文件"
description: "檢查部署 tooAzure 堆疊的範本"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: helaw
ms.openlocfilehash: ee649f2ebf77486ca5036116dd73a45d66884704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a>使用「範本驗證程式」來檢查 Azure Stack 的範本
您可以使用 hello 範本驗證工具 toocheck，如果您的 Azure 資源管理員[範本](azure-stack-arm-templates.md)已準備好進行 Azure 堆疊。 hello 範本驗證工具會提供 hello Azure 堆疊工具的一部分。 使用 hello hello 中所述的步驟來下載 hello Azure 堆疊工具[從 GitHub 下載工具](azure-stack-powershell-download.md)發行項。 

toovalidate 範本，您可以使用下列 PowerShell 模組的 hello 和 hello JSON 檔案位於**TemplateValidator**和**CloudCapabilities**資料夾： 

 - AzureRM.CloudCapabilities.psm1 建立雲端功能 JSON 檔案代表 hello 服務和 Azure 堆疊等雲端中的版本。
 - AzureRM.TemplateValidator.psm1 用雲端功能 JSON 檔案 tootest 範本來進行 Azure 堆疊中的部署。
 - AzureStackCloudCapabilities_with_AddOns_20170627.json 是預設的雲端功能檔案。  您可以建立您自己，或啟動此檔案 tooget。 

在此主題中，您會為您的範本執行驗證，而且可以選擇性建置雲端功能檔案。

## <a name="validate-templates"></a>驗證範本
在這些步驟中，您可以驗證範本使用 hello AzureRM.TemplateValidator PowerShell 模組。 您可以使用您自己的範本，或驗證 hello [Azure 堆疊快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates)。

1.  匯入 hello AzureRM.TemplateValidator.psm1 PowerShell 模組：
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  執行 hello 範本驗證程式：

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path tootemplate.json or template folder> `
    -CapabilitiesPath <path toocloudcapabilities.json> `
    -Verbose
    ```

任何範本驗證警告或錯誤記錄的 toohello PowerShell 主控台中，而且也會記錄的 tooan hello 來源目錄中的 HTML 檔案。 Hello 驗證報表輸出的範例看起來像這樣：

![範例驗證報告](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a>參數

| 參數 | 說明 | 必要 |
| ----- | -----| ----- |
| TemplatePath | 指定 hello 路徑 toorecursively 尋找資源管理員範本 | 是 | 
| TemplatePattern | 指定範本檔案 toomatch hello 名稱。 | 否 |
| CapabilitiesPath | 指定 hello 路徑 toocloud 功能 JSON 檔案 | 是 | 
| IncludeComputeCapabilities | 包括 IaaS 資源 (例如 VM 大小與 VM 擴充功能) 的評估 | 否 |
| IncludeStorageCapabilities | 包括儲存體資源 (例如 SKU 類型) 的評估 | 否 |
| 報告 | 指定名稱的 hello 產生 HTML 報表 | 否 |
| 詳細資訊 | 記錄錯誤和警告 toohello 主控台 | 否|


### <a name="examples"></a>範例
這個範例會驗證所有 hello [Azure 堆疊快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates)下載至本機，並也會都驗證 hello VM 大小和擴充功能，針對 Azure 堆疊開發套件功能。

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a>建置雲端功能檔案
hello 下載的檔案包含預設值*AzureStackCloudCapabilities_with_AddOns_20170627.json*檔案，其中描述 Azure 堆疊開發套件中可用的 hello 服務版本與安裝的 PaaS 服務。  如果您安裝額外的資源提供者，您可以使用 hello AzureRM.CloudCapabilities PowerShell 模組 toobuild 包括 hello 新服務的 JSON 檔案。  

1.  請確定您已連線 tooAzure 堆疊。  您可以從 hello Azure 堆疊開發套件主機，執行下列步驟，或者您可以使用[VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect 從您的工作站。 
2.  匯入 hello AzureRM.CloudCapabilities PowerShell 模組：

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  使用 Get CloudCapabilities hello cmdlet tooretrieve 服務版本，並建立的雲端功能的 JSON 檔案：

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a>後續步驟
 - [部署範本 tooAzure 堆疊](azure-stack-arm-templates.md)
 - [部署 Azure Stack 的範本] (azure-stack-develop-templates.md)

