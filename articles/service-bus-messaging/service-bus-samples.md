---
title: "aaaAzure 服務匯流排傳訊範例概觀 |Microsoft 文件"
description: "說明 Service Bus 訊息連結 tooeach 樣本"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0b420343-2d2a-4c65-98f1-ee0e39ef55c8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: sethm
ms.openlocfilehash: 6aa3ddca092de7f3ba462e142db7cd333a14d522
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-samples"></a><span data-ttu-id="a1fa3-103">服務匯流排傳訊範例</span><span class="sxs-lookup"><span data-stu-id="a1fa3-103">Service Bus messaging samples</span></span>

<span data-ttu-id="a1fa3-104">hello Service Bus 訊息範例示範中的主要功能[服務匯流排傳訊](https://azure.microsoft.com/services/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-104">hello Service Bus messaging samples demonstrate key features in [Service Bus messaging](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="a1fa3-105">目前，您可以在兩個地方找到 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="a1fa3-105">Currently, you can find hello samples in two places:</span></span>

- <span data-ttu-id="a1fa3-106">[GitHub 上的服務匯流排傳訊範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet)︰較新的範例組，裝載於 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-106">[Service Bus messaging samples on GitHub](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet): a newer set of samples, hosted on GitHub.</span></span> <span data-ttu-id="a1fa3-107">請參閱 hello[讀我檔案](https://github.com/Azure/azure-service-bus/blob/master/samples/DotNet/Microsoft.ServiceBus.Messaging/README.md)hello 儲存機制，如需這些.NET 範例的描述中。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-107">See hello [readme file](https://github.com/Azure/azure-service-bus/blob/master/samples/DotNet/Microsoft.ServiceBus.Messaging/README.md) in hello repo for descriptions of these .NET samples.</span></span> <span data-ttu-id="a1fa3-108">hello 範例會持續更新，因此請經常備份更新。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-108">hello samples are continuously updated, so check back often for updates.</span></span>
- <span data-ttu-id="a1fa3-109">[MSDN 範例頁面](https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=5)： 較舊 live hello MSDN 中的範例程式碼組件庫。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-109">[MSDN samples page](https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=5): older samples that live in hello MSDN code gallery.</span></span> <span data-ttu-id="a1fa3-110">雖然這些範例還能運作，但是它們不會保留，並與尊重 toocurrent 建議的程式設計作法可能已過時。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-110">Although these samples still work, they are not maintained and may be outdated with respect toocurrent recommended programming practices.</span></span>
 
## <a name="service-bus-explorer"></a><span data-ttu-id="a1fa3-111">服務匯流排總管</span><span class="sxs-lookup"><span data-stu-id="a1fa3-111">Service Bus Explorer</span></span>

<span data-ttu-id="a1fa3-112">此外，hello [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer)是可讓您的 GitHub 上裝載的範例 tooconnect tooa 服務匯流排服務命名空間，且輕鬆地管理訊息實體。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-112">In addition, hello [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer) is a sample hosted on GitHub that enables you tooconnect tooa Service Bus service namespace and easily manage messaging entities.</span></span> <span data-ttu-id="a1fa3-113">hello 工具提供進階的功能，例如匯入/匯出功能，和 hello 能力 tootest 訊息實體和轉送服務。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-113">hello tool provides advanced features such as import/export functionality, and hello ability tootest messaging entities and relay services.</span></span> <span data-ttu-id="a1fa3-114">您可以在找到 hello 完整 Service Bus Explorer 原始程式碼和文件[GitHub](https://github.com/paolosalvatori/ServiceBusExplorer)。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-114">You can find hello full Service Bus Explorer source and documentation on [GitHub](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1fa3-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1fa3-115">Next steps</span></span>

<span data-ttu-id="a1fa3-116">範例位置如下︰</span><span class="sxs-lookup"><span data-stu-id="a1fa3-116">Sample locations are here:</span></span>

- [<span data-ttu-id="a1fa3-117">GitHub 範例</span><span class="sxs-lookup"><span data-stu-id="a1fa3-117">GitHub samples</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples)
- [<span data-ttu-id="a1fa3-118">服務匯流排總管</span><span class="sxs-lookup"><span data-stu-id="a1fa3-118">Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer)

<span data-ttu-id="a1fa3-119">請參閱下列主題的服務匯流排概觀 hello。</span><span class="sxs-lookup"><span data-stu-id="a1fa3-119">See hello following topics for conceptual overviews of Service Bus.</span></span>

* [<span data-ttu-id="a1fa3-120">服務匯流排訊息概觀</span><span class="sxs-lookup"><span data-stu-id="a1fa3-120">Service Bus messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="a1fa3-121">服務匯流排架構</span><span class="sxs-lookup"><span data-stu-id="a1fa3-121">Service Bus architecture</span></span>](service-bus-architecture.md)
* [<span data-ttu-id="a1fa3-122">服務匯流排基本概念</span><span class="sxs-lookup"><span data-stu-id="a1fa3-122">Service Bus fundamentals</span></span>](service-bus-fundamentals-hybrid-solutions.md)

