---
title: "連接埠和 Url toowhitelist 的 Azure RemoteApp 部署客戶虛擬網路中的 aaaList |Microsoft 文件"
description: "了解哪些連接埠及所需的通訊透過 Azure RemoteApp tooconfigure 的 Url。"
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
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="8db7c-103">清單中的連接埠和 Url toopermit 存取的 Azure RemoteApp 部署客戶虛擬網路中</span><span class="sxs-lookup"><span data-stu-id="8db7c-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8db7c-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="8db7c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8db7c-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8db7c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8db7c-106">如果您要部署的虛擬網路 (VNET) 中的 Azure RemoteApp 雲端或混合式集合，請檢閱下列連接埠資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="8db7c-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="8db7c-107">如需虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8db7c-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="8db7c-108">如果您已經建立網路安全性群組 (NSG) 限制您的集合中的流量 toohello 虛擬網路資源，請確定下列連接埠的 hello 可存取、 允許透過 hello hello 虛擬網路上的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="8db7c-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="8db7c-109">如需網路安全性群組的詳細資訊，請參閱[什麼是網路安全性群組？(NSG)？](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="8db7c-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="8db7c-110">Azure RemoteApp 的子網路必須存取 toothese 端點和 Url:</span><span class="sxs-lookup"><span data-stu-id="8db7c-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="8db7c-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="8db7c-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="8db7c-112">*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="8db7c-112">*.servicebus.net</span></span>
* <span data-ttu-id="8db7c-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="8db7c-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="8db7c-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="8db7c-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="8db7c-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="8db7c-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="8db7c-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="8db7c-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="8db7c-117">輸出：TCP：443、9351、9352、10101-10175</span><span class="sxs-lookup"><span data-stu-id="8db7c-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="8db7c-118">選用 – UDP：10201-10275</span><span class="sxs-lookup"><span data-stu-id="8db7c-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="8db7c-119">Azure RemoteApp 用戶端需要存取 toothese 端點和 Url:</span><span class="sxs-lookup"><span data-stu-id="8db7c-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="8db7c-120">我是說 hello 等該人員的桌面裝置的用戶端使用 tooconnect toohello 應用程式部署在 hello Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="8db7c-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="8db7c-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="8db7c-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="8db7c-122">https://*.remoteapp.windowsazure.com （此位址是 hello 選擇性 UDP 連接埠）</span><span class="sxs-lookup"><span data-stu-id="8db7c-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="8db7c-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="8db7c-123">https://login.windows.net</span></span>  
* <span data-ttu-id="8db7c-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="8db7c-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="8db7c-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="8db7c-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="8db7c-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="8db7c-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="8db7c-127">輸出：TCP：443</span><span class="sxs-lookup"><span data-stu-id="8db7c-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="8db7c-128">選用 - UDP：3391</span><span class="sxs-lookup"><span data-stu-id="8db7c-128">Optional - UDP: 3391</span></span> 

