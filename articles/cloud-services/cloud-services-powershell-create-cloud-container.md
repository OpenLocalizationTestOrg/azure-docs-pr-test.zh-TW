---
title: "使用 PowerShell 的雲端服務容器 aaaCreate |Microsoft 文件"
description: "本文說明如何 toocreate 雲端服務使用 PowerShell 的容器。 hello 容器會裝載 web 和背景工作角色。"
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>使用 Azure PowerShell 命令 toocreate 空的雲端服務容器
本文說明如何 tooquickly 建立雲端服務容器，使用 Azure PowerShell cmdlet。 請遵循下列步驟 hello:

1. 安裝 hello Microsoft Azure PowerShell cmdlet 從 hello [Azure PowerShell 下載](http://aka.ms/webpi-azps)頁面。
2. 開啟 hello PowerShell 命令提示字元。
3. 使用 hello [Add-azureaccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign 中的。

   > [!NOTE]
   > 如需有關安裝 hello Azure PowerShell cmdlet 及連線 tooyour Azure 訂用帳戶的進一步指示，請參閱太[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
   >
   >
4. 使用 hello**新 AzureService** cmdlet toocreate 空白的 Azure 雲端服務容器。

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. 請依照這個範例 tooinvoke hello 指令程式：

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

如需有關建立 hello Azure 雲端服務的詳細資訊，請執行：

```
Get-help New-AzureService
```

### <a name="next-steps"></a>後續步驟
* toomanage hello 雲端服務部署，請參閱 toohello [Get-azureservice](https://msdn.microsoft.com/library/azure/dn495131.aspx)，[移除 AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx)，和[組 AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx)命令。 您也可能是指太[tooconfigure 雲端服務的方式](cloud-services-how-to-configure.md)以取得詳細資訊。
* toopublish 您的雲端服務專案 tooAzure，請參閱 toohello **PublishCloudService.ps1**中的程式碼範例[在 Azure 雲端服務的持續傳遞](cloud-services-dotnet-continuous-delivery.md)。
