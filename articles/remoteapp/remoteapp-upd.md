---
title: "aaaHow 未儲存使用者資料和設定的 Azure RemoteApp 嗎？ | Microsoft Docs"
description: "了解 Azure RemoteApp 將使用者資料使用 hello 使用者設定檔磁碟的儲存。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Azure RemoteApp 如何儲存使用者資料和設定？
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 跨越裝置和工作階段儲存使用者身分識別和自訂。 此使用者資料會依每個使用者和每個集合磁碟 (也稱為使用者設定檔磁碟 (UPD)) 儲存。 hello 磁碟遵循 hello 使用者，並確保 hello 使用者有一致的經驗，不論他們登入的位置。

使用者設定檔磁碟是完全透明 toohello 使用者-使用者儲存文件 tootheir 文件 資料夾 （在看似 toobe 本機磁碟機） 和變更他們的應用程式設定，如往常般。 在 hello 相同連接 tooAzure RemoteApp 從任何裝置時，保存階段，所有個人設定。 所有的 hello 使用者看見他們 hello 中的資料相同的位置。

每個 UPD 有 50GB 的永續性儲存體，並包含使用者資料和應用程式設定。 

請閱讀更多有關使用者設定檔資料的特殊資訊。

> [!NOTE]
> 需要 toodisable hello UPD 嗎？ 現在您可以那麼做了 - 詳細資料請查看 Pavithra 的部落格文章： [在 Azure RemoteApp 停用使用者設定檔磁碟 (UPD)](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/)(英文)。
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a>系統管理員如何取得 toohello 資料？
如果您針對您的使用者 （適用於嚴重損壞修復，或如果 hello 使用者離職後 hello 公司） 的其中一個需要 tooaccess hello 資料，請連絡 Azure 支援人員並提供 hello 訂用帳戶資訊 hello 集合和 hello 使用者識別。 hello Azure RemoteApp 小組提供 URL toohello VHD。 請下載該 VHD，並擷取您需要的任何文件或檔案。 請注意該 hello VHD 50 GB，因此將會花費元 toodownload 它。

## <a name="is-hello-data-backed-up"></a>Hello 資料備份嗎？
是，我們會儲存每個地理位置的 hello 使用者資料的備份。 hello 資料是唯讀的而且可以是存取 hello 相同方式與將 hello 一般資料 (請連絡 Azure RemoteApp tooget 它)，如果 hello 主要資料中心已關閉。 hello 資料複製即時 toohello 備份位置，以及我們不要保留不同版本的複本。 因此，資料損毀，我們不會無法 toorestore 它先前已知良好的版本，但是如果 hello 主要資料中心已關機，您將會從能夠 tooget 使用者資料的 tooa hello 其他位置。

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a>如何使用者看見 hello UPD hello 伺服器端上？
每個使用者會有自己的目錄對應 tootheir UPD hello 伺服器上： c:\Users\username。

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a>什麼是最佳方式 toouse hello Outlook 和 UPD？
Azure RemoteApp 儲存工作階段之間的 hello Outlook 狀態 （信箱，Pst）。 tooenable，我們需要 hello PST toobe 儲存在 hello 使用者設定檔資料 (c:\users\<使用者名稱 >)。 這是 hello hello 資料，因此只要您不要變更 hello 位置的預設位置，hello 資料將會保存工作階段之間。

我們也建議您在 Outlook 中使用「快取」模式，並使用「伺服器/線上」模式進行搜尋。

如需使用 Outlook 和 Azure RemoteApp 的詳細資訊，請查看 [這篇文章](remoteapp-outlook.md) 。

## <a name="what-about-redirection"></a>重新導向呢？
您可以設定 toolet 使用者來存取本機裝置設定的 Azure RemoteApp[重新導向](remoteapp-redirection.md)。 本機裝置，如此便能 tooaccess hello UPD hello 資料。

## <a name="can-i-use-my-upd-as-a-network-share"></a>我可以使用 UPD 做為網路共用嗎？
不用。 UPD 不能做為網路共用。 UPD 是只使用 toohello 時使用者 hello 使用者主動連接 tooAzure RemoteApp。

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>如果我從集合中刪除使用者，其 UPD 是否也會刪除?
否，當您刪除使用者，我們不會自動刪除 hello UPD-相反地，我們會將儲存 hello 資料直到您刪除 hello 集合。 90 天後刪除 hello 集合中，我們會刪除所有 Upd。 

如果您需要 toodelete UPD 集合中，請連絡 Azure RemoteApp-我們可以從我們這邊刪除 UPD。

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>我可以存取使用者的 UPD (目前或已刪除的使用者) 嗎？
是，如果您連絡[Azure RemoteApp](mailto:remoteappforum@microsoft.com)，我們可以設定您具有 URL tooaccess hello 資料。 您將有 10 小時 toodownload 有關任何資料或檔案從 hello UPD hello 存取到期之前。

## <a name="are-upds-available-offline"></a>UPD 可離線使用嗎？
現在我們不提供離線存取 tooUPDs，除了上面所述的 hello 10 個小時存取視窗的權限。 這表示，我們目前沒有與您的時間夠長，toocomplete 更複雜的工作，像是 hello Upd 上執行防毒軟體或存取的稽核資料存取方式 tooprovide。

## <a name="do-registry-key-settings-persist"></a>登錄機碼設定可以保存嗎？
是，撰寫 tooHKEY_Current_User 的任何項目是 hello UPD 的一部分。

## <a name="can-i-disable-upds-for-a-collection"></a>我可以停用 集合的 UPD 嗎？
是，您可以要求 Azure RemoteApp toodisable Upd 訂用帳戶，但是您無法自行。 這表示 Upd 將停用 hello 訂用帳戶中的所有集合。

您可能想 toodisable Upd 任何 hello 下列情況： 

* 您需要使用者資料的完整存取權限和控制 (針對稽核和檢閱之目的，例如金融機構)。
* 您已將 3rd 合作對象使用者設定檔管理解決方案的內部，而且想 toocontinue 已加入網域的 Azure RemoteApp 部署中使用它們。 這會需要 hello 設定檔的代理程式 toobe 載入 hello 黃金映像。 
* 您不需要任何本機資料存放區，或您擁有 hello 雲端或檔案共用中的所有資料，而且想要 toocontrol 儲存在本機使用 Azure RemoteApp 的資料。

如需詳細資訊，請參閱[在 Azure RemoteApp 停用使用者設定檔磁碟 (UPD)](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) (英文)。

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a>可以限制使用者無法儲存資料 toohello 系統磁碟機嗎？
是，但您仍需要 tooset 設定中的 hello 範本映像建立 hello 集合之前。 使用下列步驟 tooblock 存取 toohello 系統磁碟機的 hello:

1. 執行**gpedit.msc** hello 範本映像上。
2. 瀏覽過**使用者組態 > 系統管理範本 > Windows 元件 > 總管**。
3. 選取下列選項的 hello:
   * **隱藏 [我的電腦] 中這些指定的磁碟機**
   * **防止從我的電腦存取 toodrives**

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a>我可以植入 UPD 嗎？ 我想的 tooput hello 是第一個階段 hello 使用者可用的 hello 的 UPD 中的部分資料登入。
是，當您建立 hello 範本映像，您可以加入 toohello 預設設定檔資訊。 這項資訊接著會加入 toohello UPD。

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a>我可以變更 hello UPD hello 大小視資料量而定，我想 toostore 嗎？
否，所有 UPD 都有 50GB 的儲存體。 如果您想 toostore 不同的資料量，請嘗試下列 hello:

1. 停用 Upd hello 集合。
2. 設定使用者 tooaccess 的檔案共用。
3. 使用啟動指令碼的負載 hello 檔案共用。 如需 Azure RemoteApp 中啟動指令碼的詳細資訊，請參閱下列內容。
4. 直接使用者 toosave 所有資料 toohello 檔案共用。

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>如何在 Azure RemoteApp 中執行啟動指令碼？
如果您想 toorun 啟動指令碼時，開始您藉由在 hello 範本映像建立排定的工作將 toouse hello 集合。 (請在執行 sysprep「前」這麼做。) 

![建立系統工作](./media/remoteapp-upd/upd1.png)

![建立可在使用者登入時執行的系統工作](./media/remoteapp-upd/upd2.png)

在 [hello**一般**索引標籤上，確定 toochange hello**使用者帳戶**安全性] 之下太"BUILTIN\Users。 」

![變更 hello 使用者帳戶 tooa 群組](./media/remoteapp-upd/upd4.png)

hello 排定的工作將會啟動啟動指令碼，使用 hello 使用者的認證。 排程 hello 工作 toorun 每次使用者登入。

![設定為 在登入 」 的 hello 工作的 hello 觸發程序](./media/remoteapp-upd/upd3.png)

您也可以使用 [群組原則式啟動指令碼](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx)。 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a>如何將啟動指令碼置於 hello 開始功能表？ 可行嗎？
換句話說，建立.bat 檔案，執行組態視窗指令碼並將它儲存 toohello c:\ProgramData\Microsoft\Windows\Start 登錄資料夾，和後，每當使用者啟動 RemoteApp 工作階段時執行該指令碼？

否，不支援使用 Azure RemoteApp，會使用 RDSH，也不支援啟動指令碼中的 hello [開始] 功能表。

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a>可以使用 mstsc.exe （hello 遠端桌面程式） tooconfigure 登入指令碼嗎？
不行，Azure RemoteApp 不支援。

## <a name="can-i-store-data-on-hello-vm-locally"></a>可以在 hello VM 在本機上儲存資料？
否，儲存在 hello UPD 中的 hello 以外的 VM 上的資料將會遺失。 沒有高機率 hello 使用者不會收到 hello 相同 VM hello 他們登入 Azure RemoteApp 的下一次。 我們不會維護使用者 VM 持續性，因此 hello 使用者將無法登入 hello 相同的 VM 與 hello 資料將遺失。 此外，當我們更新 hello 集合，以一組新的 Vm-這表示任何 hello VM 本身上儲存的資料取代現有的 Vm 的 hello 會遺失。 hello 建議 toostore hello UPD，就像 Azure 檔案，檔案伺服器的內部 VNET，或使用 DropBox 等雲端儲存體系統 hello 雲端上的共用存放裝置中的資料。

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>如何使用 PowerShell 在 VM 上掛接 Azure File 共用?
您可以使用 hello Net PSDrive cmdlet toomount hello 磁碟機，如下所示：

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


您也可以藉由執行 hello 下列儲存您的認證：

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


可讓您略過 hello-Credential 參數 hello New-psdrive cmdlet 中的。

