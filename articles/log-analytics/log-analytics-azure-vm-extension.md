---
title: "aaaConnect Azure 虛擬機器 tooLog 分析 |Microsoft 文件"
description: "適用於 Windows 和 Linux 虛擬機器，在 Azure 中執行，hello 建議使用收集的記錄檔的方式並度量資訊是透過安裝 hello 記錄分析 Azure VM 擴充功能。 您可以使用 hello Azure 入口網站或 PowerShell tooinstall hello 記錄分析到 Azure Vm 上的虛擬機器擴充功能。"
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="2d934-104">記錄分析代理程式連接 Azure 虛擬機器 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="2d934-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="2d934-105">針對 Windows 和 Linux 電腦，hello 建議使用的方法來收集記錄檔和度量資訊是透過安裝 hello 記錄分析代理程式。</span><span class="sxs-lookup"><span data-stu-id="2d934-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="2d934-106">hello 最簡單方式 tooinstall hello 記錄分析代理程式在 Azure 虛擬機器上的都是透過 hello 記錄分析 VM 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="2d934-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="2d934-107">使用 hello 延伸模組可簡化 hello 安裝程序，並會自動設定 hello 代理程式 toosend 資料 toohello 記錄分析工作區，您所指定。</span><span class="sxs-lookup"><span data-stu-id="2d934-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="2d934-108">hello 代理程式就也會自動升級，確保您擁有 hello 最新功能和修正程式。</span><span class="sxs-lookup"><span data-stu-id="2d934-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="2d934-109">您可以為 Windows 虛擬機器，啟用 hello *Microsoft Monitoring Agent*虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="2d934-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="2d934-110">針對 Linux 虛擬機器，您可以啟用 hello *OMS Agent For Linux*虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="2d934-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="2d934-111">深入了解[Azure 虛擬機器擴充功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和 hello [Linux 代理程式](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2d934-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2d934-112">當您使用代理程式型集合的記錄資料時，您必須設定[記錄分析中的資料來源](log-analytics-data-sources.md)toospecify hello 記錄檔和度量的 toocollect。</span><span class="sxs-lookup"><span data-stu-id="2d934-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d934-113">如果您設定記錄分析 tooindex 記錄資料使用[Azure 診斷](log-analytics-azure-storage.md)，和您設定 hello 代理程式 toocollect hello 相同記錄檔時，則 hello 記錄檔會收集兩次。</span><span class="sxs-lookup"><span data-stu-id="2d934-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="2d934-114">您需支付這兩個資料來源的費用。</span><span class="sxs-lookup"><span data-stu-id="2d934-114">You are charged for both data sources.</span></span> <span data-ttu-id="2d934-115">如果您已安裝的 hello 代理程式，然後使用僅 hello 代理程式收集記錄資料-未設定來自 Azure 診斷的記錄分析 toocollect 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="2d934-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="2d934-116">有三個簡單的方法 tooenable hello 記錄分析虛擬機器擴充功能：</span><span class="sxs-lookup"><span data-stu-id="2d934-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="2d934-117">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2d934-117">By using hello Azure portal</span></span>
* <span data-ttu-id="2d934-118">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d934-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="2d934-119">透過使用 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="2d934-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="2d934-120">啟用 hello Azure 入口網站中的 hello VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="2d934-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="2d934-121">您可以記錄分析的 hello 代理程式安裝並連接 hello Azure 虛擬機器上執行使用 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2d934-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="2d934-122">tooinstall hello 記錄分析代理程式，並連接 hello 虛擬機器 tooa 記錄分析工作區</span><span class="sxs-lookup"><span data-stu-id="2d934-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="2d934-123">登入 hello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2d934-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="2d934-124">選取**瀏覽**上 hello 的左方 hello 入口網站，然後再移過**記錄分析 (OMS)**並加以選取。</span><span class="sxs-lookup"><span data-stu-id="2d934-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="2d934-125">在清單中的記錄分析工作區，選取 hello 其中一個要 toouse 以 hello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="2d934-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![OMS 工作區](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="2d934-127">在 [Log Analytics 管理] 下方，選取 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="2d934-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="2d934-128">![虛擬機器](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="2d934-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="2d934-129">中的 hello 清單**虛擬機器**，選取 hello 想 tooinstall hello 代理程式的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2d934-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="2d934-130">hello **OMS 連接狀態**hello VM 指出它是**未連接**。</span><span class="sxs-lookup"><span data-stu-id="2d934-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="2d934-131">![VM 未連接](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="2d934-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="2d934-132">在您的虛擬機器的 hello 詳細資料，選取**連接**。</span><span class="sxs-lookup"><span data-stu-id="2d934-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="2d934-133">hello 代理程式會自動安裝並設定為記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="2d934-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="2d934-134">這個程序需要幾分鐘的時間，在這段期間是 hello OMS 連接狀態*連接...*</span><span class="sxs-lookup"><span data-stu-id="2d934-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="2d934-135">![連接 VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="2d934-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="2d934-136">您安裝並連接 hello 代理程式之後，hello **OMS 連線**狀態會更新的 tooshow**這個工作區**。</span><span class="sxs-lookup"><span data-stu-id="2d934-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="2d934-137">![已連接](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="2d934-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="2d934-138">啟用使用 PowerShell 的 hello VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="2d934-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="2d934-139">當您使用 PowerShell 來設定您的虛擬機器時，您需要 tooprovide hello**工作區識別碼**和**workspaceKey**。</span><span class="sxs-lookup"><span data-stu-id="2d934-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="2d934-140">json 組態中的 hello 屬性名稱都是**區分大小寫**。</span><span class="sxs-lookup"><span data-stu-id="2d934-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="2d934-141">您可以找到 hello 識別碼和索引鍵上 hello**設定**頁面上，hello OMS 入口網站，或使用 PowerShell hello 前面範例所示。</span><span class="sxs-lookup"><span data-stu-id="2d934-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![工作區識別碼及主要金鑰](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="2d934-143">Azure 傳統虛擬機器和 Resource Manager 虛擬機器各使用不同的命令。</span><span class="sxs-lookup"><span data-stu-id="2d934-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="2d934-144">以下是傳統和 Resource Manager 虛擬機器的範例。</span><span class="sxs-lookup"><span data-stu-id="2d934-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="2d934-145">傳統的虛擬機器，請使用下列 PowerShell 範例 hello:</span><span class="sxs-lookup"><span data-stu-id="2d934-145">For classic virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="2d934-146">使用下列 CLI hello 的資源管理員 Linux Vm 的</span><span class="sxs-lookup"><span data-stu-id="2d934-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="2d934-147">資源管理員虛擬機器，請使用下列 PowerShell 範例 hello:</span><span class="sxs-lookup"><span data-stu-id="2d934-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="2d934-148">使用範本的 hello VM 延伸模組部署</span><span class="sxs-lookup"><span data-stu-id="2d934-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="2d934-149">使用 Azure Resource Manager，您可以建立定義 hello 部署和設定您的應用程式的範本 （以 JSON 格式）。</span><span class="sxs-lookup"><span data-stu-id="2d934-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="2d934-150">此範本稱為資源管理員範本，並提供宣告式方式 toodefine 部署。</span><span class="sxs-lookup"><span data-stu-id="2d934-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="2d934-151">藉由使用範本，您可以重複將整個 hello 應用程式生命週期的應用程式部署，並有信心，您部署資源時處於一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="2d934-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="2d934-152">藉由加入 hello 記錄分析代理程式做為 Resource Manager 範本的一部分，您可以確保每個虛擬機器已預先設定的 tooreport tooyour 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="2d934-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="2d934-153">如需 Resource Manager 範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="2d934-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="2d934-154">下列是用來部署虛擬機器執行 Windows hello 安裝 Microsoft Monitoring Agent 擴充功能與資源管理員範本的範例。</span><span class="sxs-lookup"><span data-stu-id="2d934-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="2d934-155">此範本是典型的虛擬機器範本，以下列新增項目 hello:</span><span class="sxs-lookup"><span data-stu-id="2d934-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="2d934-156">workspaceId 和 workspaceName 參數</span><span class="sxs-lookup"><span data-stu-id="2d934-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="2d934-157">Microsoft.EnterpriseCloud.Monitoring 資源擴充功能區段</span><span class="sxs-lookup"><span data-stu-id="2d934-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="2d934-158">輸出 toolook hello 工作區識別碼和 workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="2d934-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

<span data-ttu-id="2d934-159">您可以使用下列 PowerShell 命令的 hello 部署範本：</span><span class="sxs-lookup"><span data-stu-id="2d934-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="2d934-160">疑難排解 hello 記錄分析 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="2d934-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="2d934-161">當系統無法運作時，您通常會收到一則訊息 (從 Azure 入口網站或 Azure Powershell)。</span><span class="sxs-lookup"><span data-stu-id="2d934-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="2d934-162">登入 hello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2d934-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="2d934-163">尋找 hello VM 並開啟 VM 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2d934-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="2d934-164">按一下**延伸**toocheck 如果已啟用 OMS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="2d934-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![VM 擴充功能檢視](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="2d934-166">按一下 hello *MicrosoftMonitoringAgent*(Windows) 或*OmsAgentForLinux*(Linux) 延伸模組並檢視詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2d934-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![VM 擴充功能詳細資料](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="2d934-168">針對 Windows 虛擬機器進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="2d934-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="2d934-169">如果 hello *Microsoft Monitoring Agent*不安裝 VM 代理程式延伸模組或 reporting，您可以執行下列步驟 tootroubleshoot hello 問題 hello。</span><span class="sxs-lookup"><span data-stu-id="2d934-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="2d934-170">檢查是否安裝 hello Azure VM 代理程式，並正確地利用 hello 工作中的步驟[KB 2965986](https://support.microsoft.com/kb/2965986#mt1)。</span><span class="sxs-lookup"><span data-stu-id="2d934-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="2d934-171">您也可以檢閱 hello VM 代理程式記錄檔`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="2d934-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="2d934-172">Hello 記錄不存在，如果未安裝 hello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="2d934-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="2d934-173">在傳統的 Vm 上安裝 hello Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="2d934-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="2d934-174">確認 hello Microsoft Monitoring Agent 擴充功能的活動訊號工作正在執行使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2d934-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="2d934-175">登入 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2d934-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="2d934-176">開啟 工作排程器，並尋找 hello`update_azureoperationalinsight_agent_heartbeat`工作</span><span class="sxs-lookup"><span data-stu-id="2d934-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="2d934-177">確認 hello 工作已啟用，而且正在執行每一分鐘</span><span class="sxs-lookup"><span data-stu-id="2d934-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="2d934-178">檢查 hello 活動訊號記錄檔`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="2d934-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="2d934-179">檢閱 hello Microsoft 監視代理程式 VM 擴充功能中的記錄檔`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="2d934-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="2d934-180">確保 hello 虛擬機器可以執行 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="2d934-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="2d934-181">確定 C:\Windows\temp 的權限未變更</span><span class="sxs-lookup"><span data-stu-id="2d934-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="2d934-182">輸入下列命令，在提升權限的 PowerShell 視窗 hello 虛擬機器上的 hello 檢視 hello hello Microsoft Monitoring Agent 狀態`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="2d934-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="2d934-183">檢閱 hello Microsoft Monitoring Agent 安裝程式記錄檔中`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="2d934-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="2d934-184">如需詳細資訊，請參閱[針對 Windows 擴充功能進行疑難排解](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2d934-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="2d934-185">針對 Linux 虛擬機器進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="2d934-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="2d934-186">如果 hello *OMS Agent for Linux*不安裝 VM 代理程式延伸模組或 reporting，您可以執行下列步驟 tootroubleshoot hello 問題 hello。</span><span class="sxs-lookup"><span data-stu-id="2d934-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="2d934-187">如果 hello 擴充狀態是*未知*檢查 hello Azure VM 代理程式是否已安裝並正常運作，藉由檢閱 hello VM 代理程式記錄檔`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="2d934-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="2d934-188">Hello 記錄不存在，如果未安裝 hello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="2d934-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="2d934-189">在 Linux Vm 上安裝 hello Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="2d934-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="2d934-190">檢閱 hello OMS Agent for Linux VM 擴充功能的其他的狀況不良狀態，記錄檔`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log`和`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="2d934-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="2d934-191">如果 hello 延伸狀態為狀況良好，但不上載資料檢閱 hello OMS Agent for Linux 記錄檔`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="2d934-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d934-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d934-192">Next steps</span></span>
* <span data-ttu-id="2d934-193">設定[記錄分析中的資料來源](log-analytics-data-sources.md)toospecify hello 記錄檔和度量 toocollect。</span><span class="sxs-lookup"><span data-stu-id="2d934-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="2d934-194">虛擬機器的 toogather 資料[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="2d934-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="2d934-195">針對 Azure 中執行的其他資源，[使用 Azure 診斷收集資料](log-analytics-azure-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="2d934-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="2d934-196">對於不在 Azure 中的電腦，您可以使用 hello 方法 hello 下列文章中所述安裝 hello 記錄分析代理程式：</span><span class="sxs-lookup"><span data-stu-id="2d934-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="2d934-197">連接 Windows 電腦 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="2d934-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="2d934-198">連線 Linux 電腦 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="2d934-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
