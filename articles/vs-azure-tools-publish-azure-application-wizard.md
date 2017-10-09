---
title: "aaaUsing hello Visual Studio 發行 Azure 應用程式精靈 |Microsoft 文件"
description: "了解如何 tooconfigure hello hello Visual Studio 發行 Azure 應用程式精靈中的各種設定"
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
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a><span data-ttu-id="99be7-103">使用 hello Visual Studio 發行 Azure 應用程式精靈</span><span class="sxs-lookup"><span data-stu-id="99be7-103">Using hello Visual Studio Publish Azure Application Wizard</span></span>
<span data-ttu-id="99be7-104">開發 Visual Studio 中的 web 應用程式之後，您可以發行該應用程式 tooan Azure 雲端服務使用 hello**發行 Azure 應用程式**精靈。</span><span class="sxs-lookup"><span data-stu-id="99be7-104">After you develop a web application in Visual Studio, you can publish that application tooan Azure cloud service by using hello **Publish Azure Application** wizard.</span></span> 

> [!NOTE]
> <span data-ttu-id="99be7-105">本主題是關於部署 toocloud 服務，不 tooweb 站台。</span><span class="sxs-lookup"><span data-stu-id="99be7-105">This topic is about deploying toocloud services, not tooweb sites.</span></span> <span data-ttu-id="99be7-106">如需部署 tooweb 站台資訊，請參閱[如何 tooDeploy Azure 網站](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false)。</span><span class="sxs-lookup"><span data-stu-id="99be7-106">For information about deploying tooweb sites, see [How tooDeploy an Azure Web Site](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).</span></span>
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a><span data-ttu-id="99be7-107">存取 hello 發行 Azure 應用程式精靈</span><span class="sxs-lookup"><span data-stu-id="99be7-107">Accessing hello Publish Azure Application wizard</span></span>

<span data-ttu-id="99be7-108">您可以存取 hello 發行 Azure 應用程式精靈，根據您所擁有的 Visual Studio 專案 hello 類型有兩種。</span><span class="sxs-lookup"><span data-stu-id="99be7-108">You can access hello Publish Azure Application wizard in two ways depending on hello type of Visual Studio project you have.</span></span>

<span data-ttu-id="99be7-109">**如果您有 Azure 雲端服務專案︰**</span><span class="sxs-lookup"><span data-stu-id="99be7-109">**If you have an Azure cloud service project:**</span></span>

1. <span data-ttu-id="99be7-110">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="99be7-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="99be7-111">在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="99be7-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Publish**.</span></span>

<span data-ttu-id="99be7-112">**如果您有未啟用 Azure 的 Web 應用程式專案︰**</span><span class="sxs-lookup"><span data-stu-id="99be7-112">**If you have a web application project that is not enabled for Azure:**</span></span>

1. <span data-ttu-id="99be7-113">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="99be7-113">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="99be7-114">在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**轉換** > **轉換 tooAzure 雲端服務專案**。</span><span class="sxs-lookup"><span data-stu-id="99be7-114">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Convert** > **Convert tooAzure Cloud Service Project**.</span></span> 

1. <span data-ttu-id="99be7-115">在**方案總管 中**、 以滑鼠右鍵按一下新建立的 hello Azure 專案，和 hello 內容功能表中選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="99be7-115">In **Solution Explorer**, right-click hello newly created Azure project, and, from hello context menu, select **Publish**.</span></span>

## <a name="sign-in-page"></a><span data-ttu-id="99be7-116">登入頁面</span><span class="sxs-lookup"><span data-stu-id="99be7-116">Sign-in page</span></span>

![登入頁面](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

<span data-ttu-id="99be7-118">**帳戶**-選取的帳戶，或選取**將帳戶加入**hello 帳戶下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="99be7-118">**Account** - Select an account or select **Add an account** in hello account dropdown list.</span></span>

<span data-ttu-id="99be7-119">**選擇您的訂用帳戶**-選擇部署的 hello 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="99be7-119">**Choose your subscription** - Choose hello subscription toouse for your deployment.</span></span>
   
## <a name="settings-page---common-settings-tab"></a><span data-ttu-id="99be7-120">設定頁面 - 一般設定索引標籤</span><span class="sxs-lookup"><span data-stu-id="99be7-120">Settings page - Common Settings tab</span></span>   

![一般設定](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

<span data-ttu-id="99be7-122">**雲端服務**-使用 hello 下拉式清單中，選取現有的雲端服務，或選取**&lt;新建 >**，並建立雲端服務。</span><span class="sxs-lookup"><span data-stu-id="99be7-122">**Cloud service** - Using hello dropdown, either select an existing cloud service, or select **&lt;Create New>**, and create a cloud service.</span></span> <span data-ttu-id="99be7-123">hello 資料中心會顯示在括號內的每個雲端服務。</span><span class="sxs-lookup"><span data-stu-id="99be7-123">hello data center displays in parentheses for each cloud service.</span></span> <span data-ttu-id="99be7-124">建議的 hello 資料中心位置 hello 雲端服務是 hello 相同為 hello hello 儲存體帳戶 （進階設定） 的資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="99be7-124">It is recommended that hello data center location for hello cloud service be hello same as hello data center location for hello storage account (Advanced Settings).</span></span>  

<span data-ttu-id="99be7-125">**環境** - 選取 [生產] 或 [預備]。</span><span class="sxs-lookup"><span data-stu-id="99be7-125">**Environment** - Select either **Production** or **Staging**.</span></span> <span data-ttu-id="99be7-126">選擇在測試環境中的 hello 預備環境，如果您想 toodeploy 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="99be7-126">Choose hello staging environment if you want toodeploy your application in a test environment.</span></span> 

<span data-ttu-id="99be7-127">**建置組態** - 選取 [偵錯] 或 [發行]。</span><span class="sxs-lookup"><span data-stu-id="99be7-127">**Build configuration** - Select either **Debug** or **Release**.</span></span>

<span data-ttu-id="99be7-128">**服務組態** - 選取 [雲端] 或 [本機]。</span><span class="sxs-lookup"><span data-stu-id="99be7-128">**Service configuration** - Select either **Cloud** or **Local**.</span></span>
   
<span data-ttu-id="99be7-129">**啟用所有角色的遠端桌面**-核取此選項，如果您想 toobe 無法 tooremotely toohello 服務連接。</span><span class="sxs-lookup"><span data-stu-id="99be7-129">**Enable Remote Desktop for all roles** - Check this option if you want toobe able tooremotely connect toohello service.</span></span> <span data-ttu-id="99be7-130">此選項主要用於疑難排解。</span><span class="sxs-lookup"><span data-stu-id="99be7-130">This option is primarily used for troubleshooting.</span></span> <span data-ttu-id="99be7-131">當您選取此核取方塊時，hello**遠端桌面組態** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="99be7-131">When you select this check box, hello **Remote Desktop Configuration** dialog box appears.</span></span> <span data-ttu-id="99be7-132">選擇 hello**設定**連結 toochange hello 組態。</span><span class="sxs-lookup"><span data-stu-id="99be7-132">Choose hello **Settings** link toochange hello configuration.</span></span>
   
<span data-ttu-id="99be7-133">**啟用所有 web 角色的 Web Deploy** -核取此選項，tooenable hello 服務的 web 部署。</span><span class="sxs-lookup"><span data-stu-id="99be7-133">**Enable Web Deploy for all web roles** - Check this option, tooenable web deployment for hello service.</span></span> <span data-ttu-id="99be7-134">您必須選取 hello**啟用所有角色的遠端桌面**選項 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="99be7-134">You must select hello **Enable Remote Desktop for all roles** option toouse this feature.</span></span> <span data-ttu-id="99be7-135">如需詳細資訊，請參閱[[使用 Visual Studio 發佈 Azure 雲端服務](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99be7-135">For more information, see [[Publishing a Azure cloud service using Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx).</span></span> 

## <a name="settings-page---advanced-settings-tab"></a><span data-ttu-id="99be7-136">設定頁面 - 進階設定索引標籤</span><span class="sxs-lookup"><span data-stu-id="99be7-136">Settings page - Advanced Settings tab</span></span>

![進階設定](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

<span data-ttu-id="99be7-138">**部署標籤**-接受 hello 預設名稱，或輸入您所選擇的名稱。</span><span class="sxs-lookup"><span data-stu-id="99be7-138">**Deployment label** - Either accept hello default name, or enter a name of your choosing.</span></span> <span data-ttu-id="99be7-139">tooappend hello 日期 toohello 部署標籤，選取保持 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="99be7-139">tooappend hello date toohello deployment label, leave hello check box selected.</span></span> 
   
<span data-ttu-id="99be7-140">**儲存體帳戶**-選取 hello 這個部署的儲存體帳戶 toouse * *&lt;新建 > toocreate 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="99be7-140">**Storage account** - Select hello storage account toouse for this deployment, **&lt;Create New> toocreate a storage account.</span></span> <span data-ttu-id="99be7-141">hello 資料中心會顯示在括號內的每個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="99be7-141">hello data center displays in parentheses for each storage account.</span></span> <span data-ttu-id="99be7-142">建議的 hello 資料中心位置 hello 儲存體帳戶是 hello 相同為 hello hello 雲端服務 （通用設定） 的資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="99be7-142">It is recommended that hello data center location for hello storage account be hello same as hello data center location for hello cloud service (Common Settings).</span></span>  
   
<span data-ttu-id="99be7-143">hello Azure 儲存體帳戶會儲存 hello 應用程式部署的 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="99be7-143">hello Azure storage account stores hello package for hello application deployment.</span></span> <span data-ttu-id="99be7-144">Hello 應用程式部署之後，hello 封裝會從 hello 儲存體帳戶中移除。</span><span class="sxs-lookup"><span data-stu-id="99be7-144">After hello application is deployed, hello package is removed from hello storage account.</span></span>

<span data-ttu-id="99be7-145">**失敗時刪除部署**-選取發行期間發生任何錯誤，如果刪除此選項 toohave hello 部署。</span><span class="sxs-lookup"><span data-stu-id="99be7-145">**Delete deployment on failure** - Select this option toohave hello deployment deleted if any errors are encountered during publishing.</span></span> <span data-ttu-id="99be7-146">如果您要為您的雲端服務的 toomaintain 常數的虛擬 IP 位址，這應取消選取。</span><span class="sxs-lookup"><span data-stu-id="99be7-146">This should be unchecked if you want toomaintain a constant virtual IP address for your cloud service.</span></span>

<span data-ttu-id="99be7-147">**部署更新**-選取此選項，如果您想 toodeploy 只更新的元件。</span><span class="sxs-lookup"><span data-stu-id="99be7-147">**Deployment update** - Select this option if you want toodeploy only updated components.</span></span> <span data-ttu-id="99be7-148">這種部署類型比完整部署更快速。</span><span class="sxs-lookup"><span data-stu-id="99be7-148">This type of deployment can be faster than a full deployment.</span></span> <span data-ttu-id="99be7-149">如果您要為您的雲端服務的 toomaintain 常數的虛擬 IP 位址應該檢查此。</span><span class="sxs-lookup"><span data-stu-id="99be7-149">This should be checked if you want toomaintain a constant virtual IP address for your cloud service.</span></span> 

<span data-ttu-id="99be7-150">**部署更新-設定**-使用此對話方塊是 toofurther 可讓您指定要更新的 hello 角色 toobe 的方式。</span><span class="sxs-lookup"><span data-stu-id="99be7-150">**Deployment update - settings** - This dialog is used toofurther specify how you want hello roles toobe updated.</span></span> <span data-ttu-id="99be7-151">如果您選擇**累加式更新**，應用程式的每個執行個體是更新之後，因此該 hello 應用程式永遠都是可用。</span><span class="sxs-lookup"><span data-stu-id="99be7-151">If you choose **Incremental update**, each instance of your application is updated one after another, so that hello application is always available.</span></span> <span data-ttu-id="99be7-152">如果您選擇**同時更新**，在 hello 更新您的應用程式的所有執行個體相同的時間。</span><span class="sxs-lookup"><span data-stu-id="99be7-152">If you choose **Simultaneous update**, all instances of your application are updated at hello same time.</span></span> <span data-ttu-id="99be7-153">同時更新較為快速，但您的服務可能無法使用 hello 更新程序期間。</span><span class="sxs-lookup"><span data-stu-id="99be7-153">Simultaneous updating is faster, but your service might not be available during hello update process.</span></span> 

![部署設定](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

<span data-ttu-id="99be7-155">**啟用 IntelliTrace** -指定是否要讓 tooenable IntelliTrace。</span><span class="sxs-lookup"><span data-stu-id="99be7-155">**Enable IntelliTrace** - Specify if you want tooenable IntelliTrace.</span></span> <span data-ttu-id="99be7-156">有了 IntelliTrace，您可以於角色執行個體在 Azure 中執行時，記錄其廣泛的偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="99be7-156">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="99be7-157">如果您需要 toofind hello 問題的原因，您可以使用 hello IntelliTrace 記錄檔 toostep，透過您的程式碼，從 Visual Studio 在 Azure 中執行一樣即可。</span><span class="sxs-lookup"><span data-stu-id="99be7-157">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="99be7-158">如需使用 IntelliTrace 的詳細資訊，請參閱[使用 Visual Studio 和 IntelliTrace 進行已發佈 Azure 雲端服務的偵錯](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)。</span><span class="sxs-lookup"><span data-stu-id="99be7-158">For more information about using IntelliTrace, see [Debugging a published Azure cloud service with Visual Studio and IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md).</span></span> 

<span data-ttu-id="99be7-159">**啟用程式碼剖析**-指定是否要 tooenable 效能分析。</span><span class="sxs-lookup"><span data-stu-id="99be7-159">**Enable profiling** - Specify if you want tooenable performance profiling.</span></span> <span data-ttu-id="99be7-160">hello Visual Studio 分析工具可讓您 tooget hello 情況在計算方面的雲端服務的執行方式的深入分析。</span><span class="sxs-lookup"><span data-stu-id="99be7-160">hello Visual Studio profiler enables you tooget an in-depth analysis of hello computational aspects of how your cloud service runs.</span></span> <span data-ttu-id="99be7-161">如需有關使用 hello Visual Studio 分析工具的詳細資訊，請參閱[測試 Azure 雲端服務的 hello 效能](./vs-azure-tools-performance-profiling-cloud-services.md)。</span><span class="sxs-lookup"><span data-stu-id="99be7-161">For more information on using hello Visual Studio profiler, see [Test hello performance of an Azure cloud service](./vs-azure-tools-performance-profiling-cloud-services.md).</span></span>

<span data-ttu-id="99be7-162">**啟用所有角色的遠端偵錯工具**-指定是否要 tooenable 遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="99be7-162">**Enable Remote Debugger for all roles** - Specify if you want tooenable remote debugging.</span></span> <span data-ttu-id="99be7-163">如需使用 Visual Studio 進行雲端服務偵錯的詳細資訊，請參閱[在 Visual Studio 中進行 Azure 雲端服務或虛擬機器的偵錯](./vs-azure-tools-debug-cloud-services-virtual-machines.md)。</span><span class="sxs-lookup"><span data-stu-id="99be7-163">For more information on debugging cloud services using Visual Studio, see [Debugging an Azure cloud service or virtual machine in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).</span></span>

## <a name="diagnostics-settings-page"></a><span data-ttu-id="99be7-164">診斷設定頁面</span><span class="sxs-lookup"><span data-stu-id="99be7-164">Diagnostics Settings page</span></span>

![診斷設定](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

<span data-ttu-id="99be7-166">診斷可讓您 tootroubleshoot Azure 雲端服務 （或 Azure 虛擬機器）。</span><span class="sxs-lookup"><span data-stu-id="99be7-166">Diagnostics enables you tootroubleshoot an Azure cloud service (or Azure virtual machine).</span></span> <span data-ttu-id="99be7-167">如需診斷的相關資訊，請參閱[為 Azure 雲端服務和虛擬機器設定診斷功能](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。</span><span class="sxs-lookup"><span data-stu-id="99be7-167">For information about diagnostics, see [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> <span data-ttu-id="99be7-168">如需 Application Insights 的相關資訊，請參閱[什麼是 Application Insights？](./application-insights/app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="99be7-168">For information about Application Insights, see [What is Application Insights?](./application-insights/app-insights-overview.md).</span></span>

## <a name="summary-page"></a><span data-ttu-id="99be7-169">摘要頁面</span><span class="sxs-lookup"><span data-stu-id="99be7-169">Summary page</span></span>

![摘要](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

<span data-ttu-id="99be7-171">**Profile 當做目標**-您可以選擇 toocreate 發行設定檔從您所選擇的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="99be7-171">**Target profile** - You can choose toocreate a publishing profile from hello settings that you have chosen.</span></span> <span data-ttu-id="99be7-172">例如，您可能會建立一個設定檔用於測試環境，並建立另一個用於生產。</span><span class="sxs-lookup"><span data-stu-id="99be7-172">For example, you might create one profile for a test environment and another for production.</span></span> <span data-ttu-id="99be7-173">toosave 這個設定檔，選擇 hello**儲存**圖示。</span><span class="sxs-lookup"><span data-stu-id="99be7-173">toosave this profile, choose hello **Save** icon.</span></span> <span data-ttu-id="99be7-174">hello 精靈會建立 hello 設定檔，並將它儲存在 hello Visual Studio 專案中。</span><span class="sxs-lookup"><span data-stu-id="99be7-174">hello wizard creates hello profile and saves it in hello Visual Studio project.</span></span> <span data-ttu-id="99be7-175">toomodify hello 設定檔名稱，開啟 hello **profile 當做目標**清單，，然後選擇**< 管理... >**。</span><span class="sxs-lookup"><span data-stu-id="99be7-175">toomodify hello profile name, open hello **Target profile** list, and then choose **<Manage…>**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="99be7-176">hello 發行設定檔會出現在 Visual Studio 中的 [方案總管] 中，hello 設定檔設定寫入 tooa 副檔名為.azurePubxml 的檔案。</span><span class="sxs-lookup"><span data-stu-id="99be7-176">hello publishing profile appears in Solution Explorer in Visual Studio, and hello profile settings are written tooa file with an .azurePubxml extension.</span></span> <span data-ttu-id="99be7-177">設定會儲存為 XML 標記的屬性。</span><span class="sxs-lookup"><span data-stu-id="99be7-177">Settings are saved as attributes of XML tags.</span></span>
   > 
   > 

## <a name="publishing-your-application"></a><span data-ttu-id="99be7-178">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="99be7-178">Publishing your application</span></span>

<span data-ttu-id="99be7-179">一旦您設定您的專案部署的所有 hello 設定時，選取**發行**在 hello hello 對話方塊底部。</span><span class="sxs-lookup"><span data-stu-id="99be7-179">Once you configure all hello settings for your project's deployment, select **Publish** at hello bottom of hello dialog.</span></span> <span data-ttu-id="99be7-180">您可以監視 hello 處理序狀態在 hello**輸出**Visual Studio 中的視窗。</span><span class="sxs-lookup"><span data-stu-id="99be7-180">You can monitor hello process status in hello **Output** window in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99be7-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99be7-181">Next steps</span></span>
- [<span data-ttu-id="99be7-182">移轉並發行 Web 應用程式 tooan 從 Visual Studio 的 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="99be7-182">Migrate and publish a Web Application tooan Azure cloud service from Visual Studio</span></span>](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [<span data-ttu-id="99be7-183">了解如何 toouse Visual Studio toopublish Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="99be7-183">Learn how toouse Visual Studio toopublish an Azure cloud service</span></span>](./vs-azure-tools-publishing-a-cloud-service.md)
- [<span data-ttu-id="99be7-184">使用 Visual Studio 和 IntelliTrace 進行已發佈 Azure 雲端服務的偵錯</span><span class="sxs-lookup"><span data-stu-id="99be7-184">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [<span data-ttu-id="99be7-185">測試 Azure 雲端服務的 hello 效能</span><span class="sxs-lookup"><span data-stu-id="99be7-185">Test hello performance of an Azure cloud service</span></span>](./vs-azure-tools-performance-profiling-cloud-services.md)
- <span data-ttu-id="99be7-186">[為 Azure 雲端服務和虛擬機器設定診斷功能](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。</span><span class="sxs-lookup"><span data-stu-id="99be7-186">[Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> 
- [<span data-ttu-id="99be7-187">什麼是 Application Insights？</span><span class="sxs-lookup"><span data-stu-id="99be7-187">What is Application Insights?</span></span>](./application-insights/app-insights-overview.md)