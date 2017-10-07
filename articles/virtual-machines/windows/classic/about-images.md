---
title: "aaaAbout 映像的 Windows 虛擬機器 |Microsoft 文件"
description: "了解如何將映像與 Azure 中的 Windows 虛擬機器搭配使用。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>關於 Windows 虛擬機器的映像
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 如需尋找與 hello 資源管理員模型中使用映像相關資訊，請參閱[這裡](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>使用映像

您可以使用 hello Azure PowerShell 模組和 hello Azure 入口網站 toomanage hello 映像可用 tooyour Azure 訂用帳戶。 hello Azure PowerShell 模組可提供更多的命令選項，以便您查出到底是什麼 toosee 或執行。 hello Azure 入口網站提供的 GUI 許多 hello 日常系統管理工作。

以下是一些使用 hello Azure PowerShell 模組的範例。

* **取得所有映像**:`Get-AzureVMImage`傳回所有可用在您目前的訂用帳戶中的 hello 映像的清單： 您的映像和 Azure 或協力廠商所提供。 hello 產生清單可能是大。 hello 下一個範例顯示如何 tooget 較短的清單。
* **取得映像系列**：`Get-AzureVMImage | select ImageFamily`顯示字串 **ImageFamily** 屬性以取得映像系列清單。
* **取得特定系列中的所有映像**：`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **尋找 VM 映像**:`Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName`這個指令程式的運作方式是篩選 hello DataDiskConfiguration 屬性只適用於 tooVM 映像。 此範例也會篩選 hello 輸出 tooonly hello 標籤和映像名稱。
* **儲存一般化映像**：`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **儲存特殊化映像**：`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > hello OSState 參數是必要的 toocreate VM 映像，其中包含 hello 作業系統磁碟，並連接資料磁碟。 如果您不使用 hello 參數，hello cmdlet 會建立 OS 映像。 hello hello 參數值會指出 hello 映像為一般化或特殊化，根據 hello 作業系統磁碟是否已準備好要重複使用。

* **删除映像**：`Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>後續步驟
您也可以[建立一部使用 hello Azure 入口網站的 Windows 電腦](tutorial.md)。
