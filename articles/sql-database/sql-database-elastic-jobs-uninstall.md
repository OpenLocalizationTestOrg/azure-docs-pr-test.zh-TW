---
title: "aaaHow toouninstall 彈性資料庫工作的工具"
description: "如何 toouninstall hello 彈性資料庫工作的工具"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a>解除安裝彈性資料庫工作元件
**彈性資料庫工作**可以解除安裝元件使用 hello 入口網站或 PowerShell。

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>解除安裝使用 hello Azure 入口網站的彈性資料庫工作元件
1. 開啟 hello [Azure 入口網站](https://portal.azure.com/)。
2. 瀏覽 toohello 訂用帳戶包含**彈性資料庫工作**元件，也就是 hello 的彈性資料庫工作元件已安裝的訂用帳戶。
3. 按一下 [瀏覽]，然後按一下 [資源群組]。
4. 名為"__ElasticDatabaseJob"hello 選取資源群組。
5. 刪除 hello 資源群組。

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>使用 PowerShell 解除安裝彈性資料庫作業元件
1. 啟動 Microsoft Azure PowerShell 命令視窗並瀏覽 toohello 工具子資料夾下的目錄 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x： 型別**cd 工具**。
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools
2. 執行 hello.\UninstallElasticDatabaseJobs.ps1 PowerShell 指令碼。
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1

只要，執行下列指令碼，假設預設的 hello 或 hello 元件的安裝上使用的值：

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a>後續步驟
toore 安裝彈性資料庫作業，請參閱[安裝 hello 彈性資料庫工作服務](sql-database-elastic-jobs-service-installation.md)

如需彈性資料庫工作的概觀，請參閱 [彈性資料庫工作概觀](sql-database-elastic-jobs-overview.md)。

<!--Image references-->


