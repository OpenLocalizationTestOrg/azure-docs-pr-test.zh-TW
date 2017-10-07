---
title: "aaaCloud 應用程式探索的安全性和隱私權考量 |Microsoft 文件"
description: "本主題描述 hello 安全性和隱私權考量相關的 tooCloud 應用程式探索。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 2fce5c82-d3de-4097-808f-40214768df9e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 33659e85bd2cf4294e443512e69a85401f7c53f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-security-and-privacy-considerations"></a>Cloud App Discovery 的安全性和隱私權考量
Microsoft 是 tooprotecting 認可您的隱私權和保護您的資料，同時提供軟體和服務，幫助您管理您組織的 hello 安全性。  
我們可以辨識，當您委託資料 tooothers，該信任需要嚴格的安全性工程投資和專業知識 tooback 它。
Microsoft 遵守 toostrict 相容性與安全性指導方針，從安全軟體開發生命週期實務 toooperating 服務。  
保全和保護資料在 Microsoft 是第一要務。

本主題說明在 Azure Active Directory Cloud App Discovery 內如何收集、處理以及保護資料

## <a name="overview"></a>概觀
Cloud App Discovery 是 Azure AD 的功能，裝載在 Microsoft Azure 中。  
hello 雲端應用程式探索端點代理程式是從受管理的 IT 電腦使用的 toocollect 應用程式探索資料。  
hello 傳送收集的資料安全地透過加密的通道 toohello Azure AD 雲端應用程式探索服務。  
然後 hello Azure 入口網站中看見 hello 組織的雲端應用程式探索資料。 

![Cloud App Discovery 的運作方式](./media/active-directory-cloudappdiscovery-security-and-privacy-considerations/cad01.png) 

hello 下列各節遵循資訊 hello 流程，並描述如何受到保護，當移動從您的組織 toohello Cloud App Discovery 服務，最後 toohello 雲端應用程式探索入口網站。

## <a name="collecting-data-from-your-organization"></a>從您的組織收集資料
在訂單 toouse Azure Active Directory 的雲端應用程式探索功能 tooget 深入了解您的組織中員工所使用的 hello 應用程式，您需要 toofirst 部署 hello Azure AD Cloud App Discovery endpoint agent toomachines 您組織中的。

Hello Azure Active Directory 租用戶 （或其委派） 的系統管理員可以從 hello Azure 入口網站下載 hello 代理程式安裝封裝。 hello 代理程式可以手動安裝或使用 SCCM 或群組原則的 hello 組織中的多部電腦安裝。

如需部署選項的進一步指示，請參閱 [Cloud App Discovery 群組原則部署指南](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)。


### <a name="data-collected-by-hello-agent"></a>Hello 代理程式所收集的資料
hello 代理程式 tooa Web 應用程式建立連接時，會收集 hello hello 下面的清單中所述的資訊。 hello 資訊才會收集該 hello 系統管理員設定探索的那些應用程式。  
您可以編輯的 hello 透過 hello Microsoft 的 hello Cloud App Discovery] 刀鋒視窗的 [代理程式監視的雲端應用程式的 hello 清單[Azure 入口網站](https://portal.azure.com/)下**設定**->**資料集合**->**應用程式集合清單**。 如需詳細資訊，請參閱 [開始使用 Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)


**資訊類別**：使用者資訊  
**描述**：  
提出要求 toohello 目標 Web 應用程式的 hello 程序的 hello Windows 使用者名稱 (例如： DOMAIN\username) 以及 hello Windows 安全性識別碼 (SID) 的 hello 使用者。

**資訊類別**：處理資訊  
**描述**：  
hello 提出 hello 要求 toohello 目標 Web 應用程式的 hello 程序的名稱 (例如:"iexplore.exe")

**資訊類別**：電腦資訊  
**描述**：  
hello 的 hello 安裝代理程式電腦 NetBIOS 名稱。

**資訊類別**：應用程式流量資訊  
**描述**： 

下列連接資訊的 hello:

* hello 來源 （本機電腦） 及目的地 IP 位址和連接埠號碼
* hello 公用 IP 位址的要求會透過哪一個 hello hello 組織。
* hello hello 要求時間
* hello 磁碟區的傳送和接收的流量
* hello IP 版本 （4 或 6）
* 僅限 TLS 連線： hello 目標主機名稱，從 hello 伺服器名稱指示延伸模組或 hello 伺服器憑證。

下列 HTTP 資訊 hello:

* 方法 (GET、POST 等)
* 通訊協定 (HTTP/1.1 等)
* 使用者代理程式字串
* 主機名稱
* 目標 URI (不含查詢字串)
* 內容類型資訊
* 查閱者 URL 資訊 (不含查詢字串)

> [!NOTE]
> 所有非加密連線收集上述 HTTP 資訊 hello。
> 若是 TLS 連線，在 hello 入口網站開啟 hello 「 深度視察 」 設定時，才會擷取這項資訊。 hello 設定預設為 'ON'。
> 如需詳細資料，請參閱下方內容以及 [開始使用 Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 

此外 toohello 資料 hello 代理程式會收集有關 hello 網路活動，它也會收集 hello 軟體和硬體組態、 錯誤報表及如何使用 hello 代理程式的相關資訊的匿名資訊。


### <a name="how-hello-agent-works"></a>Hello 代理程式的運作方式
hello 代理程式安裝包含兩個元件：

* 使用者模式元件
* 核心模式驅動程式元件 (Windows 篩選平台驅動程式)

Hello 代理程式第一次安裝時它會儲存電腦專用的受信任的憑證 hello 機器上它然後使用 tooestablish 安全的連線與 hello 雲端應用程式探索服務。  
hello 代理程式定期擷取原則組態 hello Cloud App Discovery 服務透過這種安全連線。  
hello 原則包括哪些雲端應用程式 toomonitor 的相關資訊與是否自動更新啟用，以及其他項目。

因為傳送和接收 hello 電腦上從 Internet Explorer 和 Chrome Web 流量，hello Cloud App Discovery 代理程式會分析 hello 流量，並擷取 hello 相關的中繼資料 (請參閱 hello **hello 代理程式所收集的資料**區段請見上方）。  
每隔一分鐘，hello 代理程式會將上傳收集的 hello 中繼資料 toohello Cloud App Discovery 服務透過加密通道。

hello，驅動程式元件會攔截 hello 加密的流量，並將本身插入 hello 加密的資料流。 詳細資料請參閱 hello**攔截資料加密連線 （深度視察）**下一節。

### <a name="respecting-user-privacy"></a>尊重使用者隱私權
我們的目標是 tooprovide 管理員 hello 工具 tooset hello 之間平衡詳細光學視其組織的應用程式使用方式和使用者隱私權。 toothat 結束時，我們提供下列參數 hello hello 入口網站中設定 頁面中的 hello:

* **資料收集**： 系統管理員可以選擇 toospecify 哪些應用程式或他們希望 tooget 探索資料的應用程式類別目錄。
* **深度視察**： 系統管理員可以選擇 toospecify 如果 hello 代理程式會收集 SSL/TLS 連線的 HTTP 流量 (也稱為**「 深度視察 」**)。 更多有關 hello 下一節。
* **同意選項**： 系統管理員可以使用 hello 雲端應用程式探索入口網站 toochoose 是否 toonotify 使用者的 hello 所收集的資料 hello 代理程式，以及是否 toorequire 使用者同意 hello 代理程式 」 會收集使用者資料。

hello Cloud App Discovery endpoint agent 只會收集 hello 所述的 hello 資訊**hello 代理程式所收集的資料**上一節。

### <a name="intercepting-data-from-encrypted-connections-deep-inspection"></a>攔截來自加密連線的資料 (深度檢查)
如先前所述，系統管理員可以設定 hello 代理程式 toomonitor 資料，從 加密連接 （「 深度視察 」）。 TLS ([傳輸層安全性](https://msdn.microsoft.com/library/windows/desktop/aa380516%28v=vs.85%29.aspx)) 是其中一個 hello 最常見的通訊協定在 hello 網際網路上使用今天。 透過加密與 TLS 通訊，用戶端可以建立安全和私用通訊通道與網頁伺服器;TLS 提供基本保護傳遞驗證認證，並防止 hello 洩漏機密資訊。

雖然重要的安全性和隱私權保護，可讓 hello 端對端安全加密的通道提供的 TLS，hello 通訊協定通常會濫用惡意或等到惡意用途。 許多，TLS 通常被指事實上，tooas hello 「 通用的防火牆略過通訊協定 」。 hello 根 hello 問題是大部分的防火牆，會無法 tooinspect TLS 通訊，因為 hello 應用程式層級資料使用 SSL 加密。 了解這種情況，攻擊者通常利用 TLS toodeliver 惡意裝載 tooa 使用者確信甚至 hello 最智慧型應用程式層級防火牆會完全密件 tooTLS，且必須只轉送 TLS 主機之間的通訊。 使用者經常會利用透過和強制執行其公司的防火牆和 proxy 伺服器，使用它 tooconnect toopublic proxy 通道透過 hello 防火牆，否則可能會封鎖的原則-TLS 通訊協定 TLS toobypass 存取控制。

深入檢查可以讓 hello Cloud App Discovery 代理程式 tooact，做為受信任中--攔截。 當用戶端要求是 tooaccess HTTPS 受保護資源，hello Endpoint 代理程式的驅動程式會攔截 hello 連線，並建立新的連接 toohello 目的地伺服器 tooretrieves 代表 hello 用戶端 SSL 憑證。 hello 憑證可以信任 （藉由檢查，它未被撤銷，並執行其他憑證檢查），而且如果這些都通過，hello Endpoint 代理程式則會複製 hello 資訊從 hello 伺服器憑證並建立它自己，然後確認 hello 代理程式又稱為攔截憑證-使用該資訊的伺服器憑證。 帶正負號的立即 hello 端點代理程式的根憑證，安裝 hello Windows 信任的憑證存放區中的 hello 攔截憑證。 此自我簽署的根憑證會標示為非可匯出，ACL 有 tooadministrators。 它是在其所建立的預定的 toonever 保持 hello 機器。 當 hello 使用者的用戶端應用程式收到 hello 攔截憑證時，它會信任它，因為它可以成功地驗證 hello 憑證鏈結所有 hello 方式 toohello 根憑證。 從使用者的觀點來看，這個處理序大致上清楚明瞭，但有下列幾點注意事項。

藉由啟用深度視察，hello Cloud App Discovery Endpoint Agent 可以解密及檢查 TLS 加密通訊，允許 hello 服務 tooreduce 雜訊並提供深入了解 hello hello 加密雲端應用程式使用量。

#### <a name="a-word-of-caution"></a>特別注意事項
在之前的深度視察，強烈建議您進行通訊，您的意圖 tooyour 法律和人力資源部門，並取得其同意。 原因很明顯，要檢查使用者的私人加密通訊是非常敏感的話題。 生產推出的深度視察，請確認您公司的安全性，且可接受的使用原則更新之前會檢查 tooindicate 加密通訊。 使用者通知與豁免的站台視為機密 （例如銀行和醫療網站） 也可能需要設定 Cloud App Discovery toomonitor 它們。 如上面所述，系統管理員可以使用 hello 雲端應用程式探索入口網站 toochoose 是否 toonotify 使用者的 hello 所收集的資料 hello 代理程式，以及是否 toorequire 使用者同意 hello 代理程式 」 會收集使用者資料。

### <a name="known-issues-and-drawbacks"></a>已知的問題與缺點
有少數的情況下，TLS 的攔截可能會影響 hello 終端使用者體驗：

* 擴充的驗證 (EV) 憑證會轉譯為您所信任的網站瀏覽一個視覺線索的 hello web 瀏覽器綠色 tooact hello 網址列。 TLS 檢查無法中有重複的環境變數 hello 憑證就會發出 toohello 用戶端，因此使用 EV 憑證的網站運作正常，但 hello 網址列將不會顯示綠色。  
* 公用金鑰釘選 （也稱為釘選的憑證） 設計 toohelp 保護使用者免於攔截攻擊和 rogue 憑證授權單位。 Hello 釘選網站的根憑證不符合其中一個已知良好的 CA 的 hello，hello 瀏覽器會拒絕某些 hello 連接，發生錯誤。 事實上，由於 TLS 攔截是一種攔截，因此這些連線將會失敗。
* 如果使用者按一下 hello 瀏覽器位址列瀏覽器 tooinspect hello 站台資訊中的 hello 鎖定圖示，它們將不會看到結束 hello 憑證授權單位鏈結用 toosign hello 網站憑證，但是改為結尾的憑證鏈結 hello Windows受信任的憑證存放區。

tooreduce hello 發生這些問題，我們會持續追蹤的雲端服務和用戶端應用程式已知 toouse 擴充驗證或公用金鑰釘選，並指示 hello Endpoint Agent tooavoid 攔截受影響的連接。 即使在這些情況下，不過，仍會收到 hello 使用這些雲端應用程式和 hello 所傳送的資料的磁碟區的報告，但它們不會深入檢查，因為沒有相關 hello 應用程式所使用的方式將成為可用。

## <a name="sending-data-toocloud-app-discovery"></a>傳送資料 tooCloud 應用程式探索
一旦 hello 代理程式收集中繼資料，就會快取 hello 機器上為向上 tooone 分鐘或 hello 直到快取的資料到達 5 MB 的大小。 然後壓縮，並透過安全連線 toohello Cloud App Discovery 服務傳送。

如果以 hello Cloud App Discovery 服務因為任何原因無法 toocommunicate hello 代理程式，hello 收集的中繼資料會儲存在只能由授權使用者 （例如 hello 系統管理員群組） 的 hello 機器上的本機檔案快取。  
hello 代理程式會自動嘗試 tooresend hello 快取中繼資料直到它成功收到 hello 雲端應用程式探索服務。

## <a name="receiving-hello-data-at-hello-service-end"></a>收到 hello hello 服務端的資料
hello 代理程式驗證 toohello Cloud App Discovery 上述使用 hello 電腦特定的用戶端驗證憑證的服務，並透過加密通道轉送資料。  
hello Cloud App Discovery 服務的分析管線處理程序的中繼資料為每個客戶個別以邏輯方式將它分割透過 hello 分析管線的所有階段。
hello 分析中繼資料的磁碟機 hello hello 入口網站中的各種報告。

hello 未處理的中繼資料和分析 hello 中繼資料會儲存向上 too180 天。 此外，客戶可以選擇他們所選擇的 Azure blob 儲存體帳戶中的 toocapture hello 分析中繼資料。
這是適用於離線分析的中繼資料，以及較長的 hello 資料的保留。

## <a name="accessing-hello-data-using-hello-azure-portal"></a>存取 hello 資料使用 hello Azure 入口網站
在收集投入時間 tookeep hello 中繼資料安全，根據預設只有 hello 租用戶的全域系統管理員具有存取 toohello Cloud App Discovery 功能 hello Azure 入口網站中。  
不過，系統管理員可以選擇 toodelegate 此存取 tooother 使用者或群組。

> [!NOTE]
> 如需詳細資訊，請參閱 [開始使用 Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 


中的任何使用者存取 hello 資料 hello 入口網站、 必須授權與 Azure AD Premium 授權。

## <a name="additional-resources"></a>其他資源
* [如何探索組織內使用未經批准的雲端應用程式](active-directory-cloudappdiscovery-whatis.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)

