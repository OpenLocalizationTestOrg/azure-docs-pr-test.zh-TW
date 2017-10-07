---
title: "aaaAzure RemoteApp 授權 |Microsoft 文件"
description: "了解 Azure RemoteApp 中的授權如何運作。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>Azure RemoteApp 中的授權如何運作？
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

因此您設定您的 Azure RemoteApp 服務，建立您的範本，並準備好 toopublish 應用程式 tooyour 使用者。 但仍有一個出的最後一件事 toofigure： 授權。 只要如何運作授權 RemoteApp 和您共用透過 RemoteApp hello 應用程式？

RemoteApp 不需要任何 Windows 授權或遠端桌面 CAL。 Hello 本身 RemoteApp 端會負責您訂用帳戶。 (簽出 hello 詳細資料的 hello[定價方案](https://azure.microsoft.com/pricing/details/remoteapp)。)

如果您使用其中一個包含您的訂用帳戶中的 hello 映像，您可以將該映像上安裝而不需要個別授權的 hello 應用任何的程式共用。 例如，如果您使用 hello Windows Server 2012 R2 範本映像 toobuild 您的集合，您就可以與您的使用者共用 System Center Endpoint Protection。 hello 例外狀況 toothis 規則是 Office 365 ProPlus，這需要不同的訂用帳戶，以及 Office 2013，不能共用生產階段前集合中。

如果您想 toouse hello Office 365 範本映像隨附 RemoteApp，您必須擁有*現有*Office 365 ProPlus 計劃。 hello 也適用於您發佈的資料使用的自訂範本的任何 Office 365 應用程式。 您需要 tooactivate hello 應用程式與您的訂用帳戶。 無論試用版或付費訂用帳戶都是如此。 如果您想 toouse hello Office 365 範本映像 hello 試用期間*您還沒有訂用帳戶和*，移至 Office 365 toohello 頁面太[註冊](https://go.microsoft.com/fwlink/p/?LinkID=403802)試用訂用帳戶。 如需詳細資訊，請參閱 [RemoteApp 與 Office 如何共同運作？](remoteapp-o365.md) 。

如果在 hello 試用期間，您不想 tooget Office 365 試用訂閱，使用 hello Office 2013 Professional Plus 的範本映像隨附 RemoteApp。 此範本映像只能使用 30 天，而且無法轉換成付費收藏。

對於其他應用程式，您需要 toomake 確定您已擁有 hello 授權 tooshare hello 應用程式。

這很合理，對吧？ 您可以發佈任何應用程式，您有遵循和法令資格 tooshare。 而且您需要確定您真的是 toomake 標題 tooshare 為您的程式。

請注意，您不能在雲端收藏中使用 CAL 或大量授權合約。 您*可以*混合式集合 （除了 Office) 中使用大量授權合約 tooactivate 應用程式。 您只需要的 tooinstall 它們在您的範本映像從 hello 大量授權的媒體。 請依照 hello 資訊 hello 應用程式廠商 tooinstall 授權遠端桌面環境中執行。

