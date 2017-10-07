---
title: "計算 aaaAzure-Linux 診斷延伸模組 |Microsoft 文件"
description: "如何 tooconfigure hello Azure Linux 診斷延伸模組 （年輕人） toocollect 度量，並記錄在 Azure 中執行的 Linux Vm 所傳來的事件。"
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>使用 Linux 診斷延伸模組 toomonitor 度量和記錄檔

本文件描述版本 3.0 和較新的 hello Linux 診斷延伸模組。

> [!IMPORTANT]
> 如需 2.3 版與更舊版本的資訊，請參閱[本文件](./classic/diagnostic-extension-v2.md)。

## <a name="introduction"></a>簡介

hello Linux 診斷延伸模組可協助 Microsoft Azure 上執行的 Linux VM 的 hello 使用者監視健全狀況。 它有下列功能的 hello:

* 會收集從 hello VM 的系統效能度量，並將它們儲存在指定的儲存體帳戶中的特定資料表中。
* 擷取記錄事件從 syslog，並將它們儲存在指定的儲存體帳戶的 hello 中特定資料表。
* 可讓使用者 toocustomize hello 資料計量所收集和上傳。
* 可讓使用者 toocustomize hello syslog 設備與嚴重性層級的事件所收集和上傳。
* 可讓使用者 tooupload 指定的記錄檔 tooa 指定之儲存體資料表。
* 支援傳送嗨度量和記錄檔事件 tooarbitrary EventHub 端點和 JSON 格式的 blob 指定的儲存體帳戶。

此擴充功能適用於這兩個 Azure 部署模型。

## <a name="installing-hello-extension-in-your-vm"></a>安裝在 VM 中的 hello 擴充功能

您可以使用 hello Azure PowerShell cmdlet、 Azure CLI 指令碼或 Azure 的部署範本，以啟用這項擴充功能。 如需詳細資訊，請參閱[擴充功能](./extensions-features.md)。

hello Azure 入口網站無法使用的 tooenable 或設定年輕人 3.0。 相反地，它會安裝並設定 2.3 版。 Azure 入口網站的圖形和警示處理 hello 延伸模組的兩個版本的資料。

這些安裝指示與[可下載範例組態](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json)可設定 LAD 3.0 以：

* 擷取和儲存 hello 相同度量資訊是年輕人 2.3; 所提供
* 擷取檔案系統度量，新 tooLAD 3.0; 有用設
* 擷取 hello 預設 syslog 集合啟用年輕人 2.3;
* 啟用 hello 圖表和 VM 度量的警示的 Azure 入口網站體驗。

hello 可下載組態只是一個範例。修改 toosuit 您自己的需求。

### <a name="prerequisites"></a>必要條件

* **Azure Linux Agent 2.2.0 版或更新版本**。 大部分的 Azure VM Linux 資源庫映像包含版本 2.2.7 或更新版本。 執行`/usr/sbin/waagent -version`hello VM 上安裝的 tooconfirm hello 版本。 如果 hello VM 正在執行較舊版本的 hello 客體代理程式，請遵循[這些指示](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent)tooupdate 它。
* **Azure CLI**。 [設定 hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)您的電腦上的環境。
* 如果您沒有 hello wget 命令： 執行`sudo apt-get install wget`。
* 現有的 Azure 訂用帳戶和現有的儲存體帳戶內 toostore hello 資料。

### <a name="sample-installation"></a>範例安裝

填寫 hello hello 上正確的參數前三行，然後執行此指令碼為根：

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

hello hello 範例組態中，URL 和它的內容，是主體 toochange。 下載 hello 入口網站設定 JSON 檔案的副本，並針對您的需求加以自訂。 您建構的任何範本或自動化項目應使用您自己的複本，而非每次都要下載該 URL。

### <a name="updating-hello-extension-settings"></a>更新 hello 延伸模組設定

您已變更您的受保護或公用設定之後，將其部署 toohello VM 執行 hello 相同的命令。 如果任何項目在 hello 設定進行變更，hello 更新設定傳送 toohello 延伸模組。 年輕人重新載入 hello 組態，並自行重新啟動。

### <a name="migration-from-previous-versions-of-hello-extension"></a>從舊版的 hello 延伸模組的移轉

hello hello 延伸模組的最新版本是**3.0**。 **任何舊版 (2.x) 皆已被取代，並會 2018 年 7 月 31 日停止發行**。

> [!IMPORTANT]
> 這項擴充功能引進 hello 擴充的重大變更 toohello 組態。 一個這類變更 tooimprove hello 安全性 hello 延伸模組。如此一來，回溯相容性 2.x 可能不會保留。 此外，hello 擴充功能發行者針對此延伸模組是與 hello 2.x 版的 hello 發行者不同。
>
> toomigrate 從 2.x toothis 新版 hello 擴充功能，您必須先解除安裝 hello 舊擴充功能 （在 hello 舊發行者的名稱），然後安裝第 3 版的 hello 延伸模組。

建議：

* 安裝 hello 擴充功能啟用自動的次要版本升級。
  * 在傳統部署模型的 Vm，指定 '3.*' hello 版本，如果您要安裝 hello 延伸模組，透過 Azure XPLAT CLI 或 Powershell。
  * Azure Resource Manager 部署模型的 Vm，包括 '"autoUpgradeMinorVersion": true' hello VM 部署範本中。
* 為 LAD 3.0 使用新/不同的儲存體帳戶。 LAD 2.3 與 LAD 3.0 之間些許不相容，讓共用帳戶變得麻煩：
  * LAD 3.0 會將 Syslog 事件儲存在採用不同名稱的資料表中。
  * 字串 hello counterSpecifier`builtin`年輕人 3.0 在不同的度量。

## <a name="protected-settings"></a>受保護的設定

這一組的組態資訊包含敏感性資訊，應加以保護以防遭公開檢視，例如儲存體認證。 這些設定是傳輸的 tooand hello 延伸模組，以加密形式儲存。

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

名稱 | 值
---- | -----
storageAccountName | hello 資料寫入 hello 延伸模組的 hello 儲存體帳戶名稱。
storageAccountEndPoint | （選擇性） hello 端點識別 hello 雲端中的 hello 儲存體帳戶存在。 如果此設定不存在，年輕人預設 toohello Azure 公用雲端， `https://core.windows.net`。 儲存體帳戶在 Azure 德國、 Azure 政府或 Azure China toouse 據以設定此值。
storageAccountSasToken | [帳戶 SAS 權杖](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/)Blob 和表格服務 (`ss='bt'`)，適用於 toocontainers 和物件 (`srt='co'`)、 哪些授與新增，請建立、 列出、 更新和寫入權限 (`sp='acluw'`)。 請勿*不*包含 hello 前置問號 （？）。
mdsdHttpProxy | （選擇性）HTTP proxy 所需的資訊 tooenable hello 延伸 tooconnect toohello 指定儲存體帳戶及端點。
sinksConfig | （選擇性）可以傳遞替代目的地 toowhich 計量和事件的詳細資料。 hello 以下各節會說明 hello 的 hello 延伸模組支援每個資料接收的特定詳細資料。

您可以輕鬆地建構透過 hello Azure 入口網站的所需的 hello SAS 權杖。

1. 選取您想要 hello 延伸 toowrite hello 一般用途儲存體帳戶 toowhich
1. 選取從 hello 設定部分 hello 左側功能表的 [共用存取簽章]
1. 請如先前所述的 hello 適當章節
1. 按一下 hello"產生 SAS 」 按鈕。

![image](./media/diagnostic-extension/make_sas.png)

複製 hello 產生 SAS hello storageAccountSasToken 欄位;移除 hello 前置問號 (「？ 」)。

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

這個選擇性區段會定義 toowhich hello 延伸模組會將它所收集的 hello 資訊的其他目的地。 hello 的 「 接收 」 陣列會包含每個額外的資料接收的物件。 「 類型 」 屬性會決定的 hello hello hello 物件中的其他屬性。

元素 | 值
------- | -----
名稱 | 使用 toorefer toothis 接收 hello 延伸模組組態中的其他位置的字串。
類型 | hello 類型所定義的接收。 在這種情況，判斷 hello 其他值 （是否有的話）。

3.0 版的 hello Linux 診斷延伸模組支援兩種接收類型： EventHub 和 JsonBlob。

#### <a name="hello-eventhub-sink"></a>hello EventHub 接收

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

hello"sasURL"項目，包含完整的 URL，包括 SAS 權杖，如 hello 事件中樞 toowhich 資料應經過發佈的 hello。 年輕人需要 SAS 命名的原則，可讓 hello 傳送宣告。 例如：

* 建立名為 `contosohub` 的事件中樞命名空間
* 建立事件中樞時呼叫的 hello 命名空間中`syslogmsgs`
* Hello 名為事件中心上建立共用存取原則`writer`啟用 hello 傳送宣告

如果您建立了 SAS 良好 2018 年 1 月 1 午夜 UTC 直到 hello sasURL 值可能是：

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

如需為事件中樞產生 SAS 權杖的相關詳細資訊，請參閱[本網頁](../../event-hubs/event-hubs-authentication-and-security-model-overview.md)。

#### <a name="hello-jsonblob-sink"></a>hello JsonBlob 接收

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

資料導向 tooa JsonBlob 接收器會儲存在 Azure 儲存體中的 blob。 LAD 的每個執行個體每小時會為每個接收名稱建立 Blob。 每個 Blob 一律包含物件的語法有效 JSON 陣列。 Toohello 陣列，會以不可分割方式加入新項目。 Blob 會儲存在名稱為 hello 接收相同的 hello 的容器。 hello Azure 儲存體規則的 blob 容器名稱的 JsonBlob 接收 toohello 名稱： 介於 3 到 63 個小寫英數字元的 ASCII 字元或連字號。

## <a name="public-settings"></a>公用設定

此結構包含控制 hello hello 擴充所收集的資訊設定的不同區塊。 每個設定皆為選擇性。 如果您指定 `ladCfg`，則亦須指定 `StorageAccount`。

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

元素 | 值
------- | -----
StorageAccount | hello 資料寫入 hello 延伸模組的 hello 儲存體帳戶名稱。 必須是相同的名稱，指定在 hello hello[保護設定](#protected-settings)。
mdsdHttpProxy | （選擇性）如同 hello 相同[保護設定](#protected-settings)。 hello 公用值會覆寫 hello 私用的值，如果設定。 將 proxy 設定包含密碼，例如密碼 hello 中放入[保護設定](#protected-settings)。

hello 下列各節將詳細說明 hello 其餘項目。

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

此選擇性結構控制項 hello 的收集度量和記錄檔，傳遞 toohello Azure 度量服務和 tooother 資料接收器。 您必須指定 `performanceCounters` 或 `syslogEvents` 或是兩者。 您必須指定 hello`metrics`結構。

元素 | 值
------- | -----
eventVolume | （選擇性）控制項 hello hello 儲存體資料表中建立的資料分割數目。 必須是 `"Large"`、`"Medium"` 或 `"Small"` 的其中之一。 如果未指定，hello 預設值是`"Medium"`。
sampleRateInSeconds | （選擇性） hello 預設間隔原始 （未彙總） 的度量收集。 hello 最小支援的取樣率為 15 秒。 如果未指定，hello 預設值是`15`。

#### <a name="metrics"></a>metrics

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

元素 | 值
------- | -----
resourceId | 設定 toowhich hello VM 所屬 hello 的 Azure 資源管理員資源識別碼 hello VM 或 hello 虛擬機器規模。 這個設定必須也指定是否 hello 設定中使用任何 JsonBlob 接收。
scheduledTransferPeriod | 彙總度量資訊是 toobe hello 頻率計算，以及傳輸 tooAzure 度量，表示為是 8601 時間間隔。 最小傳輸週期 hello 為 60 秒，也就是 PT1M。 您必須指定至少一個 scheduledTransferPeriod。

範例的 hello hello performanceCounters 區段中指定的度量資訊會收集每 15 秒，或在 hello 明確定義 hello 計數器的取樣率。 如果多個 scheduledTransferPeriod 頻率出現 （hello 如範例所示），會個別計算每個彙總。

#### <a name="performancecounters"></a>performanceCounters

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

此選用小節控制 hello 度量收集。 未經處理的範例會針對每個彙總[scheduledTransferPeriod](#metrics) tooproduce 這些值：

* 平均值
* minimum
* maximum
* 上次收集的值
* 使用 toocompute hello 彙總的原始樣本的計數。

元素 | 值
------- | -----
sinks | （選擇性）以逗號分隔的清單名稱的接收器的 toowhich 年輕人傳送彙總的度量結果。 所有彙總的度量資訊會列出已發行的 tooeach 接收。 請參閱 [sinksConfig](#sinksconfig)。 範例： `"EHsink1, myjsonsink"`.
類型 | 識別 hello 標準的 hello 實際的提供者。
class | "Counter"，以及識別 hello hello 提供者的命名空間內的特定度量。
counter | 「 類別 」，以及識別 hello hello 提供者的命名空間內的特定度量。
counterSpecifier | 識別 hello hello Azure 度量命名空間內的特定度量。
condition | （選擇性）適用於選取 hello 物件 toowhich hello 度量的特定執行個體，或選取 hello 彙總，該物件的所有執行個體。 如需詳細資訊，請參閱 hello [ `builtin`度量定義](#metrics-supported-by-builtin)。
sampleRate | 是設定 hello 速率未經處理的範例，為此度量所收集的 8601 間隔。 如果未設定，hello 收集間隔設定 hello 值[sampleRateInSeconds](#ladcfg)。 hello 最短的受支援的取樣率為 15 秒 (PT15S)。
unit | 應為以下字串之一："Count"、"Bytes"、"Seconds"、"Percent"、"CountPerSecond"、"BytesPerSecond"、"Millisecond"。 定義 hello hello 度量單位。 Hello 收集資料的取用者期望 hello 收集的資料值 toomatch 此單元。 LAD 會忽略此欄位。
displayName | hello （在 hello hello 相關聯的區域，設定所指定的語言） 中的標籤 toobe 附加 toothis Azure 標準中的資料。 LAD 會忽略此欄位。

hello counterSpecifier 是自定的識別碼。 取用者的度量，例如 hello Azure 入口網站圖表和警示功能，會使用 counterSpecifier 做 hello 「 金鑰 」，以識別度量或標準的執行個體。 對於 `builtin` 計量，建議您使用開頭為 `/builtin/` 的 counterSpecifier 值。 如果您要收集度量資訊的特定執行個體，建議您附加 hello 識別碼 hello 執行個體 toohello counterSpecifier 值。 部分範例如下：

* `/builtin/Processor/PercentIdleTime` - 所有核心的平均閒置時間
* `/builtin/Disk/FreeSpace(/mnt)`-適用於 hello /mnt filesystem 可用空間
* `/builtin/Disk/FreeSpace` - 所有已掛接檔案系統的平均可用空間

年輕人都 hello Azure 入口網站預期 hello counterSpecifier 值 toomatch 任何模式。 應與您建構 counterSpecifier 值的方式一致。

當您指定`performanceCounters`，年輕人一律會 tooa 資料表寫入 Azure 儲存體中。 您可以擁有 hello 相同寫入 tooJSON blob 及/或事件中心的資料，但您無法停用儲存的資料 tooa 資料表。 所有執行個體的 hello 診斷延伸模組設定 toouse hello 相同的儲存體帳戶名稱與端點加入其標準和記錄檔 toohello 相同的資料表。 如果太多的 Vm 所撰寫的 toohello 相同資料表的資料分割，Azure 可以進行節流處理寫入 toothat 磁碟分割。 設定原因項目 toobe hello eventVolume 分散到 1 （小）、 （中），10 或 100 個 （大型） 不同的資料分割。 通常，"Medium"是足夠 tooensure 流量不會節流處理。 hello Azure 入口網站的 hello Azure 度量功能會使用這個資料表 tooproduce 圖形或 tootrigger 警示中的 hello 資料。 hello 資料表名稱是 hello 串連這些字串：

* `WADMetrics`
* hello"scheduledTransferPeriod"hello 彙總儲存在 hello 資料表中的值
* `P10DV2S`
* Hello 格式"YYYYMMDD 」，以變更每隔 10 天的日期

例如 `WADMetricsPT1HP10DV2S20170410` 與 `WADMetricsPT1MP10DV2S20170609`。

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

此選用小節控制記錄檔事件從 syslog hello 集合。 如果省略 hello 區段 syslog 事件不會擷取所有。

hello syslogEventConfiguration 集合具有一個項目感興趣的每個 syslog 設備。 如果 minSeverity 是 「 無 」 特定的功能，或該功能不會完全顯示 hello 項目中，會不擷取從該設備的任何事件。

元素 | 值
------- | -----
sinks | 以逗號分隔的清單名稱的接收器 toowhich 個別記錄事件發行。 比對中 syslogEventConfiguration hello 限制的所有記錄檔事件會列出已發行的 tooeach 接收。 範例："EHforsyslog"
facilityName | Syslog 設備名稱 (例如 "LOG\_USER" 或 "LOG\_LOCAL0")。 請參閱 「 功能 」 一節 hello hello [syslog man 頁面](http://man7.org/linux/man-pages/man3/syslog.3.html)hello 完整清單。
minSeverity | Syslog 嚴重性層級 (例如 "LOG\_ERR" 或 "LOG\_INFO")。 請參閱 「 層級 」 一節 hello hello [syslog man 頁面](http://man7.org/linux/man-pages/man3/syslog.3.html)hello 完整清單。 hello 擴充功能會擷取在傳送事件 toohello 設備或 hello 高於指定層級。

當您指定`syslogEvents`，年輕人一律會 tooa 資料表寫入 Azure 儲存體中。 您可以擁有 hello 相同寫入 tooJSON blob 及/或事件中心的資料，但您無法停用儲存的資料 tooa 資料表。 資料分割行為，這個資料表的 hello 是 hello 如所述相同`performanceCounters`。 hello 資料表名稱是 hello 串連這些字串：

* `LinuxSyslog`
* Hello 格式"YYYYMMDD 」，以變更每隔 10 天的日期

例如 `LinuxSyslog20170410` 與 `LinuxSyslog20170609`。

### <a name="perfcfg"></a>perfCfg

此選擇性區段會控制任意 [OMI](https://github.com/Microsoft/omi) 查詢的執行。

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

元素 | 值
------- | -----
namespace | （選擇性） hello OMI 命名空間中的 hello 應對其執行查詢。 如果未指定，hello 預設值是"root/scx"，藉由 hello [System Center 跨平台提供者](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation)。
query | hello OMI 查詢 toobe 執行。
資料表 | （選擇性） hello Azure 儲存體資料表，在 指定儲存體帳戶的 hello (請參閱[保護設定](#protected-settings))。
frequency | （選擇性） hello hello 查詢的執行之間的秒數。 預設值為 300 秒 (5 分鐘)；最小值為 15 秒。
sinks | （選擇性）應經過發佈之其他接收 toowhich 原始範例度量結果的名稱以逗號分隔清單。 Hello 延伸模組或 Azure 度量，會不計算任何彙總這些未經處理的範例。

必須指定 "table" 或 "sinks"，或兩者。

### <a name="filelogs"></a>fileLogs

控制項 hello 擷取的記錄檔。 年輕人擷取新的文字行，當它們被寫入 toohello 檔案，並將它們寫入 tootable 資料列和/或任何指定的接收 （JsonBlob 或 EventHub）。

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

元素 | 值
------- | -----
file | 監看 hello 記錄檔案 toobe hello 完整路徑名稱，並擷取。 hello pathname 必須單一檔案名稱;它不能命名目錄，或包含萬用字元。
資料表 | hello 指定儲存體中的 （選擇性） hello Azure 儲存體資料表 」 帳戶 （如指定 hello 受保護的組態中），到哪一個新行 hello"tail"hello 檔案的寫入。
sinks | （選擇性）傳送其他接收 toowhich 記錄行的名稱的逗號分隔清單。

必須指定 "table" 或 "sinks"，或兩者。

## <a name="metrics-supported-by-hello-builtin-provider"></a>Hello 內建提供者所支援的度量

hello builtin 度量的提供者會為資料來源的度量最有趣 tooa 組廣泛的使用者。 這些計量分成五大類別：

* 處理器
* 記憶體
* 網路
* 檔案系統
* 磁碟

### <a name="builtin-metrics-for-hello-processor-class"></a>hello 處理器類別的內建度量

hello 度量的處理器類別提供 hello VM 中的處理器使用量的相關資訊。 彙總百分比，hello 結果會是 hello 平均所有 cpu。 在兩個核心 VM，如果其中一個核心是 100%忙碌中，其他 hello 100%閒置，hello 報告 PercentIdleTime 會是 50。 如果每個核心已忙碌的 50 %hello 相同 hello 週期，報告結果也會是 50。 在四個核心的 VM，和一個核心的 100%忙碌和 hello 閒置，其他人 hello 報告 PercentIdleTime 是 75。

counter | 意義
------- | -------
PercentIdleTime | Hello 彙總視窗處理器在執行 hello 核心閒置迴圈期間的時間百分比
PercentProcessorTime | 執行非閒置執行緒的時間百分比
PercentIOWaitTime | IO 作業 toocomplete 正在等候的時間百分比
PercentInterruptTime | 執行硬體/軟體中斷與 DPC (延遲的程序呼叫) 的時間百分比
PercentUserTime | Hello 彙總間隔期間的非閒置時間，hello 時間百分比在 使用者以一般優先權更
PercentNiceTime | 非閒置的時間，hello 百分比降低 (nice) 的優先順序
PercentPrivilegedTime | 非閒置的時間，顯示花費在特殊權限 （核心） 模式的 hello 百分比

hello 前四個計數器的加總應該 too100%。 hello 最後三個計數器也總和 too100%;它們細分 PercentProcessorTime、 PercentIOWaitTime，和 PercentInterruptTime hello 總和。

tooobtain 單一度量彙總所有的處理器之間設定`"condition": "IsAggregate=TRUE"`。 tooobtain 特定處理器的度量，例如 hello 第二個邏輯處理器，四個核心的 VM，設定`"condition": "Name=\\"1\\""`。 邏輯處理器數目是在 hello 範圍`[0..n-1]`。

### <a name="builtin-metrics-for-hello-memory-class"></a>hello 記憶體類別的內建度量

hello 的度量資訊的記憶體類別提供有關記憶體使用率、 分頁和交換資訊。

counter | 意義
------- | -------
AvailableMemory | 可用的實體記憶體 (MiB)
PercentAvailableMemory | 以總記憶體百分比表示的可用實體記憶體
UsedMemory | 使用中實體記憶體 (MiB)
PercentUsedMemory | 以總記憶體百分比表示的使用中實體記憶體
PagesPerSec | 總分頁數 (讀取/寫入)
PagesReadPerSec | 從備份存放區讀取的分頁數 (分頁檔、程式檔、對應檔等)
PagesWrittenPerSec | 寫入 toobacking 儲存 （分頁檔、 對應的檔）
AvailableSwap | 未使用的交換空間 (MiB)
PercentAvailableSwap | 以總交換空間百分比表示的未使用交換空間
UsedSwap | 已使用交換空間 (MiB)
PercentUsedSwap | 以總交換空間表示的使用中交換空間

此計量類別只有單一執行個體。 hello 「 條件 」 屬性有任何有用的設定，且應該省略。

### <a name="builtin-metrics-for-hello-network-class"></a>hello 網路類別的內建度量

hello 網路類別的度量會提供個別的網路介面上開機後經過網路活動的相關資訊。 LAD 不會公開頻寬計量，該計量可從主機計量中取出。

counter | 意義
------- | -------
BytesTransmitted | 自開機後傳送的位元組總數
BytesReceived | 自開機後收到的位元組總數
BytesTotal | 自開機後收傳送或收到的位元組總數
PacketsTransmitted | 自開機後傳送的封包總數
PacketsReceived | 自開機後收到的封包總數
TotalRxErrors | 自開機後接收的錯誤數
TotalTxErrors | 自開機後傳輸的錯誤數
TotalCollisions | 開機後經過回報 hello 網路連接埠衝突的數目

 雖然此類別已執行個體化，但 LAD 不支援擷取從所有網路裝置彙總的網路計量。 針對特定的介面，例如 eth0，tooobtain hello 度量設定`"condition": "InstanceID=\\"eth0\\""`。

### <a name="builtin-metrics-for-hello-filesystem-class"></a>hello Filesystem 類別的內建度量

hello 的度量資訊的檔案系統類別提供的檔案系統使用量的相關資訊。 因為它們可以顯示的 tooan 一般使用者 （不是根目錄），則會報告絕對值和百分比值。

counter | 意義
------- | -------
FreeSpace | 可用磁碟空間 (位元組)
UsedSpace | 已使用的磁碟空間 (位元組)
PercentFreeSpace | 可用空間百分比
PercentUsedSpace | 已使用的空間百分比
PercentFreeInodes | 未使用 inode 的百分比
PercentUsedInodes | 所有檔案系統中已配置 (使用中) inode 總和的百分比
BytesReadPerSecond | 每秒讀取的位元組數
BytesWrittenPerSecond | 每秒寫入的位元組數
每秒位元組 | 每秒讀取或寫入的位元組數
ReadsPerSecond | 每秒的讀取作業數
WritesPerSecond | 每秒的寫入作業數
TransfersPerSecond | 每秒的讀取或寫入作業數

可透過設定 `"condition": "IsAggregate=True"` 取得的所有檔案系統彙總值。 可透過設定 `"condition": 'Name="/mnt"'` 取得的特定已掛接檔案系統 (例如 "/mnt") 的值。

### <a name="builtin-metrics-for-hello-disk-class"></a>hello 磁碟類別的內建度量

hello 磁碟類別的度量會提供磁碟裝置使用量的相關資訊。 這些統計資料套用 toohello 整個磁碟機。 如果裝置上有多個檔案系統，該裝置 hello 計數器的有效地跨所有的彙總。

counter | 意義
------- | -------
ReadsPerSecond | 每秒的讀取作業數
WritesPerSecond | 每秒的寫入作業數
TransfersPerSecond | 每秒的總作業數
AverageReadTime | 每個讀取作業的平均秒數
AverageWriteTime | 每個寫入作業的平均秒數
AverageTransferTime | 每個作業的平均秒數
AverageDiskQueueLength | 已排入佇列的磁碟作業平均數
ReadBytesPerSecond | 每秒讀取的位元組數
WriteBytesPerSecond | 每秒寫入的位元組數
每秒位元組 | 每秒讀取或寫入的位元組數

可透過設定 `"condition": "IsAggregate=True"` 取得的所有磁碟彙總值。 設定特定裝置 (例如，開發人員/sdf1)，tooget 資訊`"condition": "Name=\\"/dev/sdf1\\""`。

## <a name="installing-and-configuring-lad-30-via-cli"></a>透過 CLI 安裝與設定 LAD 3.0

假設您受保護的設定 hello 檔案 privateconfig.json 的檔案中，您的公用組態資訊是位在 PublicConfig.json，執行下列命令：

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

hello 命令假設您使用的 hello Azure CLI hello Azure 資源管理模式 (arm)。 tooconfigure 年輕人的傳統部署模型 (ASM) Vm，請切換太"asm 」 模式 (`azure config mode asm`)，並省略 hello 命令中的 hello 資源群組名稱。 如需詳細資訊，請參閱 hello[跨平台 CLI 文件](https://docs.microsoft.com/azure/xplat-cli-connect)。

## <a name="an-example-lad-30-configuration"></a>範例 LAD 3.0 組態

根據 hello 之前定義，這裡的部分說明範例年輕人 3.0 延伸模組組態。 tooapply 範例 tooyour 本例中，您應該使用您自己的儲存體帳戶名稱、 帳戶 SAS 權杖，以及 EventHubs SAS token。

### <a name="privateconfigjson"></a>PrivateConfig.json

這些私用設定會設定：

* 儲存體帳戶
* 相符的帳戶 SAS 權杖
* 數個接收 (含 SAS 權杖的 JsonBlob 或 EventHubs)

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

這些公用設定會造成 LAD：

* 上傳處理器時間百分比和使用磁碟空間度量 toohello`WADMetrics*`資料表
* 上傳訊息從 syslog 設備 「 使用者 」 和嚴重性"info"toohello`LinuxSyslog*`資料表
* 上傳原始 OMI 查詢結果 （PercentProcessorTime 和 PercentIdleTime） toohello 名為`LinuxCPU`資料表
* 上傳檔案中的 附加的行`/var/log/myladtestlog`toohello`MyLadTestLog`資料表

在每個案例中，也會將資料上傳至：

* Azure Blob 儲存體 （容器名稱為 hello JsonBlob 接收中所定義）
* EventHubs 端點 （如 hello EventHubs 接收中指定）

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

hello`resourceId`在 hello 組態必須符合的 hello VM 或 hello 虛擬機器規模集。

* Azure 平台度量圖表和警示知道 hello resourceId 的 hello 您正在使用的 VM。 預期 toofind hello 資料的 VM 使用 hello resourceId hello 查閱索引鍵。
* 如果您使用 Azure 自動調整規模，hello 自動調整規模設定中的 hello resourceId 必須符合 hello resourceId 年輕人所使用。
* hello resourceId 是內建的 JsonBlobs 年輕人所撰寫的 hello 名稱。

## <a name="view-your-data"></a>檢視資料

使用 Azure 入口網站 tooview hello 的效能資料，或設定警示：

![image](./media/diagnostic-extension/graph_metrics.png)

hello`performanceCounters`資料一律儲存在 Azure 儲存體資料表。 Azure 儲存體 API 適用於許多語言與平台。

傳送 tooJsonBlob 接收的資料會儲存在名為 hello 中的 hello 儲存體帳戶中的 blob[保護設定](#protected-settings)。 您可以使用 使用任何 Azure Blob 儲存體 Api hello blob 資料。

此外，您可以使用這些 UI 工具 tooaccess hello 資料在 Azure 儲存體：

* Visual Studio 伺服器總管。
* [Microsoft Azure 儲存體總管](https://azurestorageexplorer.codeplex.com/ "Azure 儲存體總管")。

Microsoft Azure 儲存體總管工作階段的此快照顯示 hello 產生 Azure 儲存體資料表和容器從測試 VM 上的正確設定年輕人 3.0 延伸模組。 hello 映像不完全符合 hello[範例年輕人 3.0 組態](#an-example-lad-30-configuration)。

![image](./media/diagnostic-extension/stg_explorer.png)

請參閱相關的 hello [EventHubs 文件](../../event-hubs/event-hubs-what-is-event-hubs.md)toolearn tooconsume 訊息發佈 tooan EventHubs 端點的方式。

## <a name="next-steps"></a>後續步驟

* 建立度量的警示[Azure 監視器](../../monitoring-and-diagnostics/insights-alerts-portal.md)hello 度量收集。
* 為您的計量建立[監視圖表](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。
* 了解如何太[建立虛擬機器規模集](/azure/virtual-machines/linux/tutorial-create-vmss)使用度量的 toocontrol 自動調整。
