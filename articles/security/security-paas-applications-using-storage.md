---
title: "aaaSecuring PaaS 應用程式使用 Azure 儲存體 |Microsoft 文件"
description: " 了解用來保護 PaaS Web 與行動應用程式的 Azure 儲存體安全性最佳做法。 "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: TomShinder
ms.openlocfilehash: 3fed75cb121e7f32eb8b948ee12ca35fb25eca7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-storage"></a>使用 Azure 儲存體來保護 PaaS Web 與行動應用程式
在本文中，我們將說明用來保護 PaaS Web 與行動應用程式的 Azure 儲存體安全性最佳做法。 這些最佳作法從我們的經驗與 Azure 和 hello 經驗的客戶想自己。

hello [Azure 儲存體安全性指南 》](../storage/common/storage-security-guide.md)是 Azure 儲存體和安全性的詳細資訊的絕佳來源。  本文以高層級概念 hello hello 安全性指南和連結 toohello 安全性指南 》，以及其他來源，如需詳細資訊中找到。

## <a name="azure-storage"></a>Azure 儲存體
Azure 可讓您 toodeploy 和使用的儲存方式不可以輕鬆實現 15k 在內部部署。 利用 Azure 儲存體，您不必大費周章就可以實現高水準的延展性和可用性。 不只是 Azure 儲存體 hello foundation 針對 Windows 和 Linux 的 Azure 虛擬機器，它也可以支援大型的分散式應用程式。

Azure 儲存體提供下列四項服務的 hello: Blob 儲存體，資料表儲存體、 佇列儲存體和檔案儲存體。 詳細資訊，請參閱 toolearn[簡介 tooMicrosoft Azure 儲存體](../storage/storage-introduction.md)。

## <a name="best-practices"></a>最佳作法
本文解決下列最佳作法的 hello:

- 存取保護：
   - 共用存取簽章 (SAS)
   - 受控磁碟
   - 角色型存取控制 (RBAC)

- 儲存體加密：
   - 高價值資料的用戶端加密
   - 虛擬機器 (VM) 的 Azure 磁碟加密
   - 儲存體服務加密

## <a name="access-protection"></a>存取保護
### <a name="use-shared-access-signature-instead-of-a-storage-account-key"></a>使用共用存取簽章而非儲存體帳戶金鑰

IaaS 解決方案 (通常執行 Windows Server 或 Linux 虛擬機器) 會使用存取控制機制來防止檔案外流和遭遇竄改威脅。 在 Windows 上，您會使用[存取控制清單 (ACL)](../virtual-network/virtual-networks-acl.md)，而在 Linux 上，您可能會使用 [chmod](https://en.wikipedia.org/wiki/Chmod)。 基本上，如果您今天是在自己的資料中心中保護伺服器上的檔案，您確實會這麼做。

但 PaaS 不同。 Hello 最常見方式 toostore 檔案在 Microsoft Azure 中的其中一個是 toouse [Azure Blob 儲存體](../storage/storage-dotnet-how-to-use-blobs.md)。 Blob 儲存體和其他檔案的儲存體之間的差異是 hello 檔案 I/O 和檔案 I/O 隨附 hello 保護方法。

存取控制很重要。 您可控制存取 tooAzure 儲存 toohelp，hello 系統會產生兩個 512 位元儲存體帳戶金鑰 (SAKs) 當您[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)。 hello 索引鍵的備援層級可讓您 tooavoid 服務插斷常式金鑰循環期間。

儲存體存取金鑰是高優先順序的機密，而且應該只是存取 toothose 負責儲存體的存取控制。 如果 hello 不當人士取得 toothese 金鑰的存取權，他們將可以完全控制的儲存體和無法取代、 刪除或新增檔案 toostorage。 可能會危害組織或客戶的惡意程式碼和其他類型的內容也包括在內。

您仍然需要儲存體中的方式 tooprovide 存取 tooobjects。 更細微的 tooprovide 存取，您可以利用[共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md)(SAS)。 hello SAS 可讓您 tooshare 儲存體中的特定物件的預先定義的時間間隔，並具備特定的權限。 共用存取簽章可讓您 toodefine:

- hello 的 hello 透過 SAS 有效間隔，包括 hello 開始時間和 hello 到期時間。
- hello hello SAS 所授與權限。 例如，在 blob 上的 SAS 可能授與使用者讀取和寫入權限 toothat blob，但刪除權限。
- 選擇性的 IP 位址或 IP 位址範圍從中接受 Azure 儲存體 hello SAS。 例如，您可以指定屬於 tooyour 組織某個範圍的 IP 位址。 這可讓 SAS 的安全性更上一層樓。
- hello 通訊協定的 Azure 儲存體接受 hello SAS。 您可以使用此使用 HTTPS 的選擇性參數 toorestrict 存取 tooclients。

SAS 可讓您想 tooshare tooshare 內容 hello 方法不提供儲存體帳戶金鑰。 一律在應用程式中使用 SAS 是安全的方式 tooshare 您的儲存體資源，而不會危害您的儲存體帳戶金鑰。

詳細資訊，請參閱 toolearn[使用共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md)(SAS)。 深入了解潛在的風險和建議 toomitigate toolearn 這些風險，請參閱[最佳做法時使用 SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。

### <a name="use-managed-disks-for-vms"></a>對 VM 使用受控磁碟

當您選擇[Azure 受管理磁碟](../storage/storage-managed-disks-overview.md)，Azure 管理您使用的 VM 磁碟的 hello 儲存體帳戶。 您只需要 toodo 是選擇 hello 類型 （高階或標準） 的磁碟和 hello 磁碟大小。Azure 儲存體將會執行 hello rest。 您不需要 tooworry 可能否則需 tooyou toomultiple 儲存體帳戶的延展性限制的相關。

詳細資訊，請參閱 toolearn[常見問題集有關 managed 與 unmanaged 高階磁碟](../storage/storage-faq-for-disks.md)。

### <a name="use-role-based-access-control"></a>使用角色型存取控制

我們稍早討論在您儲存體帳戶 tooother 用戶端中使用共用存取簽章 (SAS) toogrant 有限存取 tooobjects，而不會讓您帳戶的儲存體帳戶金鑰。 有時 hello 與針對儲存體帳戶的特定作業相關聯的風險，勝過 hello 優點的 SAS。 有時會以其他方式較簡單的 toomanage 存取。

另一個方式 toomanage 存取是 toouse[所有存取控制](../active-directory/role-based-access-control-what-is.md)(RBAC)。 使用 RBAC，您著重於讓員工 hello 確切權限，它們需要依據 hello 需要 tooknow 和最小權限的安全性原則。 太多權限可以公開帳戶 tooattackers。 權限太少則會讓員工無法有效率地完成工作。 RBAC 可以為 Azure 提供更細緻的存取管理來協助解決這個問題。 這是必要的 tooenforce 安全性原則所需的資料存取的組織。

您可以利用 Azure tooassign 權限 toousers 中的內建 RBAC 角色。 請考慮使用儲存體帳戶參與者需要 toomanage 儲存體帳戶和傳統的儲存體帳戶參與者角色 toomanage 傳統儲存體帳戶的雲端操作員。 雲端操作員需要 toomanage Vm，但不是 hello 虛擬網路或儲存體帳戶 toowhich 它們互相連線，請考慮將它們加入 toohello 虛擬機器參與者角色。

未利用諸如 RBAC 等功能來強制執行資料存取控制的組織，可能會對其使用者提供超過所需的權限。 這可讓它們不應該在 hello 第一個位置中有某些使用者存取 toodata 帶來 toodata 洩露。

toolearn 有關 RBAC 的詳細資訊請參閱：

- [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)
- [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md)
- [Azure 儲存體安全性指南](../storage/common/storage-security-guide.md)如上如何 toosecure 您的儲存體帳戶與 RBAC 的詳細資訊

## <a name="storage-encryption"></a>儲存體加密
### <a name="use-client-side-encryption-for-high-value-data"></a>對高價值的資料使用用戶端加密

用戶端加密啟用您 tooprogrammatically 之前上傳 tooAzure 儲存體加密傳輸中的資料，並以程式設計方式擷取從儲存體時，解密資料。  此功能除了可以將傳輸中的資料加密，也可以將待用資料加密。  用戶端加密是 hello 最安全的加密資料的方法，但其不需要您 toomake 以程式設計方式變更 tooyour 應用程式，然後備妥的金鑰管理程序。

用戶端加密也可讓您 toohave 唯一控制加密金鑰。  您可以產生和管理自己的加密金鑰。  用戶端加密使用信封的技術，其中 hello Azure 儲存體用戶端程式庫產生內容的加密金鑰 (CEK)，然後再包裝 （加密） 使用 hello 金鑰的加密金鑰 (KEK)。 hello KEK 索引鍵的識別項所識別，可非對稱金鑰組或對稱金鑰，可以是本機管理或儲存在[Azure 金鑰保存庫](../key-vault/key-vault-whatis.md)。

用戶端加密是內建 hello Java 和 hello.NET 儲存體用戶端程式庫。  如需有關將用戶端應用程式資料加密並產生及管理自有加密金鑰的資訊，請參閱 [Microsoft Azure 儲存體的用戶端加密和 Azure Key Vault](../storage/storage-client-side-encryption.md)。

### <a name="azure-disk-encryption-for-vms"></a>VM 的 Azure 磁碟加密
Azure 磁碟加密是協助您加密 Windows 和 Linux IaaS 虛擬機器磁碟的功能。 Azure 磁碟加密會利用 hello 業界標準 BitLocker 功能的 Windows 和 Linux tooprovide 磁碟區加密 hello OS hello DM Crypt 功能和 hello 資料磁碟。 hello 方案整合 Azure 金鑰保存庫 toohelp 您控制和管理您金鑰保存庫的訂用帳戶中的 hello 磁碟加密金鑰和密碼。 hello 方案也能確保 hello 虛擬機器磁碟上的所有資料會留在您 Azure 儲存體都加密。

請參閱 [Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](azure-security-disk-encryption.md)。

### <a name="storage-service-encryption"></a>儲存體服務加密
當[儲存體服務加密](../storage/storage-service-encryption.md)hello 資料檔案儲存為啟用，會自動使用 aes-256 加密進行加密。 Microsoft 會處理所有的 hello 加密、 解密和金鑰管理。 這項功能適用於 LRS 及 GRS 備援類型。

## <a name="next-steps"></a>後續步驟
這篇文章導入您的 Azure 儲存體保護您的 PaaS web 與行動應用程式的安全性最佳作法的 tooa 集合。 toolearn 深入了解保護您的 PaaS 部署，請參閱：

- [保護 PaaS 部署](security-paas-deployments.md)
- [使用 Azure App Service 來保護 PaaS Web 與行動應用程式](security-paas-applications-using-app-services.md)
- [保護 Azure 中的 PaaS 資料庫](security-paas-applications-using-sql.md)
