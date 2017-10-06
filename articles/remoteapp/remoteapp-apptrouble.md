---
title: "aaaAzure 疑難排解 RemoteApp-應用程式啟動和連線失敗 |Microsoft 文件"
description: "了解如何 tootroubleshoot 問題的啟動及連線 tooapplications Azure RemoteApp 中。"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>為 Azure RemoteApp 進行疑難排解 - 應用程式啟動和連線失敗
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

裝載於 Azure RemoteApp 中的應用程式可能失敗 toolaunch 的幾個不同的原因。 本文說明各種原因和使用者時可能會收到錯誤訊息嘗試 toolaunch 應用程式。 文章中也會討論連線失敗。 （但此發行項登入 hello Azure RemoteApp 用戶端時不會說明問題）。  

讀取上常見的錯誤訊息，因為 tooapp 啟動和連線失敗的相關資訊。

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>我們正在引導您設定...請在 10 分鐘內再試一次。
此錯誤表示 Azure RemoteApp 向上 toomeet hello 容量需求的使用者。 Hello 背景中多個 Azure RemoteApp VM 執行個體正在建立使用者 toohandle hello 容量需求。 通常這會佔用大約五分鐘，但可能會佔用 too10 分鐘。 有時候此工作完成速度不夠快，但是資源的需求卻是立即性的。 例如，許多使用者會需要 toouse 您的應用程式在 Azure RemoteAppn hello 的上午 9 點案例相同的時間。 如果發生這種情況 tooyou 我們可以啟用**容量模式**上 hello 後端。 toodo 此開啟 Azure 支援票證。 為特定 tooinclude hello 要求在您訂用帳戶 ID。  

![我們正在引導您設定](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>無法不自動重新連線 tooyour 應用程式，請重新啟動您的應用程式
如果您使用 Azure RemoteApp，然後放入您的電腦 toosleep 超過 4 小時並再喚醒您的電腦 hello Azure RemoteApp 用戶端嘗試 tooauto 重新連線且已超過逾時，通常會看到此錯誤訊息。  指示使用者 toonavigate 後 toohello 應用程式，並嘗試 tooopen 從 hello Azure RemoteApp 用戶端。

![無法不自動重新連線 tooyour 應用程式](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>Hello 暫存設定檔的問題
您的使用者設定檔 （使用者設定檔磁碟） 無法 toomount 和 hello 使用者收到暫存設定檔時，就會發生此錯誤。  系統管理員應該瀏覽 toohello hello Azure 入口網站中的集合，並前往 toohello**工作階段**索引標籤，然後嘗試過**登出**hello 使用者。 這會強制完整開 hello 使用者工作階段的記錄，然後再次具有 hello 使用者嘗試 toolaunch 應用程式。 如果失敗，請連絡 Azure 支援服務。

## <a name="azure-remoteapp-has-stopped-working"></a>Azure RemoteApp 已停止運作
這則錯誤訊息表示 hello Azure RemoteApp 用戶端有問題，而且需要 toobe 重新啟動。 指示使用者 tooclose： 選取**關閉程式**，然後再次啟動 hello Azure RemoteApp 用戶端。  如果 hello 問題仍繼續開啟與 Azure 支援票證。

![Azure RemoteApp 已停止運作](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>「遠端桌面連線」存取此資源時發生錯誤。 重試 hello 連線或連絡您的系統管理員
這是一般錯誤訊息 - 請連絡 Azure 支援服務，以便我們進行調查。 

![一般 Azure RemoteApp 訊息](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

