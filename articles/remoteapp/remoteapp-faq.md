---
title: "aaaAzure RemoteApp 常見問題集 |Microsoft 文件"
description: "了解答案 toohello 最常見問題集有關 Azure RemoteApp。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>Azure RemoteApp 常見問題集
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

我們聽說 hello 下列 Azure RemoteApp 的相關問題。 還有其他問題嗎？ 請瀏覽 hello [RemoteApp 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp)，讓我們知道您需要 tooknow，或者下方下拉式清單的註解。

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>找不到您要尋找的內容嗎？ 有問題找不到解答嗎？
如果找不到 hello 資訊在需要時，或有我們未在此處涵蓋其他問題，則請 toohello [Azure RemoteApp 論壇](http://aka.ms/araforum)並詢問您的問題。 我們可以隨時在此加入更多解答。

## <a name="what-is-azure-remoteapp"></a>什麼是 Azure RemoteApp？
* **什麼是 Azure RemoteApp？** 遠端應用程式是一項 Azure 服務可協助您提供安全、 遠端存取 tooapplications 從許多不同的使用者裝置。 深入了解 [Azure RemoteApp](remoteapp-whatis.md)。
* **Hello 部署選項有哪些？** RemoteApp 收藏有兩種：雲端和混合式。 您所需的種類取決於許多因素，像是您是否需要加入網域。 我們會在 [這裡](remoteapp-collections.md)討論所有的決策。

## <a name="quick-tips-on-using-azure-remoteapp"></a>使用 Azure RemoteApp 的快速祕訣
* **多久以後我會中斷連線？多久我之前可以閒置給我 hello 開機？** 4 小時。 如果您或其中一位使用者閒置 4 小時，您將被自動登出 Azure RemoteApp。 簽出 hello 中的其他預設設定[Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)。
* **我能免費試用這項服務嗎？** 是。 免費試用期有 30 天。 Hello 試用結束後，您可以轉換 tooa 付費帳戶 （您可以在生產環境中使用） 或使用 hello 服務停止。 開始免費試用版進行過[portal.azure.com](http://portal.azure.com) -建立 RemoteApp 的新執行個體。 使用 hello 免費試用版，您可以建立 RemoteApp 的 2 個執行個體，具有 10 個使用者每個執行個體。 請記住這個試用期只有 30 天。
  
  ## <a name="azure-remoteapp-subscription-details"></a>Azure RemoteApp 訂用帳戶詳細資料
* **Hello 服務限制有哪些？** 您可以深入了解 hello 預設設定和服務的 Azure RemoteApp 中限制[Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)。 讓我們知道您是否有更多的問題。
* **多少使用者執行的動作有 toohave？** 至少 20 個使用者。 讓我重複 toobe super 清除，-hello 最小值為 20。 您將為 20 個使用者付費。 
* **RemoteApp 的價格為何？** 請查看 [Azure RemoteApp 價格詳細資料 ](https://azure.microsoft.com/pricing/details/remoteapp/)。
* **是否有某種類型的集合成本高於其他集合？** 是的，這取決於您的集合需求。 混合式集合需要從 Azure RemoteApp tooyour 在內部部署網路連線。 如果您使用現有的 VNET/Express Route，就不需要額外的成本。 但如果您使用新的 Azure VNET，以及閘道或 Express Route，您將支付 hello [VPN 閘道](https://azure.microsoft.com/pricing/details/vpn-gateway)或[Express Route](https://azure.microsoft.com/pricing/details/expressroute/)。 這個成本 （hello 連結中詳細說明） 在每月的 Azure RemoteApp 之上成本。

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>集合 - 支援的項目、您應該使用的項目，以及其他項目
* **是否支援自訂的企業營運 (LOB) 應用程式？** 是。 toouse Azure RemoteApp 中的自訂應用程式建立[自訂的範本映像](remoteapp-create-custom-image.md)，然後再上載 toohello RemoteApp 集合。
* **我自訂的 LOB 應用程式會在 Azure RemoteApp 工作？** hello 最佳方式 toofigure 所出 tootest 它。 簽出 hello [RD 相容性中心](http://www.rdcompatibility.com/compatibility/default.aspx)。
* **哪一種部署方式 (雲端或混合式) 最適合我的組織？** 如果您要使用單一登入 (SSO) 的完整整合和安全的內部網路連線，混合式集合會提供 hello 最完整的經驗。 雲端集合提供敏捷式軟體開發輕鬆的方式 tooisolate 您的部署使用多個驗證方法。 深入了解 hello[部署選項](remoteapp-whatis.md)。
* **我們在內部部署或 Azure 中有 SQL 或其他資料庫。我們應使用何種部署類型？** 這取決於您的 SQL 或後端資料庫的所在位置。 如果 hello 資料庫是在私人網路中，使用 hello 混合式集合。 如果 hello 資料庫公開的 toohello 網際網路，並可讓用戶端連線 tooconnect tooit，您可以使用 hello 雲端集合。
* **磁碟機對應、USB 和序列埠、剪貼簿共用，以及印表機重新導向呢？** Azure RemoteApp 中都支援上述所有功能。 預設會啟用剪貼簿共用和印表機重新導向。 您可以在 [這裡](remoteapp-redirection.md)深入了解重新導向。 

## <a name="template-images"></a>範本映像
* **可以使用雲端或現有的虛擬機器做 hello 範本我 RemoteApp 集合？** 可以！ 您可以建立根據 Azure VM 映像、 使用其中一個 hello 映像包含您的訂用帳戶，或建立自訂映像。 簽出 hello [RemoteApp 映像選項](remoteapp-imageoptions.md)。

## <a name="network-options"></a>網路選項
* **hello 混合式集合需要 VNET。我們可以使用現有的 VNET 嗎？** 您可以是否 hello 現有 VNET Azure VNET。 請參閱 「 步驟 1： 設定虛擬網路 」 中 hello[混合式集合指示](remoteapp-create-hybrid-deployment.md)如需詳細資訊。
* **我可以將 VNET 與雲端集合搭配使用嗎？** 確實可以。 如需詳細資訊，請參閱 [建立雲端集合](remoteapp-create-cloud-deployment.md)(特別是步驟 1)。

## <a name="authentication-options"></a>驗證選項
* **驗證呢？支援的方法？** hello 雲端集合支援 Microsoft 帳戶與 Azure Active Directory 帳戶，以及 Office 365 帳戶。 hello 混合式集合支援只有 Azure Active Directory 已同步的帳戶 (使用這類工具[Azure Active Directory Sync](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)) 從 Windows Server Active Directory 部署; 具體而言，同步處理以 hello密碼同步處理選項或同步處理具有 Active Directory Federation Services (AD FS) 同盟設定。 您也可以設定 [Multi-Factor Authentication (MFA)](https://azure.microsoft.com/services/multi-factor-authentication/)。

> [!NOTE]
> hello Azure Active Directory 使用者必須是來自與您訂用帳戶相關聯的 hello 租用戶。 (您可以檢視並修改您的訂閱上 hello**設定**hello 入口網站中的索引標籤。 請參閱[變更由 RemoteApp 所使用的 hello Azure Active Directory 租用](remoteapp-changetenant.md)如需詳細資訊。)
> 
> 

* **為什麼無法讓我的 Azure Active Directory 帳戶存取權？** hello Azure Active Directory 使用者必須是從與您訂用帳戶相關聯的 hello 目錄。 您可以檢視或修改 hello hello 入口網站中 [設定] 索引標籤上的該目錄。 請參閱[變更由 RemoteApp 所使用的 hello Azure Active Directory 租用](remoteapp-changetenant.md)如需詳細資訊。

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>用戶端-哪些裝置可以使用 tooaccess Azure RemoteApp 嗎？
您可以找到良好的用戶端的資訊，包括安裝不同的用戶端 hello 時的步驟[存取您的應用程式在 Azure RemoteApp](remoteapp-clients.md)。

* **哪些裝置和作業系統是否 hello 用戶端應用程式支援？**
  第一個、 hello 電腦和平板電腦： 
  
  * Windows 10 (用戶端預覽版)
  * Windows 8.1 和 Windows 8
  * Windows 7 Service Pack 1
  * Mac OS X
  * Windows RT
  * Android 平板電腦
  * iPad

    與 hello 電話：
  * iPhone
  * Android Phone
  * Windows Phone
    
    [下載](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx)RemoteApp 用戶端。
* **Azure RemoteApp 是否支援精簡型用戶端？** 是，hello 下列 Windows Embedded 的精簡型用戶端支援：
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Enterprise
* **Hello 遠端桌面工作階段主機 (RDSH) 支援的 Windows Server 版本？** Windows Server 2012 R2。

## <a name="support-and-feedback"></a>支援與意見反應
* **什麼是 hello RemoteApp 的支援計劃？** 計費及訂用帳戶管理支援均為免費提供。 技術支援人員可透過 hello [Azure 服務計劃](https://azure.microsoft.com/support/plans/)。 您也可以透過我們的 [Azure 討論區論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp)獲得免費的社群支援。 
* **如何提交意見反應？** 請瀏覽 hello[意見反應論壇](https://feedback.azure.com/forums/247748-azure-remoteapp/)。
* **誰可以彼此通訊 toolearn 深入了解 Azure RemoteApp 嗎？** 在加法 tooour[討論區論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp)，是很好 toopost 問題，您可以每週加入 hello[詢問 hello 專家網路研討會](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html)、 談論一切 RemoteApp。
* **RemoteApp 文件呢？** 很高興您這麼問。 此外 toohello 說明抽屜 hello 入口網站說明的內容 (只要按一下 hello**嗎？** 任何在頁面上 hello 入口網站），下列發行項的 hello 是可用 tooteach 您 RemoteApp 的所有相關資訊：
  
  * **開始使用：**
    * [什麼是 RemoteApp？](remoteapp-whatis.md)
    * [什麼是 hello RemoteApp 範本映像中？](remoteapp-images.md)
    * [授權如何運作？](remoteapp-licensing.md)
    * [RemoteApp 與 Office 如何共同運作？](remoteapp-o365.md)
    * [重新導向如何在 RemoteApp 中運作？](remoteapp-redirection.md)
  * **部署：**
    * [建立自訂範本映像](remoteapp-create-custom-image.md)
    * [建立混合式收藏](remoteapp-create-hybrid-deployment.md)
    * [建立雲端收藏](remoteapp-create-cloud-deployment.md)
    * [設定 RemoteApp 的 Azure Active Directory](remoteapp-ad.md)
    * [在 RemoteApp 中發佈應用程式](remoteapp-publish.md)
  * **管理：**
    
    * [新增使用者](remoteapp-user.md)
    * [設定和使用 RemoteApp 的最佳作法](remoteapp-bestpractices.md)    
    
    影片！ 我們也有一些關於 RemoteApp 的影片。 有些提供簡介 ([簡介 tooAzure RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)) 其他人會引導您完成部署時 ([雲端部署](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be)和[混合式部署](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be))。 請觀賞影片！

### <a name="help-us-help-you"></a>幫我們來協助您
您知道在加法 toorating 這份文件並進行註解下下方，讓您可以變更 toohello 文章本身嗎？ 有所遺漏？ 有所錯誤？ 我是否撰寫了令人混淆的內容？ 向上捲動，然後按一下  **GitHub 上編輯**toomake 變更-這些是 toous 供檢閱，並接著，我們登入它們，就會看到您的變更與改進這裡。

