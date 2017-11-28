---
title: "使用 Visual Studio 部署 Azure Stack 中的範本 | Microsoft Docs"
description: "了解如何以 Visual Studio 部署 Azure Stack 中的範本。"
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
ms.openlocfilehash: e9b467f47f166198d9790f19dbdd3d1d0fd79947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a><span data-ttu-id="838b0-103">使用 Visual Studio 部署 Azure Stack 中的範本</span><span class="sxs-lookup"><span data-stu-id="838b0-103">Deploy templates in Azure Stack using Visual Studio</span></span>

<span data-ttu-id="838b0-104">使用 Visual Studio 將 Azure Resource Manager 範本部署到 Azure Stack 開發套件。</span><span class="sxs-lookup"><span data-stu-id="838b0-104">Use Visual Studio to deploy Azure Resource Manager templates to the Azure Stack development kit.</span></span>

1. <span data-ttu-id="838b0-105">使用 Visual Studio [安裝並連接](azure-stack-install-visual-studio.md)至 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="838b0-105">[Install and connect](azure-stack-install-visual-studio.md) to Azure Stack with Visual Studio.</span></span>
2. <span data-ttu-id="838b0-106">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="838b0-106">Open Visual Studio.</span></span>
3. <span data-ttu-id="838b0-107">依序按一下 [檔案]、[新增]，在 [新增專案] 對話方塊中，按一下 [Azure 資源群組]。</span><span class="sxs-lookup"><span data-stu-id="838b0-107">Click **File**, click **New**, and in the **New Project** dialog box click **Azure Resource Group**.</span></span>
4. <span data-ttu-id="838b0-108">輸入新專案的**名稱**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="838b0-108">Enter a **Name** for the new project, and then click **OK**.</span></span>
5. <span data-ttu-id="838b0-109">在 [選取 Azure 範本] 對話方塊中，將 [顯示此位置的範本] 下拉式清單變更為 [Azure Stack 快速入門]</span><span class="sxs-lookup"><span data-stu-id="838b0-109">In the **Select Azure Template** dialog box, change the *Show templates from this location* drop-down to **Azure Stack Quickstart**</span></span>
6. <span data-ttu-id="838b0-110">按一下 [101-建立-儲存體-帳戶]，然後再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="838b0-110">Click **101-create-storage-account**, and then click **OK**.</span></span>  
7. <span data-ttu-id="838b0-111">在您的新專案中，展開 [方案總管] 窗格中的 [範本] 節點，可以看到可用的範本清單。</span><span class="sxs-lookup"><span data-stu-id="838b0-111">In your new project, you can see a list of the templates available by expanding the **Templates** node in the **Solution Explorer** pane.</span></span>
8. <span data-ttu-id="838b0-112">在 [方案總管] 窗格中，以滑鼠右鍵按一下專案名稱，按一下 [部署]，然後按一下 [新增部署]。</span><span class="sxs-lookup"><span data-stu-id="838b0-112">In the **Solution Explorer** pane, right-click the name of your project, click **Deploy**, then click **New Deployment**.</span></span>
9. <span data-ttu-id="838b0-113">在 [部署至資源群組] 對話方塊中，於 [訂用帳戶] 下拉式清單中，選取您的 Microsoft Azure Stack 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="838b0-113">In the **Deploy to Resource Group** dialog box, in the **Subscription** drop-down, select your Microsoft Azure Stack subscription.</span></span>
10. <span data-ttu-id="838b0-114">在 [資源群組] 清單中，選擇現有資源群組或建立新群組。</span><span class="sxs-lookup"><span data-stu-id="838b0-114">In the **Resource Group** list, choose an existing resource group or create a new one.</span></span>
11. <span data-ttu-id="838b0-115">在 [資源群組位置] 清單中，選擇某個位置，然後按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="838b0-115">In the **Resource group location** list, choose a location, and then click **Deploy**.</span></span>
12. <span data-ttu-id="838b0-116">在 [編輯參數] 對話方塊中，輸入參數值 (依範本而異)，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="838b0-116">In the **Edit Parameters** dialog box, enter values for the parameters (which vary by template), and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="838b0-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="838b0-117">Next steps</span></span>
[<span data-ttu-id="838b0-118">使用命令列部署範本</span><span class="sxs-lookup"><span data-stu-id="838b0-118">Deploy templates with the command line</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="838b0-119">開發適用於 Azure Stack 的範本</span><span class="sxs-lookup"><span data-stu-id="838b0-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)

