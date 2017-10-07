---
title: "Azure VM 的 aaaDownload hello 範本 |Microsoft 文件"
description: "下載 hello templatefor VM toohelp 與自動化 hello Resource Manager 部署模型中的部署"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>下載適用於 VM 的 hello 範本
當您在 Azure 中建立 VM 時使用 hello 入口網站或 PowerShell，資源管理員範本會自動為您建立。 您可以使用此範本 tooquickly 重複部署。 hello 範本包含所有資源群組中的 hello 資源的相關資訊。 虛擬機器，這表示 hello 範本包含所有以該資源群組，包括 hello 網路功能資源中的 hello VM 支援建立的項目。

## <a name="download-hello-template-using-hello-portal"></a>下載 hello 範本使用 hello 入口網站
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 一個 hello 中樞功能表中，選取**虛擬機器**。
3. 從 [hello] 清單中選取 hello 虛擬機器。
4. 選取 [自動化指令碼]。
5. 選取**下載**並儲存 hello.zip 檔案 tooyour 本機電腦。
6. 開啟 hello.zip 檔案，並擷取 hello files tooa 資料夾。 hello.zip 檔案會包含：
   
   * deploy.ps1
   * deploy.sh 
   * deployer.rb
   * DeploymentHelper.cs
   * parameters.json
   * template.json

hello 範本 hello template.json 檔案。

## <a name="download-hello-template-using-powershell"></a>下載 hello 範本使用 PowerShell
您也可以下載 hello.json 範本檔案使用 hello[匯出 AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet。 您可以使用 hello`-path`參數 tooprovide hello 檔名和路徑 hello.json 檔案。 這個範例會示範如何 hello 資源群組的 toodownload hello 範本命名**myResourceGroup** toohello **C:\users\public\downloads**在本機電腦上的資料夾。

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解部署資源使用範本，請參閱[資源管理員範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)。

