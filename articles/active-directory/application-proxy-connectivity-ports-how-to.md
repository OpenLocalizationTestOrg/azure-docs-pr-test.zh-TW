---
title: "aaaHow tooopen hello 防火牆連接埠所需的應用程式 Proxy 應用程式 |Microsoft 文件"
description: "正確地找出 hello Azure AD 應用程式 Proxy toowork 的哪些連接埠 tooopen"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="3c8a1-103">如何 tooopen hello 應用程式 Proxy 應用程式所需的防火牆連接埠</span><span class="sxs-lookup"><span data-stu-id="3c8a1-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="3c8a1-104">toosee hello 所需的連接埠和 hello 函式的每個連接埠的完整清單，請參閱 「 hello 必要條件 > 一節的 hello[應用程式 Proxy 的文件](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable)。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="3c8a1-105">請注意，應用程式 Proxy 只會使用輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="3c8a1-106">您也可以檢查是否有所有必要的 hello 連接埠開啟所開啟的 hello[連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)從內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="3c8a1-107">越多的綠色勾選記號，表示越佳的復原功能。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="3c8a1-108">應用程式 Proxy 區域</span><span class="sxs-lookup"><span data-stu-id="3c8a1-108">App Proxy regions</span></span>

<span data-ttu-id="3c8a1-109">我們會努力 toolet 您知道哪些這些區域需要 toobe 綠色為您的方式。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="3c8a1-110">目前，請確定它們全部都是綠色。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-110">For now, make sure they all are.</span></span> <span data-ttu-id="3c8a1-111">無論您位在那個區域，美國中部 (Central US) 都是必要的。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="3c8a1-112">toomake 確定 hello 工具可讓您 hello 正確的結果是，請務必：</span><span class="sxs-lookup"><span data-stu-id="3c8a1-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="3c8a1-113">在瀏覽器從 hello hello 連接器的安裝所在的伺服器上開啟 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="3c8a1-114">請確定連接器還有任何 proxy 或防火牆適用 tooyour 套用 toothis 頁面。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="3c8a1-115">作法是在 Internet Explorer 中移過**設定** - &gt; **網際網路選項** - &gt; **連線**  - &gt; **Lan 設定**。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="3c8a1-116">這個頁面上，您會看到 hello 欄位"使用 Proxy 伺服器為您區域網路 」。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="3c8a1-117">選取此方塊，並置於 hello 「 位址 」 欄位中的 hello proxy 位址。</span><span class="sxs-lookup"><span data-stu-id="3c8a1-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c8a1-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c8a1-118">Next steps</span></span>
[<span data-ttu-id="3c8a1-119">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="3c8a1-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
