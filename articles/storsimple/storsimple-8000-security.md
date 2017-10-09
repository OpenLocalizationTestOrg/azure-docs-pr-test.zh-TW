---
title: "aaaStorSimple 8000 系列安全性 |Microsoft 文件"
description: "描述 hello 安全性和隱私權功能來保護您的 StorSimple 服務、 裝置與內部部署和 hello 雲端中的資料。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 48dd449d2908c21fe05d0ed37a4dc6f3e306e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-security-and-data-protection"></a>StorSimple 安全性和資料保護

## <a name="overview"></a>概觀

人在採用新技術，尤其是當 hello 技術用於機密或專屬資料的主要考量安全性。 評估不同的技術時，您必須考慮因為資料保護所增加的風險和成本。 Microsoft Azure StorSimple 提供的安全性和隱私性解決方案的資料保護，協助 tooensure:

* **機密性** – 只有已授權的實體才能檢視您的資料。
* **完整性** – 只有已授權的實體才能修改或刪除您的資料。

hello Microsoft Azure StorSimple 方案包含四個彼此互動的主要元件：

* **裝載於 Microsoft Azure StorSimple 裝置管理員服務**– hello tooconfigure 及佈建您使用的管理服務 hello StorSimple 裝置。
* **StorSimple 裝置** – 可安裝在您的資料中心的實體裝置。 所有主機和產生資料的用戶端都連接 toohello StorSimple 裝置，然後 hello 裝置管理 hello 資料，並將它移動 toohello Azure 雲端依適當情況。
* **用戶端/主機連接 toohello 裝置**– hello 基礎結構中 toohello StorSimple 裝置連接的用戶端，並產生需要 toobe 受保護的資料。
* **雲端儲存體**– hello hello 儲存資料的 Azure 雲端中的位置。

hello 下列章節說明 hello StorSimple 安全性功能，協助保護每個這些元件和 hello 資料儲存在其上。 它也包含一份關於 Microsoft Azure StorSimple 安全性和 hello 對應的答案，您可能遇到的問題。

## <a name="storsimple-device-manager-service-protection"></a>StorSimple 裝置管理員服務保護

管理服務裝載於 Microsoft Azure，而使用 toomanage 貴組織所購買的所有 StorSimple 裝置 hello StorSimple 裝置管理員服務。 您可以使用您的組織認證 toolog toohello Azure 入口網站透過 web 瀏覽器上存取 hello StorSimple 裝置管理員服務。

存取 toohello StorSimple 裝置管理員服務需要您的組織有內含 StorSimple 的 Azure 訂閱。 您的訂閱控管您可以在 hello Azure 入口網站存取的 hello 功能。 如果您的組織沒有 Azure 訂用帳戶，而您想 toolearn 詳細資訊，請參閱[註冊 Azure，以組織身分](../active-directory/sign-up-organization.md)。

Hello StorSimple 裝置管理員服務裝載在 Azure 中，因為它被受 hello Azure 的安全性功能。 如需有關 Microsoft Azure 所提供的 hello 安全性功能的詳細資訊，請移 toohello [Microsoft Azure 信任中心](https://azure.microsoft.com/support/trust-center/security/)。

## <a name="storsimple-device-protection"></a>StorSimple 裝置保護

hello StorSimple 裝置在內部部署混合式儲存裝置，包含固態硬碟 (Ssd) 和硬碟 (Hdd)，以及備用控制器和自動容錯移轉功能。 hello 控制器管理儲存體分層，將目前使用 （或活躍） 資料存放在本機儲存體 （在 hello StorSimple 裝置或內部部署伺服器），移動較不常用的資料 toohello 雲端時。

只有已授權的 StorSimple 裝置允許 toojoin hello StorSimple 裝置管理員服務在您的 Azure 訂用帳戶中所建立。 tooauthorize 裝置，您必須向它 hello StorSimple 裝置管理員服務藉由提供 hello 服務註冊金鑰。 hello 服務註冊金鑰是在 hello Azure 入口網站中產生的 128 位元隨機金鑰。

![服務註冊金鑰](./media/storsimple-security/ServiceRegistrationKey.png)

toolearn 如何取得服務註冊金鑰，請前往太[步驟 2： 取得 hello 服務註冊金鑰](storsimple-8000-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)。

hello 服務註冊金鑰是包含 100 個字元的長金鑰。 您可以複製 hello 金鑰，並將它儲存在安全的位置中的文字檔，以便您可以使用它 tooauthorize 其他裝置在必要時。 如果您註冊您的第一個裝置之後，遺失 hello 服務註冊金鑰，您可以從 hello StorSimple 裝置管理員服務產生新的金鑰。 這不會影響現有裝置的 hello 作業。

註冊裝置之後，它會使用語彙基元 toocommunicate 使用 Microsoft Azure。 hello 服務登錄機碼不會使用裝置註冊之後。

> [!NOTE]
> 我們建議您在每次使用後重新產生 hello 服務註冊金鑰。


## <a name="protect-your-storsimple-solution-via-passwords"></a>透過密碼保護您的 StorSimple 解決方案

密碼是電腦安全性的重要層面和廣泛使用在 hello StorSimple 解決方案中 toohelp 確保您的資料是僅限可存取 tooauthorized 使用者。 StorSimple 可讓您 tooconfigure hello 下列密碼：

* StorSimple 裝置系統管理員密碼
* Challenge Handshake 驗證通訊協定 (CHAP) 啟動器和目標密碼
* StorSimple Snapshot Manager 密碼

### <a name="windows-powershell-for-storsimple-and-hello-storsimple-device-administrator-password"></a>Windows PowerShell for StorSimple 和 StorSimple 裝置系統管理員密碼 hello

Windows PowerShell for StorSimple 是命令列介面，您可以使用 toomanage hello StorSimple 裝置。 Windows PowerShell for StorSimple 的功能可讓您 tooregister 您的裝置、 在裝置上設定 hello 網路介面、 安裝特定類型的更新、 裝置藉由存取 hello 支援工作階段，進行疑難排解和變更 hello 裝置狀態. 連接 toohello hello 裝置序列主控台或使用 Windows PowerShell 遠端功能，您可以存取 Windows PowerShell for StorSimple。

您可以透過 HTTPS 或 HTTP 執行 PowerShell 遠端處理。 如果已啟用透過 HTTPS 的遠端管理，您將需要 toodownload hello 遠端管理憑證從 hello 裝置，並將它安裝在遠端用戶端 hello。 如需有關 PowerShell 遠端執行功能的詳細資訊，請移至太[遠端連線 tooyour StorSimple 裝置](storsimple-8000-remote-connect.md)。

您可以使用 Windows PowerShell for StorSimple tooconnect toohello 裝置之後，您將需要 tooprovide hello 裝置系統管理員密碼 toolog toohello 裝置上。

![裝置系統管理員密碼](./media/storsimple-security/DeviceAdminPW.png)

請遵循最佳作法，請注意 hello:

* 遠端管理依預設為關閉。 您可以使用 hello StorSimple 裝置管理員服務 tooenable 它。 最佳安全性做法，應該只在 hello 實際所需的時間週期期間啟用遠端存取。
* 如果您變更 hello 密碼，請確定 toonotify 所有遠端存取使用者，讓它們不會遇到未預期的連線遺失。
* hello StorSimple 裝置 Manager 服務無法擷取現有的密碼： 它可以只能重設密碼。 我們建議您將所有密碼都儲存在安全的地方，可讓您不需要工作 tooreset 密碼如果忘記密碼時。 如果您需要 tooreset 密碼，請先確定 toonotify 所有使用者您重設。

您可以使用序列連線 toohello 裝置來存取 hello Windows PowerShell 介面。 您也可以使用提供額外安全性的 HTTP 或 HTTPS 遠端存取該介面。 HTTPS 提供比序列或 HTTP 連線更高層級的安全性。 不過，toouse HTTPS，您必須先安裝憑證，以便存取 hello 裝置 hello 用戶端電腦上。 您可以從 hello StorSimple 裝置管理員服務在 hello 裝置設定 頁面來下載 hello 遠端存取憑證。 如果遠端存取的 hello 憑證遺失，您必須下載新的憑證，並傳播授權的 toouse 遠端管理的 tooall 用戶端。

### <a name="challenge-handshake-authentication-protocol-chap-initiator-and-target-passwords"></a>Challenge Handshake 驗證通訊協定 (CHAP) 啟動器和目標密碼

CHAP 是 hello StorSimple 裝置 toovalidate hello 身分識別的遠端用戶端所使用的驗證配置。 hello 驗證根據共用的密碼。 CHAP 可以是單向 (單向) 或相互 (雙向)。 使用單向 CHAP 時，hello 目標 （hello StorSimple 裝置） 驗證起始端 （主機）。 相互或反向 CHAP 要求 hello 目標驗證啟動器 hello 並再 hello 啟動器驗證目標 hello。 StorSimple 可設定的 toouse 哪一種方法。

設定 CHAP 時，則應注意下列 hello:

* hello CHAP 使用者名稱必須包含少於 233 個字元。
* hello CHAP 密碼必須介於 12 到 16 個字元。 嘗試 toouse 較長的使用者名稱或密碼會導致 hello Windows 主機上的驗證失敗。
* 您無法使用 hello hello CHAP 起始端和 hello CHAP 目標相同的密碼。
* 設定 hello 密碼之後，可以變更但無法擷取。 如果 hello 密碼變更時，是確定 toonotify 所有遠端存取使用者，使其可以成功連線 toohello StorSimple 裝置。

如需 CHAP 的詳細資訊和如何 tooconfigure 會針對您的 StorSimple 解決方案移過[您 StorSimple 裝置設定 CHAP](storsimple-8000-configure-chap.md)。

### <a name="storsimple-snapshot-manager-password"></a>StorSimple Snapshot Manager 密碼

StorSimple Snapshot Manager 是 Microsoft Management Console (MMC) 嵌入式管理單元，使用磁碟區群組與 hello Windows 磁碟區陰影複製服務 toogenerate 應用程式一致備份。 此外，您可以使用 StorSimple Snapshot Manager toocreate 備份排程及複製或還原磁碟區。

當您設定裝置 toouse StorSimple Snapshot Manager 時，您將會需要的 tooprovide hello StorSimple Snapshot Manager 密碼。 此密碼最初是在 Windows PowerShell for StorSimple 中於註冊時設定。 hello 密碼也可設定及變更 hello StorSimple 裝置管理員服務。 此密碼可驗證的裝置 hello 與 StorSimple Snapshot Manager。

![StorSimple Snapshot Manager 密碼](./media/storsimple-security/SnapshotMgrPassword.png)

hello StorSimple Snapshot Manager 密碼必須是 14 too15 個字元，而且必須包含 3 個以上的大寫、 小寫、 數字及特殊字元的組合。 設定 hello StorSimple Snapshot Manager 密碼之後，可以變更但無法擷取。 如果您變更 hello 密碼，請確定 toonotify 所有遠端使用者。

如需 StorSimple Snapshot Manager 的詳細資訊，請移至太[什麼是 StorSimple Snapshot Manager？](storsimple-what-is-snapshot-manager.md)

### <a name="password-best-practices"></a>密碼最佳作法

我們建議您使用 hello 下列指導方針 toohelp 確保 StorSimple 密碼的強式且受到妥善保護：

* 每三個月變更您的密碼。 變更 hello 密碼會每年強制執行。
* 使用強式密碼。 如需詳細資訊，請移至太[建立更強的密碼，來保護它們](http://blogs.microsoft.com/cybertrust/2014/08/25/create-stronger-passwords-and-protect-them/)。
* 一律使用不同的密碼不同的存取機制。每個您所指定的 hello 密碼應該是唯一的。
* 請勿與不是授權的 tooaccess hello StorSimple 裝置的任何人共用密碼。
* 請勿面前提及密碼別人或在 hello 格式的密碼。
* 如果您懷疑帳戶或密碼已遭洩漏，報告 hello 事件 tooyour 資訊安全部門。
* 將所有密碼視為敏感的機密資訊。 

## <a name="storsimple-data-protection"></a>StorSimple 資料保護

本章節描述保護傳輸中的資料和預存的資料的 hello StorSimple 安全性功能。

其他章節所述，密碼是使用的 tooauthorize 和驗證使用者，才能存取 tooyour StorSimple 解決方案。 另一個安全性考量是，在儲存系統之間傳輸以及儲存資料時，如何保護資料以防止未經授權使用者進行存取。 hello 下列章節說明 hello 與 StorSimple 所提供的資料保護功能。

> [!NOTE]
> 重複資料刪除會提供額外保護儲存在 hello StorSimple 裝置上，並在 Microsoft Azure 儲存體中的資料。 Hello 資料物件時重複資料刪除的資料，從 hello 使用中繼資料 toomap 分開儲存，並存取它們： 沒有可用的儲存層級內容 tooreconstruct hello 資料磁碟區結構、 檔案系統或檔案名稱。


## <a name="protect-data-flowing-through-hello-service"></a>保護流動通過 hello 服務的資料

hello 的 hello StorSimple 裝置管理員服務的主要目的是 toomanage，並設定 hello StorSimple 裝置。 hello StorSimple 裝置管理員服務在 Microsoft Azure 中執行。 使用 hello Azure 入口網站 tooenter 裝置組態資料，然後 Microsoft Azure 使用 hello StorSimple 裝置管理員服務 toosend hello 資料 toohello 裝置。 StorSimple 會使用一種非對稱金鑰組 toohelp 確保洩露的 hello Azure 服務不會導致洩漏儲存資訊。

![傳輸中的資料加密](./media/storsimple-security/DataEncryption.png)

hello 的非對稱金鑰系統可協助保護 hello 資料流經 hello 服務，如下所示：

1. 使用非對稱公開和私用金鑰組的資料加密憑證會產生 hello 裝置上，並且未使用的 tooprotect hello 資料。 hello 第一個裝置註冊時，會產生 hello 金鑰。
2. hello 資料加密憑證金鑰匯出到受到 hello 服務資料加密金鑰，也就是隨機產生 hello 第一個裝置註冊期間的強式 128 位元金鑰的個人資訊交換 (.pfx) 檔案。
3. hello hello 憑證公開金鑰安全地使用 toohello StorSimple 裝置管理員服務，而且 hello 私密金鑰會保留與 hello 裝置。
4. 輸入 hello 服務會使用加密的資料 hello 公開金鑰，並使用儲存在 hello 裝置 hello 私密金鑰解密，確保該 hello Azure 服務無法解密 hello 資料流動 toohello 裝置。

只有 hello 第一個裝置註冊與 hello 服務上產生 hello 服務資料加密金鑰。 所有後續裝置註冊與 hello 服務必須使用 hello 相同的服務資料加密金鑰。

> [!IMPORTANT]
> 它是非常重要的 toomake hello 服務資料加密金鑰的副本，並將它儲存在安全的位置。 Hello 服務資料加密金鑰的複本應該儲存得則可由獲授權的人存取，而且可以輕鬆地溝通的 toohello 裝置系統管理員。
> 
> Hello 服務資料加密金鑰遺失時，Microsoft 支援人員可協助您 tooretrieve 它提供至少一個裝置在線上狀態。 我們建議您在擷取後變更 hello 服務資料加密金鑰。 如需相關指示，請移至太[變更 hello 服務資料加密金鑰](storsimple-service-dashboard.md#change-the-service-data-encryption-key)。

您可以變更 hello 服務資料加密金鑰和 hello 對應的資料加密憑證選取 hello**變更服務資料加密金鑰**hello 服務儀表板上的選項。 tooensure 資料安全性不會洩露，您必須使用實體 StorSimple 裝置 toochange hello 服務資料加密金鑰。 變更 hello 加密金鑰需要所有的裝置，會更新以 hello 新的金鑰。 因此，我們建議您在所有裝置都都在線上時變更 hello 索引鍵。 如果裝置處於離線狀態，您可以在其他時間變更金鑰。 金鑰已過期的 hello 裝置依然會無法 toorun 備份，但它們可以 toorestore 資料才會更新 hello 鍵。 如需詳細資訊，請移至太[使用 hello StorSimple 裝置管理員服務儀表板](storsimple-8000-service-dashboard.md)。

hello 服務資料加密金鑰和 hello 資料加密憑證不會過期。 不過，我們建議您變更 hello 服務資料加密金鑰每年 toohelp 防止金鑰洩露。

## <a name="protect-data-at-rest"></a>保護靜態資料的安全

hello StorSimple 裝置管理的資料儲存在層級中，在本機和 hello 雲端，視使用頻率而定。 所有的主控件的電腦，連線的 toohello 裝置傳送資料 toohello 裝置，然後移動到適當的資料 toohello 雲端。 資料是透過從傳送 hello 裝置 toohello 雲端安全地 hello 網際網路。 每個裝置都會有一個可瀏覽其上所有共用磁碟區的 iSCSI 目標。 傳送 toocloud 儲存體之前，所有的資料會加密。 

![雲端儲存體加密金鑰](./media/storsimple-security/CloudStorageEncryption.png)

toohelp 確保 hello 安全性和資料完整性移動 toohello 雲端，StorSimple 可讓您 toodefine 雲端儲存體加密金鑰，如下所示：

* 當您建立磁碟區容器時，您可以指定 hello 雲端儲存體加密金鑰。 hello 金鑰不能修改，或稍後新增。
* 磁碟區容器共用中的所有磁碟區 hello 相同的加密金鑰。 如果您想不同格式的特定磁碟區加密，我們建議您建立新的磁碟區容器 toohost 該磁碟區。
* 當您在 hello StorSimple 裝置管理員服務輸入 hello 雲端儲存體加密金鑰時，hello 金鑰進行加密，使用 hello hello 服務資料加密金鑰的公開部分，會將傳送 toohello 裝置。
* hello 雲端儲存體加密金鑰不會儲存在 hello 服務中，因此不知道只有 toohello 裝置。
* 指定雲端儲存體加密金鑰是選用選項。 您可以傳送嗨主機 toohello 裝置上已加密的資料。

### <a name="additional-security-best-practices"></a>其他的安全性最佳作法

* 分割流量：透過部署完全分開的網路並在無法使用實體隔離的位置使用 VLAN，將您的 iSCSI SAN 從公司 LAN 中的使用者流量隔離。 ISCSI 存放裝置的專用的網路將會保證 hello 安全和業務關鍵資料的效能。 不建議在公司 LAN 上將存放裝置與使用者流量混用，這會增加延遲並造成網路失敗。
* 針對主機端的網路安全性，請使用支援 TCP/IP 卸載引擎 (TOE) 的網路介面。 TOE 會 hello 網路介面卡上處理 TCP 降低 CPU 負載。

## <a name="protect-data-via-storage-accounts"></a>透過儲存體帳戶保護資料安全

每個 Microsoft Azure 訂閱可以建立一或多個儲存體帳戶。 （儲存體帳戶會提供唯一的命名空間使用資料儲存在 hello Azure 雲端中）。存取 tooa 儲存體帳戶是由該儲存體帳戶相關聯的 hello 訂用帳戶和存取金鑰所控制。

當您建立儲存體帳戶時，Microsoft Azure 會產生兩個 512 位元儲存體存取金鑰，其中用於驗證 hello StorSimple 裝置存取 hello 儲存體帳戶時。 請注意，這些金鑰中只有一個會是使用中狀態。 hello 另一個索引鍵是處於保留狀態，定期允許您 toorotate hello 金鑰。 toorotate 索引鍵，您會使 hello 次要索引鍵，然後再刪除 hello 主索引鍵。 然後，您可以建立新的金鑰使用 hello 下一個循環期間。 (基於安全性理由，許多資料中心需要金鑰輪替)。

建議您按照這些最佳作法進行金鑰輪替：

* 您應該更換儲存體帳戶金鑰定期 toohelp 也能確保未經授權的使用者無法存取儲存體帳戶。
* 定期 Azure 系統管理員應該變更或重新產生使用 hello hello Azure 入口網站 toodirectly 存取 hello 儲存體帳戶的儲存體 區段的 hello 主要或次要金鑰。

## <a name="protect-data-via-encryption"></a>透過加密保護資料安全

StorSimple 會使用下列 tooprotect 資料儲存在加密演算法或您的 StorSimple 解決方案的 hello 元件之間旅行的 hello。

| 演算法 | 金鑰長度 | 通訊協定/應用程式/註解 |
| --- | --- | --- |
| RSA |2048 |Hello Azure 入口網站 tooencrypt 傳送 toohello 裝置的組態資料使用 RSA PKCS 1 1.5 版： 例如，儲存體帳戶認證，StorSimple 裝置設定，部署和雲端儲存體加密金鑰。 |
| AES |256 |Toohello Azure 入口網站傳送嗨的 StorSimple 裝置之前，AES with CBC 是使用的 tooencrypt hello 公開部分 hello 服務資料加密金鑰。 它也會使用 hello StorSimple 裝置 tooencrypt 資料傳送嗨資料 toohello 雲端儲存體帳戶之前。 |

## <a name="storsimple-cloud-appliance-security"></a>StorSimple 雲端設備安全性

[!INCLUDE [storsimple Cloud Appliance security](../../includes/storsimple-virtual-device-security.md)]

## <a name="frequently-asked-questions-faq"></a>常見問題集 (FAQ)

hello 下面是一些關於問題和解答安全性和 Microsoft Azure StorSimple。

**問：** 我的服務遭到入侵。 我接下來該怎麼做？

**答：**您應該立即變更 hello 服務資料加密金鑰和 hello hello 用於分層資料的儲存體帳戶的儲存體帳戶金鑰。 如需相關指示，請移至：

* [變更 hello 服務資料加密金鑰](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [儲存體帳戶的金鑰輪替](storsimple-8000-manage-storage-accounts.md#key-rotation-of-storage-accounts)

**問：**我有新的 StorSimple 裝置的 hello 服務註冊金鑰。 該如何擷取此金鑰？

**答：**已建立這個機碼，當您第一次建立 hello StorSimple 裝置管理員服務。 當您使用 hello StorSimple 裝置管理員服務 tooconnect toohello 裝置時，您可以使用 hello 服務快速入門頁面 tooview 或 hello 重新產生服務註冊金鑰。 產生新的服務註冊金鑰並不會影響 hello 現有已註冊的裝置。 如需相關指示，請移至：

* [檢視或重新產生 hello 服務註冊金鑰](storsimple-8000-manage-service.md##regenerate-the-service-registration-key)

**問：** 我遺失服務資料加密金鑰。 該怎麼辦？

**答：** 請連絡「Microsoft 支援服務」。 他們可以登入 tooa 支援工作階段，在您的裝置，並協助您擷取 hello 金鑰 （提供至少一個裝置在線上）。 只有 tooyou 立即取得 hello 服務資料加密金鑰之後，您應該變更它 tooensure 知道該 hello 新的金鑰。 如需相關指示，請移至：

* [變更 hello 服務資料加密金鑰](storsimple-service-dashboard.md#change-the-service-data-encryption-key)

**問：**我已授權裝置的服務資料加密金鑰變更，但並未啟動 hello 金鑰變更程序。 我該怎麼辦？

**答：**如果 hello 逾時期限過期，您將需要 tooreauthorize hello 裝置 hello 服務資料加密金鑰變更，並重新啟動 hello 程序。

**問：**變更 hello 服務資料加密金鑰，但我無法 tooupdate hello 在 4 小時內的其他裝置。 我有 toostart 一次嗎？

**答：** hello 僅用於起始 hello 變更為 4 小時的時間間隔。 您在啟動 hello 更新程序之後 hello 授權 StorSimple 裝置，hello 授權都有效，直到所有的裝置會更新。

**問：**我們的 StorSimple 系統管理員已離開 hello 公司。 我該怎麼辦？

**答：**變更和重設 hello 允許存取 toohello StorSimple 裝置，並變更 hello 服務資料加密金鑰 tooensure hello 新資訊不知道 toounauthorized 人員的密碼。 如需相關指示，請移至：

* [使用 hello StorSimple 裝置管理員服務 toochange storsimple 密碼](storsimple-8000-change-passwords.md)
* [變更 hello 服務資料加密金鑰](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [為 StorSimple 裝置設定 CHAP](storsimple-8000-configure-chap.md)

**問：**我想要讓 tooprovide hello StorSimple Snapshot Manager 密碼 tooa 主機連接 toohello StorSimple 裝置，但沒有 hello 密碼。 我該怎麼辦？

**答：**如果您忘記 hello 密碼，您應該建立一個新。 然後，請務必的 tooinform hello 密碼的所有現有使用者已變更，他們應該更新其用戶端 toouse hello 新密碼。 如需相關指示，請移至：

* [變更 hello StorSimple Snapshot Manager 密碼](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password)
* [驗證裝置](storsimple-snapshot-manager-manage-devices.md#authenticate-a-device)

**問：**遠端存取 toohello Windows PowerShell for StorSimple 的 hello 憑證已變更 hello 裝置上。 如何更新遠端存取用戶端？

**答：**您可以下載 hello StorSimple 裝置管理員服務 hello 新憑證，並接著提供 toobe 安裝在遠端存取用戶端 hello 憑證存放區。 如需相關指示，請移至：

* [Import-Certificate cmdlet](https://technet.microsoft.com/library/hh848630.aspx)

**問：**我的資料保護如果 hello StorSimple 裝置管理員服務遭到盜用嗎？

**答：** 在網頁瀏覽器中檢視服務組態資料時，一律會使用您的公開金鑰將它加密。 Hello 服務因為 hello 服務無權存取 toohello 私密金鑰，則不會是能 toosee 任何資料。 Hello StorSimple 裝置管理員服務遭到洩露時，有任何影響，因為沒有任何金鑰儲存在 hello StorSimple 裝置管理員服務。

**問：**如果有人取得存取 toohello 資料加密憑證，將我的資料會遭到洩露嗎？

**答：** Microsoft Azure 以加密格式儲存 hello 客戶的資料加密金鑰 （.pfx 檔案）。 因為 hello.pfx 檔案已加密，且 hello StorSimple 服務沒有 hello 服務資料加密金鑰 toodecrypt hello.pfx 檔，只取得存取 toohello.pfx 檔案將不會曝露任何秘密。

**問：** 如果政府機構向 Microsoft 索取我的資料，會發生什麼情況？

**答：**實體，因此所有 hello 資料已加密 hello 服務上 hello 私密金鑰會保留與 hello 裝置 hello 政府的發照必須要求客戶 hello hello 資料。

## <a name="next-steps"></a>後續步驟

[部署您的 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。

