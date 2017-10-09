---
title: "aaaAdd 監視與診斷 tooan Azure 虛擬機器 |Microsoft 文件"
description: "使用 Azure 診斷擴充功能的 Azure 資源管理員範本 toocreate 新的 Windows 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>使用 Windows VM 和 Azure Resource Manager 範本的監視和診斷
hello Azure 診斷擴充功能提供 hello 監視和診斷功能，在 Windows Azure 虛擬機器。 您可以啟用 hello 虛擬機器上的這些功能包括 hello 副檔名 hello azure 資源管理員範本的一部分。 請參閱 [使用 VM 延伸模組編寫 Azure 資源管理員範本](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) ，以取得將任何延伸模組納入為虛擬機器範本一部分的詳細資訊。 本文說明如何新增 hello Azure 診斷擴充功能 tooa windows 虛擬機器範本。  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>新增 hello Azure 診斷擴充功能 toohello VM 資源定義
tooenable hello 診斷擴充功能在 Windows 虛擬機器您為 VM 資源中需要 tooadd hello 延伸 hello 資源管理員範本。

簡單資源管理員的基礎的虛擬機器加入 hello 延伸模組組態 toohello*資源*hello 虛擬機器的陣列： 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


另一個常見慣例是在 hello 範本，而不是定義在 hello 虛擬機器的資源 節點下的 hello 根資源節點加入 hello 延伸模組組態。 透過這種方式，您有 tooexplicitly hello 延伸模組和 hello 虛擬機器之間的階層式關聯性指定以 hello*名稱*和*類型*值。 例如： 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

hello 延伸永遠都會與 hello 虛擬機器相關聯，您可以直接定義 hello 虛擬機器的資源 節點下直接或定義在 hello 基底層級並使用 hello 階層式命名慣例 tooassociate 它以 hello 虛擬機器。

針對虛擬機器擴展集 hello 延伸模組組態會指定在 hello *extensionProfile*屬性 hello *VirtualMachineProfile*。

hello*發行者*屬性與 hello 值**Microsoft.Azure.Diagnostics**和 hello*類型*屬性 hello 值是**IaaSDiagnostics**唯一識別 hello Azure 診斷擴充功能。

hello 值 hello*名稱*屬性可以是使用的 toorefer toohello 延伸 hello 資源群組中。 將它設定特別太**Microsoft.Insights.VMDiagnosticsSettings**會啟用它 toobe hello Azure 入口網站確保 hello 監視圖表都會顯示正確在 hello Azure 入口網站，輕鬆地識別。

hello *typeHandlerVersion*指定 hello 版本 hello 延伸模組，您想要 toouse。 設定*autoUpgradeMinorVersion*太次要版本**true**可確保您會收到 hello 最新次要版本所提供的 hello 延伸模組。 強烈建議您一律將*autoUpgradeMinorVersion* tooalways 是**true**以便讓您一律取得 toouse hello 最新可用的診斷擴充功能與所有 hello 新功能和 bug修正程式。 

hello*設定*元素包含可設定及讀取來自 hello 擴充功能 （有時參照的 tooas 公用組態） 的 hello 擴充功能的組態屬性。 hello *xmlcfg*屬性包含 xml 架構組態 hello 診斷記錄檔、 效能計數器將 hello 診斷代理程式所收集的等等。 請參閱[診斷組態結構描述](https://msdn.microsoft.com/library/azure/dn782207.aspx)如需有關 hello xml 結構描述本身。 常見的作法是 toostore hello 實際的 xml 組態，因為變數在 hello Azure Resource Manager 範本，然後串連和 base64 編碼它們 tooset hello 值*xmlcfg*。 請參閱 hello 章節[診斷組態變數](#diagnostics-configuration-variables)toounderstand 深入了解如何 toostore hello 變數中的 xml。 hello *storageAccount*屬性會指定將會傳送 hello hello 儲存體帳戶 toowhich 診斷資料的名稱。 

hello 中的屬性*protectedSettings* （有時參照的 tooas 私用組態） 可以設定，但無法讀取之後設定。 hello 唯寫性質*protectedSettings*方便來儲存機密資料，例如 hello 儲存體帳戶金鑰寫入 hello 診斷資料。    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>將診斷儲存體帳戶指定為參數
hello 診斷延伸模組 json 片段上述假設兩個參數*existingdiagnosticsStorageAccountName*和*existingdiagnosticsStorageResourceGroup* toospecify hello 診斷儲存診斷資料的儲存體帳戶。 Hello 診斷儲存體帳戶指定為參數可讓您輕鬆 toochange hello 診斷儲存體帳戶跨不同的環境，例如您可能會想 toouse 不同診斷儲存體帳戶進行測試和不同的另一個用於您生產環境部署。  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

它是最佳作法 toospecify 診斷儲存體帳戶位於不同的資源群組的 hello hello 虛擬機器的資源群組。 資源群組可視為 toobe 部署單位具有自己的存留期、 虛擬機器部署及重新部署新的組態更新進行會 tooit，但是您可能想將 hello 診斷資料儲存在 hello toocontinue 相同儲存體帳戶所有這些虛擬機器部署。 具有 hello 儲存體帳戶中不同的資源啟用 hello 儲存體帳戶 tooaccept 資料從各種不同的虛擬機器部署，讓您輕鬆 tootroubleshoot 跨問題 hello 各種版本。

> [!NOTE]
> 如果您從 Visual Studio 可能會設定 hello 預設儲存體帳戶中建立 windows 虛擬機器範本 toouse hello hello 虛擬機器 VHD 會上傳所在的相同儲存體帳戶。 這是 hello VM toosimplify 初始設定。 您應重新考量因素 hello 範本 toouse 可以做為參數中傳遞不同的儲存體帳戶。 
> 
> 

## <a name="diagnostics-configuration-variables"></a>診斷組態變數
hello 診斷延伸模組 json 片段上述定義*accountid*變數 toosimplify 取得 hello hello 診斷儲存體的儲存體帳戶金鑰：   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


hello *xmlcfg* hello 診斷延伸模組屬性定義使用串連在一起的多個變數。 hello 這些變數的值是 xml 格式，所以它們需要 toobe 逸出正確地設定 hello json 的變數時。

hello 以下說明會收集標準系統層級的效能計數器，以及某些 windows 事件記錄檔和診斷基礎結構記錄檔的 hello 診斷組態 xml。 尚未逸出和正確格式化，以便 hello 組態可以直接貼到您的範本 hello 變數區段。 請參閱 hello[診斷組態結構描述](https://msdn.microsoft.com/library/azure/dn782207.aspx)更人類可讀取 hello 組態 xml 的範例。

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

hello 度量定義 hello 上述組態中的 xml 節點是重要的設定項目，因為它會定義先前已在中的 hello xml hello 效能計數器的定義方式*PerformanceCounter*節點將會彙總及儲存。 

> [!IMPORTANT]
> 這些度量磁碟機 hello 監視圖表和 hello Azure 入口網站中的警示。  hello**度量**節點以 hello *resourceID*和**MetricAggregation**必須包含在 VM 的 hello 診斷組態中，如果您想 toosee hello VM在 hello Azure 入口網站中的監視資料。 
> 
> 

hello 如下的度量定義 hello xml 範例： 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

hello *resourceID*屬性可唯一識別您的訂用帳戶中的 hello 虛擬機器。 請確定 toouse hello subscription() 和 resourceGroup() 函式使 hello 範本會自動更新這些值根據您要部署的 hello 訂用帳戶和資源群組。

如果您要在迴圈中建立多個虛擬機器，則您必須 toopopulate hello *resourceID* copyIndex() 函式 toocorrectly 值區分每個個別的 VM。 hello *xmlCfg*值可以是更新的 toosupport 這，如下所示：  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

hello MetricAggregation 值*PT1H*和*PT1M*表示彙總一分鐘內，一小時的彙總。

## <a name="wadmetrics-tables-in-storage"></a>儲存體中的 WADMetrics 資料表
上述的 hello 度量組態會在診斷儲存體帳戶中產生資料表以 hello 遵循命名慣例：

* **WADMetrics** ：所有 WADMetrics 資料表的標準前置詞
* **PT1H**或**PT1M** ： 表示該 hello 資料表包含超過 1 小時或 1 分鐘的彙總資料
* **P10D** ： 表示 hello 資料表將包含 10 天從 hello 資料表開始收集資料的資料
* **V2S** ：字串常數
* **yyyymmdd** : hello 的 hello 資料表開始收集資料的日期

範例： *WADMetricsPT1HP10DV2S20151108* 將包含從 2015 年 11 月 11 日開始 10 天內，所有超過一小時的彙總計量資料    

每個 WADMetrics 資料表將會包含下列資料行的 hello:

* **PartitionKey**: hello partitionkey 建構根據 hello *resourceID*值 toouniquely 識別 hello VM 資源。 例如：002Fsubscriptions:<subscriptionID>:002FresourceGroups:002F<ResourceGroupName>:002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** ： 如下所示 hello 格式<Descending time tick>:<Performance Counter Name>。 hello 遞減時間刻度計算是減號 hello hello 彙總期間的 hello 開始時間的最大時間刻度。 例如 如果 hello 取樣期間啟動於 2015 年 11 月 10 日 00:00Hrs UTC 然後 hello 計算就是： DateTime.MaxValue.Ticks-(新 DateTime(2015,11,10,0,0,0,DateTimeKind.Utc)。刻度為單位）。 針對 hello 記憶體可用位元組數效能計數器 hello 資料列索引鍵看起來像： 2519551871999999999__:005CMemory:005CAvailable:0020 位元組
* **CounterName** : hello hello 效能計數器名稱。 這符合 hello *counterSpecifier* hello xml 組態中定義。
* **最大**: hello 彙總期間 hello hello 效能計數器的最大值。
* **最小**: hello 彙總期間 hello hello 效能計數器的最小值。
* **總**: hello 彙總期間報告 hello 總和 hello 效能計數器的所有值。
* **計數**: hello 效能計數器回報 hello 值總數。
* **平均**: hello 彙總期間 hello hello 效能計數器的平均值 （總計/計數） 值。

## <a name="next-steps"></a>後續步驟
* 如需具有診斷擴充功能之 Windows 虛擬機器的完整範例範本，請參閱 [201-vm-monitoring-diagnostics-extension](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Hello 資源管理員範本使用部署[Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或[Azure 命令列](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* 深入了解 [編寫 Azure 資源管理員範本](../../resource-group-authoring-templates.md)

