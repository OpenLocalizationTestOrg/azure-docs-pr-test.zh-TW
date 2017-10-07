---
title: "aaaConfigure hello 角色的 Azure 雲端服務與 Visual Studio |Microsoft 文件"
description: "深入了解如何 tooset 安裝及設定 Azure 雲端服務使用 Visual Studio 的角色。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="555cc-103">使用 Visual Studio 設定 Azure 雲端服務角色</span><span class="sxs-lookup"><span data-stu-id="555cc-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="555cc-104">Azure 雲端服務可以有一或多個背景工作角色或 web 角色。</span><span class="sxs-lookup"><span data-stu-id="555cc-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="555cc-105">每個角色，您需要該角色的設定方式的 toodefine 與也設定該角色的執行方式。</span><span class="sxs-lookup"><span data-stu-id="555cc-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="555cc-106">進一步了解雲端服務中的角色 toolearn 看到 hello 視訊[簡介 tooAzure 雲端服務](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services)。</span><span class="sxs-lookup"><span data-stu-id="555cc-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="555cc-107">為雲端服務的 hello 資訊會儲存在 hello 下列檔案：</span><span class="sxs-lookup"><span data-stu-id="555cc-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="555cc-108">**ServiceDefinition.csdef** -hello 服務定義檔定義您的雲端服務，包括所需的角色、 端點和虛擬機器大小的 hello 執行階段設定。</span><span class="sxs-lookup"><span data-stu-id="555cc-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="555cc-109">不會儲存在 hello 資料`ServiceDefinition.csdef`角色正在執行時，可以變更。</span><span class="sxs-lookup"><span data-stu-id="555cc-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="555cc-110">**ServiceConfiguration.cscfg** -hello 服務組態檔會設定執行多少個角色執行個體，並為角色定義 hello hello 設定值。</span><span class="sxs-lookup"><span data-stu-id="555cc-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="555cc-111">hello 資料儲存在`ServiceConfiguration.cscfg`角色正在執行時，可以變更。</span><span class="sxs-lookup"><span data-stu-id="555cc-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="555cc-112">toostore 不同值的 hello 設定該角色的執行方式的控制項，則您可以定義多個服務組態。</span><span class="sxs-lookup"><span data-stu-id="555cc-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="555cc-113">您可以將不同的服務組態用於每個部署環境。</span><span class="sxs-lookup"><span data-stu-id="555cc-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="555cc-114">比方說，您可以在本機服務組態設定儲存體帳戶連接字串 toouse hello 本機 Azure 儲存體模擬器，並在 hello 雲端中建立另一個服務組態 toouse Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="555cc-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="555cc-115">當您在 Visual Studio 中建立 Azure 雲端服務時，則兩個服務組態會自動建立，並且加入 tooyour Azure 專案：</span><span class="sxs-lookup"><span data-stu-id="555cc-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="555cc-116">設定 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="555cc-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="555cc-117">Hello 步驟中所示，您可以在 Visual Studio 設定 Azure 雲端服務從方案總管:</span><span class="sxs-lookup"><span data-stu-id="555cc-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="555cc-118">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="555cc-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="555cc-119">在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="555cc-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![方案總管專案操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="555cc-121">在 hello 專案屬性頁面上，選取 hello**開發** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="555cc-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![專案屬性頁面- 開發索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="555cc-123">在 hello**服務組態**清單中，選取 hello 想 tooedit hello 服務組態名稱。</span><span class="sxs-lookup"><span data-stu-id="555cc-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="555cc-124">(如果您想 toomake 變更 tooall hello 服務組態，為這個角色，請選取**所有組態**。)</span><span class="sxs-lookup"><span data-stu-id="555cc-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="555cc-125">如果您選擇特定服務組態，某些屬性會停用，因為它們只能針對所有組態設定。</span><span class="sxs-lookup"><span data-stu-id="555cc-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="555cc-126">tooedit 這些屬性，您必須選取**所有組態**。</span><span class="sxs-lookup"><span data-stu-id="555cc-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Azure 雲端服務的服務組態清單](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="555cc-128">變更角色執行個體的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="555cc-128">Change hello number of role instances</span></span>
<span data-ttu-id="555cc-129">tooimprove hello 雲端服務的效能，您可以變更角色的執行，使用者或特定角色的預期的 hello 負載的 hello 數目為基礎的執行個體的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="555cc-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="555cc-130">不同的虛擬機器角色的每個執行個體執行時所建立 hello 雲端服務在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="555cc-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="555cc-131">這會影響這個雲端服務的 hello 部署的 hello 計費。</span><span class="sxs-lookup"><span data-stu-id="555cc-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="555cc-132">如需計費的詳細資訊，請參閱[了解 Microsoft Azure 帳單](billing/billing-understand-your-bill.md)。</span><span class="sxs-lookup"><span data-stu-id="555cc-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="555cc-133">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="555cc-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="555cc-134">在**方案總管 中**，展開 hello 專案節點。</span><span class="sxs-lookup"><span data-stu-id="555cc-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="555cc-135">在 hello**角色**節點、 以滑鼠右鍵按一下您想 tooupdate，並從 hello 內容功能表中，選取 hello 角色**屬性**。</span><span class="sxs-lookup"><span data-stu-id="555cc-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![方案總管 Azure 角色操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="555cc-137">選取 hello**組態** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="555cc-137">Select hello **Configuration** tab.</span></span>

    ![組態索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="555cc-139">在 hello**服務組態**清單中，您想 tooupdate 選取 hello 服務組態。</span><span class="sxs-lookup"><span data-stu-id="555cc-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![服務組態清單](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="555cc-141">在 hello**執行個體計數**文字方塊中，輸入您要此角色 toostart 的執行個體的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="555cc-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="555cc-142">當您發行 hello 雲端服務 tooAzure 個別的虛擬機器執行每個執行個體。</span><span class="sxs-lookup"><span data-stu-id="555cc-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![更新 hello 執行個體計數](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="555cc-144">Hello Visual Studio 中，從工具列上，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="555cc-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="555cc-145">管理儲存體帳戶的連接字串</span><span class="sxs-lookup"><span data-stu-id="555cc-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="555cc-146">您可以新增、移除或修改服務組態的連接字串。</span><span class="sxs-lookup"><span data-stu-id="555cc-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="555cc-147">例如，針對具有 `UseDevelopmentStorage=true`值的本機服務組態，您可能想要本機連接字串。</span><span class="sxs-lookup"><span data-stu-id="555cc-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="555cc-148">您也可以 tooconfigure 在 Azure 中使用的儲存體帳戶的雲端服務組態。</span><span class="sxs-lookup"><span data-stu-id="555cc-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="555cc-149">當您輸入的儲存體帳戶連接字串的 hello Azure 儲存體帳戶金鑰資訊時，這項資訊儲存在本機 hello 服務組態檔中。</span><span class="sxs-lookup"><span data-stu-id="555cc-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="555cc-150">不過，這項資訊目前不會儲存為加密文字。</span><span class="sxs-lookup"><span data-stu-id="555cc-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="555cc-151">每個服務組態使用不同的值，執行不在您的雲端服務中有 toouse 不同的連接字串或您發行您的雲端服務 tooAzure 時修改程式碼。</span><span class="sxs-lookup"><span data-stu-id="555cc-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="555cc-152">您可以使用相同的名稱，針對您的程式碼和 hello 值中的 hello 的連接字串是不同，根據您選取當您建置您的雲端服務，或將它發行的 hello 服務組態的 hello。</span><span class="sxs-lookup"><span data-stu-id="555cc-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="555cc-153">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="555cc-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="555cc-154">在**方案總管 中**，展開 hello 專案節點。</span><span class="sxs-lookup"><span data-stu-id="555cc-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="555cc-155">在 hello**角色**節點、 以滑鼠右鍵按一下您想 tooupdate，並從 hello 內容功能表中，選取 hello 角色**屬性**。</span><span class="sxs-lookup"><span data-stu-id="555cc-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![方案總管 Azure 角色操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="555cc-157">選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="555cc-157">Select hello **Settings** tab.</span></span>

    ![[設定] 索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="555cc-159">在 hello**服務組態**清單中，您想 tooupdate 選取 hello 服務組態。</span><span class="sxs-lookup"><span data-stu-id="555cc-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![服務組態](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="555cc-161">tooadd 連接字串中，選取**加入設定**。</span><span class="sxs-lookup"><span data-stu-id="555cc-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![新增連接字串](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="555cc-163">一旦 hello 新設定已新增 toohello 清單，更新 hello 清單中的 hello 列 hello 必要資訊。</span><span class="sxs-lookup"><span data-stu-id="555cc-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![New connection string](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="555cc-165">**名稱**-輸入您要的連接字串 hello toouse hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="555cc-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="555cc-166">**型別**-選取**連接字串**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="555cc-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="555cc-167">**值**-您可以直接在 hello 輸入 hello 連接字串**值**資料格或選取 hello hello 中的省略符號 （...） toowork**建立儲存體連接字串**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="555cc-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="555cc-168">在 hello**建立儲存體連接字串**對話方塊中，選取一個選項，如**使用連接**。</span><span class="sxs-lookup"><span data-stu-id="555cc-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="555cc-169">然後依照您所選取的 hello 選項 hello 指示：</span><span class="sxs-lookup"><span data-stu-id="555cc-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="555cc-170">**Microsoft Azure 儲存體模擬器**-如果您選取此選項，因為它們會套用只 tooAzure，會停用 hello hello 對話方塊上的其餘設定。</span><span class="sxs-lookup"><span data-stu-id="555cc-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="555cc-171">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="555cc-171">Select **OK**.</span></span>
    - <span data-ttu-id="555cc-172">**您的訂用帳戶**-如果您選取此選項，使用 hello 下拉式清單 tooeither 選取和登入 Microsoft 帳戶，或新增 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="555cc-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="555cc-173">選取 Azure 訂用帳戶和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="555cc-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="555cc-174">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="555cc-174">Select **OK**.</span></span>
    - <span data-ttu-id="555cc-175">**手動輸入的認證**-輸入 hello 儲存體帳戶名稱，並請 hello 主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="555cc-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="555cc-176">選取 **[連線]** 的 (在大部分情況下建議適用 HTTPS)。選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="555cc-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="555cc-177">toodelete 連接字串中，選取 hello 連接字串，然後選取**移除設定**。</span><span class="sxs-lookup"><span data-stu-id="555cc-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="555cc-178">Hello Visual Studio 中，從工具列上，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="555cc-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="555cc-179">以程式設計方式存取連接字串</span><span class="sxs-lookup"><span data-stu-id="555cc-179">Programmatically access a connection string</span></span>

<span data-ttu-id="555cc-180">hello 下列步驟顯示如何 tooprogrammatically 存取使用 C# 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="555cc-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="555cc-181">新增 hello 下列使用指示詞 tooa C# 檔案將 toouse hello 設定：</span><span class="sxs-lookup"><span data-stu-id="555cc-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="555cc-182">hello 下列程式碼說明如何的範例 tooaccess 連接字串。</span><span class="sxs-lookup"><span data-stu-id="555cc-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="555cc-183">取代 hello &lt;ConnectionStringName > 預留位置 hello 適當的值。</span><span class="sxs-lookup"><span data-stu-id="555cc-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="555cc-184">在 Azure 雲端服務中加入自訂設定 toouse</span><span class="sxs-lookup"><span data-stu-id="555cc-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="555cc-185">Hello 服務組態檔中的自訂設定可讓您加入的名稱及針對特定服務的組態字串的值。</span><span class="sxs-lookup"><span data-stu-id="555cc-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="555cc-186">您可以選擇您的雲端服務所讀取的 hello 值中的功能 hello 設定以及程式碼中使用此值 toocontrol hello 邏輯這個設定 tooconfigure toouse。</span><span class="sxs-lookup"><span data-stu-id="555cc-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="555cc-187">您可以變更這些服務組態值，而不需要 toorebuild 服務封裝，或您的雲端服務正在執行。</span><span class="sxs-lookup"><span data-stu-id="555cc-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="555cc-188">您的程式碼可以檢查設定變更時的通知。</span><span class="sxs-lookup"><span data-stu-id="555cc-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="555cc-189">請參閱 [RoleEnvironment.Changing 事件](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)。</span><span class="sxs-lookup"><span data-stu-id="555cc-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="555cc-190">您可以新增、移除或修改服務組態的自訂設定。</span><span class="sxs-lookup"><span data-stu-id="555cc-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="555cc-191">針對不同的服務組態，您可能會想要這些連接字串的不同值。</span><span class="sxs-lookup"><span data-stu-id="555cc-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="555cc-192">每個服務組態使用不同的值，請勿不在您的雲端服務中有 toouse 不同的字串或當您發行您的雲端服務 tooAzure 時修改程式碼。</span><span class="sxs-lookup"><span data-stu-id="555cc-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="555cc-193">您可以使用相同的名稱，您的程式碼和 hello 值中的 hello 字串是不同，根據您選取當您建置您的雲端服務，或將它發行的 hello 服務組態的 hello。</span><span class="sxs-lookup"><span data-stu-id="555cc-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="555cc-194">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="555cc-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="555cc-195">在**方案總管 中**，展開 hello 專案節點。</span><span class="sxs-lookup"><span data-stu-id="555cc-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="555cc-196">在 hello**角色**節點、 以滑鼠右鍵按一下您想 tooupdate，並從 hello 內容功能表中，選取 hello 角色**屬性**。</span><span class="sxs-lookup"><span data-stu-id="555cc-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![方案總管 Azure 角色操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="555cc-198">選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="555cc-198">Select hello **Settings** tab.</span></span>

    ![[設定] 索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="555cc-200">在 hello**服務組態**清單中，您想 tooupdate 選取 hello 服務組態。</span><span class="sxs-lookup"><span data-stu-id="555cc-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![服務組態清單](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="555cc-202">tooadd 自訂設定中，選取**加入設定**。</span><span class="sxs-lookup"><span data-stu-id="555cc-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![新增自訂設定](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="555cc-204">一旦 hello 新設定已新增 toohello 清單，更新 hello 清單中的 hello 列 hello 必要資訊。</span><span class="sxs-lookup"><span data-stu-id="555cc-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![新增自訂設定](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="555cc-206">**名稱**-輸入 hello hello 設定名稱。</span><span class="sxs-lookup"><span data-stu-id="555cc-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="555cc-207">**型別**-選取**字串**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="555cc-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="555cc-208">**值**-輸入 hello hello 設定值。</span><span class="sxs-lookup"><span data-stu-id="555cc-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="555cc-209">您可以輸入 hello 值直接插入 hello**值**資料格或選取 hello 省略符號 （...） tooenter hello 值 hello**編輯字串**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="555cc-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="555cc-210">toodelete 自訂設定中，選取 hello 設定，然後選取**移除設定**。</span><span class="sxs-lookup"><span data-stu-id="555cc-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="555cc-211">Hello Visual Studio 中，從工具列上，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="555cc-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="555cc-212">以程式設計方式存取自訂設定的值</span><span class="sxs-lookup"><span data-stu-id="555cc-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="555cc-213">hello 下列步驟顯示如何 tooprogrammatically 存取使用 C# 自訂設定。</span><span class="sxs-lookup"><span data-stu-id="555cc-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="555cc-214">新增 hello 下列使用指示詞 tooa C# 檔案將 toouse hello 設定：</span><span class="sxs-lookup"><span data-stu-id="555cc-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="555cc-215">hello 下列程式碼說明如何的範例 tooaccess 自訂設定。</span><span class="sxs-lookup"><span data-stu-id="555cc-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="555cc-216">取代 hello &lt;SettingName > 預留位置 hello 適當的值。</span><span class="sxs-lookup"><span data-stu-id="555cc-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="555cc-217">管理每個角色執行個體的本機儲存體</span><span class="sxs-lookup"><span data-stu-id="555cc-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="555cc-218">您可以為角色的每個執行個體新增本機檔案系統儲存體。</span><span class="sxs-lookup"><span data-stu-id="555cc-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="555cc-219">預存在於儲存體不是可存取哪些 hello 會儲存資料，hello 角色的其他執行個體或其他角色的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="555cc-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="555cc-220">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="555cc-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="555cc-221">在**方案總管 中**，展開 hello 專案節點。</span><span class="sxs-lookup"><span data-stu-id="555cc-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="555cc-222">在 hello**角色**節點、 以滑鼠右鍵按一下您想 tooupdate，並從 hello 內容功能表中，選取 hello 角色**屬性**。</span><span class="sxs-lookup"><span data-stu-id="555cc-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![方案總管 Azure 角色操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="555cc-224">選取 hello**本機儲存體** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="555cc-224">Select hello **Local Storage** tab.</span></span>

    ![本機儲存體索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="555cc-226">在 hello**服務組態**清單，請確定**所有組態**hello 本機儲存體設定適用於 tooall 服務組態已選取。</span><span class="sxs-lookup"><span data-stu-id="555cc-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="555cc-227">任何其他值會導致在 hello 頁面上，已停用的 hello 輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="555cc-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![服務組態清單](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="555cc-229">tooadd 本機儲存體項目中，選取**加入本機儲存體**。</span><span class="sxs-lookup"><span data-stu-id="555cc-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![新增本機儲存體](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="555cc-231">一旦 hello 新的本機儲存體項目已加入 toohello 清單，更新 hello 清單中的 hello 列 hello 必要資訊。</span><span class="sxs-lookup"><span data-stu-id="555cc-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![新增本機儲存體項目](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="555cc-233">**名稱**-輸入您要 hello 新的本機儲存體 toouse hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="555cc-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="555cc-234">**大小 (MB)** -輸入 hello 大小以 mb 為單位，您需要的 hello 新的本機存放裝置。</span><span class="sxs-lookup"><span data-stu-id="555cc-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="555cc-235">**清除在角色回收**-hello hello 角色的虛擬機器回收時，選取此選項 tooremove hello 資料 hello 新區域儲存區中。</span><span class="sxs-lookup"><span data-stu-id="555cc-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="555cc-236">toodelete 本機儲存體項目中，選取 hello 項目，然後再選取**移除本機儲存體**。</span><span class="sxs-lookup"><span data-stu-id="555cc-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="555cc-237">Hello Visual Studio 中，從工具列上，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="555cc-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="555cc-238">以程式設計方式存取本機儲存體</span><span class="sxs-lookup"><span data-stu-id="555cc-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="555cc-239">本節說明如何 tooprogrammatically 存取使用 C# 撰寫測試文字檔案的本機儲存體`MyLocalStorageTest.txt`。</span><span class="sxs-lookup"><span data-stu-id="555cc-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="555cc-240">寫入文字檔案 toolocal 存放裝置</span><span class="sxs-lookup"><span data-stu-id="555cc-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="555cc-241">hello，下列程式碼示範如何 toowrite 文字檔案 toolocal 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="555cc-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="555cc-242">取代 hello &lt;LocalStorageName > 預留位置 hello 適當的值。</span><span class="sxs-lookup"><span data-stu-id="555cc-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="555cc-243">尋找寫入 toolocal 儲存體的檔案</span><span class="sxs-lookup"><span data-stu-id="555cc-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="555cc-244">hello hello 前一節中的程式碼所建立的 tooview hello 檔案，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="555cc-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="555cc-245">在 hello Windows 通知區域中 hello Azure 圖示，以滑鼠右鍵按一下，然後從 hello 內容功能表中，選取**顯示計算模擬器 UI**。</span><span class="sxs-lookup"><span data-stu-id="555cc-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![顯示 Azure 計算模擬器](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="555cc-247">選取 hello web 角色。</span><span class="sxs-lookup"><span data-stu-id="555cc-247">Select hello web role.</span></span>

    ![Azure 計算模擬器](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="555cc-249">在 hello **Microsoft Azure 計算模擬器**功能表上，選取**工具** > **開啟本機存放區**。</span><span class="sxs-lookup"><span data-stu-id="555cc-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![開啟本機存放區功能表項目](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="555cc-251">當 hello Windows 檔案總管視窗開啟時，請輸入 'MyLocalStorageTest.txt' hello 到**搜尋**文字方塊，然後選取**Enter** toostart hello 搜尋。</span><span class="sxs-lookup"><span data-stu-id="555cc-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="555cc-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="555cc-252">Next steps</span></span>
<span data-ttu-id="555cc-253">藉由參閱 [設定 Azure 專案](vs-azure-tools-configuring-an-azure-project.md)深入了解 Visual Studio 中的 Azure 專案。</span><span class="sxs-lookup"><span data-stu-id="555cc-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="555cc-254">深入了解 hello 雲端服務結構描述讀取[結構描述參考](https://msdn.microsoft.com/library/azure/dd179398)。</span><span class="sxs-lookup"><span data-stu-id="555cc-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

