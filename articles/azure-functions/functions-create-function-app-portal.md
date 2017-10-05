---
title: "從 Azure 入口網站建立函數應用程式 | Microsoft Docs"
description: "從入口網站，在 Azure App Service 中建立新的函數應用程式。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 85a88c537415cd6f2b6bc005cc18e3baaa29e9a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-app-from-the-azure-portal"></a><span data-ttu-id="432a6-103">從 Azure 入口網站建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="432a6-103">Create a function app from the Azure portal</span></span>

<span data-ttu-id="432a6-104">Azure 函數應用程式使用 Azure App Service 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="432a6-104">Azure Function Apps uses the Azure App Service infrastructure.</span></span> <span data-ttu-id="432a6-105">本主題說明如何在 Azure 入口網站中建立函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="432a6-105">This topic shows you how to create a function app in the Azure portal.</span></span> <span data-ttu-id="432a6-106">函數應用程式是裝載個別函式執行的容器。</span><span class="sxs-lookup"><span data-stu-id="432a6-106">A function app is the container that hosts the execution of individual functions.</span></span> <span data-ttu-id="432a6-107">當您在 App Service 主控方案中建立函數應用程式時，您的函數應用程式可以使用 App Service 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="432a6-107">When you create a function app in the App Service hosting plan, your function app can use all the features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="432a6-108">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="432a6-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="432a6-109">當您建立函數應用程式時，請提供有效的**應用程式名稱**，其中只能包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="432a6-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="432a6-110">不允許使用底線 (**_**) 字元。</span><span class="sxs-lookup"><span data-stu-id="432a6-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="432a6-111">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="432a6-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="432a6-112">儲存體帳戶名稱必須在 Azure 中是獨一無二的。</span><span class="sxs-lookup"><span data-stu-id="432a6-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="432a6-113">函數應用程式建立之後，您可以使用一或多個不同的語言建立個別的函式。</span><span class="sxs-lookup"><span data-stu-id="432a6-113">After the function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="432a6-114">使用[入口網站](functions-create-first-azure-function.md#create-function)、[連續部署](functions-continuous-deployment.md)或者[透過 FTP 上傳](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp)來建立函式。</span><span class="sxs-lookup"><span data-stu-id="432a6-114">Create functions [by using the portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="432a6-115">服務方案</span><span class="sxs-lookup"><span data-stu-id="432a6-115">Service plans</span></span>

<span data-ttu-id="432a6-116">Azure Functions 有兩個不同的服務方案︰取用方案和 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="432a6-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="432a6-117">取用方案會在您的程式碼執行時自動配置計算能力、視需要相應放大來處理負載，然後在程式碼未執行時相應縮小。</span><span class="sxs-lookup"><span data-stu-id="432a6-117">The Consumption plan automatically allocates compute power when your code is running, scales-out as necessary to handle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="432a6-118">App Service 方案可讓您的函數應用程式存取 App Service 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="432a6-118">The App Service plan gives your function app access to all the facilities of App Service.</span></span> <span data-ttu-id="432a6-119">建立您的函數應用程式時，您必須選擇您的服務方案，且目前無法變更。</span><span class="sxs-lookup"><span data-stu-id="432a6-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="432a6-120">如需詳細資訊，請參閱[選擇 Azure Functions 主控方案](functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="432a6-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="432a6-121">若計畫在 App Service 方案上執行 JavaScript 函式，您應該選擇核心數目較少的方案。</span><span class="sxs-lookup"><span data-stu-id="432a6-121">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="432a6-122">如需詳細資訊，請參閱 [JavaScript 函式參考資料](functions-reference-node.md#choose-single-core-app-service-plans)。</span><span class="sxs-lookup"><span data-stu-id="432a6-122">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="432a6-123">儲存體帳戶需求</span><span class="sxs-lookup"><span data-stu-id="432a6-123">Storage account requirements</span></span>

<span data-ttu-id="432a6-124">在 App Service 中建立函數應用程式時，您必須建立或連結支援 Blob、「佇列」及「表格」儲存體的一般用途「Azure 儲存體」帳戶。</span><span class="sxs-lookup"><span data-stu-id="432a6-124">When creating a function app in App Service, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="432a6-125">Azure Functions 會在內部使用「Azure 儲存體」來進行作業，例如管理觸發程序和記錄函式執行。</span><span class="sxs-lookup"><span data-stu-id="432a6-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="432a6-126">有些儲存體帳戶並不支援佇列和表格，例如僅限 Blob 的儲存體帳戶、Azure 進階儲存體和搭配 ZRS 複寫的一般用途儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="432a6-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="432a6-127">建立函數應用程式時，[儲存體帳戶] 刀鋒視窗中會過濾掉這些帳戶。</span><span class="sxs-lookup"><span data-stu-id="432a6-127">These accounts are filtered out of from the Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="432a6-128">當使用「使用情況主控方案」時，您的函式程式碼和繫結組態檔會儲存在主要儲存體帳戶中的 Azure 檔案儲存體中。</span><span class="sxs-lookup"><span data-stu-id="432a6-128">When using the Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in the main storage account.</span></span> <span data-ttu-id="432a6-129">當您刪除主要儲存體帳戶時，會刪除此內容且無法復原。</span><span class="sxs-lookup"><span data-stu-id="432a6-129">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="432a6-130">若要深入了解儲存體帳戶類型，請參閱 [Azure 儲存體服務簡介](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)。</span><span class="sxs-lookup"><span data-stu-id="432a6-130">To learn more about storage account types, see [Introducing the Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="432a6-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="432a6-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



