---
title: "aaaStore 和檢視診斷資料，在 Azure 儲存體 |Microsoft 文件"
description: "將 Azure 診斷資料放入 Azure 儲存體並加以檢視"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>在 Azure 儲存體中儲存和檢視診斷資料
除非您傳送 toohello Microsoft Azure 儲存體模擬器或 tooAzure 存放裝置，不會永久儲存診斷資料。 一旦位於儲存體，即可利用其中一個可用的工具進行檢視。

## <a name="specify-a-storage-account"></a>指定儲存體帳戶
您指定您想 toouse hello ServiceConfiguration.cscfg 檔案中的 hello 儲存體帳戶。 hello 帳戶資訊定義為組態設定中的連接字串。 hello 下例示範建立新的雲端服務專案，Visual Studio 中的 hello 預設連接字串：

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

您可以變更此連接字串 tooprovide 帳戶資訊的 Azure 儲存體帳戶。

根據 hello 所收集的診斷資料類型，Azure 診斷會使用 hello Blob 服務或 hello 表格服務。 hello 下表顯示 hello 會保存的資料來源以及其格式。

| 資料來源 | 儲存體格式 |
| --- | --- |
| Azure 記錄檔 |資料表 |
| IIS 7.0 記錄檔 |Blob |
| Azure 診斷基礎結構記錄檔 |資料表 |
| 失敗要求追蹤記錄檔 |Blob |
| Windows 事件記錄檔 |資料表 |
| 效能計數器 |資料表 |
| 損毀傾印 |Blob |
| 自訂錯誤記錄檔 |Blob |

## <a name="transfer-diagnostic-data"></a>傳輸診斷資料
SDK 2.5 和更新版本、 hello 要求 tootransfer 診斷資料可能透過 hello 設定檔。 您可以在 hello 組態中所指定的排程間隔傳輸診斷資料。

SDK 2.4 和前一個您可以透過 hello 設定檔，以程式設計方式要求 tootransfer hello 診斷資料。 hello 以程式設計的方式也可讓您 toodo 上隨選傳輸。

> [!IMPORTANT]
> 當您將傳輸診斷資料 tooan Azure 儲存體帳戶時，就會發生 hello 儲存體資源的診斷資料所使用的成本。
> 
> 

## <a name="store-diagnostic-data"></a>儲存診斷資料
記錄檔資料會儲存在 Blob 或資料表儲存體，以下列名稱的 hello:

**資料表 (英文)**

* **WadLogsTable** -以使用 hello 追蹤接聽程式的程式碼撰寫的記錄檔。
* **WADDiagnosticInfrastructureLogsTable** - 診斷監視器和組態變更。
* **WADDirectoriesTable** – 該 hello 診斷監視器所監視的目錄。  這包括 IIS 記錄檔、IIS 失敗要求記錄檔和自訂目錄。  hello Container 欄位中指定 hello hello blob 記錄檔的位置，且 hello hello blob 名稱 hello RelativePath 欄位中。  hello AbsolutePath 欄位會指示 hello 位置和名稱 hello 檔案，存在於 hello Azure 虛擬機器上。
* **WADPerformanceCountersTable** - 效能計數器。
* **WADWindowsEventLogsTable** – Windows 事件記錄檔。

**Blobs (英文)**

* **wad 控制項容器**– （僅 SDK 2.4 及先前） 包含控制 hello Azure 診斷的 hello XML 組態檔。
* **wad-iis-failedreqlogfiles** – 包含 IIS 失敗要求記錄檔中的資訊。
* **wad-iis-logfiles** – 包含 IIS 記錄檔的相關資訊。
* **"custom"** – 自訂容器，根據設定 hello 診斷監視器所監視的目錄。  hello 這個 blob 容器的名稱將會在 WADDirectoriesTable 中指定。

## <a name="tools-tooview-diagnostic-data"></a>工具 tooview 診斷資料
數個工具都可用 tooview hello 資料之後傳送的 toostorage。 例如：

* 伺服器總管，在 Visual Studio-如果您已安裝 hello Azure Tools for Microsoft Visual Studio，您可以使用 hello Azure 儲存體節點在 伺服器總管 tooview 唯讀 blob 和資料表資料從 Azure 儲存體帳戶。 您可以從您的本機儲存體模擬器帳戶顯示資料，也可以從您為 Azure 建立的儲存體帳戶顯示資料。 如需詳細資訊，請參閱 [使用伺服器總管瀏覽和管理儲存體資源](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md)。
* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是獨立應用程式，可讓您 tooeasily 使用在 Windows、 OSX 和 Linux 的 Azure 儲存體資料。
* [Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction)包含 Azure 診斷管理員可讓您 tooview，下載及管理 hello hello Azure 上執行的應用程式所收集的診斷資料。

## <a name="next-steps"></a>後續步驟
[在雲端服務應用程式中使用 Azure 診斷追蹤 hello 流程](cloud-services-dotnet-diagnostics-trace-flow.md)

