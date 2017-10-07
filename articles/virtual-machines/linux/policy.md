---
title: "在 Azure 中的 Linux Vm 上的原則 aaaEnforce 安全性 |Microsoft 文件"
description: "如何 tooapply 原則 tooan Azure 資源管理員 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a>套用原則 tooLinux Vm 與 Azure 資源管理員
藉由使用原則，組織可以強制執行各種不同的慣例和 hello 企業內的規則。 強制執行 hello 預期行為可以協助降低風險，同時也參與狀況 hello 組織 toohello 成功。 在本文中，我們會說明如何使用 Azure 資源管理員原則 toodefine hello 預期行為，以及在貴組織的虛擬機器。

如簡介 toopolicies，請參閱[使用原則 toomanage 資源和控制存取](../../azure-resource-manager/resource-manager-policy.md)。

## <a name="permitted-virtual-machines"></a>允許的虛擬機器
tooensure 貴組織的虛擬機器會與應用程式相容，您可以限制允許使用作業系統的 hello。 在 hello 下列原則範例，您將允許只有 Ubuntu 14.04.2-LTS 虛擬機器建立 toobe。

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

使用上述任何 Ubuntu LTS 影像原則 tooallow 萬用字元 toomodify hello: 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

如需原則欄位的相關資訊，請參閱[原則別名](../../azure-resource-manager/resource-manager-policy.md#aliases)。

## <a name="managed-disks"></a>受控磁碟

toorequire hello 的使用受管理的磁碟使用 hello 下列原則：

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a>虛擬機器的映像

基於安全性理由，您可以要求只在環境中部署已核准的自訂映像。 您可以指定 hello 資源群組含有 hello 核准的映像，或是 hello 特定核准的映像。

下列範例中的 hello 需要從核准的資源群組的映像：

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

hello 下列範例會指定 hello 核准的映像識別碼：

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>虛擬機器延伸模組

您可能想 tooforbid 某些類型的擴充功能的使用方式。 例如，一個延伸模組可能與某些自訂虛擬機器映像不相容。 下列範例會示範如何 hello tooblock 特定擴充功能。 它會使用發行者和類型 toodetermine 哪些延伸模組 tooblock。

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a>後續步驟
* 定義原則規則 （如 hello 前面範例所示） 之後, 您會需要 toocreate hello 原則定義，並將它指派 tooa 範圍。 hello 領域可以訂用帳戶、 資源群組或資源。 tooassign 原則透過 hello 入口網站，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](../../azure-resource-manager/resource-manager-policy-portal.md)。 tooassign 原則透過 REST API、 PowerShell 或 Azure CLI，請參閱[指派及管理透過指令碼的原則](../../azure-resource-manager/resource-manager-policy-create-assign.md)。
* 如簡介 tooresource 原則，請參閱[資源原則概觀](../../azure-resource-manager/resource-manager-policy.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](../../azure-resource-manager/resource-manager-subscription-governance.md)。
