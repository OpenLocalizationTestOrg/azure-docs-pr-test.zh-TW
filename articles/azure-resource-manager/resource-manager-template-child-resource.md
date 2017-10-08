---
title: "在 Azure 範本 aaaDefine 子資源 |Microsoft 文件"
description: "示範如何 tooset hello 資源類型和 Azure 資源管理員範本中的子資源的名稱"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>在 Resource Manager 範本中設定子資源的名稱和類型
建立範本時，您經常需要 tooinclude 相關的 tooa 父資源的子資源。 例如，您的範本可能包含 SQL Server 和資料庫。 hello SQL server，就是 「 hello 父資源，而且 hello 資料庫 hello 子資源。 

hello hello 子資源類型的格式如下：`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

hello 的 hello 子資源名稱的格式如下：`{parent-resource-name}/{child-resource-name}`

不過，您可以指定 hello 類型和範本中的名稱以不同的方式根據它是否為巢狀方式內 hello 父資源，或它自己在 hello 高層級。 本主題說明如何 toohandle 這兩個方法。

當建構完整的參考 tooa 資源，hello 順序 toocombine 區段從 hello 類型和名稱不是只需串連 hello 兩個。  相反地，在 hello 命名空間之後, 使用一連串的*類型/名稱*最不特定 toomost 特定配對：

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

例如：

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` 為正確 `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` 為不正確

## <a name="nested-child-resource"></a>巢狀子資源
最簡單方式 toodefine hello 子資源是 toonest 在 hello 父資源。 hello 下列範例顯示巢狀內，SQL Server 中的 SQL 資料庫。

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

Hello 子資源，hello 類型設定太`databases`完整資源類型，而`Microsoft.Sql/servers/databases`。 您未提供`Microsoft.Sql/servers/`因為它會假設來自 hello 父資源類型。 hello 子資源名稱設定得`exampledatabase`但 hello 完整名稱包括 hello 父系名稱。 您未提供`exampleserver`因為它會假設從 hello 父資源。

## <a name="top-level-child-resource"></a>最上層的子資源
您可以定義在 hello 上層 hello 子資源。 您可以使用這個方法，如果 hello 父資源未部署在 hello 相同的範本或如果想 toouse `copy` toocreate 子系的多個資源。 使用此方法時，您必須提供 hello 完整資源類型，而且 hello 父資源中包含 hello 子資源名稱。

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

hello 資料庫是子資源 toohello 伺服器，即使它們在 hello hello 範本中相同層級上定義。

## <a name="next-steps"></a>後續步驟
* 如需有關如何建議 toocreate 範本，請參閱[最佳作法來建立 Azure 資源管理員範本](resource-manager-template-best-practices.md)。
* 如需建立多個子資源的範例，請參閱[在 Azure Resource Manager 範本中部署資源的多個執行個體](resource-group-create-multiple.md)。
