---
title: "aaaPass Azure 範本之間的複雜值 |Microsoft 文件"
description: "顯示建議的方法可搭配 Azure 資源管理員範本和連結的範本中使用複雜物件 tooshare 狀態資料。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>從 Azure Resource Manager 範本的共用狀態 tooand
這個主題說明在範本中管理和共用狀態的最佳做法。 hello 參數與本主題所顯示的變數是範例的 hello 類型的物件，您可以定義 tooconveniently 組織您的部署需求。 在這些範例中，您可以實作自己的物件與您環境適用的屬性值。

本主題是較大份白皮書的一部分。 tooread hello 完整紙張，下載[世界類別資源管理員範本考量和證明作法](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf)。

## <a name="provide-standard-configuration-settings"></a>提供標準的組態設定
而不是提供範本，提供總彈性和無數的變化，常見的模式是 tooprovide 已知設定的選取範圍。 實際上，使用者可選取沙箱、小型、中型和大型等標準 T 恤尺寸。 T 恤尺寸的其他範例包括產品供應項目，例如社群版本或企業版本。 在其他情況下，這可能是某種技術的工作負載特定組態，例如，對應減少或沒有 SQL。

具有複雜的物件，您可以建立包含集合的資料，有時也稱為 「 屬性包"的變數，並在範本中使用該資料 toodrive hello 資源宣告。 這種方法可針對預先為客戶設定好的各種大小提供良好且已知的組態。 沒有已知的組態，hello 範本的使用者必須決定根據自己的因數中的平台資源條件約束的叢集大小，再執行數學 tooidentify hello 產生資料分割的儲存體帳戶和其他資源 (因為 toocluster 大小和資源的條件約束）。 此外 toomaking hello 客戶更好的體驗，幾個已知的設定會更容易 toosupport，可協助您提供更高的密度。

下列範例會示範如何 hello toodefine 變數，其中包含複雜的物件，代表資料的集合。 hello 集合會定義用於虛擬機器大小、 網路設定、 作業系統設定和可用性設定的值。

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

請注意該 hello **tshirtSize**變數串連您透過參數所提供的 hello t 恤尺寸 (**小**，**媒體**，**大**) toohello 文字**tshirtSize**。 您會將此變數 tooretrieve hello 關聯的複雜物件變數用於該 t 恤尺寸。

然後，您可以參考這些變數，稍後在 hello 範本中。 hello 能力 tooreference 名為的變數和其屬性可簡化 hello 樣板語法，並讓您輕鬆 toounderstand 內容。 hello 下列範例會使用先前顯示 tooset 值 hello 物件，定義資源 toodeploy。 Hello VM 大小所擷取的 hello 值的設定，例如`variables('tshirtSize').vmSize`而 hello 值為 hello 磁碟大小擷取自`variables('tshirtSize').diskSize`。 此外，在連結的範本設定與 hello 值 hello URI `variables('tshirtSize').vmTemplate`。

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a>傳遞狀態 tooa 範本
您可以透過於部署期間直接提供的參數，在範本中共用狀態。

下列資料表列出常用的參數，在範本中的 hello。

| 名稱 | 值 | 說明 |
| --- | --- | --- |
| location |來自 Azure 區域之條件約束清單的字串 |hello hello 資源部署所在的位置。 |
| storageAccountNamePrefix |String |Hello 放置 hello VM 磁碟儲存體帳戶的唯一 DNS 名稱 |
| domainName |String |Hello 可公開存取 jumpbox VM，hello 格式的網域名稱： **{domainName}。 {location}.cloudapp.com**例如： **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |String |Hello Vm 的使用者名稱 |
| adminPassword |String |Hello Vm 的密碼 |
| tshirtSize |來自提供 T 恤大小之條件約束清單的字串 |名為延展單位大小 tooprovision hello。 例如，"Small"、"Medium"、"Large" |
| virtualNetworkName |String |Hello hello 取用者的虛擬網路名稱想 toouse。 |
| enableJumpbox |來自條件約束清單的字串 (enabled/disabled) |識別的參數是否 tooenable jumpbox hello 環境。 值："enabled"、"disabled" |

hello **tshirtSize** hello 前一節中所使用的參數定義為：

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a>傳遞狀態 toolinked 範本
連接時 toolinked 範本，您通常使用靜態混用，並產生變數。

### <a name="static-variables"></a>靜態變數
靜態變數通常是使用的 tooprovide 基底值，例如用於整個範本的 Url。

在下列範本摘錄 hello `templateBaseUrl` hello hello 範本的根位置指定在 GitHub 中。 hello 下一行會建立新的變數`sharedTemplateUrl`，串連 hello 與 hello 已知 hello 共用的資源的範本名稱的基底 URL。 線下, 面的複雜物件變數是使用的 toostore t 恤尺寸，其中 hello 基底 URL 是串連的 toohello 已知的組態範本位置，並儲存在 hello`vmTemplate`屬性。

這種方法的 hello 好處是，如果 hello 範本位置變更，您只需要在一個地方，將它傳遞至連結的 hello 範本整個 toochange hello 靜態變數。

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a>產生的變數
在加法 toostatic 變數中，會動態產生數個變數。 本章節識別 hello 常見類型的產生的變數。

#### <a name="tshirtsize"></a>tshirtSize
您已熟悉上述 hello 範例從這個產生的變數。

#### <a name="networksettings"></a>networkSettings
在容量、 功能或已設定領域的端對端解決方案範本 hello 連結的範本通常在網路上建立存在的資源。 其中一個簡單的方法是 toouse 複雜物件 toostore 網路設定，並將其傳遞 toolinked 範本。

通訊網路設定的範例如下所示。

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a>availabilitySettings
連結的範本中所建立的資源通常會放置在可用性集合中。 在下列範例的 hello，hello 可用性設定組名稱指定也 hello 容錯網域和更新網域計數 toouse。

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

如果您需要多個可用性設定組 （例如，一個主要節點），另一個用於資料節點，您可以使用名稱做為前置詞，指定多個可用性設定組，或遵循 hello 模型建立特定的 t 恤尺寸的變數稍早所示。

#### <a name="storagesettings"></a>storageSettings
儲存體詳細資料通常會與連結的範本共用。 在 hello 範例所示， *storageSettings*物件提供有關 hello 詳細資料儲存體帳戶和容器名稱。

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
連結的範本，您可能需要 toopass 作業系統設定 toovarious 節點類型的各種不同的已知的組態類型。 複雜物件的簡單方法 toostore 和共用作業系統資訊並也可讓您更輕鬆 toosupport 部署多個作業系統選擇。

hello 下列範例顯示的物件*osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
產生的變數 *machineSettings* 是複雜物件，包含用於建立 VM 的核心變數的混合。 hello 變數包含系統管理員使用者名稱和密碼、 hello VM 名稱的前置詞和作業系統映像參考。

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

請注意， *osImageReference*擷取 hello 值從 hello *osSettings* hello 主要範本中定義的變數。 這表示您可以輕鬆地變更 hello 作業系統的 vm-完全或根據範本的取用者的 hello 喜好設定。

#### <a name="vmscripts"></a>vmScripts
hello *vmScripts*物件包含有關 hello 指令碼 toodownload 詳細資料，並包括內部和外部參考的 VM 執行個體上執行。 外部參考包含 hello 基礎結構。
內部參考包含 hello 安裝軟體安裝和設定。

使用 hello *scriptsToDownload*屬性 toolist hello 指令碼 toodownload toohello VM。 此物件也會包含參考 toocommand 列的引數為不同的動作類型。 這些動作包括執行 hello 預設安裝中針對每個個別的節點、 執行所有的節點會在部署之後，安裝可能會提供範本的特定 tooa 任何其他指令碼。

這個範例是使用樣板 toodeploy MongoDB，需要仲裁 toodeliver 高可用性。 hello *arbiterNodeInstallCommand*太已加入*vmScripts* tooinstall hello 仲裁。

hello 變數區段是您在其中找到 hello 變數定義 hello 特定文字 tooexecute hello 指令碼以 hello 適當的值。

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>從範本傳回狀態
不只可以將資料傳遞至範本，您也可以共用資料回復 toohello 呼叫範本。 在 hello**輸出**> 一節的連結的範本，您可以提供可供 hello 來源範本的索引鍵/值組。

hello 下列範例顯示如何 toopass hello 產生連結的範本中的私人 IP 位址。

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

內 hello 主要範本，您可以使用該資料以 hello，請使用下列語法：

    "[reference('master-node').outputs.masterip.value]"

您可以使用這個 hello 輸出區段或 hello hello 主要範本的資源 > 一節中的運算式。 您無法使用 hello 運算式 hello 變數區段中，因為它是倚賴 hello 執行階段狀態。 tooreturn hello 主要範本，使用此值：

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

如需使用 hello 的範例輸出區段的連結的範本 tooreturn 資料磁碟的虛擬機器，請參閱 <<c0> [ 建立多個資料磁碟的虛擬機器](resource-group-create-multiple.md)。

## <a name="define-authentication-settings-for-virtual-machine"></a>為虛擬機器定義驗證設定
您可以使用 hello 先前顯示的組態設定 toospecify hello 驗證設定的虛擬機器相同的模式。 您傳遞的參數建立 hello 的驗證類型。

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

您加入為 hello 不同的驗證類型和變數的 toostore 這個 hello hello 參數值為基礎的部署所使用哪種類型的變數。

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

在定義 hello 虛擬機器時，您會設定 hello **osProfile** toohello 您建立的變數。

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>後續步驟
* toolearn 關於 hello 區段 hello 範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)
* toosee hello 函式可用在樣板中，請參閱[Azure 資源管理員範本函式](resource-group-template-functions.md)
