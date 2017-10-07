---
title: "aaaAzure 加密概觀 |Microsoft 文件"
description: "了解 Azure 中的各種加密選項"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/18/2017
ms.author: barclayn
ms.openlocfilehash: ef9ab46de32b857e99e8fe628a61386b95cf197f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-overview"></a>Azure 加密概觀

本文提供如何在 Microsoft Azure 中使用加密的概觀。 它涵蓋了 hello 的加密，包括靜態加密、 加密中分段，並使用金鑰保存庫金鑰管理的主要區域。 每節都包含詳細資訊的連結。

## <a name="encryption-of-data-at-rest"></a>待用資料加密

待用資料包含位於實體媒體之永續性儲存體中任何數位格式的資訊。 這包括磁性或光學媒體上的檔案、已封存的資料，以及資料備份。 Microsoft Azure 提供的資料儲存體解決方案 toomeet 各種不同的需求，包括檔案、 磁碟、 blob 和資料表儲存體。 Microsoft 也有提供加密 tooprotect [Azure SQL Database](../sql-database/sql-database-technical-overview.md)， [CosmosDB](../cosmos-db/introduction.md)，和 Azure 資料湖。

待用資料加密整個 hello Azure 軟體做為服務 (SaaS)，平台做為服務 (PaaS) 是可用的服務和基礎結構做為服務 (IaaS) 雲端模型。 本文摘要說明並提供資源 toohelp 您使用 Azure 的加密選項。

如需詳細的待用資料在 Azure 中的加密方式的討論，請參閱標題為 hello 文件[Azure 資料--靜態加密](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Azure 加密模型

Azure 支援各種加密模型，包括使用服務管理金鑰的伺服器端加密、在 Azure Key Vault 中使用客戶管理的金鑰，或在受客戶控制硬體上使用客戶管理的金鑰。 用戶端加密可讓您 toomanage 和存放區索引鍵在內部部署或在另一個安全的位置。

### <a name="client-side-encryption"></a>用戶端加密

用戶端加密是在 Azure 外部執行。 用戶端加密包括：

- 由執行在 hello 客戶的資料中心的應用程式或服務應用程式加密的資料
- Azure 收到時便已加密的資料。

用戶端加密與 hello 雲端服務提供者沒有存取 toohello 加密金鑰，並無法將此資料解密。 您維護 hello 金鑰的完整控制權。

### <a name="server-side-encryption"></a>伺服器端加密

hello 三個伺服器端加密模型提供不同的金鑰管理特性，可以選擇每個您的需求。

- **服務管理的金鑰**結合控制能力與便利性，而且額外負荷很低

- **客戶管理的金鑰**可讓您控制 hello 索引鍵，包括 hello 能力 toobring 您自己的金鑰 (BYOK) 或 toogenerate 新的。

- **服務管理的金鑰，在 ccustomer controlledhardware**可讓您 toomanage 您專屬儲存機制中，Microsoft 的控制之外的索引鍵。 這稱為託管您自己的金鑰 (HYOK)。 不過，設定很複雜，而且大多數 Azure 服務並不支援此模型。

### <a name="azure-disk-encryption"></a>Azure 磁碟加密

Windows 和 Linux 虛擬機器可以受到使用[Azure 磁碟加密](azure-security-disk-encryption.md)，它會使用 hello [Windows BitLocker](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx)技術和 Linux [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooprotect作業系統磁碟和完整磁碟區加密的資料磁碟。

加密金鑰和密碼會在您的 [Azure Key Vault](../key-vault/key-vault-whatis.md) 訂用帳戶中受到保護。 您可以備份及還原加密會加密與 hello KEK 組態使用 hello Azure 備份服務的 Vm。

### <a name="azure-storage-service-encryption"></a>Azure 儲存體服務加密

Azure 儲存體 (Blob 和檔案) 中的待用資料可以在伺服器端和用戶端案例中進行加密。

[Azure 儲存體服務加密](../storage/storage-service-encryption.md)(SSE 中) 可以自動加密資料，然後再儲存和擷取時，進行 hello 處理完全透明的使用者會自動解密。 儲存體服務加密會使用 256 位元[AES 加密](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)，這是其中一個 hello 最強的區塊密碼，而且會處理加密、 解密和金鑰管理，以透明的方式。

### <a name="client-side-encryption-of-azure-blobs"></a>Azure Blob 的用戶端加密

Azure Blob 的用戶端加密可以透過不同的方式來執行。

您可以使用 Azure 儲存體用戶端程式庫 hello.NET NuGet 封裝 tooencrypt 資料內用戶端應用程式的先前 toouploading 它 tooAzure 儲存體。

toolearn 深入了解並下載 hello.NET NuGet 套件的 Azure 儲存體用戶端程式庫，請參閱標題為 hello 文件[Windows Azure 儲存體 8.3.0](https://www.nuget.org/packages/WindowsAzure.Storage)

當您使用用戶端加密使用 Azure 金鑰保存庫時，會使用單次對稱內容加密金鑰 (CEK) 所產生的 hello Azure 儲存體用戶端 SDK 來加密您的資料。 使用加密金鑰 (KEK)，可以對稱金鑰或非對稱金鑰組，hello CEK 進行加密。 您可以在本機進行管理，或將它儲存在 Azure Key Vault 中。 hello 加密的資料是然後上傳 tooAzure 儲存體服務。

深入了解使用 Azure 金鑰保存庫的用戶端加密 toolearn 和如何 tooinstructions 快速入門，請參閱標題為 hello 文件[教學課程： 加密和解密使用 Azure 金鑰保存庫的 Microsoft Azure 儲存體中的 blob](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

最後，您也可以使用 Java tooperform 用戶端加密下載它 toohello 用戶端時，將資料 tooAzure 儲存體和 toodecrypt hello 資料上傳之前 hello Azure 儲存體用戶端程式庫。 此程式庫也支援與 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 整合，以進行儲存體帳戶金鑰管理。

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>使用 Azure SQL Database 加密待用資料

[Azure SQL Database](../sql-database/sql-database-technical-overview.md) 是 Microsoft Azure 中的一般目的關聯式資料庫服務，可支援關聯式資料、JSON、空間和 XML 等結構。 Azure SQL 支援透過 hello 透明資料加密 (TDE) 功能的伺服器端加密和用戶端加密透過 hello 一律加密 」 功能。

#### <a name="transparent-data-encryption"></a>透明資料加密

[TDE 透明資料加密](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde)是使用的 tooencrypt [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016)， [Azure SQL Database](../sql-database/sql-database-technical-overview.md)，和[Azure SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)即時資料檔案使用資料庫加密金鑰 (DEK)，在復原期間儲存在 hello 資料庫開機記錄的可用性。

TDE 使用 AES 和 3DES 加密演算法來保護資料和記錄檔。 Hello 資料庫檔案的加密會執行在 hello 頁面層級;加密資料庫中的 hello 頁面寫入 toodisk 之前已經加密，並在讀入記憶體時，會解密。 現在預設會在新建立的 Azure SQL Database 上啟用 TDE。

#### <a name="always-encrypted"></a>一律加密

hello[永遠加密](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine)Azure SQL 中的功能可讓您在 Azure SQL Database 中用戶端應用程式先前 toostoring tooencrypt 資料，並可讓您在內部部署資料庫管理 toothird tooenable 委派合作對象和維護的擁有者且可以檢視 hello 資料和者加以管理，但不是應該存取 tooit 區隔。

#### <a name="cellcolumn-level-encryption"></a>資料格/資料行層級加密

Azure SQL Database 可讓您 tooapply 對稱式加密 tooa 資料的資料行使用 Transact SQL。 這稱為[資料格層級加密或資料行層級加密](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data)(CLE)，因為您可以使用它 tooencrypt 特定資料行或更特定的資料格的資料使用不同的加密金鑰。 這提供您比 TDE 更細微的加密功能，來加密頁面中的資料。

CLE 有內建函式，您可以使用 tooencrypt hello 公開金鑰的憑證，或使用 3DES 的複雜密碼，請使用對稱或非對稱金鑰的資料。

### <a name="cosmos-db-database-encryption"></a>Cosmos DB 資料庫加密

[Azure Cosmos DB](../cosmos-db/database-encryption-at-rest.md) 是 Microsoft 之全域散發的多模型資料庫。 依預設，會加密使用者資料儲存在 Cosmos DB 中的非揮發性儲存體 （固態磁碟機）不有任何控制項 tooturn 開啟或關閉它。 待用加密是使用數種安全性技術來實作的，這些技術包括安全金鑰儲存體系統、加密的網路，以及密碼編譯 API。 加密金鑰是由 Microsoft 管理，並根據 Microsoft 內部方針來輪替。

### <a name="at-rest-encryption-in-azure-data-lake"></a>Azure Data Lake 的待用加密

[Azure 資料湖](../data-lake-store/data-lake-store-encryption.md)是整個企業的儲存機制每一種資料收集的需求或結構描述的單一位置先前 tooany 正式定義中。 Azure Data Lake Store 支援 」 上依預設，「 透明加密在其餘部分，您的帳戶 hello 建立期間設定的資料。 根據預設，資料湖存放區 hello 金鑰會為您管理，但您已擁有 hello 選項 toomanage 它們自己。

三種類型的金鑰用於加密及解密資料： hello 主要加密金鑰 (MEK)、 資料加密金鑰 (DEK) 和區塊加密金鑰 (BEK)。 hello MEK 為使用的 tooencrypt hello DEK，都儲存在持續性的媒體，並衍生 hello BEK hello DEK 和 hello 資料區塊。 如果您要管理您自己的金鑰，您可以旋轉 hello MEK。

## <a name="encryption-of-data-in-transit"></a>傳輸中資料加密

Azure 提供許多從一個位置 tooanother 移動保存資料私用的機制。

### <a name="tlsssl-encryption-in-azure"></a>Azure 的 TLS/SSL 加密

Microsoft 會使用 hello[傳輸層安全性](https://en.wikipedia.org/wiki/Transport_Layer_Security)(TLS) 通訊協定 tooprotect 資料時傳送嗨雲端服務與客戶之間。 Microsoft 的資料中心交涉 tooAzure 服務連接的用戶端系統的 TLS 連線。 TLS 提供增強式驗證、訊息隱私權、完整性 (可偵測訊息竄改、攔截和偽造)、互通性、演算法彈性，並方便部署和使用。

[完整轉寄密碼](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) 透過唯一金鑰來保護客戶的用戶端系統與 Microsoft 的雲端服務之間的連線。 這些連線也會使用 RSA 型 2048 位元加密金鑰長度。 此組合可讓人 toointercept 及存取已傳輸中的資料。

### <a name="azure-storage-transactions"></a>Azure 儲存體交易

當您透過 hello Azure 入口網站互動與 Azure 儲存體時，所有的交易進行透過 HTTPS。 您也可以使用透過 HTTPS toointeract hello 儲存體 REST API 與 Azure 儲存體。 呼叫儲存體帳戶中的 hello REST Api tooaccess 物件透過啟用安全傳輸所需的 hello 儲存體帳戶時，您可以強制 hello 使用 HTTPS。

共用存取簽章 ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md))，它可以是使用的 toodelegate 存取 tooAzure 儲存物件，包含選項 toospecify 可以使用 HTTPS 通訊協定，使用共用存取簽章時，只有 hello。 這會確保送出連結使用 SAS 權杖的任何人使用 hello 適當的通訊協定。

[SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption)使用的 tooaccess Azure 檔案共用支援加密，且它隨附於 Windows Server 2012 R2、 Windows 8、 Windows 8.1 和 Windows 10 中，允許跨區域存取，甚至在 hello 桌面存取。

用戶端加密會加密 hello 資料之前已傳送 tooAzure 存放裝置，以便傳送嗨網路上加密。

### <a name="smb-encryption-over-azure-virtual-networks"></a>透過 Azure 虛擬網路的 SMB 加密 

[SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) Azure Vm 執行 Windows Server 2012 和更新版本提供 hello 能力 toomake 資料傳輸保護方法是在 Azure 虛擬網路上加密傳輸中的資料，防止竄改和竊聽 tooprotect 攻擊。 系統管理員可以啟用 SMB 加密 hello 整個伺服器，或是特定的共用。

根據預設，一旦 SMB 加密開啟的共用或伺服器上，只有用戶端 SMB 3 會允許 tooaccess hello 加密共用。

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Azure 虛擬機器的傳輸中加密

若要、，然後執行 Windows Azure Vm 之間的傳輸中的資料被加密的數種方式，根據 hello 連接 hello 本質。

### <a name="rdp-sessions"></a>RDP 工作階段

您可以連接並登入 tooan Azure VM 使用 hello[遠端桌面通訊協定](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx)(RDP) 從 Windows 用戶端電腦，或從 Mac 使用 RDP 用戶端安裝。 透過 RDP 工作階段中的 hello 網路傳輸中的資料可以受 TLS 保護。

您也可以在 Azure 中使用遠端桌面 tooconnect tooa Linux VM。

### <a name="secure-access-toolinux-vms-with-ssh"></a>透過 SSH tooLinux Vm 安全存取

您可以使用[Secure Shell](../virtual-machines/linux/ssh-from-windows.md) (SSH) tooconnect tooLinux Vm 在 Azure 中執行遠端管理。 SSH 是允許透過不安全的連線進行安全登入的加密連線通訊協定。 它是在 Azure 中裝載的 Linux Vm 的 hello 預設連線通訊協定。 使用 SSH 金鑰進行驗證時，您就可以排除在密碼 toolog hello 需要。 SSH 使用公開/私密金鑰組 (非對稱式加密) 進行驗證。

## <a name="azure-vpn-encryption"></a>Azure VPN 加密

您可以透過建立安全通道 tooprotect hello 隱私權 hello 資料傳送嗨網路上的虛擬私人網路連線 tooAzure。

### <a name="azure-vpn-gateway"></a>Azure VPN 閘道

[Azure VPN 閘道](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md)可以是您的虛擬網路和跨公用連線，您在內部部署位置之間使用的 toosend 加密流量或 toosend 虛擬網路之間的流量。

站對站 VPN 使用 [IPsec](https://en.wikipedia.org/wiki/IPsec) 進行傳輸加密。 Azure VPN 閘道使用一組預設提案。 您可以使用特定的密碼編譯演算法和金鑰長度，設定 Azure VPN 閘道 toouse 自訂 IPsec/IKE 原則而 hello Azure 的預設原則集。

### <a name="point-to-site-vpn"></a>點對站 VPN

點對站 Vpn 讓個別用戶端電腦存取 tooan Azure 虛擬網路。 [hello 安全通訊端通道通訊協定](https://technet.microsoft.com/library/2007.06.cableguy.aspx)(SSTP) 是使用的 toocreate hello VPN 通道，而且可以周遊的防火牆 （做為 HTTPS 連線會顯示 hello 通道）。 您可以使用自己的內部 PKI 根 CA 進行點對站連線。

您可以設定點對站 VPN 連線 tooa 虛擬網路 hello Azure 入口網站使用憑證驗證或 PowerShell。

toolearn 更多關於點對站 VPN 連線 tooAzure Vnet，請參閱：[設定點對站連線 tooa VNet 使用憑證驗證： Azure 入口網站](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)和

[設定點對站連線 tooa VNet 使用憑證驗證： PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>站對站 VPN 

站對站 VPN 閘道連線是使用的 tooconnect 您內部網路 tooan Azure 虛擬網路透過 VPN IPsec/IKE （IKEv1 或 IKEv2） 通道。 這種類型的連線需要 VPN 裝置位於內部部署具有對外開放的公用 IP 位址指派 tooit。

您可以設定站對站 VPN 連線 tooa 虛擬網路使用 hello Azure 入口網站、 PowerShell 或 hello Azure 命令列介面 (CLI)。

如需詳細資訊，請閱讀：

[Hello Azure 入口網站中建立站對站連接](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[建立站對站連線](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[使用 CLI 建立具有站對站 VPN 連線的虛擬網路](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Azure Data Lake 的傳輸中加密

傳輸中的資料 (也稱為移動中的資料) 也一律會在 Data Lake Store 中加密。 此外 tooencrypting 資料先前 toostoring toopersistent 媒體 hello 資料也都受到保護傳輸中使用 HTTPS。 HTTPS 是 hello 唯一的通訊協定支援的資料湖存放區 REST 介面的 hello。

toolearn 進一步了解 Azure 資料湖，在傳輸中資料的加密，請參閱標題為 hello 文件[Azure 資料湖存放區中的資料加密。](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Azure Key Vault 的金鑰管理

沒有適當的保護和管理 hello 金鑰，加密會變成無法使用。 Azure 金鑰保存庫是 Microsoft 的管理和控制存取 tooencryption 金鑰雲端服務所使用的建議的解決方案。 Tooservices 或 toousers 透過 Azure Active Directory 帳戶，可以指派權限 tooaccess 索引鍵。

Azure 金鑰保存庫減輕組織的 hello 需要 tooconfigure，修補程式，以及維護硬體安全性模組 (Hsm) 與金鑰管理的軟體。 使用 Azure 金鑰保存庫，Microsoft 不會看到您的金鑰和應用程式不需要直接存取 toothem;維護控制項時。 您也可以在 HSM 中匯入或產生金鑰。

## <a name="next-steps"></a>後續步驟

- [Azure 安全性概觀](security-get-started-overview.md)
- [Azure 網路安全性概觀](security-network-overview.md)
- [Azure 資料庫安全性概觀](azure-database-security-overview.md)
- [Azure 虛擬機器安全性概觀](security-virtual-machines-overview.md)
- [待用資料加密](azure-security-encryption-atrest.md)
- [資料安全性與加密的最佳做法](azure-security-data-encryption-best-practices.md)
