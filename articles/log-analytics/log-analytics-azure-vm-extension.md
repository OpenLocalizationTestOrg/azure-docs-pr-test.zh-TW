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
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>記錄分析代理程式連接 Azure 虛擬機器 tooLog 分析

針對 Windows 和 Linux 電腦，hello 建議使用的方法來收集記錄檔和度量資訊是透過安裝 hello 記錄分析代理程式。

hello 最簡單方式 tooinstall hello 記錄分析代理程式在 Azure 虛擬機器上的都是透過 hello 記錄分析 VM 延伸模組。  使用 hello 延伸模組可簡化 hello 安裝程序，並會自動設定 hello 代理程式 toosend 資料 toohello 記錄分析工作區，您所指定。 hello 代理程式就也會自動升級，確保您擁有 hello 最新功能和修正程式。

您可以為 Windows 虛擬機器，啟用 hello *Microsoft Monitoring Agent*虛擬機器擴充功能。
針對 Linux 虛擬機器，您可以啟用 hello *OMS Agent For Linux*虛擬機器擴充功能。

深入了解[Azure 虛擬機器擴充功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和 hello [Linux 代理程式](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

當您使用代理程式型集合的記錄資料時，您必須設定[記錄分析中的資料來源](log-analytics-data-sources.md)toospecify hello 記錄檔和度量的 toocollect。

> [!IMPORTANT]
> 如果您設定記錄分析 tooindex 記錄資料使用[Azure 診斷](log-analytics-azure-storage.md)，和您設定 hello 代理程式 toocollect hello 相同記錄檔時，則 hello 記錄檔會收集兩次。 您需支付這兩個資料來源的費用。 如果您已安裝的 hello 代理程式，然後使用僅 hello 代理程式收集記錄資料-未設定來自 Azure 診斷的記錄分析 toocollect 記錄資料。
>
>

有三個簡單的方法 tooenable hello 記錄分析虛擬機器擴充功能：

* 使用 hello Azure 入口網站
* 使用 Azure PowerShell
* 透過使用 Azure Resource Manager 範本

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>啟用 hello Azure 入口網站中的 hello VM 擴充功能
您可以記錄分析的 hello 代理程式安裝並連接 hello Azure 虛擬機器上執行使用 hello [Azure 入口網站](https://portal.azure.com)。

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall hello 記錄分析代理程式，並連接 hello 虛擬機器 tooa 記錄分析工作區
1. 登入 hello [Azure 入口網站](http://portal.azure.com)。
2. 選取**瀏覽**上 hello 的左方 hello 入口網站，然後再移過**記錄分析 (OMS)**並加以選取。
3. 在清單中的記錄分析工作區，選取 hello 其中一個要 toouse 以 hello Azure VM。  
   ![OMS 工作區](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. 在 [Log Analytics 管理] 下方，選取 [虛擬機器]。  
   ![虛擬機器](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. 中的 hello 清單**虛擬機器**，選取 hello 想 tooinstall hello 代理程式的虛擬機器。 hello **OMS 連接狀態**hello VM 指出它是**未連接**。  
   ![VM 未連接](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. 在您的虛擬機器的 hello 詳細資料，選取**連接**。 hello 代理程式會自動安裝並設定為記錄分析工作區。 這個程序需要幾分鐘的時間，在這段期間是 hello OMS 連接狀態*連接...*  
   ![連接 VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. 您安裝並連接 hello 代理程式之後，hello **OMS 連線**狀態會更新的 tooshow**這個工作區**。  
   ![已連接](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>啟用使用 PowerShell 的 hello VM 擴充功能
當您使用 PowerShell 來設定您的虛擬機器時，您需要 tooprovide hello**工作區識別碼**和**workspaceKey**。 json 組態中的 hello 屬性名稱都是**區分大小寫**。

您可以找到 hello 識別碼和索引鍵上 hello**設定**頁面上，hello OMS 入口網站，或使用 PowerShell hello 前面範例所示。

![工作區識別碼及主要金鑰](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Azure 傳統虛擬機器和 Resource Manager 虛擬機器各使用不同的命令。 以下是傳統和 Resource Manager 虛擬機器的範例。

傳統的虛擬機器，請使用下列 PowerShell 範例 hello:

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

使用下列 CLI hello 的資源管理員 Linux Vm 的
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

資源管理員虛擬機器，請使用下列 PowerShell 範例 hello:

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


## <a name="deploy-hello-vm-extension-using-a-template"></a>使用範本的 hello VM 延伸模組部署
使用 Azure Resource Manager，您可以建立定義 hello 部署和設定您的應用程式的範本 （以 JSON 格式）。 此範本稱為資源管理員範本，並提供宣告式方式 toodefine 部署。 藉由使用範本，您可以重複將整個 hello 應用程式生命週期的應用程式部署，並有信心，您部署資源時處於一致的狀態。

藉由加入 hello 記錄分析代理程式做為 Resource Manager 範本的一部分，您可以確保每個虛擬機器已預先設定的 tooreport tooyour 記錄分析工作區。

如需 Resource Manager 範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。

下列是用來部署虛擬機器執行 Windows hello 安裝 Microsoft Monitoring Agent 擴充功能與資源管理員範本的範例。 此範本是典型的虛擬機器範本，以下列新增項目 hello:

* workspaceId 和 workspaceName 參數
* Microsoft.EnterpriseCloud.Monitoring 資源擴充功能區段
* 輸出 toolook hello 工作區識別碼和 workspaceSharedKey

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

您可以使用下列 PowerShell 命令的 hello 部署範本：

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>疑難排解 hello 記錄分析 VM 擴充功能
當系統無法運作時，您通常會收到一則訊息 (從 Azure 入口網站或 Azure Powershell)。

1. 登入 hello [Azure 入口網站](http://portal.azure.com)。
2. 尋找 hello VM 並開啟 VM 詳細資料。
3. 按一下**延伸**toocheck 如果已啟用 OMS 擴充功能。

   ![VM 擴充功能檢視](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. 按一下 hello *MicrosoftMonitoringAgent*(Windows) 或*OmsAgentForLinux*(Linux) 延伸模組並檢視詳細資料。 

   ![VM 擴充功能詳細資料](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>針對 Windows 虛擬機器進行疑難排解
如果 hello *Microsoft Monitoring Agent*不安裝 VM 代理程式延伸模組或 reporting，您可以執行下列步驟 tootroubleshoot hello 問題 hello。

1. 檢查是否安裝 hello Azure VM 代理程式，並正確地利用 hello 工作中的步驟[KB 2965986](https://support.microsoft.com/kb/2965986#mt1)。
   * 您也可以檢閱 hello VM 代理程式記錄檔`C:\WindowsAzure\logs\WaAppAgent.log`
   * Hello 記錄不存在，如果未安裝 hello VM 代理程式。
     * [在傳統的 Vm 上安裝 hello Azure VM 代理程式](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. 確認 hello Microsoft Monitoring Agent 擴充功能的活動訊號工作正在執行使用 hello 下列步驟：
   * 登入 toohello 虛擬機器
   * 開啟 工作排程器，並尋找 hello`update_azureoperationalinsight_agent_heartbeat`工作
   * 確認 hello 工作已啟用，而且正在執行每一分鐘
   * 檢查 hello 活動訊號記錄檔`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. 檢閱 hello Microsoft 監視代理程式 VM 擴充功能中的記錄檔`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. 確保 hello 虛擬機器可以執行 PowerShell 指令碼
5. 確定 C:\Windows\temp 的權限未變更
6. 輸入下列命令，在提升權限的 PowerShell 視窗 hello 虛擬機器上的 hello 檢視 hello hello Microsoft Monitoring Agent 狀態`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. 檢閱 hello Microsoft Monitoring Agent 安裝程式記錄檔中`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

如需詳細資訊，請參閱[針對 Windows 擴充功能進行疑難排解](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

### <a name="troubleshooting-linux-virtual-machines"></a>針對 Linux 虛擬機器進行疑難排解
如果 hello *OMS Agent for Linux*不安裝 VM 代理程式延伸模組或 reporting，您可以執行下列步驟 tootroubleshoot hello 問題 hello。

1. 如果 hello 擴充狀態是*未知*檢查 hello Azure VM 代理程式是否已安裝並正常運作，藉由檢閱 hello VM 代理程式記錄檔`/var/log/waagent.log`
   * Hello 記錄不存在，如果未安裝 hello VM 代理程式。
   * [在 Linux Vm 上安裝 hello Azure VM 代理程式](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. 檢閱 hello OMS Agent for Linux VM 擴充功能的其他的狀況不良狀態，記錄檔`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log`和`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. 如果 hello 延伸狀態為狀況良好，但不上載資料檢閱 hello OMS Agent for Linux 記錄檔`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>後續步驟
* 設定[記錄分析中的資料來源](log-analytics-data-sources.md)toospecify hello 記錄檔和度量 toocollect。
* 虛擬機器的 toogather 資料[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。
* 針對 Azure 中執行的其他資源，[使用 Azure 診斷收集資料](log-analytics-azure-storage.md)。

對於不在 Azure 中的電腦，您可以使用 hello 方法 hello 下列文章中所述安裝 hello 記錄分析代理程式：

* [連接 Windows 電腦 tooLog 分析](log-analytics-windows-agents.md)
* [連線 Linux 電腦 tooLog 分析](log-analytics-linux-agents.md)
