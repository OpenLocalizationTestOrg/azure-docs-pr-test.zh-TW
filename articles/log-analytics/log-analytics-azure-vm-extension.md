---
title: "將 Azure 虛擬機器連接到 Log Analytics | Microsoft Docs"
description: "針對在 Azure 中執行的 Windows 和 Linux 虛擬機器，收集記錄和計量的建議方法是安裝 Log Analytics Azure VM 擴充功能。 您可以使用 Azure 入口網站或 PowerShell，將 Log Analytics 虛擬機器擴充功能安裝到 Azure VM。"
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
ms.openlocfilehash: cdae291b546fef4d7fdb8b067c8e4f4c9708d43f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="connect-azure-virtual-machines-to-log-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="d4ae9-104">使用 Log Analytics 代理程式將 Azure 虛擬機器連接到 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d4ae9-104">Connect Azure virtual machines to Log Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="d4ae9-105">針對 Windows 和 Linux 電腦，收集記錄和度量的建議方式是安裝 Log Analytics 代理程式。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-105">For Windows and Linux computers, the recommended method for collecting logs and metrics is by installing the Log Analytics agent.</span></span>

<span data-ttu-id="d4ae9-106">在 Azure 虛擬機器上安裝 Log Analytics 代理程式最簡單的方式是透過 Log Analytics VM 擴充。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-106">The easiest way to install the Log Analytics agent on Azure virtual machines is through the Log Analytics VM Extension.</span></span>  <span data-ttu-id="d4ae9-107">使用擴充可以簡化安裝程序，並自動設定代理程式將資料傳送到您指定的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-107">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span></span> <span data-ttu-id="d4ae9-108">代理程式也會自動升級，以確保您擁有最新的功能和修正程式。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-108">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span></span>

<span data-ttu-id="d4ae9-109">對於 Windows 虛擬機器，啟用 *Microsoft Monitoring Agent* 虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-109">For Windows virtual machines, you enable the *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="d4ae9-110">對於 Linux 虛擬機器，啟用 *OMS Agent for Linux* 虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-110">For Linux virtual machines, you enable the *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="d4ae9-111">深入了解 [Azure 虛擬機器擴充功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和 [Linux 代理程式](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and the [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d4ae9-112">如果您使用代理程式來收集記錄資料，則必須設定 [Log Analytics 中的資料來源](log-analytics-data-sources.md)，以指定您要收集的記錄和度量。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics that you want to collect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4ae9-113">如果您已將 Log Analytics 設為使用 [Azure 診斷](log-analytics-azure-storage.md)來編製記錄資料的索引，並設定代理程式來收集相同的記錄，則記錄會收集兩次。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-113">If you configure Log Analytics to index log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure the agent to collect the same logs, then the logs are collected twice.</span></span> <span data-ttu-id="d4ae9-114">您需支付這兩個資料來源的費用。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-114">You are charged for both data sources.</span></span> <span data-ttu-id="d4ae9-115">如果您已安裝代理程式，則請僅使用代理程式來收集記錄資料 - 不要設定 Log Analytics 從 Azure 診斷收集記錄資料。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-115">If you have the agent installed, then collect log data by using only the agent - don't configure Log Analytics to collect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="d4ae9-116">有三個簡單的方法可啟用 Log Analytics 虛擬機器擴充功能︰</span><span class="sxs-lookup"><span data-stu-id="d4ae9-116">There are three easy ways to enable the Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="d4ae9-117">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d4ae9-117">By using the Azure portal</span></span>
* <span data-ttu-id="d4ae9-118">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4ae9-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="d4ae9-119">透過使用 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="d4ae9-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-the-vm-extension-in-the-azure-portal"></a><span data-ttu-id="d4ae9-120">在 Azure 入口網站中啟用 VM 擴充</span><span class="sxs-lookup"><span data-stu-id="d4ae9-120">Enable the VM extension in the Azure portal</span></span>
<span data-ttu-id="d4ae9-121">您可以安裝 Log Analytics 的代理程式，並使用 [Azure 入口網站](https://portal.azure.com)來連接執行該代理程式的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-121">You can install the agent for Log Analytics and connect the Azure virtual machine that it runs on by using the [Azure portal](https://portal.azure.com).</span></span>

### <a name="to-install-the-log-analytics-agent-and-connect-the-virtual-machine-to-a-log-analytics-workspace"></a><span data-ttu-id="d4ae9-122">安裝 Log Analytics 代理程式，並將虛擬機器連接到 Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="d4ae9-122">To install the Log Analytics agent and connect the virtual machine to a Log Analytics workspace</span></span>
1. <span data-ttu-id="d4ae9-123">登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-123">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="d4ae9-124">在入口網站左側選取 [瀏覽]，然後移至 [Log Analytics (OMS)] 並選取它。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-124">Select **Browse** on the left side of the portal, and then go to **Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="d4ae9-125">在您的 Log Analytics 工作區清單中，選取要用於 Azure VM 的工作區。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-125">In your list of Log Analytics workspaces, select the one that you want to use with the Azure VM.</span></span>  
   ![OMS 工作區](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="d4ae9-127">在 [Log Analytics 管理] 下方，選取 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="d4ae9-128">![虛擬機器](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="d4ae9-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="d4ae9-129">在 [虛擬機器] 清單中，選取您要安裝代理程式的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-129">In the list of **Virtual machines**, select the virtual machine on which you want to install the agent.</span></span> <span data-ttu-id="d4ae9-130">VM 的 [OMS 連接狀態] 會指出它是 [未連接] 狀態。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-130">The **OMS connection status** for the VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="d4ae9-131">![VM 未連接](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="d4ae9-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="d4ae9-132">在虛擬機器的詳細資訊中，選取 [連接]。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-132">In the details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="d4ae9-133">隨即會為 Log Analytics 工作區自動安裝和設定代理程式。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-133">The agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="d4ae9-134">這個程序需要幾分鐘的時間，在這段期間 OMS 連線狀態是「連接中...」</span><span class="sxs-lookup"><span data-stu-id="d4ae9-134">This process takes a few minutes, during which time the OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="d4ae9-135">![連接 VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="d4ae9-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="d4ae9-136">安裝並連接代理程式之後，[OMS 連接] 狀態會更新為顯示 [此工作區]。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-136">After you install and connect the agent, the **OMS connection** status will be updated to show **This workspace**.</span></span>  
   <span data-ttu-id="d4ae9-137">![已連接](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="d4ae9-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-the-vm-extension-using-powershell"></a><span data-ttu-id="d4ae9-138">使用 PowerShell 啟用 VM 擴充</span><span class="sxs-lookup"><span data-stu-id="d4ae9-138">Enable the VM extension using PowerShell</span></span>
<span data-ttu-id="d4ae9-139">使用 PowerShell 設定虛擬機器時，您必須提供 **workspaceId** 和 **workspaceKey**。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-139">When you configure your virtual machine by using PowerShell, you need to provide the **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="d4ae9-140">json 組態中的屬性名稱需**區分大小寫**。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-140">The property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="d4ae9-141">您可以在 OMS 入口網站的 [設定] 頁面上，或使用上述範例所示的 PowerShell，找到識別碼及金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-141">You can find the Id and key on the **Settings** page of the OMS portal, or by using PowerShell as shown in the preceding example.</span></span>

![工作區識別碼及主要金鑰](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="d4ae9-143">Azure 傳統虛擬機器和 Resource Manager 虛擬機器各使用不同的命令。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="d4ae9-144">以下是傳統和 Resource Manager 虛擬機器的範例。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="d4ae9-145">若是傳統 Azure 虛擬機器，請使用下列 PowerShell 範例：</span><span class="sxs-lookup"><span data-stu-id="d4ae9-145">For classic virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="d4ae9-146">針對 Resource Manager Linux VM 請使用下列 CLI</span><span class="sxs-lookup"><span data-stu-id="d4ae9-146">For Resource Manager Linux VMs using the following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="d4ae9-147">若是 Resource Manager 虛擬機器，請使用下列 PowerShell 範例：</span><span class="sxs-lookup"><span data-stu-id="d4ae9-147">For Resource Manager virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable to find OMS Workspace $workspaceName. Do you need to run Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-the-vm-extension-using-a-template"></a><span data-ttu-id="d4ae9-148">使用範本部署 VM 擴充</span><span class="sxs-lookup"><span data-stu-id="d4ae9-148">Deploy the VM extension using a template</span></span>
<span data-ttu-id="d4ae9-149">您可以利用 Azure Resource Manager 建立範本 (JSON 格式)，以定義應用程式的部署和設定。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines the deployment and configuration of your application.</span></span> <span data-ttu-id="d4ae9-150">此範本就是所謂的資源管理員範本，並提供定義部署的宣告方式。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-150">This template is known as a Resource Manager template and provides a declarative way to define deployment.</span></span> <span data-ttu-id="d4ae9-151">在整個應用程式生命週期內，您可以使用範本來重複部署應用程式，並確信您的資源會以一致的狀態部署。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-151">By using a template, you can repeatedly deploy your application throughout the app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="d4ae9-152">您可以將 Log Analytics 代理程式納入 Resource Manager 範本中，以確定每個虛擬機器都預先設定為向您的 Log Analytics 工作區報告。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-152">By including the Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured to report to your Log Analytics workspace.</span></span>

<span data-ttu-id="d4ae9-153">如需 Resource Manager 範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d4ae9-154">以下是用來部署虛擬機器的 Resource Manager 範本的範例，此虛擬機器執行 Windows 且已安裝 Microsoft Monitoring Agent 擴充。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with the Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="d4ae9-155">此範例是一個典型的虛擬機器範本，而且還增加下列項目︰</span><span class="sxs-lookup"><span data-stu-id="d4ae9-155">This template is a typical virtual machine template, with the following additions:</span></span>

* <span data-ttu-id="d4ae9-156">workspaceId 和 workspaceName 參數</span><span class="sxs-lookup"><span data-stu-id="d4ae9-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="d4ae9-157">Microsoft.EnterpriseCloud.Monitoring 資源擴充功能區段</span><span class="sxs-lookup"><span data-stu-id="d4ae9-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="d4ae9-158">輸出以查詢 workspaceId 和 workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="d4ae9-158">Outputs to look up the workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for the Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for the Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for the Public IP. Must be lowercase. It should match with the following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
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
        "description": "The Windows version for the VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
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

<span data-ttu-id="d4ae9-159">您可以使用下列 PowerShell 命令來部署範本：</span><span class="sxs-lookup"><span data-stu-id="d4ae9-159">You can deploy a template by using the following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-the-log-analytics-vm-extension"></a><span data-ttu-id="d4ae9-160">針對 Log Analytics VM 擴充功能進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d4ae9-160">Troubleshooting the Log Analytics VM extension</span></span>
<span data-ttu-id="d4ae9-161">當系統無法運作時，您通常會收到一則訊息 (從 Azure 入口網站或 Azure Powershell)。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="d4ae9-162">登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-162">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="d4ae9-163">找出 VM 並開啟 VM 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-163">Find the VM and open VM details.</span></span>
3. <span data-ttu-id="d4ae9-164">按一下 [擴充功能]，檢查是否已啟用 OMS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-164">Click **Extensions** to check if OMS extension is enabled or not.</span></span>

   ![VM 擴充功能檢視](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="d4ae9-166">按一下 [MicrosoftMonitoringAgent] \(Windows) 或 [OmsAgentForLinux] \(Linux) 擴充功能，並檢視詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-166">Click the *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![VM 擴充功能詳細資料](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="d4ae9-168">針對 Windows 虛擬機器進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d4ae9-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="d4ae9-169">如果未安裝或沒有回報 Microsoft Monitoring Agent VM 代理程式擴充功能，您可以執行下列步驟來針對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-169">If the *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="d4ae9-170">使用 [KB 2965986](https://support.microsoft.com/kb/2965986#mt1) 中的步驟，檢查 Azure VM 代理程式是否已安裝且正確運作。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-170">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="d4ae9-171">您也可以檢閱 VM 代理程式記錄檔 `C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="d4ae9-171">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="d4ae9-172">如果記錄檔不存在，則表示未安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-172">If the log does not exist, the VM agent is not installed.</span></span>
     * [<span data-ttu-id="d4ae9-173">在傳統 VM 上安裝 Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="d4ae9-173">Install the Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="d4ae9-174">使用下列步驟，確認 Microsoft Monitoring Agent 擴充活動訊號工作正在執行︰</span><span class="sxs-lookup"><span data-stu-id="d4ae9-174">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span></span>
   * <span data-ttu-id="d4ae9-175">登入虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d4ae9-175">Log in to the virtual machine</span></span>
   * <span data-ttu-id="d4ae9-176">開啟工作排程器，找出 `update_azureoperationalinsight_agent_heartbeat` 工作</span><span class="sxs-lookup"><span data-stu-id="d4ae9-176">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="d4ae9-177">確認此工作已啟用，且每一分鐘執行一次</span><span class="sxs-lookup"><span data-stu-id="d4ae9-177">Confirm the task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="d4ae9-178">檢查 `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log` 中的活動訊號記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4ae9-178">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="d4ae9-179">檢閱 `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent` 中的 Microsoft Monitoring Agent VM 擴充記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4ae9-179">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="d4ae9-180">確定虛擬機器可以執行 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="d4ae9-180">Ensure the virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="d4ae9-181">確定 C:\Windows\temp 的權限未變更</span><span class="sxs-lookup"><span data-stu-id="d4ae9-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="d4ae9-182">在虛擬機器上提高權限的 PowerShell 視窗中輸入下列命令，以檢視 Microsoft Monitoring Agent 的狀態 `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="d4ae9-182">View the status of the Microsoft Monitoring Agent by typing the following command in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="d4ae9-183">檢閱 `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs` 中的 Microsoft Monitoring Agent 安裝記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4ae9-183">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="d4ae9-184">如需詳細資訊，請參閱[針對 Windows 擴充功能進行疑難排解](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="d4ae9-185">針對 Linux 虛擬機器進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d4ae9-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="d4ae9-186">如果未安裝或沒有回報 OMS Agent for Linux VM 代理程式擴充功能，您可以執行下列步驟來針對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-186">If the *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="d4ae9-187">如果擴充狀態是「未知」，請檢閱 VM 代理程式記錄檔 `/var/log/waagent.log`，以檢查 Azure VM 代理程式是否已安裝且正常運作</span><span class="sxs-lookup"><span data-stu-id="d4ae9-187">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="d4ae9-188">如果記錄檔不存在，則表示未安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-188">If the log does not exist, the VM agent is not installed.</span></span>
   * [<span data-ttu-id="d4ae9-189">在 Linux VM 上安裝 Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="d4ae9-189">Install the Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="d4ae9-190">若是其他不良狀態，請檢閱 `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` 和 `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log` 中的 OMS Agent for Linux VM 擴充記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4ae9-190">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="d4ae9-191">如果擴充狀態良好，但資料未上傳，請檢閱 `/var/opt/microsoft/omsagent/log/omsagent.log` 中的 OMS Agent for Linux 記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4ae9-191">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4ae9-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4ae9-192">Next steps</span></span>
* <span data-ttu-id="d4ae9-193">設定 [Log Analytics 中的資料來源](log-analytics-data-sources.md) 來指定要收集的記錄和計量。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics to collect.</span></span>
* <span data-ttu-id="d4ae9-194">[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)，以收集來自虛擬機器的資料。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-194">To gather data from virtual machines [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="d4ae9-195">針對 Azure 中執行的其他資源，[使用 Azure 診斷收集資料](log-analytics-azure-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ae9-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="d4ae9-196">如果電腦不是在 Azure 中，您可以使用下列文章中所述的方法來安裝 Log Analytics 代理程式︰</span><span class="sxs-lookup"><span data-stu-id="d4ae9-196">For computers that are not in Azure, you can install the Log Analytics agent by using the methods that are described in the following articles:</span></span>

* [<span data-ttu-id="d4ae9-197">將 Windows 電腦連接到 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d4ae9-197">Connect Windows computers to Log Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="d4ae9-198">將 Linux 電腦連接到 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d4ae9-198">Connect Linux computers to Log Analytics</span></span>](log-analytics-linux-agents.md)
