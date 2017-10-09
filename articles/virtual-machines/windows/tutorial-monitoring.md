---
title: "aaaAzure 監視和 Windows 虛擬機器 |Microsoft 文件"
description: "教學課程 - 使用 Azure PowerShell 監視 Windows 虛擬機器"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="2977b-103">使用 Azure PowerShell 監視 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2977b-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="2977b-104">Azure 監視會使用代理程式 toocollect 開機和 Azure Vm 的效能資料，將此資料儲存在 Azure 儲存體，讓它可以透過入口網站、 hello Azure PowerShell 模組，以及 hello Azure CLI 存取。</span><span class="sxs-lookup"><span data-stu-id="2977b-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="2977b-105">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="2977b-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2977b-106">啟用 VM 上的開機診斷</span><span class="sxs-lookup"><span data-stu-id="2977b-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="2977b-107">檢視開機診斷</span><span class="sxs-lookup"><span data-stu-id="2977b-107">View boot diagnostics</span></span>
> * <span data-ttu-id="2977b-108">檢視 VM 主機計量</span><span class="sxs-lookup"><span data-stu-id="2977b-108">View VM host metrics</span></span>
> * <span data-ttu-id="2977b-109">安裝 hello 診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="2977b-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="2977b-110">檢視 VM 計量</span><span class="sxs-lookup"><span data-stu-id="2977b-110">View VM metrics</span></span>
> * <span data-ttu-id="2977b-111">建立警示</span><span class="sxs-lookup"><span data-stu-id="2977b-111">Create an alert</span></span>
> * <span data-ttu-id="2977b-112">設定進階監視</span><span class="sxs-lookup"><span data-stu-id="2977b-112">Set up advanced monitoring</span></span>

<span data-ttu-id="2977b-113">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2977b-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2977b-114">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="2977b-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="2977b-115">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="2977b-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="2977b-116">在本教學課程 toocomplete hello 範例中的，您必須擁有現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2977b-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="2977b-117">如有需要，這個[指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)可以為您建立一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2977b-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="2977b-118">當使用 hello 教學課程時，取代 hello 資源群組、 VM 名稱和位置在需要時。</span><span class="sxs-lookup"><span data-stu-id="2977b-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="2977b-119">檢視開機診斷</span><span class="sxs-lookup"><span data-stu-id="2977b-119">View boot diagnostics</span></span>

<span data-ttu-id="2977b-120">為 Windows 虛擬機器開機，hello 開機診斷代理程式會擷取可用於疑難排解用途的螢幕輸出。</span><span class="sxs-lookup"><span data-stu-id="2977b-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="2977b-121">此功能預設為啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="2977b-121">This capability is enabled by default.</span></span> <span data-ttu-id="2977b-122">hello 擷取的螢幕擷取畫面會儲存在 Azure 儲存體帳戶，也會建立預設。</span><span class="sxs-lookup"><span data-stu-id="2977b-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="2977b-123">您可以取得 hello 開機診斷資料以 hello [Get AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata)命令。</span><span class="sxs-lookup"><span data-stu-id="2977b-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="2977b-124">在下列範例的 hello，開機診斷是下載的 toohello 根的 hello * c:\*磁碟機。</span><span class="sxs-lookup"><span data-stu-id="2977b-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="2977b-125">檢視主機計量</span><span class="sxs-lookup"><span data-stu-id="2977b-125">View host metrics</span></span>

<span data-ttu-id="2977b-126">在 Azure 中有 Windows VM 專用的主機 VM 與它互動。</span><span class="sxs-lookup"><span data-stu-id="2977b-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="2977b-127">度量自動和收集到的 hello 主機可以在 hello Azure 入口網站中檢視。</span><span class="sxs-lookup"><span data-stu-id="2977b-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="2977b-128">在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。</span><span class="sxs-lookup"><span data-stu-id="2977b-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="2977b-129">按一下**度量**在 hello VM 刀鋒視窗中，，然後選取任何下 hello 主機計量**可用的度量**toosee hello 主機 VM 執行的方式。</span><span class="sxs-lookup"><span data-stu-id="2977b-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![檢視主機計量](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="2977b-131">安裝診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="2977b-131">Install diagnostics extension</span></span>

<span data-ttu-id="2977b-132">hello 基本主機計量可供使用，但更細微的 toosee 和特定 VM 的度量，您 tooneed tooinstall hello Azure 診斷擴充功能在 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="2977b-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="2977b-133">hello Azure 診斷擴充功能可讓其他監視和診斷資料 toobe hello VM 從擷取。</span><span class="sxs-lookup"><span data-stu-id="2977b-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="2977b-134">您可以檢視這些效能度量，並依據 hello VM 執行的方式建立警示。</span><span class="sxs-lookup"><span data-stu-id="2977b-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="2977b-135">hello 診斷延伸模組會安裝透過 hello Azure 入口網站，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2977b-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="2977b-136">在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。</span><span class="sxs-lookup"><span data-stu-id="2977b-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="2977b-137">按一下 [診斷設定]。</span><span class="sxs-lookup"><span data-stu-id="2977b-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="2977b-138">hello 清單顯示*開機診斷*已經啟用 hello 前一節。</span><span class="sxs-lookup"><span data-stu-id="2977b-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="2977b-139">按一下核取方塊 hello*基本度量*。</span><span class="sxs-lookup"><span data-stu-id="2977b-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="2977b-140">按一下 hello**啟用客體層級監視** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2977b-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![檢視診斷計量](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="2977b-142">檢視 VM 計量</span><span class="sxs-lookup"><span data-stu-id="2977b-142">View VM metrics</span></span>

<span data-ttu-id="2977b-143">您可以在 hello 檢視 hello VM 度量您檢視 hello 主機 VM 計量的相同方式：</span><span class="sxs-lookup"><span data-stu-id="2977b-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="2977b-144">在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。</span><span class="sxs-lookup"><span data-stu-id="2977b-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="2977b-145">toosee 如何 hello VM 正在執行中，按一下**度量**hello VM 刀鋒視窗中，且然後選取其中一個下 hello 診斷度量**可用的度量**。</span><span class="sxs-lookup"><span data-stu-id="2977b-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![檢視 VM 計量](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="2977b-147">建立警示</span><span class="sxs-lookup"><span data-stu-id="2977b-147">Create alerts</span></span>

<span data-ttu-id="2977b-148">您可以根據特定效能計量來建立警示。</span><span class="sxs-lookup"><span data-stu-id="2977b-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="2977b-149">警示可能會使用的 toonotify 時的平均 CPU 使用率超過某個臨界值或可用的磁碟空間低於特定大小，例如。</span><span class="sxs-lookup"><span data-stu-id="2977b-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="2977b-150">警示會顯示在 hello Azure 入口網站，或可以透過電子郵件傳送。</span><span class="sxs-lookup"><span data-stu-id="2977b-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="2977b-151">您也可以在所產生的回應 tooalerts 觸發 Azure 自動化 runbook 或 Azure 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2977b-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="2977b-152">hello 下列範例會建立警示的平均 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="2977b-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="2977b-153">在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。</span><span class="sxs-lookup"><span data-stu-id="2977b-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="2977b-154">按一下**警示規則**hello VM 刀鋒視窗，然後按一下**新增度量的警示**hello 的 hello 警示 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="2977b-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="2977b-155">提供警示的 [名稱]，例如 myAlertRule。</span><span class="sxs-lookup"><span data-stu-id="2977b-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="2977b-156">tootrigger 警示時的 CPU 百分比超過五分鐘，1.0 會保留所有 hello 選取其他預設值。</span><span class="sxs-lookup"><span data-stu-id="2977b-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="2977b-157">（選擇性） 核取方塊 hello*電子郵件擁有者、 參與者與讀者*toosend 電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="2977b-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="2977b-158">hello 預設動作是 toopresent hello 入口網站中的通知。</span><span class="sxs-lookup"><span data-stu-id="2977b-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="2977b-159">按一下 hello**確定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2977b-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="2977b-160">進階監視</span><span class="sxs-lookup"><span data-stu-id="2977b-160">Advanced monitoring</span></span> 

<span data-ttu-id="2977b-161">您可以使用 [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) (OMS) 對您的 VM 進行更進階的監視。</span><span class="sxs-lookup"><span data-stu-id="2977b-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="2977b-162">如果您尚未這麼做，可以註冊 Operations Management Suite 的[免費試用版](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)。</span><span class="sxs-lookup"><span data-stu-id="2977b-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="2977b-163">當您擁有存取 toohello OMS 入口網站時，您可以在 hello 設定 刀鋒視窗上找到 hello 工作區的索引鍵和工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="2977b-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="2977b-164">使用 hello[組 AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS 擴充 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="2977b-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="2977b-165">更新 hello 變數中的值如下範例 tooreflect hello 您 OMS 工作區金鑰和工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="2977b-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

<span data-ttu-id="2977b-166">您應該在幾分鐘之後, 會看到 hello hello OMS 工作區中的新 VM。</span><span class="sxs-lookup"><span data-stu-id="2977b-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![OMS 刀鋒視窗](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="2977b-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2977b-168">Next steps</span></span>
<span data-ttu-id="2977b-169">在本教學課程中，您利用 Azure 資訊安全中心設定並檢閱 VM。</span><span class="sxs-lookup"><span data-stu-id="2977b-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="2977b-170">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="2977b-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2977b-171">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="2977b-171">Create a virtual network</span></span>
> * <span data-ttu-id="2977b-172">建立資源群組和 VM</span><span class="sxs-lookup"><span data-stu-id="2977b-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="2977b-173">啟用 hello VM 上的開機診斷功能</span><span class="sxs-lookup"><span data-stu-id="2977b-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="2977b-174">檢視開機診斷</span><span class="sxs-lookup"><span data-stu-id="2977b-174">View boot diagnostics</span></span>
> * <span data-ttu-id="2977b-175">檢視主機計量</span><span class="sxs-lookup"><span data-stu-id="2977b-175">View host metrics</span></span>
> * <span data-ttu-id="2977b-176">安裝 hello 診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="2977b-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="2977b-177">檢視 VM 計量</span><span class="sxs-lookup"><span data-stu-id="2977b-177">View VM metrics</span></span>
> * <span data-ttu-id="2977b-178">建立警示</span><span class="sxs-lookup"><span data-stu-id="2977b-178">Create an alert</span></span>
> * <span data-ttu-id="2977b-179">設定進階監視</span><span class="sxs-lookup"><span data-stu-id="2977b-179">Set up advanced monitoring</span></span>

<span data-ttu-id="2977b-180">前進 toohello 下一個教學課程的 toolearn 有關 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="2977b-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2977b-181">管理 VM 安全性</span><span class="sxs-lookup"><span data-stu-id="2977b-181">Manage VM security</span></span>](./tutorial-azure-security.md)