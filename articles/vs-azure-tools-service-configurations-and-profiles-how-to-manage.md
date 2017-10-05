---
title: "如何管理服務組態和設定檔 | Microsoft Docs"
description: "了解如何使用服務組態和設定檔組態檔案 | 其儲存部署環境的設定及雲端服務的發佈設定。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: af1205f8c3e477d123d4835c80a68b3afd6ee5ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-service-configurations-and-profiles"></a><span data-ttu-id="60260-103">如何管理服務組態和設定檔</span><span class="sxs-lookup"><span data-stu-id="60260-103">How to manage service configurations and profiles</span></span>
## <a name="overview"></a><span data-ttu-id="60260-104">Overview</span><span class="sxs-lookup"><span data-stu-id="60260-104">Overview</span></span>
<span data-ttu-id="60260-105">當您發佈雲端服務時，Visual Studio 會將組態資訊儲存在兩種組態檔中：服務組態和設定檔。</span><span class="sxs-lookup"><span data-stu-id="60260-105">When you publish a cloud service, Visual Studio stores configuration information in two kinds of configuration files: service configurations and profiles.</span></span> <span data-ttu-id="60260-106">服務組態 (.cscfg 檔) 可儲存 Azure 雲端服務的部署環境設定。</span><span class="sxs-lookup"><span data-stu-id="60260-106">Service configurations (.cscfg files) store settings for the deployment environments for an Azure cloud service.</span></span> <span data-ttu-id="60260-107">Azure 會在管理雲端服務時使用這些組態檔。</span><span class="sxs-lookup"><span data-stu-id="60260-107">Azure uses these configuration files when it manages your cloud services.</span></span> <span data-ttu-id="60260-108">另一方面，設定檔 (.azurePubxml 檔案) 可儲存雲端服務的發佈設定。</span><span class="sxs-lookup"><span data-stu-id="60260-108">On the other hand, profiles (.azurePubxml files) store publish settings for cloud services.</span></span> <span data-ttu-id="60260-109">這些設定是您使用發佈精靈時所選內容的記錄，可由 Visual Studio 在本機使用。</span><span class="sxs-lookup"><span data-stu-id="60260-109">These settings are a record of what you choose when you use the publish wizard, and are used locally by Visual Studio.</span></span> <span data-ttu-id="60260-110">本主題說明如何使用這兩種類型的組態檔。</span><span class="sxs-lookup"><span data-stu-id="60260-110">This topic explains how to work with both types of configuration files.</span></span>

## <a name="service-configurations"></a><span data-ttu-id="60260-111">服務組態</span><span class="sxs-lookup"><span data-stu-id="60260-111">Service Configurations</span></span>
<span data-ttu-id="60260-112">您可以建立多個服務組態，以便用於每個部署環境。</span><span class="sxs-lookup"><span data-stu-id="60260-112">You can create multiple service configurations to use for each of your deployment environments.</span></span> <span data-ttu-id="60260-113">例如，您可針對用來執行和測試 Azure 應用程式的本機環境建立一個服務組態，針對實際執行環境建立另一個服務組態。</span><span class="sxs-lookup"><span data-stu-id="60260-113">For example, you might create a service configuration for the local environment that you use to run and test an Azure application and another service configuration for your production environment.</span></span>

<span data-ttu-id="60260-114">您可以根據需求來新增、刪除、重新命名和修改這些服務組態。</span><span class="sxs-lookup"><span data-stu-id="60260-114">You can add, delete, rename, and modify these service configurations based on your requirements.</span></span> <span data-ttu-id="60260-115">您可以從 Visual Studio 管理這些服務組態，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="60260-115">You can manage these service configurations from Visual Studio, as shown in the following illustration.</span></span>

![管理服務組態](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

<span data-ttu-id="60260-117">您也可以從角色的屬性頁面開啟 [管理組態]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="60260-117">You can also open the **Manage Configurations** dialog box from the role’s property pages.</span></span> <span data-ttu-id="60260-118">若要開啟 Azure 專案中角色的屬性，請開啟該角色的捷徑功能表，然後選擇 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="60260-118">To open the properties for a role in your Azure project, open the shortcut menu for that role, and then choose **Properties**.</span></span> <span data-ttu-id="60260-119">在 [設定] 索引標籤上，展開 [服務組態] 清單，然後選取 [管理] 以開啟 [管理組態] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="60260-119">On the **Settings** tab, expand the **Service Configuration** list, and then select **Manage** to open the **Manage Configurations** dialog box.</span></span>

### <a name="to-add-a-service-configuration"></a><span data-ttu-id="60260-120">新增服務組態</span><span class="sxs-lookup"><span data-stu-id="60260-120">To add a service configuration</span></span>
1. <span data-ttu-id="60260-121">在 [方案總管] 中，開啟 Azure 專案的捷徑功能表，然後選取 [管理組態] 。</span><span class="sxs-lookup"><span data-stu-id="60260-121">In Solution Explorer, open the shortcut menu for the Azure project and then select **Manage Configurations**.</span></span>
   
    <span data-ttu-id="60260-122">[管理服務組態]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="60260-122">The **Manage Service Configurations** dialog box appears.</span></span>
2. <span data-ttu-id="60260-123">若要新增服務組態，您必須建立一份現有的組態。</span><span class="sxs-lookup"><span data-stu-id="60260-123">To add a service configuration, you must create a copy of an existing configuration.</span></span> <span data-ttu-id="60260-124">若要這樣做，請從 [名稱] 清單中選擇您要複製的組態，然後選取 [建立複本] 。</span><span class="sxs-lookup"><span data-stu-id="60260-124">To do this, choose the configuration that you want to copy from the Name list and then select **Create copy**.</span></span>
3. <span data-ttu-id="60260-125">(選擇性) 若要給予服務組態不同的名稱，請從 [名稱] 清單中選擇新的服務組態，然後選取 [重新命名] 。</span><span class="sxs-lookup"><span data-stu-id="60260-125">(Optional) To give the service configuration a different name, choose the new service configuration from the Name list and then select **Rename**.</span></span> <span data-ttu-id="60260-126">在 [名稱] 文字方塊中輸入您要用於此服務組態的名稱，然後按選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="60260-126">In the **Name** text box, type the name that you want to use for this service configuration and then select **OK**.</span></span>
   
    <span data-ttu-id="60260-127">方案總管中的 Azure 專案已新增了一個叫做 ServiceConfiguration.[New Name].cscfg 的新服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="60260-127">A new service configuration file that is named ServiceConfiguration.[New Name].cscfg is added to the Azure project in Solution Explorer.</span></span>

### <a name="to-delete-a-service-configuration"></a><span data-ttu-id="60260-128">刪除服務組態</span><span class="sxs-lookup"><span data-stu-id="60260-128">To delete a service configuration</span></span>
1. <span data-ttu-id="60260-129">在 [方案總管] 中，開啟 Azure 專案的捷徑功能表，然後選取 [管理組態] 。</span><span class="sxs-lookup"><span data-stu-id="60260-129">In Solution Explorer, open the shortcut menu for the Azure project and then select **Manage Configurations**.</span></span>
   
    <span data-ttu-id="60260-130">[管理服務組態]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="60260-130">The **Manage Service Configurations** dialog box appears.</span></span>
2. <span data-ttu-id="60260-131">若要刪除服務組態，請從 [名稱] 清單中選擇您要刪除的組態，然後選取 [移除]。</span><span class="sxs-lookup"><span data-stu-id="60260-131">To delete a service configuration, choose the configuration that you want to delete from the **Name** list and then select **Remove**.</span></span> <span data-ttu-id="60260-132">隨即出現一個對話方塊，以確認您要刪除此組態。</span><span class="sxs-lookup"><span data-stu-id="60260-132">A dialog box appears to verify that you want to delete this configuration.</span></span>
3. <span data-ttu-id="60260-133">選取 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="60260-133">Select **Delete**.</span></span>
   
     <span data-ttu-id="60260-134">在 [方案總管] 中，此服務組態檔會從 Azure 專案中移除。</span><span class="sxs-lookup"><span data-stu-id="60260-134">The service configuration file is removed from the Azure project in Solution Explorer.</span></span>

### <a name="to-rename-a-service-configuration"></a><span data-ttu-id="60260-135">重新命名服務組態</span><span class="sxs-lookup"><span data-stu-id="60260-135">To rename a service configuration</span></span>
1. <span data-ttu-id="60260-136">在 [方案總管] 中，開啟 Azure 專案的捷徑功能表，然後選取 [管理組態] 。</span><span class="sxs-lookup"><span data-stu-id="60260-136">In Solution Explorer, open the shortcut menu for the Azure project, and then select **Manage Configurations**.</span></span>
   
    <span data-ttu-id="60260-137">[管理服務組態]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="60260-137">The **Manage Service Configurations** dialog box appears.</span></span>
2. <span data-ttu-id="60260-138">若要將服務組態重新命名，請從 [名稱] 清單中選擇新的服務組態，然後選取 [重新命名]。</span><span class="sxs-lookup"><span data-stu-id="60260-138">To rename a service configuration, choose the new service configuration from the **Name** list, and then select **Rename**.</span></span> <span data-ttu-id="60260-139">在 [名稱] 文字方塊中輸入您要用於此服務組態的名稱，然後按選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="60260-139">In the **Name** text box, type the name that you want to use for this service configuration, and then select **OK**.</span></span>
   
    <span data-ttu-id="60260-140">在 [方案總管] 中，此服務組態檔的名稱會在 Azure 專案中變更。</span><span class="sxs-lookup"><span data-stu-id="60260-140">The name of the service configuration file is changed in the Azure project in Solution Explorer.</span></span>

### <a name="to-change-a-service-configuration"></a><span data-ttu-id="60260-141">變更服務組態</span><span class="sxs-lookup"><span data-stu-id="60260-141">To change a service configuration</span></span>
* <span data-ttu-id="60260-142">如果您想要變更服務組態，請開啟 Azure 專案中您要變更的特定角色的捷徑功能表，然後按一下 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="60260-142">If you want to change a service configuration, open the shortcut menu for the specific role you want to change in the Azure project, and then select **Properties**.</span></span> <span data-ttu-id="60260-143">如需詳細資訊，請參閱 [如何：使用 Visual Studio 設定 Azure 雲端服務的角色](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) 。</span><span class="sxs-lookup"><span data-stu-id="60260-143">See [How to: Configure the Roles for an Azure Cloud Service with Visual Studio](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) for more information.</span></span>

## <a name="make-different-setting-combinations-by-using-profiles"></a><span data-ttu-id="60260-144">使用設定檔製作不同的設定組合</span><span class="sxs-lookup"><span data-stu-id="60260-144">Make different setting combinations by using profiles</span></span>
<span data-ttu-id="60260-145">只要使用設定檔，您就能針對不同用途，以不同的設定組合來自動填滿 [發佈精靈]  。</span><span class="sxs-lookup"><span data-stu-id="60260-145">By using a profile, you can automatically fill in the **Publish Wizard** with different combinations of settings for different purposes.</span></span> <span data-ttu-id="60260-146">例如，您可有一個設定檔用於偵錯，另一個設定檔用於發行組建。</span><span class="sxs-lookup"><span data-stu-id="60260-146">For example, you can have one profile for debugging and another for release builds.</span></span> <span data-ttu-id="60260-147">在此情況下，[偵錯] 設定檔會啟用 [IntelliTrace] 並選取 [偵錯] 組態，而 [發行] 設定檔會停用 [IntelliTrace] 並選取 [發行] 組態。</span><span class="sxs-lookup"><span data-stu-id="60260-147">In that case, your **Debug** profile would have **IntelliTrace** enabled and the **Debug** configuration selected, and your **Release** profile would have **IntelliTrace** disabled and the **Release** configuration selected.</span></span> <span data-ttu-id="60260-148">您也可以使用不同的設定檔，部署使用不同儲存體帳戶的服務。</span><span class="sxs-lookup"><span data-stu-id="60260-148">You could also use different profiles to deploy a service using a different storage account.</span></span>

<span data-ttu-id="60260-149">當您第一次執行精靈時，會建立預設設定檔。</span><span class="sxs-lookup"><span data-stu-id="60260-149">When you run the wizard for the first time, a default profile is created.</span></span> <span data-ttu-id="60260-150">Visual Studio 會將此設定檔儲存在副檔名為 .azurePubXml 的檔案中，而該檔案會新增至 Azure 專案的 [設定檔]  資料夾之下。</span><span class="sxs-lookup"><span data-stu-id="60260-150">Visual Studio stores the profile in a file that has an .azurePubXml extension, which is added to your Azure project under the **Profiles** folder.</span></span> <span data-ttu-id="60260-151">如果您在執行精靈時手動指定不同的選擇，此檔案會自動更新。</span><span class="sxs-lookup"><span data-stu-id="60260-151">If you manually specify different choices when you run the wizard later, the file automatically updates.</span></span> <span data-ttu-id="60260-152">執行下列程序之前，您應該已經發佈您的雲端服務至少一次。</span><span class="sxs-lookup"><span data-stu-id="60260-152">Before you run the following procedure, you should have already published your cloud service at least once.</span></span>

### <a name="to-add-a-profile"></a><span data-ttu-id="60260-153">新增設定檔</span><span class="sxs-lookup"><span data-stu-id="60260-153">To add a profile</span></span>
1. <span data-ttu-id="60260-154">開啟 Azure 專案的捷徑功能表，然後選取 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="60260-154">Open the shortcut menu for your Azure project, and then select **Publish**.</span></span>
2. <span data-ttu-id="60260-155">選取 [目標設定檔] 清單旁邊的 [儲存設定檔] 按鈕，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="60260-155">Next to the **Target profile** list, select the **Save Profile** button, as the following illustration shows.</span></span> <span data-ttu-id="60260-156">這會為您建立設定檔。</span><span class="sxs-lookup"><span data-stu-id="60260-156">This creates a profile for you.</span></span>
   
    ![建立新的設定檔](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. <span data-ttu-id="60260-158">建立設定檔之後，選取 [目標設定檔] 清單中的 [<管理...>]。</span><span class="sxs-lookup"><span data-stu-id="60260-158">After the profile is created, select **<Manage…>** in the **Target profile** list.</span></span>
   
    <span data-ttu-id="60260-159">[管理設定檔]  對話方塊會隨即出現，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="60260-159">The **Manage Profiles** dialog box appears, as the following illustration shows.</span></span>
   
    ![管理設定檔對話方塊](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. <span data-ttu-id="60260-161">在 [名稱] 清單中選擇某個設定檔，然後選取 [建立複本]。</span><span class="sxs-lookup"><span data-stu-id="60260-161">In the **Name** list, choose a profile, and then select **Create Copy**.</span></span>
5. <span data-ttu-id="60260-162">選擇 [關閉]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="60260-162">Choose the **Close** button.</span></span>
   
    <span data-ttu-id="60260-163">新的設定檔會出現在 [目標設定檔] 清單中。</span><span class="sxs-lookup"><span data-stu-id="60260-163">The new profile appears in the Target profile list.</span></span>
6. <span data-ttu-id="60260-164">在 [目標設定檔]  清單中，選取您剛建立的設定檔。</span><span class="sxs-lookup"><span data-stu-id="60260-164">In the **Target profile** list, select the profile that you just created.</span></span> <span data-ttu-id="60260-165">[發佈精靈] 設定會填入您所選設定檔中的選項。</span><span class="sxs-lookup"><span data-stu-id="60260-165">The Publish Wizard settings are filled in with the choices from the profile you selected.</span></span>
7. <span data-ttu-id="60260-166">選取 [上一步] 和 [下一步] 按鈕以顯示「發佈精靈」的每個頁面，然後自訂此設定檔的設定。</span><span class="sxs-lookup"><span data-stu-id="60260-166">Select the **Previous** and **Next** buttons to display each page of the Publish Wizard, and then customize the settings for this profile.</span></span> <span data-ttu-id="60260-167">如需相關資訊，請參閱 [發佈 Azure 應用程式精靈](http://go.microsoft.com/fwlink/p/?LinkID=623085) 。</span><span class="sxs-lookup"><span data-stu-id="60260-167">See [Publish Azure Application Wizard](http://go.microsoft.com/fwlink/p/?LinkID=623085) for information.</span></span>
8. <span data-ttu-id="60260-168">自訂完設定之後，選取 [下一步]  以返回「設定」頁面。</span><span class="sxs-lookup"><span data-stu-id="60260-168">After you finish customizing the settings, select **Next** to go back to the Settings page.</span></span> <span data-ttu-id="60260-169">當您使用這些設定來發佈服務，或是選取設定檔清單旁邊的 [儲存]  時，就會儲存設定檔。</span><span class="sxs-lookup"><span data-stu-id="60260-169">The profile is saved when you publish the service by using these settings or if you select **Save** next to the list of profiles.</span></span>

### <a name="to-rename-or-delete-a-profile"></a><span data-ttu-id="60260-170">重新命名或刪除設定檔</span><span class="sxs-lookup"><span data-stu-id="60260-170">To rename or delete a profile</span></span>
1. <span data-ttu-id="60260-171">開啟 Azure 專案的捷徑功能表，然後選取 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="60260-171">Open the shortcut menu for your Azure project, and then select **Publish**.</span></span>
2. <span data-ttu-id="60260-172">在 [目標設定檔] 清單中，選取 [管理]。</span><span class="sxs-lookup"><span data-stu-id="60260-172">In the **Target profile** list, select **Manage**.</span></span>
3. <span data-ttu-id="60260-173">在 [管理設定檔] 對話方塊方塊中，選取您要刪除的設定檔，然後選取 [移除]。</span><span class="sxs-lookup"><span data-stu-id="60260-173">In the **Manage Profiles** dialog box, select the profile that you want to delete, and then select **Remove**.</span></span>
4. <span data-ttu-id="60260-174">在出現的確認對話方塊中，選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="60260-174">In the confirmation dialog box that appears, select **OK**.</span></span>
5. <span data-ttu-id="60260-175">選取 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="60260-175">Select **Close**.</span></span>

### <a name="to-change-a-profile"></a><span data-ttu-id="60260-176">變更設定檔</span><span class="sxs-lookup"><span data-stu-id="60260-176">To change a profile</span></span>
1. <span data-ttu-id="60260-177">開啟 Azure 專案的捷徑功能表，然後選取 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="60260-177">Open the shortcut menu for your Azure project, and then select **Publish**.</span></span>
2. <span data-ttu-id="60260-178">在 [目標設定檔]  清單中，選取您要變更的設定檔。</span><span class="sxs-lookup"><span data-stu-id="60260-178">In the **Target profile** list, select the profile that you want to change.</span></span>
3. <span data-ttu-id="60260-179">選取 [上一步] 和 [下一步] 按鈕以顯示「發佈精靈」的每個頁面，然後變更您想要的設定。</span><span class="sxs-lookup"><span data-stu-id="60260-179">Select the **Previous** and **Next** buttons to display each page of the Publish Wizard, and then change the settings you want.</span></span> <span data-ttu-id="60260-180">如需相關資訊，請參閱 [發佈 Azure 應用程式精靈](http://go.microsoft.com/fwlink/p/?LinkID=623085) 。</span><span class="sxs-lookup"><span data-stu-id="60260-180">See [Publish Azure Application Wizard](http://go.microsoft.com/fwlink/p/?LinkID=623085) for information.</span></span>
4. <span data-ttu-id="60260-181">變更完設定之後，選取 [下一步] 以返回**「設定」**頁面。</span><span class="sxs-lookup"><span data-stu-id="60260-181">After you finish changing the settings, select **Next** to go back to the **Settings** page.</span></span>
5. <span data-ttu-id="60260-182">(選擇性) 選取 [發佈]  以使用新設定來發佈雲端服務。</span><span class="sxs-lookup"><span data-stu-id="60260-182">(Optional) select **Publish** to publish the cloud service using the new settings.</span></span> <span data-ttu-id="60260-183">如果您不想在此時發佈雲端服務，而關閉 [發佈精靈]，Visual Studio 會詢問您是否要將變更儲存至設定檔。</span><span class="sxs-lookup"><span data-stu-id="60260-183">If you don’t want to publish your cloud service at this time, and you close the Publish Wizard, Visual Studio asks you if you want to save the changes to the profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60260-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60260-184">Next steps</span></span>
<span data-ttu-id="60260-185">若要了解如何從 Visual Studio 設定 Azure 專案的其他部分，請參閱 [設定 Azure 專案](http://go.microsoft.com/fwlink/p/?LinkID=623075)</span><span class="sxs-lookup"><span data-stu-id="60260-185">To learn about configuring other parts of your Azure project from Visual Studio, see [Configuring an Azure Project](http://go.microsoft.com/fwlink/p/?LinkID=623075)</span></span>

