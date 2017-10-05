---
title: "使用 Visual Studio 發佈 Azure 應用程式精靈 | Microsoft Docs"
description: "了解如何在 Visual Studio 發佈 Azure 應用程式精靈中進行各種設定"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 25b3ca9af2639860d9cfcb1492aef745fb47beb9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-visual-studio-publish-azure-application-wizard"></a><span data-ttu-id="9abba-103">使用 Visual Studio 發佈 Azure 應用程式精靈</span><span class="sxs-lookup"><span data-stu-id="9abba-103">Using the Visual Studio Publish Azure Application Wizard</span></span>
<span data-ttu-id="9abba-104">在 Visual Studio 中開發 web 應用程式之後，您可以使用 [發佈 Azure 應用程式] 精靈，將應用程式發佈至 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="9abba-104">After you develop a web application in Visual Studio, you can publish that application to an Azure cloud service by using the **Publish Azure Application** wizard.</span></span> 

> [!NOTE]
> <span data-ttu-id="9abba-105">本主題是關於部署到雲端服務，而不是網站。</span><span class="sxs-lookup"><span data-stu-id="9abba-105">This topic is about deploying to cloud services, not to web sites.</span></span> <span data-ttu-id="9abba-106">如需部署到網站的相關資訊，請參閱 [如何部署到 Azure 網站](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false)。</span><span class="sxs-lookup"><span data-stu-id="9abba-106">For information about deploying to web sites, see [How to Deploy an Azure Web Site](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).</span></span>
> 
> 

## <a name="accessing-the-publish-azure-application-wizard"></a><span data-ttu-id="9abba-107">存取發佈 Azure 應用程式精靈</span><span class="sxs-lookup"><span data-stu-id="9abba-107">Accessing the Publish Azure Application wizard</span></span>

<span data-ttu-id="9abba-108">視您擁有的 Visual Studio 專案類型而定，您有兩種方式可存取 [發佈 Azure 應用程式] 精靈。</span><span class="sxs-lookup"><span data-stu-id="9abba-108">You can access the Publish Azure Application wizard in two ways depending on the type of Visual Studio project you have.</span></span>

<span data-ttu-id="9abba-109">**如果您有 Azure 雲端服務專案︰**</span><span class="sxs-lookup"><span data-stu-id="9abba-109">**If you have an Azure cloud service project:**</span></span>

1. <span data-ttu-id="9abba-110">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="9abba-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="9abba-111">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後從操作功能表中選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="9abba-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Publish**.</span></span>

<span data-ttu-id="9abba-112">**如果您有未啟用 Azure 的 Web 應用程式專案︰**</span><span class="sxs-lookup"><span data-stu-id="9abba-112">**If you have a web application project that is not enabled for Azure:**</span></span>

1. <span data-ttu-id="9abba-113">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="9abba-113">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="9abba-114">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後從操作功能表中選取 [轉換] > [轉換為 Azure 雲端服務專案]。</span><span class="sxs-lookup"><span data-stu-id="9abba-114">In **Solution Explorer**, right-click the project, and, from the context menu, select **Convert** > **Convert to Azure Cloud Service Project**.</span></span> 

1. <span data-ttu-id="9abba-115">在 [方案總管] 中，以滑鼠右鍵按一下新建立的 Azure 專案，然後從操作功能表中選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="9abba-115">In **Solution Explorer**, right-click the newly created Azure project, and, from the context menu, select **Publish**.</span></span>

## <a name="sign-in-page"></a><span data-ttu-id="9abba-116">登入頁面</span><span class="sxs-lookup"><span data-stu-id="9abba-116">Sign-in page</span></span>

![登入頁面](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

<span data-ttu-id="9abba-118">**帳戶** - 選取帳戶或選取帳戶下拉式清單中的 [新增帳戶]。</span><span class="sxs-lookup"><span data-stu-id="9abba-118">**Account** - Select an account or select **Add an account** in the account dropdown list.</span></span>

<span data-ttu-id="9abba-119">**選擇您的訂用帳戶** - 選擇要用於部署的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9abba-119">**Choose your subscription** - Choose the subscription to use for your deployment.</span></span>
   
## <a name="settings-page---common-settings-tab"></a><span data-ttu-id="9abba-120">設定頁面 - 一般設定索引標籤</span><span class="sxs-lookup"><span data-stu-id="9abba-120">Settings page - Common Settings tab</span></span>   

![一般設定](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

<span data-ttu-id="9abba-122">**雲端服務** - 使用下拉式清單中，選取現有的雲端服務，或選取 &lt;新建>，然後建立雲端服務。</span><span class="sxs-lookup"><span data-stu-id="9abba-122">**Cloud service** - Using the dropdown, either select an existing cloud service, or select **&lt;Create New>**, and create a cloud service.</span></span> <span data-ttu-id="9abba-123">資料中心會針對每項雲端服務顯示於括號內。</span><span class="sxs-lookup"><span data-stu-id="9abba-123">The data center displays in parentheses for each cloud service.</span></span> <span data-ttu-id="9abba-124">建議雲端服務的資料中心位置與儲存體帳戶的資料中心位置相同 (進階設定)。</span><span class="sxs-lookup"><span data-stu-id="9abba-124">It is recommended that the data center location for the cloud service be the same as the data center location for the storage account (Advanced Settings).</span></span>  

<span data-ttu-id="9abba-125">**環境** - 選取 [生產] 或 [預備]。</span><span class="sxs-lookup"><span data-stu-id="9abba-125">**Environment** - Select either **Production** or **Staging**.</span></span> <span data-ttu-id="9abba-126">如果您想要在測試環境中部署應用程式，請選擇預備環境。</span><span class="sxs-lookup"><span data-stu-id="9abba-126">Choose the staging environment if you want to deploy your application in a test environment.</span></span> 

<span data-ttu-id="9abba-127">**建置組態** - 選取 [偵錯] 或 [發行]。</span><span class="sxs-lookup"><span data-stu-id="9abba-127">**Build configuration** - Select either **Debug** or **Release**.</span></span>

<span data-ttu-id="9abba-128">**服務組態** - 選取 [雲端] 或 [本機]。</span><span class="sxs-lookup"><span data-stu-id="9abba-128">**Service configuration** - Select either **Cloud** or **Local**.</span></span>
   
<span data-ttu-id="9abba-129">**啟用所有角色的遠端桌面** - 如果您想要從遠端連線到服務，請核取此選項。</span><span class="sxs-lookup"><span data-stu-id="9abba-129">**Enable Remote Desktop for all roles** - Check this option if you want to be able to remotely connect to the service.</span></span> <span data-ttu-id="9abba-130">此選項主要用於疑難排解。</span><span class="sxs-lookup"><span data-stu-id="9abba-130">This option is primarily used for troubleshooting.</span></span> <span data-ttu-id="9abba-131">當您選取此核取方塊，[遠端桌面組態]  對話方塊會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="9abba-131">When you select this check box, the **Remote Desktop Configuration** dialog box appears.</span></span> <span data-ttu-id="9abba-132">選擇 [設定] 連結以變更組態。</span><span class="sxs-lookup"><span data-stu-id="9abba-132">Choose the **Settings** link to change the configuration.</span></span>
   
<span data-ttu-id="9abba-133">**啟用所有 Web 角色的 Web 部署** - 核取此選項，以啟用服務的 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="9abba-133">**Enable Web Deploy for all web roles** - Check this option, to enable web deployment for the service.</span></span> <span data-ttu-id="9abba-134">您必須選取 [啟用所有角色的遠端桌面] 選項才能使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="9abba-134">You must select the **Enable Remote Desktop for all roles** option to use this feature.</span></span> <span data-ttu-id="9abba-135">如需詳細資訊，請參閱[[使用 Visual Studio 發佈 Azure 雲端服務](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9abba-135">For more information, see [[Publishing a Azure cloud service using Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx).</span></span> 

## <a name="settings-page---advanced-settings-tab"></a><span data-ttu-id="9abba-136">設定頁面 - 進階設定索引標籤</span><span class="sxs-lookup"><span data-stu-id="9abba-136">Settings page - Advanced Settings tab</span></span>

![進階設定](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

<span data-ttu-id="9abba-138">**部署標籤**：接受預設名稱，或輸入您所選擇的名稱。</span><span class="sxs-lookup"><span data-stu-id="9abba-138">**Deployment label** - Either accept the default name, or enter a name of your choosing.</span></span> <span data-ttu-id="9abba-139">若要將日期附加至部署標籤，請選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="9abba-139">To append the date to the deployment label, leave the check box selected.</span></span> 
   
<span data-ttu-id="9abba-140">**儲存體帳戶**：選取想用於此部署的儲存體帳戶，**&lt;新建> 可建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9abba-140">**Storage account** - Select the storage account to use for this deployment, **&lt;Create New> to create a storage account.</span></span> <span data-ttu-id="9abba-141">資料中心會針對每個儲存體帳戶顯示於括號內。</span><span class="sxs-lookup"><span data-stu-id="9abba-141">The data center displays in parentheses for each storage account.</span></span> <span data-ttu-id="9abba-142">建議儲存體帳戶的資料中心位置與雲端服務的資料中心位置相同 (一般設定)。</span><span class="sxs-lookup"><span data-stu-id="9abba-142">It is recommended that the data center location for the storage account be the same as the data center location for the cloud service (Common Settings).</span></span>  
   
<span data-ttu-id="9abba-143">Azure 儲存體帳戶會儲存應用程式部署的封裝。</span><span class="sxs-lookup"><span data-stu-id="9abba-143">The Azure storage account stores the package for the application deployment.</span></span> <span data-ttu-id="9abba-144">部署應用程式之後，封裝會從儲存體帳戶中移除。</span><span class="sxs-lookup"><span data-stu-id="9abba-144">After the application is deployed, the package is removed from the storage account.</span></span>

<span data-ttu-id="9abba-145">**失敗時刪除部署**- 選取此選項，可以在發佈期間遇到任何錯誤時刪除部署。</span><span class="sxs-lookup"><span data-stu-id="9abba-145">**Delete deployment on failure** - Select this option to have the deployment deleted if any errors are encountered during publishing.</span></span> <span data-ttu-id="9abba-146">如果您想要針對您的雲端服務維護固定的虛擬 IP 位址，應該取消核取此選項。</span><span class="sxs-lookup"><span data-stu-id="9abba-146">This should be unchecked if you want to maintain a constant virtual IP address for your cloud service.</span></span>

<span data-ttu-id="9abba-147">**部署更新** - 如果您只想要部署已更新的元件，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="9abba-147">**Deployment update** - Select this option if you want to deploy only updated components.</span></span> <span data-ttu-id="9abba-148">這種部署類型比完整部署更快速。</span><span class="sxs-lookup"><span data-stu-id="9abba-148">This type of deployment can be faster than a full deployment.</span></span> <span data-ttu-id="9abba-149">如果您想要針對您的雲端服務維護固定的虛擬 IP 位址，應該核取此選項。</span><span class="sxs-lookup"><span data-stu-id="9abba-149">This should be checked if you want to maintain a constant virtual IP address for your cloud service.</span></span> 

<span data-ttu-id="9abba-150">**部署更新 - 設定** - 此對話方塊用來進一步指定您希望更新角色的方式。</span><span class="sxs-lookup"><span data-stu-id="9abba-150">**Deployment update - settings** - This dialog is used to further specify how you want the roles to be updated.</span></span> <span data-ttu-id="9abba-151">如果您選擇 [累加式更新]，就會逐一更新應用程式的每個執行個體，讓應用程式隨時可供使用。</span><span class="sxs-lookup"><span data-stu-id="9abba-151">If you choose **Incremental update**, each instance of your application is updated one after another, so that the application is always available.</span></span> <span data-ttu-id="9abba-152">如果您選擇 [同時更新]，即會同時更新應用程式的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="9abba-152">If you choose **Simultaneous update**, all instances of your application are updated at the same time.</span></span> <span data-ttu-id="9abba-153">同時更新較為快速，但是您的服務可能無法在更新過程中使用。</span><span class="sxs-lookup"><span data-stu-id="9abba-153">Simultaneous updating is faster, but your service might not be available during the update process.</span></span> 

![部署設定](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

<span data-ttu-id="9abba-155">**啟用 IntelliTrace** - 指定您是否要啟用 IntelliTrace。</span><span class="sxs-lookup"><span data-stu-id="9abba-155">**Enable IntelliTrace** - Specify if you want to enable IntelliTrace.</span></span> <span data-ttu-id="9abba-156">有了 IntelliTrace，您可以於角色執行個體在 Azure 中執行時，記錄其廣泛的偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="9abba-156">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="9abba-157">如果您需要找出問題的原因，您可以從 Visual Studio 使用 IntelliTrace 記錄檔來瀏覽程式碼，如同它是在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="9abba-157">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="9abba-158">如需使用 IntelliTrace 的詳細資訊，請參閱[使用 Visual Studio 和 IntelliTrace 進行已發佈 Azure 雲端服務的偵錯](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)。</span><span class="sxs-lookup"><span data-stu-id="9abba-158">For more information about using IntelliTrace, see [Debugging a published Azure cloud service with Visual Studio and IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md).</span></span> 

<span data-ttu-id="9abba-159">**啟用剖析** - 指定您是否要啟用效能剖析。</span><span class="sxs-lookup"><span data-stu-id="9abba-159">**Enable profiling** - Specify if you want to enable performance profiling.</span></span> <span data-ttu-id="9abba-160">Visual Studio 分析工具可讓您取得雲端服務執行情況在計算方面的深入分析。</span><span class="sxs-lookup"><span data-stu-id="9abba-160">The Visual Studio profiler enables you to get an in-depth analysis of the computational aspects of how your cloud service runs.</span></span> <span data-ttu-id="9abba-161">如需有關如何使用 Visual Studio 分析工具的詳細資訊，請參閱[測試 Azure 雲端服務的效能](./vs-azure-tools-performance-profiling-cloud-services.md)。</span><span class="sxs-lookup"><span data-stu-id="9abba-161">For more information on using the Visual Studio profiler, see [Test the performance of an Azure cloud service](./vs-azure-tools-performance-profiling-cloud-services.md).</span></span>

<span data-ttu-id="9abba-162">**啟用所有角色的遠端偵錯工具** - 指定您是否要啟用遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="9abba-162">**Enable Remote Debugger for all roles** - Specify if you want to enable remote debugging.</span></span> <span data-ttu-id="9abba-163">如需使用 Visual Studio 進行雲端服務偵錯的詳細資訊，請參閱[在 Visual Studio 中進行 Azure 雲端服務或虛擬機器的偵錯](./vs-azure-tools-debug-cloud-services-virtual-machines.md)。</span><span class="sxs-lookup"><span data-stu-id="9abba-163">For more information on debugging cloud services using Visual Studio, see [Debugging an Azure cloud service or virtual machine in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).</span></span>

## <a name="diagnostics-settings-page"></a><span data-ttu-id="9abba-164">診斷設定頁面</span><span class="sxs-lookup"><span data-stu-id="9abba-164">Diagnostics Settings page</span></span>

![診斷設定](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

<span data-ttu-id="9abba-166">診斷可讓您針對 Azure 雲端服務 (或 Azure 虛擬機器) 進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="9abba-166">Diagnostics enables you to troubleshoot an Azure cloud service (or Azure virtual machine).</span></span> <span data-ttu-id="9abba-167">如需診斷的相關資訊，請參閱[為 Azure 雲端服務和虛擬機器設定診斷功能](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。</span><span class="sxs-lookup"><span data-stu-id="9abba-167">For information about diagnostics, see [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> <span data-ttu-id="9abba-168">如需 Application Insights 的相關資訊，請參閱[什麼是 Application Insights？](./application-insights/app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9abba-168">For information about Application Insights, see [What is Application Insights?](./application-insights/app-insights-overview.md).</span></span>

## <a name="summary-page"></a><span data-ttu-id="9abba-169">摘要頁面</span><span class="sxs-lookup"><span data-stu-id="9abba-169">Summary page</span></span>

![摘要](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

<span data-ttu-id="9abba-171">**目標設定檔** - 您可以選擇從您所選擇的設定建立發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="9abba-171">**Target profile** - You can choose to create a publishing profile from the settings that you have chosen.</span></span> <span data-ttu-id="9abba-172">例如，您可能會建立一個設定檔用於測試環境，並建立另一個用於生產。</span><span class="sxs-lookup"><span data-stu-id="9abba-172">For example, you might create one profile for a test environment and another for production.</span></span> <span data-ttu-id="9abba-173">若要儲存這個設定檔，請選擇 **儲存** 圖示。</span><span class="sxs-lookup"><span data-stu-id="9abba-173">To save this profile, choose the **Save** icon.</span></span> <span data-ttu-id="9abba-174">此精靈會建立設定檔並將它儲存在 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="9abba-174">The wizard creates the profile and saves it in the Visual Studio project.</span></span> <span data-ttu-id="9abba-175">若要修改設定檔名稱，請開啟 [目標設定檔] 清單，然後選擇 **<管理...>**。</span><span class="sxs-lookup"><span data-stu-id="9abba-175">To modify the profile name, open the **Target profile** list, and then choose **<Manage…>**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9abba-176">發佈設定檔會出現在 Visual Studio 的 [方案總管] 中，而且設定檔設定會寫入至副檔名為.azurePubxml 的檔案。</span><span class="sxs-lookup"><span data-stu-id="9abba-176">The publishing profile appears in Solution Explorer in Visual Studio, and the profile settings are written to a file with an .azurePubxml extension.</span></span> <span data-ttu-id="9abba-177">設定會儲存為 XML 標記的屬性。</span><span class="sxs-lookup"><span data-stu-id="9abba-177">Settings are saved as attributes of XML tags.</span></span>
   > 
   > 

## <a name="publishing-your-application"></a><span data-ttu-id="9abba-178">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="9abba-178">Publishing your application</span></span>

<span data-ttu-id="9abba-179">設定專案部署的所有設定後，請選取對話方塊底部的 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="9abba-179">Once you configure all the settings for your project's deployment, select **Publish** at the bottom of the dialog.</span></span> <span data-ttu-id="9abba-180">您可以在 Visual Studio 中監視 [輸出]  視窗中的處理序狀態。</span><span class="sxs-lookup"><span data-stu-id="9abba-180">You can monitor the process status in the **Output** window in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9abba-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9abba-181">Next steps</span></span>
- [<span data-ttu-id="9abba-182">從 Visual Studio 將 Web 應用程式移轉並發佈至 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="9abba-182">Migrate and publish a Web Application to an Azure cloud service from Visual Studio</span></span>](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [<span data-ttu-id="9abba-183">了解如何使用 Visual Studio 來發佈 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="9abba-183">Learn how to use Visual Studio to publish an Azure cloud service</span></span>](./vs-azure-tools-publishing-a-cloud-service.md)
- [<span data-ttu-id="9abba-184">使用 Visual Studio 和 IntelliTrace 進行已發佈 Azure 雲端服務的偵錯</span><span class="sxs-lookup"><span data-stu-id="9abba-184">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [<span data-ttu-id="9abba-185">測試 Azure 雲端服務的效能</span><span class="sxs-lookup"><span data-stu-id="9abba-185">Test the performance of an Azure cloud service</span></span>](./vs-azure-tools-performance-profiling-cloud-services.md)
- <span data-ttu-id="9abba-186">[為 Azure 雲端服務和虛擬機器設定診斷功能](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。</span><span class="sxs-lookup"><span data-stu-id="9abba-186">[Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> 
- [<span data-ttu-id="9abba-187">什麼是 Application Insights？</span><span class="sxs-lookup"><span data-stu-id="9abba-187">What is Application Insights?</span></span>](./application-insights/app-insights-overview.md)