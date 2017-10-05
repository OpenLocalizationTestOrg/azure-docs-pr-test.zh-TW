---
title: "Azure RemoteApp network bandwidth - general guidelines (Azure RemoteApp 網路頻寬 - 一般指導方針) | Microsoft Docs"
description: "了解 Azure RemoteApp 集合和應用程式的一些基本網路頻寬指導方針。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="a5065-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own) (Azure RemoteApp 網路頻寬 - 一般指導方針 (如果您無法自行測試))</span><span class="sxs-lookup"><span data-stu-id="a5065-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a5065-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="a5065-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a5065-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="a5065-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a5065-106">如果您沒有時間或無法執行 Azure RemoteApp 的 [網路頻寬測試](remoteapp-bandwidthtests.md) ，以下是一些相當常用的指導方針，可協助您估計每位使用者的網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="a5065-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="a5065-107">如果您混合使用這些案例，則不建議將小於 (或等於) 10 MB/s 的任何項目用作遠端環境中現代網際網路連線之應用程式的最小網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="a5065-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="a5065-108">(但是，如所述，這不保證會優於一般使用者體驗)。</span><span class="sxs-lookup"><span data-stu-id="a5065-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="a5065-109">複雜 PowerPoint, 簡單 PowerPoint</span><span class="sxs-lookup"><span data-stu-id="a5065-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="a5065-110">Azure RemoteApp 在 100 MB LAN 上運作地最好。</span><span class="sxs-lookup"><span data-stu-id="a5065-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="a5065-111">在 10 MB/s 網路設定檔中，高於 120 毫秒的抖動超過 5% 時，使用者會看到一般體驗。</span><span class="sxs-lookup"><span data-stu-id="a5065-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span></span> <span data-ttu-id="a5065-112">在 1 MB/s 上，差異十分明顯 - 例如，在投影片放映中，使用者可能根本看不到動畫轉換，因為會略過畫面格。</span><span class="sxs-lookup"><span data-stu-id="a5065-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="a5065-113">Internet Explorer, 混合 PDF, PDF, 文字</span><span class="sxs-lookup"><span data-stu-id="a5065-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="a5065-114">10 MB/s 網路設定檔的大部分層面都接近 LAN。</span><span class="sxs-lookup"><span data-stu-id="a5065-114">10 MB/s network profile is close to LAN in most aspects.</span></span> <span data-ttu-id="a5065-115">1 MB/s 將提供正常體驗，但是使用者捲動時可能會有一些抖動，而螢幕上會有影像。</span><span class="sxs-lookup"><span data-stu-id="a5065-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="a5065-116">Flash 視訊 (YouTube)</span><span class="sxs-lookup"><span data-stu-id="a5065-116">Flash video (YouTube)</span></span>
<span data-ttu-id="a5065-117">100 MB/s LAN 提供最佳體驗，而 10 MB/s 為可接受的體驗 (表示可以跟上畫面格速率，但抖動會增加)。</span><span class="sxs-lookup"><span data-stu-id="a5065-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span></span> <span data-ttu-id="a5065-118">在 1 MB/s，抖動狀況極高，而且明顯。</span><span class="sxs-lookup"><span data-stu-id="a5065-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="a5065-119">Word 輸入 (Word 遠端輸入)</span><span class="sxs-lookup"><span data-stu-id="a5065-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="a5065-120">這是低頻寬使用案例。</span><span class="sxs-lookup"><span data-stu-id="a5065-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="a5065-121">在 256 KB/s，我們提供與 LAN 一樣好的體驗。</span><span class="sxs-lookup"><span data-stu-id="a5065-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="a5065-122">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="a5065-122">Learn more</span></span>
* [<span data-ttu-id="a5065-123">Estimate Azure RemoteApp network bandwidth usage (評估 Azure RemoteApp 網路頻寬使用量)</span><span class="sxs-lookup"><span data-stu-id="a5065-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="a5065-124">Azure RemoteApp - how do network bandwidth and quality of experience work together? (Azure RemoteApp - 如何兼顧網路頻寬和體驗品質？)</span><span class="sxs-lookup"><span data-stu-id="a5065-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="a5065-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios (Azure RemoteApp - 利用一些常見案例測試您的網路頻寬使用量)</span><span class="sxs-lookup"><span data-stu-id="a5065-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

