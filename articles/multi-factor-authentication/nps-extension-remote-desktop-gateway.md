---
title: "aaaRemote 桌面閘道與 Azure MFA NPS 擴充功能的整合 |Microsoft 文件"
description: "這篇文章會討論與使用 Microsoft azure 的 hello 網路原則伺服器 (NPS) 延伸模組的 Azure MFA 整合您的遠端桌面閘道基礎結構。"
services: active-directory
keywords: "Azure MFA, 整合遠端桌面閘道, Azure Active Directory, 網路原則伺服器擴充功能"
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
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a>將您的遠端桌面閘道基礎結構使用 hello 網路原則伺服器 (NPS) 延伸模組和 Azure AD 整合

這篇文章詳細說明如何整合您的遠端桌面閘道基礎結構與 Azure Multi-factor Authentication (MFA) 使用 Microsoft azure 的 hello 網路原則伺服器 (NPS) 延伸模組。 

hello azure 網路原則服務 」 (NPS) 延伸模組可讓客戶 toosafeguard 遠端驗證撥號使用者服務 (RADIUS) 用戶端驗證使用 Azure 的雲端式[Multi-factor Authentication (MFA)](multi-factor-authentication.md)。 此解決方案可提供新增的第二層安全性 toouser 登入和交易的兩步驟驗證。

本文章提供整合 hello NPS 基礎結構使用 Azure MFA 的逐步指示，使用 Azure 的 hello NPS 擴充功能。 這可讓使用者 toolog tooa 遠端桌面閘道上的安全驗證。 

hello 網路原則與存取服務 」 (NPS) 可讓組織 hello 能力 toodo hello 下列：
* 藉由指定誰可以連線定義 hello 管理和控制的網路要求的中央位置，允許的連線，每天何時 hello 的連線的持續時間和 hello 層級的安全性，用戶端必須使用 tooconnect，依此類推。 組織不必在每個 VPN 或遠端桌面 (RD) 閘道伺服器上指定這些原則，而是在中央位置一次指定這些原則。 hello RADIUS 通訊協定提供 hello 集中式驗證、 授權以及帳戶處理 (AAA)。 
* 建立並強制執行判斷裝置是否會授與不受限制或限制存取 toonetwork 資源的網路存取保護 (NAP) 用戶端健康原則。
* 提供表示 tooenforce 驗證和授權的存取 too802.1x 無線存取點及乙太網路交換器。    

一般而言，使用 NPS (RADIUS) toosimplify 組織，和集中 VPN hello 管理原則。 不過，許多組織也使用 NPS toosimplify，並集中管理 hello RD 桌面連線授權原則 (RD Cap)。 

組織也可以使用 Azure MFA tooenhance 安全性整合 NPS，並提供高層級的相容性。 這有助於確保使用者建立雙步驟驗證 toolog toohello 遠端桌面閘道上。 針對使用者 toobe 授與存取權，他們必須提供其使用者名稱/密碼組合與 hello 使用者的資訊有其控制項中。 這項資訊必須能夠讓人信任且無法輕易複製，例如行動電話號碼、室內電話號碼、行動裝置上的應用程式等等。

先前 toohello 可用性的 hello azure NPS 擴充功能，客戶必須承擔更多的 tooimplement 雙步驟驗證整合 NPS 和 Azure MFA 環境有 tooconfigure 和維護個別的 MFA 伺服器在 hello 與內部部署環境中記載於[遠端桌面閘道和使用 RADIUS 的 Azure Multi-factor Authentication Server](multi-factor-authentication-get-started-server-rdg.md)。

azure 的 hello NPS 擴充功能 hello 可用性現在可以讓組織 hello 選擇 toodeploy 在內部部署基礎 MFA 解決方案或以雲端為基礎 MFA 解決方案 toosecure RADIUS 用戶端驗證。

## <a name="authentication-flow"></a>驗證流程

使用者 toobe 授與存取 toonetwork 資源，透過遠端桌面閘道，必須符合 hello 一個 RD 連線授權原則 (RD CAP) 和一個 RD 資源授權原則 (RD RAP) 中所指定的條件。 RD Cap 指定誰是授權的 tooconnect tooRD 閘道。 RD Rap 指定 hello 網路資源，例如遠端桌面或遠端的應用程式，該 hello 允許使用者 tooconnect toothrough hello RD 閘道。 

RD 閘道可以設定的 toouse RD Cap 的集中原則存放區。 RD Rap 無法使用集中原則，在處理 hello RD 閘道上。 舉例來說，RD 閘道設定 toouse RD Cap 的集中原則存放區是 RADIUS 用戶端 tooanother NPS 伺服器做為 hello 中央原則存放區。

NPS 擴充 azure hello 與 hello NPS 和遠端桌面閘道整合時，hello 成功驗證流程如下所示：

1. hello 遠端桌面閘道伺服器會收到的驗證要求，從遠端桌面使用者 tooconnect tooa 資源，例如遠端桌面工作階段。 做為 RADIUS 用戶端時，hello 遠端桌面閘道伺服器 hello 要求 tooa RADIUS Access-request 訊息轉換，並將傳送 hello 訊息 toohello RADIUS (NPS) 伺服器 hello NPS 擴充功能的安裝位置。 
2. hello 使用者名稱和密碼組合 Active Directory 中驗證而且 hello 使用者驗證。
3. 如果所有 hello 中所指定的條件 hello NPS 連線要求，並符合 hello 網路原則 (例如，時間一天或群組的成員資格的限制)，hello NPS 擴充觸發程序使用 Azure MFA 的次要驗證的要求。 
4. Azure MFA 與 Azure AD 通訊、 擷取 hello 使用者詳細資料，然後執行 hello 次要驗證使用 hello hello 使用者 （簡訊、 行動裝置應用程式，等等） 所設定的方法。 
5. 成功時的 hello MFA 挑戰，Azure MFA 通訊 hello 結果 toohello NPS 擴充功能。
6. hello 擴充功能安裝所在的 hello NPS 伺服器會傳送 hello RD CAP 原則 toohello 遠端桌面閘道伺服器的 RADIUS 存取接受訊息。
7. hello 使用者被授與存取 toohello 要求透過 hello RD 閘道的網路資源。

## <a name="prerequisites"></a>必要條件
本節詳述 hello hello 遠端桌面閘道與整合 Azure MFA 之前所需的必要條件。 在開始之前，您必須擁有下列先決條件備妥的 hello。  

* 遠端桌面服務 (RDS) 基礎結構
* Azure MFA 授權
* Windows Server 軟體
* 網路原則與存取服務 (NPS) 角色
* 與內部部署 AD 同步的 Azure AD 
* Azure Active Directory GUID 識別碼

### <a name="remote-desktop-services-rds-infrastructure"></a>遠端桌面服務 (RDS) 基礎結構
您必須備妥中運作中的遠端桌面服務 (RDS) 基礎結構。 如果不這麼做，您可以在 Azure 中快速建立這個基礎結構，然後使用 hello 下列快速入門範本：[建立遠端桌面工作階段集合部署](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment)。 

如果您想 toomanually 建立內部 RDS 基礎結構快速基於測試目的，後續 hello 步驟 toodeploy 其中一個。 
**深入了解**：[使用 Azure 快速入門部署 RDS](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure)和[基本 RDS 基礎結構部署](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure)。 

### <a name="licenses"></a>授權
需要 Azure MFA 的授權，此授權可透過 Azure AD Premium、Enterprise Mobility plus Security (EMS) 或 MFA 訂用帳戶來獲得。 如需詳細資訊，請參閱[如何 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)。 若要進行測試，您可以使用試用版訂用帳戶。

### <a name="software"></a>軟體
hello NPS 擴充功能需要 Windows Server 2008 R2 SP1 或更新版本已安裝的 hello NPS 角色服務。 使用 Windows Server 2016 中未執行本節中的所有 hello 步驟。

### <a name="network-policy-and-access-services-nps-role"></a>網路原則與存取服務 (NPS) 角色
hello NPS 角色服務提供 hello RADIUS 伺服器和用戶端功能以及網路存取原則的健全狀況服務。 此角色必須安裝在您的基礎結構中的至少兩部電腦上： hello 遠端桌面閘道，而另一個成員伺服器或網域控制站。 根據預設，hello 角色已經設定為遠端桌面閘道 hello hello 電腦上。  您必須也 hello NPS 角色上安裝至少另一部電腦，例如網域控制站或成員伺服器上。

如需有關安裝 hello NPS 角色服務的 Windows Server 2012 或較舊，請參閱[安裝 NAP 健康原則伺服器](https://technet.microsoft.com/library/dd296890.aspx)。 如需 NPS，網域控制站上的包括 hello 建議 tooinstall NPS 的最佳作法的說明，請參閱[NPS 的最佳作法](https://technet.microsoft.com/library/cc771746)。

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>與內部部署 Active Directory 同步的 Azure Active Directory 
toouse hello NPS 擴充內部必須與 Azure AD 進行同步處理並啟用 MFA 的使用者。 這一節假設內部部署使用者已使用 AD Connect 來與 Azure AD 保持同步。 如需 Azure AD Connect 的相關資訊，請參閱[整合您的內部部署目錄與 Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)。 

### <a name="azure-active-directory-guid-id"></a>Azure Active Directory GUID 識別碼
tooinstall NPS，您需要 tooknow hello hello Azure AD 的 GUID。 下面將提供指示來尋找 hello hello Azure AD 的 GUID。

## <a name="configure-multi-factor-authentication"></a>設定 Multi-Factor Authentication 
本節中的 hello 遠端桌面閘道與整合 Azure MFA 的指示。 身為管理員，您必須設定 hello Azure MFA 服務之前，使用者可以自行註冊其多因素裝置或應用程式。

中的 hello 步驟[開始使用 Azure Multi-factor Authentication hello 定域機組中](multi-factor-authentication-get-started-cloud.md)tooenable MFA 為您的 Azure AD 使用者。 

### <a name="configure-accounts-for-two-step-verification"></a>為帳戶設定雙步驟驗證
一旦帳戶已啟用 MFA，您無法登入 tooresources 由 hello MFA 原則之前的第二個驗證因素 hello 已通過驗證，使用兩步驟驗證，您已成功設定信任的裝置 toouse。

中的 hello 步驟[Azure Multi-factor Authentication 什麼適合我？](./end-user/multi-factor-authentication-end-user.md) toounderstand 並正確設定 MFA 的裝置與您的使用者帳戶。

## <a name="install-and-configure-nps-extension"></a>安裝和設定 NPS 擴充功能
本節提供設定以 hello 遠端桌面閘道用戶端驗證的 RDS 基礎結構 toouse Azure MFA 的指示。

### <a name="acquire-azure-active-directory-guid-id"></a>取得 Azure Active Directory GUID 識別碼

Hello NPS 擴充功能的 hello 組態的一部分，您需要 toosupply 系統管理員認證和 hello Azure AD 識別碼的 Azure AD 租用戶。 下列步驟的 hello 顯示您 tooget hello 租用戶的識別碼。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello Azure hello 全域管理員身分租用戶。
2. 在左瀏覽 hello，選取 hello **Azure Active Directory**圖示。
3. 選取 [屬性] 。
4. 在 hello 屬性刀鋒視窗中，目錄識別碼 hello 旁邊按一下 hello**複製**圖示，如下所示 toocopy hello 識別碼 tooclipboard。

 ![屬性](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a>安裝 hello NPS 擴充功能
具有 hello 網路原則與存取服務 」 (NPS) 角色安裝在伺服器上安裝 hello NPS 擴充功能。 這項功能可以為您的設計 hello RADIUS 伺服器。 

>[!Important]
> 請確定您沒有遠端桌面閘道伺服器上安裝 hello NPS 擴充功能。
> 

1. 下載 hello [NPS 擴充](https://aka.ms/npsmfa)。 
2. 將複製 hello 安裝程式可執行檔 (NpsExtnForAzureMfaInstaller.exe) toohello NPS 伺服器。
3. 在 hello NPS 伺服器上，按兩下**NpsExtnForAzureMfaInstaller.exe**。 出現提示時，按一下 [執行]。
4. 在 hello NPS 擴充功能的 Azure MFA 對話方塊中，檢閱 hello 軟體授權條款，請檢查**toohello 授權條款和條件，即表示我同意**，然後按一下**安裝**。
 
  ![Azure MFA 設定](./media/nps-extension-remote-desktop-gateway/image2.png)

5. 在 hello NPS 擴充功能的 Azure MFA 對話方塊中，按一下 [關閉]。 

  ![Azure MFA 的 NPS 擴充功能](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Hello NPS 擴充功能的 PowerShell 指令碼以設定使用的憑證
接下來，您需要使用 hello NPS 擴充 tooensure 安全通訊和保證的 tooconfigure 憑證。 hello NPS 元件包括 Windows PowerShell 指令碼，以設定 nps 使用的自我簽署的憑證。 

hello 指令碼會執行下列動作的 hello:

* 建立自我簽署憑證
* 將公開金鑰憑證 tooservice 上 Azure AD 主體產生關聯
* 存放區 hello hello 本機電腦存放區中的憑證
* 授與存取 toohello 憑證的私用金鑰 toohello 網路使用者
* 重新啟動網路原則伺服器服務

如果您想 toouse 您自己的憑證，您在 Azure AD 中，需要您憑證 toohello 服務主體的 tooassociate hello 公用等等。

toouse hello 指令碼會使用您的 Azure AD 系統管理員認證提供 hello 副檔名和 hello 您之前複製的 Azure AD 租用戶識別碼。 Hello NPS 擴充功能安裝在每個 NPS 伺服器上執行 hello 指令碼。 然後 hello 遵循：

1. 開啟系統管理 Windows PowerShell 提示字元。
2. 在 hello PowerShell 提示字元中輸入**cd 'c:\Program Files\Microsoft\AzureMfa\Config'**，按**ENTER**。
3. 輸入 _.\AzureMfsNpsExtnConfigSetup.ps1_，然後按 **ENTER**。 hello 指令碼會檢查 toosee hello Azure Active Directory PowerShell 模組安裝。 如果未安裝，hello 指令碼會安裝 hello 模組。

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. Hello 指令碼驗證的 hello PowerShell 模組的 hello 安裝之後，它會顯示 hello Azure Active Directory PowerShell 模組對話方塊。 在 [hello] 對話方塊中，輸入您的 Azure AD 系統管理員認證和密碼，然後按一下**登入**。

  ![開啟 Powershell 帳戶](./media/nps-extension-remote-desktop-gateway/image5.png)

5. 出現提示時，貼上您先前複製 toohello 剪貼簿的 hello 租用戶識別碼，然後按**ENTER**。

  ![輸入租用戶識別碼](./media/nps-extension-remote-desktop-gateway/image6.png)

6. hello 指令碼會建立自我簽署的憑證，並執行其他組態變更。 hello 輸出應類似如下所示的 hello 影像。

  ![自我簽署憑證](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a>設定遠端桌面閘道上的 NPS 元件
在本節中，您可以設定 hello 遠端桌面閘道連線授權原則和其他 RADIUS 設定。

hello 驗證流程要求，RADIUS 訊息交換之間 hello 遠端桌面閘道和 hello NPS 伺服器 hello NPS 伺服器的安裝位置。 這表示，您必須設定 RADIUS 用戶端 hello NPS 擴充功能安裝所在的遠端桌面閘道和 hello NPS 伺服器上。 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a>設定遠端桌面閘道連線授權原則 toouse 中央存放區
遠端桌面連線授權原則 (RD Cap) 指定連線 tooa 遠端桌面閘道伺服器 hello 需求。 RD CAP 可以儲存在本機 (預設值)，也可以儲存在執行 NPS 的中央 RD CAP 存放區中。 Azure MFA 與 RDS tooconfigure 整合，您需要 toospecify hello 中央存放區使用。

1. Hello RD 閘道伺服器上，開啟**伺服器管理員**。 
2. 在 [hello] 功能表上按一下**工具**，點太**遠端桌面服務**，然後按一下**遠端桌面閘道管理員**。

  ![遠端桌面服務問題](./media/nps-extension-remote-desktop-gateway/image8.png)

3. 在 hello RD 閘道管理員，以滑鼠右鍵按一下**\[伺服器名稱\]（本機）**，按一下**屬性**。

  ![伺服器名稱](./media/nps-extension-remote-desktop-gateway/image9.png)

4. 在 hello 內容 對話方塊中，選取 hello **RD CAP**存放區索引標籤。
5. 在 hello RD CAP 存放區索引標籤上，選取 **執行 NPS 的中央伺服器**。 
6. 在 hello**輸入 hello 執行 NPS 的伺服器名稱或 IP 位址**欄位中，輸入 hello IP 位址或伺服器名稱的 hello 伺服器 hello NPS 擴充功能的安裝位置。

  ![輸入名稱或 IP 位址](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. 按一下 [新增] 。
8. 在 hello**共用密碼**對話方塊中，輸入共用的密碼，然後按一下**確定**。 請確定您記錄這個共用的密碼，並安全地儲存 hello 記錄。

 >[!NOTE]
 >共用的密碼可用 tooestablish hello RADIUS 伺服器與用戶端之間的信任。 建立長而複雜的密碼。
 >

 ![共用祕密](./media/nps-extension-remote-desktop-gateway/image11.png)

9. 按一下**確定**tooclose hello 對話方塊。

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a>在遠端桌面閘道 NPS 上設定 RADIUS 逾時值
那里的 tooensure 時間 toovalidate 使用者的認證、 執行雙步驟驗證、 接收回應，並回應 tooRADIUS 訊息，則是必要的 tooadjust hello RADIUS 逾時值。

1. Hello RD 閘道伺服器上，在 [伺服器管理員] 中，按一下**工具**，然後按一下**網路原則伺服器**。 
2. 在 hello **NPS （本機）**主控台中，展開**RADIUS 用戶端和伺服器**，然後選取**遠端 RADIUS 伺服器**。

 ![遠端 RADIUS 伺服器](./media/nps-extension-remote-desktop-gateway/image12.png)

3. 在 [hello] 詳細資料窗格中，按兩下**TS GATEWAY SERVER GROUP**。

 >[!NOTE]
 >當您設定 NPS 原則 hello 中央伺服器建立此 RADIUS 伺服器群組。 hello RD 閘道轉送 RADIUS 訊息 toothis 伺服器或伺服器群組，超過一個 hello 群組中。
 >

4. 在 [hello **TS 閘道伺服器群組內容**] 對話方塊中，選取 hello IP 位址或名稱的 hello 設定 toostore RD Cap 的 NPS 伺服器，然後按一下**編輯**。 

 ![TS Gateway Server Group](./media/nps-extension-remote-desktop-gateway/image13.png)

5. 在 [hello**編輯 RADIUS 伺服器**對話方塊中，選取 hello**負載平衡**] 索引標籤。
6. 在 hello**負載平衡**索引標籤上，在 hello**卸除的要求都視為前，無回應的秒數**欄位中，變更 hello 預設 3 tooa 值介於 30 到 60 秒。
7. 在 hello**伺服器被識別為無法使用時，在要求之間的秒數**欄位中，變更 hello 預設值是 30 秒 tooa 值，這個值會等於 tooor 大於 hello hello 先前步驟中所指定的值。

 ![編輯 Radius 伺服器](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  按一下 [確定] 兩個時間 tooclose hello 對話方塊。

### <a name="verify-connection-request-policies"></a>驗證連線要求原則 
根據預設，當您設定 hello RD 閘道 toouse 中央原則存放區的連線授權原則，hello RD 閘道是設定的 tooforward CAP 要求 toohello NPS 伺服器。 hello Azure MFA 副檔名 hello NPS 伺服器安裝程序 hello RADIUS 存取要求。 hello 下列步驟顯示如何 tooverify hello 預設連線要求原則。 

1. 在 hello RD 閘道在 hello NPS （本機） 主控台中，展開 **原則**，然後選取**連線要求原則**。
2. 以滑鼠右鍵按一下 [連線要求原則]，然後連按兩下 [TS GATEWAY AUTHORIZATION POLICY]。
3. 在 [hello **TS GATEWAY AUTHORIZATION POLICY 屬性**對話方塊方塊中，按一下 hello**設定**] 索引標籤。
4. 在 [設定] 索引標籤上，按一下 [轉送連線要求] 之下的 [驗證]。 RADIUS 用戶端可設定的 tooforward 要求驗證。

 ![驗證設定](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. 按一下 [取消]。 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a>Hello hello NPS 擴充功能安裝所在的伺服器上設定 NPS
hello NPS 伺服器的 hello NPS 擴充功能安裝的需求 toobe 無法 tooexchange 具有 hello hello 遠端桌面閘道上的 NPS 伺服器的 RADIUS 訊息。 tooenable 此訊息交換，您需要 tooconfigure hello NPS 元件 hello hello NPS 擴充服務安裝所在的伺服器上。 

### <a name="register-server-in-active-directory"></a>在 Active Directory 中註冊伺服器
在此案例中正常運作的 toofunction，hello NPS 伺服器需要 toobe Active Directory 中登錄。

1. 開啟 [伺服器管理員] 。
2. 在 伺服器管理員 中按一下 工具，然後按一下網路原則伺服器。 
3. 在 hello 網路原則伺服器主控台中，以滑鼠右鍵按一下**NPS （本機）**，然後按一下 **Active Directory 中的註冊伺服器**。 
4. 按 [確定] 兩次。

 ![在 AD 中註冊伺服器](./media/nps-extension-remote-desktop-gateway/image16.png)

5. 將 hello 主控台保持開啟以供 hello 下一個程序。

### <a name="create-and-configure-radius-client"></a>建立及設定 RADIUS 用戶端 
hello 遠端桌面閘道需要 toobe 設定為 RADIUS 用戶端 toohello NPS 伺服器。 

1. Hello NPS 擴充功能已安裝在 hello hello NPS 伺服器上**NPS （本機）**主控台中，以滑鼠右鍵按一下**RADIUS 用戶端**按一下**新增**。

 ![新增 RADIUS 用戶端](./media/nps-extension-remote-desktop-gateway/image17.png)

2. 在 hello**新的 RADIUS 用戶端**對話方塊方塊中，提供易記的名稱，例如_閘道_，和 hello IP 位址或 hello 遠端桌面閘道伺服器的 DNS 名稱。 
3. 在 hello**共用密碼**和 hello**確認共用的密碼**欄位中，輸入 hello 使用之前所用的相同密碼。

 ![名稱和位址](./media/nps-extension-remote-desktop-gateway/image18.png)

4. 按一下**確定**tooclose hello 新的 RADIUS 用戶端 對話方塊。

### <a name="configure-network-policy"></a>設定網路原則
回收 hello NPS 伺服器 hello Azure MFA 延伸模組是 hello 連線授權原則 (CAP) 的 hello 指定集中原則存放區。 因此，您需要 tooimplement 端點上 hello NPS 伺服器 tooauthorize 有效的連接要求。  

1. 在 hello NPS （本機） 主控台中，展開**原則**，然後按一下**網路原則**。
2. 以滑鼠右鍵按一下**連線 tooother 存取伺服器**，然後按一下**重複原則**。 

 ![複製原則](./media/nps-extension-remote-desktop-gateway/image19.png)

3. 以滑鼠右鍵按一下**複本的連接 tooother 存取伺服器**，然後按一下**屬性**。

 ![網路屬性](./media/nps-extension-remote-desktop-gateway/image20.png)

4. 在 hello**複本的連接 tooother 存取伺服器**對話方塊中，在 原則名稱，輸入適當的名稱，例如**RDG_CAP**。 勾選 [啟用原則]，然後選取 [授與存取權]。 (選擇性) 在 [網路存取類型] 中選取 [遠端桌面閘道]，您也可以將它保留為 [未指定]。

 ![複製連線](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  按一下 hello**條件約束**索引標籤，然後檢查**沒有交涉驗證方法仍然允許用戶端 tooconnect**。

 ![允許用戶端 tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. （選擇性） 按一下 hello**條件**索引標籤和加入的 hello 連接 toobe 獲授權，例如，特定的 Windows 群組成員資格，必須符合的條件。

 ![條件](./media/nps-extension-remote-desktop-gateway/image23.png)

7. 按一下 [確定] 。 當提示的 tooview hello 對應的說明主題時，按一下 **否**。
8. 請確定您的新原則 hello hello 清單頂端，確定已啟用 hello 原則，而且它會授與存取權。

 ![網路原則](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a>驗證組態
tooverify hello 組態，您需要 toolog hello 遠端桌面閘道上的都有適合的 RDP 用戶端。 是確定 toouse 允許由您的連線授權原則，且已啟用 Azure MFA 的帳戶。 

Hello 圖所顯示，您可以使用 hello**遠端桌面 Web 存取**頁面。

![遠端桌面 Web 存取](./media/nps-extension-remote-desktop-gateway/image25.png)

在成功地輸入您的認證進行主要驗證，hello 遠端桌面連線 對話方塊會顯示起始遠端連線，狀態，如下所示。 

如果您已成功驗證與您先前設定 Azure MFA 的 hello 次要驗證方法時，您必須連接的 toohello 資源。 不過，如果 hello 次要驗證不成功，則會被拒絕存取 tooresource。 

![起始遠端連線](./media/nps-extension-remote-desktop-gateway/image26.png)

在下方 hello 驗證器 hello 範例 Windows phone 上的應用程式會是使用的 tooprovide hello 次要驗證。

![帳戶](./media/nps-extension-remote-desktop-gateway/image27.png)

已成功驗證使用 hello 次要驗證方法，一旦您已登入 hello 遠端桌面閘道，像平常一樣。 不過，因為您不需要的 toouse 行動裝置應用程式使用信任的裝置上的次要驗證方法時，會更安全，否則會比 hello 登入程序。

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>檢視事件檢視器記錄來找到成功的登入事件
tooview hello 成功登入事件 hello Windows 事件檢視器記錄檔中的，您可以發出下列 Windows PowerShell 命令 tooquery hello Windows 終端機服務和 Windows 安全性記錄檔的 hello。

tooquery 成功登入事件 hello 閘道操作記錄檔中的_(事件 Viewer\Applications 和服務 Logs\Microsoft\Windows\TerminalServices Gateway\Operational_，使用下列命令的 hello:

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL 
* 此命令會顯示顯示 hello 使用者符合資源授權原則需求 (RD RAP)，並已授與存取的 Windows 事件。

![檢視事件檢視器](./media/nps-extension-remote-desktop-gateway/image28.png)

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL
* 此命令會顯示 hello 使用者遇到連線授權原則的需求時顯示的事件。

![連線授權](./media/nps-extension-remote-desktop-gateway/image29.png)

您也可以檢視此記錄並依據事件識別碼 (300 和 200) 進行篩選。 hello 安全性事件檢視器記錄檔、 tooquery 成功登入事件都會使用下列命令的 hello:

* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 
* 此命令可以執行在 hello 中央 NPS 或 hello RD 閘道伺服器。 

![成功的登入事件](./media/nps-extension-remote-desktop-gateway/image30.png)

您也可以檢視 hello 安全性記錄檔或 hello 網路原則與存取服務自訂檢視，如下所示：

![網路原則與存取服務](./media/nps-extension-remote-desktop-gateway/image31.png)

Hello 在伺服器上安裝 hello NPS 擴充 Azure MFA 的位置，您可以找到事件檢視器應用程式記錄檔特定 toohello 延伸在_應用程式和服務 Logs\Microsoft\AzureMfa_。 

![事件檢視器應用程式記錄](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a>疑難排解指南

Hello 組態無法如預期般運作，如果第一個位置 toostart tootroubleshoot hello 是 hello 使用者的 tooverify 設定的 toouse Azure MFA。 擁有 hello 使用者連接 toohello [Azure 入口網站](https://portal.azure.com)。 如果使用者收到次要驗證提示而且可以成功地完成驗證，您就可以排除 Azure MFA 設定不正確的可能性。

如果為 hello 使用者正在 Azure MFA，您應該檢閱 hello 相關事件記錄檔。 這些包括 hello 前一節中討論的 hello 安全性事件、 操作、 閘道和 Azure MFA 記錄。 

以下是安全性記錄的輸出範例，其中顯示了失敗登入事件 (事件識別碼 6273)。

![失敗的登入事件](./media/nps-extension-remote-desktop-gateway/image33.png)

以下是從 hello AzureMFA 記錄檔的相關的事件：

![Azure MFA 記錄](./media/nps-extension-remote-desktop-gateway/image34.png)

tooperform 進階疑難排解選項，請洽詢 hello NPS 資料庫格式記錄檔安裝 hello NPS 服務。 這些記錄檔會建立於 %SystemRoot%\System32\Logs 資料夾，並以逗號分隔文字檔的形式存在。 

如需這些記錄檔的說明，請參閱[解譯 NPS 資料庫格式記錄檔](https://technet.microsoft.com/library/cc771748.aspx)。 這些記錄檔中的 hello 項目可以是很困難 toointerpret 而不匯入至試算表或資料庫。 您可以找到數個 IAS 剖析器線上 tooassist 中解譯 hello 記錄檔。 

hello 下方影像顯示 hello 輸出的其中一個這類可下載[共享軟體應用程式](http://www.deepsoftware.com/iasviewer)。 

![共享軟體應用程式](./media/nps-extension-remote-desktop-gateway/image35.png)

最後，如需其他疑難排解選項，您可以使用通訊協定分析器，例如 [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)。 

hello 從 Microsoft Message Analyzer 下的圖顯示篩選包含 hello 使用者名稱的 RADIUS 通訊協定上的網路流量**Contoso\AliceC**。

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a>後續步驟
[如何 tooget Azure 多重要素驗證](multi-factor-authentication-versions-plans.md)

[使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server-rdg.md)

[整合您的內部部署目錄與 Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)
