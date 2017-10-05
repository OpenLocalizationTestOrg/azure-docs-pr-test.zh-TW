---
title: "加入客戶虛擬網路中部署的 Azure RemoteApp 白名單的連接埠和 URL 清單 | Microsoft Docs"
description: "了解您必須設定哪些連接埠及 URL，才能透過 Azure RemoteApp 進行通訊。"
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="60dc6-103">允許存取客戶虛擬網路中部署的 Azure RemoteApp 的連接埠和 URL 清單</span><span class="sxs-lookup"><span data-stu-id="60dc6-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="60dc6-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="60dc6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="60dc6-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="60dc6-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="60dc6-106">如果您要在虛擬網路 (VNET) 中部署 Azure RemoteApp 雲端或混合式集合，請看以下的連接埠資訊。</span><span class="sxs-lookup"><span data-stu-id="60dc6-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span></span> <span data-ttu-id="60dc6-107">如需虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="60dc6-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="60dc6-108">如果您已經建立網路安全性群組 (NSG) 來限制流向您的集合中虛擬網路資源的流量，請確定可透過虛擬網路上的安全性原則存取並允許使用以下連接埠。</span><span class="sxs-lookup"><span data-stu-id="60dc6-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span></span> <span data-ttu-id="60dc6-109">如需網路安全性群組的詳細資訊，請參閱[什麼是網路安全性群組？(NSG)？](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="60dc6-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a><span data-ttu-id="60dc6-110">Azure RemoteApp 子網路必須存取以下端點和 URL：</span><span class="sxs-lookup"><span data-stu-id="60dc6-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span></span>
* <span data-ttu-id="60dc6-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="60dc6-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="60dc6-112">*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="60dc6-112">*.servicebus.net</span></span>
* <span data-ttu-id="60dc6-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="60dc6-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="60dc6-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="60dc6-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="60dc6-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="60dc6-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="60dc6-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="60dc6-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="60dc6-117">輸出：TCP：443、9351、9352、10101-10175</span><span class="sxs-lookup"><span data-stu-id="60dc6-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="60dc6-118">選用 – UDP：10201-10275</span><span class="sxs-lookup"><span data-stu-id="60dc6-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a><span data-ttu-id="60dc6-119">Azure RemoteApp 用戶端必須存取以下端點和 URL：</span><span class="sxs-lookup"><span data-stu-id="60dc6-119">Azure RemoteApp clients need access to these endpoints and URLs:</span></span>
<span data-ttu-id="60dc6-120">這裡的用戶端指的是使用者用來連線到 Azure RemoteApp 集合中部署應用程式的桌上型電腦、裝置等等。</span><span class="sxs-lookup"><span data-stu-id="60dc6-120">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span></span>

* <span data-ttu-id="60dc6-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="60dc6-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="60dc6-122">https://*.remoteapp.windowsazure.com (選用的 UDP 連接埠是供此位址使用)</span><span class="sxs-lookup"><span data-stu-id="60dc6-122">https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="60dc6-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="60dc6-123">https://login.windows.net</span></span>  
* <span data-ttu-id="60dc6-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="60dc6-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="60dc6-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="60dc6-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="60dc6-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="60dc6-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="60dc6-127">輸出：TCP：443</span><span class="sxs-lookup"><span data-stu-id="60dc6-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="60dc6-128">選用 - UDP：3391</span><span class="sxs-lookup"><span data-stu-id="60dc6-128">Optional - UDP: 3391</span></span> 

