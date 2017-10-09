---
title: "保護個人資料使用加密待用 aaaAzure |Microsoft 文件"
description: "這篇文章是協助您使用 Azure tooprotect 個人資料的一系列的一部分"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>Azure 加密技術：使用加密保護個人待用資料

這篇文章可協助您了解及使用 Azure 加密技術 toosecure 資料靜止。

待用資料加密務必要做為最佳作法 tooprotect 機密或個人資料以及 toomeet 相容性和資料的隱私權需求。
設計的 tooprevent hello 攻擊者存取 hello 未加密資料，方法是確保資料會加密磁碟的 hello 靜止的加密。

## <a name="scenario"></a>案例 

大型出航公司搬遷後在 hello 美國，展開在 hello 地中海與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。 toosupport 努力，它所取得數個較小的出航行位於義大利、 德國、 丹麥和 hello 英國

hello 公司使用 Microsoft Azure toostore 公司資料 hello 雲端中。 這可能包括員工及/或客戶資訊，例如：

- 地址
- 電話號碼
- 稅務識別編號
- 醫療資訊
- 信用卡資訊

hello 公司必須保護員工和客戶資料的 hello 的隱私權，同時進行資料存取 toothose 部門需要它。 (例如薪資部門和訂位部門) 可以存取資料。

hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。

### <a name="problem-statement"></a>問題陳述

hello 公司必須保護員工和客戶的個人資料的 hello 的隱私權，同時進行資料存取 toothose 部門需要 （例如，薪資和保留項目的部門）。 此個人資料會儲存在 hello 公司控制資料中心外部，而不在 hello 公司的實體控制項。

### <a name="company-goal"></a>公司目標

多層的深度防禦的安全性策略的一部分，就會加密所有資料來源，包含個人資料，包括雲端儲存體中公司目標 tooensure。 如果未經授權的人員獲得存取 toohello 個人資料，它必須是會轉譯無法讀取的格式。 對於使用者和系統管理員而言，套用加密應該很容易或很透明。

## <a name="solutions"></a>解決方案

Azure 服務可提供多個工具和技術 toohelp 加密保護靜止的個人資料。

### <a name="azure-key-vault"></a>Azure 金鑰保存庫

[Azure 金鑰保存庫](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)提供安全的儲存體的 Azure 服務中的靜止使用 tooencrypt 資料 hello 金鑰並且 hello 建議儲存和管理的金鑰方案。 儲存的重要 toosecuring 資料加密金鑰管理。

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>如何使用 Azure 金鑰保存庫 tooprotect 金鑰加密的個人資料？

toouse Azure 金鑰保存庫，您需要訂用帳戶 tooan Azure 帳戶。 您也需要安裝 Azure Powershell。 步驟包括使用 PowerShell cmdlet toodo hello 下列：

1. 連接 tooyour 訂用帳戶

2. 建立金鑰保存庫

3. 新增金鑰或密碼 toohello 金鑰保存庫

4. 註冊將使用金鑰保存庫 hello 與 Azure Active Directory 應用程式

5. 授權 hello 應用程式 toouse hello 金鑰或密碼

toocreate 金鑰保存庫中，使用 hello 新增 AzureRmKeyVault PowerShell CmDlt。 您將會指派保存庫名稱、資源群組名稱和地理位置。 管理透過其他 Cmdlet 的索引鍵時，您將使用 hello 保存庫名稱。 使用透過 hello REST API 的 hello 保存庫的應用程式會使用 hello 保存庫 URI。

Azure Key Vault 可為您提供受軟體保護的金鑰；或者，您也可以匯入 .PFX 檔案中的現有金鑰。 您也可以在 hello 保存庫中儲存機密資訊 （密碼）。

您也可以在本機 HSM 中產生金鑰並將金鑰傳輸 tooHSMs hello 金鑰保存庫服務中的沒有 hello 離開 hello HSM 界限的索引鍵。

中的詳細說明如何使用 Azure 金鑰保存庫，請依照下列步驟 hello[開始使用 Azure 金鑰保存庫。](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

如需搭配 Azure Key Vault 使用的 PowerShell Cmdlet 清單，請參閱 [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0)。

### <a name="azure-disk-encryption-for-windows"></a>Windows 適用的 Azure 磁碟加密

[Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)會保護 Azure 虛擬機器上的個人待用資料，並與 Azure Key Vault 整合。 Azure 磁碟加密使用[BitLocker](https://technet.microsoft.com/library/cc732774.aspx)在 Windows 和[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux tooencrypt 中同時 hello OS 和 hello 資料磁碟。 Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 以及 Windows 8 和 Windows 10 用戶端支援 Azure 磁碟加密。

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>如何使用 Azure 磁碟加密 tooprotect 個人資料？

toouse Azure 磁碟加密，您需要訂用帳戶 tooan Azure 帳戶。 下列 hello tooenable Azure 磁碟加密適用於 Windows 及 Linux Vm:

1. 使用 hello Azure 磁碟加密 Resource Manager 範本、 PowerShell 或 hello 命令列介面 (CLI) tooenable 磁碟加密，並指定的加密組態。 

2. 授與存取 toohello Azure 平台 tooread hello 從金鑰保存庫的加密內容。

3. 提供 Azure Active Directory (AAD) 應用程式識別 toowrite hello 加密金鑰材料 tooyour 金鑰保存庫。

Azure 將會更新 hello VM 和 hello 金鑰保存庫設定，與您加密的 VM 設定。

當您設定您的金鑰保存庫 toosupport Azure 磁碟加密時，您可以提高的安全性和加密的虛擬機器 toosupport 備份加入加密金鑰 (KEK)。

![](media/protect-personal-data-at-rest/create-key.png)

如需特定部署案例和使用者體驗的詳細指示，請參閱 [Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)。

### <a name="azure-storage-service-encryption"></a>Azure 儲存體服務加密

[Azure 儲存體服務加密 (SSE) 中的靜止資料](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption)可協助您保護與防衛資料 toomeet 您組織的安全性與相容性承諾。 Azure 儲存體自動會使用 256 位元 AES 加密先前 toopersisting toostorage 資料加密和解密先前 tooretrieval。 這個服務適用於 Azure Blob 和檔案。

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>如何使用儲存體服務加密 tooprotect 個人資料？

tooenable 儲存體服務加密，請勿 hello 遵循：

1. 登入 hello Azure 入口網站。

2. 選取儲存體帳戶。

3. 在 [設定] 底下 hello Blob 服務區段中，選取加密。

4. 在 hello 檔案服務 區段中，選取 加密。

按一下 hello 加密設定之後，您可以啟用或停用儲存體服務加密。

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

新的資料將會加密。 此儲存體帳戶中現有檔案的資料將保持未加密狀態。

啟用加密之後, 將複製資料 toohello 儲存體帳戶使用其中一種 hello 下列方法：

1. 複製 blob 或檔案以 hello [AzCopy 命令列公用程式](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy)。

2. [掛上使用 SMB 檔案共用](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows)因此您可以使用公用程式，例如 Robocopy toocopy 檔案。

3. 複製 blob 或檔案資料 tooand 從 blob 儲存體或儲存體帳戶使用[儲存體用戶端程式庫，例如.NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs)。

4.  使用[存放裝置總管](https://docs.microsoft.com/en-us/azure/storage/storage-explorers)tooupload blob tooyour 儲存體帳戶並啟用加密。

### <a name="transparent-data-encryption"></a>透明資料加密

透明資料加密 (TDE) 是 SQL Azure，您可以用來加密這兩個 hello 資料庫和伺服器層級的資料中的功能。 現在預設會在所有新建立的資料庫上啟用 TDE。 TDE 會執行即時 I/O 加密和解密的 hello 資料和記錄檔。

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>如何使用 TDE tooprotect 個人資料？

使用 hello REST API 或 PowerShell，您可以透過 hello Azure 入口網站設定 TDE。 在現有的資料庫使用 hello Azure 入口網站，tooenable TDE hello 遵循：

1. 請瀏覽 hello Azure 入口網站在<https://portal.azure.com>和使用您的 Azure 系統管理員或參與者帳戶登入。

2. 在 hello 左邊的橫幅中，按一下 tooBROWSE，，然後按一下 SQL 資料庫。

3. Hello 左窗格中選取的 SQL 資料庫，按一下您的使用者資料庫。

4. 在 hello 資料庫刀鋒視窗中，按一下 所有設定。

5. 在 hello 設定刀鋒視窗中，按一下 透明資料加密部分 tooopen hello 透明資料加密 刀鋒視窗。

6. 在 hello 資料加密 刀鋒視窗，將資料加密 按鈕 tooOn hello，，然後按一下儲存 （hello 頁面頂端的 hello） tooapply hello 設定。 hello 加密的狀態會顯示概略 hello 透明資料加密的 hello 的進度。

![啟用資料加密](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

說明如何在 hello 文章中找到 tooenable TDE，以及有關解密 TDE 保護的資料庫和多個[Azure SQL Database 的透明資料加密。](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>摘要

hello 公司可以完成其加密儲存在 hello Azure 雲端中的個人資料的目標。 他們可以使用 Azure 磁碟加密來進行這太保護整個磁碟區。 這可能包括 hello 作業系統檔案和存放個人識別資訊與其他敏感性資料的資料檔案。 Azure 儲存體服務加密可使用的 tooprotect 個人資料會儲存在 blob 和檔案。 對於儲存在 Azure SQL Database 中的資料，透明資料加密會提供保護，以防止未經授權公開個人資訊。

在 Azure 中使用的 tooencrypt 資料 tooprotect hello 索引鍵，hello 公司可以使用 Azure 金鑰保存庫。 這可簡化 hello 金鑰管理程序，並啟用 hello 公司 toomaintain 控制存取和個人資料加密金鑰。

## <a name="next-steps"></a>後續步驟

- [Azure 磁碟加密疑難排解指南](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [加密 Azure 虛擬機器](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Azure Data Lake Store 中的資料加密](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [Azure Cosmos DB 資料庫待用加密](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
