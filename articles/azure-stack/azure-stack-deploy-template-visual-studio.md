---
title: "使用 Azure 堆疊中的 Visual Studio aaaDeploy 範本 |Microsoft 文件"
description: "深入了解如何使用 Azure 堆疊中的 Visual Studio toodeploy 範本。"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: aea917b585a30ef4fbe7263db66f0659b56b21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a><span data-ttu-id="ef445-103">使用 Visual Studio 部署 Azure Stack 中的範本</span><span class="sxs-lookup"><span data-stu-id="ef445-103">Deploy templates in Azure Stack using Visual Studio</span></span>

<span data-ttu-id="ef445-104">使用 Visual Studio toodeploy Azure Resource Manager 範本 toohello Azure 堆疊開發套件。</span><span class="sxs-lookup"><span data-stu-id="ef445-104">Use Visual Studio toodeploy Azure Resource Manager templates toohello Azure Stack development kit.</span></span>

1. <span data-ttu-id="ef445-105">[安裝並連接](azure-stack-install-visual-studio.md)tooAzure Visual Studio 中的堆疊。</span><span class="sxs-lookup"><span data-stu-id="ef445-105">[Install and connect](azure-stack-install-visual-studio.md) tooAzure Stack with Visual Studio.</span></span>
2. <span data-ttu-id="ef445-106">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ef445-106">Open Visual Studio.</span></span>
3. <span data-ttu-id="ef445-107">按一下**檔案**，按一下 **新增**，並在 hello**新專案**對話方塊中，按一下**Azure 資源群組**。</span><span class="sxs-lookup"><span data-stu-id="ef445-107">Click **File**, click **New**, and in hello **New Project** dialog box click **Azure Resource Group**.</span></span>
4. <span data-ttu-id="ef445-108">輸入**名稱**hello 新專案，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="ef445-108">Enter a **Name** for hello new project, and then click **OK**.</span></span>
5. <span data-ttu-id="ef445-109">在 hello**選取 Azure 範本**對話方塊中，變更 hello*顯示從這個位置的範本*下拉式太**Azure 堆疊快速入門**</span><span class="sxs-lookup"><span data-stu-id="ef445-109">In hello **Select Azure Template** dialog box, change hello *Show templates from this location* drop-down too**Azure Stack Quickstart**</span></span>
6. <span data-ttu-id="ef445-110">按一下 [101-建立-儲存體-帳戶]，然後再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ef445-110">Click **101-create-storage-account**, and then click **OK**.</span></span>  
7. <span data-ttu-id="ef445-111">在新的專案中，您可以看到一份可用的 hello 範本展開 hello**範本**節點 hello**方案總管 中**窗格。</span><span class="sxs-lookup"><span data-stu-id="ef445-111">In your new project, you can see a list of hello templates available by expanding hello **Templates** node in hello **Solution Explorer** pane.</span></span>
8. <span data-ttu-id="ef445-112">在 hello**方案總管 中**窗格，以滑鼠右鍵按一下 hello 您的專案名稱，按一下 **部署**，然後按一下**新部署**。</span><span class="sxs-lookup"><span data-stu-id="ef445-112">In hello **Solution Explorer** pane, right-click hello name of your project, click **Deploy**, then click **New Deployment**.</span></span>
9. <span data-ttu-id="ef445-113">在 hello**部署 tooResource 群組**對話方塊中的，在 hello**訂用帳戶**下拉式清單中，選取您的 Microsoft Azure 堆疊訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ef445-113">In hello **Deploy tooResource Group** dialog box, in hello **Subscription** drop-down, select your Microsoft Azure Stack subscription.</span></span>
10. <span data-ttu-id="ef445-114">在 hello**資源群組**清單中，選擇現有的資源群組或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="ef445-114">In hello **Resource Group** list, choose an existing resource group or create a new one.</span></span>
11. <span data-ttu-id="ef445-115">在 hello**資源群組位置**清單中，選擇的位置，然後按一下**部署**。</span><span class="sxs-lookup"><span data-stu-id="ef445-115">In hello **Resource group location** list, choose a location, and then click **Deploy**.</span></span>
12. <span data-ttu-id="ef445-116">在 hello**編輯參數**對話方塊方塊中，輸入 hello 參數 （這會因範本） 的值，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="ef445-116">In hello **Edit Parameters** dialog box, enter values for hello parameters (which vary by template), and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef445-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef445-117">Next steps</span></span>
[<span data-ttu-id="ef445-118">部署範本以 hello 命令列</span><span class="sxs-lookup"><span data-stu-id="ef445-118">Deploy templates with hello command line</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="ef445-119">開發適用於 Azure Stack 的範本</span><span class="sxs-lookup"><span data-stu-id="ef445-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)

