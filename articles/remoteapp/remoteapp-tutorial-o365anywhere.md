---
title: "在任何具有 Azure RemoteApp 的裝置上取得相同的 Office 365 體驗 | Microsoft Docs"
description: "了解如何使用 Azure RemoteApp 與使用者共用任何 Office 365 應用程式。"
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 584c781c97097cda3c1455ade05cba8659f11073
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>在任何具有 Azure RemoteApp 的裝置上取得相同的 Office 365 體驗
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

本文涵蓋如何在公司的任何裝置上部署 Office 365。 您的使用者可以在 Android、Apple 和 Windows 上取得相同的功能和 UI 體驗。

在 Azure 中使用者可連接的可調整虛擬機器上裝載 Office 365，即可使用 Azure RemoteApp 完成這項作業。 這組虛擬機器稱為「雲端收藏」。

## <a name="create-a-cloud-collection"></a>建立雲端收藏
首先，建立 Azure 帳戶之後，請按一下左側的連結，以瀏覽至 **RemoteApp** 。
![在 Azure 入口網站上顯示 Azure RemoteApp](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

然後，按一下底部的 [ **新增** ] 並「快速建立」收藏，以繼續進行。 提供所提供的名稱、區域、訂用帳戶、計畫和映像 "Office Proffesional 2013"。
![建立對話方塊](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

完成表單之後，應該會啟動集合建立程序。 這可能需要一個小時左右。

![等候](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

完成程序之後，結果會與以下範例類似。 如果按一下 [發佈]  ，可以看到已發佈大部分的 Office 應用程式。
![已建立集合](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![已發佈的應用程式](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

此時，按一下 [使用者存取] ，也可以加入可存取此收藏的更多使用者。
![設定使用者存取](./media/remoteapp-tutorial-o365anywhere/6-user.png)

現在讓我們嘗試連接至 Office 365！

## <a name="connect-to-office-365"></a>連接至 Office 365
我們將會前往 [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/)，向下捲動並按一下 [下載用戶端]，以在您所在的裝置上安裝 Azure RemoteApp 用戶端。 下面的螢幕擷取畫面適用於 Windows。

啟動應用程式之後，系統會要求您使用 Microsoft 帳戶 (先前稱為 Live ID) 登入，請現在使用相同的 Live ID 做為您的 Azure 帳戶。 登入時，您應該會看到有關新邀請的通知，而按一下該處，您應該會看到與下面類似的清單。 請接受符合您 Azure 帳戶擁有者電子郵件的邀請。

![新的邀請](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

它看起來就像有新的邀請。

![接受應用程式](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

接受邀請之後，應該會看到 Azure RemoteApp 用戶端中的所有 Office 應用程式。

![應用程式清單](./media/remoteapp-tutorial-o365anywhere/9-work.png)

按一下其中任何一項時，應該會在 Azure 虛擬機器上啟動應用程式，而您應該已完成所有設定！ 盡情享受！

![啟動](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

