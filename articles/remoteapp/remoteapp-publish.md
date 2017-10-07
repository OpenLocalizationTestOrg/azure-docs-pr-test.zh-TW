---
title: "aaaPublish Azure RemoteApp 中的應用程式 |Microsoft 文件"
description: "深入了解如何 toopublish 應用程式與 Azure RemoteApp 中的資源。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>如何 toopublish RemoteApp 應用程式
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

建立您的 RemoteApp 集合之後，您需要 toopublish hello 應用程式或您為您的使用者想 toomake 可用資源。 hello 與您的訂用帳戶所提供的範本映像只能有少數應用程式發佈的預設值-tooshare hello 其他應用程式，您就需要 toopublish 它們。

> [!NOTE]
> 您需要 tooupdate 應用程式嗎？ 您必須太[更新 hello 影像](remoteapp-update.md)第一次。
> 
> 

在 hello**發行**hello 入口網站中索引標籤上，按一下 **發行**。 您可以從您的範本映像加入應用程式**啟動**功能表或提供 hello 路徑 toowhere hello 應用程式安裝在 hello 範本映像上。 如果您選擇 tooadd hello**啟動**功能表上，從 hello 清單中選擇 hello 應用程式 toopublish。 如果您選擇 tooprovide hello 路徑 toohello 應用程式，輸入 hello 和 hello 路徑 toohello app 的名稱。 使用 hello path-例如，"%systemdrive%"中的變數，而不是"c:\"。

> [!NOTE]
> 如果您想 tooadd hello 應用程式**啟動**功能表上，您需要 toohave*加入該應用程式 toohello**啟動**範本映像上的功能表。* 否則，RemoteApp 只會看到什麼*是*hello 上**啟動**功能表上，而且您會產生混淆。 
> 
> toomake 確定您的應用程式處於 hello**啟動**功能表上，將快顯檔案- **.lnk** -hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs 資料夾內。
> 
> 如果您忘記 tooadd hello 應用程式 toohello**啟動**功能表建立 hello 範本時選擇 tooadd hello 路徑 toohello 應用程式。 (或者重新建立您的範本映像，但是這會比較費工。)
> 
> 

