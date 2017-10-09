---
title: "Azure 雲端服務專案與 Visual Studio aaaCreating |Microsoft 文件"
description: "了解現在 toocreate Visual Studio 中的 Azure 雲端服務專案"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="e3283-103">使用 Visual Studio 建立 Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="e3283-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="e3283-104">hello Azure Tools for Visual Studio 提供可讓您建立 Azure 雲端服務專案範本。</span><span class="sxs-lookup"><span data-stu-id="e3283-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="e3283-105">一旦建立 hello 專案之後，Visual Studio 可讓您 tooconfigure、 偵錯和部署 hello 雲端服務 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="e3283-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="e3283-106">步驟 toocreate Visual Studio 中的 Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="e3283-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="e3283-107">本節將逐步引導您在 Visual Studio 中使用一或多個 Web 角色來建立 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="e3283-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="e3283-108">以系統管理員身分啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e3283-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="e3283-109">Hello 主功能表上，選取**檔案** > **新增** > **專案**。</span><span class="sxs-lookup"><span data-stu-id="e3283-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="e3283-110">選取**雲端**從 hello Visual C# 或 Visual Basic 專案範本節點，然後選取**Azure 雲端服務**從 hello 範本清單。</span><span class="sxs-lookup"><span data-stu-id="e3283-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![新增 Azure 雲端服務](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="e3283-112">指定 hello 您希望 toouse toodevelop 專案的.NET Framework 的版本。</span><span class="sxs-lookup"><span data-stu-id="e3283-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="e3283-113">輸入名稱和您的專案位置和 hello 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="e3283-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="e3283-114">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e3283-114">Select **OK**.</span></span>

1. <span data-ttu-id="e3283-115">在 hello**新 Microsoft Azure 雲端服務**對話方塊中，選取 hello 角色 tooadd，並選擇 hello 向右箭號按鈕 tooadd 它們 tooyour 方案。</span><span class="sxs-lookup"><span data-stu-id="e3283-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![選取新的 Azure 雲端服務角色](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="e3283-117">toorename 角色已新增在 hello hello 角色上的動態顯示**新 Microsoft Azure 雲端服務** 對話方塊中，並從 hello 內容功能表中，選取**重新命名**。</span><span class="sxs-lookup"><span data-stu-id="e3283-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="e3283-118">您可以在您的方案也重新命名角色 (在 hello**方案總管 中**) 已加入之後。</span><span class="sxs-lookup"><span data-stu-id="e3283-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![將 Azure 雲端服務角色重新命名](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="e3283-120">hello Visual Studio Azure 專案中 hello 方案有關聯 toohello 角色專案。</span><span class="sxs-lookup"><span data-stu-id="e3283-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="e3283-121">hello 專案還包括 hello*服務定義檔*和*服務組態檔*:</span><span class="sxs-lookup"><span data-stu-id="e3283-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="e3283-122">**服務定義檔**-定義您的應用程式，包括所需的角色、 端點和虛擬機器大小的 hello 執行階段設定。</span><span class="sxs-lookup"><span data-stu-id="e3283-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="e3283-123">**服務組態檔**-設定多少個角色執行個體執行，hello hello 設定為角色定義的值。</span><span class="sxs-lookup"><span data-stu-id="e3283-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="e3283-124">如需有關這些檔案的詳細資訊，請參閱[使用 Visual Studio 設定 Azure 雲端服務的 hello 角色](vs-azure-tools-configure-roles-for-cloud-service.md)。</span><span class="sxs-lookup"><span data-stu-id="e3283-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3283-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3283-125">Next steps</span></span>
- [<span data-ttu-id="e3283-126">使用 Visual Studio 在 Azure 雲端服務專案中管理角色</span><span class="sxs-lookup"><span data-stu-id="e3283-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
