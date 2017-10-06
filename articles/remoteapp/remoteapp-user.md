---
title: "aaaAdd 使用者 tooyour Azure RemoteApp 集合 |Microsoft 文件"
description: "深入了解如何 tooadd 使用者 tooyour Azure RemoteApp 集合"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>如何 tooadd 使用者 tooyour Azure RemoteApp 集合
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

您的使用者可以看到並使用 Azure RemoteApp 中的應用程式之前，您會有 toogrant 它們 tooyour 集合的存取。 這是 hello 簡單的部分： hello 上**使用者存取**索引標籤上，輸入 hello hello 使用者的帳戶資訊，然後按一下hello 核取記號。

您需要什麼帳戶資訊？ 相依於 hello 集合型別所建立 （雲端或混合式） 以及您使用 Office 365 ProPlus 該集合中。

## <a name="supported-user-identities"></a>支援的使用者識別
hello 不同集合類型 （與混合式雲端） 支援存取 tooapplications 使用不同的使用者識別。  

RemoteApp 的混合式集合，您需要 Active Directory 網域基礎結構，在內部部署以及與目錄整合 Azure Active Directory 租用戶 tooset （以及選擇性地單一登入）。 此外，您需要 toocreate hello 在內部部署目錄中的某些 Active Directory 物件。  

雲端的 RemoteApp 集合，只要使用者擁有 Azure Active Directory 支援身分識別可以授與使用者存取 tooRemoteApp tooinclude Microsoft 帳戶。  請參閱 hello 表。

Office 365 使用者為 Azure Active Directory 使用者。 如果這些使用者有 Azure Active Directory 混合式、目錄同步處理的帳戶，就可以在 RemoteApp 混合式部署中授與他們使用者存取權。   

您可以使用此表格識別支援在您的集合和 hello Active Directory 需求為何，快速參考。

| 使用者帳戶 | 雲端 | 混合式 |
| --- | --- | --- |
| Microsoft 帳戶 |是 |否 |
| Azure Active Directory (Azure AD) | | |
| 僅 Azure AD 雲端 |是 |否 |
| 具有密碼同步的 ADsync |是 |是 |
| 不具密碼同步的 ADsync |是 |否 |
| 具 AD FS 的 ADsync |是 |是 |
| [Azure 支援的第 3 方識別提供者](https://msdn.microsoft.com/library/azure/jj679342.aspx) (例如 Ping) |是 |是 |
| Multi-Factor Authentication |是 |是 |

請查看有關設定 RemoteApp 的 Active Directory 的 [詳細資訊](remoteapp-ad.md) 。

> [!NOTE]
> hello Azure Active Directory 使用者必須是來自與您訂用帳戶相關聯的 hello 租用戶。 (您可以檢視並修改您的訂閱上 hello**設定**hello 入口網站中的索引標籤。 請參閱[變更由 RemoteApp 所使用的 hello Azure Active Directory 租用](remoteapp-changetenant.md)如需詳細資訊。)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Office 365 ProPlus 使用者帳戶資訊
如果您使用 Office 365 ProPlus 範本映像 hello 集合中*或*如果您建立使用 Office 365 的自訂映像，您只允許有 Office 365 訂用帳戶的 hello 的 tooadd Azure Active Directory 使用者您的訂用帳戶的預設網域。 如需詳細資訊，請參閱 [透過 Azure RemoteApp 使用 Office 365](remoteapp-o365.md) 。

