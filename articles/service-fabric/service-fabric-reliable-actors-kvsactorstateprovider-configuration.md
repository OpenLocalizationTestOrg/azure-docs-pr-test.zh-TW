---
title: "變更 Azure 微服務中的 KVSActorStateProvider 設定 | Microsoft Docs"
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
ms.openlocfilehash: 2af1d21a46cde5ba63c967461a1835b5e34ca3cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a><span data-ttu-id="7e04c-103">設定 Reliable Actors - KVSActorStateProvider</span><span class="sxs-lookup"><span data-stu-id="7e04c-103">Configuring Reliable Actors--KVSActorStateProvider</span></span>
<span data-ttu-id="7e04c-104">您可以在指定之動作項目的 Config 資料夾下，變更 Microsoft Visual Studio 封裝根中所產生的 settings.xml，來修改 KVSActorStateProvider 的預設組態。</span><span class="sxs-lookup"><span data-stu-id="7e04c-104">You can modify the default configuration of KVSActorStateProvider by changing the settings.xml file that is generated in the Microsoft Visual Studio package root under the Config folder for the specified actor.</span></span>

<span data-ttu-id="7e04c-105">Azure Service Fabric 執行階段會在建立基礎執行階段元件時，在 settings.xml 檔案中尋找預先定義的區段名稱，並使用組態值。</span><span class="sxs-lookup"><span data-stu-id="7e04c-105">The Azure Service Fabric runtime looks for predefined section names in the settings.xml file and consumes the configuration values while creating the underlying runtime components.</span></span>

> [!NOTE]
> <span data-ttu-id="7e04c-106">請 **不要** 刪除或修改在 Visual Studio 方案中產生之 settings.xml 檔案中的下列組態區段名稱。</span><span class="sxs-lookup"><span data-stu-id="7e04c-106">Do **not** delete or modify the section names of the following configurations in the settings.xml file that is generated in the Visual Studio solution.</span></span>
> 
> 

## <a name="replicator-security-configuration"></a><span data-ttu-id="7e04c-107">複寫器安全性組態</span><span class="sxs-lookup"><span data-stu-id="7e04c-107">Replicator security configuration</span></span>
<span data-ttu-id="7e04c-108">複寫器安全性組態用來保護在複寫期間使用的通訊通道。</span><span class="sxs-lookup"><span data-stu-id="7e04c-108">Replicator security configurations are used to secure the communication channel that is used during replication.</span></span> <span data-ttu-id="7e04c-109">這表示服務將無法看到彼此的複寫流量，並且也會確保高度可用資料的安全。</span><span class="sxs-lookup"><span data-stu-id="7e04c-109">This means that services cannot see each other's replication traffic, ensuring that the data that is made highly available is also secure.</span></span>
<span data-ttu-id="7e04c-110">依預設，空白的安全性組態區段會妨礙複寫安全性。</span><span class="sxs-lookup"><span data-stu-id="7e04c-110">By default, an empty security configuration section prevents replication security.</span></span>

### <a name="section-name"></a><span data-ttu-id="7e04c-111">區段名稱</span><span class="sxs-lookup"><span data-stu-id="7e04c-111">Section name</span></span>
<span data-ttu-id="7e04c-112">&lt;ActorName&gt;ServiceReplicatorSecurityConfig</span><span class="sxs-lookup"><span data-stu-id="7e04c-112">&lt;ActorName&gt;ServiceReplicatorSecurityConfig</span></span>

## <a name="replicator-configuration"></a><span data-ttu-id="7e04c-113">複寫器組態</span><span class="sxs-lookup"><span data-stu-id="7e04c-113">Replicator configuration</span></span>
<span data-ttu-id="7e04c-114">複寫器組態會設定負責讓動作項目狀態提供者狀態高度可靠的複寫器。</span><span class="sxs-lookup"><span data-stu-id="7e04c-114">Replicator configurations configure the replicator that is responsible for making the Actor State Provider state highly reliable.</span></span>
<span data-ttu-id="7e04c-115">預設組態由 Visual Studio 範本所產生，且應該已經足夠。</span><span class="sxs-lookup"><span data-stu-id="7e04c-115">The default configuration is generated by the Visual Studio template and should suffice.</span></span> <span data-ttu-id="7e04c-116">本節說明可用於微調複寫器的其他組態。</span><span class="sxs-lookup"><span data-stu-id="7e04c-116">This section talks about additional configurations that are available to tune the replicator.</span></span>

### <a name="section-name"></a><span data-ttu-id="7e04c-117">區段名稱</span><span class="sxs-lookup"><span data-stu-id="7e04c-117">Section name</span></span>
<span data-ttu-id="7e04c-118">&lt;ActorName&gt;ServiceReplicatorConfig</span><span class="sxs-lookup"><span data-stu-id="7e04c-118">&lt;ActorName&gt;ServiceReplicatorConfig</span></span>

### <a name="configuration-names"></a><span data-ttu-id="7e04c-119">組態名稱</span><span class="sxs-lookup"><span data-stu-id="7e04c-119">Configuration names</span></span>
| <span data-ttu-id="7e04c-120">名稱</span><span class="sxs-lookup"><span data-stu-id="7e04c-120">Name</span></span> | <span data-ttu-id="7e04c-121">單位</span><span class="sxs-lookup"><span data-stu-id="7e04c-121">Unit</span></span> | <span data-ttu-id="7e04c-122">預設值</span><span class="sxs-lookup"><span data-stu-id="7e04c-122">Default value</span></span> | <span data-ttu-id="7e04c-123">備註</span><span class="sxs-lookup"><span data-stu-id="7e04c-123">Remarks</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e04c-124">BatchAcknowledgementInterval</span><span class="sxs-lookup"><span data-stu-id="7e04c-124">BatchAcknowledgementInterval</span></span> |<span data-ttu-id="7e04c-125">秒</span><span class="sxs-lookup"><span data-stu-id="7e04c-125">Seconds</span></span> |<span data-ttu-id="7e04c-126">0.015</span><span class="sxs-lookup"><span data-stu-id="7e04c-126">0.015</span></span> |<span data-ttu-id="7e04c-127">次要複寫器收到作業後，將通知傳回給主要複寫器前所等待的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="7e04c-127">Time period for which the replicator at the secondary waits after receiving an operation before sending back an acknowledgement to the primary.</span></span> <span data-ttu-id="7e04c-128">任何要在此間隔內傳送給作業處理的其他通知，會集中以一個回應傳送。</span><span class="sxs-lookup"><span data-stu-id="7e04c-128">Any other acknowledgements to be sent for operations processed within this interval are sent as one response.</span></span> |
| <span data-ttu-id="7e04c-129">ReplicatorEndpoint</span><span class="sxs-lookup"><span data-stu-id="7e04c-129">ReplicatorEndpoint</span></span> |<span data-ttu-id="7e04c-130">N/A</span><span class="sxs-lookup"><span data-stu-id="7e04c-130">N/A</span></span> |<span data-ttu-id="7e04c-131">無預設值--必要的參數</span><span class="sxs-lookup"><span data-stu-id="7e04c-131">No default--required parameter</span></span> |<span data-ttu-id="7e04c-132">主要/次要複寫器將用於與複本集中其他複寫器通訊的 IP 位址與連接埠。</span><span class="sxs-lookup"><span data-stu-id="7e04c-132">IP address and port that the primary/secondary replicator will use to communicate with other replicators in the replica set.</span></span> <span data-ttu-id="7e04c-133">這應該參考服務資訊清單中的 TCP 資源端點。</span><span class="sxs-lookup"><span data-stu-id="7e04c-133">This should reference a TCP resource endpoint in the service manifest.</span></span> <span data-ttu-id="7e04c-134">請參閱 [服務資訊清單資源](service-fabric-service-manifest-resources.md) ，深入了解如何在服務資訊清單中定義端點資源。</span><span class="sxs-lookup"><span data-stu-id="7e04c-134">Refer to [Service manifest resources](service-fabric-service-manifest-resources.md) to read more about defining endpoint resources in the service manifest.</span></span> |
| <span data-ttu-id="7e04c-135">RetryInterval</span><span class="sxs-lookup"><span data-stu-id="7e04c-135">RetryInterval</span></span> |<span data-ttu-id="7e04c-136">秒</span><span class="sxs-lookup"><span data-stu-id="7e04c-136">Seconds</span></span> |<span data-ttu-id="7e04c-137">5</span><span class="sxs-lookup"><span data-stu-id="7e04c-137">5</span></span> |<span data-ttu-id="7e04c-138">複寫器若未收到作業通知，在重新傳輸訊息前的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="7e04c-138">Time period after which the replicator re-transmits a message if it does not receive an acknowledgement for an operation.</span></span> |
| <span data-ttu-id="7e04c-139">MaxReplicationMessageSize</span><span class="sxs-lookup"><span data-stu-id="7e04c-139">MaxReplicationMessageSize</span></span> |<span data-ttu-id="7e04c-140">位元組</span><span class="sxs-lookup"><span data-stu-id="7e04c-140">Bytes</span></span> |<span data-ttu-id="7e04c-141">50 MB</span><span class="sxs-lookup"><span data-stu-id="7e04c-141">50 MB</span></span> |<span data-ttu-id="7e04c-142">單一訊息可傳輸的複寫資料大小上限。</span><span class="sxs-lookup"><span data-stu-id="7e04c-142">Maximum size of replication data that can be transmitted in a single message.</span></span> |
| <span data-ttu-id="7e04c-143">MaxPrimaryReplicationQueueSize</span><span class="sxs-lookup"><span data-stu-id="7e04c-143">MaxPrimaryReplicationQueueSize</span></span> |<span data-ttu-id="7e04c-144">作業數目</span><span class="sxs-lookup"><span data-stu-id="7e04c-144">Number of operations</span></span> |<span data-ttu-id="7e04c-145">1024</span><span class="sxs-lookup"><span data-stu-id="7e04c-145">1024</span></span> |<span data-ttu-id="7e04c-146">主要佇列中作業數目上限。</span><span class="sxs-lookup"><span data-stu-id="7e04c-146">Maximum number of operations in the primary queue.</span></span> <span data-ttu-id="7e04c-147">主要複寫器收到所有次要複寫器的通知後，系統便會釋放作業。</span><span class="sxs-lookup"><span data-stu-id="7e04c-147">An operation is freed up after the primary replicator receives an acknowledgement from all the secondary replicators.</span></span> <span data-ttu-id="7e04c-148">此值必須大於 64 且為 2 的乘冪。</span><span class="sxs-lookup"><span data-stu-id="7e04c-148">This value must be greater than 64 and a power of 2.</span></span> |
| <span data-ttu-id="7e04c-149">MaxSecondaryReplicationQueueSize</span><span class="sxs-lookup"><span data-stu-id="7e04c-149">MaxSecondaryReplicationQueueSize</span></span> |<span data-ttu-id="7e04c-150">作業數目</span><span class="sxs-lookup"><span data-stu-id="7e04c-150">Number of operations</span></span> |<span data-ttu-id="7e04c-151">2048</span><span class="sxs-lookup"><span data-stu-id="7e04c-151">2048</span></span> |<span data-ttu-id="7e04c-152">次要佇列中作業數目上限。</span><span class="sxs-lookup"><span data-stu-id="7e04c-152">Maximum number of operations in the secondary queue.</span></span> <span data-ttu-id="7e04c-153">透過持續性讓狀態成為高可用性後，系統便會釋放作業。</span><span class="sxs-lookup"><span data-stu-id="7e04c-153">An operation is freed up after making its state highly available through persistence.</span></span> <span data-ttu-id="7e04c-154">此值必須大於 64 且為 2 的乘冪。</span><span class="sxs-lookup"><span data-stu-id="7e04c-154">This value must be greater than 64 and a power of 2.</span></span> |

## <a name="store-configuration"></a><span data-ttu-id="7e04c-155">存放區組態</span><span class="sxs-lookup"><span data-stu-id="7e04c-155">Store configuration</span></span>
<span data-ttu-id="7e04c-156">存放區組態用於設定本機存放區以用來保存正在複寫的狀態。</span><span class="sxs-lookup"><span data-stu-id="7e04c-156">Store configurations are used to configure the local store that is used to persist the state that is being replicated.</span></span>
<span data-ttu-id="7e04c-157">預設組態由 Visual Studio 範本所產生，且應該已經足夠。</span><span class="sxs-lookup"><span data-stu-id="7e04c-157">The default configuration is generated by the Visual Studio template and should suffice.</span></span> <span data-ttu-id="7e04c-158">本節將討論其他可用來微調本機存放區的組態。</span><span class="sxs-lookup"><span data-stu-id="7e04c-158">This section talks about additional configurations that are available to tune the local store.</span></span>

### <a name="section-name"></a><span data-ttu-id="7e04c-159">區段名稱</span><span class="sxs-lookup"><span data-stu-id="7e04c-159">Section name</span></span>
<span data-ttu-id="7e04c-160">&lt;ActorName&gt;ServiceLocalStoreConfig</span><span class="sxs-lookup"><span data-stu-id="7e04c-160">&lt;ActorName&gt;ServiceLocalStoreConfig</span></span>

### <a name="configuration-names"></a><span data-ttu-id="7e04c-161">組態名稱</span><span class="sxs-lookup"><span data-stu-id="7e04c-161">Configuration names</span></span>
| <span data-ttu-id="7e04c-162">名稱</span><span class="sxs-lookup"><span data-stu-id="7e04c-162">Name</span></span> | <span data-ttu-id="7e04c-163">單位</span><span class="sxs-lookup"><span data-stu-id="7e04c-163">Unit</span></span> | <span data-ttu-id="7e04c-164">預設值</span><span class="sxs-lookup"><span data-stu-id="7e04c-164">Default value</span></span> | <span data-ttu-id="7e04c-165">備註</span><span class="sxs-lookup"><span data-stu-id="7e04c-165">Remarks</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e04c-166">MaxAsyncCommitDelayInMilliseconds</span><span class="sxs-lookup"><span data-stu-id="7e04c-166">MaxAsyncCommitDelayInMilliseconds</span></span> |<span data-ttu-id="7e04c-167">毫秒</span><span class="sxs-lookup"><span data-stu-id="7e04c-167">Milliseconds</span></span> |<span data-ttu-id="7e04c-168">200</span><span class="sxs-lookup"><span data-stu-id="7e04c-168">200</span></span> |<span data-ttu-id="7e04c-169">設定長期本機存放區認可的批次間隔上限。</span><span class="sxs-lookup"><span data-stu-id="7e04c-169">Sets the maximum batching interval for durable local store commits.</span></span> |
| <span data-ttu-id="7e04c-170">MaxVerPages</span><span class="sxs-lookup"><span data-stu-id="7e04c-170">MaxVerPages</span></span> |<span data-ttu-id="7e04c-171">頁面數目</span><span class="sxs-lookup"><span data-stu-id="7e04c-171">Number of pages</span></span> |<span data-ttu-id="7e04c-172">16384</span><span class="sxs-lookup"><span data-stu-id="7e04c-172">16384</span></span> |<span data-ttu-id="7e04c-173">本機存放區資料庫中版本頁面數上限。</span><span class="sxs-lookup"><span data-stu-id="7e04c-173">The maximum number of version pages in the local store database.</span></span> <span data-ttu-id="7e04c-174">其會判定未完成交易數上限。</span><span class="sxs-lookup"><span data-stu-id="7e04c-174">It determines the maximum number of outstanding transactions.</span></span> |

## <a name="sample-configuration-file"></a><span data-ttu-id="7e04c-175">範例組態檔</span><span class="sxs-lookup"><span data-stu-id="7e04c-175">Sample configuration file</span></span>
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
## <a name="remarks"></a><span data-ttu-id="7e04c-176">備註</span><span class="sxs-lookup"><span data-stu-id="7e04c-176">Remarks</span></span>
<span data-ttu-id="7e04c-177">BatchAcknowledgementInterval 參數會控制複寫延遲性。</span><span class="sxs-lookup"><span data-stu-id="7e04c-177">The BatchAcknowledgementInterval parameter controls replication latency.</span></span> <span data-ttu-id="7e04c-178">值為 '0' 時延遲可能性最低，但代價是降低輸送量 (隨著必須傳送與處理的通知訊息增加，每個訊息包含的通知會變少)。</span><span class="sxs-lookup"><span data-stu-id="7e04c-178">A value of '0' results in the lowest possible latency, at the cost of throughput (as more acknowledgement messages must be sent and processed, each containing fewer acknowledgements).</span></span>
<span data-ttu-id="7e04c-179">BatchAcknowledgementInterval 的值越大，整體複寫輸送量越高，代價是作業延遲變高。</span><span class="sxs-lookup"><span data-stu-id="7e04c-179">The larger the value for BatchAcknowledgementInterval, the higher the overall replication throughput, at the cost of higher operation latency.</span></span> <span data-ttu-id="7e04c-180">這會直接轉換成交易認可的延遲。</span><span class="sxs-lookup"><span data-stu-id="7e04c-180">This directly translates to the latency of transaction commits.</span></span>
