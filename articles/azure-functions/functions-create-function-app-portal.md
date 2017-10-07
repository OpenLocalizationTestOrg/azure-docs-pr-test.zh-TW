---
title: "aaaCreate 函式中的應用程式 hello Azure 入口網站 |Microsoft 文件"
description: "Azure App Service 中建立新的函式應用程式，從 hello 入口網站。"
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
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="a67e8-103">建立函式的應用程式從 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a67e8-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="a67e8-104">Azure 的函式應用程式使用 hello Azure 應用程式服務基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a67e8-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="a67e8-105">本主題說明如何 toocreate hello Azure 入口網站中的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="a67e8-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="a67e8-106">函式應用程式是裝載 hello 執行個別的函式的 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="a67e8-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="a67e8-107">當您建立函式應用程式在 hello 應用程式服務的主控方案中時，函式應用程式可以使用應用程式服務的所有 hello 的功能。</span><span class="sxs-lookup"><span data-stu-id="a67e8-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="a67e8-108">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="a67e8-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="a67e8-109">當您建立函數應用程式時，請提供有效的**應用程式名稱**，其中只能包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="a67e8-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="a67e8-110">不允許使用底線 (**_**) 字元。</span><span class="sxs-lookup"><span data-stu-id="a67e8-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="a67e8-111">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="a67e8-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="a67e8-112">儲存體帳戶名稱必須在 Azure 中是獨一無二的。</span><span class="sxs-lookup"><span data-stu-id="a67e8-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="a67e8-113">建立 hello 函式應用程式之後，您可以建立個別的函式中一或多個不同的語言。</span><span class="sxs-lookup"><span data-stu-id="a67e8-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="a67e8-114">建立函式[使用 hello 網站](functions-create-first-azure-function.md#create-function)，[連續部署](functions-continuous-deployment.md)，或由[使用 FTP 上載](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp)。</span><span class="sxs-lookup"><span data-stu-id="a67e8-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="a67e8-115">服務方案</span><span class="sxs-lookup"><span data-stu-id="a67e8-115">Service plans</span></span>

<span data-ttu-id="a67e8-116">Azure Functions 有兩個不同的服務方案︰取用方案和 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="a67e8-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="a67e8-117">當您的程式碼執行時，標尺外必要 toohandle 負載，然後調整-在程式碼未執行時，hello 耗用量計劃自動配置運算能力。</span><span class="sxs-lookup"><span data-stu-id="a67e8-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="a67e8-118">hello App Service 方案可讓您的函式應用程式服務的應用程式存取 tooall hello 設備。</span><span class="sxs-lookup"><span data-stu-id="a67e8-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="a67e8-119">建立您的函數應用程式時，您必須選擇您的服務方案，且目前無法變更。</span><span class="sxs-lookup"><span data-stu-id="a67e8-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="a67e8-120">如需詳細資訊，請參閱[選擇 Azure Functions 主控方案](functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="a67e8-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="a67e8-121">如果您打算 toorun JavaScript 函式上的應用程式服務計劃，您應該選擇具有較少的核心方案。</span><span class="sxs-lookup"><span data-stu-id="a67e8-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="a67e8-122">如需詳細資訊，請參閱 hello [JavaScript 函式的參考](functions-reference-node.md#choose-single-core-app-service-plans)。</span><span class="sxs-lookup"><span data-stu-id="a67e8-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="a67e8-123">儲存體帳戶的需求</span><span class="sxs-lookup"><span data-stu-id="a67e8-123">Storage account requirements</span></span>

<span data-ttu-id="a67e8-124">在建立 App Service 中的函式應用程式，您必須建立或連結 tooa 一般用途 Azure 儲存體帳戶支援 Blob、 佇列和資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="a67e8-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="a67e8-125">Azure Functions 會在內部使用「Azure 儲存體」來進行作業，例如管理觸發程序和記錄函式執行。</span><span class="sxs-lookup"><span data-stu-id="a67e8-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="a67e8-126">有些儲存體帳戶並不支援佇列和表格，例如僅限 Blob 的儲存體帳戶、Azure 進階儲存體和搭配 ZRS 複寫的一般用途儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a67e8-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="a67e8-127">這些帳戶會篩選掉的 hello 儲存體帳戶 刀鋒視窗建立函數應用程式時。</span><span class="sxs-lookup"><span data-stu-id="a67e8-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="a67e8-128">當使用 hello 耗用量主控方案，函式程式碼和繫結組態檔會儲存在 Azure 檔案儲存在 hello 主要儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a67e8-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="a67e8-129">當您刪除 hello 主要儲存體帳戶時，此內容會被刪除，且無法復原。</span><span class="sxs-lookup"><span data-stu-id="a67e8-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="a67e8-130">toolearn 進一步了解儲存體帳戶類型，請參閱[簡介 hello Azure 儲存體服務](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)。</span><span class="sxs-lookup"><span data-stu-id="a67e8-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a67e8-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a67e8-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



