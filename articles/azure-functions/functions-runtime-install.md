---
title: "aaaAzure 函式執行階段安裝 |Microsoft 文件"
description: "如何 tooInstall hello Azure 函式執行階段"
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
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="2a1b9-103">安裝 hello Azure 函式執行階段預覽</span><span class="sxs-lookup"><span data-stu-id="2a1b9-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="2a1b9-104">如果您想要 tooinstall hello Azure 函式執行階段預覽，您必須遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2a1b9-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="2a1b9-105">請確定您的電腦傳送 hello 最低需求</span><span class="sxs-lookup"><span data-stu-id="2a1b9-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="2a1b9-106">下載 hello [Azure 函式執行階段 Preview 安裝程式](https://aka.ms/azafr)。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="2a1b9-107">安裝 hello Azure 函式執行階段 preview</span><span class="sxs-lookup"><span data-stu-id="2a1b9-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="2a1b9-108">Hello Azure 函式執行階段預覽的完整 hello 組態</span><span class="sxs-lookup"><span data-stu-id="2a1b9-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a1b9-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a1b9-109">Prerequisites</span></span>

<span data-ttu-id="2a1b9-110">安裝 hello Azure 函式執行階段預覽之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2a1b9-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="2a1b9-111">執行 Microsoft Windows Server 2016 或 Microsoft Windows 10 Creators Update (Professional 或 Enterprise Edition) 的電腦。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="2a1b9-112">在您的網路內執行的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="2a1b9-113">最小版本需求是 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="2a1b9-114">安裝 hello Azure 函式執行階段預覽</span><span class="sxs-lookup"><span data-stu-id="2a1b9-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="2a1b9-115">hello Azure 函式執行階段 preview 安裝程式會引導您完成 hello hello Azure 函式執行階段預覽管理和背景工作角色的安裝。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="2a1b9-116">它是可能 tooinstall hello 管理和背景工作角色上 hello 同一部電腦。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="2a1b9-117">不過，當您加入多個函式，您必須部署多個背景工作角色上的其他電腦 toobe 無法 tooscale 到多個背景工作函式。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="2a1b9-118">Hello 上安裝 hello 管理和背景工作角色相同的電腦</span><span class="sxs-lookup"><span data-stu-id="2a1b9-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="2a1b9-119">執行 hello Azure 函式執行階段 Preview 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Azure Functions 執行階段預覽安裝程式][1]

1. <span data-ttu-id="2a1b9-121">**按一下 下一步**前進過去 hello 第一個階段中的 hello 安裝程式</span><span class="sxs-lookup"><span data-stu-id="2a1b9-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="2a1b9-122">一旦您已經讀取的 hello hello 條款**EULA**，**核取方塊 hello** tooaccept hello 條款和**按下一步**tooadvance。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="2a1b9-123">現在選取 hello 角色您想在這部電腦上的 tooinstall**函式管理角色**及/或**函式背景工作角色**和**按一下 [下一步]**</span><span class="sxs-lookup"><span data-stu-id="2a1b9-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Azure Functions 執行階段預覽安裝程式 - 選取角色][3]

    > [!NOTE]
    > <span data-ttu-id="2a1b9-125">您可以安裝 hello**函式背景工作角色**在許多其他機器 toodo 因此，請遵循這些指示，然後只選取**函式背景工作角色**hello 安裝程式中。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="2a1b9-126">**按一下 下一步**toohave hello **Azure 函式執行階段安裝程式**在電腦上安裝。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="2a1b9-127">一旦完成 hello 安裝程式將會啟動 hello **Azure 函式執行階段組態工具**。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Azure Functions 執行階段預覽安裝程式完成][5]

    > [!NOTE]
    > <span data-ttu-id="2a1b9-129">如果您要安裝在**Windows 10**和 hello**容器**功能有先前未啟用，hello **Azure 函式執行階段**安裝程式會提示您 tooreboot您的機器 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="2a1b9-130">設定 hello Azure 函式執行階段</span><span class="sxs-lookup"><span data-stu-id="2a1b9-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="2a1b9-131">toocomplete hello Azure 函式執行階段安裝，您必須先完成 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="2a1b9-132">hello **Azure 函式執行階段組態工具**顯示您的電腦上安裝哪些角色。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Azure Functions 執行階段預覽設定工具][6]

1. <span data-ttu-id="2a1b9-134">按一下 hello**資料庫**索引標籤上，輸入 hello**連接詳細資料，您的 SQL Server 執行個體**和**按一下 套用**。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="2a1b9-135">這被必要的順序 toohello Azure 函式執行階段 toocreate 資料庫 toosupport hello 執行階段中。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Azure Functions 執行階段預覽資料庫設定][7]

1. <span data-ttu-id="2a1b9-137">按一下 hello**認證** 索引標籤。在此畫面上，您必須建立兩個新的認證，以使用 FileShare 來裝載您的所有 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="2a1b9-138">**指定使用者名稱和密碼**hello 組合**檔案共用擁有者**和 hello**檔案共用使用者**按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Azure Functions 執行階段預覽認證][8]

1. <span data-ttu-id="2a1b9-140">按一下 hello**檔案共用** 索引標籤。在此畫面中，您必須指定 hello 詳細資料的 hello**檔案共用位置**。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="2a1b9-141">您可以建立此項目，也可以使用現有的檔案共用，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="2a1b9-142">如果您選取新的檔案共用位置，您必須指定 hello Azure 函式執行階段使用的目錄。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Azure Functions 執行階段預覽檔案共用][9]

1. <span data-ttu-id="2a1b9-144">按一下 hello **IIS**  索引標籤。此索引標籤會顯示在 IIS Azure 函式執行階段安裝將會建立該 hello hello 網站 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="2a1b9-145">**按一下 套用**toocomplete。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-145">**Click Apply** toocomplete.</span></span>

    ![Azure Functions 執行階段預覽 IIS][10]

1. <span data-ttu-id="2a1b9-147">按一下 hello**服務** 索引標籤。此索引標籤會顯示 hello hello 服務狀態，在 Azure 函式執行階段安裝。</span><span class="sxs-lookup"><span data-stu-id="2a1b9-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="2a1b9-148">如果在初始設定 hello **Azure 函式主機啟用服務**正在按一下**啟動服務**</span><span class="sxs-lookup"><span data-stu-id="2a1b9-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Azure Functions 執行階段預覽設定完成][11]

1. <span data-ttu-id="2a1b9-150">最後瀏覽 toohello **Azure 函式執行階段網站**為`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="2a1b9-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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