---
title: "aaaUsing Emulator Express toorun 偵錯 Azure 雲端服務在本機電腦上的 |Microsoft 文件"
description: "在 本機電腦上使用 Emulator Express toorun 和偵錯雲端服務"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="3a204-103">使用 Emulator Express toorun 和偵錯 Azure 雲端服務在本機電腦上</span><span class="sxs-lookup"><span data-stu-id="3a204-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="3a204-104">使用 Emulator Express，您可以測試及偵錯雲端服務，而不需以系統管理員身分執行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3a204-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="3a204-105">您可以設定您的專案設定 toouse 任一 Emulator Express 或 hello 完整模擬器，視您的雲端服務的 hello 需求而定。</span><span class="sxs-lookup"><span data-stu-id="3a204-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="3a204-106">如需 hello 完整模擬器的詳細資訊，請參閱[hello 計算模擬器中執行 Azure 應用程式](storage/common/storage-use-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="3a204-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="3a204-107">在 Visual Studio 中使用 Emulator Express</span><span class="sxs-lookup"><span data-stu-id="3a204-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="3a204-108">當您在 Azure SDK 2.3 或更新版本中建立 Azure 專案時，會自動使用 Emulator Express。</span><span class="sxs-lookup"><span data-stu-id="3a204-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="3a204-109">使用較早版本的 hello Azure SDK 所建立的現有專案，使用下列步驟 tooselect Emulator Express hello:</span><span class="sxs-lookup"><span data-stu-id="3a204-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="3a204-110">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="3a204-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="3a204-111">在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="3a204-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="3a204-112">在 hello 專案屬性頁中，選取 [hello **Web** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3a204-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Azure 雲端服務專案的屬性](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="3a204-114">在 [本機程式開發伺服器] 之下，選取 [使用 IIS Express] 選項。</span><span class="sxs-lookup"><span data-stu-id="3a204-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="3a204-115">在 [模擬器] 之下，選取 [使用 Emulator Express]。</span><span class="sxs-lookup"><span data-stu-id="3a204-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="3a204-116">toolaunch hello Emulator Express，執行下列命令，在命令提示字元中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3a204-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="3a204-117">Emulator Express 限制</span><span class="sxs-lookup"><span data-stu-id="3a204-117">Emulator Express limitations</span></span>
<span data-ttu-id="3a204-118">下列問題的 hello 是已知 Emulator Express 的限制：</span><span class="sxs-lookup"><span data-stu-id="3a204-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="3a204-119">Emulator Express 與「IIS Web 伺服器」不相容。</span><span class="sxs-lookup"><span data-stu-id="3a204-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="3a204-120">您的雲端服務可包含多個角色，但每個角色都有限的 tooone 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3a204-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="3a204-121">您無法存取低於 1000 的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="3a204-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="3a204-122">如果您使用的驗證提供者通常使用低於 1000年的連接埠，您可能需要 toochange 為高於 1000年這個值 tooa 通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="3a204-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="3a204-123">套用 toohello Azure 計算模擬器的所有限制也適都用於 tooEmulator Express。</span><span class="sxs-lookup"><span data-stu-id="3a204-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="3a204-124">例如，每一個部署不能有 50 個以上的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3a204-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="3a204-125">如需 hello Azure 計算模擬器的詳細資訊，請參閱[hello 計算模擬器中執行 Azure 應用程式](http://go.microsoft.com/fwlink/p/?LinkId=623050)。</span><span class="sxs-lookup"><span data-stu-id="3a204-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a204-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a204-126">Next steps</span></span>
[<span data-ttu-id="3a204-127">進行 Azure 雲端服務偵錯</span><span class="sxs-lookup"><span data-stu-id="3a204-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
