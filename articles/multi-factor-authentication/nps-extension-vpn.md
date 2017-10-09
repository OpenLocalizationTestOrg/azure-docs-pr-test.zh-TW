---
title: "使用 NPS 延伸模組的 Azure mfa aaaVPN 整合 |Microsoft 文件"
description: "這篇文章會討論與使用 Microsoft azure 的 hello 網路原則伺服器 (NPS) 延伸模組的 Azure MFA 整合您的 VPN 基礎結構。"
services: active-directory
keywords: "Azure MFA, 整合 VPN, Azure Active Directory, 網路原則伺服器擴充功能"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a>整合您的 VPN 基礎結構使用 Azure 的 hello 網路原則伺服器 (NPS) 擴充 Azure Multi-factor Authentication (MFA)

## <a name="overview"></a>概觀

hello azure 網路原則服務 」 (NPS) 延伸模組可讓組織使用 toosafeguard 遠端驗證撥號使用者服務 (RADIUS) 用戶端驗證雲端架構[Azure Multi-factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md)，提供兩步驟驗證。

本文章提供使用 Azure MFA 整合 hello NPS 基礎結構的指示，使用 Azure tooenable 安全的雙步驟驗證使用者使用 VPN tooconnect tooyour 網路的 hello NPS 延伸模組。 

hello 網路原則與存取服務 」 (NPS) 可讓組織 hello 下列能力：

* 指定 hello 管理和控制的網路要求 toospecify 可以連線，每天何時允許連線，連線，hello 持續時間和安全性的用戶端必須使用 tooconnect，並依此類推 hello 層級的中央的位置。 組織不必在每個 VPN 或遠端桌面 (RD) 閘道伺服器上指定這些原則，而是在中央位置一次指定這些原則。 使用 RADIUS 通訊協定 hello tooprovide hello 集中式驗證、 授權以及帳戶處理 (AAA)。 
* 建立並強制執行判斷裝置是否會授與不受限制或限制存取 toonetwork 資源的網路存取保護 (NAP) 用戶端健康原則。
* 提供表示 tooenforce 驗證和授權的存取 too802.1x 無線存取點及乙太網路交換器。    

如需詳細資訊，請參閱[網路原則伺服器 (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top)。 

tooenhance 安全性，並提供高層級的相容性，組織可以整合 NPS 使用使用者使用雙步驟驗證的 Azure MFA tooensure toobe 無法連線 toohello hello VPN 伺服器上的虛擬通訊埠。 針對使用者 toobe 授與存取權，他們必須提供其使用者名稱/密碼組合與 hello 使用者的資訊有其控制項中。 這項資訊必須能夠讓人信任且無法輕易複製，例如行動電話號碼、室內電話號碼、行動裝置上的應用程式等等。

先前 toohello 可用性的 hello azure NPS 擴充功能，客戶必須承擔更多的 tooimplement 雙步驟驗證整合 NPS 和 Azure MFA 環境有 tooconfigure 和維護個別的 MFA 伺服器在 hello 與內部部署環境中遠端桌面閘道和使用 RADIUS 的 Azure Multi-factor Authentication Server 中所述。

azure 的 hello NPS 擴充功能 hello 可用性現在可以讓組織 hello 選擇 toodeploy 在內部部署基礎 MFA 解決方案或以雲端為基礎 MFA 解決方案 toosecure RADIUS 用戶端驗證。
 
## <a name="authentication-flow"></a>驗證流程
當使用者連接 tooa VPN 伺服器上的虛擬通訊埠時，它們必須先通過驗證使用不同的通訊協定，允許 hello 使用使用者名稱/密碼和憑證型驗證方法的組合。 

在加法 tooauthenticating 與驗證身分識別，使用者必須擁有適當的撥入權限的 hello。 在簡單的實作中，直接在 hello Active Directory 使用者物件上設定這些電話撥入權限，以允許存取。 

 ![使用者屬性](./media/nps-extension-vpn/image1.png)

在簡單的實作中，每一部 VPN 伺服器都會根據每個本機 VPN 伺服器上所定義的原則來授與或拒絕存取權。

在較大且更靈活地實作 hello 原則該授與或拒絕 VPN 存取都集中在 RADIUS 伺服器上。 在此情況下，hello VPN 伺服器會做為存取伺服器 （RADIUS 用戶端），轉寄連線要求與帳戶訊息 tooa RADIUS 伺服器。 tooconnect toohello 虛擬通訊埠 hello VPN 伺服器上的，使用者必須先通過驗證，並符合 hello RADIUS 伺服器上集中所定義的條件。 

當以 hello NPS 整合 hello azure NPS 擴充功能時，hello 成功驗證流程如下所示：

1. hello VPN 伺服器接收包含 hello 使用者名稱和密碼 tooconnect tooa 資源，例如遠端桌面工作階段的 VPN 使用者的驗證要求。 
2. 做為 RADIUS 用戶端時，VPN 伺服器轉換 hello 要求 tooa RADIUS Access-request 訊息，並傳送 hello 訊息 （加密密碼） hello NPS 擴充功能安裝所在的 toohello RADIUS (NPS) 伺服器。 
3. hello 使用者名稱和密碼組合中 Active Directory 驗證。 如果 hello 使用者名稱 / 密碼不正確、 hello RADIUS 伺服器會傳送 Access-reject 訊息。 
4. 如果在指定的所有條件為 hello NPS 連線要求，並符合網路原則 (例如，時間一天或群組的成員資格的限制)，hello NPS 擴充觸發程序使用 Azure MFA 的次要驗證的要求。 
5. Azure MFA 與 Azure Active Directory 通訊、 擷取 hello 使用者詳細資料，然後執行 hello 次要驗證使用 hello hello 使用者 （簡訊、 行動裝置應用程式，等等） 所設定的方法。 
6. 成功時的 hello MFA 挑戰，Azure MFA 通訊 hello 結果 toohello NPS 擴充功能。
7. Hello 連線嘗試會同時驗證和授權之後，hello 擴充功能安裝所在的 hello NPS 伺服器會傳送 RADIUS Access-accept 訊息 toohello VPN 伺服器 （RADIUS 用戶端）。
8. hello 使用者已獲得存取 toohello 虛擬通訊埠 VPN 伺服器上的，建立加密的 VPN 通道。

## <a name="prerequisites"></a>必要條件
本節詳述 hello hello 遠端桌面閘道與整合 Azure MFA 之前所需的必要條件。 在開始之前，您必須擁有下列先決條件備妥的 hello。

* VPN 基礎結構
* 網路原則與存取服務 (NPS) 角色
* Azure MFA 授權
* Windows Server 軟體
* 程式庫
* 與內部部署 AD 同步的 Azure AD 
* Azure Active Directory GUID 識別碼

### <a name="vpn-infrastructure"></a>VPN 基礎結構
本文假設您有使用 Microsoft Windows Server 2016 就地工作 VPN 基礎結構，而且該 hello VPN 伺服器不目前是設定的 tooforward 連線要求 tooa RADIUS 伺服器。 本指南中，您將設定 hello VPN 基礎結構 toouse 中央的 RADIUS 伺服器。

如果您沒有就地工作基礎結構，您可以快速建立這個基礎結構提供許多您可以找到 hello Microsoft 和協力廠商站台的 VPN 安裝教學課程中的下列 hello 指導方針。 

### <a name="network-policy-and-access-services-nps-role"></a>網路原則與存取服務 (NPS) 角色

hello NPS 角色服務提供 hello RADIUS 伺服器和用戶端功能。 本文假設您已在成員伺服器或網域控制站上安裝 hello NPS 角色，您的環境中。 在本指南中，您要設定 RADIUS 以進行 VPN 設定。 在伺服器上安裝 hello NPS 角色_其他_比您的 VPN 伺服器。

如需有關安裝 hello NPS 角色服務的 Windows Server 2012 或更高版本，請參閱[安裝 NAP 健康原則伺服器](https://technet.microsoft.com/library/dd296890.aspx)。 Windows Server 2016 已淘汰網路存取原則 (NAP)。 如需 NPS，網域控制站上的包括 hello 建議 tooinstall NPS 的最佳作法的說明，請參閱[NPS 的最佳作法](https://technet.microsoft.com/library/cc771746)。

### <a name="licenses"></a>授權

需要 Azure MFA 的授權，此授權可透過 Azure AD Premium、Enterprise Mobility plus Security (EMS) 或 MFA 訂用帳戶來獲得。 如需詳細資訊，請參閱[如何 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)。 若要進行測試，您可以使用試用版訂用帳戶。

### <a name="software"></a>軟體

hello NPS 擴充功能需要 Windows Server 2008 R2 SP1 或更新版本已安裝的 hello NPS 角色服務。 使用 Windows Server 2016 中未執行本指南中的所有 hello 步驟。

### <a name="libraries"></a>程式庫

下列兩個程式庫的 hello 是必要的：

* [適用於 Visual Studio 2013 的 Visual C++ 可轉散發套件 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
* 適用於 Windows PowerShell 1.1.166.0 版或更新版本的 Microsoft Azure Active Directory 模組。 Hello 最新版本和安裝指示，請參閱[Microsoft Azure Active Directory PowerShell 模組版本發行歷程記錄](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx)。

這些程式庫不會封裝與 hello NPS 擴充功能安裝程式檔案 （版本 0.9.1.2），儘管現有文件集，否則為表示。 最少，您必須安裝 Visual Studio 2013 hello Visual c + + 可轉散發套件。 如果尚不存在，透過您 hello 安裝程序的一部分執行組態指令碼，會安裝 hello Microsoft Azure Active Directory 的 Windows PowerShell 模組。 沒有任何需要 tooinstall 事先本單元如果尚未安裝。

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>與內部部署 Active Directory 同步的 Azure Active Directory 

toouse hello NPS 擴充內部部署使用者必須向 Azure Active Directory 同步處理，並啟用 Multi-factor authentication。 本指南假設內部部署使用者已使用 AD Connect 來與 Azure Active Directory 保持同步。 下面會提供為使用者啟用 MFA 的指示。
如需 Azure AD Connect 的相關資訊，請參閱[整合您的內部部署目錄與 Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)。 

### <a name="azure-active-directory-guid-id"></a>Azure Active Directory GUID 識別碼 
tooinstall hello NPS，您需要 tooknow hello hello Azure Active Directory 的 GUID。 Hello 下一節中提供的指示尋找 hello hello Azure Active Directory 的 GUID。

## <a name="configure-radius-for-vpn-connections"></a>設定 RADIUS 的 VPN 連線

如果您已經安裝 hello NPS 伺服器角色的成員伺服器上，您會需要 tooconfigure tooauthenticate 並授權要求 VPN 連線的 VPN 用戶端。 

本節假設您已經安裝 hello 網路原則伺服器角色，但不是設定它使用基礎結構中。

>[!NOTE]
>如果您已擁有運作中的 VPN 伺服器，且使用集中式的 RADIUS 伺服器來進行驗證，則可以略過本節。
>

### <a name="register-server-in-active-directory"></a>在 Active Directory 中註冊伺服器
在此案例中正常運作的 toofunction，hello NPS 伺服器需要 toobe Active Directory 中登錄。

1. 開啟 [伺服器管理員]。
2. 在 伺服器管理員 中按一下 工具，然後按一下網路原則伺服器。 
3. 在 hello 網路原則伺服器主控台中，以滑鼠右鍵按一下**NPS （本機）**，然後按一下 **Active Directory 中的註冊伺服器**。 按 [確定] 兩次。

 ![網路原則伺服器](./media/nps-extension-vpn/image2.png)

4. 將 hello 主控台保持開啟以供 hello 下一個程序。

### <a name="use-wizard-tooconfigure-radius-server"></a>使用精靈 tooconfigure RADIUS 伺服器
您可以使用 （以精靈為基礎） 的標準或進階的組態選項 tooconfigure hello RADIUS 伺服器。 本節假設 hello 使用 hello 精靈為基礎的標準組態選項。

1. 在 hello 網路原則伺服器主控台中，按一下  **NPS （本機）**。
2. 選取 標準設定 底下的 撥號或 VPN 連線的 RADIUS 伺服器，然後按一下設定 VPN 或撥號。

 ![設定 VPN](./media/nps-extension-vpn/image3.png)

3. 在 hello 選取撥號或虛擬私人網路連線類型 頁面上，選取 **虛擬私人網路連線**，按一下**下一步**。

 ![虛擬私人網路](./media/nps-extension-vpn/image4.png)

4. 在 hello 指定撥號或 VPN 伺服器頁面上，按一下 **新增**。
5. 在 hello**新的 RADIUS 用戶端**對話方塊中，提供好記的名稱，輸入 hello 可解析名稱或 IP 位址 hello VPN 伺服器，並輸入共用密碼的密碼。 請為此共用祕密使用較長且複雜的形式。 記錄此密碼，您需要 hello 下一節中的步驟。

 ![新增 RADIUS 用戶端](./media/nps-extension-vpn/image5.png)

6. 按一下 [確定]，然後按 [下一步]。
7. 在 hello**設定驗證方法**頁面上，接受 hello 預設選取項目 (Microsoft 加密驗證版本 2 (Ms-chapv2)，或選擇另一個選項，然後按一下 **下一步**。

  >[!NOTE]
  >如果您設定可延伸的驗證通訊協定 (EAP)，則必須使用 MS CHAPv2 或 PEAP。 其他 EAP 皆不受支援。
 
8. 在 hello 指定使用者群組 頁面上，按一下 **新增**和選取適當的群組，如果有的話。 否則，保留空白 toogrant 存取 tooall 使用者 hello 選取項目。

 ![指定使用者群組](./media/nps-extension-vpn/image7.png)

9. 按一下 [下一步] 。
10. 在 hello 指定 IP 篩選器 頁面上，按一下 **下一步**。
11. 在 hello 指定加密設定 頁面上，接受 hello 預設設定，並按一下**下一步**。

 ![指定加密](./media/nps-extension-vpn/image8.png)

12. Hello 指定領域名稱，在 hello 名稱保留空白，接受 hello 預設設定，然後按一下**下一步**。

 ![指定領域名稱](./media/nps-extension-vpn/image9.png)

13. 在 hello 完成新增撥號或虛擬私人網路連線和 RADIUS 用戶端頁面上，按一下 **完成**。

 ![完成連線](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a>確認 RADIUS 設定
本節將詳細說明使用 hello 精靈所建立的 hello 組態。

1. 在 hello NPS 伺服器 hello NPS （本機） 主控台中，展開 RADIUS 用戶端，並選取**RADIUS 用戶端**。
2. 在 hello 詳細資料窗格中，以滑鼠右鍵按一下您使用精靈，建立 hello RADIUS 用戶端，然後按一下**屬性**。 您的 RADIUS 用戶端 （hello VPN 伺服器） 的 hello 屬性應該類似 toothose 如下所示。

 ![VPN 屬性](./media/nps-extension-vpn/image11.png)

3. 按一下 [取消]。
4. 在 hello NPS 伺服器 hello NPS （本機） 主控台中，展開 **原則**，然後選取**連線要求原則**。 您應該會看到類似下面的 hello 影像的 hello VPN 連線原則。

 ![連線要求](./media/nps-extension-vpn/image12.png)

5. 在 [原則] 底下選取 [網路原則]。 您應該類似下面的 hello 影像的虛擬私人網路 (VPN) 連線原則。

 ![網路屬性](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a>設定 VPN 伺服器 toouse RADIUS 驗證
在本節中，您可以設定 hello VPN 伺服器 toouse RADIUS 驗證。 本節假設您有工作中設定的 VPN 伺服器，但尚未設定 hello VPN 伺服器 toouse RADIUS 驗證。 設定後 hello VPN 伺服器，您可以確認您的組態如預期般。

>[!NOTE]
>如果您已擁有運作中的 VPN 伺服器設定，且該設定使用 RADIUS 驗證，則可以略過本節。
>

### <a name="configure-authentication-provider"></a>設定驗證提供者
1. 在 hello VPN 伺服器上，開啟 [伺服器管理員]。
2. 在 [伺服器管理員] 中按一下 [工具]，然後按一下 [路由及遠端存取]。
3. 在 hello 路由及遠端存取主控台中，以滑鼠右鍵按一下**\[伺服器名稱\]（本機）**，然後按一下**屬性**。

 ![路由及遠端存取](./media/nps-extension-vpn/image14.png)
 
4. 在 hello **[伺服器名稱} （本機） 屬性**對話方塊方塊中，按一下 hello**安全性**] 索引標籤。 
5. 在 [hello**安全性**索引標籤的驗證提供者] 下按一下**RADIUS 驗證**，，然後**設定**。

 ![RADIUS 驗證](./media/nps-extension-vpn/image15.png)
 
6. 在 hello RADIUS 驗證 對話方塊中，按一下 **新增**。
7. 在 hello 新增 RADIUS 伺服器，在 伺服器名稱，並將您設定 hello 前一節中的 hello RADIUS 伺服器 hello 名稱或 hello IP 位址。
8. 在 共用密碼，按一下 **變更**和加入 hello 的共用密碼建立，並記錄先前的密碼。
9. 在 逾時 （秒），變更 hello tooa 值之間**30**和**60**。 這是必要的 tooallow toocomplete hello 第二個驗證因素足夠時間。
 
 ![新增 RADIUS 伺服器](./media/nps-extension-vpn/image16.png)
 
10. 持續按 [確定]直到您徹底關閉所有對話方塊。

### <a name="test-vpn-connectivity"></a>測試 VPN 連線能力
在本節中，您會確認該 hello VPN 用戶端已驗證及授權 hello RADIUS 伺服器，當您嘗試 tooconnect tooVPN 虛擬通訊埠。 本節假設您使用 Windows 10 來作為 VPN 用戶端。 

>[!NOTE]
>如果您已設定 VPN 用戶端 tooconnect toohello VPN 伺服器，並已儲存的 hello 設定，您可以略過 hello 步驟相關的 tooconfiguring 並儲存 VPN 連線物件。
>

1. 在 VPN 用戶端電腦上按一下 [啟動]，然後按一下 [設定] \(齒輪圖示)。
2. 在 [視窗設定] 中按一下 [網路和網際網路]。
3. 按一下 [VPN]。
4. 按一下 [新增 VPN 連線]。
5. 在新增 VPN 連線，因為 hello VPN 提供者，然後完成 hello 其餘欄位，視需要指定 Windows （內建），然後按一下**儲存**。 

 ![新增 VPN 連線](./media/nps-extension-vpn/image17.png)
 
6. 開啟 hello**網路和共用中心**控制台 中。
7. 按一下 [變更介面卡設定]。

 ![變更介面卡設定](./media/nps-extension-vpn/image18.png)

8. 以滑鼠右鍵按一下 hello VPN 網路連線，然後按一下屬性。 

 ![VPN 網路屬性](./media/nps-extension-vpn/image19.png)

9. 在 [hello VPN 內容] 對話方塊中，按一下 [hello**安全性**] 索引標籤。 
10. 在 hello 安全性索引標籤上，確定只**Microsoft CHAP 版本 2 (MS-CHAP v2)**已選取，然後按一下 確定。

 ![允許通訊協定](./media/nps-extension-vpn/image20.png)

11. 以滑鼠右鍵按一下 hello VPN 連線，然後按一下**連接**。
12. 在 hello 設定頁面上，按一下 **連接**。

如下所示，成功的連線會出現在 hello 做為事件編號 6272，hello RADIUS 伺服器上的安全性記錄檔。

 ![事件屬性](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a>疑難排解指南
假設已使用 VPN 設定，才能設定 hello VPN 伺服器 toouse 集中式的 RADIUS 伺服器進行驗證和授權。 在此情況下，很可能 hello 問題可能因組態 hello RADIUS 伺服器或 hello 使用的使用者名稱無效或密碼不正確。 比方說，如果您在 hello 使用者名稱中使用 hello 替代的 UPN 尾碼，hello 登入嘗試可能會失敗 (您應該使用相同的帳戶名稱，為獲得最佳結果的 hello)。 

這些問題，理想的位置 toostart 位於 tooexamine hello 安全性事件記錄檔的 tootroubleshoot hello RADIUS 伺服器。 toosave 時間搜尋事件，您可以使用 hello 以角色為基礎網路原則與存取伺服器自訂檢視在事件檢視器，如下所示。 事件識別碼 6273 指出其中 hello 網路原則伺服器拒絕存取 tooa 使用者的事件。 

 ![事件檢視器](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a>設定 Multi-Factor Authentication
本節提供為使用者啟用 MFA 以及為帳戶設定雙步驟驗證的指示。 

### <a name="enable-multi-factor-authentication"></a>啟用 Multi-Factor Authentication
在本節中，您將為 Azure AD 帳戶啟用 MFA。 使用 hello**傳統入口網站**tooenable MFA 的使用者。 

1. 開啟瀏覽器，並瀏覽過[https://manage.windowsazure.com](https://manage.windowsazure.com)。 
2. Hello 系統管理員身分登入。
3. 在 hello 入口網站中 hello 左方導覽中，按一下**ACTIVE DIRECTORY**。

 ![預設目錄](./media/nps-extension-vpn/image23.png)

4. 在 hello NAME 欄位中，按一下 **預設目錄**（或另一個目錄，如果適當的話）。
5. 在 hello 快速入門 頁面上，按一下 **設定**。

 ![設定預設值](./media/nps-extension-vpn/image24.png)

6. 在 hello 設定頁面上，向下捲動並在 hello 多因素驗證 區段中，按一下 **管理服務設定**。

 ![管理 MFA 設定](./media/nps-extension-vpn/image25.png)
 
7. 在 hello 多因素驗證頁面上，檢閱 hello 預設服務設定，然後再按一下**使用者**。 

 ![MFA 使用者](./media/nps-extension-vpn/image26.png)
 
8. Hello 使用者在頁面上，選取您希望 tooenable MFA，然後按一下 hello 使用者**啟用**。

 ![屬性](./media/nps-extension-vpn/image27.png)
 
9. 出現提示時，按一下 [啟用多重要素驗證]。

 ![啟用 MFA](./media/nps-extension-vpn/image28.png)
 
10. 按一下 [關閉] 。 
11. 重新整理 hello 頁面。 hello MFA 狀態是已變更的 tooEnabled。

如需詳細資訊 tooenable 使用者進行多重要素驗證，請參閱[開始使用 Azure Multi-factor Authentication hello 定域機組中](multi-factor-authentication-get-started-cloud.md)。 

### <a name="configure-accounts-for-two-step-verification"></a>為帳戶設定雙步驟驗證
一旦帳戶已啟用 MFA，使用者不能 toosign 中 tooresources 由 hello MFA 原則，直到它們已經成功設定信任的裝置 toouse hello 在使用雙步驟驗證第二個驗證因素。

在本節中，您要設定受信任的裝置以供雙步驟驗證使用。 有幾個選項供您 tooconfigure 這些包括 hello 下列：

* **行動裝置應用程式**。 您在 Windows Phone、 Android 或 iOS 裝置上安裝 hello Microsoft 驗證器應用程式。 根據組織的原則，您會在兩種模式的其中一個必要的 toouse hello 應用程式： 接收通知的驗證 （將通知推送 tooyour 裝置），或使用的驗證碼 (需要 tooenter 驗證程式碼更新每隔 30 秒）。 
* **行動電話通話或文字**。 您會收到自動發出的來電或簡訊。 Hello 電話選項時，您可以回答 hello 呼叫，並按下 hello # 符號 tooauthenticate。 Hello 文字選項時，您可以回覆 toohello 文字訊息，或輸入 hello 登入介面的 hello 驗證碼。
* **辦公室電話通話**。 此程序是 hello 與自動撥打電話上面所述相同。

遵循下列指示來設定裝置 toouse hello 行動裝置應用程式 tooreceive 推播通知進行驗證。

1. 登入太[https://aka.ms/mfasetup](https://aka.ms/mfasetup)或任何站台，例如[https://portal.azure.com](https://portal.azure.com)，您必須有 tooauthenticate 使用啟用 MFA 的認證。 
2. 在登入您的使用者名稱和密碼，您會看到的畫面會提示您 tooset hello 進行額外安全性驗證的帳戶。

 ![額外的安全性](./media/nps-extension-vpn/image29.png)

3. 按一下 [立即設定]。
4. 在 hello 其他安全性驗證] 頁面上，選取 [連絡人類型 （驗證電話、 辦公室電話或行動裝置應用程式）。 然後選取國家或地區並選取方法。 hello 方法會因您所選取的連絡人類型。 例如，如果您選擇行動裝置應用程式，您可以選取是否驗證或驗證碼 toouse tooreceive 通知。 hello 遵循的步驟假設您選擇**行動裝置應用程式**hello 以連絡人類型。

 ![電話驗證](./media/nps-extension-vpn/image30.png)

5. 選取 [行動裝置應用程式]，按一下 [接收驗證通知]，然後按一下 [設定]。 

 ![行動裝置應用程式驗證](./media/nps-extension-vpn/image31.png)
 
6. 如果您尚未這樣做，請在裝置上安裝 hello authenticator 行動應用程式。 
7. 遵循 hello 行動裝置應用程式 tooscan hello 呈現列程式碼中的 hello 指示或手動輸入 hello 資訊，然後按一下**完成**。

 ![設定行動裝置應用程式](./media/nps-extension-vpn/image32.png)

8. 在 hello 其他安全性驗證 頁面上，按一下 **與我連絡**和回覆傳送 toonotification tooyour 裝置。
9. 在 hello 其他安全性驗證 頁面上，輸入萬一您遺失存取 toohello 行動裝置應用程式，然後按一下的連絡電話號碼**下一步**。

 ![行動電話號碼](./media/nps-extension-vpn/image33.png)
 
10. 在 hello 其他安全性驗證，按一下 **完成**。

hello 的裝置已設定的 tooprovide 第二種驗證方法。 如需為帳戶設定雙步驟驗證的相關資訊，請參閱[對我的帳戶進行雙步驟驗證設定](./end-user/multi-factor-authentication-end-user-first-time.md)。

## <a name="install-and-configure-nps-extension"></a>安裝和設定 NPS 擴充功能

本節提供設定以 hello VPN 伺服器的用戶端驗證的 VPN toouse Azure MFA 的指示。

一旦您安裝並設定 hello NPS 延伸模組，此伺服器所處理的所有 RADIUS 用戶端驗證都是必要的 toouse Azure MFA。 若未在 Azure MFA 中註冊您的所有 VPN 使用者，您可以設定另一個 RADIUS 伺服器 tooauthenticate 不是使用者設定的 toouse MFA。 或者，您可以建立登錄項目，第二個驗證因素，可讓挑戰使用者 tooprovide，才在 MFA 註冊。 

建立新的字串值，名為_中 HKLM\SOFTWARE\Microsoft\AzureMfa REQUIRE_USER_MATCH_，並將設定 hello 值 tooTRUE 或 FALSE。 

 ![需要使用者比對](./media/nps-extension-vpn/image34.png)
 
如果 hello 值組 tooTRUE 或未設定，所有驗證要求，都則主體 tooan MFA 挑戰。 為已註冊 MFA 的 toousers tooFALSE 設定 hello 值，如果發出 MFA 挑戰。 只使用 hello FALSE 設定在測試或實際執行環境中，在上架期間。

### <a name="acquire-azure-active-directory-guid-id"></a>取得 Azure Active Directory GUID 識別碼

Hello NPS 擴充功能的 hello 組態的一部分，您需要 toosupply 系統管理員認證和 Azure Active Directory 識別碼 hello Azure AD 租用戶。 hello 下列步驟顯示 tooget hello 租用戶的識別碼。

1. 登入 toohello 在 Azure 入口網站[https://portal.azure.com](https://portal.azure.com) hello Azure hello 全域管理員身分租用戶。
2. 在左瀏覽 hello，按一下 hello **Azure Active Directory**圖示。
3. 按一下 [內容] 。
4. toocopy 您的目錄識別碼 toohello 剪貼簿、 選取 hello**複製**圖示。
 
 ![目錄識別碼](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a>安裝 hello NPS 擴充功能
hello NPS 擴充功能需要 toobe 具有 hello 網路原則伺服器上安裝和存取服務 」 (NPS) 角色安裝和該函式做 hello RADIUS 伺服器，在您的設計。 請勿在您的遠端桌面伺服器上安裝 hello NPS 擴充功能。

1. 下載 hello NPS 擴充功能，從[https://aka.ms/npsmfa](https://aka.ms/npsmfa)。 
2. 將複製 hello 安裝程式可執行檔 (NpsExtnForAzureMfaInstaller.exe) toohello NPS 伺服器。
3. 在 hello NPS 伺服器上，按兩下**NpsExtnForAzureMfaInstaller.exe**。 出現提示時，按一下 [執行]。
4. 在 hello NPS 擴充功能的 Azure MFA 對話方塊中，檢閱 hello 軟體授權條款，請檢查**toohello 授權條款和條件，即表示我同意**，然後按一下**安裝**。

 ![NPS 擴充功能](./media/nps-extension-vpn/image36.png)
 
5. 在 hello NPS 擴充功能的 Azure MFA 對話方塊中，按一下 **關閉**。  

 ![設定成功](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Hello NPS 擴充功能的 PowerShell 指令碼以設定使用的憑證
tooensure 安全通訊和保證，您需要 tooconfigure 憑證以供 hello NPS 延伸模組。 hello NPS 元件包括 Windows PowerShell 指令碼，以設定 nps 使用的自我簽署的憑證。 

hello 指令碼會執行下列動作的 hello:

* 建立自我簽署憑證
* 將公開金鑰憑證 tooservice 上 Azure AD 主體產生關聯
* 存放區 hello hello 本機電腦存放區中的憑證
* 授與存取 toohello 憑證的私用金鑰 toohello 網路使用者
* 重新啟動網路原則伺服器服務

如果您想 toouse 您自己的憑證，您在 Azure AD 中，需要您憑證 toohello 服務主體的 tooassociate hello 公用等等。
toouse hello 指令碼提供與 Azure Active Directory 系統管理認證的 hello 副檔名和 hello 您之前複製的 Azure Active Directory 租用戶識別碼。 您用來安裝 hello NPS 擴充每個 NPS 伺服器上執行 hello 指令碼。

1. 開啟系統管理 Windows PowerShell 提示字元。
2. 在 hello PowerShell 提示字元中輸入_cd 'c:\Program Files\Microsoft\AzureMfa\Config'_，按**ENTER**。
3. 輸入 _.\AzureMfsNpsExtnConfigSetup.ps1_，然後按 **ENTER**。 
 * hello 指令碼會檢查 toosee hello Azure Active Directory PowerShell 模組安裝。 如果未安裝，hello 指令碼會安裝 hello 模組。
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. Hello 指令碼驗證的 hello PowerShell 模組的 hello 安裝之後，它會顯示 hello Azure Active Directory PowerShell 模組對話方塊。 在 [hello] 對話方塊中，輸入您的 Azure AD 系統管理員認證和密碼，然後按一下**登入**。 
 
 ![PowerShell 登入](./media/nps-extension-vpn/image39.png)
 
5. 出現提示時，貼上您先前複製 toohello 剪貼簿的 hello 租用戶識別碼，然後按**ENTER**。 

 ![租用戶識別碼](./media/nps-extension-vpn/image40.png)

6. hello 指令碼會建立自我簽署的憑證，並執行其他組態變更。 hello 輸出就像是 hello 映像，如下所示。

 ![自我簽署憑證](./media/nps-extension-vpn/image41.png)

7. Hello 伺服器重新開機。
 
### <a name="verify-configuration"></a>驗證組態
tooverify hello 組態中，您需要 tooestablish 與 VPN 伺服器的新 VPN 連線。 在成功地輸入您的認證進行主要驗證，hello VPN 連線等候 hello 次要驗證 toosucceed 才建立 hello 連線時，如下所示。 

 ![驗證設定](./media/nps-extension-vpn/image42.png)

如果您已成功驗證與您先前設定 Azure MFA 的 hello 次要驗證方法時，您必須連接的 toohello 資源。 不過，如果 hello 次要驗證不成功，則會被拒絕存取 tooresource。 

在下方 hello 驗證器 hello 範例 Windows phone 上的應用程式會是使用的 tooprovide hello 次要驗證。

 ![驗證帳戶](./media/nps-extension-vpn/image43.png)

您已成功驗證之後使用 hello 第二種方法，會授與存取 toohello 虛擬通訊埠 hello VPN 伺服器上。 不過，因為您很有必要的 toouse 行動裝置應用程式使用信任的裝置上的次要驗證方法，程序中的 hello 記錄是更安全，它會使用使用者名稱 / 密碼組合。

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>檢視事件檢視器記錄來找到成功的登入事件
tooview hello hello Windows 事件檢視器記錄檔中的成功登入事件，您可以發出下列 Windows PowerShell 命令 tooquery hello Windows 安全性記錄檔 hello NPS 伺服器上的 hello。

hello 安全性事件檢視器記錄檔、 tooquery 成功登入事件都會使用下列命令 hello
* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 

 ![安全性事件檢視器](./media/nps-extension-vpn/image44.png)
 
您也可以檢視 hello 安全性記錄檔或 hello 網路原則與存取服務自訂檢視，如下所示：

 ![網路原則存取](./media/nps-extension-vpn/image45.png)

Hello 在伺服器上安裝 hello NPS 擴充 Azure MFA 的位置，您可以找到事件檢視器應用程式記錄檔特定 toohello 延伸在**應用程式和服務 Logs\Microsoft\AzureMfa**。 

* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL

 ![事件數目](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a>疑難排解指南
如果 hello 組態無法如預期般運作，很好的起點 toostart tootroubleshoot 是 hello 使用者的 tooverify 設定的 toouse Azure MFA。 擁有 hello 使用者連接太[https://portal.azure.com](https://portal.azure.com)。如果他們收到次要驗證提示而且可以成功地完成驗證，您就可以排除 Azure MFA 設定不正確的可能性。

如果為 hello 使用者正在 Azure MFA，您應該檢閱 hello 相關事件記錄檔。 這些包括 hello 前一節中討論的 hello 安全性事件、 操作、 閘道和 Azure MFA 記錄。 

以下是安全性記錄的輸出範例，其中顯示了失敗登入事件 (事件識別碼 6273)：

 ![安全性記錄](./media/nps-extension-vpn/image47.png)

以下是從 hello AzureMFA 記錄檔的相關的事件：

 ![Azure MFA 記錄](./media/nps-extension-vpn/image48.png)

tooperform 進階疑難排解選項，請洽詢 hello NPS 資料庫格式記錄檔安裝 hello NPS 服務。 這些記錄檔會建立於 %SystemRoot%\System32\Logs 資料夾，並以逗號分隔文字檔的形式存在。 如需這些記錄檔的說明，請參閱[解譯 NPS 資料庫格式記錄檔](https://technet.microsoft.com/library/cc771748.aspx)。 

這些記錄檔中的 hello 項目是很困難 toointerpret 而不匯入至試算表或資料庫。 您可以找到數字的 IAS 剖析器線上 tooassist 中解譯 hello 記錄檔。 以下是 hello 輸出的其中一個這類可下載[共享軟體應用程式](http://www.deepsoftware.com/iasviewer): 

 ![共享軟體應用程式](./media/nps-extension-vpn/image49.png)

最後，如需其他疑難排解選項，您可以使用通訊協定分析器，例如 Wireshark 或 [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)。 hello Wireshark 從下列影像顯示 hello hello VPN 伺服器與 hello NPS 伺服器之間的 RADIUS 訊息。

 ![Microsoft Message Analyzer](./media/nps-extension-vpn/image50.png)

如需詳細資訊，請參閱[將現有的 NPS 基礎結構與 Azure Multi-Factor Authentication 整合](multi-factor-authentication-nps-extension.md)。  

## <a name="next-steps"></a>後續步驟
[如何 tooget Azure 多重要素驗證](multi-factor-authentication-versions-plans.md)

[使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server-rdg.md)

[整合您的內部部署目錄與 Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)

