---
title: "Azure 雲端服務專案與 Visual Studio aaaConfigure |Microsoft 文件"
description: "了解如何 tooconfigure Azure 雲端服務 Visual Studio 專案中，根據您針對該專案的需求。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="1a197-103">使用 Visual Studio 來設定 Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="1a197-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="1a197-104">您可以根據 Azure 雲端服務專案的需求來設定專案。</span><span class="sxs-lookup"><span data-stu-id="1a197-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="1a197-105">您可以設定下列類別目錄的 hello 的 hello 專案的屬性：</span><span class="sxs-lookup"><span data-stu-id="1a197-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="1a197-106">**發行雲端服務 tooAzure** -您可以設定屬性 toomake 確定現有的雲端服務部署 tooAzure 不意外刪除。</span><span class="sxs-lookup"><span data-stu-id="1a197-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="1a197-107">**執行或偵錯 hello 本機電腦上的雲端服務**-您可以選取 服務組態 toouse 並指出您是否想 toostart hello Azure 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="1a197-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="1a197-108">**雲端服務封裝時就會建立驗證**-您可以決定的 tootreat 任何警告視為錯誤，讓您可以確保該 hello 雲端服務套件部署沒有任何問題。</span><span class="sxs-lookup"><span data-stu-id="1a197-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="1a197-109">步驟 tooconfigure Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="1a197-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="1a197-110">在 Visual Studio 中開啟或建立雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="1a197-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="1a197-111">在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="1a197-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="1a197-112">在 hello 專案屬性頁面上，選取 hello**開發** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1a197-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![專案屬性功能表](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="1a197-114">設定**刪除現有部署之前提示**太**True**。</span><span class="sxs-lookup"><span data-stu-id="1a197-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="1a197-115">此設定可協助您不小心不要刪除 Azure 中的現有部署 tooensure</span><span class="sxs-lookup"><span data-stu-id="1a197-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="1a197-116">選取所需的 hello**服務組態**tooindicate 哪些服務您想要設定 toouse 當您執行或偵錯您的雲端服務在本機。</span><span class="sxs-lookup"><span data-stu-id="1a197-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="1a197-117">如需有關如何 toomodify 服務組態的角色，請參閱[如何 tooconfigure hello 角色的 Azure 雲端服務與 Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md)。</span><span class="sxs-lookup"><span data-stu-id="1a197-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="1a197-118">設定**啟動 Azure 儲存體模擬器**太**True** toostart hello Azure 儲存體模擬器執行或偵錯雲端服務在本機上時。</span><span class="sxs-lookup"><span data-stu-id="1a197-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="1a197-119">設定**將警告視為錯誤**太**True** toomake 確定您無法發佈套件驗證錯誤時。</span><span class="sxs-lookup"><span data-stu-id="1a197-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="1a197-120">設定**使用 web 專案連接埠**太**True** toomake 確定您的 web 角色會使用相同的每個連接埠的 hello 次在 IIS Express 本機啟動。</span><span class="sxs-lookup"><span data-stu-id="1a197-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="1a197-121">從 hello Visual Studio 工具列上，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="1a197-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a197-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a197-122">Next steps</span></span>
- [<span data-ttu-id="1a197-123">使用多個服務組態設定 Azure 專案</span><span class="sxs-lookup"><span data-stu-id="1a197-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

