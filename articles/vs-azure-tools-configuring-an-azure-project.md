---
title: "使用 Visual Studio 來設定 Azure 雲端服務專案 | Microsoft Docs"
description: "了解如何在 Visual Studio 中根據 Azure 雲端服務專案的需求來設定專案。"
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
ms.openlocfilehash: 799715093bd1a8c8e77e6cdb7168670dc263dfa5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="13337-103">使用 Visual Studio 來設定 Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="13337-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="13337-104">您可以根據 Azure 雲端服務專案的需求來設定專案。</span><span class="sxs-lookup"><span data-stu-id="13337-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="13337-105">您可以設定下列類別的專案的屬性：</span><span class="sxs-lookup"><span data-stu-id="13337-105">You can set properties for the project for the following categories:</span></span>

- <span data-ttu-id="13337-106">**將雲端服務發佈至 Azure** - 您可以設定屬性以確保部署至 Azure 的現有雲端服務不會被意外刪除。</span><span class="sxs-lookup"><span data-stu-id="13337-106">**Publish a cloud service to Azure** - You can set a property to make sure that an existing cloud service deployed to Azure is not accidentally deleted.</span></span>
- <span data-ttu-id="13337-107">**在本機電腦上執行雲端服務或對其進行偵錯** - 您可以選取一個要使用的服務組態，並指示是否要啟動 Azure 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="13337-107">**Run or debug a cloud service on the local computer** - You can select a service configuration to use and indicate whether you want to start the Azure storage emulator.</span></span>
- <span data-ttu-id="13337-108">**在建立雲端服務套件時加以驗證** - 您可以決定將任何警告都視為錯誤，以便確保在部署雲端服務套件時不會發生任何問題。</span><span class="sxs-lookup"><span data-stu-id="13337-108">**Validate a cloud service package when it is created** - You can decide to treat any warnings as errors so that you can ensure that the cloud service package deploys without any issues.</span></span> 

## <a name="steps-to-configure-an-azure-cloud-service-project"></a><span data-ttu-id="13337-109">設定 Azure 雲端服務專案的步驟</span><span class="sxs-lookup"><span data-stu-id="13337-109">Steps to configure an Azure cloud service project</span></span>
1. <span data-ttu-id="13337-110">在 Visual Studio 中開啟或建立雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="13337-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="13337-111">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後從操作功能表中選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="13337-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="13337-112">在專案的屬性頁面中，選取 [開發] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="13337-112">In the project's properties page, select the **Development** tab.</span></span>

    ![專案屬性功能表](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="13337-114">將 [刪除現有部署前先提示] 設定為 [True]。</span><span class="sxs-lookup"><span data-stu-id="13337-114">Set **Prompt before deleting an existing deployment** to **True**.</span></span> <span data-ttu-id="13337-115">這項設定可協助確保您不會意外刪除 Azure 中現有的部署</span><span class="sxs-lookup"><span data-stu-id="13337-115">This setting helps to ensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="13337-116">選取想要的 [服務組態]，以指出您在本機執行雲端服務或對其進行偵錯時，所想要使用的服務組態。</span><span class="sxs-lookup"><span data-stu-id="13337-116">Select the desired **Service configuration** to indicate which service configuration you want to use when you run or debug your cloud service locally.</span></span> <span data-ttu-id="13337-117">如需有關如何修改某個角色之服務組態的詳細資訊，請參閱[如何使用 Visual Studio 來設定 Azure 雲端服務的角色](./vs-azure-tools-configure-roles-for-cloud-service.md)。</span><span class="sxs-lookup"><span data-stu-id="13337-117">For more information on how to modify a service configuration for a role, see [How to configure the roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="13337-118">將 [啟動 Azure 儲存體模擬器] 設定為 [True]，以在您於本機執行雲端服務或對其進行偵錯時，啟動 Azure 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="13337-118">Set **Start Azure storage emulator** to **True** to start the Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="13337-119">將 [將警告視為錯誤] 設定為 [True]，以確保您在套件驗證發生錯誤時無法發佈。</span><span class="sxs-lookup"><span data-stu-id="13337-119">Set **Treat warnings as errors** to **True** to make sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="13337-120">將 [使用 Web 專案連接埠] 設定為 [True]，以確保您的 Web 角色每次在 IIS Express 中於本機啟動時都使用相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="13337-120">Set **Use web project ports** to **True** to make sure that your web role uses the same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="13337-121">從 Visual Studio 工具列中，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="13337-121">From the Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13337-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13337-122">Next steps</span></span>
- [<span data-ttu-id="13337-123">使用多個服務組態設定 Azure 專案</span><span class="sxs-lookup"><span data-stu-id="13337-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

