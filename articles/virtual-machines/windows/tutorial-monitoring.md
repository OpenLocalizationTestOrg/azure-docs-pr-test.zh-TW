---
title: "Azure 監視器和 Windows 虛擬機器 | Microsoft Docs"
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
ms.openlocfilehash: 42a475092bdd615c23154e5f813861b0acefcf29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="db732-103">使用 Azure PowerShell 監視 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="db732-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="db732-104">Azure 監視器使用代理程式從 Azure VM 收集開機和效能資料，將此資料儲存在 Azure 儲存體，並讓資料可透過入口網站、Azure PowerShell 模組和 Azure CLI 存取。</span><span class="sxs-lookup"><span data-stu-id="db732-104">Azure monitoring uses agents to collect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, the Azure PowerShell module, and the Azure CLI.</span></span> <span data-ttu-id="db732-105">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="db732-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db732-106">啟用 VM 上的開機診斷</span><span class="sxs-lookup"><span data-stu-id="db732-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="db732-107">檢視開機診斷</span><span class="sxs-lookup"><span data-stu-id="db732-107">View boot diagnostics</span></span>
> * <span data-ttu-id="db732-108">檢視 VM 主機計量</span><span class="sxs-lookup"><span data-stu-id="db732-108">View VM host metrics</span></span>
> * <span data-ttu-id="db732-109">安裝診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="db732-109">Install the diagnostics extension</span></span>
> * <span data-ttu-id="db732-110">檢視 VM 計量</span><span class="sxs-lookup"><span data-stu-id="db732-110">View VM metrics</span></span>
> * <span data-ttu-id="db732-111">建立警示</span><span class="sxs-lookup"><span data-stu-id="db732-111">Create an alert</span></span>
> * <span data-ttu-id="db732-112">設定進階監視</span><span class="sxs-lookup"><span data-stu-id="db732-112">Set up advanced monitoring</span></span>

<span data-ttu-id="db732-113">本教學課程需要 Azure PowerShell 模組 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="db732-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="db732-114">執行 ` Get-Module -ListAvailable AzureRM` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="db732-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="db732-115">如果您需要升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="db732-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="db732-116">若要完成本教學課程中的範例，您目前必須具有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="db732-116">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="db732-117">如有需要，這個[指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)可以為您建立一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="db732-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="db732-118">逐步完成教學課程之後，請視需要取代資源群組、VM 名稱、位置。</span><span class="sxs-lookup"><span data-stu-id="db732-118">When working through the tutorial, replace the resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="db732-119">檢視開機診斷</span><span class="sxs-lookup"><span data-stu-id="db732-119">View boot diagnostics</span></span>

<span data-ttu-id="db732-120">Windows 虛擬機器開機時，開機診斷代理程式會擷取可用於疑難排解的螢幕輸出。</span><span class="sxs-lookup"><span data-stu-id="db732-120">As Windows virtual machines boot up, the boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="db732-121">此功能預設為啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="db732-121">This capability is enabled by default.</span></span> <span data-ttu-id="db732-122">擷取的螢幕畫面會儲存在 Azure 儲存體帳戶，這也是預設會建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="db732-122">The captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="db732-123">您可以使用 [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) 命令取得開機診斷資料。</span><span class="sxs-lookup"><span data-stu-id="db732-123">You can get the boot diagnostic data with the [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="db732-124">在下列範例中，開機診斷會下載到 *c:\* 磁碟機的根目錄。</span><span class="sxs-lookup"><span data-stu-id="db732-124">In the following example, boot diagnostics are downloaded to the root of the *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="db732-125">檢視主機計量</span><span class="sxs-lookup"><span data-stu-id="db732-125">View host metrics</span></span>

<span data-ttu-id="db732-126">在 Azure 中有 Windows VM 專用的主機 VM 與它互動。</span><span class="sxs-lookup"><span data-stu-id="db732-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="db732-127">系統會自動收集主機的計量，而且可以在 Azure 入口網站中檢視這些計量。</span><span class="sxs-lookup"><span data-stu-id="db732-127">Metrics are automatically collected for the Host and can be viewed in the Azure portal.</span></span>

1. <span data-ttu-id="db732-128">在 Azure 入口網站中，按一下 [資源群組]，選取 [myResourceGroup]，然後選取資源清單中的 [myVM]。</span><span class="sxs-lookup"><span data-stu-id="db732-128">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="db732-129">按一下 VM 刀鋒視窗上的 [計量]，然後選取 [可用的計量] 下的任何 [主機] 計量以查看主機 VM 的執行狀況。</span><span class="sxs-lookup"><span data-stu-id="db732-129">Click **Metrics** on the VM blade, and then select any of the Host metrics under **Available metrics** to see how the Host VM is performing.</span></span>

    ![檢視主機計量](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="db732-131">安裝診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="db732-131">Install diagnostics extension</span></span>

<span data-ttu-id="db732-132">系統提供基本的主機計量，但若要查看更細微或 VM 特定的計量，則需要在 VM 上安裝 Azure 診斷的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="db732-132">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="db732-133">Azure 診斷擴充功能可額外提供從 VM 擷取的監視和診斷資料。</span><span class="sxs-lookup"><span data-stu-id="db732-133">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="db732-134">您可以檢視這些效能計量，並依據 VM 的執行狀況建立警示。</span><span class="sxs-lookup"><span data-stu-id="db732-134">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="db732-135">診斷擴充功能可透過 Azure 入口網站安裝，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="db732-135">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="db732-136">在 Azure 入口網站中，按一下 [資源群組]，選取 [myResourceGroup]，然後選取資源清單中的 [myVM]。</span><span class="sxs-lookup"><span data-stu-id="db732-136">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="db732-137">按一下 [診斷設定]。</span><span class="sxs-lookup"><span data-stu-id="db732-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="db732-138">清單會顯示在上一節已啟用開機診斷。</span><span class="sxs-lookup"><span data-stu-id="db732-138">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="db732-139">按一下 [基本計量] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="db732-139">Click the check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="db732-140">按一下 [啟用來賓層級監視] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="db732-140">Click the **Enable guest-level monitoring** button.</span></span>

    ![檢視診斷計量](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="db732-142">檢視 VM 計量</span><span class="sxs-lookup"><span data-stu-id="db732-142">View VM metrics</span></span>

<span data-ttu-id="db732-143">您可以檢視 VM 計量，和您檢視主機 VM 計量資訊的方式相同︰</span><span class="sxs-lookup"><span data-stu-id="db732-143">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="db732-144">在 Azure 入口網站中，按一下 [資源群組]，選取 [myResourceGroup]，然後選取資源清單中的 [myVM]。</span><span class="sxs-lookup"><span data-stu-id="db732-144">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="db732-145">若要查看 VM 的執行狀況，按一下 VM 刀鋒視窗上的 [計量]，然後選取 [可用的計量] 下的任何診斷計量。</span><span class="sxs-lookup"><span data-stu-id="db732-145">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![檢視 VM 計量](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="db732-147">建立警示</span><span class="sxs-lookup"><span data-stu-id="db732-147">Create alerts</span></span>

<span data-ttu-id="db732-148">您可以根據特定效能計量來建立警示。</span><span class="sxs-lookup"><span data-stu-id="db732-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="db732-149">舉例來說，可使用警示來通知您平均 CPU 使用量超過特定臨界值、或是可用磁碟空間降到低於某個量。</span><span class="sxs-lookup"><span data-stu-id="db732-149">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="db732-150">警示會顯示在 Azure 入口網站，或是可以透過電子郵件傳送。</span><span class="sxs-lookup"><span data-stu-id="db732-150">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="db732-151">您也可以觸發 Azure 自動化 Runbook 或 Azure Logic Apps 以回應產生的警示。</span><span class="sxs-lookup"><span data-stu-id="db732-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="db732-152">以下範例會建立平均 CPU 使用量的警示。</span><span class="sxs-lookup"><span data-stu-id="db732-152">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="db732-153">在 Azure 入口網站中，按一下 [資源群組]，選取 [myResourceGroup]，然後選取資源清單中的 [myVM]。</span><span class="sxs-lookup"><span data-stu-id="db732-153">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="db732-154">按一下VM 刀鋒視窗中的 [警示規則]，按一下橫跨在警示刀鋒視窗上方的 [新增計量警示]。</span><span class="sxs-lookup"><span data-stu-id="db732-154">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="db732-155">提供警示的 [名稱]，例如 myAlertRule。</span><span class="sxs-lookup"><span data-stu-id="db732-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="db732-156">若要在 CPU 百分比連續五分鐘超過 1.0 時觸發警示，保留所有其他已選取的預設值。</span><span class="sxs-lookup"><span data-stu-id="db732-156">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="db732-157">(選擇性) 選取 [電子郵件的擁有者、參與者及讀者] 核取方塊以傳送電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="db732-157">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="db732-158">預設動作是在入口網站中顯示通知。</span><span class="sxs-lookup"><span data-stu-id="db732-158">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="db732-159">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="db732-159">Click the **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="db732-160">進階監視</span><span class="sxs-lookup"><span data-stu-id="db732-160">Advanced monitoring</span></span> 

<span data-ttu-id="db732-161">您可以使用 [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) (OMS) 對您的 VM 進行更進階的監視。</span><span class="sxs-lookup"><span data-stu-id="db732-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="db732-162">如果您尚未這麼做，可以註冊 Operations Management Suite 的[免費試用版](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)。</span><span class="sxs-lookup"><span data-stu-id="db732-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="db732-163">當您可以存取 OMS 入口網站時，可以在 [設定] 刀鋒視窗中找到工作區金鑰和工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="db732-163">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="db732-164">使用 [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) 命令將 OMS 擴充功能新增到 VM。</span><span class="sxs-lookup"><span data-stu-id="db732-164">Use the [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand to to add the OMS extension to the VM.</span></span> <span data-ttu-id="db732-165">更新以下範例中的變數值，以反映您的 OMS 工作區金鑰和工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="db732-165">Update the variable values in the below sample to reflect you OMS workspace key and workspace Id.</span></span>  

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

<span data-ttu-id="db732-166">幾分鐘後，您應該會在 OMS 工作區中看到新的 VM。</span><span class="sxs-lookup"><span data-stu-id="db732-166">After a few minutes, you should see the new VM in the OMS workspace.</span></span> 

![OMS 刀鋒視窗](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="db732-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db732-168">Next steps</span></span>
<span data-ttu-id="db732-169">在本教學課程中，您利用 Azure 資訊安全中心設定並檢閱 VM。</span><span class="sxs-lookup"><span data-stu-id="db732-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="db732-170">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="db732-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db732-171">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="db732-171">Create a virtual network</span></span>
> * <span data-ttu-id="db732-172">建立資源群組和 VM</span><span class="sxs-lookup"><span data-stu-id="db732-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="db732-173">啟用 VM 上的開機診斷</span><span class="sxs-lookup"><span data-stu-id="db732-173">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="db732-174">檢視開機診斷</span><span class="sxs-lookup"><span data-stu-id="db732-174">View boot diagnostics</span></span>
> * <span data-ttu-id="db732-175">檢視主機計量</span><span class="sxs-lookup"><span data-stu-id="db732-175">View host metrics</span></span>
> * <span data-ttu-id="db732-176">安裝診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="db732-176">Install the diagnostics extension</span></span>
> * <span data-ttu-id="db732-177">檢視 VM 計量</span><span class="sxs-lookup"><span data-stu-id="db732-177">View VM metrics</span></span>
> * <span data-ttu-id="db732-178">建立警示</span><span class="sxs-lookup"><span data-stu-id="db732-178">Create an alert</span></span>
> * <span data-ttu-id="db732-179">設定進階監視</span><span class="sxs-lookup"><span data-stu-id="db732-179">Set up advanced monitoring</span></span>

<span data-ttu-id="db732-180">請前進到下一個教學課程，了解 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="db732-180">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db732-181">管理 VM 安全性</span><span class="sxs-lookup"><span data-stu-id="db732-181">Manage VM security</span></span>](./tutorial-azure-security.md)