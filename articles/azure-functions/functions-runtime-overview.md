---
title: "Azure Functions 執行階段概觀 | Microsoft Docs"
description: "Azure Functions 執行階段預覽的概觀"
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
ms.openlocfilehash: cb98d5f2aaa526555820c15ba5a32fb7e78ffc5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="4d10c-103">Azure Functions 執行階段概觀</span><span class="sxs-lookup"><span data-stu-id="4d10c-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="4d10c-104">Azure Functions 執行階段提供新的方法，讓您在內部部署利用 Azure Functions 程式設計模型的簡易性和彈性。</span><span class="sxs-lookup"><span data-stu-id="4d10c-104">The Azure Functions Runtime provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="4d10c-105">與 Azure Functions 一樣，Azure Functions 執行階段以相同的開放原始碼根源為基礎，並於內部部署，提供與雲端服務幾乎完全相同的開發經驗。</span><span class="sxs-lookup"><span data-stu-id="4d10c-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Azure Functions 執行階段預覽入口網站][1]

<span data-ttu-id="4d10c-107">Azure Functions 執行階段可讓您先體驗 Azure Functions，再移轉至雲端。</span><span class="sxs-lookup"><span data-stu-id="4d10c-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="4d10c-108">如此一來，您建置的程式碼資產可以隨著您一起移轉至雲端。</span><span class="sxs-lookup"><span data-stu-id="4d10c-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="4d10c-109">此執行階段也提供新的選項，例如，在夜間使用內部部署電腦閒置的計算能力，執行批次程序。</span><span class="sxs-lookup"><span data-stu-id="4d10c-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="4d10c-110">您也可以使用組織內的裝置，依情況將資料傳送至其他系統，包括在內部部署和雲端。</span><span class="sxs-lookup"><span data-stu-id="4d10c-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="4d10c-111">Azure Functions 執行階段包含兩個部分︰</span><span class="sxs-lookup"><span data-stu-id="4d10c-111">The Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="4d10c-112">Azure Functions 執行階段管理角色</span><span class="sxs-lookup"><span data-stu-id="4d10c-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="4d10c-113">Azure Functions 執行階段背景工作角色</span><span class="sxs-lookup"><span data-stu-id="4d10c-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="4d10c-114">Azure Functions 管理角色</span><span class="sxs-lookup"><span data-stu-id="4d10c-114">Azure Functions Management Role</span></span>

<span data-ttu-id="4d10c-115">Azure Functions 管理角色提供主機，讓您在內部部署管理您的 Functions。</span><span class="sxs-lookup"><span data-stu-id="4d10c-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="4d10c-116">此角色執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="4d10c-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="4d10c-117">裝載 Azure Functions 管理入口網站，也就是您在 [Azure 入口網站](https://portal.azure.com)中看到的同一個入口網站。</span><span class="sxs-lookup"><span data-stu-id="4d10c-117">Hosting of the Azure Functions Management Portal, which is the the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4d10c-118">就像在 Azure 入口網站中一樣，這可讓您以相同的方式開發函式。</span><span class="sxs-lookup"><span data-stu-id="4d10c-118">This lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="4d10c-119">將函式分配給多個 Functions 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="4d10c-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="4d10c-120">提供發佈端點，讓您直接從 Microsoft Visual Studio 發佈函式。</span><span class="sxs-lookup"><span data-stu-id="4d10c-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="4d10c-121">Azure Functions 背景工作角色</span><span class="sxs-lookup"><span data-stu-id="4d10c-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="4d10c-122">Azure Functions 背景工作角色部署在 Windows 容器中，您的函式程式碼就在此處執行。</span><span class="sxs-lookup"><span data-stu-id="4d10c-122">The Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="4d10c-123">您可以將多個背景工作角色部署到整個組織中，這也是讓客戶利用閒置計算能力的主要方法。</span><span class="sxs-lookup"><span data-stu-id="4d10c-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="4d10c-124">最低需求</span><span class="sxs-lookup"><span data-stu-id="4d10c-124">Minimum Requirements</span></span>

<span data-ttu-id="4d10c-125">若要開始使用 Azure Functions 執行階段，您必須有一部電腦已安裝 **Windows Server 2016 或 Windows 10 Creators Update** 且可存取 **SQL Server** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="4d10c-125">To get started with the Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access to a **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d10c-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d10c-126">Next Steps</span></span>

<span data-ttu-id="4d10c-127">安裝 [Azure Functions 執行階段預覽](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="4d10c-127">Install the [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
