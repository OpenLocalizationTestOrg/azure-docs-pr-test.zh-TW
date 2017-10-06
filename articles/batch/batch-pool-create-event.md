---
title: "aaa\"Azure Batch 集區建立事件 |Microsoft 文件 」"
description: "Batch 集區建立事件的參考。"
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>集區建立事件

 一旦集區建立完成，就會發出此事件。 hello hello 記錄檔的內容會公開 hello 集區相關的一般資訊。 請注意是否 hello 目標 hello 集區大小大於 0 的計算節點，集區調整大小的開始事件會遵循此事件後面。

 hello 下列範例顯示 hello 主體的集區建立集區使用 hello CloudServiceConfiguration 屬性所建立的事件。

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|元素|類型|注意事項|
|-------------|----------|-----------|
|id|String|hello hello 集區識別碼。|
|displayName|String|hello 顯示 hello 集區的名稱。|
|vmSize|String|hello hello hello 集區中的虛擬機器大小。 集區中的所有虛擬機器都都 hello 相同的大小。 <br/><br/> 如需雲端服務集區 (使用 cloudServiceConfiguration 建立的集區) 的虛擬機器可用大小相關資訊，請參閱[雲端服務的大小](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/)。 Batch 支援 `ExtraSmall` 以外的所有雲端服務 VM 大小。<br/><br/> 如需可用的 VM 使用映像從 hello 虛擬機器 Marketplace （集區建立 virtualMachineConfiguration） 集區的大小請參閱[虛擬機器的大小](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/)(Linux) 或[的大小虛擬機器](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/)(Windows)。 除了 `STANDARD_A0` 和進階儲存體的大小 (`STANDARD_GS`、`STANDARD_DS` 和 `STANDARD_DSV2` 系列) 以外，Batch 支援所有的 Azure VM 大小。|
|[cloudServiceConfiguration](#bk_csconf)|複雜類型|hello 雲端 hello 集區的服務組態。|
|[virtualMachineConfiguration](#bk_vmconf)|複雜類型|hello hello 集區的虛擬機器組態。|
|[networkConfiguration](#bk_netconf)|複雜類型|hello hello 集區的網路組態。|
|resizeTimeout|時間|指定給 hello 最後一個調整大小作業 hello 集區上的計算節點 toohello 集區配置的 hello 逾時。  (hello 初始時 hello 建立集區計數大小調整為調整大小。)|
|targetDedicated|Int32|hello hello 集區要求的運算節點數目。|
|enableAutoScale|Bool|指定是否 hello 集區大小會自動調整一段時間。|
|enableInterNodeCommunication|Bool|指定 hello 集區是否已設定的節點之間直接進行通訊。|
|isAutoPool|Bool|指定是否已透過作業的 AutoPool 機制建立 hello 集區。|
|maxTasksPerNode|Int32|hello 的 hello 集區內單一計算節點可同時執行的工作數上限。|
|vmFillType|String|定義 hello 批次服務如何散發 hello 集區中的計算節點之間的工作。 有效值為 Spread 或 Pack。|

###  <a name="bk_csconf"></a> cloudServiceConfiguration

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|osFamily|String|hello Azure 客體作業系統系列 toobe hello hello 集區中的虛擬機器上安裝。<br /><br /> 可能的值包括：<br /><br /> **2** – OS 系列 2 相等 tooWindows Server 2008 R2 SP1。<br /><br /> **3** – 作業系統系列 3 相等 tooWindows Server 2012。<br /><br /> **4** – 作業系統系列 4，相當 tooWindows Server 2012 R2。<br /><br /> 如需詳細資訊，請參閱[客體 ​OS 發佈新聞](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases)。|
|targetOSVersion|String|hello Azure 客體作業系統版本 toobe hello hello 集區中的虛擬機器上安裝。<br /><br /> hello 預設值是 **\*** 指定 hello 最新作業系統版本指定系列。<br /><br /> 如需其他允許的值，請參閱[客體 OS 發佈新聞](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases)。|

###  <a name="bk_vmconf"></a> virtualMachineConfiguration

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|[imageReference](#bk_imgref)|複雜類型|指定 hello 平台或 Marketplace 映像 toouse 相關資訊。|
|nodeAgentSKUId|String|hello hello 批次節點佈建 hello 計算節點上的代理程式 」 的 SKU。|
|[windowsConfiguration](#bk_winconf)|複雜類型|指定 hello 虛擬機器上的 Windows 作業系統設定。 這個屬性不能指定 hello imageReference 是否會參考 Linux 作業系統映像。|

###  <a name="bk_imgref"></a> imageReference

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|publisher|String|hello hello 映像的發行者。|
|提供項目|String|hello 提供項目的 hello 映像。|
|sku|String|hello hello 映像的 SKU。|
|版本|String|hello hello 映像的版本。|

###  <a name="bk_winconf"></a> windowsConfiguration

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|enableAutomaticUpdates|Boolean|指出是否啟用自動更新的 hello 虛擬機器。 如果未指定這個屬性，hello 預設值為 true。|

###  <a name="bk_netconf"></a> networkConfiguration

|元素名稱|類型|注意事項|
|------------------|--------------|----------|
|subnetId|String|指定 hello hello 建立哪個 hello 集區計算節點的子網路的資源識別碼。|
