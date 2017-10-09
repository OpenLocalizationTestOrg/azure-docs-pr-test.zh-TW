---
title: "aaaHow 導向 Azure RemoteApp 中的 USB 裝置嗎？ | Microsoft Docs"
description: "深入了解如何在 Azure RemoteApp 中的 USB 裝置的 toouse 重新導向。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>如何在 Azure RemoteApp 中重新導向 QuickBooks？
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

裝置重新導向可以讓使用者使用 Azure RemoteApp 中的 hello 應用程式中的 hello USB 裝置連接的 tootheir 電腦或平板電腦。 例如，如果您已共用 Skype 透過 Azure RemoteApp，您的使用者需要 toobe 無法 toouse 其裝置相機。

您在進一步討論前，請確定您讀取中的 hello USB 重新導向資訊[使用 Azure RemoteApp 中的重新導向](remoteapp-redirection.md)。 不過 hello 建議 nusbdevicestoredirect:s: * 無法用於 USB 網路攝影機和部分 USB 印表機或 USB multifunctional 裝置可能無法運作。 根據設計，並基於安全性理由，hello Azure RemoteApp 管理員有 tooenable 重新導向裝置類別 GUID 或裝置執行個體識別碼之前，您的使用者可以使用這些裝置。

雖然這篇文章討論有關 web 數位相機重新導向，您可以使用類似的方法 tooredirect USB 印表機和其他 USB multifunctional 裝置不會重新導向的 hello **nusbdevicestoredirect:s:*** 命令。

## <a name="redirection-options-for-usb-devices"></a>USB 裝置的重新導向選項
Azure RemoteApp 使用非常類似的機制，將 USB 裝置重新導向，當 hello 可用的遠端桌面服務。 hello 基礎技術可讓您選擇 hello 正確重新導向方法指定的裝置，最佳的高層級 tooget hello 和使用 hello 的 RemoteFX USB 裝置重新導向**usbdevicestoredirect:s:**命令。 有四個項目 toothis 命令：

| 處理順序 | 參數 | 說明 |
| --- | --- | --- |
| 1 |* |選取高層級重新導向未挑選的所有裝置。 附註：根據設計，* 不適用於 USB 網路攝影機。 |
| {Device class GUID} |選取 所有裝置都符合指定的 hello 裝置安裝類別。 | |
| USB\InstanceID |選取指定的給定執行個體識別碼 hello 的 USB 裝置 | |
| 2 |-USB\Instance ID |移除 hello hello 指定裝置的重新導向設定。 |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>將 USB 裝置重新導向使用 hello 裝置類別 GUID
有兩種方式 toofind hello 裝置類別 GUID，可用於重新導向。 

hello 第一個選項是 toouse hello [System-Defined 裝置安裝類別可以使用 tooVendors](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx)。 挑選最能符合 hello 裝置附加的 toohello 本機電腦的 hello 類別。 若為數位相機，這可能是 [影像裝置] 類別或 [視訊擷取裝置] 類別。 您將需要 toodo 某些實驗 hello 裝置類別 toofind hello 正確類別可搭配本機 hello GUID 附加 （在我們的案例 hello 網路攝影機） 的 USB 裝置。

更好的方法或 hello 第二個選項，是 toofollow 這些步驟 toofind hello 特定裝置類別 GUID:

1. 開啟裝置管理員 hello，找出 hello 裝置會被重新導向，以滑鼠右鍵按一下，並開啟 hello 屬性。
   ![開啟裝置管理員 hello](./media/remoteapp-usbredir/ra-devicemanager.png)
2. 在 hello**詳細資料**索引標籤上，選擇 hello 屬性**類別 Guid**。 會顯示 hello 值為 hello 為該類型的裝置類別 GUID。
   ![攝影機屬性](./media/remoteapp-usbredir/ra-classguid.png)
3. 使用 hello 類別 Guid 值 tooredirect 裝置加以比對。

例如：

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

您可以結合多個裝置重新導向 hello 中的相同的 cmdlet。 例如： tooredirect 本機儲存體和 USB web 相機，指令程式看起來像這樣：

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

當您將裝置重新導向設定由類別 GUID 符合類別 GUID hello 中的指定的集合的所有裝置重新都導向。 例如，如果沒有 hello 區域網路上的多部電腦具有 hello 相同 USB 網路攝影機，您可以執行單一 cmdlet tooredirect 所有 hello 網路攝影機。

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>將 USB 裝置重新導向使用 hello 裝置執行個體識別碼
如果您想要更細微的控制，而且想 toocontrol 每一裝置的重新導向，您可以使用 hello **USB\InstanceID**重新導向參數。

hello 最困難的部分，這個方法尋找 hello USB 裝置執行個體識別碼。 您需要存取 toohello 電腦與 hello 特定 USB 裝置。 接著，遵循下列步驟：

1. 中所述，啟用遠端桌面工作階段中的 hello 裝置重新導向[如何使用我的裝置和資源的遠端桌面工作階段中？](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. 開啟遠端桌面連線，然後按一下 [顯示選項] 。
3. 按一下**存**toosave hello 目前連線的設定 tooan RDP 檔。  
    ![將 hello 設定儲存為 RDP 檔案](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. 選擇 檔案名稱和位置，例如 MyConnection.rdp 和此 PC\Documents，並儲存 hello 檔案。
5. 開啟 hello MyConnection.rdp 檔案使用文字編輯器，並尋找 hello 執行個體識別碼的裝置 hello 想 tooredirect。

現在，在下列指令程式的 hello 使用 hello 執行個體識別碼：

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>幫我們來協助您
您知道在加法 toorating 這份文件並進行註解下下方，讓您可以變更 toohello 文章本身嗎？ 有所遺漏？ 有所錯誤？ 我是否撰寫了令人混淆的內容？ 向上捲動，然後按一下  **GitHub 上編輯**toomake 變更-這些是 toous 供檢閱，並接著，我們登入它們，就會看到您的變更與改進這裡。

