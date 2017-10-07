---
title: "適用於 Linux Vm 的執行個體中繼資料服務 aaaAzure |Microsoft 文件"
description: "關於 Linux VM 的計算、 網路以及即將進行維護事件 rESTful 介面 tooget 資訊。"
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: 138822addea322c6e565b39a1b2002d7305f5fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a>適用於 Linux VM 的 Azure 執行個體中繼資料服務


hello Azure 執行個體中繼資料服務提供執行可使用的 toomanage 和設定虛擬機器的虛擬機器執行個體的相關資訊。
這包括 SKU、網路組態及近期維護事件等資訊。 如需可用資訊類型的詳細資訊，請參閱[中繼資料類別](#instance-metadata-data-categories)。

Azure 的執行個體中繼資料服務是可存取 tooall IaaS Vm 建立 hello 透過 REST 端點[Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/)。 hello 端點位於已知的路由的內部 IP 位址 (`169.254.169.254`) 以存取只能從 hello VM 內。

> [!IMPORTANT]
> 這項服務已在全域 Azure 區域中**正式推出**。 目前有 Government、China 和 German Azure Cloud 的公開預覽版。 定期收到更新 tooexpose 新虛擬機器執行個體相關資訊。 此頁面會反映最新的 hello[資料分類](#instance-metadata-data-categories)可用。

## <a name="service-availability"></a>服務可用性
hello 服務處於可用正式推出的所有全域 Azure 區域。 hello 服務為 hello 政府、 China 或德國區域中的公用預覽。

區域                                        | 可用性？
-----------------------------------------------|-----------------------------------------------
[所有正式推出的全域 Azure 區域](https://azure.microsoft.com/regions/)     | 正式推出 
[Azure Government](https://azure.microsoft.com/overview/clouds/government/)              | 預覽狀態 
[Azure China](https://www.azure.cn/)                                                           | 預覽狀態
[Azure Germany](https://azure.microsoft.com/overview/clouds/germany/)                    | 預覽狀態

Hello 服務變為可以使用其他的 Azure 雲端中時，會更新這個資料表。

tootry 出 hello 執行個體中繼資料服務，建立從 VM [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/)或 hello [Azure 入口網站](http://portal.azure.com)hello 上方區域和後續 hello 以下的範例中。

## <a name="usage"></a>使用量

### <a name="versioning"></a>版本控制
hello 執行個體中繼資料服務已進行版本設定。 版本都是必要項，而 hello 目前版本為`2017-04-02`。

> [!NOTE] 
> 預覽舊版的排程為 hello 的 api 版本 {最新} 支援的事件。 不再支援這種格式，而且將在未來的 hello 中被取代。

當我們新增較新版本時，如果您的指令碼對於特定資料格式有相依性，則因為相容性，仍然可以存取較舊版本。 不過請注意該 hello 目前預覽 version(2017-03-01) 通常可使用 hello 服務後，可能無法使用。

### <a name="using-headers"></a>使用標頭
當您查詢 hello 執行個體中繼資料服務時，您必須提供 hello 標頭`Metadata: true`tooensure hello 要求不小心重新導向。

### <a name="retrieving-metadata"></a>擷取中繼資料

執行個體中繼資料適用於使用 [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) 建立/管理的執行中 VM。 存取使用 hello 下列要求的虛擬機器執行個體的所有資料分類：

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> 所有執行個體中繼資料查詢都會區分大小寫。

### <a name="data-output"></a>資料輸出
根據預設，hello 執行個體中繼資料服務會傳回資料以 JSON 格式 (`Content-Type: application/json`)。 不過，不同的 API 可以依照要求傳回不同格式的資料。
hello 表是應用程式開發介面可能支援其他資料格式的參考。

API | 預設資料格式 | 其他格式
--------|---------------------|--------------
/instance | json | 文字
/scheduledevents | json | 無

tooaccess 為非預設回應格式，指定 hello 要求的格式為 hello 要求查詢字串參數。 例如：

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>安全性
hello 非路由的 IP 位址上執行虛擬機器執行個體只能從存取 hello 執行個體中繼資料服務端點。 此外，任何要求與`X-Forwarded-For`hello 服務已拒絕郵件標頭。
我們也需要要求 toocontain `Metadata: true` hello 實際要求的標頭 tooensure 直接的方式，而且不屬於預期的重新導向。 

### <a name="error"></a>錯誤
如果找不到的資料元素或格式不正確的要求，hello 執行個體中繼資料服務會傳回標準 HTTP 錯誤。 例如：

HTTP 狀態碼 | 原因
----------------|-------
200 確定 |
400 不正確的要求 | 遺漏 `Metadata: true` 標頭
404 找不到 | hello 要求的項目不存在 
405 不允許的方法 | 僅支援 `GET` 和 `POST` 要求
429 要求太多 | hello API 目前最多支援 5 每秒查詢數
500 服務錯誤     | 稍後重試

### <a name="examples"></a>範例

> [!NOTE] 
> 所有 API 回應都是 JSON 字串。 下列所有範例回應均列印清晰，很容易閱讀。

#### <a name="retrieving-network-information"></a>擷取網路資訊

**要求**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**回應**

> [!NOTE] 
> hello 回應是 JSON 字串。 下列範例回應 hello 是美觀列印來提高可讀性。

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>擷取公用 IP 位址

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>擷取執行個體的所有中繼資料

**要求**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**回應**

> [!NOTE] 
> hello 回應是 JSON 字串。 下列範例回應 hello 是美觀列印來提高可讀性。

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>擷取 Windows 虛擬機器中的中繼資料

**要求**

可以透過 hello PowerShell 公用程式在 Windows 中擷取執行個體中繼資料`curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

或透過 hello `Invoke-RestMethod` cmdlet:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**回應**

> [!NOTE] 
> hello 回應是 JSON 字串。 下列範例回應 hello 是美觀列印來提高可讀性。

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>執行個體中繼資料資料類別
下列資料類別目錄的 hello 都是透過 hello 執行個體中繼資料服務：

資料 | 說明
-----|------------
location | Azure 區域 hello VM 正在執行
名稱 | Hello VM 的名稱 
提供項目 | 提供 hello VM 映像的資訊。 此值只會針對從 Azure 映像庫部署的映像呈現。
publisher | Hello VM 映像的發行者
sku | 特定 hello VM 映像的 SKU  
版本 | Hello VM 映像的版本 
osType | Linux 或 Windows 
platformUpdateDomain |  [更新網域](manage-availability.md)VM 正在執行中的 hello
platformFaultDomain | [容錯網域](manage-availability.md)VM 正在執行中的 hello
vmId | [唯一識別項](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)hello VM
vmSize | [VM 大小](sizes.md)
ipv4/privateIpAddress | Hello VM 本機 IPv4 位址 
ipv4/publicIpAddress | Hello VM 的公用 IPv4 位址
subnet/address | Hello VM 子網路位址
subnet/prefix | 子網路首碼，範例 24
ipv6/ipAddress | Hello VM 本機 IPv6 位址
macAddress | VM mac 位址 
scheduledevents | 目前為公開預覽版，請參閱 [scheduledevents](scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>使用方式的範例案例  

### <a name="tracking-vm-running-on-azure"></a>追蹤在 Azure 上執行的 VM

做為服務提供者，您可能需要執行您的軟體的 Vm tootrack hello 數目或有需要唯一性 tootrack hello VM 代理程式。 toobe 無法 tooget 的唯一識別碼，讓 VM 時，使用 hello`vmId`欄位從 執行個體中繼資料服務。

**要求**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**回應**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>容器的位置，資料分割基礎容錯/更新網域 

對於特定案例，不同資料複本的放置相當重要。 例如， [HDFS 複本放置](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps)或透過容器位置[orchestrator](https://kubernetes.io/docs/user-guide/node-selection/)可能需要 tooknow hello`platformFaultDomain`和`platformUpdateDomain`hello VM 執行。
您可以查詢此資料直接透過 hello 執行個體中繼資料服務。

**要求**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**回應**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>取得支援案例期間 hello VM 之詳細資訊 

做為服務提供者，您可能會收到支援呼叫您要放置 tooknow hello VM 的詳細資訊。 詢問 hello 客戶 tooshare hello 計算中繼資料可提供基本資訊的 hello 支援專業人員 tooknow hello 種 VM 在 Azure 上。 

**要求**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**回應**

> [!NOTE] 
> hello 回應是 JSON 字串。 下列範例回應 hello 是美觀列印來提高可讀性。

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>呼叫使用 hello VM 內的不同語言的中繼資料服務的範例 

語言 | 範例 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb
Go Lan   | https://github.com/Microsoft/azureimds/blob/master/imdssample.go            
Python   | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py
C++      | https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp
C#       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs
Javascript | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js
Powershell | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh
    

## <a name="faq"></a>常見問題集
1. 我收到 hello 錯誤`400 Bad Request, Required metadata header not specified`。 這代表什麼？
   * hello 執行個體中繼資料服務需要 hello 標頭`Metadata: true`toobe 傳入 hello 要求。 在 hello REST 呼叫中傳遞此標頭可讓存取 toohello 執行個體中繼資料服務。 
2. 為什麼我沒有收到我的 VM 計算資訊？
   * 目前執行個體中繼資料服務的 hello 僅支援使用 Azure Resource Manager 建立的執行個體。 在 hello 未來，我們可能會加入雲端服務 Vm 的支援。
3. 我在一陣子之後回過頭來透過 Azure Resource Manager 建立我的虛擬機器。 為什麼我看不到計算中繼資料資訊？
   * 對於任何 2016 年 9 月之後建立的 Vm，新增[標記](../../azure-resource-manager/resource-group-using-tags.md)toostart 文件都看到計算中繼資料。 對於較舊的 Vm （2016 年 9 月之前建立），新增/移除延伸模組或資料磁碟 toohello VM toorefresh 中繼資料。
4. 為什麼我會收到 hello 錯誤`500 Internal Server Error`？
   * 請根據指數型輪詢系統重試您的要求。 如果 hello 問題持續發生，請連絡 Azure 支援。
5. 我要在哪裡共用其他問題/註解？
   * 請在 http://feedback.azure.com 上傳送您的註解。
7. 這是否適用於虛擬機器擴展集執行個體？
   * 是，中繼資料服務適用於擴展集執行個體。 
6. 如何在 hello 服務取得支援？
   * hello 服務 tooget 支援 hello VM，您不能 tooget 中繼資料回應長時間重試後的 Azure 入口網站中建立的支援問題 

   ![執行個體中繼資料支援](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>後續步驟

- 深入了解 hello[排程的事件](scheduled-events.md)API**處於公開預覽狀態**hello 執行個體中繼資料服務所提供。
