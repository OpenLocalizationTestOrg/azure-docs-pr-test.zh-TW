---
title: "將使用者新增至您的 Azure RemoteApp 集合 | Microsoft Docs"
description: "了解如何將使用者新增至您的 Azure RemoteApp 集合"
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
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a>如何將使用者新增至您的 Azure RemoteApp 集合
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

您必須先授與使用者您集合的存取權，他們才能在 Azure RemoteApp 中看到和使用您的應用程式。 這是最簡單的部分：在 [ **使用者存取** ] 索引標籤上，輸入使用者的帳戶資訊，然後按一下核取記號。

您需要什麼帳戶資訊？ 這取決於您建立的收藏類型 (雲端或混合式)，還有您是否正在該收藏中使用 Office 365 ProPlus。

## <a name="supported-user-identities"></a>支援的使用者識別
不同的集合類型 (雲端或混合式) 支援使用不同的使用者身分識別，存取應用程式。  

對於 RemoteApp 的混合式收藏，您必須設定內部部署的 Active Directory 網域基礎結構和具備目錄整合的 Azure Active Directory 租用戶 (及選擇性的單一登入)。 此外，您必須在內部部署的目錄中建立一些 Active Directory 物件。  

對於 RemoteApp 的雲端收藏，具有 Azure Active Directory 支援識別的任何使用者都可以被授與 RemoteApp 的使用者存取權以包含 Microsoft 帳戶。  請參閱下表。

Office 365 使用者為 Azure Active Directory 使用者。 如果這些使用者有 Azure Active Directory 混合式、目錄同步處理的帳戶，就可以在 RemoteApp 混合式部署中授與他們使用者存取權。   

您可以使用這個表格快速參考在您的收藏中支援何種識別，以及 Active Directory 的需求為何。

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
> Azure Active Directory 使用者必須來自於與您的訂用帳戶相關聯的租用戶。 (您可以在入口網站的 [設定] 索引標籤上檢視和修改您的訂用帳戶。 如需詳細資訊，請參閱[變更 RemoteApp 所使用的 Azure Active Directory 租用戶](remoteapp-changetenant.md))。
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Office 365 ProPlus 使用者帳戶資訊
如果您的收藏中使用 Office 365 ProPlus 範本映像， *或者* 如果您建立了使用 Office 365 的自訂映像，則您只能新增在您的訂用帳戶的預設網域中擁有 Office 365 訂閱的 Azure Active Directory 使用者。 如需詳細資訊，請參閱 [透過 Azure RemoteApp 使用 Office 365](remoteapp-o365.md) 。

