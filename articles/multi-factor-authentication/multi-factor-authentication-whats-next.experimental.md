---
title: "Azure MFA aaaConfigure |Microsoft 文件"
description: "這是使用 MFA，接下來描述哪些 toodo hello Azure 多因素驗證頁面。  其內容包括報告、詐騙警示、一次性略過、自訂語音訊息、快取、信任的 IP 及應用程式密碼。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: kgremban
ms.openlocfilehash: db7d87d95b73fed78d3ce599fd03da9692851663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-settings"></a>設定 Azure Multi-Factor Authentication 設定
既然您已啟動並執行 Azure Multi-Factor Authentication，本文將協助您進行管理。  它涵蓋了不同的主題可協助您充分利用 Azure Multi-factor Authentication tooget hello。  並非所有版本的 Azure Multi-Factor Authentication 均提供所有這些功能。

| 功能 | 說明 | 
|:--- |:--- |
| [詐騙警示](#fraud-alert) |可設定詐騙警示與設定，讓您的使用者可以報告詐騙嘗試 tooaccess 其資源。 |
| [一次性略過](#one-time-bypass) |單次許可能夠讓使用者 tooauthenticate 一次可以 「 略過 「 多重要素驗證。 |
| [自訂語音訊息](#custom-voice-messages) |自訂語音訊息可讓您 toouse 您自己的記錄或 greetings 與多重要素驗證。 |
| [快取](#caching-in-azure-multi-factor-authentication) |快取可讓您 tooset 在特定時間週期，以便後續驗證嘗試會自動成功完成。 |
| [信任的 IP](#trusted-ips) |受管理或同盟租用戶的系統管理員可以使用信任的 Ip toobypass 雙步驟驗證，從 hello 公司近端內部網路登入的使用者。 |
| [應用程式密碼](#app-passwords) |應用程式密碼允許不 MFA 感知 toobypass 多重要素驗證，並繼續工作的應用程式。 |
| [針對已記住的裝置和瀏覽器，記住其 Multi-Factor Authentication](#remember-multi-factor-authentication-for-devices-that-users-trust) |可讓您 tooremember 裝置設定天數之後，使用者已成功登入使用 MFA。 |
| [可選取的驗證方法](#selectable-verification-methods) |可讓您可供使用者 toouse toochoose hello 驗證方法。 |

## <a name="access-hello-azure-mfa-management-portal"></a>存取 hello Azure MFA 管理入口網站

涵蓋在本文中的 hello 功能 hello Azure Multi-factor Authentication 管理入口網站中設定。 有兩種 tooaccess hello hello Azure 傳統入口網站透過 MFA 管理入口網站。 hello 第一個是藉由管理 Multi-factor Auth 提供者。 hello 第二個是透過 hello MFA 服務設定。 

### <a name="use-an-authentication-provider"></a>使用驗證提供者

如果您使用多因素驗證提供者的耗用量為基礎的 MFA 時，使用此方法 tooaccess hello 管理入口網站。

tooaccess hello MFA 管理入口網站，透過 Azure 多重要素驗證提供者，登入 hello Azure 傳統入口網站做為系統管理員，並且選取 hello Active Directory 選項。 按一下 hello **Multi-factor Auth 提供者**索引標籤，然後選取您的目錄並按一下 hello**管理**hello 底部的按鈕。

### <a name="use-hello-mfa-service-settings-page"></a>使用 hello MFA 服務設定 頁面 

如果您有一個 hello 遵循授權，您可以使用 hello MFA 服務設定 頁面上：
- Azure MFA
- Azure AD Premium 
- Enterprise Mobility + Security

tooaccess hello MFA 服務設定 頁面上，登入 hello Azure 傳統入口網站，以系統管理員透過 hello MFA 管理入口網站，並選取 hello Active Directory 選項。 在您的目錄中按一下，然後按一下hello**設定** 索引標籤。Hello 多因素驗證 區段下，選取**管理服務設定**。 在 hello hello MFA 服務設定] 頁面底部，按一下 [hello **Go toohello 入口網站**連結。


## <a name="fraud-alert"></a>詐騙警示
可設定詐騙警示與設定，讓您的使用者可以報告詐騙嘗試 tooaccess 其資源。  使用者可以報告詐騙與 hello 行動裝置應用程式或透過他們的電話號碼。

### <a name="set-up-fraud-alert"></a>設定詐騙警示
1. 瀏覽每個在 hello 這個頁面頂端的 hello 指示 toohello MFA 管理入口網站。
2. 在 hello Azure Multi-factor Authentication 管理入口網站中，按一下 **設定**hello 設定 區段底下。
3. 在 hello 詐騙警示 區段的 hello 設定 頁面上，檢查 hello**允許使用者 toosubmit 詐騙警示**核取方塊。
4. 選取**儲存**tooapply 您的變更。 

### <a name="configuration-options"></a>組態選項

- **回報詐騙時封鎖使用者** - 如果使用者報告詐騙，將會封鎖其帳戶。
- **程式碼 tooReport 初始問候語期間詐騙**位使用者通常會按 # tooconfirm 雙步驟驗證。 如果他們想 tooreport 詐騙，然後再按 # 進入程式碼。 根據預設，此代碼是 **0**，但您可以自訂。

> [!NOTE]
> Microsoft 的預設語音問候語指示使用者 toopress &#0; toosubmit 詐騙警示。 如果您想 toouse 0 以外的程式碼，您應該記錄，並上傳您自己的自訂語音問候語與適當的指示。

![詐騙警示選項 - 螢幕擷取畫面](./media/multi-factor-authentication-whats-next/fraud.png)

### <a name="how-users-report-fraud"></a>使用者如何報告詐騙 
提報詐騙活動的方法有兩種。  無論是透過 hello 行動裝置應用程式或是透過 hello 電話。  

#### <a name="report-fraud-with-hello-mobile-app"></a>與 hello 行動裝置應用程式報告詐騙
1. 驗證傳送 tooyour 電話，當選取它 tooopen hello Microsoft 驗證器應用程式。
2. 選取**拒絕**hello 通知。 
3. 選取 [回報詐騙]。
4. 關閉 hello 應用程式。

#### <a name="report-fraud-with-a-phone"></a>使用電話報告詐騙
1. Tooyour 的電話以進行驗證通話時，接聽。  
2. tooreport 詐騙輸入 hello 詐騙代碼 （預設值為 0），然後再 hello # 符號。 接著，系統會通知您詐騙警示已提交。
3. 結束 hello 呼叫。

### <a name="view-fraud-reports"></a>檢視詐騙報告
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. Hello 左側選取 Active Directory。
3. 在 hello 頂端，選取**Multi-factor Auth 提供者**tooshow 您的 Multi-factor Auth 提供者的清單。
4. 選取您的 Multi-factor Auth 提供者，然後按一下**管理**hello hello 頁底端。 hello Azure Multi-factor Authentication 管理入口網站隨即開啟。
5. 在 hello Azure Multi-factor Authentication 管理入口網站中，在檢視報表，按一下 **詐騙警示**。
6. 指定您希望 tooview hello 報表中的 hello 日期範圍。 您也可以指定使用者名稱、 電話號碼和 hello 使用者的狀態。
7. 按一下**執行**tooshow 的詐騙警示報告。 按一下**匯出 tooCSV**如果您希望 tooexport hello 報表。

## <a name="one-time-bypass"></a>一次性略過
單次許可能夠讓使用者 tooauthenticate 一次而不需執行兩步驟驗證。 hello 略過是暫時性的指定的秒數後過期。 在其中 hello 行動裝置應用程式或電話未收到通知或電話的情況下，您可以啟用一次性略過讓 hello 使用者能夠存取所需的 hello 資源。

### <a name="create-a-one-time-bypass"></a>建立單次許可
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 瀏覽每個在 hello 這個頁面頂端的 hello 指示 toohello MFA 管理入口網站。
3. 如果您發現您的 Azure MFA 提供者名稱 hello hello 保有 **+** 下一步 tooit，按一下 hello  **+** 。 會顯示不同的 MFA 伺服器複寫群組與 hello Azure 預設群組。 選取 hello 適當的群組。
4. 在 [使用者管理] 底下，選取 [單次許可] 。
5. 在 hello 單次許可 頁面上，按一下 **新增單次許可**。

  ![雲端](./media/multi-factor-authentication-whats-next/create1.png)

6. 輸入 hello 使用者名稱、 hello 持續期間 hello 略過，以及 hello hello 許可的原因。 按一下 [許可]。
7. hello 時間限制進入效果立即，因此 hello 使用者需求 toosign 在 hello 一次性略過前到期。 

### <a name="view-hello-one-time-bypass-report"></a>檢視 hello 一次性略過的報表
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. Hello 左側選取 Active Directory。
3. 在 hello 頂端，選取**Multi-factor Auth 提供者**tooshow 您的 Multi-factor Auth 提供者的清單。
4. 選取您的 Multi-factor Auth 提供者，然後按一下**管理**hello hello 頁底端。 hello Azure Multi-factor Authentication 管理入口網站隨即開啟。
5. 在左側 hello，檢視報表，在 hello Azure Multi-factor Authentication 管理入口網站，按一下 **單次許可**。
6. 指定您希望 tooview hello 報表中的 hello 日期範圍。 您也可以指定使用者名稱、 電話號碼和 hello 使用者的狀態。
7. 按一下**執行**tooshow 略過的報表。 按一下**匯出 tooCSV**如果您希望 tooexport hello 報表。

## <a name="custom-voice-messages"></a>自訂語音訊息
自訂語音訊息可讓您 toouse 您自己的記錄或 greetings 進行兩步驟驗證。 您可以使用自訂語音訊息加法 tooor tooreplace hello Microsoft 記錄中。

在開始之前，請注意下列事項：

* hello 支援檔案格式為.wav 和.mp3。
* hello 檔案大小上限是 5 MB。
* 驗證訊息應該少於 20 秒。 超過 20 秒的訊息不 hello 為使用者提供足夠時間 toorespond hello 驗證時間之前。

### <a name="set-up-a-custom-message"></a>設定自訂訊息

有兩個部分 toocreating 自訂訊息。 首先，您上傳 hello 訊息，然後您將它為您的使用者。

tooupload 您自訂的訊息：

1. 建立自訂語音訊息，使用其中一種支援的 hello 檔案格式。
2. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
3. 瀏覽每個在 hello 這個頁面頂端的 hello 指示 toohello MFA 管理入口網站。
4. 在 hello Azure Multi-factor Authentication 管理入口網站中，按一下 **語音訊息**hello 設定 區段底下。
5. 在 [hello 設定： 語音訊息] 頁面上，按一下**新增語音訊息**。
   ![雲端](./media/multi-factor-authentication-whats-next/custom1.png)
6. 在 hello 設定： 新增語音訊息 頁面上，按一下 **管理音效檔**。
   ![雲端](./media/multi-factor-authentication-whats-next/custom2.png)
7. 在 [hello 設定： 音效檔案] 頁面上，按一下**上傳音效檔**。
   ![雲端](./media/multi-factor-authentication-whats-next/custom3.png)
8. 在 hello 設定： 上傳音效檔，請按一下**瀏覽**並瀏覽 tooyour 語音訊息，請按一下**開啟**。
9. 新增 [描述]，然後按一下 [上傳]。
10. 一旦上傳 hello 語音訊息時，出現訊息，確認您已成功上傳 hello 檔案。

tooturn hello 訊息，為您的使用者上：

1. Hello 左側，按一下 **語音訊息**。
2. Hello 語音訊息] 區段中，按一下 [**新增語音訊息**。
3. Hello 語言 下拉式清單中，從選取的語言。
4. 如果這個訊息是特定應用程式，則會指定在 hello 應用程式 方塊中。
5. 從 hello 訊息類型 下拉式清單中，選取 hello 訊息類型 toobe 以新的自訂訊息覆寫。
6. 從 hello 音效檔 下拉式清單中，選取您上傳的 hello 音效檔 hello 第一個部分中。
7. 按一下 [建立] 。 即會出現一則訊息，確認已成功建立語音訊息。
    ![雲端](./media/multi-factor-authentication-whats-next/custom5.png)</center>

## <a name="caching-in-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication 中的快取
快取可讓您 tooset 在特定時間週期，以便在該時間週期內的後續驗證嘗試會自動成功完成。 在內部部署系統，例如 VPN hello 第一個要求仍在進行中時，請傳送驗證要求多時，會使用快取。 Hello 使用者之後自動讓 hello 後續要求 toosucceed 成功 hello 第一個驗證進行中。 

快取不是預期的 toobe 用於登入 tooAzure AD。

### <a name="set-up-caching"></a>設定快取 
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 瀏覽每個在 hello 這個頁面頂端的 hello 指示 toohello MFA 管理入口網站。
3. 在 hello Azure Multi-factor Authentication 管理入口網站中，按一下 **快取**hello 設定 區段底下。
4. 按一下**新的快取**hello 設定快取 頁面上。
5. 選取 hello 快取類型和 hello 快取秒數。 按一下 [建立] 。

<center>![雲端](./media/multi-factor-authentication-whats-next/cache.png)</center>

## <a name="trusted-ips"></a>信任的 IP
信任的 Ip 是 Azure MFA 的受管理或同盟租用戶系統管理員可以使用 toobypass 雙步驟驗證的功能。 這適用於從 hello 公司近端內部網路登入的使用者。 這項功能可與 hello 完整版本的 Azure Multi-factor Authentication，而非 hello 免費版本的系統管理員。 如需如何 tooget hello 完整版的 Azure Multi-factor Authentication 的詳細資訊，請參閱[Azure Multi-factor Authentication](multi-factor-authentication.md)。

| Azure AD 租用戶類型 | 可用的信任 IP 選項 |
|:--- |:--- |
| 受管理 |<li>特定的 IP 位址範圍-系統管理員可以指定 IP 位址範圍，可以略過從 hello 公司內部網路登入的使用者的雙步驟驗證。</li> |
| 同盟 |<li>所有同盟使用者的所有同盟使用者將簽署中從 hello 內組織將會略過雙步驟驗證，使用 AD FS 所發出的宣告。</li><br><li>特定的 IP 位址範圍-系統管理員可以指定 IP 位址範圍，可以略過從 hello 公司內部網路登入的使用者的雙步驟驗證。 |

此略過機制只適用於公司內部網路。 

**公司網路內部的使用者體驗︰**

停用「信任的 IP」時，瀏覽器流程需要雙步驟驗證，較舊的豐富型用戶端應用程式需要應用程式密碼。 

當「信任的 IP」啟用時，瀏覽器流程就「不」需要雙步驟驗證。 應用程式密碼*不*需要針對較舊的豐富型用戶端應用程式，前提是 hello 使用者尚未已經建立應用程式密碼。 應用程式密碼一旦使用，以後就都需要使用。 

**公司網路外部的使用者體驗︰**

不論啟用或停用「信任的 IP」，瀏覽器流程需要雙步驟驗證，較舊的豐富型用戶端應用程式需要應用程式密碼。 

### <a name="tooenable-trusted-ips"></a>tooenable 信任 Ip
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 瀏覽每 hello 開頭的這篇文章的 hello 指示 toohello MFA 服務設定 頁面。
3. 在 hello 服務設定頁面的 信任的 Ip，您有兩個選項：
   
   * **針對來自我的內部網路同盟使用者要求**– hello 核取方塊。 從使用 AD FS 所發出的宣告 hello 公司網路略過雙步驟驗證登入的所有同盟的使用者。
   * **針對來自特定範圍之公開 Ip 的要求**– 提供使用 CIDR 表示法的 hello 文字方塊中輸入 hello IP 位址。 例如： xxx.xxx.xxx.0/24 的 IP 位址在 hello 範圍 xxx.xxx.xxx.1 – xxx.xxx.xxx.254 或 xxx.xxx.xxx.xxx/32 單一 IP 位址。 您可以輸入向上 too50 IP 位址範圍。 從這些 IP 位址登入的使用者會略過雙步驟驗證。
4. 按一下 [儲存] 。
5. 一旦套用 hello 更新之後，按一下 **關閉**。

![信任的 IP](./media/multi-factor-authentication-whats-next/trustedips3.png)

## <a name="app-passwords"></a>應用程式密碼
某些應用程式 (例如 Office 2010 或更舊版本和 Apple Mail) 不支援雙步驟驗證。 它們不設定的 tooaccept 第二個驗證。 toouse 這些應用程式，您需要 toouse 」 應用程式密碼 」 取代傳統密碼。 hello 應用程式密碼允許 hello 應用程式 toobypass 雙步驟驗證，並繼續工作。

> [!NOTE]
> 新式驗證 hello Office 2013 用戶端
> 
> Office 2013 用戶端 （包括 Outlook） 和較新的支援新式驗證通訊協定，而且可以是啟用的 toowork 具有雙步驟驗證。 一旦啟用，這些用戶端應用程式就不需要應用程式密碼。  如需詳細資訊，請參閱[發表的 Office 2013 新式驗證公開預覽](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。

### <a name="important-things-tooknow-about-app-passwords"></a>重要事項 tooknow 有關應用程式密碼
以下是您應該了解的應用程式密碼重要事項清單。

* Hello 一次每個應用程式的輸入方塊中輸入應用程式密碼。 使用者不具有這些 tookeep 追蹤，並輸入每次。
* hello 實際的密碼自動產生，而不由 hello 使用者提供。 hello 自動產生的密碼比較難攻擊者 tooguess 和更為安全。
* 每位使用者的密碼以 40 組為限。 
* 應用程式密碼並用於內部部署案例中可能會開始失敗，因為 hello 組織識別碼以外得知 hello 應用程式密碼，不會快取。例如，在內部部署的 Exchange 電子郵件但 hello 封存郵件 hello 雲端中。 hello 相同的密碼無法運作。
* 當多重要素驗證啟動時，您可以對某些非瀏覽器用戶端使用您的密碼。 您無法對系統管理工作使用應用程式密碼。 確認您建立的服務帳戶具有強式密碼 toorun PowerShell 指令碼，請勿啟用該帳戶進行兩步驟驗證。

> [!WARNING]
> 應用程式密碼無法在用戶端會同時與內部部署及雲端自動探索端點通訊的混合環境作用。 網域密碼是必要的 tooauthenticate 內部部署和應用程式密碼是必要的 tooauthenticate 與 hello 雲端。

### <a name="naming-guidance-for-app-passwords"></a>應用程式密碼的命名指引
應用程式密碼名稱應反映出 hello 裝置使用。 例如，如果您的膝上型電腦有非瀏覽器應用程式，請建立一個名為 Laptop 的應用程式密碼，並使用該應用程式密碼。 然後，建立另一個應用程式密碼名為 桌面 hello 桌面的電腦上的相同應用程式。 

Microsoft 建議為每個裝置建立一個應用程式密碼，而不是為每個應用程式建立一個應用程式密碼。

### <a name="federated-sso-app-passwords"></a>同盟 (SSO) 應用程式密碼
Azure AD 支援與內部部署 Windows Server Active Directory Domain Services (AD DS) 同盟 (單一登入)。 如果貴組織已與 Azure AD 同盟，您將使用 Azure Multi-factor Authentication toobe hello 應用程式密碼的資訊是很重要。 本節僅適用於 toofederated (SSO) 客戶。

* 應用程式密碼由 Azure AD 驗證，因此會略過同盟。 唯有在設定應用程式密碼時才會主動使用同盟。
* 適用於同盟 (SSO) 使用者，我們絕不 toohello 身分識別提供者 (IdP) 與 hello 被動流程不同。 hello 密碼儲存在 hello 組織識別碼。如果 hello 使用者離開 hello 公司，該資訊會有 tooflow tooorganizational 識別碼使用 DirSync 中實際的時間。 帳戶停用/刪除可能佔用 toothree 小時 toosync，延遲在 Azure AD 中的停用/刪除的應用程式密碼。
* 應用程式密碼不會遵守內部部署用戶端存取控制設定。
* 應用程式密碼不適用內部部署驗證記錄/稽核功能。
* 某些進階架構設計在使用雙步驟驗證時，可能需要有組織使用者名稱、密碼和應用程式密碼的組合。 不過，這取決於它們的驗證位置。 對於根據內部部署基礎結構進行驗證的用戶端，您可以使用組織使用者名稱和密碼。 對 Azure AD 進行驗證的用戶端，您會使用 hello 應用程式密碼。

  例如，假設您的架構由以下執行個體組成：

  * 您要讓內部部署 Active Directory 執行個體與 Azure AD 同盟
  * 您正在使用 Exchange Online
  * 您只在內部使用 Lync
  * 您正在使用 Azure Multi-Factor Authentication

  ![Proofup](./media/multi-factor-authentication-whats-next/federated.png)

  在這些情況下，您必須遵循下列步驟：

  * 登入時-在 tooLync，使用您的組織使用者名稱和密碼。
  * 當嘗試 tooaccess hello 通訊錄，透過連接 tooExchange 線上 Outlook 用戶端，請使用 應用程式密碼。

### <a name="allow-app-password-creation"></a>允許建立應用程式密碼
根據預設，使用者無法建立應用程式密碼，但您可以自行啟用 hello 功能。 tooallow 使用者 hello 能力 toocreate 應用程式密碼，請使用下列程序的 hello:

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 瀏覽每 hello 開頭的這篇文章的 hello 指示 toohello MFA 服務設定 頁面。
3. 選取選項按鈕，hello 接下來太**入非瀏覽器應用程式允許使用者 toocreate 應用程式密碼 toosign**。

![建立應用程式密碼](./media/multi-factor-authentication-whats-next/trustedips3.png)

### <a name="create-app-passwords"></a>建立應用程式密碼
使用者可以在一開始的註冊期間建立應用程式密碼。 這些系統提供的選項，在 hello 結尾 hello 註冊程序可讓它們 toocreate 應用程式密碼。

使用者也可以在註冊後建立應用程式密碼。 他們可以變更其設定值，在 hello Azure 入口網站或 hello Office 365 入口網站中的建立 hello 應用程式密碼。 如需使用者的詳細資訊和詳細步驟，請參閱[什麼是 Azure Multi-Factor Authentication 中的應用程式密碼](./end-user/multi-factor-authentication-end-user-app-passwords.md)。

## <a name="remember-multi-factor-authentication-for-devices-that-users-trust"></a>針對使用者信任的裝置，記住 Multi-Factor Authentication
記住裝置和瀏覽器的 Multi-Factor Authentication，使用者信任是供給所有 MFA 使用者的免費功能。 Multi-factor authentication 可讓使用者 tooby 通過 MFA 設定天數之後登入。 這項功能增強可用性藉由減少使用者可能會對 hello 雙步驟驗證的 hello 次數相同的裝置。

不過，若帳戶或裝置遭到入侵，則記住受信任裝置的 MFA 可能會影響安全性。 如果公司帳戶洩漏或受信任的裝置遺失或遭竊，您需要太[所有裝置上還原 Multi-factor Authentication](multi-factor-authentication-manage-users-and-devices.md#restore-mfa-on-all-remembered-devices-for-a-user)。 此動作會撤銷 hello 信任狀態，請從所有的裝置，且 hello 使用者需要的 tooperform 雙步驟驗證一次。 您也可以指示在自己的裝置 hello 指示您使用者 toorestore MFA 在[管理您的設定進行兩步驟驗證](./end-user/multi-factor-authentication-end-user-manage-settings.md#require-two-step-verification-again-on-a-device-youve-marked-as-trusted)

### <a name="how-it-works"></a>運作方式

記住 Multi-factor Authentication 的運作方式是永續性 cookie 設定 hello 瀏覽器上，當使用者簽 hello 「 不要再詢問我**X**天 」 在登入時的方塊。 hello 使用者不會提示您輸入 MFA 再次來自該瀏覽器 hello cookie 到期之前。 如果 hello 使用者開啟不同的瀏覽器上 hello 同一部裝置或清除其 cookie，它們是提示的 tooverify 一次。 

hello 「 不要再詢問我**X**天 」 核取方塊並不會顯示非瀏覽器應用程式，無論它們支援新式驗證。 這些應用程式使用每隔一小時會提供新存取權杖的重新整理權杖。 當重新整理權杖已經驗證時，Azure AD 會檢查 hello 最後一個時間雙步驟驗證已執行的天數內 hello 設定。 

結論，受信任的裝置上記住 MFA 會減少 hello 驗證 web 應用程式 （通常每次詢問） 上的數目。 但它也會增加 hello 數目新式驗證的用戶端 （通常要求每隔 90 天） 的驗證。

> [!NOTE]
>使用者執行雙步驟驗證，透過 hello Azure MFA Server AD fs 或協力廠商 MFA 解決方案時，這項功能不與 hello 的 AD FS [保留我登入] 功能相容。 如果您的使用者選取 AD FS 上的 「 讓我保持登 」，而且也將他們的裝置，以信任標示為 MFA，它們將無法能 tooverify hello 「 記住 MFA"數天內過期之後。 Azure AD 要求全新雙步驟驗證，但是 AD FS 會傳回原始 MFA 宣告 hello 和日期，而不是執行一次雙步驟驗證的語彙基元。 此程序會啟動 Azure AD 與 AD FS 之間的驗證迴圈。 

### <a name="enable-remember-multi-factor-authentication"></a>啟用記住 Multi-Factor Authentication
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 瀏覽每 hello 開頭的這篇文章的 hello 指示 toohello MFA 服務設定 頁面。
3. 在 hello 服務設定 頁面上，在管理使用者裝置設定，請檢查 hello**他們信任的裝置上允許使用者 tooremember 多重要素驗證**方塊。
   ![記住裝置](./media/multi-factor-authentication-whats-next/remember.png)
4. 設定您想 tooallow hello 信任裝置 toobypass 雙步驟驗證的 hello 天數。 hello 預設值為 14 天。
5. 按一下 [儲存] 。
6. 按一下 [關閉] 。

### <a name="mark-a-device-as-trusted"></a>將裝置標示為受信任

一旦您啟用此功能，使用者可以在登入時勾選 [不再詢問]，將裝置標示為受信任。

![不再詢問 - 螢幕擷取畫面](./media/multi-factor-authentication-whats-next/trusted.png)

## <a name="selectable-verification-methods"></a>可選取的驗證方法
您可以選擇可供使用者使用的驗證方法。 hello 下表提供每個方法的簡短概觀。

當您的使用者為 MFA 註冊他們的帳戶時，他們可以選擇您已啟用 hello 選項超出其慣用的驗證方法。 hello 指導其註冊程序在講述[設定進行兩步驟驗證我的帳戶](multi-factor-authentication-end-user-first-time.md)

| 方法 | 說明 |
|:--- |:--- |
| 呼叫 toophone |撥打自動語音電話。 hello 使用者答案 hello 呼叫，並在 hello 電話數字鍵台 tooauthenticate 中按下 #。 此電話號碼不是已同步處理的 tooon 內部部署 Active Directory。 |
| 文字訊息 toophone |傳送包含驗證碼的簡訊。 hello 使用者是提示的 tooeither 回覆 toohello 文字訊息與 hello 驗證碼或 tooenter hello 驗證碼到 hello 登入介面。 |
| 行動應用程式的通知 |傳送推播通知 tooyour 電話或已註冊的裝置。 hello 使用者檢視 hello 通知，並選取**確認**toocomplete 驗證。 <br>hello Microsoft 驗證器應用程式是供[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)， [Android](http://go.microsoft.com/fwlink/?Linkid=825072)，和[IOS](http://go.microsoft.com/fwlink/?Linkid=825073)。 |
| 行動應用程式傳回的驗證碼 |hello Microsoft 驗證器應用程式會產生新的 OATH 代碼驗證每隔 30 秒。 hello 使用者會將此驗證碼輸入 hello 登入介面。<br>hello Microsoft 驗證器應用程式是供[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)， [Android](http://go.microsoft.com/fwlink/?Linkid=825072)，和[IOS](http://go.microsoft.com/fwlink/?Linkid=825073)。 |

### <a name="how-tooenabledisable-authentication-methods"></a>如何 tooenable/停用驗證方法
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 瀏覽每 hello 開頭的這篇文章的 hello 指示 toohello MFA 服務設定 頁面。
3. 在 hello 服務設定 頁面上，在驗證選項 下選取/取消選取您想 toouse hello 選項。
   ![驗證選項](./media/multi-factor-authentication-whats-next/authmethods.png)
4. 按一下 [儲存] 。
5. 按一下 [關閉] 。
