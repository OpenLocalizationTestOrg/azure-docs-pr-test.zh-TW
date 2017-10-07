---
title: "在 Azure RemoteApp VNET aaaSizing 資訊 |Microsoft 文件"
description: "深入了解 Azure RemoteApp VNET 執行 hello IP 位址需求"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="6fd02-103">Azure RemoteApp 中 VNET 的大小調整資訊</span><span class="sxs-lookup"><span data-stu-id="6fd02-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6fd02-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="6fd02-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6fd02-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6fd02-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6fd02-106">當您使用 Azure RemoteApp 搭配虛擬網路 (VNET) 時，RemoteApp 會使用 hello 子網路內的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6fd02-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="6fd02-107">根據您的 RemoteApp 服務的 hello 小數位數，必須 tooensure 子網路有足夠可用的 RemoteApp 虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6fd02-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="6fd02-108">雖然此大小調整指導方針未完美地指定 RemoteApp 如何動態旋轉集合內的虛擬機器，但是可協助您估計子網路範圍。</span><span class="sxs-lookup"><span data-stu-id="6fd02-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="6fd02-109">這是因為一旦 RemoteApp 服務放置在 VNET 中，您無法增加 hello 子網路大小，不會移除 RemoteApp 尤其重要。</span><span class="sxs-lookup"><span data-stu-id="6fd02-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="6fd02-110">每個您想要以最大容量 toorun RemoteApp 集合，您應指派 100 可用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6fd02-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="6fd02-111">比方說，如果 hello 標準方案中有一個 RemoteApp 集合，而且您想 toohave hello 上限 500 位使用者，您應該有 100 的 IP 位址，該集合。</span><span class="sxs-lookup"><span data-stu-id="6fd02-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="6fd02-112">同樣地，您需要 100 的 IP 位址的 RemoteApp 集合有 800 使用者 hello 基本計劃中。</span><span class="sxs-lookup"><span data-stu-id="6fd02-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="6fd02-113">如果您計劃 toohave 較少的使用者 （大於或等於最大的 hello），您可以減少每個集合所需的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6fd02-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="6fd02-114">hello 最小的子網路大小需求是 30 個 IP 位址 （/ 27）。</span><span class="sxs-lookup"><span data-stu-id="6fd02-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="6fd02-115">請參閱下列資訊 toomake 確定您的 VNET 設定且運作卻 hello:</span><span class="sxs-lookup"><span data-stu-id="6fd02-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="6fd02-116">從個人的 VNET tooan Azure VNET 移轉</span><span class="sxs-lookup"><span data-stu-id="6fd02-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="6fd02-117">驗證與 Azure RemoteApp 一起 hello Azure VNET toouse</span><span class="sxs-lookup"><span data-stu-id="6fd02-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

