---
title: "aaaAzure 轉送連接埠設定 |Microsoft 文件"
description: "Azure 轉送連接埠值的相關詳細資料。"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: e66785f786ee241c974d250f9ec29dfcc1fdc3fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-port-settings"></a><span data-ttu-id="d55c7-103">Azure 轉送連接埠設定</span><span class="sxs-lookup"><span data-stu-id="d55c7-103">Azure Relay port settings</span></span>

<span data-ttu-id="d55c7-104">hello 下表描述 hello 必要的組態之連接埠值 Azure 轉送。</span><span class="sxs-lookup"><span data-stu-id="d55c7-104">hello following table describes hello required configuration for port values for Azure Relay.</span></span>

## <a name="hybrid-connections"></a><span data-ttu-id="d55c7-105">混合式連線</span><span class="sxs-lookup"><span data-stu-id="d55c7-105">Hybrid Connections</span></span>
<span data-ttu-id="d55c7-106">混合式連線會使用 WebSockets hello 基礎傳輸機制，會使用為**HTTPS**只。</span><span class="sxs-lookup"><span data-stu-id="d55c7-106">Hybrid Connections uses WebSockets as hello underlying transport mechanism, which uses **HTTPS** only.</span></span> 

## <a name="wcf-relays"></a><span data-ttu-id="d55c7-107">WCF 轉送</span><span class="sxs-lookup"><span data-stu-id="d55c7-107">WCF Relays</span></span>
  
|<span data-ttu-id="d55c7-108">繫結</span><span class="sxs-lookup"><span data-stu-id="d55c7-108">Binding</span></span>|<span data-ttu-id="d55c7-109">傳輸安全性</span><span class="sxs-lookup"><span data-stu-id="d55c7-109">Transport Security</span></span>|<span data-ttu-id="d55c7-110">連接埠</span><span class="sxs-lookup"><span data-stu-id="d55c7-110">Port</span></span>|  
|-------------|------------------------|----------|  
|<span data-ttu-id="d55c7-111">[BasicHttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="d55c7-111">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)</span></span>|<span data-ttu-id="d55c7-112">是</span><span class="sxs-lookup"><span data-stu-id="d55c7-112">Yes</span></span>|<span data-ttu-id="d55c7-113">HTTPS</span><span class="sxs-lookup"><span data-stu-id="d55c7-113">HTTPS</span></span>| 
| |<span data-ttu-id="d55c7-114">"</span><span class="sxs-lookup"><span data-stu-id="d55c7-114">"</span></span> |<span data-ttu-id="d55c7-115">否</span><span class="sxs-lookup"><span data-stu-id="d55c7-115">No</span></span>|<span data-ttu-id="d55c7-116">HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-116">HTTP</span></span>|  
|<span data-ttu-id="d55c7-117">[BasicHttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="d55c7-117">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)</span></span>|<span data-ttu-id="d55c7-118">無論是</span><span class="sxs-lookup"><span data-stu-id="d55c7-118">Either</span></span>|<span data-ttu-id="d55c7-119">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-119">9351/HTTP</span></span>|  
|<span data-ttu-id="d55c7-120">[NetEventRelayBinding 類別](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="d55c7-120">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)</span></span>|<span data-ttu-id="d55c7-121">是</span><span class="sxs-lookup"><span data-stu-id="d55c7-121">Yes</span></span>|<span data-ttu-id="d55c7-122">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="d55c7-122">9351/HTTPS</span></span>|  
||<span data-ttu-id="d55c7-123">"</span><span class="sxs-lookup"><span data-stu-id="d55c7-123">"</span></span> |<span data-ttu-id="d55c7-124">否</span><span class="sxs-lookup"><span data-stu-id="d55c7-124">No</span></span>|<span data-ttu-id="d55c7-125">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-125">9350/HTTP</span></span>|  
|<span data-ttu-id="d55c7-126">[NetEventRelayBinding 類別](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="d55c7-126">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)</span></span>|<span data-ttu-id="d55c7-127">無論是</span><span class="sxs-lookup"><span data-stu-id="d55c7-127">Either</span></span>|<span data-ttu-id="d55c7-128">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-128">9351/HTTP</span></span>|  
|<span data-ttu-id="d55c7-129">[NetTcpRelayBinding 類別](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (用戶端/服務)</span><span class="sxs-lookup"><span data-stu-id="d55c7-129">[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)</span></span>|<span data-ttu-id="d55c7-130">無論是</span><span class="sxs-lookup"><span data-stu-id="d55c7-130">Either</span></span>|<span data-ttu-id="d55c7-131">5671/9352/HTTP (如果使用混合式則為 9352/9353)</span><span class="sxs-lookup"><span data-stu-id="d55c7-131">5671/9352/HTTP (9352/9353 if using hybrid)</span></span>|  
|<span data-ttu-id="d55c7-132">[NetOnewayRelayBinding 類別](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="d55c7-132">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)</span></span>|<span data-ttu-id="d55c7-133">是</span><span class="sxs-lookup"><span data-stu-id="d55c7-133">Yes</span></span>|<span data-ttu-id="d55c7-134">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="d55c7-134">9351/HTTPS</span></span>|  
||<span data-ttu-id="d55c7-135">"</span><span class="sxs-lookup"><span data-stu-id="d55c7-135">"</span></span> |<span data-ttu-id="d55c7-136">否</span><span class="sxs-lookup"><span data-stu-id="d55c7-136">No</span></span>|<span data-ttu-id="d55c7-137">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-137">9350/HTTP</span></span>|  
|<span data-ttu-id="d55c7-138">[NetOnewayRelayBinding 類別](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="d55c7-138">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)</span></span>|<span data-ttu-id="d55c7-139">無論是</span><span class="sxs-lookup"><span data-stu-id="d55c7-139">Either</span></span>|<span data-ttu-id="d55c7-140">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-140">9351/HTTP</span></span>|  
|<span data-ttu-id="d55c7-141">[WebHttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="d55c7-141">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)</span></span>|<span data-ttu-id="d55c7-142">是</span><span class="sxs-lookup"><span data-stu-id="d55c7-142">Yes</span></span>|<span data-ttu-id="d55c7-143">HTTPS</span><span class="sxs-lookup"><span data-stu-id="d55c7-143">HTTPS</span></span>|  
||<span data-ttu-id="d55c7-144">"</span><span class="sxs-lookup"><span data-stu-id="d55c7-144">"</span></span> |<span data-ttu-id="d55c7-145">否</span><span class="sxs-lookup"><span data-stu-id="d55c7-145">No</span></span>|<span data-ttu-id="d55c7-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-146">HTTP</span></span>|  
|<span data-ttu-id="d55c7-147">[WebHttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="d55c7-147">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)</span></span>|<span data-ttu-id="d55c7-148">無論是</span><span class="sxs-lookup"><span data-stu-id="d55c7-148">Either</span></span>|<span data-ttu-id="d55c7-149">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-149">9351/HTTP</span></span>|  
|<span data-ttu-id="d55c7-150">[WS2007HttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="d55c7-150">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)</span></span>|<span data-ttu-id="d55c7-151">是</span><span class="sxs-lookup"><span data-stu-id="d55c7-151">Yes</span></span>|<span data-ttu-id="d55c7-152">HTTPS</span><span class="sxs-lookup"><span data-stu-id="d55c7-152">HTTPS</span></span>|  
||<span data-ttu-id="d55c7-153">"</span><span class="sxs-lookup"><span data-stu-id="d55c7-153">"</span></span> |<span data-ttu-id="d55c7-154">否</span><span class="sxs-lookup"><span data-stu-id="d55c7-154">No</span></span>|<span data-ttu-id="d55c7-155">HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-155">HTTP</span></span>|  
|<span data-ttu-id="d55c7-156">[WS2007HttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="d55c7-156">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)</span></span>|<span data-ttu-id="d55c7-157">無論是</span><span class="sxs-lookup"><span data-stu-id="d55c7-157">Either</span></span>|<span data-ttu-id="d55c7-158">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="d55c7-158">9351/HTTP</span></span>|

## <a name="next-steps"></a><span data-ttu-id="d55c7-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d55c7-159">Next steps</span></span>
<span data-ttu-id="d55c7-160">toolearn 深入了解 Azure 轉送，請前往下列連結：</span><span class="sxs-lookup"><span data-stu-id="d55c7-160">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="d55c7-161">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="d55c7-161">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="d55c7-162">轉送常見問題集</span><span class="sxs-lookup"><span data-stu-id="d55c7-162">Relay FAQ</span></span>](relay-faq.md)