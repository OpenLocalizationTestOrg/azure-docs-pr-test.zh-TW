---
title: "如何將專案升級為目前版本的 Azure Tools | Microsoft Docs"
description: "了解如何在 Visual Studio 中將 Azure 專案升級至目前版本的 Azure Tools"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 9a35de7ca0e7161468181b21709e1bd9915d566f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-upgrade-projects-to-the-current-version-of-the-azure-tools-for-visual-studio"></a><span data-ttu-id="40881-103">如何將專案升級為目前版本的 Azure Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40881-103">How to upgrade projects to the current version of the Azure Tools for Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="40881-104">Overview</span><span class="sxs-lookup"><span data-stu-id="40881-104">Overview</span></span>
<span data-ttu-id="40881-105">安裝目前版本的 Azure Tools (或是比 1.6 版更新的舊版) 之後，任何使用 1.6 版 (2011 年 11 月) 以前的 Azure Tools 所建立的專案，在您開啟時會立即自動升級。</span><span class="sxs-lookup"><span data-stu-id="40881-105">After you install the current release of the Azure Tools (or a previous release that's newer than 1.6), any projects that were created by using a Azure Tools release before 1.6 (November 2011) will be automatically upgraded as soon as you open them.</span></span> <span data-ttu-id="40881-106">如果您使用這些工具的 1.6 版 (2011 年 11 月) 建立專案，且仍然安裝該版本，您可以在較舊版本中開啟這些專案，稍後再決定是否要將它們升級。</span><span class="sxs-lookup"><span data-stu-id="40881-106">If you created projects by using the 1.6 (November 2011) release of those tools and you still have that release installed, you can open those projects in the older release and decide later whether to upgrade them.</span></span>

## <a name="how-your-project-changes-when-you-upgrade-it"></a><span data-ttu-id="40881-107">專案升級時有何變更</span><span class="sxs-lookup"><span data-stu-id="40881-107">How your project changes when you upgrade it</span></span>
<span data-ttu-id="40881-108">如果專案自動升級，或您指定要將它升級，您的專案會修改為使用目前版本的某些組件，某些屬性也會變更，如本節所述。</span><span class="sxs-lookup"><span data-stu-id="40881-108">If a project is automatically upgraded or you specify that you want to upgrade it, your project is modified to work with current versions of certain assemblies, and some properties are also changed as this section describes.</span></span> <span data-ttu-id="40881-109">如果您的專案需要其他變更，才能與較新版本的工具相容，您必須手動進行這些變更。</span><span class="sxs-lookup"><span data-stu-id="40881-109">If your project requires other changes to be compatible with the newer version of the tools, you must make those changes manually.</span></span>

* <span data-ttu-id="40881-110">Web 角色的 web.config 檔案和背景工作角色的 app.config 檔案會更新為參考較新版的 Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll。</span><span class="sxs-lookup"><span data-stu-id="40881-110">The web.config file for web roles and the app.config file for worker roles are updated to reference the newer version of Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll.</span></span>
* <span data-ttu-id="40881-111">Microsoft.WindowsAzure.StorageClient.dll、Microsoft.WindowsAzure.Diagnostics.dll 和 Microsoft.WindowsAzure.ServiceRuntime.dll 組件會升級至新的版本。</span><span class="sxs-lookup"><span data-stu-id="40881-111">The Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll, and Microsoft.WindowsAzure.ServiceRuntime.dll assemblies are upgraded to the new versions.</span></span>
* <span data-ttu-id="40881-112">已儲存在 Azure 專案檔 (.ccproj) 的發佈設定檔，將會移到 **Publish** 子目錄中的另一個檔案，副檔名為 .azurePubXml。</span><span class="sxs-lookup"><span data-stu-id="40881-112">Publish profiles that were stored in the Azure project file (.ccproj) are moved to a separate file, with the extension .azurePubXml, in the **Publish** subdirectory.</span></span>
* <span data-ttu-id="40881-113">發佈設定檔中的某些屬性會更新為支援新的和變更的功能。</span><span class="sxs-lookup"><span data-stu-id="40881-113">Some properties in the publish profile are updated to support new and changed features.</span></span> <span data-ttu-id="40881-114">**AllowUpgrade** 會取代為 **DeploymentReplacementMethod**，因為您可以同時或以累加方式更新已部署的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="40881-114">**AllowUpgrade** is replaced by **DeploymentReplacementMethod** because you can update a deployed cloud service simultaneously or incrementally.</span></span>
* <span data-ttu-id="40881-115">屬性 **UseIISExpressByDefault** 會加入並設為 false，使得用於偵錯的 Web 伺服器不會自動從網際網路資訊服務 (IIS) 切換為 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="40881-115">The property **UseIISExpressByDefault** is added and set to false so that the web server that’s used for debugging won’t automatically change from Internet Information Services (IIS) to IIS Express.</span></span> <span data-ttu-id="40881-116">IIS Express 是由較新版本的工具所建立之專案的預設 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="40881-116">IIS Express is the default web server for projects that are created with the newer releases of the tools.</span></span>
* <span data-ttu-id="40881-117">如果 Azure 快取裝載於一或多個專案的角色，當專案升級時，服務組態 (.cscfg 檔) 和服務定義 (.csdef 檔) 中的某些屬性會變更。</span><span class="sxs-lookup"><span data-stu-id="40881-117">If Azure Caching is hosted in one or more of your project’s roles, some properties in the service configuration (.cscfg file) and service definition (.csdef file) are changed when a project is upgraded.</span></span> <span data-ttu-id="40881-118">如果專案使用 Azure 快取 NuGet 封裝，專案會升級到最新版的封裝。</span><span class="sxs-lookup"><span data-stu-id="40881-118">If the project uses the Azure Caching NuGet package, the project is upgraded to the most recent version of the package.</span></span> <span data-ttu-id="40881-119">您應該開啟 web.config 檔案，並確認用戶端組態在升級程序期間已妥善維護。</span><span class="sxs-lookup"><span data-stu-id="40881-119">You should open the web.config file and verify that the client configuration was maintained properly during the upgrade process.</span></span> <span data-ttu-id="40881-120">如果您加入 Azure 快取用戶端組件的參考，而未使用 NuGet 封裝，則不會更新這些組件。您必須手動更新對於新版本的參考。</span><span class="sxs-lookup"><span data-stu-id="40881-120">If you added the references to Azure Caching client assemblies without using the NuGet package, these assemblies won't be updated; you must manually update these references to the new versions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40881-121">在 F# 專案中，您必須手動更新 Azure 組件的參考，使它們參考這些組件的較新版本。</span><span class="sxs-lookup"><span data-stu-id="40881-121">For F# projects, you must manually update references to Azure assemblies so that they reference the newer versions of those assemblies.</span></span>
> 
> 

### <a name="how-to-upgrade-an-azure-project-to-the-current-release"></a><span data-ttu-id="40881-122">如何將 Azure 專案升級至目前版本</span><span class="sxs-lookup"><span data-stu-id="40881-122">How to upgrade an Azure project to the current release</span></span>
1. <span data-ttu-id="40881-123">將目前版本的 Azure tools 安裝到您想要用於升級專案的 Visual Studio 安裝，然後開啟您想要升級的專案。</span><span class="sxs-lookup"><span data-stu-id="40881-123">Install the current version of the Azure Tools into the installation of Visual Studio that you want to use for the upgraded project, and then open the project that you want to upgrade.</span></span> <span data-ttu-id="40881-124">如果專案是使用 1.6 版 (2011 年 11 月) 以前的 Azure Tools 建立，專案會自動升級至目前版本。</span><span class="sxs-lookup"><span data-stu-id="40881-124">If the project was created with a Azure Tools release before 1.6 (November 2011), the project is automatically upgraded to the current version.</span></span> <span data-ttu-id="40881-125">如果專案是使用 2011 年 11 月版本建立，且仍然安裝該版本，則會在該版本中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="40881-125">If the project was created with the November 2011 release and that release is still installed, the project opens in that release.</span></span>
2. <span data-ttu-id="40881-126">在 [方案總管] 中，開啟專案節點的捷徑功能表，選擇 [屬性]，然後在出現的對話方塊中選擇 [應用程式] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="40881-126">In Solution Explorer, open the shortcut menu for the project node, choose **Properties**, and then choose the **Application** tab of the dialog box that appears.</span></span>
   
    <span data-ttu-id="40881-127">[應用程式]  索引標籤會顯示與專案相關聯的工具版本。</span><span class="sxs-lookup"><span data-stu-id="40881-127">The **Application** tab shows the tools version that’s associated with the project.</span></span> <span data-ttu-id="40881-128">如果出現目前版本的 Azure Tools，表示已經升級專案。</span><span class="sxs-lookup"><span data-stu-id="40881-128">If the current version of Azure Tools appears, the project has already been upgraded.</span></span> <span data-ttu-id="40881-129">如果您已安裝的工具版本比索引標籤顯示的版本更新，則會出現 [升級]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="40881-129">If you've installed a newer version of the tools than what the tab shows, an **Upgrade** button appears.</span></span>
3. <span data-ttu-id="40881-130">選擇 [升級]  按鈕，將專案升級為目前版本的工具。</span><span class="sxs-lookup"><span data-stu-id="40881-130">Choose the **Upgrade** button to upgrade a project to the current version of the tools.</span></span>
4. <span data-ttu-id="40881-131">建置專案，然後解決因為 API 變更而造成的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="40881-131">Build the project, and then address any errors that result from API changes.</span></span> <span data-ttu-id="40881-132">如需如何針對新版本來修改程式碼的相關資訊，請參閱特定 API 的文件。</span><span class="sxs-lookup"><span data-stu-id="40881-132">For information about how to modify your code for the new version, see the documentation for the specific API.</span></span>

