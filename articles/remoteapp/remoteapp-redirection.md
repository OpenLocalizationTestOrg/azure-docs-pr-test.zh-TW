---
title: "在 Azure RemoteApp 中的 aaaUsing 重新導向 |Microsoft 文件"
description: "深入了解如何 tooconfigure 並用 RemoteApp 中的重新導向"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>在 Azure RemoteApp 中使用重新導向
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

裝置重新導向，可讓您與使用 hello 裝置附加的 tootheir 本機電腦、 電話或平板電腦的遠端應用程式互動的使用者。 比方說，如果您有提供透過 Azure RemoteApp 的 Skype，您的使用者必須安裝在與 Skype 其 PC toowork hello 相機。 印表機、麥克風、監視器以及各種不同以 USB 連接的周邊裝置也是如此。

RemoteApp 會利用 hello 遠端桌面通訊協定 (RDP) 和 RemoteFX tooprovide 重新導向。

## <a name="what-redirection-is-enabled-by-default"></a>依預設會何種重新導向功能？
當您使用 RemoteApp 時，預設會啟用 hello 遵循重新導向。 在括號中的 hello 資訊會顯示 hello RDP 設定。

* Hello 本機電腦上播放音效 (**這部電腦上播放**)。 (audiomode:i:0)
* 擷取從 hello 本機電腦，並傳送 toohello 遠端電腦的音訊 (**從這部電腦錄製**)。 (audiocapturemode:i:1)
* 列印 toolocal 印表機 (redirectprinters:i:1)
* COM 連接埠 (redirectcomports:i:1)
* 智慧卡裝置 (redirectsmartcards:i:1)
* 剪貼簿 （能力 toocopy 和貼上） (redirectclipboard:i:1)
* 清除字型平滑處理 (允許字型平滑處理:i:1)
* 重新導向所有支援的隨插即用裝置。 (devicestoredirect:s:*)

## <a name="what-other-redirection-is-available"></a>還有其他哪些重新導向功能？
預設會停用兩個重新導向選項：

* 磁碟機重新導向 （磁碟機對應）： 本機電腦的磁碟機變成 hello 遠端工作階段中的對應磁碟機。 這可讓您儲存或開啟的檔案從本機磁碟機 hello 遠端工作階段中工作時。
* USB 重新導向： 您可以使用 hello 遠端工作階段中的 hello USB 裝置連接的 tooyour 本機電腦。

## <a name="change-your-redirection-settings-in-remoteapp"></a>在 RemoteApp 中變更重新導向設定
您可以使用 hello Microsoft Azure PowerShell sdk 變更 hello 裝置重新導向設定集合。 您安裝之後 hello 新 PowerShell 及 SDK，請先設定您的訂閱中所述的 toomanage[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

接著，使用下列 tooset hello 自訂 RDP 屬性命令類似 toohello:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(請注意，  *`n* 做為個別的屬性之間的分隔符號。)

tooget 何種自訂 RDP 屬性的設定，執行下列 cmdlet 的 hello 的清單。 請注意，只能自訂屬性會顯示為輸出結果，並且不 hello 預設屬性：  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

當您設定自訂屬性，您必須指定所有自訂屬性每個時間;否則 hello 設定會還原 toodisabled。   

### <a name="common-examples"></a>常見範例
使用下列 cmdlet tooenable 磁碟機重新導向的 hello:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

使用這個指令程式 tooenable USB 和磁碟機重新導向：

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

使用這個指令程式 toodisable 剪貼簿共用：  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> 要確定 toocompletely 登出 hello 集合中的所有使用者 （和不只是將它們中斷連線） 測試 hello 變更之前。 tooensure 使用者會完全登出，請移 toohello**工作階段**hello Azure 入口網站中的 hello 集合中索引標籤，然後中斷連接或登入任何使用者登出。 有時可能要花幾秒鐘 hello 本機磁碟機 tooshow 在 [總管] 內 hello 工作階段。
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>變更 Windows 用戶端的 USB 重新導向設定
如果您想 toouse 連線 tooRemoteApp 的電腦上的 USB 重新導向，皆有 2 需要 toohappen 的動作。 1-您的系統管理員必須使用 Azure PowerShell 的 tooenable hello 集合層級的 USB 重新導向。 2-每個在裝置上您想要 toouse USB 重新導向，您需要 tooenable 的群組原則，允許它。 此步驟需要 toobe 完成每個使用者，想 toouse USB 重新導向。

> [!NOTE]
> 只支援 Windows 電腦使用 Azure RemoteApp 提供 USB 重新導向。
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>啟用 hello RemoteApp 集合的 USB 重新導向
使用下列 cmdlet tooenable USB 重新導向 hello 集合層級的 hello:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>啟用 hello 用戶端電腦的 USB 重新導向
在您的電腦上的 tooconfigure USB 重新導向設定：

1. 開啟 hello 本機群組原則編輯器 (GPEDIT。MSC)。 (從命令提示字元中執行 gpedit.msc)。
2. 開啟 [電腦設定]\[原則]\[系統管理範本]\[Windows 元件]\[遠端桌面服務]\[遠端桌面連線用戶端]\[RemoteFX USB 裝置重新導向]。
3. 按兩下 [允許 RDP 重新導向這部電腦中其他支援的 RemoteFX USB 裝置] 。
4. 選取**啟用**，然後選取**系統管理員和使用者在 hello RemoteFX USB 重新導向的存取權限**。
5. 以系統管理權限，開啟命令提示字元，然後執行下列命令的 hello:
   
        gpupdate /force
6. Hello 電腦重新啟動。

您也可以使用 hello 群組原則管理工具 toocreate 及 hello 所有電腦的 USB 重新導向原則套用在網域中：

1. Hello 網域系統管理員身分登入 hello 網域控制站。
2. 開啟 hello 群組原則管理主控台。 (按一下 [開始] > [系統管理工具] > [群組員則管理]。)
3. 瀏覽 toohello 網域或組織單位，您會想 toocreate hello 原則。
4. 以滑鼠右鍵按一下 預設網域原則，然後按一下編輯。
5. 開啟 [電腦設定]\[原則]\[系統管理範本]\[Windows 元件]\[遠端桌面服務]\[遠端桌面連線用戶端]\[RemoteFX USB 裝置重新導向]。
6. 按兩下 [允許 RDP 重新導向這部電腦中其他支援的 RemoteFX USB 裝置] 。
7. 選取**啟用**，然後選取**系統管理員和使用者在 hello RemoteFX USB 重新導向的存取權限**。
8. 按一下 [確定] 。  

