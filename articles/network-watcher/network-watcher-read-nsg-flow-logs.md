---
title: "aaaRead NSG 流程記錄檔 |Microsoft 文件"
description: "本文將說明 tooparse NSG 流程記錄的方式"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: b4f0f64639c7b2a6b4db50e54d15056bfd809e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="read-nsg-flow-logs"></a>讀取 NSG 流量記錄

了解 tooread NSG 流程與 PowerShell 所記錄的項目。

NSG 流量記錄會以[區塊 Blob](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs) 的形式儲存在儲存體帳戶中。 區塊 Blob 是由較小的區塊組成。 每個記錄都是於每小時產生的個別區塊 Blob。 新的記錄檔會產生每個小時，hello 記錄檔會更新與新的項目與 hello 最新的資料每隔幾分鐘。 在本文中您學習如何 tooread 部份 hello 流程記錄檔。

## <a name="scenario"></a>案例

Hello 遵照案例，您必須儲存在儲存體帳戶中的範例資料流程記錄檔。 我們逐步執行方式可以選擇性地讀取 hello NSG 流程記錄中的最新事件。 在本文中，我們將使用 PowerShell，不過，hello hello 文章中討論的概念不是有限的 toohello 程式設計語言，並適用於 tooall hello Azure 儲存體 Api 所支援的語言

## <a name="setup"></a>設定

開始之前，您必須在帳戶中的一或多個網路安全性群組上，啟用網路安全性群組流程記錄。 如需有關啟用網路安全性指示傳送記錄檔，請參閱下列文章 toohello:[網路安全性群組的簡介 tooflow 記錄](network-watcher-nsg-flow-logging-overview.md)。

## <a name="retrieve-hello-block-list"></a>擷取 hello 封鎖清單

hello 遵循 hello 變數的 PowerShell 設定所需 tooquery hello NSG 流程記錄 blob 和清單的 hello 區塊內 hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3)區塊 blob。 更新您的環境的 hello 指令碼 toocontain 正確值。

```powershell
# hello SubscriptionID toouse
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains hello Network Security Group
$resourceGroupName = "<resourceGroupName>"

# hello name of hello Network Security Group
$nsgName = "NSGName"

# hello storage account name that contains hello NSG logs
$storageAccountName = "<storageAccountName>" 

# hello date and time for hello log toobe queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve hello primary storage account key tooaccess hello NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context toobe used tooquery hello logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of hello blob that contains hello NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets hello storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets hello block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from hello storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores hello block list in a variable from hello block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

hello`$blockList`變數則會傳回一份 hello 區塊 hello blob 中。 每個區塊 Blob 都至少包含兩個區塊。  hello 第一個區塊長度為`21`個位元組，此區塊包含 hello 括 hello json 記錄檔。 hello 其他區塊 hello 右括號，長度為`9`位元組。  如您所見 hello 遵循範例記錄檔有七個項目中，每個正在的個別項目。 Hello 記錄檔中的所有新項目會加入 toohello 前 hello 最後一個區塊的結尾。

```
Name                                         Length Committed
----                                         ------ ---------
ZDk5MTk5N2FkNGE0MmY5MTk5ZWViYjA0YmZhODRhYzY=     21      True
NzQxNDA5MTRhNDUzMGI2M2Y1MDMyOWZlN2QwNDZiYzQ=   2685      True
ODdjM2UyMWY3NzFhZTU3MmVlMmU5MDNlOWEwNWE3YWY=   2586      True
ZDU2MjA3OGQ2ZDU3MjczMWQ4MTRmYWNhYjAzOGJkMTg=   2688      True
ZmM3ZWJjMGQ0ZDA1ODJlOWMyODhlOWE3MDI1MGJhMTc=   2775      True
ZGVkYTc4MzQzNjEyMzlmZWE5MmRiNjc1OWE5OTc0OTQ=   2676      True
ZmY2MjUzYTIwYWIyOGU1OTA2ZDY1OWYzNmY2NmU4ZTY=   2777      True
Mzk1YzQwM2U0ZWY1ZDRhOWFlMTNhYjQ3OGVhYmUzNjk=   2675      True
ZjAyZTliYWE3OTI1YWZmYjFmMWI0MjJhNzMxZTI4MDM=      9      True
```

## <a name="read-hello-block-blob"></a>讀取 hello 區塊 blob

接下來我們需要 tooread hello`$blocklist`變數 tooretrieve hello 資料。 在此範例中，我們逐一 hello 封鎖清單，從每個區塊讀取 hello 位元組和這些劇本在陣列中。 我們使用 hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_)方法 tooretrieve hello 資料。

```powershell
# Set hello size of hello byte array toohello largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array toostore values in
$valuearray = @()

# Define hello starting index tootrack hello current block being read
$index = 0

# Loop through each block in hello block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object toostory hello bytes from hello block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download hello data into hello ByteArray, starting with hello current index, for hello number of bytes in hello current block. Index is increased by 3 when reading tooremove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment hello index by adding hello current block length toohello previous index
$index = $index + $blockList[$i].Length

# Retrieve hello string from hello byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add hello log entry toohello value array
$valuearray += $value
}
```

現在 hello`$valuearray`陣列包含的每個區塊的 hello 字串值。 tooverify hello 項目，get hello 第二個 toohello 最後一個值從執行 hello 陣列`$valuearray[$valuearray.Length-2]`。 我們不想 hello 最後一個值是只 hello 右括號。

此值的 hello 結果會顯示在下列範例中的 hello:

```json
        {
             "time": "2017-06-16T20:59:43.7340000Z",
             "systemId": "5f4d02d3-a7d0-4ed4-9ce8-c0ae9377951c",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/CONTOSONSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_AllowInternetOutBound","flows":[{"mac":"000D3A18077E","flowTuples":["1497646722,10.0.0.4,168.62.32.14,44904,443,T,O,A","1497646722,10.0.0.4,52.240.48.24,45218,443,T,O,A","1497646725,10.
0.0.4,168.62.32.14,44910,443,T,O,A","1497646725,10.0.0.4,52.240.48.24,45224,443,T,O,A","1497646728,10.0.0.4,168.62.32.14,44916,443,T,O,A","1497646728,10.0.0.4,52.240.48.24,45230,443,T,O,A","1497646732,10.0.0.4,168.62.32.14,44922,443,T,O,A","14976
46732,10.0.0.4,52.240.48.24,45236,443,T,O,A","1497646735,10.0.0.4,168.62.32.14,44928,443,T,O,A","1497646735,10.0.0.4,52.240.48.24,45242,443,T,O,A","1497646738,10.0.0.4,168.62.32.14,44934,443,T,O,A","1497646738,10.0.0.4,52.240.48.24,45248,443,T,O,
A","1497646742,10.0.0.4,168.62.32.14,44942,443,T,O,A","1497646742,10.0.0.4,52.240.48.24,45256,443,T,O,A","1497646745,10.0.0.4,168.62.32.14,44948,443,T,O,A","1497646745,10.0.0.4,52.240.48.24,45262,443,T,O,A","1497646749,10.0.0.4,168.62.32.14,44954
,443,T,O,A","1497646749,10.0.0.4,52.240.48.24,45268,443,T,O,A","1497646753,10.0.0.4,168.62.32.14,44960,443,T,O,A","1497646753,10.0.0.4,52.240.48.24,45274,443,T,O,A","1497646756,10.0.0.4,168.62.32.14,44966,443,T,O,A","1497646756,10.0.0.4,52.240.48
.24,45280,443,T,O,A","1497646759,10.0.0.4,168.62.32.14,44972,443,T,O,A","1497646759,10.0.0.4,52.240.48.24,45286,443,T,O,A","1497646763,10.0.0.4,168.62.32.14,44978,443,T,O,A","1497646763,10.0.0.4,52.240.48.24,45292,443,T,O,A","1497646766,10.0.0.4,
168.62.32.14,44984,443,T,O,A","1497646766,10.0.0.4,52.240.48.24,45298,443,T,O,A","1497646769,10.0.0.4,168.62.32.14,44990,443,T,O,A","1497646769,10.0.0.4,52.240.48.24,45304,443,T,O,A","1497646773,10.0.0.4,168.62.32.14,44996,443,T,O,A","1497646773,
10.0.0.4,52.240.48.24,45310,443,T,O,A","1497646776,10.0.0.4,168.62.32.14,45002,443,T,O,A","1497646776,10.0.0.4,52.240.48.24,45316,443,T,O,A","1497646779,10.0.0.4,168.62.32.14,45008,443,T,O,A","1497646779,10.0.0.4,52.240.48.24,45322,443,T,O,A"]}]}
,{"rule":"DefaultRule_DenyAllInBound","flows":[]},{"rule":"UserRule_ssh-rule","flows":[]},{"rule":"UserRule_web-rule","flows":[{"mac":"000D3A18077E","flowTuples":["1497646738,13.82.225.93,10.0.0.4,1180,80,T,I,A","1497646750,13.82.225.93,10.0.0.4,
1184,80,T,I,A","1497646768,13.82.225.93,10.0.0.4,1181,80,T,I,A","1497646780,13.82.225.93,10.0.0.4,1336,80,T,I,A"]}]}]}
        }
```

此案例中是 tooread NSG 中的項目而不需要 tooparse hello 整個記錄檔所傳送的記錄檔的範例。 您可以閱讀 hello 記錄檔中的新項目，因為寫法是使用 hello 區塊識別碼，或藉由追蹤 hello 長度儲存在 hello 區塊 blob 的區塊。 這可讓您 tooread 只有 hello 新項目。


## <a name="next-steps"></a>後續步驟

請瀏覽[Azure 網路監看員 NSG 流程記錄檔使用開放原始碼工具以視覺化方式檢視](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)深入了解其他方式 tooview NSG toolearn 流程記錄檔。

有關儲存體 blob 的詳細資訊請造訪的 toolearn: [Azure 函式的 Blob 儲存體繫結](../azure-functions/functions-bindings-storage-blob.md)
