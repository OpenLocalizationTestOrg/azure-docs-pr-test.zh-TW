---
title: "Azure RemoteApp 如何儲存使用者資料和設定？ | Microsoft Docs"
description: "了解 Azure RemoteApp 如何使用使用者設定檔磁碟來儲存使用者資料。"
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
ms.openlocfilehash: 4993bf507536659d7951e1552559cf0a6061d345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Azure RemoteApp 如何儲存使用者資料和設定？
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

Azure RemoteApp 跨越裝置和工作階段儲存使用者身分識別和自訂。 此使用者資料會依每個使用者和每個集合磁碟 (也稱為使用者設定檔磁碟 (UPD)) 儲存。 不論使用者登入的位置為何，此磁碟都會追蹤使用者並確保使用者擁有一致的經驗。

對使用者而言，使用者設定檔磁碟是完全透明的 — 使用者會將文件儲存至其 Documents 資料夾 (似乎是本機磁碟機) 並如往常般變更其應用程式設定。 同時，從任何裝置連線到 Azure RemoteApp 時會保存所有的個人設定。 使用者會在相同的位置看到其資料。

每個 UPD 有 50GB 的永續性儲存體，並包含使用者資料和應用程式設定。 

請閱讀更多有關使用者設定檔資料的特殊資訊。

> [!NOTE]
> 必須停用 UPD 嗎？ 現在您可以那麼做了 - 詳細資料請查看 Pavithra 的部落格文章： [在 Azure RemoteApp 停用使用者設定檔磁碟 (UPD)](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/)(英文)。
> 
> 

## <a name="how-can-an-admin-get-to-the-data"></a>系統管理員如何取得資料？
如果您需要存取您其中一個使用者的資料 (為了災害復原或如果使用者離開公司)，請連絡 Azure 支援服務並提供集合和使用者身分識別的訂用帳戶資訊。 Azure RemoteApp 小組會為您提供 VHD 的 URL。 請下載該 VHD，並擷取您需要的任何文件或檔案。 請注意，VHD 為 50 GB，因此下載需要一些時間。

## <a name="is-the-data-backed-up"></a>已備份資料嗎？
是，我們依據每個地理位置儲存使用者資料的備份。 如果主要資料中心已關閉，則資料是唯讀的並可用與存取一般資料相同的方式存取 (連絡 Azure RemoteApp 以取得)。 資料會即時複製到備份位置，而且我們不需要保留不同版本的複本。 因此，在資料損毀的情況下，我們不能將它還原到上次已知正確的版本，但如果主要資料中心不能使用時，您將能夠從其他位置取得使用者資料。

## <a name="how-do-users-see-the-upd-on-the-server-side"></a>使用者如何在伺服器端查看 UPD？
每位使用者在伺服器上都有對應至其 UPD 的專屬目錄：c:\Users\username。

## <a name="whats-the-best-way-to-use-outlook-and-upd"></a>使用 Outlook 和 UPD 的最佳方式為何？
Azure RemoteApp 會儲存工作階段間的 Outlook 狀態 (信箱、PST)。 若要啟用此功能，我們需要將 PST 儲存在使用者設定檔資料 (c:\users\<username>) 中。 這是資料的預設位置，只要您不變更位置，資料將會在工作階段之間保存。

我們也建議您在 Outlook 中使用「快取」模式，並使用「伺服器/線上」模式進行搜尋。

如需使用 Outlook 和 Azure RemoteApp 的詳細資訊，請查看 [這篇文章](remoteapp-outlook.md) 。

## <a name="what-about-redirection"></a>重新導向呢？
您可以設定 Azure RemoteApp，讓使用者藉由設定 [重新導向](remoteapp-redirection.md)來存取本機裝置。 然後本機裝置即可存取 UPD 上的資料。

## <a name="can-i-use-my-upd-as-a-network-share"></a>我可以使用 UPD 做為網路共用嗎？
不用。 UPD 不能做為網路共用。 UPD 僅適用於使用者主動連線到 Azure RemoteApp 時。

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>如果我從集合中刪除使用者，其 UPD 是否也會刪除?
否，當您刪除使用者時，我們不會自動刪除 UPD - 相反地，我們會儲存資料，直到您刪除集合為止。 刪除集合後 90 天，我們才會刪除所有 UPD。 

如果您需要從集合中刪除 UPD，請連絡 Azure RemoteApp - 我們可以從我們這端刪除 UPD。

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>我可以存取使用者的 UPD (目前或已刪除的使用者) 嗎？
可以，如果您連絡 [Azure RemoteApp](mailto:remoteappforum@microsoft.com)，我們可以為您設定一個 URL 以存取資料。 在存取到期前，您將有大約 10 小時的時間可從 UPD 下載任何資料或檔案。

## <a name="are-upds-available-offline"></a>UPD 可離線使用嗎？
除了上述 10 小時的存取時段以外，我們現在並不提供 UPD 的離線存取。 這表示我們目前沒辦法讓您長時間存取以完成更複雜的工作，像是在 UPD 上執行防毒軟體或存取資料進行稽核。

## <a name="do-registry-key-settings-persist"></a>登錄機碼設定可以保存嗎？
可以，寫入 HKEY_Current_User 的任何項目都是 UPD 的一部分。

## <a name="can-i-disable-upds-for-a-collection"></a>我可以停用 集合的 UPD 嗎？
可以，您可以要求 Azure RemoteApp 停用訂用帳戶的 UPD，但無法自己執行該作業。 這表示將會針對訂用帳戶中的所有集合停用 UPD。

遇到下列情況時，建議您停用 UPD： 

* 您需要使用者資料的完整存取權限和控制 (針對稽核和檢閱之目的，例如金融機構)。
* 您有內部部署的第三方使用者設定檔管理解決方案，並想要加入網域的 Azure RemoteApp 部署繼續使用它們。 這會需要將設定檔代理程式載入主要映像。 
* 您不需要任何本機資料儲存空間，或者您的所有資料都在雲端或檔案共用，並且想要使用 Azure RemoteApp 控制在本機的檔案儲存。

如需詳細資訊，請參閱[在 Azure RemoteApp 停用使用者設定檔磁碟 (UPD)](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) (英文)。

## <a name="can-i-restrict-users-from-saving-data-to-the-system-drive"></a>我可以限制使用者不要將資料儲存到系統磁碟機嗎？
可以，但您必須在建立集合之前，在範本映像中加以設定。 使用下列步驟來封鎖系統磁碟機的存取：

1. 在範本映像上執行 **gpedit.msc** 。
2. 瀏覽至 [使用者設定] > [系統管理範本] > [Windows 元件] > [Explorer]。
3. 選取下列選項：
   * **隱藏 [我的電腦] 中這些指定的磁碟機**
   * **防止從 [我的電腦] 存取磁碟機**

## <a name="can-i-seed-upds-i-want-to-put-some-data-in-the-upd-thats-available-the-first-time-the-user-signs-in"></a>我可以植入 UPD 嗎？ 我想要在使用者第一次登入時可用的 UPD 中放入一些資料。
是，當您建立範本映像時，您可以將資訊加入至預設設定檔。 這項資訊會接著加入至 UPD。

## <a name="can-i-change-the-size-of-the-upd-depending-on-how-much-data-i-want-to-store"></a>我可以根據想要儲存的資料量來變更 UPD 的大小嗎？
否，所有 UPD 都有 50GB 的儲存體。 如果您想要儲存不同的資料量，請嘗試下列方法：

1. 停用集合的 UPD。
2. 設定檔案共用以供使用者存取。
3. 使用啟動指令碼來載入檔案共用。 如需 Azure RemoteApp 中啟動指令碼的詳細資訊，請參閱下列內容。
4. 引導使用者將所有資料儲存至檔案共用。

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>如何在 Azure RemoteApp 中執行啟動指令碼？
如果您想要執行啟動指令碼，請從在您即將用於收集的範本映像中建立排定的工作著手。 (請在執行 sysprep「前」這麼做。) 

![建立系統工作](./media/remoteapp-upd/upd1.png)

![建立可在使用者登入時執行的系統工作](./media/remoteapp-upd/upd2.png)

在 [一般] 索引標籤上，務必將 [安全性] 底下的 [使用者帳戶] 變更為 BUILTIN\Users。

![變更使用者帳戶為群組](./media/remoteapp-upd/upd4.png)

排定的工作將會使用使用者的認證，啟動您的啟動指令碼。 將此工作安排在使用者每次登入時執行。

![將工作的觸發程序設定為「登入時」](./media/remoteapp-upd/upd3.png)

您也可以使用 [群組原則式啟動指令碼](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx)。 

## <a name="what-about-placing-a-startup-script-in-the-start-menu-would-that-work"></a>將啟動指令碼置於 [開始] 功能表？ 可行嗎？
換句話說，我可以建立一個可執行 config 視窗指令碼的 .bat 檔並將它儲存至 c:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp 資料夾，然後讓該指令碼在使用者每次啟動 RemoteApp 工作階段時執行嗎？

不行，Azure RemoteApp 不支援，會使用 RDSH，也不支援 [開始] 功能表中的啟動指令碼。

## <a name="can-i-use-mstscexe-the-remote-desktop-program-to-configure-logon-scripts"></a>我可以使用 mstsc.exe (遠端桌面程式) 來設定登入指令碼嗎？
不行，Azure RemoteApp 不支援。

## <a name="can-i-store-data-on-the-vm-locally"></a>可以在 VM 本機儲存資料嗎?
否，資料若不儲存在 UPD 而儲存在 VM 上的任何地方，資料將會遺失。 使用者下次登入 Azure RemoteApp 時不會得到同一 VM 的可能性很高。 我們不會維護「使用者-VM」持續性，因此使用者無法登入相同的 VM，故資料會遺失。 此外，當我們更新集合時，現有 VM 會被一組新的 VM 取代 - 這表示儲存在 VM 本身的所有資料都會遺失。 建議將資料儲存在 UPD、共用儲存體 (如 Azure Files)、VNET 內部的檔案伺服器，或儲存在使用雲端儲存體系統 (如 DropBox) 的雲端上。

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>如何使用 PowerShell 在 VM 上掛接 Azure File 共用?
您可以使用 New-PSDrive Cmdlet 來掛接磁碟機，如下所示︰

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


您也可以執行下列命令儲存您的認證︰

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


這可讓您略過 New-PSDrive Cmdlet 中的 -Credential 參數。

