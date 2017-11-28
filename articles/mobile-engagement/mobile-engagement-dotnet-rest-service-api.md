---
title: "aaaUsing hello REST API tooaccess Azure Mobile Engagement 服務 Api"
description: "描述如何 toouse hello Mobile Engagement REST Api tooaccess Azure Mobile Engagement 服務 Api"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="00de3-103">使用 REST tooaccess Azure Mobile Engagement 服務 Api</span><span class="sxs-lookup"><span data-stu-id="00de3-103">Using REST tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="00de3-104">Azure Mobile Engagement 提供 hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx)您 toomanage 裝置觸達/推送活動等等。</span><span class="sxs-lookup"><span data-stu-id="00de3-104">Azure Mobile Engagement provides hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you toomanage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="00de3-105">hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。</span><span class="sxs-lookup"><span data-stu-id="00de3-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="00de3-106">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="00de3-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="00de3-107">如果您不要 toouse hello REST Api 直接，我們也提供[Swagger 檔案](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json)您可以使用工具 toogenerate Sdk 您慣用的語言。</span><span class="sxs-lookup"><span data-stu-id="00de3-107">If you do not want toouse hello REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="00de3-108">我們建議您使用 hello [AutoRest](https://github.com/Azure/AutoRest)工具 toogenerate 我們的 Swagger 檔案從您的 SDK。</span><span class="sxs-lookup"><span data-stu-id="00de3-108">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span> <span data-ttu-id="00de3-109">我們也可以建立類似的方式可讓您 toointeract 使用這些 Api 的 C# 包裝函式的使用.NET SDK，而且不需要 toodo hello 驗證語彙基元交涉並重新整理自己。</span><span class="sxs-lookup"><span data-stu-id="00de3-109">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="00de3-110">請參閱[服務應用程式開發介面.NET sdk > 範例的](mobile-engagement-dotnet-sdk-service-api.md)toolearn toouse hello.net SDK 的應用程式開發介面的方式</span><span class="sxs-lookup"><span data-stu-id="00de3-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn how toouse hello .net SDK for API</span></span>
