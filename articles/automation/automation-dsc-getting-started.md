---
title: "開始使用 Azure 自動化 DSC | Microsoft Docs"
description: "Azure 自動化預期狀態設定 (DSC) 中最常見工作的說明和範例"
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
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="980f8-103">開始使用 Azure 自動化 DSC</span><span class="sxs-lookup"><span data-stu-id="980f8-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="980f8-104">本主題說明如何使用 Azure 自動化期望狀態設定 (DSC) 來執行常見的工作，例如建立、匯入和編譯組態、將要管理的機器上架，以及檢視報告。</span><span class="sxs-lookup"><span data-stu-id="980f8-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="980f8-105">如需何謂 Azure 自動化 DSC 的概觀，請參閱 [Azure 自動化 DSC 概觀](automation-dsc-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="980f8-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="980f8-106">如需 DSC 文件，請參閱 [Windows PowerShell 預期狀態設定概觀](https://msdn.microsoft.com/PowerShell/dsc/overview)。</span><span class="sxs-lookup"><span data-stu-id="980f8-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="980f8-107">本主題提供如何使用 Azure 自動化 DSC 的逐步指南。</span><span class="sxs-lookup"><span data-stu-id="980f8-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="980f8-108">如果您不想遵循本主題中所述的步驟，但想要已經設定好的範例環境，您可以使用 [下列 ARM 範本](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup)。</span><span class="sxs-lookup"><span data-stu-id="980f8-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="980f8-109">此範本會設定完整的 Azure 自動化 DSC 環境，包括由 Azure 自動化 DSC 管理的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="980f8-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="980f8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="980f8-110">Prerequisites</span></span>
<span data-ttu-id="980f8-111">若要完成本主題中的範例，需要有下列項目：</span><span class="sxs-lookup"><span data-stu-id="980f8-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="980f8-112">Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="980f8-112">An Azure Automation account.</span></span> <span data-ttu-id="980f8-113">如需建立 Azure 自動化執行身分帳戶的指示，請參閱 [Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)。</span><span class="sxs-lookup"><span data-stu-id="980f8-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="980f8-114">執行 Windows Server 2008 R2 或更新版本的 Azure Resource Manager VM (不是傳統)。</span><span class="sxs-lookup"><span data-stu-id="980f8-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="980f8-115">如需建立 VM 的指示，請參閱 [在 Azure 入口網站中建立第一個 Windows 虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="980f8-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="980f8-116">建立 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="980f8-116">Creating a DSC configuration</span></span>
<span data-ttu-id="980f8-117">我們將建立簡單的 [DSC 設定](https://msdn.microsoft.com/powershell/dsc/configurations) ，根據您指派節點的方式，確定是否有 **Web 伺服器** Windows 功能 (IIS) 存在。</span><span class="sxs-lookup"><span data-stu-id="980f8-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="980f8-118">啟動 Windows PowerShell ISE (或任何文字編輯器)。</span><span class="sxs-lookup"><span data-stu-id="980f8-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="980f8-119">輸入下列文字：</span><span class="sxs-lookup"><span data-stu-id="980f8-119">Type the following text:</span></span>
   
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
3. <span data-ttu-id="980f8-120">將檔案儲存為 `TestConfig.ps1`。</span><span class="sxs-lookup"><span data-stu-id="980f8-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="980f8-121">此設定會在每個節點區塊中呼叫一個資源 ( [WindowsFeature 資源](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource))，這可確保 **Web 伺服器** 功能是否存在。</span><span class="sxs-lookup"><span data-stu-id="980f8-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="980f8-122">將組態匯入 Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="980f8-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="980f8-123">接下來，我們會將組態匯入自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="980f8-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="980f8-124">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-125">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-126">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 組態]。</span><span class="sxs-lookup"><span data-stu-id="980f8-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="980f8-127">在 [DSC 組態] 刀鋒視窗上，按一下 [新增組態]。</span><span class="sxs-lookup"><span data-stu-id="980f8-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="980f8-128">在 [匯入組態] 刀鋒視窗上，瀏覽至您電腦上的 `TestConfig.ps1` 檔案。</span><span class="sxs-lookup"><span data-stu-id="980f8-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![[匯入組態] 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="980f8-130">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="980f8-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="980f8-131">在 Azure 自動化中檢視組態</span><span class="sxs-lookup"><span data-stu-id="980f8-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="980f8-132">在匯入組態之後，您可以在 Azure 入口網站中檢視它。</span><span class="sxs-lookup"><span data-stu-id="980f8-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="980f8-133">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-134">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-135">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 組態]</span><span class="sxs-lookup"><span data-stu-id="980f8-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="980f8-136">在 [DSC 組態] 刀鋒視窗上，按一下 [TestConfig] \(這是您在上一個程序中匯入的組態名稱)。</span><span class="sxs-lookup"><span data-stu-id="980f8-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="980f8-137">在 [TestConfig 組態] 刀鋒視窗上，按一下 [檢視組態來源]。</span><span class="sxs-lookup"><span data-stu-id="980f8-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![TestConfig 組態刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="980f8-139">[TestConfig 設定來源]  刀鋒視窗隨即開啟，顯示此設定的 PowerShell 程式碼。</span><span class="sxs-lookup"><span data-stu-id="980f8-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="980f8-140">在 Azure 自動化中編譯組態</span><span class="sxs-lookup"><span data-stu-id="980f8-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="980f8-141">定義預期狀態的 DSC 組態必須先編譯成一或多個節點組態 (MOF 文件)，並放在自動化 DSC 提取伺服器上，才可以將該預期狀態套用至節點。</span><span class="sxs-lookup"><span data-stu-id="980f8-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="980f8-142">如需在 Azure 自動化 DSC 中編譯設定的詳細說明，請參閱 [在 Azure 自動化 DSC 中編譯設定](automation-dsc-compile.md)。</span><span class="sxs-lookup"><span data-stu-id="980f8-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="980f8-143">如需編譯設定的詳細資訊，請參閱 [DSC 設定](https://msdn.microsoft.com/PowerShell/DSC/configurations)。</span><span class="sxs-lookup"><span data-stu-id="980f8-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="980f8-144">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-145">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-146">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 組態]</span><span class="sxs-lookup"><span data-stu-id="980f8-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="980f8-147">在 [DSC 組態] 刀鋒視窗上，按一下 [TestConfig] \(先前匯入的組態名稱)。</span><span class="sxs-lookup"><span data-stu-id="980f8-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="980f8-148">在 [TestConfig 組態] 刀鋒視窗上，按一下 [編譯]，然後按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="980f8-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="980f8-149">這會啟動編譯作業。</span><span class="sxs-lookup"><span data-stu-id="980f8-149">This starts a compilation job.</span></span>
   
    ![醒目提示編譯按鈕之 TestConfig 組態刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="980f8-151">當您在 Azure 自動化中編譯組態時，它會自動將任何已建立的節點組態 MOF 部署至提取伺服器。</span><span class="sxs-lookup"><span data-stu-id="980f8-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="980f8-152">檢視編譯作業</span><span class="sxs-lookup"><span data-stu-id="980f8-152">Viewing a compilation job</span></span>
<span data-ttu-id="980f8-153">啟動編譯之後，您可以在 [組態] 刀鋒視窗的 [編譯作業] 圖格中檢視它。</span><span class="sxs-lookup"><span data-stu-id="980f8-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="980f8-154">[編譯作業]  圖格會顯示目前執行中、已完成及失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="980f8-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="980f8-155">當您開啟編譯作業刀鋒視窗時，它會顯示該工作的相關資訊，包括發生的任何錯誤或警告、組態中使用的參數以及編譯記錄檔。</span><span class="sxs-lookup"><span data-stu-id="980f8-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="980f8-156">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-157">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-158">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 組態]。</span><span class="sxs-lookup"><span data-stu-id="980f8-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="980f8-159">在 [DSC 組態] 刀鋒視窗上，按一下 [TestConfig] \(先前匯入的組態名稱)。</span><span class="sxs-lookup"><span data-stu-id="980f8-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="980f8-160">在 [TestConfig 組態] 刀鋒視窗的 [編譯作業] 圖格上，按一下任何列出的工作。</span><span class="sxs-lookup"><span data-stu-id="980f8-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="980f8-161">[編譯作業]  刀鋒視窗隨即開啟，並標示編譯作業的啟動日期。</span><span class="sxs-lookup"><span data-stu-id="980f8-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![[編譯作業] 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="980f8-163">按一下 [編譯作業]  刀鋒視窗中的任何圖格，以查看作業的進一步詳細資料。</span><span class="sxs-lookup"><span data-stu-id="980f8-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="980f8-164">檢視節點組態</span><span class="sxs-lookup"><span data-stu-id="980f8-164">Viewing node configurations</span></span>
<span data-ttu-id="980f8-165">成功完成編譯作業會建立一或多個新的節點組態。</span><span class="sxs-lookup"><span data-stu-id="980f8-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="980f8-166">節點組態是已部署到提取伺服器且準備由一或多個節點提取並套用的 MOF 文件。</span><span class="sxs-lookup"><span data-stu-id="980f8-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="980f8-167">您可以在 [DSC 節點設定]  刀鋒視窗中檢視您的自動化帳戶的節點設定。</span><span class="sxs-lookup"><span data-stu-id="980f8-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="980f8-168">節點組態的名稱格式為 ConfigurationName.NodeName。</span><span class="sxs-lookup"><span data-stu-id="980f8-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="980f8-169">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-170">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-171">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 節點組態]。</span><span class="sxs-lookup"><span data-stu-id="980f8-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![[DSC 節點組態] 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="980f8-173">將 Azure VM 上架以供 Azure 自動化 DSC 管理</span><span class="sxs-lookup"><span data-stu-id="980f8-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="980f8-174">您可以使用 Azure 自動化 DSC 來管理 Azure VM (傳統和 Resource Manager)、內部部署 VM、Linux 機器、AWS VM 和內部部署實體機器。</span><span class="sxs-lookup"><span data-stu-id="980f8-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="980f8-175">在本主題中，我們將討論如何只上架 Azure Resource Manager VM。</span><span class="sxs-lookup"><span data-stu-id="980f8-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="980f8-176">如需將其他類型的機器上架的詳細資訊，請參閱 [將機器上架以供 Azure 自動化 DSC 管理](automation-dsc-onboarding.md)。</span><span class="sxs-lookup"><span data-stu-id="980f8-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="980f8-177">將 Azure Resource Manager VM 上架以便 Azure 自動化 DSC 管理</span><span class="sxs-lookup"><span data-stu-id="980f8-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="980f8-178">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-179">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-180">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 節點]。</span><span class="sxs-lookup"><span data-stu-id="980f8-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="980f8-181">在 [DSC 節點] 刀鋒視窗中，按一下 [新增 Azure VM]。</span><span class="sxs-lookup"><span data-stu-id="980f8-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![醒目提示 [新增 Azure VM] 按鈕之 [DSC 節點] 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="980f8-183">在 [新增 Azure VM] 刀鋒視窗中，按一下 [選取要上架的虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="980f8-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="980f8-184">在 [選取 VM] 刀鋒視窗中，選取您要上架的 VM，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="980f8-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="980f8-185">這必須是執行 Windows Server 2008 R2 或更新版本的 Azure Resource Manager VM。</span><span class="sxs-lookup"><span data-stu-id="980f8-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="980f8-186">在 [新增 Azure VM] 刀鋒視窗中，按一下 [設定註冊資料]。</span><span class="sxs-lookup"><span data-stu-id="980f8-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="980f8-187">在 [註冊] 刀鋒視窗的 [節點組態名稱] 方塊中，輸入您要套用至 VM 的節點組態名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="980f8-188">這必須完全符合自動化帳戶中的節點組態名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="980f8-189">在此時提供名稱是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="980f8-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="980f8-190">您可以在節點上架後，變更指派的節點組態。</span><span class="sxs-lookup"><span data-stu-id="980f8-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="980f8-191">勾選 [必要時重新啟動節點]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="980f8-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![[註冊] 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="980f8-193">您指定的節點設定會依 [設定模式頻率] 所指定的間隔套用到 VM，而 VM 會依 [重新整理頻率] 所指定的間隔檢查節點組態的更新。</span><span class="sxs-lookup"><span data-stu-id="980f8-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="980f8-194">如需有關如何使用這些值的詳細資訊，請參閱 [設定本機設定管理員](https://msdn.microsoft.com/PowerShell/DSC/metaConfig)。</span><span class="sxs-lookup"><span data-stu-id="980f8-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="980f8-195">在 [新增 Azure VM] 刀鋒視窗中，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="980f8-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="980f8-196">Azure 會啟動 VM 上架的程序。</span><span class="sxs-lookup"><span data-stu-id="980f8-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="980f8-197">完成時，VM 將會顯示在自動化帳戶的 [DSC 節點]  刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="980f8-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="980f8-198">檢視 DSC 節點的清單</span><span class="sxs-lookup"><span data-stu-id="980f8-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="980f8-199">您可以在 [DSC 節點]  刀鋒視窗中檢視您的自動化帳戶中已上架以供管理的所有機器清單。</span><span class="sxs-lookup"><span data-stu-id="980f8-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="980f8-200">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-201">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-202">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 節點]。</span><span class="sxs-lookup"><span data-stu-id="980f8-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="980f8-203">檢視 DSC 節點的報告</span><span class="sxs-lookup"><span data-stu-id="980f8-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="980f8-204">每次 Azure 自動化 DSC 在受管理的節點上執行一致性檢查時，此節點會將狀態報告傳回到提取伺服器。</span><span class="sxs-lookup"><span data-stu-id="980f8-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="980f8-205">您可以在該節點的刀鋒視窗上檢視這些報告。</span><span class="sxs-lookup"><span data-stu-id="980f8-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="980f8-206">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-207">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-208">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 節點]。</span><span class="sxs-lookup"><span data-stu-id="980f8-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="980f8-209">在 [報告]  圖格上，按一下清單中的任何報告。</span><span class="sxs-lookup"><span data-stu-id="980f8-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![[報告] 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="980f8-211">在個別報告的刀鋒視窗上，您可以看到相對應一致性檢查的下列狀態資訊︰</span><span class="sxs-lookup"><span data-stu-id="980f8-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="980f8-212">報告狀態 — 節點是否「相容」、設定「失敗」，或節點「不相容」(當節點處於 **applyandmonitor** 模式且機器不在預期狀態時)。</span><span class="sxs-lookup"><span data-stu-id="980f8-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="980f8-213">一致性檢查的開始時間。</span><span class="sxs-lookup"><span data-stu-id="980f8-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="980f8-214">一致性檢查的總執行時間。</span><span class="sxs-lookup"><span data-stu-id="980f8-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="980f8-215">一致性檢查的類型。</span><span class="sxs-lookup"><span data-stu-id="980f8-215">The type of consistency check.</span></span>
* <span data-ttu-id="980f8-216">任何錯誤，包括錯誤碼和錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="980f8-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="980f8-217">設定中使用的任何 DSC 資源，以及每個資源的狀態 (不論節點是否處於該資源的預期狀態) — 您可以按一下每個資源，以取得該資源的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="980f8-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="980f8-218">節點的名稱、IP 位址和組態模式。</span><span class="sxs-lookup"><span data-stu-id="980f8-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="980f8-219">您也可以按一下 [檢視原始報告]  ，查看節點傳送至伺服器的實際資料。</span><span class="sxs-lookup"><span data-stu-id="980f8-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="980f8-220">如需有關使用該資料的詳細資訊，請參閱 [使用 DSC 報告伺服器](https://msdn.microsoft.com/powershell/dsc/reportserver)。</span><span class="sxs-lookup"><span data-stu-id="980f8-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="980f8-221">在節點上架後，可能需要一些時間才可取得第一份報告。</span><span class="sxs-lookup"><span data-stu-id="980f8-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="980f8-222">在節點上架後，您可能必須等待多達 30 分鐘的時間才可取得第一份報告。</span><span class="sxs-lookup"><span data-stu-id="980f8-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="980f8-223">將節點重新指派至不同的節點組態</span><span class="sxs-lookup"><span data-stu-id="980f8-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="980f8-224">您可以指派節點以使用不同於您最初指派的節點組態。</span><span class="sxs-lookup"><span data-stu-id="980f8-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="980f8-225">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-226">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-227">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 節點]。</span><span class="sxs-lookup"><span data-stu-id="980f8-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="980f8-228">在 [DSC 節點]  刀鋒視窗上，按一下您要重新指派的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="980f8-229">在該節點的刀鋒視窗上，按一下 [指派節點] 。</span><span class="sxs-lookup"><span data-stu-id="980f8-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![醒目提示 [指派節點] 按鈕之 [節點] 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="980f8-231">在 [指派節點設定] 刀鋒視窗上，選取您要指派節點的節點設定，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="980f8-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![[指派節點組態] 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="980f8-233">取消註冊節點</span><span class="sxs-lookup"><span data-stu-id="980f8-233">Unregistering a node</span></span>
<span data-ttu-id="980f8-234">如果您不想再由 Azure 自動化 DSC 管理節點，您可以將該節點取消註冊。</span><span class="sxs-lookup"><span data-stu-id="980f8-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="980f8-235">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="980f8-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="980f8-236">在 [中樞] 功能表上，依序按一下 [所有資源]  和您的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="980f8-237">在 [自動化帳戶] 刀鋒視窗上，按一下 [DSC 節點]。</span><span class="sxs-lookup"><span data-stu-id="980f8-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="980f8-238">在 [DSC 節點]  刀鋒視窗上，按一下您要取消註冊的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="980f8-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="980f8-239">在該節點的刀鋒視窗上，按一下 [取消註冊] 。</span><span class="sxs-lookup"><span data-stu-id="980f8-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![醒目提示 [取消註冊] 按鈕之 [節點] 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="980f8-241">相關文章</span><span class="sxs-lookup"><span data-stu-id="980f8-241">Related Articles</span></span>
* [<span data-ttu-id="980f8-242">Azure 自動化 DSC 概觀</span><span class="sxs-lookup"><span data-stu-id="980f8-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="980f8-243">上架由 Azure 自動化 DSC 管理的機器</span><span class="sxs-lookup"><span data-stu-id="980f8-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="980f8-244">Windows PowerShell 預期狀態設定概觀</span><span class="sxs-lookup"><span data-stu-id="980f8-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="980f8-245">Azure 自動化 DSC Cmdlet</span><span class="sxs-lookup"><span data-stu-id="980f8-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="980f8-246">Azure 自動化 DSC 價格</span><span class="sxs-lookup"><span data-stu-id="980f8-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

