---
title: "aaaAzure 診斷副檔名組態結構描述版本與歷程記錄 |Microsoft 文件"
description: "在 Azure 虛擬機器、 VM 規模集、 Service Fabric 和雲端服務的相關 toocollecting 效能計數器。"
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Azure 診斷延伸模組的設定結構描述版本和歷程記錄
此頁面索引 Azure 診斷擴充功能的結構描述版本隨附於 hello Microsoft Azure SDK 的一部分。  

> [!NOTE]
> hello Azure 診斷擴充功能是 hello 元件使用 toocollect 效能計數器和其他統計資料：
> - Azure 虛擬機器 
> - 虛擬機器擴展集
> - Service Fabric 
> - 雲端服務 
> - 網路安全性群組
> 
> 此頁面只在您使用其中一個服務時才相關。

hello Azure 診斷延伸模組可搭配 Azure 監視、 Application Insights 和記錄分析等其他 Microsoft 診斷產品。 如需詳細資訊，請參閱 [Microsoft 監視工具概觀](monitoring-overview.md)。

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a>Azure SDK 和診斷版本推出方式圖表  

|Azure SDK 版本 | 診斷擴充功能版本 | 模型|  
|------------------|-------------------------------|------|  
|1.x               |1.0                            |外掛程式|  
|2.0 - 2.4         |1.0                            |外掛程式|  
|2.5               |1.2                            |擴充功能|  
|2.6               |1.3                            |"|  
|2.7               |1.4                            |"|  
|2.8               |1.5                            |"|  
|2.9               |1.6                            |"|
|2.96              |1.7                            |"|
|2.96              |1.8                            |"|
|2.96              |1.8.1                          |"|
|2.96              |1.9                            |"|



 Azure 診斷 1.0 版第一次隨附在外掛程式模型--這表示安裝 hello Azure SDK 之後，您會收到 hello 版本隨附於它的 Azure 診斷。  

 SDK 2.5 （診斷 1.2 版），從 Azure 診斷發生 tooan 延伸模型。 hello 工具 tooutilize 新功能只用於較新的 Azure Sdk，但使用 Azure 診斷的任何服務將會收取 hello 傳送新版直接從 Azure。 比方說，仍在使用 SDK 2.5 的任何人都可以載入 hello 最新版本中所顯示 hello 上表中，不論他們使用 hello 較新的功能。  

## <a name="schemas-index"></a>結構描述索引  
不同版本的 Azure 診斷會使用不同的組態結構描述。 

[Azure 診斷 1.0 組態結構描述](azure-diagnostics-schema-1dot0.md)  

[Azure 診斷 1.2 組態結構描述](azure-diagnostics-schema-1dot2.md)  

[診斷 1.3 和更新版本的組態結構描述](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>版本歷程記錄


### <a name="diagnostics-extension-19"></a>診斷擴充功能 1.9 版 
已新增 Docker 支援。


### <a name="diagnostics-extension-181"></a>診斷擴充功能 1.8.1 版 
可以在 hello 私用組態中指定的 SAS 權杖，而不是儲存體帳戶金鑰。如果提供的 SAS 權杖，則會忽略 hello 儲存體帳戶金鑰。


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a>診斷擴充功能 1.8 版 
加入儲存體類型 tooPublicConfig。 StorageType 可以是 Table、Blob、TableAndBlob。 *資料表*hello 預設值。


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a>診斷擴充功能 1.7 版 
加入的 hello 能力 tooroute tooEventHub。

### <a name="diagnostics-extension-15"></a>診斷延伸模組 1.5 版
加入 hello 接收器元素與 hello 能力 toosend 診斷資料太[Application Insights](../application-insights/app-insights-cloudservices.md)讓它更容易 toodiagnose 問題跨您應用程式，以及 hello 系統和基礎結構層級。

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>Azure SDK 2.6 和診斷擴充功能 1.3 版 
Visual Studio 中的雲端服務專案，進行下列變更 hello。 （這些變更也適用於 Azure SDK toolater 版本。）

* hello 本機模擬器現在支援診斷。 這表示您可以收集診斷資料，並確認您的應用程式會建立 hello 正確的追蹤時您正在開發和測試 Visual Studio 中。 hello 連接字串`UseDevelopmentStorage=true`時，您在 Visual Studio 中執行雲端服務專案，使用 hello Azure 儲存體模擬器，請啟用收集診斷資料。 所有診斷資料都收集 hello （開發儲存體） 儲存體帳戶中。
* hello 診斷儲存體帳戶連接字串 (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) 再一次儲存 hello 服務組態 (.cscfg) 檔中。 在 Azure SDK 2.5 hello 診斷儲存體帳戶指定 hello diagnostics.wadcfgx 檔案中。

有一些值得注意的差異之間 hello 連接字串已在 Azure SDK 2.4 及更早版本的運作，而且在 Azure SDK 2.6 和更新版本，它的運作方式。

* 在 Azure SDK 2.4 及更早版本，hello 已使用的連接字串做為執行階段 hello 診斷外掛程式 tooget hello 儲存體帳戶資訊的傳輸診斷記錄檔。
* 在 Azure SDK 2.6 和更新版本，hello 診斷連接字串使用 Visual Studio tooconfigure hello 診斷延伸模組以在發行期間的 hello 適當的儲存體帳戶資訊。 hello 連接字串可讓您定義不同的服務組態，Visual Studio 在發行時使用不同的儲存體帳戶。 不過，因為 （在 Azure SDK 2.5) 已無法再使用 hello 診斷外掛程式，hello.cscfg 檔案本身無法啟用 hello 診斷延伸模組。 您有透過 Visual Studio 或 PowerShell 之類的工具來分別 tooenable hello 延伸模組。
* toosimplify hello 程序使用 PowerShell 設定 hello 診斷延伸模組，從 Visual Studio 的 hello 封裝輸出也包含 hello 公用組態 XML，每個角色的 hello 診斷延伸模組。 Visual Studio 使用 hello 診斷連接字串 toopopulate hello 儲存體帳戶資訊出現在 hello 公用組態。 hello 公用組態檔 hello 擴充功能 資料夾中建立，並遵循 Paasdiagnostics.<rolename>.pubconfig.xml 的 hello 模式。<RoleName>.模式。 任何 PowerShell 部署可以使用此模式 toomap 每個組態 tooa 角色。
* hello hello.cscfg 檔案中的連接字串也會使用 hello Azure 入口網站 tooaccess hello 診斷資料，它可以出現在 hello**監視** 索引標籤 hello 連接字串是所需的 tooconfigure hello 服務 tooshow 詳細資訊hello 入口網站中的監視資料。

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a>移轉專案 tooAzure SDK 2.6 和更新版本
當移轉從 Azure SDK 2.5 tooAzure SDK 2.6 或更新版本，如果您在診斷儲存體帳戶，指定在 hello.wadcfgx 檔案中，然後它會留在那裡。 tootake 優點 hello 彈性使用不同的儲存體帳戶的不同存放裝置組態，您必須加入 hello 連接字串 tooyour 專案 toomanually。 如果您從 Azure SDK 2.4 或較早 tooAzure SDK 2.6 移轉專案，然後 hello 的診斷連接字串會保留。 不過，請注意 hello 變更連接字串中的處理方式在 Azure SDK 2.6 中所述的 hello 上一節。

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Visual Studio 如何決定 hello 診斷儲存體帳戶
* 如果 hello.cscfg 檔案中指定診斷連接字串，Visual Studio 會使用 tooconfigure hello 診斷擴充功能發行時，並在封裝期間產生 hello 公用組態 xml 檔案時。
* 如果 hello.cscfg 檔案中不指定任何診斷連接字串，然後 Visual Studio 會回復指定 hello.wadcfgx 檔案 tooconfigure hello 診斷擴充功能發行時及產生 hello 公用 toousing hello 儲存體帳戶設定 xml 檔案封裝時。
* hello.cscfg 檔案中的 hello 診斷連接字串的優先順序高於 hello hello.wadcfgx 檔案中的儲存體帳戶。 如果診斷連接字串 hello.cscfg 檔案中指定然後 Visual Studio 會使用，並忽略.wadcfgx 中的 hello 儲存體帳戶。

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>功能沒有 hello 「 更新開發儲存體連接字串...」 作用為何？
hello 核取方塊**更新開發儲存體連接字串以供診斷和快取，使用 Microsoft Azure 儲存體帳戶認證發行 tooMicrosoft Azure 時**可讓您方便 tooupdate 任何開發儲存體帳戶連接字串與 hello 發行期間指定的 Azure 儲存體帳戶。

例如，假設您選取此核取方塊並 hello 診斷連接字串指定`UseDevelopmentStorage=true`。 當您發行 hello 專案 tooAzure 時，Visual Studio 會自動更新 hello 診斷連接字串與 hello hello 發行精靈中指定的儲存體帳戶。 不過，如果實際的儲存體帳戶指定為 hello 診斷連接字串，然後該帳戶改用。

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Azure SDK 2.4 及更舊版本和 Azure SDK 2.5 及更新版本之間的診斷功能差異
如果您要升級您的專案，從 Azure SDK 2.4 tooAzure SDK 2.5 或更新版本，您應該謹記在心 hello 下列診斷功能差異。

* **組態 API 已被取代** – 診斷的程式設計組態可在 Azure SDK 2.4 或更舊版本中使用，但在 Azure SDK 2.5 及更新版本中已被取代。 如果您的診斷組態目前定義在程式碼中，您將需要 tooreconfigure 從頭診斷 tookeep 工作順序中的 hello 移轉專案中的這些設定。 hello Azure SDK 2.4 的診斷組態檔是 diagnostics.wadcfg，是 diagnostics.wadcfgx Azure SDK 2.5 和更新版本。
* **雲端服務應用程式的診斷功能只能在 hello 角色層級，不是在 hello 執行個體層級設定。**
* **每次您部署應用程式時，會更新 hello 診斷組態**– 如果您從 [伺服器總管] 中變更診斷組態，然後重新部署您的應用程式，這可能會造成同位檢查問題。
* **在 Azure SDK 2.5 和更新版本，hello 診斷組態檔中，未在程式碼中設定損毀傾印**– 如果您有程式碼中設定損毀傾印，您就必須 toomanually 傳送嗨組態從程式碼 toohello 組態檔由於 hello 損毀傾印不傳送 hello 移轉 tooAzure SDK 2.6 期間。

