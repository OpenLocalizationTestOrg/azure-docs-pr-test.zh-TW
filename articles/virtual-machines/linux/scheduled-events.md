---
title: "適用於 Linux Vm 在 Azure 中的事件 aaaScheduled |Microsoft 文件"
description: "在您的 Linux 虛擬機器上使用 hello Azure 中繼資料服務，進行排程的事件。"
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a>Azure 中繼資料服務：Linux VM 的已排定事件 (預覽)

> [!NOTE] 
> 預覽是可用 tooyou 對貴用戶同意 toohello 使用條款 hello 條件。 如需詳細資訊，請參閱 [Microsoft Azure 預覽版增補使用條款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)。
>

排程的事件是在 hello Azure 中繼資料服務的 hello 子服務。 其會呈現即將發生的事件 (例如，重新開機) 相關資訊，以便應用程式做好準備並限制中斷造成的影響。 它適用於所有 Azure 虛擬機器類型 (包括 PaaS 和 IaaS)。 排程的事件可讓您虛擬機器階段 tooperform 預防工作 toominimize hello 效果的事件。 

排定的事件適用於 Windows 和 Linux VM。 如需 Windows 上已排定事件的資訊，請參閱 [Windows VM 的已排定事件](../windows/scheduled-events.md)。

## <a name="why-scheduled-events"></a>為什麼要使用排定的事件？

與排程的事件，您可以採取步驟的平台 intiated 維護或使用者啟動的動作 toolimit hello 影響您的服務。 

多個執行個體的工作負載，可以使用複寫技術 toomaintain 狀態，可能容易遭受 toooutages 發生多個執行個體。 例如中斷可能會導致耗費資源的工作 (例如，重建索引) 或甚至是複本遺失。 

在其他許多情況下，hello 整體服務可用性，可以改善執行的非失誤性關機順序，例如完成 （或取消） 進行中的交易，重新指派工作 tooother Vm hello 叢集中 （手動容錯移轉），或移除 hello從網路負載平衡器集區的虛擬機器。 

一些情況下，通知系統管理員有關即將發生的事件，或將記錄這類事件協助改善 hello hello 雲端中裝載的應用程式的服務性。

Azure 服務中繼資料介面排程的事件中 hello 下列使用案例：
-   平台起始的維護 (例如，主機作業系統推出)
-   使用者起始的呼叫 (例如，使用者重新啟動或重新部署 VM)


## <a name="hello-basics"></a>hello 基本概念  

Azure 的中繼資料服務會公開執行使用從 hello VM 中存取 REST 端點的虛擬機器的相關資訊。 hello 資訊可透過路由的內部 IP，讓它不會顯示 hello VM 之外。

### <a name="scope"></a>Scope
排程的事件會呈現的 tooall 雲端服務中的虛擬機器或 tooall 可用性設定組中的虛擬機器。 如此一來，您應該檢查 hello`Resources`欄位中的 Vm 會影響 toobe hello 事件 tooidentify。 

### <a name="discovering-hello-endpoint"></a>探索 hello 端點
在虛擬機器建立虛擬網路 (VNet) 中的位置 hello 的情況下，hello 中繼資料服務可以使用靜態路由的內部 ip 位址，從`169.254.169.254`。
如果 hello 虛擬機器不虛擬網路，hello 預設情況下，雲端服務和傳統的 Vm 中建立額外的邏輯是必要的 toodiscover hello 端點 toouse。 請參閱 toothis 範例 toolearn 如何太[探索 hello 主機端點](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)。

### <a name="versioning"></a>版本控制 
hello 執行個體中繼資料服務已進行版本設定。 版本都是必要項，而 hello 目前版本為`2017-03-01`。

> [!NOTE] 
> 預覽舊版的排程為 hello 的 api 版本 {最新} 支援的事件。 不再支援這種格式，而且將在未來的 hello 中被取代。

### <a name="using-headers"></a>使用標頭
當您查詢 hello 中繼資料服務時，您必須提供 hello 標頭`Metadata: true`tooensure hello 要求不小心重新導向。

### <a name="enabling-scheduled-events"></a>啟用排定的事件
hello 進行排程的事件，要求第一次 Azure 隱含啟用 hello 功能在您的虛擬機器上。 如此一來，您應該預期延遲的回應中的總 tootwo 分鐘您第一次呼叫。

### <a name="user-initiated-maintenance"></a>使用者起始的維護
使用者啟動的虛擬機器維護透過 hello Azure 入口網站應用程式開發介面、 CLI 或 PowerShell 導致排程的事件。 這可讓您在應用程式中的 tootest hello 維護準備邏輯，並允許使用者起始維護您的應用程式 tooprepare。

重新啟動虛擬機器會排定 `Reboot` 類型的事件。 重新部署虛擬機器會排定 `Redeploy` 類型的事件。

> [!NOTE] 
> 目前最多可同時排程 10 個使用者起始的維護作業。 「排定的事件」正式運作之前，將會放寬這項限制。

> [!NOTE] 
> 使用者起始的維護會導致「排程的事件」，這個狀況目前尚無法設定。 預計在未來版本中，將可針對此狀況作設定。

## <a name="using-hello-api"></a>使用 hello API

### <a name="query-for-events"></a>查詢事件
您可以查詢排程的事件只是藉由呼叫 hello 下列：

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

回應包含排定的事件陣列。 空白陣列表示目前沒有任何排定的事件。
萬一 hello 回應 hello 中排程的事件，包含陣列的事件： 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>事件屬性
|屬性  |  說明 |
| - | - |
| EventId | 此事件的全域唯一識別碼。 <br><br> 範例： <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| EventType | 此事件造成的影響。 <br><br> 值： <br><ul><li> `Freeze`: hello 虛擬機器是排程的 toopause 幾秒鐘的時間。 hello CPU 已暫停，但不會影響到記憶體中，開啟的檔案或網路連線。 <li>`Reboot`: hello 已排定重新開機的虛擬機器 （非持續性記憶體是遺失）。 <li>`Redeploy`: hello 虛擬機器是排程的 toomove tooanother 節點 （暫時磁碟會遺失）。 |
| ResourceType | 受此事件影響的資源類型。 <br><br> 值： <ul><li>`VirtualMachine`|
| 資源| 受此事件影響的資源清單。 這從最多一個保證 toocontain 機器[更新網域](manage-availability.md)，但不是能包含 hello UD 中的所有機器。 <br><br> 範例： <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| 事件狀態 | 此事件的狀態。 <br><br> 值： <ul><li>`Scheduled`： 此事件是排程的 toostart hello hello 中指定的時間之後`NotBefore`屬性。<li>`Started`︰已啟動事件。</ul> 否`Completed`或曾經提供類似的狀態; hello 事件完成時，將不會再傳回 hello 事件。
| NotBefore| 自此之後可能會啟動此事件的時間。 <br><br> 範例： <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>事件排定
每個事件已排程的時間在未來的 hello 最小數量取決於事件類型。 事件的 `NotBefore` 屬性會反映這個時間。 

|EventType  | 最短時間通知 |
| - | - |
| 凍結| 15 分鐘 |
| 重新啟動 | 15 分鐘 |
| 重新部署 | 10 分鐘 |

### <a name="starting-an-event"></a>啟動事件 

一旦您已學到的即將發生的事件，並完成您的邏輯非失誤性關機，您可以藉由核准 hello 未處理的事件`POST`呼叫 toohello 中繼資料服務，以 hello `EventId`。 這表示它可以縮短 hello 最小通知 tooAzure 的時間 （可能的話）。 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> 用來認可事件會允許所有 hello 事件 tooproceed `Resources` hello 事件中不只是 hello 會 hello 事件認可的虛擬機器。 您可能會因此選擇 tooelect 可能越簡單越 hello hello 中的第一部機器的指引 toocoordinate hello 通知`Resources`欄位。




## <a name="python-sample"></a>Python 範例 

hello 下列查詢範例 hello 排程的事件的中繼資料服務和核准每個未處理的事件。

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>後續步驟 

- 深入了解 hello Api 可在 hello[執行個體中繼資料服務](instance-metadata-service.md)。
- 了解 [Azure 中 Linux 虛擬機器預定進行的維修](planned-maintenance.md)。
