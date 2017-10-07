---
title: "aaaSettings 及數據漫遊常見問題集 |Microsoft 文件"
description: "提供有關設定和應用程式資料同步可能答案 toosome 問題 IT 系統管理員。"
services: active-directory
keywords: "企業狀態漫遊設定, windows 雲端, 企業狀態漫遊常見問題集"
documentationcenter: 
author: tanning
manager: swadhwa
editor: curtand
ms.assetid: c0824f5c-129b-4240-969f-921f6a64eae7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4d6d6619b3a5fbd1d274603808d89b73ed942cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="settings-and-data-roaming-faq"></a>設定和資料漫遊常見問題集
本主題將回答 IT 系統管理員可能會遇到的設定和應用程式資料同步處理的一些問題。

## <a name="what-data-roams"></a>哪些資料會漫遊？
**Windows 設定**: hello hello Windows 作業系統內建的電腦設定。 一般而言，這些是個人化您的電腦的設定，且包含 hello 下列三大類別：

* *佈景主題*- 包括桌面主題和工作列設定之類的功能。
* *Internet Explorer 設定*- 包括最近開啟的索引標籤和我的最愛。
* *Edge 瀏覽器設定*- 例如我的最愛和閱讀清單。
* *密碼*- 包括網際網路密碼、Wi-Fi 設定檔等。
* *語言喜好設定*- 包括鍵盤配置、系統語言、日期和時間等的設定。
* *輕鬆存取功能*- 例如高對比佈景主題、朗讀程式及放大鏡。
* *其他 Windows 設定*- 例如命令提示字元設定和應用程式清單。

**應用程式資料**： 通用 Windows 應用程式可以寫入設定資料 tooa 漫遊 資料夾，並自動進行同步處理寫入 toothis 資料夾的任何資料。 是由 toohello 個別的應用程式開發人員 toodesign 這項功能的應用程式 tootake 優點。 如需有關如何 toodevelop 通用 Windows 應用程式使用漫遊，請參閱 hello [appdata 儲存體 API](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx)和 hello[漫遊開發人員部落格的 Windows 8 appdata](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx)。

## <a name="what-account-is-used-for-settings-sync"></a>哪些帳戶用於設定同步處理？
在 Windows 8 和 Windows 8.1 中，設定同步處理一律使用取用者 Microsoft 帳戶。 企業使用者必須 hello 能力 tooconnect Microsoft 帳戶 tootheir Active Directory 網域帳戶 toogain 存取 toosettings 同步處理。在 Windows 10 中，這項連接的 Microsoft 帳戶功能將由主要/次要帳戶架構取代。

hello 帳戶中所使用 toosign tooWindows 定義 hello 主要帳戶。 這可以是 Microsoft 帳戶、Azure Active Directory (Azure AD) 帳戶、內部部署 Active Directory 帳戶或本機帳戶。 加法 toohello 主要帳戶，在 Windows 10 使用者可以加入一個或多個次要雲端帳戶 tootheir 裝置。 次要帳戶通常是 Microsoft 帳戶、Azure AD 帳戶或一些像是 Gmail 或 Facebook 的其他帳戶。 這些次要帳戶提供存取 tooadditional 服務，例如單一登入和 hello Windows 市集，但它們不支援的電源設定同步處理。

在 Windows 10 中，只有 hello 主要帳戶 hello 裝置可用於設定同步處理 (請參閱[如何升級 Windows 10 中的 Windows 8 tooAzure AD 設定同步處理中的 Microsoft 帳戶設定同步處理從？](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10))。

資料永遠不會混之間 hello hello 裝置上的不同的使用者帳戶中。 有兩個設定可用來同步處理設定：

* Windows 設定一律將漫遊與 hello 主要帳戶。
* 應用程式資料會加上 hello 使用帳戶 tooacquire hello 應用程式。 加上 hello 主要帳戶的唯一應用程式會同步。當應用程式是透過 hello Windows 市集或行動裝置管理 (MDM) 側邊載入應用程式擁有權標記決定。

找不到應用程式的擁有者，它將漫遊與 hello 主要帳戶。 如果裝置已從 Windows 8 或 Windows 8.1 tooWindows 10 升級，因為取得 hello Microsoft 帳戶，將會標記 hello 的所有應用程式。 這是因為大部分的使用者取得透過 hello Windows 市集應用程式和 Azure AD 帳戶先前 tooWindows 10 沒有 Windows 市集支援有所。 如果透過離線的授權安裝應用程式，則將 hello 裝置上使用 hello 主要帳戶標記 hello 應用程式。

> [!NOTE]
> Windows 10 裝置的企業擁有，而連線的 tooAzure AD 可以不再連線其 Microsoft 帳戶 tooa 網域帳戶。 hello 能力 tooconnect Microsoft 帳戶 tooa 網域帳戶，而且具有所有 hello 使用者的資料同步處理從移除 toohello Microsoft 帳戶 （也就是 hello Microsoft 帳戶漫遊透過 hello 連接 Microsoft 帳戶與 Active Directory 功能）Windows 10 裝置的聯結的 tooa 連線 Active Directory 或 Azure AD 環境。
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-tooazure-ad-settings-sync-in-windows-10"></a>如何將 Windows 8 tooAzure AD 設定同步處理，在 Windows 10 中的 Microsoft 帳戶設定同步處理從升級？
如果您已連線的 Microsoft 帳戶與執行 Windows 8 或 Windows 8.1 的聯結的 toohello Active Directory 網域，您會透過您的 Microsoft 帳戶同步設定。 在升級之後 tooWindows 10，您將繼續 toosync 透過 Microsoft 帳戶的使用者設定，只要您是網域的使用者並不會與 Azure AD 連接 hello Active Directory 網域。

如果 hello 內部部署 Active Directory 網域沒有與 Azure AD 連接，您的裝置將會嘗試 toosync 設定使用連接的 hello Azure AD 帳戶。 如果 hello Azure AD 系統管理員不會啟用企業狀態漫遊、 已連接的 Azure AD 帳戶將會停止同步處理設定。 如果您是 Windows 10 使用者且使用 Azure AD 身分識別來登入，則在您的系統管理員啟用透過 Azure AD 進行設定同步處理的功能之後，您將會立即開始同步處理 Windows 設定。

如果您在公司的裝置上儲存個人資料，您應該注意，Windows 作業系統和應用程式資料將會開始同步 tooAzure AD。 這有下列影響 hello:

* 您的個人 Microsoft 帳戶設定將會漂移除了 hello 設定在您的工作或學校的 Azure AD 帳戶。 這是因為 hello Microsoft 帳戶和設定 Azure AD 同步現在正使用不同的帳戶。
* 個人資料 (例如 Wi-Fi 密碼、Web 認證，以及先前透過已連接的 Microsoft 帳戶同步處理的 Internet Explorer 我的最愛) 將會透過 Azure AD 進行同步處理。

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>Microsoft 帳戶和 Azure AD 企業狀態漫遊互通性如何運作？
在 hello 2015 年 11 月版或更新版本的 Windows 10 中，企業狀態漫遊只支援單一帳戶一次。 如果您使用工作或學校的 Azure AD 帳戶登入 tooWindows，所有資料會透過 Azure AD 同步都處理。 如果您使用個人 Microsoft 帳戶登入 tooWindows，所有資料會透過 hello Microsoft 帳戶同步都處理。 通用 appdata 將漫遊 hello 在裝置上，使用只有 hello 主要登入帳戶，並將會漫遊才 hello 應用程式授權由 hello 主要帳戶所擁有。 通用 appdata hello 任何次要帳戶所擁有的應用程式會同步處理。

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>對來自多個租用戶的 Azure AD 帳戶進行設定同步處理？
Azure AD 租用戶與 hello 時從不同的多個 Azure AD 帳戶位於相同的裝置，您必須使用 Azure Rights Management (Azure RMS) 更新 hello 裝置登錄 toocommunicate，每個 Azure AD 租用戶。  

1. Hello GUID 尋找每個 Azure AD 租用戶。 開啟 hello Azure 傳統入口網站，然後選取 Azure AD 租用戶。 hello GUID hello 租用戶是 hello 瀏覽器的網址列中的 hello URL 中。 例如：`https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. 您已擁有 hello GUID 之後，您必須登錄機碼 tooadd hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<租用戶識別碼 GUID >**。
   從 hello**租用戶識別碼 GUID**索引鍵，建立的是新的多字串值 (多重-REG-SZ) 名為**AllowedRMSServerUrls**。 針對其資料，指定 hello hello 裝置存取其他 Azure 租用戶授權 hello 的發佈點 Url。
3. 您可以找到授權發佈點的 Url 執行 hello hello **Get-aadrmconfiguration** cmdlet。 如果值為 hello 的 hello **LicensingIntranetDistributionPointUrl**和**LicensingExtranetDistributionPointUrl**不同，指定兩個值。 如果值為的 hello hello 相同，就可以一次指定 hello 值。

## <a name="what-are-hello-roaming-settings-options-for-existing-windows-desktop-applications"></a>現有的 Windows 桌面應用程式的 hello 漫遊設定選項有哪些？
漫遊僅適用於通用 Windows 應用程式。 有兩個選項可用來在現有 Windows 傳統型應用程式上啟用漫遊：

* hello[桌面橋接器](http://aka.ms/desktopbridge)可協助您將您現有的 Windows 桌面應用程式 toohello 通用 Windows 平台。 從這裡，變更將會最小的程式碼所需 tootake 利用 Azure AD 應用程式資料漫遊。 hello 桌面橋接器提供您的應用程式的應用程式身分，也就是需要 tooenable 應用程式資料漫遊針對現有的桌面應用程式。
* [User Experience Virtualization (UE-V)](https://technet.microsoft.com/library/dn458947.aspx) 可協助您為現有的 Windows 傳統型應用程式建立自訂設定範本，並為 Win32 應用程式啟用漫遊功能。 這個選項就不需要 hello 應用程式開發人員 toochange 程式碼的 hello 應用程式。 UE-V 是有限的 tooon 內部部署 Active Directory 的客戶已購買 Microsoft Desktop Optimization Pack hello 漫遊。

系統管理員可以藉由變更的 Windows 作業系統設定和通用應用程式資料漫遊設定 UE-V tooroam Windows 傳統型應用程式資料[UE-V 群組原則](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2)，包括：

* 「漫遊 Windows 設定」群組原則
* 「不要同步處理 Windows 應用程式」群組原則
* 漫遊 hello 應用程式 > 一節中的 Internet Explorer

在未來的 hello，Microsoft 可能會調查方式 toomake UE-V 緊密整合至 Windows，並擴充 UE-V tooroam 設定透過 hello Azure AD 雲端。

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>我可以將同步處理的設定和資料儲存在內部部署環境中嗎？
企業狀態漫遊 hello Azure 雲端中儲存所有的同步處理的資料。 UE-V 提供一個內部部署漫遊解決方案。

## <a name="who-owns-hello-data-thats-being-roamed"></a>為正在漫遊的 hello 資料擁有者是誰？
hello 企業自己 hello 漫遊透過企業狀態漫遊的資料。 資料會儲存在 Azure 資料中心。 所有的使用者資料會加密傳輸中和靜止 hello 雲端中使用 Azure RMS。 這是之前離開 hello 裝置加密僅特定使用者認證等敏感性資料比較的改進 tooMicrosoft 帳戶為基礎的設定同步。

Microsoft 是認可的 toosafeguarding 客戶資料。 企業使用者的設定資料在離開 Windows 10 裝置前會自動由 Azure RMS 加密，因此沒有任何其他使用者可以讀取此資料。 如果您的組織有 Azure RMS 的付費訂用帳戶，您可以使用其他的 Azure RMS 功能，例如追蹤及撤銷文件、 自動保護電子郵件包含敏感資訊，並管理您自己的金鑰 (也 hello 「 攜帶您自己的金鑰 」 的方案，也稱為 BYOK）。 如需有關這些功能及 Azure RMS 運作方式的詳細資訊，請參閱 [什麼是 Azure Rights Management](https://technet.microsoft.com/jj585026.aspx)。

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>我可以管理特定應用程式或設定的同步處理嗎？
在 Windows 10 中，漫遊個別應用程式沒有 MDM 或群組原則設定 toodisable。 租用戶系統管理員可以停用受管理裝置上所有應用程式的 AppData 同步處理，但是在每個應用程式或應用程式內的層級並沒有更細微的控制。

## <a name="how-can-i-enable-or-disable-roaming"></a>如何啟用或停用漫遊功能？
在 hello**設定**應用程式時，跳過**帳戶** > **同步您的設定**。 從這個頁面上，您可以看到哪些帳戶正在使用的 tooroam 設定，您可以啟用或停用設定 toobe 漫遊的個別群組。

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>Microsoft 對於在 Windows 10 中啟用漫遊功能有什麼建議？
Microsoft 提供數個不同的設定漫遊解決方案可供使用，包括漫遊使用者設定檔、UE-V 和企業狀態漫遊。  Microsoft 是認可的 toomaking 企業狀態漫遊在未來版本的 Windows 中的投資。 如果您的組織未就緒或舒適與移動資料 toohello 雲端，我們建議您為您主要的漫遊技術使用 UE-V。 如果您的組織需要漫遊現有的 Windows 桌面應用程式的支援，但急切 toomove toohello 雲端，我們建議您在企業狀態漫遊和 UE-V 時使用。 雖然 UE-V 和「企業狀態漫遊」是非常類似的技術，但是它們並不互斥。 Toohelp 確保您的組織提供 hello 漫遊您的使用者需要的服務彼此互補它們。  

使用企業狀態漫遊和 UE-V 時，適用下列規則的 hello:

* 企業狀態漫遊是 hello 主要漫遊代理程式在 hello 裝置上。 UE-V 正在使用的 toosupplement hello"Win32 間距 」。
* 當使用 hello UE-V 群組原則時，應該停用 UE-V Windows 設定和現代 UWP 應用程式資料漫遊。 「企業狀態漫遊」已經涵蓋這些漫遊。

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>企業狀態漫遊如何支援虛擬桌面基礎結構 (VDI)？
Windows 10 用戶端 SKU 支援「企業狀態漫遊」，但伺服器 SKU 則不支援。 如果 hypervisor 機器上裝載的用戶端 VM，且您從遠端登入 toohello 虛擬機器，將會漫遊您的資料。 如果多個使用者共用相同的作業系統和使用者從遠端登入，以完整桌面體驗 tooa 伺服器 hello，可能無法運作漫遊。 未正式支援 hello 後面工作階段為基礎的案例。

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>我的組織在使用漫遊之後購買 Azure RMS 會發生什麼情況？
如果您的組織已使用在 Windows 10 漫遊以 hello Azure RMS 有限用途免費訂用帳戶，購買付費的 Azure RMS 訂用帳戶不會造成任何影響 hello 功能 hello 漫遊功能，且不變更設定將需要您的 IT 管理員。

## <a name="known-issues"></a>已知問題
請參閱 hello 文件以 hello[疑難排解](active-directory-windows-enterprise-state-roaming-troubleshooting.md)清單中的已知問題 > 一節。 

## <a name="related-topics"></a>相關主題
* [企業狀態漫遊概觀](active-directory-windows-enterprise-state-roaming-overview.md)
* [在 Azure Active Directory 中啟用企業狀態漫遊](active-directory-windows-enterprise-state-roaming-enable.md)
* [設定同步處理的群組原則和 MDM 設定](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 漫遊設定參考](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [疑難排解](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
