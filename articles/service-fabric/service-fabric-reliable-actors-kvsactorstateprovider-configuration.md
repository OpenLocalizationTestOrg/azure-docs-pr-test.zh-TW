---
title: "在 Azure microservices aaaChange KVSActorStateProvider 設定 |Microsoft 文件"
description: "了解設定 KVSActorStateProvider 類型的 Azure Service Fabric 可設定狀態的動作項目。"
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>設定 Reliable Actors - KVSActorStateProvider
您可以藉由變更產生 hello Microsoft Visual Studio 封裝根目錄下 hello 指定執行者的 hello Config 資料夾中的 hello settings.xml 檔修改 KVSActorStateProvider hello 預設組態。

hello Azure Service Fabric 執行階段會尋找 hello settings.xml 檔案中的預先定義的區段名稱，並時都會佔用掉 hello 組態值建立 hello 基礎執行階段元件。

> [!NOTE]
> 請勿**不**刪除或修改的設定產生 hello Visual Studio 方案中的 hello settings.xml 檔案中的 hello hello 的區段名稱。
> 
> 

## <a name="replicator-security-configuration"></a>複寫器安全性組態
複寫器的安全性設定是在複寫期間所使用的 toosecure hello 通訊通道。 這表示服務無法看到彼此的複寫流量，確保 hello 資料，則高可用性的安全。
依預設，空白的安全性組態區段會妨礙複寫安全性。

### <a name="section-name"></a>區段名稱
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>複寫器組態
複寫器的組態設定，負責建立 hello 動作項目狀態提供者狀態可靠 hello 複寫器。
hello 預設設定由 hello Visual Studio 範本所產生，並應已足夠。 本節討論有關可用 tootune hello 複寫器的其他組態。

### <a name="section-name"></a>區段名稱
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>組態名稱
| 名稱 | 單位 | 預設值 | 備註 |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |秒 |0.015 |一段時間的哪些 hello 複寫器在 hello 次要等候接收之前傳送回認可 toohello 主要的作業之後。 傳送作業在此時間間隔內處理的任何其他通知 toobe 會以一個回應傳送。 |
| ReplicatorEndpoint |N/A |無預設值--必要的參數 |IP 位址和連接埠 hello 主要/次要複寫器都會使用 toocommunicate，而其他購 hello 複本集中。 這應該參考 hello 服務資訊清單中的 TCP 資源端點。 請參閱太[服務資訊清單資源](service-fabric-service-manifest-resources.md)tooread 更多關於 hello 服務資訊清單中定義端點資源。 |
| RetryInterval |秒 |5 |之後如果收到作業認可訊息的 hello 複寫器重新傳輸的時間週期。 |
| MaxReplicationMessageSize |位元組 |50 MB |單一訊息可傳輸的複寫資料大小上限。 |
| MaxPrimaryReplicationQueueSize |作業數目 |1024 |Hello 主要佇列中的作業數目上限。 作業釋放 hello 主要複寫器接收到所有的 hello 次要購自之後。 此值必須大於 64 且為 2 的乘冪。 |
| MaxSecondaryReplicationQueueSize |作業數目 |2048 |Hello 次要佇列中的作業數目上限。 透過持續性讓狀態成為高可用性後，系統便會釋放作業。 此值必須大於 64 且為 2 的乘冪。 |

## <a name="store-configuration"></a>存放區組態
會使用的 tooconfigure hello 本機存放區所使用的 toopersist hello 狀態正在複寫的存放區組態。
hello 預設設定由 hello Visual Studio 範本所產生，並應已足夠。 本節討論有關其他設定，可以使用 tootune hello 本機存放區。

### <a name="section-name"></a>區段名稱
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>組態名稱
| 名稱 | 單位 | 預設值 | 備註 |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |毫秒 |200 |設定批次處理間隔可用之區域的長期存放區認可 hello 最大值。 |
| MaxVerPages |頁面數目 |16384 |存放區資料庫的版本中的頁數 hello 本機的 hello 最大數目。 它會判斷 hello 的未處理的交易數目上限。 |

## <a name="sample-configuration-file"></a>範例組態檔
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```
## <a name="remarks"></a>備註
hello BatchAcknowledgementInterval 參數控制複寫延遲。 值 '0' 會導致 hello 最低可能延遲，輸送量的 hello 成本 （如需收條訊息必須傳送和處理，每個包含較少的通知）。
hello BatchAcknowledgementInterval，hello 值越大 hello 較高的 hello 整體複寫輸送量，在 hello 成本較高的作業延遲。 這會直接轉譯 toohello 延遲的交易認可。

