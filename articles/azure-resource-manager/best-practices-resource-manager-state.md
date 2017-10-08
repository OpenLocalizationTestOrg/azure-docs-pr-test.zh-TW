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
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="2aa73-103">從 Azure Resource Manager 範本的共用狀態 tooand</span><span class="sxs-lookup"><span data-stu-id="2aa73-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="2aa73-104">這個主題說明在範本中管理和共用狀態的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="2aa73-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="2aa73-105">hello 參數與本主題所顯示的變數是範例的 hello 類型的物件，您可以定義 tooconveniently 組織您的部署需求。</span><span class="sxs-lookup"><span data-stu-id="2aa73-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="2aa73-106">在這些範例中，您可以實作自己的物件與您環境適用的屬性值。</span><span class="sxs-lookup"><span data-stu-id="2aa73-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="2aa73-107">本主題是較大份白皮書的一部分。</span><span class="sxs-lookup"><span data-stu-id="2aa73-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="2aa73-108">tooread hello 完整紙張，下載[世界類別資源管理員範本考量和證明作法](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf)。</span><span class="sxs-lookup"><span data-stu-id="2aa73-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="2aa73-109">提供標準的組態設定</span><span class="sxs-lookup"><span data-stu-id="2aa73-109">Provide standard configuration settings</span></span>
<span data-ttu-id="2aa73-110">而不是提供範本，提供總彈性和無數的變化，常見的模式是 tooprovide 已知設定的選取範圍。</span><span class="sxs-lookup"><span data-stu-id="2aa73-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="2aa73-111">實際上，使用者可選取沙箱、小型、中型和大型等標準 T 恤尺寸。</span><span class="sxs-lookup"><span data-stu-id="2aa73-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="2aa73-112">T 恤尺寸的其他範例包括產品供應項目，例如社群版本或企業版本。</span><span class="sxs-lookup"><span data-stu-id="2aa73-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="2aa73-113">在其他情況下，這可能是某種技術的工作負載特定組態，例如，對應減少或沒有 SQL。</span><span class="sxs-lookup"><span data-stu-id="2aa73-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="2aa73-114">具有複雜的物件，您可以建立包含集合的資料，有時也稱為 「 屬性包"的變數，並在範本中使用該資料 toodrive hello 資源宣告。</span><span class="sxs-lookup"><span data-stu-id="2aa73-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="2aa73-115">這種方法可針對預先為客戶設定好的各種大小提供良好且已知的組態。</span><span class="sxs-lookup"><span data-stu-id="2aa73-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="2aa73-116">沒有已知的組態，hello 範本的使用者必須決定根據自己的因數中的平台資源條件約束的叢集大小，再執行數學 tooidentify hello 產生資料分割的儲存體帳戶和其他資源 (因為 toocluster 大小和資源的條件約束）。</span><span class="sxs-lookup"><span data-stu-id="2aa73-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="2aa73-117">此外 toomaking hello 客戶更好的體驗，幾個已知的設定會更容易 toosupport，可協助您提供更高的密度。</span><span class="sxs-lookup"><span data-stu-id="2aa73-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="2aa73-118">下列範例會示範如何 hello toodefine 變數，其中包含複雜的物件，代表資料的集合。</span><span class="sxs-lookup"><span data-stu-id="2aa73-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="2aa73-119">hello 集合會定義用於虛擬機器大小、 網路設定、 作業系統設定和可用性設定的值。</span><span class="sxs-lookup"><span data-stu-id="2aa73-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

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

<span data-ttu-id="2aa73-120">請注意該 hello **tshirtSize**變數串連您透過參數所提供的 hello t 恤尺寸 (**小**，**媒體**，**大**) toohello 文字**tshirtSize**。</span><span class="sxs-lookup"><span data-stu-id="2aa73-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="2aa73-121">您會將此變數 tooretrieve hello 關聯的複雜物件變數用於該 t 恤尺寸。</span><span class="sxs-lookup"><span data-stu-id="2aa73-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="2aa73-122">然後，您可以參考這些變數，稍後在 hello 範本中。</span><span class="sxs-lookup"><span data-stu-id="2aa73-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="2aa73-123">hello 能力 tooreference 名為的變數和其屬性可簡化 hello 樣板語法，並讓您輕鬆 toounderstand 內容。</span><span class="sxs-lookup"><span data-stu-id="2aa73-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="2aa73-124">hello 下列範例會使用先前顯示 tooset 值 hello 物件，定義資源 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="2aa73-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="2aa73-125">Hello VM 大小所擷取的 hello 值的設定，例如`variables('tshirtSize').vmSize`而 hello 值為 hello 磁碟大小擷取自`variables('tshirtSize').diskSize`。</span><span class="sxs-lookup"><span data-stu-id="2aa73-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="2aa73-126">此外，在連結的範本設定與 hello 值 hello URI `variables('tshirtSize').vmTemplate`。</span><span class="sxs-lookup"><span data-stu-id="2aa73-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

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

## <a name="pass-state-tooa-template"></a><span data-ttu-id="2aa73-127">傳遞狀態 tooa 範本</span><span class="sxs-lookup"><span data-stu-id="2aa73-127">Pass state tooa template</span></span>
<span data-ttu-id="2aa73-128">您可以透過於部署期間直接提供的參數，在範本中共用狀態。</span><span class="sxs-lookup"><span data-stu-id="2aa73-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="2aa73-129">下列資料表列出常用的參數，在範本中的 hello。</span><span class="sxs-lookup"><span data-stu-id="2aa73-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="2aa73-130">名稱</span><span class="sxs-lookup"><span data-stu-id="2aa73-130">Name</span></span> | <span data-ttu-id="2aa73-131">值</span><span class="sxs-lookup"><span data-stu-id="2aa73-131">Value</span></span> | <span data-ttu-id="2aa73-132">說明</span><span class="sxs-lookup"><span data-stu-id="2aa73-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2aa73-133">location</span><span class="sxs-lookup"><span data-stu-id="2aa73-133">location</span></span> |<span data-ttu-id="2aa73-134">來自 Azure 區域之條件約束清單的字串</span><span class="sxs-lookup"><span data-stu-id="2aa73-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="2aa73-135">hello hello 資源部署所在的位置。</span><span class="sxs-lookup"><span data-stu-id="2aa73-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="2aa73-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="2aa73-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="2aa73-137">String</span><span class="sxs-lookup"><span data-stu-id="2aa73-137">String</span></span> |<span data-ttu-id="2aa73-138">Hello 放置 hello VM 磁碟儲存體帳戶的唯一 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="2aa73-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="2aa73-139">domainName</span><span class="sxs-lookup"><span data-stu-id="2aa73-139">domainName</span></span> |<span data-ttu-id="2aa73-140">String</span><span class="sxs-lookup"><span data-stu-id="2aa73-140">String</span></span> |<span data-ttu-id="2aa73-141">Hello 可公開存取 jumpbox VM，hello 格式的網域名稱： **{domainName}。 {location}.cloudapp.com**例如： **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="2aa73-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="2aa73-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="2aa73-142">adminUsername</span></span> |<span data-ttu-id="2aa73-143">String</span><span class="sxs-lookup"><span data-stu-id="2aa73-143">String</span></span> |<span data-ttu-id="2aa73-144">Hello Vm 的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="2aa73-144">Username for hello VMs</span></span> |
| <span data-ttu-id="2aa73-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="2aa73-145">adminPassword</span></span> |<span data-ttu-id="2aa73-146">String</span><span class="sxs-lookup"><span data-stu-id="2aa73-146">String</span></span> |<span data-ttu-id="2aa73-147">Hello Vm 的密碼</span><span class="sxs-lookup"><span data-stu-id="2aa73-147">Password for hello VMs</span></span> |
| <span data-ttu-id="2aa73-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="2aa73-148">tshirtSize</span></span> |<span data-ttu-id="2aa73-149">來自提供 T 恤大小之條件約束清單的字串</span><span class="sxs-lookup"><span data-stu-id="2aa73-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="2aa73-150">名為延展單位大小 tooprovision hello。</span><span class="sxs-lookup"><span data-stu-id="2aa73-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="2aa73-151">例如，"Small"、"Medium"、"Large"</span><span class="sxs-lookup"><span data-stu-id="2aa73-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="2aa73-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="2aa73-152">virtualNetworkName</span></span> |<span data-ttu-id="2aa73-153">String</span><span class="sxs-lookup"><span data-stu-id="2aa73-153">String</span></span> |<span data-ttu-id="2aa73-154">Hello hello 取用者的虛擬網路名稱想 toouse。</span><span class="sxs-lookup"><span data-stu-id="2aa73-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="2aa73-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="2aa73-155">enableJumpbox</span></span> |<span data-ttu-id="2aa73-156">來自條件約束清單的字串 (enabled/disabled)</span><span class="sxs-lookup"><span data-stu-id="2aa73-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="2aa73-157">識別的參數是否 tooenable jumpbox hello 環境。</span><span class="sxs-lookup"><span data-stu-id="2aa73-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="2aa73-158">值："enabled"、"disabled"</span><span class="sxs-lookup"><span data-stu-id="2aa73-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="2aa73-159">hello **tshirtSize** hello 前一節中所使用的參數定義為：</span><span class="sxs-lookup"><span data-stu-id="2aa73-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

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


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="2aa73-160">傳遞狀態 toolinked 範本</span><span class="sxs-lookup"><span data-stu-id="2aa73-160">Pass state toolinked templates</span></span>
<span data-ttu-id="2aa73-161">連接時 toolinked 範本，您通常使用靜態混用，並產生變數。</span><span class="sxs-lookup"><span data-stu-id="2aa73-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="2aa73-162">靜態變數</span><span class="sxs-lookup"><span data-stu-id="2aa73-162">Static variables</span></span>
<span data-ttu-id="2aa73-163">靜態變數通常是使用的 tooprovide 基底值，例如用於整個範本的 Url。</span><span class="sxs-lookup"><span data-stu-id="2aa73-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="2aa73-164">在下列範本摘錄 hello `templateBaseUrl` hello hello 範本的根位置指定在 GitHub 中。</span><span class="sxs-lookup"><span data-stu-id="2aa73-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="2aa73-165">hello 下一行會建立新的變數`sharedTemplateUrl`，串連 hello 與 hello 已知 hello 共用的資源的範本名稱的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="2aa73-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="2aa73-166">線下, 面的複雜物件變數是使用的 toostore t 恤尺寸，其中 hello 基底 URL 是串連的 toohello 已知的組態範本位置，並儲存在 hello`vmTemplate`屬性。</span><span class="sxs-lookup"><span data-stu-id="2aa73-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="2aa73-167">這種方法的 hello 好處是，如果 hello 範本位置變更，您只需要在一個地方，將它傳遞至連結的 hello 範本整個 toochange hello 靜態變數。</span><span class="sxs-lookup"><span data-stu-id="2aa73-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

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

### <a name="generated-variables"></a><span data-ttu-id="2aa73-168">產生的變數</span><span class="sxs-lookup"><span data-stu-id="2aa73-168">Generated variables</span></span>
<span data-ttu-id="2aa73-169">在加法 toostatic 變數中，會動態產生數個變數。</span><span class="sxs-lookup"><span data-stu-id="2aa73-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="2aa73-170">本章節識別 hello 常見類型的產生的變數。</span><span class="sxs-lookup"><span data-stu-id="2aa73-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="2aa73-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="2aa73-171">tshirtSize</span></span>
<span data-ttu-id="2aa73-172">您已熟悉上述 hello 範例從這個產生的變數。</span><span class="sxs-lookup"><span data-stu-id="2aa73-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="2aa73-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="2aa73-173">networkSettings</span></span>
<span data-ttu-id="2aa73-174">在容量、 功能或已設定領域的端對端解決方案範本 hello 連結的範本通常在網路上建立存在的資源。</span><span class="sxs-lookup"><span data-stu-id="2aa73-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="2aa73-175">其中一個簡單的方法是 toouse 複雜物件 toostore 網路設定，並將其傳遞 toolinked 範本。</span><span class="sxs-lookup"><span data-stu-id="2aa73-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="2aa73-176">通訊網路設定的範例如下所示。</span><span class="sxs-lookup"><span data-stu-id="2aa73-176">An example of communicating network settings can be seen below.</span></span>

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

#### <a name="availabilitysettings"></a><span data-ttu-id="2aa73-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="2aa73-177">availabilitySettings</span></span>
<span data-ttu-id="2aa73-178">連結的範本中所建立的資源通常會放置在可用性集合中。</span><span class="sxs-lookup"><span data-stu-id="2aa73-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="2aa73-179">在下列範例的 hello，hello 可用性設定組名稱指定也 hello 容錯網域和更新網域計數 toouse。</span><span class="sxs-lookup"><span data-stu-id="2aa73-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="2aa73-180">如果您需要多個可用性設定組 （例如，一個主要節點），另一個用於資料節點，您可以使用名稱做為前置詞，指定多個可用性設定組，或遵循 hello 模型建立特定的 t 恤尺寸的變數稍早所示。</span><span class="sxs-lookup"><span data-stu-id="2aa73-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="2aa73-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="2aa73-181">storageSettings</span></span>
<span data-ttu-id="2aa73-182">儲存體詳細資料通常會與連結的範本共用。</span><span class="sxs-lookup"><span data-stu-id="2aa73-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="2aa73-183">在 hello 範例所示， *storageSettings*物件提供有關 hello 詳細資料儲存體帳戶和容器名稱。</span><span class="sxs-lookup"><span data-stu-id="2aa73-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="2aa73-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="2aa73-184">osSettings</span></span>
<span data-ttu-id="2aa73-185">連結的範本，您可能需要 toopass 作業系統設定 toovarious 節點類型的各種不同的已知的組態類型。</span><span class="sxs-lookup"><span data-stu-id="2aa73-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="2aa73-186">複雜物件的簡單方法 toostore 和共用作業系統資訊並也可讓您更輕鬆 toosupport 部署多個作業系統選擇。</span><span class="sxs-lookup"><span data-stu-id="2aa73-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="2aa73-187">hello 下列範例顯示的物件*osSettings*:</span><span class="sxs-lookup"><span data-stu-id="2aa73-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="2aa73-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="2aa73-188">machineSettings</span></span>
<span data-ttu-id="2aa73-189">產生的變數 *machineSettings* 是複雜物件，包含用於建立 VM 的核心變數的混合。</span><span class="sxs-lookup"><span data-stu-id="2aa73-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="2aa73-190">hello 變數包含系統管理員使用者名稱和密碼、 hello VM 名稱的前置詞和作業系統映像參考。</span><span class="sxs-lookup"><span data-stu-id="2aa73-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

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

<span data-ttu-id="2aa73-191">請注意， *osImageReference*擷取 hello 值從 hello *osSettings* hello 主要範本中定義的變數。</span><span class="sxs-lookup"><span data-stu-id="2aa73-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="2aa73-192">這表示您可以輕鬆地變更 hello 作業系統的 vm-完全或根據範本的取用者的 hello 喜好設定。</span><span class="sxs-lookup"><span data-stu-id="2aa73-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="2aa73-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="2aa73-193">vmScripts</span></span>
<span data-ttu-id="2aa73-194">hello *vmScripts*物件包含有關 hello 指令碼 toodownload 詳細資料，並包括內部和外部參考的 VM 執行個體上執行。</span><span class="sxs-lookup"><span data-stu-id="2aa73-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="2aa73-195">外部參考包含 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="2aa73-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="2aa73-196">內部參考包含 hello 安裝軟體安裝和設定。</span><span class="sxs-lookup"><span data-stu-id="2aa73-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="2aa73-197">使用 hello *scriptsToDownload*屬性 toolist hello 指令碼 toodownload toohello VM。</span><span class="sxs-lookup"><span data-stu-id="2aa73-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="2aa73-198">此物件也會包含參考 toocommand 列的引數為不同的動作類型。</span><span class="sxs-lookup"><span data-stu-id="2aa73-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="2aa73-199">這些動作包括執行 hello 預設安裝中針對每個個別的節點、 執行所有的節點會在部署之後，安裝可能會提供範本的特定 tooa 任何其他指令碼。</span><span class="sxs-lookup"><span data-stu-id="2aa73-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="2aa73-200">這個範例是使用樣板 toodeploy MongoDB，需要仲裁 toodeliver 高可用性。</span><span class="sxs-lookup"><span data-stu-id="2aa73-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="2aa73-201">hello *arbiterNodeInstallCommand*太已加入*vmScripts* tooinstall hello 仲裁。</span><span class="sxs-lookup"><span data-stu-id="2aa73-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="2aa73-202">hello 變數區段是您在其中找到 hello 變數定義 hello 特定文字 tooexecute hello 指令碼以 hello 適當的值。</span><span class="sxs-lookup"><span data-stu-id="2aa73-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="2aa73-203">從範本傳回狀態</span><span class="sxs-lookup"><span data-stu-id="2aa73-203">Return state from a template</span></span>
<span data-ttu-id="2aa73-204">不只可以將資料傳遞至範本，您也可以共用資料回復 toohello 呼叫範本。</span><span class="sxs-lookup"><span data-stu-id="2aa73-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="2aa73-205">在 hello**輸出**> 一節的連結的範本，您可以提供可供 hello 來源範本的索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="2aa73-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="2aa73-206">hello 下列範例顯示如何 toopass hello 產生連結的範本中的私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2aa73-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="2aa73-207">內 hello 主要範本，您可以使用該資料以 hello，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="2aa73-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="2aa73-208">您可以使用這個 hello 輸出區段或 hello hello 主要範本的資源 > 一節中的運算式。</span><span class="sxs-lookup"><span data-stu-id="2aa73-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="2aa73-209">您無法使用 hello 運算式 hello 變數區段中，因為它是倚賴 hello 執行階段狀態。</span><span class="sxs-lookup"><span data-stu-id="2aa73-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="2aa73-210">tooreturn hello 主要範本，使用此值：</span><span class="sxs-lookup"><span data-stu-id="2aa73-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="2aa73-211">如需使用 hello 的範例輸出區段的連結的範本 tooreturn 資料磁碟的虛擬機器，請參閱 <<c0> [ 建立多個資料磁碟的虛擬機器](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="2aa73-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="2aa73-212">為虛擬機器定義驗證設定</span><span class="sxs-lookup"><span data-stu-id="2aa73-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="2aa73-213">您可以使用 hello 先前顯示的組態設定 toospecify hello 驗證設定的虛擬機器相同的模式。</span><span class="sxs-lookup"><span data-stu-id="2aa73-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="2aa73-214">您傳遞的參數建立 hello 的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="2aa73-214">You create a parameter for passing in hello type of authentication.</span></span>

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

<span data-ttu-id="2aa73-215">您加入為 hello 不同的驗證類型和變數的 toostore 這個 hello hello 參數值為基礎的部署所使用哪種類型的變數。</span><span class="sxs-lookup"><span data-stu-id="2aa73-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

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

<span data-ttu-id="2aa73-216">在定義 hello 虛擬機器時，您會設定 hello **osProfile** toohello 您建立的變數。</span><span class="sxs-lookup"><span data-stu-id="2aa73-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="2aa73-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2aa73-217">Next steps</span></span>
* <span data-ttu-id="2aa73-218">toolearn 關於 hello 區段 hello 範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="2aa73-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="2aa73-219">toosee hello 函式可用在樣板中，請參閱[Azure 資源管理員範本函式](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="2aa73-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
