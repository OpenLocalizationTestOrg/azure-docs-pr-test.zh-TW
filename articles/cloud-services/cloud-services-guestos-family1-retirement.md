---
title: "請注意 aaaGuest OS 系列 1 淘汰 |Microsoft 文件"
description: "提供下列相關資訊以及 hello Azure 客體作業系統系列 1 淘汰發生時如何 toodetermine 如果影響"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a>客體作業系統系列 1 淘汰通知
2013 年 6 月 1 日首次宣佈淘汰作業系統系列 1 hello。

**2014 年 9 月 2 日**hello Azure 客體作業系統 (客體 OS) 系列 1.x 以 hello Windows Server 2008 作業系統為基礎，正式淘汰。 所有嘗試 toodeploy 新服務或升級現有的服務使用系列 1 已淘汰客體 OS 系列 1 的錯誤訊息通知您該 hello 將會都失敗。

**2014 年 11 月 3 日** 客體 OS 系列 1 的延伸支援已結束，並且已完全淘汰。 所有仍以系列 1 為基礎的服務都將受到影響。 我們可能會隨時停止這些服務。 沒有保證您的服務將繼續 toorun，除非您自行手動升級它們。

如果您有其他問題，請瀏覽 hello[雲端服務論壇](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc)或[連絡 Azure 支援](https://azure.microsoft.com/support/options/)。

## <a name="are-you-affected"></a>您受到影響了嗎？
您的雲端服務會受到影響，如果 hello 下列任何一個適用於：

1. 值為"osFamily ="1"為您的雲端服務 hello ServiceConfiguration.cscfg 檔案中明確指定。
2. 您沒有為您的雲端服務 hello ServiceConfiguration.cscfg 檔案中明確指定的 osFamily 的值。 目前，hello 系統會在此情況下使用 hello 預設值為"1"。
3. hello Azure 入口網站列出的客體作業系統系列值為"Windows Server 2008"。

toofind 正在執行哪個作業系統系列的雲端服務，您可以執行下列指令碼在 Azure PowerShell 中的 hello，但您必須[設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)第一次。 如需有關 hello 指令碼的詳細資訊，請參閱[Azure 客體 OS 系列 1 生命週期結束： 2014 年 6 月](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx)。

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

您的雲端服務將受到作業系統系列 1 淘汰如果 hello 指令碼輸出中的 hello osFamily 資料行是空的或包含"1"。

## <a name="recommendations-if-you-are-affected"></a>受影響時的建議
我們建議您移轉您的 hello 支援的客體作業系統系列的雲端服務角色 tooone:

**客體 OS 系列 4.x** - Windows Server 2012 R2 *(建議選項)*

1. 請確認您的應用程式使用 SDK 2.1 或更新版本，搭配 .NET Framework 4.0、4.5 或 4.5.1。
2. 設定 hello osFamily 屬性太"4 的 「 在 hello ServiceConfiguration.cscfg 檔案，並重新部署雲端服務。

**客體 OS 系列 3.x** - Windows Server 2012

1. 請確認您的應用程式使用 SDK 1.8 或更新版本，搭配 .NET Framework 4.0 或 4.5。
2. 設定 hello osFamily 屬性太"3 的"中的 hello ServiceConfiguration.cscfg 檔案，並重新部署雲端服務。

**客體 OS 系列 2.x** - Windows Server 2008 R2

1. 請確認您的應用程式使用 SDK 1.3 和更新版本，搭配 .NET Framework 3.5 或 4.0。
2. 設定 hello osFamily 屬性太"2 的"中的 hello ServiceConfiguration.cscfg 檔案，並重新部署雲端服務。

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>客體作業系統系列 1 的延長支援已在 2014 年 11 月 3 日結束。
以客體作業系統系列 1 為基礎的雲端服務將不再受到支援。 速移轉系列 1 儘速可能 tooavoid 服務中斷。  

## <a name="next-steps"></a>後續步驟
最新檢閱 hello[客體 OS 版本](cloud-services-guestos-update-matrix.md)。
