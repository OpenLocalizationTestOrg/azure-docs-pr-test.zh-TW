---
title: "Azure Functions 執行階段安裝 | Microsoft Docs"
description: "如何安裝 Azure Functions 執行階段"
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
ms.openlocfilehash: 1e4188313a87d07f396e5f8edc8969dd5da2c436
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="10012-103">安裝 Azure Functions 執行階段預覽</span><span class="sxs-lookup"><span data-stu-id="10012-103">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="10012-104">如果您想要安裝 Azure Functions 執行階段預覽，您必須遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="10012-104">If you would like to install the Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="10012-105">請確定您的電腦符合最低需求</span><span class="sxs-lookup"><span data-stu-id="10012-105">Ensure your machine passes the minimum requirements</span></span>
1. <span data-ttu-id="10012-106">下載 [Azure Functions 執行階段預覽安裝程式](https://aka.ms/azafr)。</span><span class="sxs-lookup"><span data-stu-id="10012-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="10012-107">安裝 Azure Functions 執行階段預覽</span><span class="sxs-lookup"><span data-stu-id="10012-107">Install the Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="10012-108">完成 Azure Functions 執行階段預覽的設定</span><span class="sxs-lookup"><span data-stu-id="10012-108">Complete the configuration of the Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10012-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="10012-109">Prerequisites</span></span>

<span data-ttu-id="10012-110">安裝 Azure Functions 執行階段預覽之前，您必須備妥下列各項：</span><span class="sxs-lookup"><span data-stu-id="10012-110">Before you install the Azure Functions Runtime preview, you must have the following:</span></span>

1. <span data-ttu-id="10012-111">執行 Microsoft Windows Server 2016 或 Microsoft Windows 10 Creators Update (Professional 或 Enterprise Edition) 的電腦。</span><span class="sxs-lookup"><span data-stu-id="10012-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="10012-112">在您的網路內執行的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="10012-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="10012-113">最小版本需求是 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="10012-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="10012-114">安裝 Azure Functions 執行階段預覽</span><span class="sxs-lookup"><span data-stu-id="10012-114">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="10012-115">Azure Functions 執行階段預覽安裝程式會引導您完成安裝 Azure Functions 執行階段預覽版的管理角色和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="10012-115">The Azure Functions Runtime preview installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="10012-116">管理角色和背景工作角色可以安裝在同一部電腦上。</span><span class="sxs-lookup"><span data-stu-id="10012-116">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="10012-117">不過，當您新增更多 Functions 時，您必須將更多背景工作角色部署在其他電腦上，才能將您的函式擴展至多個背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="10012-117">However, as you add more Functions, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="10012-118">在同一部電腦上安裝管理角色和背景工作角色</span><span class="sxs-lookup"><span data-stu-id="10012-118">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="10012-119">執行 Azure Functions 執行階段預覽安裝程式。</span><span class="sxs-lookup"><span data-stu-id="10012-119">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Azure Functions 執行階段預覽安裝程式][1]

1. <span data-ttu-id="10012-121">按 [下一步] 跳過安裝程式的第一個階段</span><span class="sxs-lookup"><span data-stu-id="10012-121">**Click Next** advance past the first stage of the installer</span></span>
1. <span data-ttu-id="10012-122">閱讀 **EULA** 的條款之後，**勾選方塊接受條款**，然後按 [下一步] 前進。</span><span class="sxs-lookup"><span data-stu-id="10012-122">Once you have read the terms of the **EULA**, **check the box** to accept the terms and **click Next** to advance.</span></span>
1. <span data-ttu-id="10012-123">現在，選取您想要在這部電腦上安裝的角色：**Functions 管理角色**及/或 **Functions 背景工作角色**，然後按 [下一步]</span><span class="sxs-lookup"><span data-stu-id="10012-123">Now select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Azure Functions 執行階段預覽安裝程式 - 選取角色][3]

    > [!NOTE]
    > <span data-ttu-id="10012-125">您可以在其他許多電腦上安裝 **Functions 背景工作角色**，若要這樣做，請遵循這些指示，在安裝程式中只選取 [Functions 背景工作角色]。</span><span class="sxs-lookup"><span data-stu-id="10012-125">You can install the **Functions Worker Role** on many other machines to do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="10012-126">按 [下一步]，將**Azure Functions 執行階段安裝程式**安裝在電腦上。</span><span class="sxs-lookup"><span data-stu-id="10012-126">**Click Next** to have the **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="10012-127">完成後，安裝程式將會啟動 **Azure Functions 執行階段設定工具**。</span><span class="sxs-lookup"><span data-stu-id="10012-127">Once complete the installer will launch the **Azure Functions Runtime Configuration tool**.</span></span>

    ![Azure Functions 執行階段預覽安裝程式完成][5]

    > [!NOTE]
    > <span data-ttu-id="10012-129">如果您要安裝在 **Windows 10**，但先前未啟用 [容器] 功能，**Azure Functions 執行階段** 安裝程式會提示您重新開機才能完成安裝。</span><span class="sxs-lookup"><span data-stu-id="10012-129">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime** Installer prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="10012-130">設定 Azure Functions 執行階段</span><span class="sxs-lookup"><span data-stu-id="10012-130">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="10012-131">若要完成 Azure Functions 執行階段安裝，您必須完成設定。</span><span class="sxs-lookup"><span data-stu-id="10012-131">To complete the Azure Functions Runtime installation you must complete the configuration.</span></span>

1. <span data-ttu-id="10012-132">**Azure Functions 執行階段設定工具**會顯示您的電腦上安裝哪些角色。</span><span class="sxs-lookup"><span data-stu-id="10012-132">The **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Azure Functions 執行階段預覽設定工具][6]

1. <span data-ttu-id="10012-134">按一下 [資料庫] 索引標籤，輸入 SQL Server 執行個體的連線詳細資料，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="10012-134">Click the **Database** tab, enter the **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="10012-135">需要如此，Azure Functions 執行階段才能建立資料庫以支援執行階段。</span><span class="sxs-lookup"><span data-stu-id="10012-135">This is required in order to the Azure Functions Runtime to create a database to support the Runtime.</span></span>
    
    ![Azure Functions 執行階段預覽資料庫設定][7]

1. <span data-ttu-id="10012-137">按一下 [認證] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="10012-137">Click the **Credentials** tab.</span></span>  <span data-ttu-id="10012-138">在此畫面上，您必須建立兩個新的認證，以使用 FileShare 來裝載您的所有 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="10012-138">On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="10012-139">在 [檔案共用擁有者] 和 [檔案共用使用者] 中，指定**使用者名稱和密碼**組合，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="10012-139">**Specify Username and Password** combinations for the **File Share Owner** and for the **File Share User** and click **Apply**.</span></span>

    ![Azure Functions 執行階段預覽認證][8]

1. <span data-ttu-id="10012-141">按一下 [檔案共用] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="10012-141">Click the **File Share** tab.</span></span>  <span data-ttu-id="10012-142">在此畫面中，您必須指定 [檔案共用位置] 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="10012-142">In this screen you must specify the details of the **File Share location**.</span></span>  <span data-ttu-id="10012-143">您可以建立此項目，也可以使用現有的檔案共用，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="10012-143">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="10012-144">如果您選取新的檔案共用位置，您必須指定供 Azure Functions 執行階段使用的目錄。</span><span class="sxs-lookup"><span data-stu-id="10012-144">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>
    
    ![Azure Functions 執行階段預覽檔案共用][9]

1. <span data-ttu-id="10012-146">按一下 [IIS] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="10012-146">Click the **IIS** tab.</span></span>  <span data-ttu-id="10012-147">此索引標籤會顯示 IIS 中將建立 Azure Functions 執行階段安裝之網站的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="10012-147">This tab shows the details of the websites in IIS that the Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="10012-148">按一下 [套用] 完成。</span><span class="sxs-lookup"><span data-stu-id="10012-148">**Click Apply** to complete.</span></span>

    ![Azure Functions 執行階段預覽 IIS][10]

1. <span data-ttu-id="10012-150">按一下 [服務] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="10012-150">Click the **Services** tab.</span></span>  <span data-ttu-id="10012-151">此索引標籤會顯示 Azure Functions 執行階段安裝中的服務狀態。</span><span class="sxs-lookup"><span data-stu-id="10012-151">This tab shows the status of the services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="10012-152">初始設定之後，如果 **Azure Functions 主機啟用服務**未執行，請按一下 [啟動服務]</span><span class="sxs-lookup"><span data-stu-id="10012-152">If after initial configuration the **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Azure Functions 執行階段預覽設定完成][11]

1. <span data-ttu-id="10012-154">最後，瀏覽至 **Azure Functions 執行階段入口網站**：`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="10012-154">Finally browse to the **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

    ![Azure Functions 執行階段預覽入口網站][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png