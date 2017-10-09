---
title: "aaaAutoscale Linux 虛擬機器擴展集 |Microsoft 文件"
description: "使用 Azure CLI 設定自動調整 Linux 虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a>在虛擬機器擴展集中自動調整 Linux 機器
虛擬機器擴展集讓您輕鬆為您 toodeploy 和管理一組相同的虛擬機器。 調整集可為超大規模的應用程式提供高度擴充和可自訂的計算層，並且可支援 Windows 平台映像、Linux 平台映像、自訂映像和擴充。 詳細資訊，請參閱 toolearn[虛擬機器規模集概觀](virtual-machine-scale-sets-overview.md)。

本教學課程會示範使用 Ubuntu Linux hello 最新版本的 Linux 虛擬機器設定 toocreate 小數位數的方式。 hello 教學課程也會顯示在 hello tooautomatically 標尺 hello 機器的設定方式。 您建立設定和設定調整建立 Azure 資源管理員範本，並將它使用 Azure CLI 部署的 hello 小數位數。 如需範本的詳細資訊，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。 請參閱詳細的擴展集自動調整 toolearn[自動縮放和虛擬機器規模設定](virtual-machine-scale-sets-autoscale-overview.md)。

在此教學課程中，您將部署 hello 下列資源和擴充功能：

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Insights.VMDiagnosticsSettings
* Microsoft.Insights/autoscaleSettings

如需 Resource Manager 資源的詳細資訊，請參閱 [Azure Resource Manager 與傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。

您在本教學課程中，開始使用 hello 步驟之前[安裝 hello Azure CLI](../cli-install-nodejs.md)。

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a>步驟 1：建立資源群組和儲存體帳戶

1. **登入 tooMicrosoft Azure**  
在您的命令列介面 （Bash，終端機，命令提示字元），切換 tooResource 管理員模式中，然後[登入您的工作或學校 id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login)。請遵循互動式登入經驗 tooyour Azure 帳戶的 hello 提示。

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > 如果您有工作或學校識別碼，而且您不啟用雙因素驗證，請使用`azure login -u`與 hello 識別碼 toolog 中不包含互動式工作階段。 如果您沒有工作或學校識別碼，您可以[從個人的 Microsoft 帳戶建立工作或學校識別碼](../active-directory/active-directory-users-create-azure-portal.md)。
    
2. **建立資源群組**  
所有資源必須都是已部署的 tooa 資源群組。 本教學課程中，命名 hello 資源群組**vmsstest1**。
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. **將儲存體帳戶部署到 hello 新資源群組**  
這個儲存體帳戶是儲存 hello 範本。 建立名為 **vmsstestsa**的儲存體帳戶。
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a>步驟 2： 建立 hello 範本
Azure 資源管理員範本可讓您 toodeploy，並使用 hello 資源和相關聯的部署參數的 JSON 描述一起管理 Azure 資源。

1. 在您最愛的編輯器，建立 hello 檔案 VMSSTemplate.json 並加入 hello 初始 JSON 結構 toosupport hello 範本。

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. 參數並非必要，但它們的方式 tooinput 值時提供部署 hello 範本。 加入這些參數，就像加入 toohello 範本 hello 參數父元素底下。

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * Hello 不同的虛擬機器使用的 tooaccess hello 機器 hello 規模集中的名稱。
   * Hello hello 範本儲存所在的儲存體帳戶名稱。
   * 執行個體的虛擬機器 tooinitially 的 hello 數目建立 hello 規模集中。
   * 名稱和 hello hello 虛擬機器上的系統管理員帳戶的密碼。
   * 設定會建立 toosupport hello 標尺的 hello 資源的名稱前置詞。

3. 變數可以用於會經常變更的範本 toospecify 值，或從參數值組合建立需要 toobe 的值。 新增這些變數，就像加入 toohello 範本 hello 變數的父元素底下。

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * Hello 網路介面所使用的 DNS 名稱。
   * hello IP 位址名稱和 hello 虛擬網路和子網路前置詞。
   * hello 名稱和識別碼 hello 虛擬網路的負載平衡器，與網路介面。
   * Hello 帳戶 hello 規模集中的 hello 機器相關聯的儲存體帳戶名稱。
   * Hello hello 虛擬機器已安裝的診斷延伸模組的設定。 如需 hello 診斷延伸模組的詳細資訊，請參閱[使用監視和診斷使用 Azure Resource Manager 範本建立 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

4. 將您加入 toohello 範本 hello 資源父元素底下的 hello 儲存體帳戶資源。 此範本會使用建議的五個儲存體帳戶迴圈 toocreate hello hello 作業系統磁碟和診斷資料的儲存位置。 這組帳戶可以支援註冊 too100 虛擬機器規模集中的也就是 hello 目前最大值。 每個儲存體帳戶是名為具有與 hello 尾碼 hello 範本 hello 參數中提供的 hello 變數中定義的字母指示項。
   
        {
          "type": "Microsoft.Storage/storageAccounts",
          "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
          "apiVersion": "2015-06-15",
          "copy": {
            "name": "storageLoop",
            "count": 5
          },
          "location": "[resourceGroup().location]",
          "properties": { "accountType": "Standard_LRS" }
        },

5. 新增 hello 虛擬網路資源。 如需詳細資訊，請參閱 [網路資源提供者](../virtual-network/resource-groups-networking.md)。

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. 加入所使用的 hello 的 hello 公用 IP 位址資源負載平衡器和網路介面。

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. 新增 hello 負載平衡器資源，以供 hello 規模集。 如需詳細資料，請參閱 [Azure 資源管理員的負載平衡器支援](../load-balancer/load-balancer-arm.md)。

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. 新增 hello 網路介面資源，以供 hello 不同的虛擬機器。 規模集中的電腦無法存取透過公用 IP 位址，因為不同的虛擬機器中建立 hello 相同虛擬網路 tooremotely 存取 hello 機器。

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. 新增的 hello hello 小數位數設定為相同網路中的 hello 不同的虛擬機器。

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
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
        }
      }
    },
    ```

10. 新增 hello 虛擬機器規模集的資源，並指定 hello 規模集中的所有虛擬機器已安裝的 hello 診斷延伸模組。 其中許多 hello 這個資源的設定都與 hello 虛擬機器資源。 hello 主要差異是指定的虛擬機器的 hello 數目 hello 規模集中的 hello 容量項目以及 upgradePolicy，指定如何進行更新 toovirtual 機器。 hello 規模集不會建立直到所有 hello 儲存體帳戶都建立與 hello dependsOn 元素所指定。

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. 新增定義如何 hello 規模集調整根據 hello 集合中的 hello 機器上的處理器使用量的 hello autoscaleSettings 資源。

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor\\PercentProcessorTime",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```
    
    在本教學課程中，以下的值相當重要：
    
    * **metricName**  
    此值為 hello 相同 hello 我們 hello wadperfcounter 變數中所定義的效能計數器。 使用該變數，hello 診斷擴充功能會收集 hello **Processor\PercentProcessorTime**計數器。
    
    * **metricResourceUri**  
    此值為 hello 虛擬機器規模集的 hello 資源識別項。
    
    * **timeGrain**  
    此值為 hello 的 hello 計量所收集的資料粒度。 在此範本，它會設定 tooone 分鐘。
    
    * **statistic**  
    這個值會決定如何 hello 度量資訊會結合的 tooaccommodate hello 自動調整規模動作。 hello 可能的值為： 平均值、 最小值、 最大值。 在此範本中，會收集 hello 平均 CPU 使用量總計的 hello 虛擬機器。

    * **timeWindow**  
    此值為 hello 收集執行個體資料的時間範圍。 其值必須介於 5 分鐘到 12 小時之間。
    
    * **timeAggregation**  
    其值會決定如何隨著時間結合收集的 hello 資料。 hello 預設值是 Average。 hello 可能的值為： 平均、 最小值、 最大值、 最後一個、 總和、 計數。
    
    * **operator**  
    這個值是使用的 toocompare hello 度量資料與 hello 臨界值的 hello 運算子。 hello 可能的值為： NotEquals、 GreaterThan、 GreaterThanOrEqual、 LessThan、 LessThanOrEqual 等於。
    
    * **threshold**  
    這個值會觸發 hello 調整規模動作。 在此範本中，機器會新增 toohello 小數位數時，設定 hello 集合中的機器之間 hello 平均 CPU 使用量超過 50%。
    
    * **direction**  
    這個值會決定 hello 為止 hello 臨界值時所執行的動作。 hello 可能的值為增加或減少。 此範本中 hello hello 規模集中的虛擬機器數目會增加如果 hello 臨界值超過所定義的 hello 時間視窗中的 50%。

    * **type**  
    此值為 hello 應該會發生，且必須設定 tooChangeCount 的動作類型。
    
    * **value**  
    此值為 hello 的新增或移除 hello 規模集中的虛擬機器的數目。 此值必須是 1 或更大。 hello 預設值為 1。 此範本中 hello 機器 hello 規模組數目會增加 1 符合 hello 臨界值時。

    * **cooldown**  
    Hello 下一個動作發生之前，這個值會是 hello 數量時間 toowait 自 hello 的最後一個調整動作。 此值必須介於一分鐘到一週之間。

12. 儲存 hello 範本檔案。    

## <a name="step-3-upload-hello-template-toostorage"></a>步驟 3： 上傳 hello 範本 toostorage
可以上傳 hello 範本，只要您知道 hello 名稱以及您在步驟 1 中建立的 hello 儲存體帳戶的主索引鍵。

1. 在您的命令列介面 （Bash，終端機，命令提示字元），執行這些命令 tooset hello 環境變數所需 tooaccess hello 儲存體帳戶：

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    您可以按一下 hello 索引鍵圖示，在 hello Azure 入口網站中檢視 hello 儲存體帳戶資源時，以取得 hello 索引鍵。 使用 Windows 命令提示字元時，請輸入 **set** 而不是 export。

2. 建立 hello 容器儲存 hello 範本。
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. 上傳 hello 範本檔案 toohello 新容器。
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a>步驟 4： 部署的 hello 範本
現在，您建立 hello 範本時，就可以開始部署 hello 資源。 使用此命令 toostart hello 程序：

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

當您按下輸入，會提示的 tooprovide hello 變數指派給您的值。 請提供下列值：

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

它的所有 hello 資源 toosuccessfully 都部署時間大約 15 分鐘。

> [!NOTE]
> 您也可以使用 hello 入口網站的能力 toodeploy hello 資源。 請使用此連結：https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>


## <a name="step-5-monitor-resources"></a>步驟 5：監視資源
您可以使用下列方法，取得關於虛擬機器調整集的某些資訊：

* hello Azure 入口網站-目前就可以使用 hello 入口網站的資訊數量有限。

* hello [Azure 資源總管](https://resources.azure.com/)-此工具為 hello 最適合瀏覽 hello 擴展集的目前狀態。 按照此路徑，您應該會看到您建立 hello hello 標尺的執行個體檢視集：
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* Azure CLI-使用此命令 tooget 一些資訊：

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* Toohello jumpbox 虛擬機器連線，就像任何其他電腦，然後您可以從遠端存取 hello hello 小數位數組 toomonitor 個別處理程序中的虛擬機器時，一樣。

> [!NOTE]
> 在 [虛擬機器調整集](https://msdn.microsoft.com/library/mt589023.aspx)中可以找到用來取得調整集相關資訊的完整 REST API。

## <a name="step-6-remove-hello-resources"></a>步驟 6： 移除 hello 資源
因為您負責 Azure 中使用的資源，但它永遠是很好的作法 toodelete 資源不再需要的。 您不需要 toodelete 分開資源群組的每個資源。 您可以刪除 hello 資源群組，而且會自動刪除其所有資源。

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a>後續步驟
* 在 [Azure 監視器跨平台 CLI 快速入門範例](../monitoring-and-diagnostics/insights-cli-samples.md)中找到 Azure 監視器監視功能的範例
* 了解通知功能[用於 Azure 監視的自動調整規模動作 toosend 電子郵件和 webhook 警示通知](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* 了解如何太[使用稽核記錄 toosend 電子郵件和 webhook 警示通知，在 Azure 監視器](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)
* 簽出 hello[自動調整規模示範應用程式上 Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)設定 Python/bottle 應用程式 tooexercise hello 自動調整的虛擬機器規模設定功能的範本。

