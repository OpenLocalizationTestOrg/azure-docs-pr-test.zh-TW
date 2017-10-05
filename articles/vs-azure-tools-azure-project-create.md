---
title: "使用 Visual Studio 建立 Azure 雲端服務專案 | Microsoft Docs"
description: "立即了解如何使用 Visual Studio 建立 Azure 雲端服務專案"
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
ms.openlocfilehash: 1f6ded87b551f660853ea4eb0548f3d942e28fa8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="64d00-103">使用 Visual Studio 建立 Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="64d00-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="64d00-104">Azure Tools for Visual Studio 提供可讓您建立 Azure 雲端服務的專案範本。</span><span class="sxs-lookup"><span data-stu-id="64d00-104">The Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="64d00-105">一旦建立專案之後，Visual Studio 可讓您對雲端服務進行設定和偵錯，以及部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="64d00-105">Once the project has been created, Visual Studio enables you to configure, debug, and deploy the cloud service to Azure.</span></span>

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="64d00-106">在 Visual Studio 中建立 Azure 雲端服務專案的步驟</span><span class="sxs-lookup"><span data-stu-id="64d00-106">Steps to create an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="64d00-107">本節將逐步引導您在 Visual Studio 中使用一或多個 Web 角色來建立 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="64d00-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="64d00-108">以系統管理員身分啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="64d00-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="64d00-109">在主功能表中，選取 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="64d00-109">On the main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="64d00-110">從 Visual C# 或 Visual Basic 專案範本節點中選取 [雲端]，然後從範本清單中選取 [Azure 雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="64d00-110">Select **Cloud** from the Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from the list of templates.</span></span>

    ![新增 Azure 雲端服務](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="64d00-112">指定您想要用來開發專案的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="64d00-112">Specify which version of the .NET Framework you want to use to develop your project.</span></span>

1. <span data-ttu-id="64d00-113">輸入專案的名稱和位置以及方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="64d00-113">Enter a name and location for your project and a name for the solution.</span></span> 

1. <span data-ttu-id="64d00-114">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="64d00-114">Select **OK**.</span></span>

1. <span data-ttu-id="64d00-115">在 [新增 Microsoft Azure 雲端服務] 對話方塊中，選取您想要新增的角色，然後選擇向右箭號按鈕以將它們新增到您的方案。</span><span class="sxs-lookup"><span data-stu-id="64d00-115">In the **New Microsoft Azure Cloud Service** dialog, select the roles that you want to add, and choose the right arrow button to add them to your solution.</span></span>

    ![選取新的 Azure 雲端服務角色](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="64d00-117">若要將您所新增的角色重新命名，可將滑鼠游標停留在 [新增 Microsoft Azure 雲端服務] 對話方塊中的角色上方，然後從操作功能表中選取[重新命名]。</span><span class="sxs-lookup"><span data-stu-id="64d00-117">To rename a role that you've added, hover on the role in the **New Microsoft Azure Cloud Service** dialog, and, from the context menu, select **Rename**.</span></span> <span data-ttu-id="64d00-118">您也可以在方案內 (在 [方案總管] 中) 為已新增的角色重新命名。</span><span class="sxs-lookup"><span data-stu-id="64d00-118">You can also rename a role within your solution (in the **Solution Explorer**) after it has been added.</span></span>

    ![將 Azure 雲端服務角色重新命名](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="64d00-120">Visual Studio Azure 專案與方案中的角色專案有關。</span><span class="sxs-lookup"><span data-stu-id="64d00-120">The Visual Studio Azure project has associations to the role projects in the solution.</span></span> <span data-ttu-id="64d00-121">專案還包含「服務定義檔」和「服務組態檔」：</span><span class="sxs-lookup"><span data-stu-id="64d00-121">The project also includes the *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="64d00-122">**服務定義檔** - 定義應用程式的執行階段設定，包括需要哪些角色、端點和虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="64d00-122">**Service definition file** - Defines the runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="64d00-123">**服務組態檔** - 設定一個角色可以執行的執行個體數目，以及為角色定義的設定值。</span><span class="sxs-lookup"><span data-stu-id="64d00-123">**Service configuration file** - Configures how many instances of a role are run and the values of the settings defined for a role.</span></span> 

<span data-ttu-id="64d00-124">如需這些檔案的詳細資訊，請參閱[使用 Visual Studio 設定 Azure 雲端服務的角色](vs-azure-tools-configure-roles-for-cloud-service.md)。</span><span class="sxs-lookup"><span data-stu-id="64d00-124">For more information about these files, see [Configure the Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="64d00-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64d00-125">Next steps</span></span>
- [<span data-ttu-id="64d00-126">使用 Visual Studio 在 Azure 雲端服務專案中管理角色</span><span class="sxs-lookup"><span data-stu-id="64d00-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
