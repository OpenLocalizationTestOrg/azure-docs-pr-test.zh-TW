---
title: "aaaAn 應用程式 Proxy 應用程式會採用太長 tooload |Microsoft 文件"
description: "疑難排解 hello Azure AD Application Proxy 的頁面載入效能問題"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="f0a92-103">應用程式 Proxy 應用程式便會太長 tooload</span><span class="sxs-lookup"><span data-stu-id="f0a92-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="f0a92-104">本文將協助您 toounderstand 為什麼 Azure AD Application Proxy 應用程式可能需要很長的時間 tooload，以及您可以執行 tooresolve 此問題。</span><span class="sxs-lookup"><span data-stu-id="f0a92-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="f0a92-105">概觀</span><span class="sxs-lookup"><span data-stu-id="f0a92-105">Overview</span></span>
<span data-ttu-id="f0a92-106">如果正在您的應用程式，但您會看到很長的延遲，您可以考慮 tooimprove hello 速度的網路拓撲中可能有做一些調整。</span><span class="sxs-lookup"><span data-stu-id="f0a92-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="f0a92-107">評估不同拓撲，請參閱 hello[網路考量文件](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations)。</span><span class="sxs-lookup"><span data-stu-id="f0a92-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="f0a92-108">如果這些考量沒有幫助，很抱歉我們目前對於效能調整沒有進一步的建議。</span><span class="sxs-lookup"><span data-stu-id="f0a92-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="f0a92-109">由於 hello 應用程式 Proxy 服務會展開，可能會更接近 tooyou toomore 資料中心，您可能會直接啟動 toosee 改善延遲。</span><span class="sxs-lookup"><span data-stu-id="f0a92-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="f0a92-110">toosee hello 的完整清單 Azure 資料中心，您可以查看 hello[延遲測試頁](http://www.azurespeed.com/Azure/Latency)。</span><span class="sxs-lookup"><span data-stu-id="f0a92-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="f0a92-111">hello 與 hello 應用程式 Proxy 服務的資料中心可以找到以 hello[連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)。</span><span class="sxs-lookup"><span data-stu-id="f0a92-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="f0a92-112">對 Application Proxy 資料中心位置的意見反應</span><span class="sxs-lookup"><span data-stu-id="f0a92-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="f0a92-113">可能還不包括應用程式 Proxy，但結果可能會導致 tooa 絕佳延遲改善您的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="f0a92-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="f0a92-114">hello 資料中心位置< aadapfeedback@microsoft.com >讓我們可做為您的意見反應 tooplan 我們展開。</span><span class="sxs-lookup"><span data-stu-id="f0a92-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="f0a92-115">我們使用一些其他功能，可協助改善 hello 延遲目前看到很長的延遲時間的租用戶，而且是確定 tooshare 文件之後使用。</span><span class="sxs-lookup"><span data-stu-id="f0a92-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0a92-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0a92-116">Next steps</span></span>
[<span data-ttu-id="f0a92-117">使用現有的內部部署 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="f0a92-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
