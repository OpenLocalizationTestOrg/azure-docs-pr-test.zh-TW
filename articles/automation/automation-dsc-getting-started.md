---
title: "開始使用 Azure Automation DSC 的 aaaGetting |Microsoft 文件"
description: "說明與 hello 最常見的工作在 Azure 自動化預期狀態設定 (DSC) 的範例"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="9f001-103">開始使用 Azure 自動化 DSC</span><span class="sxs-lookup"><span data-stu-id="9f001-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="9f001-104">本主題說明如何 toodo hello 與 Azure 自動化預期狀態設定 (DSC)，建立、 匯入，並編譯設定，登入機器太管理和檢視報表之類的常見工作。</span><span class="sxs-lookup"><span data-stu-id="9f001-104">This topic explains how toodo hello most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines too manage, and viewing reports.</span></span> <span data-ttu-id="9f001-105">如需何謂 Azure 自動化 DSC 的概觀，請參閱 [Azure 自動化 DSC 概觀](automation-dsc-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9f001-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="9f001-106">如需 DSC 文件，請參閱 [Windows PowerShell 預期狀態設定概觀](https://msdn.microsoft.com/PowerShell/dsc/overview)。</span><span class="sxs-lookup"><span data-stu-id="9f001-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="9f001-107">本主題提供逐步指南 toousing Azure Automation DSC。</span><span class="sxs-lookup"><span data-stu-id="9f001-107">This topic provides a step-by-step guide toousing Azure Automation DSC.</span></span> <span data-ttu-id="9f001-108">如果您想未遵循本主題中所述的 hello 步驟已經設定好的範例環境，您可以使用[hello ARM 範本下列](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup)。</span><span class="sxs-lookup"><span data-stu-id="9f001-108">If you want a sample environment that is already set up without following hello steps described in this topic, you can use [hello following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="9f001-109">此範本會設定完整的 Azure 自動化 DSC 環境，包括由 Azure 自動化 DSC 管理的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="9f001-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f001-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9f001-110">Prerequisites</span></span>
<span data-ttu-id="9f001-111">本主題中的 toocomplete hello 範例，hello 需要下列憑證：</span><span class="sxs-lookup"><span data-stu-id="9f001-111">toocomplete hello examples in this topic, hello following are required:</span></span>

* <span data-ttu-id="9f001-112">Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f001-112">An Azure Automation account.</span></span> <span data-ttu-id="9f001-113">如需建立 Azure 自動化執行身分帳戶的指示，請參閱 [Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)。</span><span class="sxs-lookup"><span data-stu-id="9f001-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="9f001-114">執行 Windows Server 2008 R2 或更新版本的 Azure Resource Manager VM (不是傳統)。</span><span class="sxs-lookup"><span data-stu-id="9f001-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="9f001-115">如需建立 VM 的指示，請參閱[hello Azure 入口網站中建立第一個 Windows 虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="9f001-115">For instructions on creating a VM, see [Create your first Windows virtual machine in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="9f001-116">建立 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="9f001-116">Creating a DSC configuration</span></span>
<span data-ttu-id="9f001-117">我們將建立簡單[DSC 設定](https://msdn.microsoft.com/powershell/dsc/configurations)這可確保 hello 存在或不存在的 hello **Web 伺服器**Windows 功能 (IIS)，根據您指定節點的方式。</span><span class="sxs-lookup"><span data-stu-id="9f001-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either hello presence or absence of hello **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="9f001-118">啟動 Windows PowerShell ISE hello （或任何文字編輯器）。</span><span class="sxs-lookup"><span data-stu-id="9f001-118">Start hello Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="9f001-119">輸入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f001-119">Type hello following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="9f001-120">將 hello 檔案儲存為`TestConfig.ps1`。</span><span class="sxs-lookup"><span data-stu-id="9f001-120">Save hello file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="9f001-121">這項設定會呼叫一項資源中每個節點區塊，hello [WindowsFeature 資源](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource)，這可確保 hello 存在或不存在的 hello **Web 伺服器**功能。</span><span class="sxs-lookup"><span data-stu-id="9f001-121">This configuration calls one resource in each node block, hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either hello presence or absence of hello **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="9f001-122">將組態匯入 Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="9f001-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="9f001-123">接下來，我們將會匯入 hello 組態 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f001-123">Next, we'll import hello configuration into hello Automation account.</span></span>

1. <span data-ttu-id="9f001-124">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-125">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-125">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-126">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 設定**。</span><span class="sxs-lookup"><span data-stu-id="9f001-126">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="9f001-127">在 hello **DSC 設定**刀鋒視窗中，按一下 **加入組態**。</span><span class="sxs-lookup"><span data-stu-id="9f001-127">On hello **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="9f001-128">在 hello**匯入組態**刀鋒視窗中，瀏覽 toohello`TestConfig.ps1`電腦上的檔案。</span><span class="sxs-lookup"><span data-stu-id="9f001-128">On hello **Import Configuration** blade, browse toohello `TestConfig.ps1` file on your computer.</span></span>
   
    ![螢幕擷取畫面的 hello * * 匯入設定 * * 刀鋒視窗](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="9f001-130">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9f001-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="9f001-131">在 Azure 自動化中檢視組態</span><span class="sxs-lookup"><span data-stu-id="9f001-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="9f001-132">在匯入組態之後，您可以在 hello Azure 入口網站中檢視它。</span><span class="sxs-lookup"><span data-stu-id="9f001-132">After you have imported a configuration, you can view it in hello Azure portal.</span></span>

1. <span data-ttu-id="9f001-133">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-133">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-134">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-134">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-135">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 設定**</span><span class="sxs-lookup"><span data-stu-id="9f001-135">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="9f001-136">在 hello **DSC 設定**刀鋒視窗中，按一下  **TestConfig** （這是您所匯入的 hello 組態的名稱，hello hello 前程序中）。</span><span class="sxs-lookup"><span data-stu-id="9f001-136">On hello **DSC Configurations** blade, click **TestConfig** (this is hello name of hello configuration you imported in hello previous procedure).</span></span>
5. <span data-ttu-id="9f001-137">在 hello **TestConfig 組態**刀鋒視窗中，按一下**檢視組態來源**。</span><span class="sxs-lookup"><span data-stu-id="9f001-137">On hello **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Hello TestConfig 組態刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="9f001-139">A **TestConfig 組態來源**刀鋒視窗隨即開啟，顯示 hello 組態 hello PowerShell 程式碼。</span><span class="sxs-lookup"><span data-stu-id="9f001-139">A **TestConfig Configuration source** blade opens, displaying hello PowerShell code for hello configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="9f001-140">在 Azure 自動化中編譯組態</span><span class="sxs-lookup"><span data-stu-id="9f001-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="9f001-141">您可以套用所需的狀態 tooa 節點之前，必須編譯成一或多個節點組態 （MOF 文件），並放在 hello 自動化 DSC 提取伺服器上 DSC 設定定義該狀態。</span><span class="sxs-lookup"><span data-stu-id="9f001-141">Before you can apply a desired state tooa node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on hello Automation DSC Pull Server.</span></span> <span data-ttu-id="9f001-142">如需在 Azure 自動化 DSC 中編譯設定的詳細說明，請參閱 [在 Azure 自動化 DSC 中編譯設定](automation-dsc-compile.md)。</span><span class="sxs-lookup"><span data-stu-id="9f001-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="9f001-143">如需編譯設定的詳細資訊，請參閱 [DSC 設定](https://msdn.microsoft.com/PowerShell/DSC/configurations)。</span><span class="sxs-lookup"><span data-stu-id="9f001-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="9f001-144">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-144">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-145">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-145">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-146">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 設定**</span><span class="sxs-lookup"><span data-stu-id="9f001-146">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="9f001-147">在 hello **DSC 設定**刀鋒視窗中，按一下  **TestConfig** （hello hello 名稱先前匯入組態）。</span><span class="sxs-lookup"><span data-stu-id="9f001-147">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="9f001-148">在 hello **TestConfig 組態**刀鋒視窗中，按一下 **編譯**，然後按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="9f001-148">On hello **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="9f001-149">這會啟動編譯作業。</span><span class="sxs-lookup"><span data-stu-id="9f001-149">This starts a compilation job.</span></span>
   
    ![編譯按鈕反白顯示的 hello TestConfig 組態刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="9f001-151">當您編譯 Azure 自動化中的組態時，自動將部署任何建立的節點設定 Mof toohello 提取伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f001-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs toohello pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="9f001-152">檢視編譯作業</span><span class="sxs-lookup"><span data-stu-id="9f001-152">Viewing a compilation job</span></span>
<span data-ttu-id="9f001-153">開始編譯之後，可以檢視在 hello**編譯工作**磚中 hello**組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f001-153">After you start a compilation, you can view it in hello **Compilation jobs** tile in hello **Configuration** blade.</span></span> <span data-ttu-id="9f001-154">hello**編譯工作**磚顯示目前正在執行、 已完成，以及失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="9f001-154">hello **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="9f001-155">當您開啟編譯工作刀鋒視窗時，它會顯示該工作，包括任何錯誤或警告發生的相關資訊、 輸入的參數用於 hello 組態和編譯記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9f001-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in hello configuration, and compilation logs.</span></span>

1. <span data-ttu-id="9f001-156">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-157">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-157">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-158">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 設定**。</span><span class="sxs-lookup"><span data-stu-id="9f001-158">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="9f001-159">在 hello **DSC 設定**刀鋒視窗中，按一下  **TestConfig** （hello hello 名稱先前匯入組態）。</span><span class="sxs-lookup"><span data-stu-id="9f001-159">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="9f001-160">在 hello**編譯工作**磚 hello **TestConfig 組態**刀鋒視窗中，按一下任何所列的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="9f001-160">On hello **Compilation jobs** tile of hello **TestConfig Configuration** blade, click on any of hello jobs listed.</span></span> <span data-ttu-id="9f001-161">A**編譯工作**啟動刀鋒視窗隨即開啟，加上 hello hello 編譯作業的日期。</span><span class="sxs-lookup"><span data-stu-id="9f001-161">A **Compilation Job** blade opens, labeled with hello date that hello compilation job was started.</span></span>
   
    ![Hello 編譯工作刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="9f001-163">按一下任何磚中 hello**編譯工作**進一步刀鋒視窗 toosee hello 作業的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9f001-163">Click on any tile in hello **Compilation Job** blade toosee further details about hello job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="9f001-164">檢視節點組態</span><span class="sxs-lookup"><span data-stu-id="9f001-164">Viewing node configurations</span></span>
<span data-ttu-id="9f001-165">成功完成編譯作業會建立一或多個新的節點組態。</span><span class="sxs-lookup"><span data-stu-id="9f001-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="9f001-166">節點設定為已部署的 toohello 提取伺服器與準備好 toobe 提取，且套用一個或多個節點的 MOF 文件。</span><span class="sxs-lookup"><span data-stu-id="9f001-166">A node configuration is a MOF document that is deployed toohello pull server and ready toobe pulled and applied by one or more nodes.</span></span> <span data-ttu-id="9f001-167">您可以檢視您的自動化帳戶中 hello hello 節點設定**DSC 節點組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f001-167">You can view hello node configurations in your Automation account in hello **DSC Node Configurations** blade.</span></span> <span data-ttu-id="9f001-168">節點組態都有名稱與 hello 表單*ConfigurationName*。*NodeName*。</span><span class="sxs-lookup"><span data-stu-id="9f001-168">A node configuration has a name with hello form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="9f001-169">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-170">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-170">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-171">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點組態**。</span><span class="sxs-lookup"><span data-stu-id="9f001-171">On hello **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Hello DSC 節點組態 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="9f001-173">將 Azure VM 上架以供 Azure 自動化 DSC 管理</span><span class="sxs-lookup"><span data-stu-id="9f001-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="9f001-174">您可以使用 Azure 自動化 DSC toomanage Azure Vm （傳統和資源管理員），在內部部署 Vm、 Linux 機器、 AWS Vm 和內部部署實體機器。</span><span class="sxs-lookup"><span data-stu-id="9f001-174">You can use Azure Automation DSC toomanage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="9f001-175">在本主題中，我們將討論如何 tooonboard Azure 資源管理員 Vm。</span><span class="sxs-lookup"><span data-stu-id="9f001-175">In this topic, we cover how tooonboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="9f001-176">如需將其他類型的機器上架的詳細資訊，請參閱 [將機器上架以供 Azure 自動化 DSC 管理](automation-dsc-onboarding.md)。</span><span class="sxs-lookup"><span data-stu-id="9f001-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="9f001-177">tooonboard 供 Azure Automation DSC 來管理 Azure 資源管理員 VM</span><span class="sxs-lookup"><span data-stu-id="9f001-177">tooonboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="9f001-178">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-179">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-179">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-180">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。</span><span class="sxs-lookup"><span data-stu-id="9f001-180">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="9f001-181">在 hello **DSC 節點**刀鋒視窗中，按一下 **新增 Azure VM**。</span><span class="sxs-lookup"><span data-stu-id="9f001-181">In hello **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Hello DSC 節點刀鋒視窗中反白顯示 hello 新增 Azure VM 按鈕的螢幕擷取畫面](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="9f001-183">在 hello**新增 Azure Vm**刀鋒視窗中，按一下 **選取虛擬機器 tooonboard**。</span><span class="sxs-lookup"><span data-stu-id="9f001-183">In hello **Add Azure VMs** blade, click **Select virtual machines tooonboard**.</span></span>
6. <span data-ttu-id="9f001-184">在 hello**選取 Vm**刀鋒視窗中，選取 hello VM tooonboard，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="9f001-184">In hello **Select VMs** blade, select hello VM you want tooonboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9f001-185">這必須是執行 Windows Server 2008 R2 或更新版本的 Azure Resource Manager VM。</span><span class="sxs-lookup"><span data-stu-id="9f001-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="9f001-186">在 hello**新增 Azure Vm**刀鋒視窗中，按一下 **設定註冊資料**。</span><span class="sxs-lookup"><span data-stu-id="9f001-186">In hello **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="9f001-187">在 hello**註冊**刀鋒視窗中，輸入 hello 名稱 hello 節點組態中，您想在 hello tooapply toohello VM**節點設定名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="9f001-187">In hello **Registration** blade, enter hello name of hello node configuration you want tooapply toohello VM in hello **Node Configuration Name** box.</span></span> <span data-ttu-id="9f001-188">這必須完全符合 hello hello 自動化帳戶中之節點組態的名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-188">This must exactly match hello name of a node configuration in hello Automation account.</span></span> <span data-ttu-id="9f001-189">在此時提供名稱是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="9f001-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="9f001-190">您可以變更指派的 hello 節點組態上架 hello 節點之後。</span><span class="sxs-lookup"><span data-stu-id="9f001-190">You can change hello assigned node configuration after onboarding hello node.</span></span>
   <span data-ttu-id="9f001-191">勾選 必要時重新啟動節點，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="9f001-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Hello 註冊刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="9f001-193">您指定的 hello 節點組態將會套用的 toohello VM hello 所指定的間隔**設定模式頻率**，和 hello VM 將會檢查在 hello所指定的間隔更新toohello節點組態**重新整理頻率**。</span><span class="sxs-lookup"><span data-stu-id="9f001-193">hello node configuration you specified will be applied toohello VM at intervals specified by hello **Configuration Mode Frequency**, and hello VM will check for updates toohello node configuration at intervals specified by hello **Refresh Frequency**.</span></span> <span data-ttu-id="9f001-194">如需有關如何使用這些值的詳細資訊，請參閱[設定 hello 本機設定管理員](https://msdn.microsoft.com/PowerShell/DSC/metaConfig)。</span><span class="sxs-lookup"><span data-stu-id="9f001-194">For more information about how these values are used, see [Configuring hello Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="9f001-195">在 hello**新增 Azure Vm**刀鋒視窗中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="9f001-195">In hello **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="9f001-196">Azure 將啟動上架 hello VM 的 hello 程的序。</span><span class="sxs-lookup"><span data-stu-id="9f001-196">Azure will start hello process of onboarding hello VM.</span></span> <span data-ttu-id="9f001-197">當完成時，hello VM 將會顯示在 hello **DSC 節點**hello 自動化帳戶中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f001-197">When it is complete, hello VM will show up in hello **DSC Nodes** blade in hello Automation account.</span></span>

## <a name="viewing-hello-list-of-dsc-nodes"></a><span data-ttu-id="9f001-198">檢視 hello DSC 節點清單</span><span class="sxs-lookup"><span data-stu-id="9f001-198">Viewing hello list of DSC nodes</span></span>
<span data-ttu-id="9f001-199">您可以檢視已被 onboarded hello 自動化帳戶中管理的所有機器的 hello 清單**DSC 節點**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f001-199">You can view hello list of all machines that have been onboarded for management in your Automation account in hello **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="9f001-200">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-200">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-201">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-201">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-202">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。</span><span class="sxs-lookup"><span data-stu-id="9f001-202">On hello **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="9f001-203">檢視 DSC 節點的報告</span><span class="sxs-lookup"><span data-stu-id="9f001-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="9f001-204">Azure 自動化 DSC 執行一致性檢查，受管理節點上，每次 hello 節點會傳送狀態報表後 toohello 提取伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f001-204">Each time Azure Automation DSC performs a consistency check on a managed node, hello node sends a status report back toohello pull server.</span></span> <span data-ttu-id="9f001-205">您可以在該節點的 hello 刀鋒視窗上檢視這些報表。</span><span class="sxs-lookup"><span data-stu-id="9f001-205">You can view these reports on hello blade for that node.</span></span>

1. <span data-ttu-id="9f001-206">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-206">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-207">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-207">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-208">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。</span><span class="sxs-lookup"><span data-stu-id="9f001-208">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="9f001-209">在 hello**報表**磚中，按一下任何 hello hello 清單中的報表。</span><span class="sxs-lookup"><span data-stu-id="9f001-209">On hello **Reports** tile, click on any of hello reports in hello list.</span></span>
   
    ![Hello 報表刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="9f001-211">在 hello 刀鋒視窗中個別報表，您可以看到 hello 下列狀態資訊的 hello 對應一致性檢查：</span><span class="sxs-lookup"><span data-stu-id="9f001-211">On hello blade for an individual report, you can see hello following status information for hello corresponding consistency check:</span></span>

* <span data-ttu-id="9f001-212">hello 報告狀態 — hello 節點是 「 符合標準 「 hello 設定 「 失敗 」，還是 hello 節點是 「 不相容 」 (當 hello 節點處於**applyandmonitor**模式和 hello 機器未處於預期的 hello 狀態)。</span><span class="sxs-lookup"><span data-stu-id="9f001-212">hello report status — whether hello node is "Compliant", hello configuration "Failed", or hello node is "Not Compliant" (when hello node is in **applyandmonitor** mode and hello machine is not in hello desired state).</span></span>
* <span data-ttu-id="9f001-213">hello hello 一致性檢查的開始時間。</span><span class="sxs-lookup"><span data-stu-id="9f001-213">hello start time for hello consistency check.</span></span>
* <span data-ttu-id="9f001-214">hello 總執行時間的 hello 一致性檢查。</span><span class="sxs-lookup"><span data-stu-id="9f001-214">hello total runtime for hello consistency check.</span></span>
* <span data-ttu-id="9f001-215">hello 的一致性檢查類型。</span><span class="sxs-lookup"><span data-stu-id="9f001-215">hello type of consistency check.</span></span>
* <span data-ttu-id="9f001-216">任何錯誤，包括 hello 錯誤程式碼和錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="9f001-216">Any errors, including hello error code and error message.</span></span> 
* <span data-ttu-id="9f001-217">Hello 組態和 hello 狀態，每個資源 （hello 節點是否在該資源的所需的 hello 狀態） 中使用任何 DSC 資源，您可以按一下每個資源 tooget 上更詳細的資源資訊。</span><span class="sxs-lookup"><span data-stu-id="9f001-217">Any DSC resources used in hello configuration, and hello state of each resource (whether hello node is in hello desired state for that resource) — you can click on each resource tooget more detailed information for that resource.</span></span>
* <span data-ttu-id="9f001-218">hello 名稱、 IP 位址和 hello 節點的組態模式。</span><span class="sxs-lookup"><span data-stu-id="9f001-218">hello name, IP address, and configuration mode of hello node.</span></span>

<span data-ttu-id="9f001-219">您也可以按一下**檢視未經處理的報表**toosee hello 實際資料 hello 節點傳送 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f001-219">You can also click **View raw report** toosee hello actual data that hello node sends toohello server.</span></span> <span data-ttu-id="9f001-220">如需有關使用該資料的詳細資訊，請參閱 [使用 DSC 報告伺服器](https://msdn.microsoft.com/powershell/dsc/reportserver)。</span><span class="sxs-lookup"><span data-stu-id="9f001-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="9f001-221">它可能需要一些時間之後的節點時 onboarded hello 第一份報表之前。</span><span class="sxs-lookup"><span data-stu-id="9f001-221">It can take some time after a node is onboarded before hello first report is available.</span></span> <span data-ttu-id="9f001-222">您可能需要向上 too30 分鐘 toowait hello 第一個報表之後，您將產品上架節點。</span><span class="sxs-lookup"><span data-stu-id="9f001-222">You might need toowait up too30 minutes for hello first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-tooa-different-node-configuration"></a><span data-ttu-id="9f001-223">重新指派節點 tooa 不同節點組態</span><span class="sxs-lookup"><span data-stu-id="9f001-223">Reassigning a node tooa different node configuration</span></span>
<span data-ttu-id="9f001-224">Hello 一個一開始指派比您可以指派指定節點 toouse 的不同節點設定。</span><span class="sxs-lookup"><span data-stu-id="9f001-224">You can assign a node toouse a different node configuration than hello one you initially assigned.</span></span>

1. <span data-ttu-id="9f001-225">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-225">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-226">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-226">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-227">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。</span><span class="sxs-lookup"><span data-stu-id="9f001-227">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="9f001-228">在 hello **DSC 節點**刀鋒視窗中，按一下 hello 名稱要 tooreassign 的 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="9f001-228">On hello **DSC Nodes** blade, click on hello name of hello node you want tooreassign.</span></span>
5. <span data-ttu-id="9f001-229">在該節點的 hello 刀鋒視窗，按一下 **指派節點**。</span><span class="sxs-lookup"><span data-stu-id="9f001-229">On hello blade for that node, click **Assign node**.</span></span>
   
    ![Hello 節點刀鋒視窗中反白顯示 hello 指派節點按鈕的螢幕擷取畫面](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="9f001-231">在 hello**指派節點設定**刀鋒視窗中，選取 hello 節點組態 toowhich tooassign hello 節點，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="9f001-231">On hello **Assign Node Configuration** blade, select hello node configuration toowhich you want tooassign hello node, and then click **OK**.</span></span>
   
    ![Hello 指派節點設定刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="9f001-233">取消註冊節點</span><span class="sxs-lookup"><span data-stu-id="9f001-233">Unregistering a node</span></span>
<span data-ttu-id="9f001-234">如果您不想再由 Azure Automation DSC 節點 toobe，您就可以將它移除註冊。</span><span class="sxs-lookup"><span data-stu-id="9f001-234">If you no longer want a node toobe managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="9f001-235">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9f001-235">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f001-236">在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f001-236">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9f001-237">在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。</span><span class="sxs-lookup"><span data-stu-id="9f001-237">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="9f001-238">在 hello **DSC 節點**刀鋒視窗中，按一下 hello 名稱要 toounregister 的 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="9f001-238">On hello **DSC Nodes** blade, click on hello name of hello node you want toounregister.</span></span>
5. <span data-ttu-id="9f001-239">在該節點的 hello 刀鋒視窗，按一下 **取消註冊**。</span><span class="sxs-lookup"><span data-stu-id="9f001-239">On hello blade for that node, click **Unregister**.</span></span>
   
    ![Hello 節點刀鋒視窗中反白顯示 hello 取消註冊按鈕的螢幕擷取畫面](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="9f001-241">相關文章</span><span class="sxs-lookup"><span data-stu-id="9f001-241">Related Articles</span></span>
* [<span data-ttu-id="9f001-242">Azure 自動化 DSC 概觀</span><span class="sxs-lookup"><span data-stu-id="9f001-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="9f001-243">上架由 Azure 自動化 DSC 管理的機器</span><span class="sxs-lookup"><span data-stu-id="9f001-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="9f001-244">Windows PowerShell 預期狀態設定概觀</span><span class="sxs-lookup"><span data-stu-id="9f001-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="9f001-245">Azure 自動化 DSC Cmdlet</span><span class="sxs-lookup"><span data-stu-id="9f001-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="9f001-246">Azure 自動化 DSC 價格</span><span class="sxs-lookup"><span data-stu-id="9f001-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

