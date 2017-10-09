---
title: "aaaRun Azure RemoteApp 使用任何裝置上的所有 Windows 應用程式 |Microsoft 文件"
description: "深入了解如何 tooshare 與您的使用者使用 Azure RemoteApp 的所有 Windows 應用程式。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 961d40ca-9673-4977-aa54-d6b22fc61ce1
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 750f3b881e0cb671ff6e8f3e851bccdf2262d156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-any-windows-app-on-any-device-with-azure-remoteapp"></a>使用 Azure RemoteApp 在任何裝置上執行任何 Windows 應用程式
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

只要使用 Azure RemoteApp，您可以在任何裝置的任何位置立即執行 Windows 應用程式。 無論是 10 年前的自訂應用程式或 Office 應用程式，您的使用者不再需要繫結 toobe tooa 特定作業系統 （例如 Windows XP) 針對幾個應用程式。

使用 Azure RemoteApp，您的使用者也可以使用他們自己的 Android 或 Apple 的裝置，以及如何取得 hello 了在 Windows 上 （或在 Windows Phone） 相同的體驗。 完成方式是在 Azure 的 Windows 虛擬機器集合中裝載 Windows 應用程式，而您的使用者可以從具有網際網路連線的任何地方進行存取。 

閱讀並了解的範例完全如何 toodo 這。

在本文中，我們會 tooshare 存取與所有使用者。 不過，您可以使用任何應用程式。 只要您可以在 Windows Server 2012 R2 電腦上安裝應用程式，您可以使用下列步驟執行 hello 共用。 您可以檢閱 hello[應用程式需求](remoteapp-appreqs.md)toomake 確定您的應用程式運作。

請注意，因為存取是資料庫，而且我們想要該資料庫 toobe 很有用，我們會進行一些額外的步驟 toolet 使用者存取 hello 存取資料共用。 如果您的應用程式不是資料庫，或您不需要您的使用者 toobe 無法 tooaccess 檔案共用，您可以略過這些步驟在本教學課程

> [!NOTE]
> <a name="note"></a>您需要 Azure 帳戶 toocomplete 本教學課程：
> 
> * 您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)： 取得信用額度您可以使用 tootry 出支付 Azure 服務，而且即使他們用於之後您可以在最多保留 hello 帳戶，並使用免費的 Azure 服務，例如網站。 永遠不會將向您的信用卡，除非您明確地變更您的設定，並詢問 toobe 收費。
> * 您可以 [啟用 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)- 您的 MSDN 訂用帳戶每月會提供您額度，您可以用在 Azure 付費服務。
> 
> 

## <a name="create-a-collection-in-remoteapp"></a>在 RemoteApp 中建立集合
由建立集合開始。 hello 集合做為您的應用程式和使用者的容器。 每個集合都是根據映像，而您可以建立專屬映像或使用訂用帳戶所提供的映像。 此教學課程中，我們會使用 hello Office 2013 試用版映像-它包含我們想要 tooshare hello 應用程式。

1. 在 hello Azure 入口網站，向下捲動 hello 左側瀏覽樹狀目錄中直到您看到 RemoteApp。 開啟該頁面。
2. 按一下 [ **建立 RemoteApp 集合**]。
3. 按一下 [ **快速建立** ]，然後輸入集合的名稱。
4. 選取您想要 toouse toocreate 您集合 hello 地區。 Hello 達到最佳體驗效果，選取 在地理上最接近的 hello 地區 toohello 位置，您的使用者存取 hello 應用程式的位置。 例如，在本教學課程中，將位於 hello 使用者中 Redmond，Washington。 hello 最接近的 Azure 區域**美國西部**。
5. 選取您想要 toouse hello 計費方案。 hello 基本計費方案放置 16 使用者大型的 Azure VM，而 hello 標準的計費方案大型的 Azure VM 上有 10 個使用者。 如同一般的範例，hello 基本方案運作方式很適合用於處理資料的項目類型工作流程。 產能應用程式中，像是 Office，您會想 hello 標準方案。
6. 最後，選取 hello Office 2013 Professional 映像。 此映像包含 Office 2013 應用程式。 提醒您，此映像僅適合試用版的集合和 POC。 您無法在生產集合中使用此映像。
7. 現在，按一下 [ **建立 RemoteApp 集合**]。

![在 RemoteApp 中建立雲端集合](./media/remoteapp-anyapp/ra-anyappcreatecollection.png)

這會開始建立您的集合，但它可能會佔用 tooan 小時。

現在您正在準備 tooadd 您的使用者。

## <a name="share-hello-app-with-users"></a>與使用者共用 hello 應用程式
一旦已成功建立您的集合，它會是時間 toopublish 存取 toousers，以及加入 hello 的使用者存取 tooit。

如果您導覽離開 hello Azure RemoteApp 節點建立 hello 集合時，，啟動藉由從 hello Azure 首頁回 tooit 好。

1. 按一下 其他選項建立舊版 tooaccess hello 集合，並設定 hello 集合。
   ![新的 RemoteApp 雲端集合](./media/remoteapp-anyapp/ra-anyappcollection.png)
2. 在 hello**發行**索引標籤上，按一下 **發行**底端 hello 囉 」 畫面，然後按一下**發佈開始功能表程式**。
   ![發佈 RemoteApp 程式](./media/remoteapp-anyapp/ra-anyapppublish.png)
3. 選取您想要從 hello 清單 toopublish hello 應用程式。 基於我們的目的，我們已選擇 [Access]。 按一下頁面底部的 [新增] 。 等候 hello 應用程式 toofinish 發行。
   ![在 RemoteApp 中發佈 Access](./media/remoteapp-anyapp/ra-anyapppublishaccess.png)
4. 一旦 hello 應用程式已完成發行，前端透過 toohello**使用者存取**索引標籤上的 tooadd 所有 hello 使用者需要存取 tooyour 應用程式。 輸入您使用者的使用者名稱 (電子郵件地址)，然後按一下儲存 。

![新增使用者 tooRemoteApp](./media/remoteapp-anyapp/ra-anyappaddusers.png)

1. 現在，它是時間 tootell 您有關這些新的應用程式的使用者以及 tooaccess 它們。 toodo，指向它們 toohello 遠端桌面用戶端下載 URL 的電子郵件傳送給使用者。
   ![RemoteApp hello 用戶端下載 URL](./media/remoteapp-anyapp/ra-anyappurl.png)

## <a name="configure-access-tooaccess"></a>設定存取 tooAccess
部分應用程式在透過 RemoteApp 部署之後，需要進行額外的設定。 特別是，存取，我們進行 toocreate 任何使用者可以存取在 Azure 的檔案共用。 (如果您不想 toodo，您可以建立[混合式集合](remoteapp-create-hybrid-deployment.md)[而不是雲端集合]，可讓您的使用者存取檔案與本機網路上的資訊。)然後，我們需要 tootell 我們使用者 toomap 其電腦 toohello Azure 檔案系統上的本機磁碟機。

您以 hello 系統管理員身分 hello 的第一個部分。 然後，是您的使用者執行的一些步驟。

1. 從開始發佈 hello 命令列介面 (cmd.exe)。 在 hello**發行**索引標籤上，選取**cmd**，然後按一下**發行 > 使用路徑發行程式**。
2. 輸入 hello hello 應用程式和 hello 路徑名稱。 基於我們的目的，使用 「 檔案總管 」 做為 hello 名稱"%systemdrive%\windows\explorer.exe"作為 hello 路徑。
   ![發行 hello cmd.exe 檔案。](./media/remoteapp-anyapp/ra-publishcmd.png)
3. 現在您需要 toocreate Azure[儲存體帳戶](../storage/common/storage-create-storage-account.md)。 我們名為我們"accessstorage，"因此挑選 tooyou 有意義的名稱。 (toomisquote Highlander，可以有只有一個 「 accessstorage"。)![我們的 Azure 儲存體帳戶](./media/remoteapp-anyapp/ra-anyappazurestorage.png)
4. 現在，請回到 tooyour 儀表板，您可以取得 hello 路徑 tooyour 儲存空間 （端點位置）。 您將經常用到它，因此請確定在某個位置複製它。
   ![hello 儲存體帳戶的路徑](./media/remoteapp-anyapp/ra-anyappstoragelocation.png)
5. 接下來，一旦建立 hello 儲存體帳戶之後，您會需要 hello 主要存取金鑰。 按一下**管理存取金鑰**，，然後複製 hello 主要存取金鑰。
6. 現在，設定 hello hello 儲存體帳戶的內容，並建立新的檔案共用的存取。 執行下列 cmdlet 提高權限的 Windows PowerShell 視窗中的 hello:
   
        $ctx=New-AzureStorageContext <account name> <account key>
        $s = New-AzureStorageShare <share name> -Context $ctx
   
    因此我們的共用，這些是我們執行 hello cmdlet:
   
        $ctx=New-AzureStorageContext accessstorage <key>
        $s = New-AzureStorageShare <share name> -Context $ctx

現在，它的 hello 使用者開啟。 首先，讓您的使用者安裝 [RemoteApp 用戶端](remoteapp-clients.md)。 接下來，hello 使用者需要的 toomap 從其帳戶 toothat Azure 檔案的磁碟機共用您所建立，並加入其存取的檔案。 這是他們執行的作業：

1. 在 hello RemoteApp 用戶端，存取 hello 已發佈應用程式。 啟動 hello cmd.exe 程式。
2. 執行下列命令 toomap hello 磁碟機從您的電腦 toohello 檔案共用：
   
        net use z: \\<accountname>.file.core.windows.net\<share name> /u:<user name> <account key>
   
    如果您設定 hello **/ 持續性**參數 tooyes hello 對應磁碟機將會保存在工作階段之間。
3. 現在，啟動 RemoteApp hello 檔案總管 中應用程式。 複製任何您想 toouse hello 共用應用程式 toohello 檔案共用的存取檔案。
   ![將 Access 檔案放在 Azure 共用中](./media/remoteapp-anyapp/ra-anyappuseraccess.png)
4. 最後，開啟存取，及您共用的 hello 資料庫。 您應該會看到您在執行從 hello 雲端存取的資料。
   ![從 hello 雲端執行的實際存取資料庫](./media/remoteapp-anyapp/ra-anyapprunningaccess.png)

現在，您可以在任何裝置上使用 Access - 只要確定您安裝 RemoteApp 用戶端。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
現在，您已經熟悉如何建立集合，請嘗試建立 [使用 Office 365 的集合](remoteapp-tutorial-o365anywhere.md)。 或者，您可以建立可存取區域網路的 [混合式集合 ](remoteapp-create-hybrid-deployment.md)。

<!--Image references-->

