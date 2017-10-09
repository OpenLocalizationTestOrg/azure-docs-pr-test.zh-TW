---
title: "aaaAzure 函式執行階段概觀 |Microsoft 文件"
description: "Hello Azure 函式執行階段預覽的概觀"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="d91de-103">Azure Functions 執行階段概觀</span><span class="sxs-lookup"><span data-stu-id="d91de-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="d91de-104">hello Azure 函式執行階段提供新方式您 tootake 利用 hello 簡化與彈性 hello Azure 函式程式設計模型內部。</span><span class="sxs-lookup"><span data-stu-id="d91de-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="d91de-105">根據 hello 相同開啟來源根目錄 Azure 函式、 Azure 函式執行階段會在內部部署的 tooprovide 幾乎完全相同的開發經驗 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d91de-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Azure Functions 執行階段預覽入口網站][1]

<span data-ttu-id="d91de-107">hello Azure 函式執行階段會提供讓您 tooexperience Azure 函式的方式，再認可 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="d91de-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="d91de-108">如此一來，可以移轉時，與您 toohello 雲端採取 hello 您建置的程式碼資產。</span><span class="sxs-lookup"><span data-stu-id="d91de-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="d91de-109">hello 執行階段也會開啟新選項，例如整夜使用內部部署電腦 toorun 批次程序的 hello 備用的運算能力。</span><span class="sxs-lookup"><span data-stu-id="d91de-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="d91de-110">您的組織 tooconditionally 傳送資料 tooother 系統內，這兩個內部部署和 hello 雲端中，您也可以使用裝置。</span><span class="sxs-lookup"><span data-stu-id="d91de-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="d91de-111">hello Azure 函式執行階段是由兩個部分所組成：</span><span class="sxs-lookup"><span data-stu-id="d91de-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="d91de-112">Azure Functions 執行階段管理角色</span><span class="sxs-lookup"><span data-stu-id="d91de-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="d91de-113">Azure Functions 執行階段背景工作角色</span><span class="sxs-lookup"><span data-stu-id="d91de-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="d91de-114">Azure Functions 管理角色</span><span class="sxs-lookup"><span data-stu-id="d91de-114">Azure Functions Management Role</span></span>

<span data-ttu-id="d91de-115">hello Azure 函式管理角色提供的函式內部的 hello 管理的主機。</span><span class="sxs-lookup"><span data-stu-id="d91de-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="d91de-116">此角色會執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="d91de-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="d91de-117">裝載的 hello 函式，Azure 管理入口網站即 hello hello 同一個 hello 中看到[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d91de-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d91de-118">這可讓您開發您的函式在 hello 相同方式與在 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d91de-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="d91de-119">將函式分配給多個 Functions 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="d91de-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="d91de-120">提供發佈端點，讓您直接從 Microsoft Visual Studio 發佈函式。</span><span class="sxs-lookup"><span data-stu-id="d91de-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="d91de-121">Azure Functions 背景工作角色</span><span class="sxs-lookup"><span data-stu-id="d91de-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="d91de-122">hello Azure 函式背景工作角色部署 Windows 容器中，並且這是您的函式程式碼執行的位置。</span><span class="sxs-lookup"><span data-stu-id="d91de-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="d91de-123">您可以將多個背景工作角色部署到整個組織中，這也是讓客戶利用閒置計算能力的主要方法。</span><span class="sxs-lookup"><span data-stu-id="d91de-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="d91de-124">最低需求</span><span class="sxs-lookup"><span data-stu-id="d91de-124">Minimum Requirements</span></span>

<span data-ttu-id="d91de-125">tooget 入門 hello Azure 函式執行階段，您必須擁有一部電腦**Windows Server 2016 或 Windows 10 建立者更新**與存取 tooa **SQL Server**執行個體。</span><span class="sxs-lookup"><span data-stu-id="d91de-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d91de-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d91de-126">Next Steps</span></span>

<span data-ttu-id="d91de-127">安裝 hello [Azure 函式執行階段預覽](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="d91de-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
