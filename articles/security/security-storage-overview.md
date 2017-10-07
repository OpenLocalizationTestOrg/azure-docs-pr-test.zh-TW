---
title: "可以搭配 Azure 儲存體的 aaaSecurity 功能 |Microsoft 文件"
description: " 本文章提供可以搭配 Azure 儲存體的 hello 核心 Azure 的安全性功能的概觀。 "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Azure 儲存體安全性概觀
Azure 儲存體是 hello 雲端儲存體解決方案，依賴持續性、 可用性和延展性 toomeet hello 需求的客戶的現代應用程式。 Azure 儲存體提供一組完整的安全性功能：

* 可以使用角色型存取控制與 Azure Active Directory 來保護 hello 儲存體帳戶。
* 您可以使用用戶端加密、HTTP 或 SMB 3.0，在應用程式和 Azure 之間進行傳輸時保護資料的安全。
* 資料可以設定自動加密 toobe 寫入 tooAzure 使用儲存體服務加密的存放裝置時。
* 虛擬機器所使用的作業系統和資料磁碟可以設定 toobe 使用 Azure 磁碟加密進行加密。
* Azure 儲存體中的委派的存取 toohello 資料物件可以使用共用存取簽章授與。
* 存取儲存體時使用的其他人的 hello 驗證方法可以使用儲存體分析追蹤。

Azure 儲存體中的安全性更詳細探討，請參閱 hello [Azure 儲存體安全性指南 》](../storage/common/storage-security-guide.md)。 本指南提供深入探討 hello 安全性功能，Azure 儲存體的儲存體帳戶金鑰，例如資料加密傳輸中和在其餘部分和儲存體分析。

本文提供可與「Azure 儲存體」搭配使用的 Azure 安全性功能概觀。 提供給每項功能的詳細資料，因此，您可以深入的 tooarticles 時，會提供連結。

以下是本文章涵蓋 hello 核心功能 toobe:

* 角色型存取控制
* 委派的存取 toostorage 物件
* 傳輸中加密
* 待用加密/儲存體服務加密
* Azure 磁碟加密
* Azure 金鑰保存庫

## <a name="role-based-access-control-rbac"></a>角色型存取控制 (RBAC)
您可以使用角色型存取控制 (RBAC) 來保護儲存體帳戶。 限制存取根據 hello[需要 tooknow](https://en.wikipedia.org/wiki/Need_to_know)和[最小權限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)安全性原則是命令式 tooenforce 安全性原則所需的資料存取的組織。 這些存取權限會授與指定適當 RBAC 角色 toogroups hello 與應用程式在特定範圍內。 您可以使用[內建的 RBAC 角色](../active-directory/role-based-access-built-in-roles.md)，例如儲存體帳戶參與者 tooassign 權限 toousers。

深入了解：

* [Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>委派的存取 toostorage 物件
共用的存取簽章 (SAS) 提供儲存體帳戶中的委派的存取 tooresources。 hello SAS 表示您可以授與用戶端有限的儲存體帳戶中的權限 tooobjects 指定期間內的時間與指定權限集。 您可以授與這些有限權限，而不需要 tooshare 帳戶存取金鑰。 hello SAS 是包含在其查詢參數中所有的 hello 資訊所需的已驗證的存取 tooa 儲存體資源的 URI。 tooaccess 以 hello SAS 存放裝置資源，hello 用戶端只需要 tooprovide hello SAS toohello 適當建構函式或方法。

深入了解：

* [了解 hello SAS 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [透過 Blob 儲存體來建立與使用 SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>傳輸中加密
傳輸中加密是透過網路傳輸資料時用來保護資料的機制。 使用 Azure 儲存體，您可以使用下列各向來保護資料︰

* [傳輸層級加密](../storage/common/storage-security-guide.md#encryption-in-transit)，例如從 Azure 儲存體傳入或傳出資料時的 HTTPS。
* [連線加密](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares)，例如 Azure 檔案共用的 SMB 3.0 加密。
* [用戶端加密](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage)，tooencrypt hello 資料在傳輸之前儲存和 toodecrypt hello 資料超出儲存體傳輸後。

深入了解用戶端加密︰

* [Microsoft Azure 儲存體的用戶端加密](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [雲端安全性控制項系列︰加密傳輸中的資料](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>待用加密
對許多組織來說， [待用資料加密](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) 是達到資料隱私性、法規遵循及資料主權的必要步驟。 有三個 Azure 功能可提供「待用」資料的加密。

* [儲存體服務加密](../storage/common/storage-security-guide.md#encryption-at-rest)可讓您 toorequest 寫入它 tooAzure 儲存體時，hello 儲存體服務會自動加密資料。
* [用戶端加密](../storage/common/storage-security-guide.md#client-side-encryption)也提供的加密在靜止 hello 功能。
* [Azure 磁碟加密](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines)可讓您 tooencrypt hello OS 磁碟和 IaaS 虛擬機器所使用的資料磁碟。

深入了解儲存體服務加密：

* [Azure 儲存體服務加密](https://azure.microsoft.com/services/storage/)適用於 [Azure Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)。 如需其他 Azure 儲存體類型的詳細資訊，請參閱[檔案](https://azure.microsoft.com/services/storage/files/)、[磁碟 (進階儲存體)](https://azure.microsoft.com/services/storage/premium-storage/)、[資料表](https://azure.microsoft.com/services/storage/tables/)和[佇列](https://azure.microsoft.com/services/storage/queues/)。
* [待用資料的 Azure 儲存體服務加密](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Azure 磁碟加密
適用於虛擬機器 (VM) 的 Azure 磁碟加密會使用您在 [Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)所控制的金鑰與原則將 VM 磁碟 (包括開機和資料磁碟) 加密，協助您達成組織安全性與相容性需求。

適用於 VM 的磁碟加密可用於 Linux 與 Windows 作業系統。 它也會使用金鑰保存庫 toohelp 保護、 管理及稽核磁碟加密金鑰的使用。 VM 磁碟中的所有 hello 資料都加密待用使用業界標準加密技術在 Azure 儲存體帳戶。 hello 適用於 Windows 的磁碟加密解決方案根據[Microsoft BitLocker 磁碟機加密](https://technet.microsoft.com/library/cc732774.aspx)，並且根據 hello Linux 方案[dm crypt](https://en.wikipedia.org/wiki/Dm-crypt)。

深入了解：

* [適用於 Windows 和 Linux IaaS 虛擬機器的 Azure 磁碟加密](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>Azure 金鑰保存庫
Azure 磁碟加密使用[Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)toohelp 您控制，和您金鑰保存庫的訂用帳戶，同時確保 hello 虛擬機器磁碟中的所有資料會都加密在靜止於 Azure 中管理磁碟加密金鑰和密碼儲存體。 您應該使用金鑰保存庫 tooaudit 金鑰和原則使用方式。

深入了解：

* [什麼是 Azure 金鑰保存庫？](../key-vault/key-vault-whatis.md)
* [開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)
