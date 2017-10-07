---
title: "Azure RemoteApp 中 Outlook aaaUsing |Microsoft 文件"
description: "深入了解如何 tooconfigure 和 Azure RemoteApp 中使用的 Outlook |Microsoft Azure"
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>在 Azure RemoteApp 中使用 Microsoft Outlook
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 支援 Microsoft Outlook O365。 深入了解 [Office 在 Azure RemoteApp 中運作](remoteapp-officesubscription.md)的方式。 在 Azure RemoteApp 中使用 Outlook 時，有幾個建議的設定。

## <a name="cached-mode"></a>快取模式
在 Azure RemoteApp 中使用 Outlook 時，快取模式是建議的組態。 當您設定 Outlook 2013 帳戶 toouse 快取 Exchange 模式，Outlook 2013 運作方式與 hello 使用者的 Microsoft Exchange 信箱 hello 使用者在電腦上，搭配 hello 離線通訊錄的離線資料檔案 （OST 檔案） 中所儲存的本機複本(OAB)。 hello 快取的信箱和 OAB 會定期更新從 hello O365 服務。 深入了解[hello 快取和線上模式之間的差異](https://technet.microsoft.com/library/jj683103.aspx)。

hello 使用者可以選取**快取 Exchange 模式**或**線上模式**帳戶安裝期間或藉由變更 hello 帳戶設定。 您也可以部署一個模式或其他 hello 使用 hello Office 自訂工具 （10 月） 或群組原則。  

閱讀 [啟用快取模式的逐步指示](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc)。

## <a name="search"></a>搜尋
在 Azure RemoteApp 中，使用 Outlook 中的搜尋有限制。 Azure RemoteApp 使用管理的集區的 Vm tooaccommodate 使用者工作階段。 搜尋索引相依於 hello 機器識別碼不同，不同的 Vm。 很可能在每次使用者登入 Azure RemoteApp，它們會導向的 tooa 新的 VM。 這表示，每次 hello 機器 ID 就會變更 （當 hello 使用者在不同的 VM 上），如果我們啟用當地搜尋，會執行 hello 索引子。 根據 hello hello 大小。OST 檔案 hello 索引子可能需要很長的時間 toocomplete，並使用資源所需的其他應用程式。 搜尋不只很慢，而且可能不會產生結果。 使用線上模式帳戶設定檔會解決這個問題，但因為 toohello 缺乏本機快取，則會犧牲整體效能 （請參閱上方連結，如需有關快取和線上模式的 hello 差異 hello）。 不幸的是，在 Outlook 2013 中無法停用已編製索引/本機搜尋，且預設無法啟用線上搜尋。

