---
title: "Azure 轉送連接埠設定 | Microsoft Docs"
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
ms.openlocfilehash: 5906495c565dad583e74a43b2e5eed57e0c68df1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-port-settings"></a><span data-ttu-id="3c413-103">Azure 轉送連接埠設定</span><span class="sxs-lookup"><span data-stu-id="3c413-103">Azure Relay port settings</span></span>

<span data-ttu-id="3c413-104">下表說明 Azure 轉送的連接埠值所需的設定。</span><span class="sxs-lookup"><span data-stu-id="3c413-104">The following table describes the required configuration for port values for Azure Relay.</span></span>

## <a name="hybrid-connections"></a><span data-ttu-id="3c413-105">混合式連線</span><span class="sxs-lookup"><span data-stu-id="3c413-105">Hybrid Connections</span></span>
<span data-ttu-id="3c413-106">混合式連線使用 WebSockets 做為基礎傳輸機制，僅使用 **HTTPS**。</span><span class="sxs-lookup"><span data-stu-id="3c413-106">Hybrid Connections uses WebSockets as the underlying transport mechanism, which uses **HTTPS** only.</span></span> 

## <a name="wcf-relays"></a><span data-ttu-id="3c413-107">WCF 轉送</span><span class="sxs-lookup"><span data-stu-id="3c413-107">WCF Relays</span></span>
  
|<span data-ttu-id="3c413-108">繫結</span><span class="sxs-lookup"><span data-stu-id="3c413-108">Binding</span></span>|<span data-ttu-id="3c413-109">傳輸安全性</span><span class="sxs-lookup"><span data-stu-id="3c413-109">Transport Security</span></span>|<span data-ttu-id="3c413-110">連接埠</span><span class="sxs-lookup"><span data-stu-id="3c413-110">Port</span></span>|  
|-------------|------------------------|----------|  
|<span data-ttu-id="3c413-111">[BasicHttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="3c413-111">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)</span></span>|<span data-ttu-id="3c413-112">是</span><span class="sxs-lookup"><span data-stu-id="3c413-112">Yes</span></span>|<span data-ttu-id="3c413-113">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3c413-113">HTTPS</span></span>| 
| |<span data-ttu-id="3c413-114">"</span><span class="sxs-lookup"><span data-stu-id="3c413-114">"</span></span> |<span data-ttu-id="3c413-115">否</span><span class="sxs-lookup"><span data-stu-id="3c413-115">No</span></span>|<span data-ttu-id="3c413-116">HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-116">HTTP</span></span>|  
|<span data-ttu-id="3c413-117">[BasicHttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="3c413-117">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)</span></span>|<span data-ttu-id="3c413-118">無論是</span><span class="sxs-lookup"><span data-stu-id="3c413-118">Either</span></span>|<span data-ttu-id="3c413-119">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-119">9351/HTTP</span></span>|  
|<span data-ttu-id="3c413-120">[NetEventRelayBinding 類別](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="3c413-120">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)</span></span>|<span data-ttu-id="3c413-121">是</span><span class="sxs-lookup"><span data-stu-id="3c413-121">Yes</span></span>|<span data-ttu-id="3c413-122">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="3c413-122">9351/HTTPS</span></span>|  
||<span data-ttu-id="3c413-123">"</span><span class="sxs-lookup"><span data-stu-id="3c413-123">"</span></span> |<span data-ttu-id="3c413-124">否</span><span class="sxs-lookup"><span data-stu-id="3c413-124">No</span></span>|<span data-ttu-id="3c413-125">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-125">9350/HTTP</span></span>|  
|<span data-ttu-id="3c413-126">[NetEventRelayBinding 類別](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="3c413-126">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)</span></span>|<span data-ttu-id="3c413-127">無論是</span><span class="sxs-lookup"><span data-stu-id="3c413-127">Either</span></span>|<span data-ttu-id="3c413-128">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-128">9351/HTTP</span></span>|  
|<span data-ttu-id="3c413-129">[NetTcpRelayBinding 類別](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (用戶端/服務)</span><span class="sxs-lookup"><span data-stu-id="3c413-129">[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)</span></span>|<span data-ttu-id="3c413-130">無論是</span><span class="sxs-lookup"><span data-stu-id="3c413-130">Either</span></span>|<span data-ttu-id="3c413-131">5671/9352/HTTP (如果使用混合式則為 9352/9353)</span><span class="sxs-lookup"><span data-stu-id="3c413-131">5671/9352/HTTP (9352/9353 if using hybrid)</span></span>|  
|<span data-ttu-id="3c413-132">[NetOnewayRelayBinding 類別](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="3c413-132">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)</span></span>|<span data-ttu-id="3c413-133">是</span><span class="sxs-lookup"><span data-stu-id="3c413-133">Yes</span></span>|<span data-ttu-id="3c413-134">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="3c413-134">9351/HTTPS</span></span>|  
||<span data-ttu-id="3c413-135">"</span><span class="sxs-lookup"><span data-stu-id="3c413-135">"</span></span> |<span data-ttu-id="3c413-136">否</span><span class="sxs-lookup"><span data-stu-id="3c413-136">No</span></span>|<span data-ttu-id="3c413-137">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-137">9350/HTTP</span></span>|  
|<span data-ttu-id="3c413-138">[NetOnewayRelayBinding 類別](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="3c413-138">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)</span></span>|<span data-ttu-id="3c413-139">無論是</span><span class="sxs-lookup"><span data-stu-id="3c413-139">Either</span></span>|<span data-ttu-id="3c413-140">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-140">9351/HTTP</span></span>|  
|<span data-ttu-id="3c413-141">[WebHttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="3c413-141">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)</span></span>|<span data-ttu-id="3c413-142">是</span><span class="sxs-lookup"><span data-stu-id="3c413-142">Yes</span></span>|<span data-ttu-id="3c413-143">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3c413-143">HTTPS</span></span>|  
||<span data-ttu-id="3c413-144">"</span><span class="sxs-lookup"><span data-stu-id="3c413-144">"</span></span> |<span data-ttu-id="3c413-145">否</span><span class="sxs-lookup"><span data-stu-id="3c413-145">No</span></span>|<span data-ttu-id="3c413-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-146">HTTP</span></span>|  
|<span data-ttu-id="3c413-147">[WebHttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="3c413-147">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)</span></span>|<span data-ttu-id="3c413-148">無論是</span><span class="sxs-lookup"><span data-stu-id="3c413-148">Either</span></span>|<span data-ttu-id="3c413-149">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-149">9351/HTTP</span></span>|  
|<span data-ttu-id="3c413-150">[WS2007HttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (用戶端)</span><span class="sxs-lookup"><span data-stu-id="3c413-150">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)</span></span>|<span data-ttu-id="3c413-151">是</span><span class="sxs-lookup"><span data-stu-id="3c413-151">Yes</span></span>|<span data-ttu-id="3c413-152">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3c413-152">HTTPS</span></span>|  
||<span data-ttu-id="3c413-153">"</span><span class="sxs-lookup"><span data-stu-id="3c413-153">"</span></span> |<span data-ttu-id="3c413-154">否</span><span class="sxs-lookup"><span data-stu-id="3c413-154">No</span></span>|<span data-ttu-id="3c413-155">HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-155">HTTP</span></span>|  
|<span data-ttu-id="3c413-156">[WS2007HttpRelayBinding 類別](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (服務)</span><span class="sxs-lookup"><span data-stu-id="3c413-156">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)</span></span>|<span data-ttu-id="3c413-157">無論是</span><span class="sxs-lookup"><span data-stu-id="3c413-157">Either</span></span>|<span data-ttu-id="3c413-158">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="3c413-158">9351/HTTP</span></span>|

## <a name="next-steps"></a><span data-ttu-id="3c413-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c413-159">Next steps</span></span>
<span data-ttu-id="3c413-160">若要深入了解 Azure 轉送，請造訪下列連結：</span><span class="sxs-lookup"><span data-stu-id="3c413-160">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="3c413-161">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="3c413-161">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="3c413-162">轉送常見問題集</span><span class="sxs-lookup"><span data-stu-id="3c413-162">Relay FAQ</span></span>](relay-faq.md)