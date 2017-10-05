---
title: "使用 REST API 存取 Azure Mobile Engagement 服務 API"
description: "描述如何使用 Mobile Engagement REST API 存取 Azure Mobile Engagement 服務 API"
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
ms.openlocfilehash: 4b21bca6fee7012ce1dba96950ae075eded414f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="using-rest-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="0cfb6-103">使用 REST 存取 Azure Mobile Engagement 服務 API</span><span class="sxs-lookup"><span data-stu-id="0cfb6-103">Using REST to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="0cfb6-104">Azure Mobile Engagement 提供 [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx)，讓您可以管理裝置、觸達/推送活動等。</span><span class="sxs-lookup"><span data-stu-id="0cfb6-104">Azure Mobile Engagement provides the [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you to manage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="0cfb6-105">Azure Mobile Engagement 服務將於 2018 年 3 月淘汰，目前僅供現有客戶使用。</span><span class="sxs-lookup"><span data-stu-id="0cfb6-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="0cfb6-106">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="0cfb6-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="0cfb6-107">如果您不想直接使用 REST API，我們也提供 [Swagger 檔案](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) ，可以與工具搭配使用來針對您慣用的語言產生 SDK。</span><span class="sxs-lookup"><span data-stu-id="0cfb6-107">If you do not want to use the REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="0cfb6-108">我們建議使用 [AutoRest](https://github.com/Azure/AutoRest) 工具從我們的 Swagger 檔案產生 SDK。</span><span class="sxs-lookup"><span data-stu-id="0cfb6-108">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span> <span data-ttu-id="0cfb6-109">我們已經以類似的方式建立 .NET SDK，可讓您使用 C# 包裝函式與這些 API 互動，且您不需要自行執行驗證權杖交涉和重新整理。</span><span class="sxs-lookup"><span data-stu-id="0cfb6-109">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="0cfb6-110">請參閱[服務 API .NET SDK 範例](mobile-engagement-dotnet-sdk-service-api.md)，以了解如何使用 .NET SDK for API。</span><span class="sxs-lookup"><span data-stu-id="0cfb6-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) to learn how to use the .net SDK for API</span></span>
