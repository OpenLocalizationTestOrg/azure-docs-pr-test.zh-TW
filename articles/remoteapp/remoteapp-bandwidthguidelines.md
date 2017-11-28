---
title: "aaaAzure RemoteApp 網路頻寬的一般指導方針 |Microsoft 文件"
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
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="7b11b-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own) (Azure RemoteApp 網路頻寬 - 一般指導方針 (如果您無法自行測試))</span><span class="sxs-lookup"><span data-stu-id="7b11b-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7b11b-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="7b11b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7b11b-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7b11b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7b11b-106">如果您沒有 hello 時間或功能 toorun hello[網路頻寬測試](remoteapp-bandwidthtests.md)的 Azure RemoteApp，以下是一些相當普遍的指導方針可協助您估計每個使用者的網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="7b11b-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="7b11b-107">如果您有混合的這些案例，我們不建議的任何項目 （或等於） 小於 10 MB/s 為 hello 現代化的網際網路連線應用程式，在遠端環境中的最小網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="7b11b-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="7b11b-108">(但是，如所述，這不保證會優於一般使用者體驗)。</span><span class="sxs-lookup"><span data-stu-id="7b11b-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="7b11b-109">複雜 PowerPoint, 簡單 PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7b11b-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="7b11b-110">Azure RemoteApp 在 100 MB LAN 上運作地最好。</span><span class="sxs-lookup"><span data-stu-id="7b11b-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="7b11b-111">在 hello 10 MB/s 網路設定檔，上述 120 ms 抖動超過 5%時，hello 使用者會看到平均的體驗。</span><span class="sxs-lookup"><span data-stu-id="7b11b-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="7b11b-112">在 1 MB/s hello 不同 glaring-例如，以投影片放映，hello 使用者可能不會看到動畫的轉換完全因為框架會略過。</span><span class="sxs-lookup"><span data-stu-id="7b11b-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="7b11b-113">Internet Explorer, 混合 PDF, PDF, 文字</span><span class="sxs-lookup"><span data-stu-id="7b11b-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="7b11b-114">10 MB/s 的網路設定檔是關閉 tooLAN 在大部分的層面。</span><span class="sxs-lookup"><span data-stu-id="7b11b-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="7b11b-115">1 MB/s 會提供 [確定] 的經驗，雖然可能會有一些抖動使用者捲動時囉 」 畫面上沒有映像時。</span><span class="sxs-lookup"><span data-stu-id="7b11b-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="7b11b-116">Flash 視訊 (YouTube)</span><span class="sxs-lookup"><span data-stu-id="7b11b-116">Flash video (YouTube)</span></span>
<span data-ttu-id="7b11b-117">100 MB/s LAN 提供 hello 獲得最佳經驗，而 10 MB/s 為可接受 （表示我們跟上 hello 畫面播放速率，但抖動增加）。</span><span class="sxs-lookup"><span data-stu-id="7b11b-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="7b11b-118">在 1 MB/s，抖動狀況極高，而且明顯。</span><span class="sxs-lookup"><span data-stu-id="7b11b-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="7b11b-119">Word 輸入 (Word 遠端輸入)</span><span class="sxs-lookup"><span data-stu-id="7b11b-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="7b11b-120">這是低頻寬使用案例。</span><span class="sxs-lookup"><span data-stu-id="7b11b-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="7b11b-121">在 256 KB/s，我們提供與 LAN 一樣好的體驗。</span><span class="sxs-lookup"><span data-stu-id="7b11b-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="7b11b-122">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="7b11b-122">Learn more</span></span>
* [<span data-ttu-id="7b11b-123">Estimate Azure RemoteApp network bandwidth usage (評估 Azure RemoteApp 網路頻寬使用量)</span><span class="sxs-lookup"><span data-stu-id="7b11b-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="7b11b-124">Azure RemoteApp - how do network bandwidth and quality of experience work together? (Azure RemoteApp - 如何兼顧網路頻寬和體驗品質？)</span><span class="sxs-lookup"><span data-stu-id="7b11b-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="7b11b-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios (Azure RemoteApp - 利用一些常見案例測試您的網路頻寬使用量)</span><span class="sxs-lookup"><span data-stu-id="7b11b-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

