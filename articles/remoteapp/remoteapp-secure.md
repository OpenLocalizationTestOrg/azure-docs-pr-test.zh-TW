---
title: "aaaSecure 應用程式與 Azure RemoteApp 中的資源 |Microsoft 文件"
description: "深入了解如何 toolock 向應用程式與 Azure RemoteApp 中的資源"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>保護 Azure RemoteApp 中的應用程式和資源
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 可讓使用者存取 toocentrally 管理 Windows 應用程式，可讓您控制哪些使用者可以和無法執行的動作。  Hello 使用者連接來自未受管理的裝置 （例如其個人 Macbook) 和您想 toocontrol hello 使用者存取權，或是體驗時，這是特別有用。

例如，如果您使用 Active Directory 進行使用者驗證，而且您希望 tooprevent 複製應用程式中的資料使用者，您可以設定遠端桌面群組原則 tooblock 使用者從複製資料。

另一個範例是如果您想在特定應用程式的 tooblock 網際網路存取集合中。 您可以建立區塊 hello 存取，當您建立集合的 hello 映像的 Windows 防火牆規則。

## <a name="implementation-options"></a>實作選項
  以下是 hello 金鑰實作選項可以個別使用或一起視：

1. 如果您的 RemoteApp 集合已加入網域您可以強制執行任何[群組原則](https://technet.microsoft.com/library/cc725828.aspx)(hello 例外狀況的 hello 閒置和中斷連線逾時所述的原則與[這裡](../azure-subscription-service-limits.md))。
2. 作為替代 tooGroup 原則 （如果您的集合不是已加入網域，或您沒有在 AD 中 hello 正確權限），您可以設定[本機原則](https://technet.microsoft.com/library/cc775702.aspx)到您的範本映像。  請注意，當群組原則與本機原則發生衝突時，以群組原則為準。
3. 某些 OS/應用程式設定不是可透過原則設定，但是可以透過使用 hello 的登錄機碼[RegEdit 工具](remoteapp-hybridtrouble.md)設定您的範本映像時。
4. 您可以使用[Windows 防火牆](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish)toocontrol 網路存取 tooand 從 hello hello 應用程式執行所在的電腦。 只要確定您未封鎖 hello Url 和此處定義的連接埠。
5. 您可以使用[AppLocker](https://technet.microsoft.com/library/hh831440.aspx) toocontrol 可執行應用程式和檔案的使用者。 例如，知識的使用者可以找出如何 toorun 應用程式未發佈，但可用於 hello 映像您使用 toocreate hello 集合-AppLocker 可以封鎖了這項。

## <a name="detailed-information"></a>詳細資訊
* hello 下列 RDS 原則是可能 toobe 最有用：
  * [裝置及資源重新導向](https://technet.microsoft.com/library/ee791794.aspx)
  * [印表機重新導向](https://technet.microsoft.com/library/ee791784.aspx)
  * [設定檔](https://technet.microsoft.com/library/ee791865.aspx)。
* 請注意，透過設定重新導向 hello RemoteApp PowerShell 模組 (見[這裡](remoteapp-redirection.md)) 依賴 hello 用戶端機器 tooenforce hello 原則，因此如果安全性 hello 主要目標，您會想透過 tooenforce hello 原則hello 範本映像的本機原則或透過群組原則。
* [Windows Server 2012 R2 原則](https://technet.microsoft.com/library/hh831791.aspx)。
* [Office 2013 原則](https://technet.microsoft.com/library/cc178969.aspx)(包括[toocustomize 如何 hello Office 工具列](https://technet.microsoft.com/library/cc179143.aspx))。

