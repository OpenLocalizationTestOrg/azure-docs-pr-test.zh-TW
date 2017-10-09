---
title: "aaaScheduled 事件與中繼資料的 Azure 服務 |Microsoft 文件"
description: "發生之前加以反應 tooImpactful 虛擬機器上的事件。"
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: b5c0849958c3ab48fa9c2cbff7db62f2e9d7daf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a>Azure 中繼資料服務 - 排定的事件 (預覽)

> [!NOTE] 
> 預覽是可用 tooyou 對貴用戶同意 toohello 使用條款 hello 條件。 如需詳細資訊，請參閱 [Microsoft Azure 預覽版增補使用條款](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/)。
>

排程的事件是在 hello Azure 中繼資料服務的 hello 子服務。 其會呈現即將發生的事件 (例如，重新開機) 相關資訊，以便應用程式做好準備並限制中斷造成的影響。 它適用於所有 Azure 虛擬機器類型 (包括 PaaS 和 IaaS)。 排程的事件可讓您虛擬機器階段 tooperform 預防工作 toominimize hello 效果的事件。 

## <a name="introduction---why-scheduled-events"></a>簡介 - 為何使用排定的事件？

與排程的事件，您可以採取步驟的平台 intiated 維護或使用者啟動的動作 toolimit hello 影響您的服務。 

多個執行個體的工作負載，可以使用複寫技術 toomaintain 狀態，可能容易遭受 toooutages 發生多個執行個體。 例如中斷可能會導致耗費資源的工作 (例如，重建索引) 或甚至是複本遺失。 

在其他許多情況下，hello 整體服務可用性，可以改善執行的非失誤性關機順序，例如完成 （或取消） 進行中的交易，重新指派工作 tooother Vm hello 叢集中 （手動容錯移轉），或移除 hello從網路負載平衡器集區的虛擬機器。 

一些情況下，通知系統管理員有關即將發生的事件，或將記錄這類事件協助改善 hello hello 雲端中裝載的應用程式的服務性。

Azure 服務中繼資料介面排程的事件中 hello 下列使用案例：
-   平台起始的維護 (例如，主機作業系統推出)
-   使用者起始的呼叫 (例如，使用者重新啟動或重新部署 VM)


## <a name="scheduled-events---hello-basics"></a>排程的事件-hello 基本概念  

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
使用者啟動的虛擬機器維護透過 hello Azure 入口網站應用程式開發介面、 CLI 或 PowerShell 將會導致排程的事件。 這可讓您在應用程式中的 tootest hello 維護準備邏輯，並允許使用者起始維護您的應用程式 tooprepare。

重新啟動虛擬機器將會排程 `Reboot` 類型的事件。 重新部署虛擬機器將會排程 `Redeploy` 類型的事件。

> [!NOTE] 
> 目前最多可同時排程 10 個使用者起始的維護作業。 「排程的事件」正式運作之前，將會放寬這項限制。

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
| EventType | 此事件造成的影響。 <br><br> 值： <br><ul><li> `Freeze`: hello 虛擬機器是排程的 toopause 幾秒鐘的時間。 hello CPU 將遭擱置，但不會影響到記憶體中，開啟的檔案或網路連線。 <li>`Reboot`: hello 已排定重新開機的虛擬機器 （非持續性記憶體是遺失）。 <li>`Redeploy`: hello 虛擬機器是排程的 toomove tooanother 節點 （暫時磁碟會遺失）。 |
| ResourceType | 受此事件影響的資源類型。 <br><br> 值： <ul><li>`VirtualMachine`|
| 資源| 受此事件影響的資源清單。 這從最多一個保證 toocontain 機器[更新網域](windows/manage-availability.md)，但不是能包含 hello UD 中的所有機器。 <br><br> 範例： <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| 事件狀態 | 此事件的狀態。 <br><br> 值： <ul><li>`Scheduled`： 此事件是排程的 toostart hello hello 中指定的時間之後`NotBefore`屬性。<li>`Started`︰已啟動事件。</ul> 否`Completed`或曾經提供類似的狀態; hello 事件完成時，將不會再傳回 hello 事件。
| NotBefore| 自此之後可能會啟動此事件的時間。 <br><br> 範例： <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>事件排程
每個事件已排程的時間在未來的 hello 最小數量取決於事件類型。 事件的 `NotBefore` 屬性會反映這個時間。 

|EventType  | 最短時間通知 |
| - | - |
| 凍結| 15 分鐘 |
| 重新啟動 | 15 分鐘 |
| 重新部署 | 10 分鐘 |

### <a name="starting-an-event-expedite"></a>啟動事件 (加速)

一旦您已學到的即將發生的事件，並完成您的邏輯非失誤性關機，您可以藉由核准 hello 未處理的事件`POST`呼叫 toohello 中繼資料服務，以 hello `EventId`。 這表示它可以縮短 hello 最小通知 tooAzure 的時間 （可能的話）。 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> 用來認可事件可讓您 hello 事件 tooproceed 所有`Resources`hello 事件中不只是 hello 會 hello 事件認可的虛擬機器。 您可能會因此選擇 tooelect 可能越簡單越 hello hello 中的第一部機器的指引 toocoordinate hello 通知`Resources`欄位。

## <a name="samples"></a>範例

### <a name="powershell-sample"></a>PowerShell 範例 

hello 下列查詢範例 hello 排程的事件的中繼資料服務和核准每個未處理的事件。

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


### <a name="c-sample"></a>C\# 範例 

hello 下列範例是簡單的用戶端與 hello 中繼資料服務進行通訊。

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

可以使用下列資料結構的 hello 表示排程的事件：

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

hello 下列查詢範例 hello 排程的事件的中繼資料服務和核准每個未處理的事件。

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

### <a name="python-sample"></a>Python 範例 

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

- 深入了解 hello Api 可在 hello[執行個體中繼資料服務](virtual-machines-instancemetadataservice-overview.md)。
- 了解 [Azure 中 Windows 虛擬機器預定進行的維修](windows/planned-maintenance.md)。
- 了解 [Azure 中 Linux 虛擬機器預定進行的維修](linux/planned-maintenance.md)。
