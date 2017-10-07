---
title: "aaaGetting 啟動 Azure Multi-factor Authentication Server |Microsoft 文件"
description: "這是描述 tooget 如何開始使用 Azure MFA Server hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
keywords: "驗證伺服器, azure multi factor authentication 應用程式啟動頁面, 驗證伺服器下載"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Hello Azure Multi-factor Authentication Server 使用者入門

<center>![MFA 內部部署](./media/multi-factor-authentication-get-started-server/server2.png)</center>

既然我們判定 toouse 內部 Multi-factor Authentication Server，讓我們開始。 此頁面涵蓋 hello 伺服器並設定與內部部署 Active Directory 的新安裝。 如果您已經安裝 hello MFA server，並尋找 tooupgrade，請參閱[升級 toohello 最新的 Azure Multi-factor Authentication Server](multi-factor-authentication-server-upgrade.md)。 如果您想要尋求安裝只 hello web 服務的詳細資訊，請參閱[部署 hello Azure Multi-factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md)。

## <a name="plan-your-deployment"></a>規劃您的部署

下載 hello Azure Multi-factor Authentication Server 之前，請考慮您的負載和高可用性需求為何。 使用此資訊 toodecide 方式和位置 toodeploy。

最好定期 hello 所需的記憶體數量是使用者的 hello 數目預期 tooauthenticate。

| 使用者 | RAM |
| ----- | --- |
| 1-10,000 | 4 GB |
| 10,001-50,000 | 8 GB |
| 50,001-100,000 | 12 GB |
| 100,000-200,001 | 16 GB |
| 200,001+ | 32 GB |

需要 tooset 的多部伺服器的高可用性或負載平衡嗎？ 有多種方式 tooset 此組態使用 Azure MFA Server。 當您安裝您的第一個 Azure MFA Server 時，它會變成 hello master。 任何其他伺服器會變成從屬，及自動同步處理使用者和組態 hello 主機。 然後，您可以在 設定一部主要伺服器，然後利用 hello rest 做為備份，或者您可以設定負載平衡 hello 的所有伺服器之間。

Azure MFA Server 的主機離線時，hello 次級伺服器仍然可以處理兩步驟驗證要求。 不過，您無法加入新的使用者和現有的使用者之前，無法更新其設定 hello 主機已上線，或取得升級部屬。

### <a name="prepare-your-environment"></a>準備您的環境

請確定您使用 Azure Multi-factor authentication 的 hello 伺服器符合下列需求的 hello:

| Azure Multi-Factor Authentication Server 需求 | 說明 |
|:--- |:--- |
| 硬體 |<li>200 MB 的硬碟空間</li><li>具有 x32 或 x64 功能的處理器</li><li>1 GB 或更高的 RAM</li> |
| 軟體 |<li>Windows Server 2008 或更新版本，如果 hello 主機伺服器 OS</li><li>Windows 7 或更新版本，如果 hello 主機作業系統的用戶端</li><li>Microsoft .NET 4.0 Framework</li><li>IIS 7.0 或更新版本，如果安裝 hello 使用者入口網站或 web 服務 SDK</li> |

### <a name="azure-mfa-server-components"></a>Azure MFA Server 元件

構成 Azure MFA Server 的 Web 元件有三個：

* Web 服務 SDK 層啟用與通訊 hello 其他元件和 hello Azure MFA 應用程式伺服器上已安裝
* 使用者入口網站的 IIS 網站，允許使用者 tooenroll Azure Multi-factor Authentication (MFA)，並維護自己的帳戶。
* 行動應用程式 Web 服務-可讓您使用行動裝置的應用程式，例如 hello Microsoft 驗證器應用程式進行兩步驟驗證。

所有的三個元件可以安裝在 hello hello 伺服器是否為網際網路對向的同一部伺服器。 如果分解成 hello 元件，hello Azure MFA 應用程式伺服器上安裝 hello Web 服務 SDK 和 hello 使用者入口網站和行動裝置應用程式 Web 服務安裝在網際網路對向伺服器。

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Azure Multi-Factor Authentication Server 防火牆需求

每個 MFA 伺服器必須可以在下列位址的連接埠 443 輸出 toohello toocommunicate:

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

如果連外防火牆連接埠 443 上受限，開啟下列的 IP 位址範圍的 hello:

| IP 子網路 | 網路遮罩 | IP 範圍 |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

如果您不使用 hello 事件確認功能，而且您的使用者不使用從裝置的行動裝置應用程式 tooverify hello 公司網路上，您只需要下列範圍的 hello:

| IP 子網路 | 網路遮罩 | IP 範圍 |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>下載 Azure Multi-factor Authentication Server hello

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。
2. Hello 左側選取**Active Directory**
3. 按一下 [使用者和群組]
4. 按一下 [所有使用者]
5. 按一下 [Multi-Factor Authentication]
6. 在 [多重要素驗證] 區域之下，選取 [服務設定]

   ![服務設定頁面](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. 在 hello 服務設定 頁面上，在 hello 囉 」 畫面底部按一下**Go toohello 入口網站**。 新的頁面隨即開啟。
7. 按一下 [下載]。
8. 按一下 hello**下載**連結，並儲存 hello 安裝程式。

   ![下載 MFA Server](./media/multi-factor-authentication-get-started-server/download4.png)

9. 保留此頁面開啟，因為我們將 tooit 之後執行 hello 安裝程式。

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>安裝及設定 Azure Multi-factor Authentication Server hello

既然您已經下載 hello 伺服器，您可以安裝並設定它。 請確定您安裝在該 hello 伺服器符合 hello 規劃 > 一節中所列的需求。

1. 按兩下 hello 可執行檔。
2. 在 [hello 選取安裝資料夾] 畫面上，請確定該 hello 資料夾是否正確，然後按一下**下一步**。
3. Hello 安裝完成之後，請按一下**完成**。  hello 組態精靈 隨即啟動。
4. 在 [hello 組態精靈歡迎畫面中，核取**略過使用 hello 驗證設定精靈**按一下**下一步]**。  hello 精靈關閉並 hello 伺服器開始。

   ![雲端](./media/multi-factor-authentication-get-started-server/skip2.png)

5. 回到上我們下載 hello 伺服器 hello 頁面上，按一下 [hello**產生啟用認證**] 按鈕。 提供，這項資訊複製到 hello Azure MFA Server hello 方塊中，然後按一下**Activate**。

## <a name="send-users-an-email"></a>傳送電子郵件給使用者

tooease 首度發行、 允許 MFA Server toocommunicate 與您的使用者。 MFA Server 可以傳送電子郵件 tooinform 它們，它們已註冊的雙步驟驗證。

您傳送嗨電子郵件應該取決您將進行兩步驟驗證使用者的設定。 例如，如果您不能 tooimport hello 公司目錄中的電話號碼，hello 電子郵件應該包含 hello 預設電話號碼，讓使用者知道哪些 tooexpect。 如果您無法匯入電話號碼，或您的使用者將 toouse hello 行動裝置應用程式，將它們傳送電子郵件，其中會將他們導向 toocomplete 帳戶註冊。 Hello 電子郵件中包含超連結 toohello Azure Multi-factor Authentication 使用者入口網站。

hello 電子郵件的 hello 內容也有所不同 hello hello 使用者 （通話、 簡訊或行動裝置應用程式） 已設定的驗證方法。  比方說，如果 hello 使用者需要的 toouse PIN 驗證時，hello 電子郵件通知他們什麼他們初始 PIN 已設定為。  使用者在其第一個驗證期間會需要的 toochange 他們的 pin 碼。

### <a name="configure-email-and-email-templates"></a>設定電子郵件和電子郵件範本

針對傳送這些電子郵件中按一下 hello 電子郵件圖示 hello 左 tooset hello 的設定。 此頁面是您可以在其中輸入藉由檢查 hello hello SMTP 郵件伺服器和傳送電子郵件資訊**傳送電子郵件寄給 toousers**核取方塊。

![MFA Server 電子郵件組態](./media/multi-factor-authentication-get-started-server/email1.png)

Hello 電子郵件內容索引標籤上，您可以看到從可用 toochoose 的 hello 電子郵件範本。 根據您如何設定您的使用者 tooperform 雙步驟驗證，選擇最適合您的 hello 範本。

![MFA Server 電子郵件範本](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>從 Active Directory 匯入使用者

現在該 hello 伺服器已安裝，您會想 tooadd 使用者。 您可以選擇 toocreate 它們，手動從 Active Directory 中，匯入使用者，或設定自動同步處理與 Active Directory。

### <a name="manual-import-from-active-directory"></a>從 Active Directory 手動匯入

1. 在 hello 左側 hello Azure MFA Server 中，選取 **使用者**。
2. 在 hello 下方，選取**從 Active Directory 匯入**。
3. 現在您可以搜尋個別使用者或搜尋 hello AD 目錄的 Ou 與它們的使用者。  在此情況下，我們指定 hello 使用者 OU。
4. 反白顯示右 hello 上的所有 hello 使用者，然後按一下 **匯入**。  您應該會看到指出成功完成作業的快顯視窗。  關閉 hello 匯入 視窗。

   ![MFA Server 使用者匯入](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>自動與 Active Directory 同步處理

1. 在 hello 左側 hello Azure MFA Server 中，選取 **目錄整合**。
2. 瀏覽 toohello**同步** 索引標籤。
3. Hello 底部，選擇 **新增**
4. 在 hello**加入同步處理項目**出現方塊選擇 hello 網域、 OU**或**安全性群組、 設定、 預設值的方法，以及語言的預設值為這個同步處理工作，並按一下**新增**。
5. 標示的核取 hello 方塊**啟用與 Active Directory 同步處理**選擇**同步處理間隔**一分鐘到 24 小時之間。

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>Hello Azure Multi-factor Authentication Server 如何處理使用者資料

當您使用 hello Multi-factor Authentication (MFA) Server 內部部署時，使用者的資料會儲存在 hello 在內部部署伺服器。 Hello 雲端中不儲存任何持續性的使用者資料。 當 hello 使用者執行雙步驟驗證時，hello MFA Server 會傳送資料 toohello Azure MFA 雲端服務 tooperform hello 驗證。 當這些驗證要求傳送 toohello 雲端服務時，hello 下列欄位會傳送 hello 要求及記錄檔中，如此會出現在 hello 客戶的驗證及使用報表。 有些 hello 欄位是選擇性的因此可以啟用或停用 hello Multi-factor Authentication Server 內。 來自 hello MFA Server toohello MFA 雲端服務的 hello 通訊會透過連接埠 443 輸出使用 SSL/TLS。 這些欄位包括：

* 唯一識別碼 - 使用者名稱或內部的 MFA 伺服器識別碼
* 名字和姓氏 (選擇性)
* 電子郵件地址 (選擇性)
* 電話號碼 - 進行語音通話或簡訊驗證時
* 安全性權杖 - 執行行動應用程式驗證時
* 驗證模式
* 驗證結果
* MFA Server 名稱
* MFA Server IP
* 用戶端 IP – 如果有的話

此外 toohello 上述欄位，hello 驗證結果 （成功/拒絕） 和任何被拒絕的原因也是儲存與 hello 驗證資料，而且可透過 hello 驗證及使用報表。

## <a name="back-up-and-restore-azure-mfa-server"></a>備份和還原 Azure MFA Server

確定您具有正確的備份是使用任何系統的重要步驟 tootake。

tooback Azure MFA server，確定您有一份 hello **C:\Program files\multi-factor Authentication 驗證 Server\Data**資料夾包括 hello **PhoneFactor.pfdata**檔案。 

在還原的情況下會需要完整的 hello 下列步驟：

1. 在新的伺服器上重新安裝 Azure MFA Server。
2. 啟動 hello 新的 Azure MFA Server。
3. 停止 hello **MultiFactorAuth**服務。
4. 覆寫 hello **PhoneFactor.pfdata**以 hello 備份複本。
5. 啟動 hello **MultiFactorAuth**服務。

hello 新的伺服器現在會啟動並執行與 hello 原始備份組態和使用者資料。

## <a name="next-steps"></a>後續步驟

- 安裝和設定 hello[使用者入口網站](multi-factor-authentication-get-started-portal.md)自助使用者。
- 安裝和設定 hello 與 Azure MFA Server [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md)， [RADIUS 驗證](multi-factor-authentication-get-started-server-radius.md)，或[LDAP 驗證](multi-factor-authentication-get-started-server-ldap.md)。
- 安裝和設定[使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server-rdg.md)。
- [部署 Azure Multi-factor Authentication 伺服器行動應用程式 Web 服務的 hello](multi-factor-authentication-get-started-server-webservice.md)。
- [使用 Azure Multi-Factor Authentication 與協力廠商 VPN 的進階案例](multi-factor-authentication-advanced-vpn-configurations.md)。
