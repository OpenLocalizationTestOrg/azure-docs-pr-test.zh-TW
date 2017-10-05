---
title: "在 Azure RemoteApp 中發佈 App | Microsoft Docs"
description: "了解如何在 Azure RemoteApp 中發佈應用程式和資源。"
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
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a>如何在 RemoteApp 中發佈應用程式
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

建立 RemoteApp 收藏之後，您必須發佈想供使用者使用的應用程式或資源。 隨您的訂閱提供的範本映像預設只會發佈幾個應用程式，若要共用其他應用程式，您必須發佈它們。

> [!NOTE]
> 您需要更新應用程式嗎？ 您將需要先 [更新映像](remoteapp-update.md) 。
> 
> 

在入口網站的 [發佈] 索引標籤中，按一下 [發佈]。 您可以從您範本映像的 [ **開始** ] 功能表新增應用程式，或是在範本映像提供安裝程式的路徑。 如果您選擇從 [開始]  功能表新增，請從清單中選擇要發佈的 App。 如果您選擇提供應用程式的路徑，請輸入應用程式的名稱和應用程式路徑。 請在路徑中使用變數，例如 "%systemdrive%" 而非 "c:\"。

> [!NOTE]
> 如果您想要從 [開始] 功能表新增您的應用程式，就必須先「在您的範本映像上將該應用程式新增至 [開始] 功能表」。 否則，RemoteApp 只會看到在 [開始] 功能表上的項目，而您會覺得很困惑。 
> 
> 若要確定您的 App 位於 [開始] 功能表，請將捷徑檔案 (**.lnk**) 置於 %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs 資料夾內。
> 
> 如果您忘記在建立範本時將應用程式新增到 [開始] 功能表，請選擇新增路徑到應用程式。 (或者重新建立您的範本映像，但是這會比較費工。)
> 
> 

