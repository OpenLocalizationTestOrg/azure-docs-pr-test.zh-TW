---
title: "aaaWhat 處於 hello Azure RemoteApp 範本映像嗎？ | Microsoft Docs"
description: "深入了解 hello 隨附於 Azure RemoteApp 的範本映像。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>什麼是 hello Azure RemoteApp 範本映像中？
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 訂用帳戶包含三個範本映像：

* Windows Server 2012
* Microsoft Office 365 ProPlus (需有 Office 365 訂用帳戶)
* Microsoft Office 2013 Professional Plus (僅限試用版)

> [!IMPORTANT]
> Azure RemoteApp 訂用帳戶會授與存取 toohello hello 映像，但 hello 的例外是 Office 365 ProPlus，這需要不同的訂用帳戶，並不能在生產環境中的 Office 2013 中的軟體。 這表示您可以與您的使用者共用 hello 程式或 hello 範本映像上的應用程式。 例如，如果您建立使用 hello Windows Server 2012 R2 映像的集合，您可以發佈 System Center Endpoint Protection 的使用者透過 RemoteApp 的 tooaccess。
> 
> 簽出 hello[授權詳細資料的 RemoteApp](remoteapp-licensing.md)如需詳細資訊。 和[與 Azure RemoteApp 一起使用的 Office](remoteapp-o365.md) hello Office 授權資訊。
> 
> 

閱讀每個映像包含之內容的詳細資訊。

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 （"hello 香草映像）
此影像以 Microsoft Windows Server 2012 R2 Datacenter 作業系統且已 hello 下列角色和功能安裝 Azure RemoteApp 範本映像的 toomeet hello 需求：

* .NET Framework 4.5、3.5.1、3.5
* 桌面體驗
* 筆跡和手寫服務
* 媒體基礎
* 遠端桌面工作階段主機
* Windows PowerShell 4.0
* Windows PowerShell ISE
* WoW64 支援

這個映像也有下列安裝的應用程式的 hello:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (需有訂用帳戶)
Office 365 是 hello 最要求的應用程式，讓我們的 「 自訂 」 映像為您建立與 toowork。

此映像 hello 香草映像的延伸模組並已 hello 安裝下列元件的 Microsoft Office 365 ProPlus 此外 toohello hello Windows Server 2012 R2 映像中所述的元件：

* Access
* Excel
* Lync
* OneNote
* 商務用 OneDrive （請注意該 hello 同步代理程式不支援與 Azure RemoteApp 搭配使用）
* Outlook
* PowerPoint
* Word
* Microsoft Office 校訂工具

hello 映像也包括 Visio 專業版和專業版的專案。

和下列應用程式，以及 hello:

* SQL 原生用戶端
* ODBC 驅動程式
* SQL Server 資料採礦用戶端
* MasterDataServices 用戶端
* Microsoft Publisher
* PowerQuery
* PowerMap

Office 365 ProPlus 應用程式的完整功能只適用於擁有 Office 365 ProPlus 方案的使用者。 如需有關 hello Office 365 訂用帳戶查看計劃[Office 365 服務計劃](http://technet.microsoft.com/library/office-365-plan-options.aspx)。 還有疑問嗎？ 簽出 hello [Office 365 + RemoteApp](remoteapp-o365.md)資訊。 也請參閱 hello 新發行項，[如何 toouse 您 Office 365 訂用帳戶與 Azure RemoteApp 一起](remoteapp-officesubscription.md)。

請注意，您需要 Office 365 ProPlus toolicense、 Visio 專業版、 和專案 Pro 個別-它們都各自具有自己的授權。

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus (僅限試用版)
Hello 免費試用期間，您可以測試 hello 服務與 hello Office 2013 映像。

此映像 hello 香草映像的延伸模組並已 hello 安裝下列元件的 Microsoft Office 2013 Professional Plus 此外 toohello hello Windows Server 2012 R2 映像中所述的元件：

* Access
* Excel
* Lync
* OneNote
* 商務用 OneDrive （請注意該 hello 同步代理程式不支援與 Azure RemoteApp 搭配使用）
* Outlook
* PowerPoint
* 隨附此逐步解說的專案
* Visio
* Word
* Microsoft Office 校訂工具

> [!IMPORTANT]
> **法律資訊：**此映像不包含 Microsoft Office 授權，且「無法用於生產環境」。 hello Office 2013 Professional Plus 影像是只能用於試用版。 如果您想要實際執行 toouse Azure RemoteApp 中的 Office 應用程式，您會需要 toouse hello Office 365 ProPlus 映像。 如需授權 Office 的詳細資訊，請參閱 [使用 Office 365 與 Azure RemoteApp 搭配](remoteapp-o365.md)
> 
> 

