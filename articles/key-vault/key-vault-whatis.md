---
title: "aaaWhat 是 Azure 金鑰保存庫？ | Microsoft Docs"
description: "Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。 使用 Azure 金鑰保存庫之後，客戶可以加密金鑰和密碼 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.PFX 檔案和密碼)，方法是使用受硬體安全模組 (HSM) 保護的金鑰。"
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e759df6f-0638-43b1-98ed-30b3913f9b82
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 296fcce03658b96b84afab299b73681bbe8ac9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-key-vault"></a>什麼是 Azure 金鑰保存庫？
大部分地區均提供 Azure 金鑰保存庫。 如需詳細資訊，請參閱 hello[金鑰保存庫定價頁面](https://azure.microsoft.com/pricing/details/key-vault/)。

## <a name="introduction"></a>簡介
Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。 使用金鑰保存庫之後，您可以加密金鑰和密碼 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.PFX 檔案和密碼)，方法是使用受硬體安全模組 (HSM) 保護的金鑰。 為了加強保證，您可以在 HSM 中匯入或產生金鑰。 如果您選擇此，Microsoft 處理程序 toodo 您 FIPS 140-2 中的索引鍵層級 2 的已驗證的 Hsm （硬體和韌體）。  

金鑰保存庫可簡化 hello 金鑰管理程序，並讓您 toomaintain 控制項的索引鍵，以存取並加密資料。 開發人員可以建立開發和測試以分鐘為單位的索引鍵，並再順暢地移轉 tooproduction 索引鍵。 安全性系統管理員可以授與，並撤銷權限 tookeys，視需要。

下列表格 toobetter 使用 hello 了解如何金鑰保存庫可協助開發人員和安全性管理員 toomeet hello 需求。

| 角色 | 問題陳述 | Azure 金鑰保存庫已解決問題 |
| --- | --- | --- |
| Azure 應用程式的開發人員 |「 我想要用於簽署及加密，會使用金鑰的 Azure toowrite 應用程式，但我想要這些機碼 toobe 外部我的應用程式從如此 hello 方案適合地理位置分散的應用程式。 <br/><br/>我也想這些金鑰和秘密 toobe，受保護，而不需要自行 toowrite hello 程式碼。 我也想這些金鑰和秘密 toobe 輕鬆我 toouse 從我的應用程式，以獲得最佳效能。 」 |√ 金鑰會儲存在保存庫中，並且視需要由 URI 叫用。<br/><br/> √ Azure 使用會業界標準演算法、金鑰長度和硬體安全性模組 (HSM) 保護金鑰。<br/><br/> √ 索引鍵會處理相同位於 hello 的 Hsm hello 應用程式的 Azure 資料中心。 這提供更佳的可靠性和減少的延遲比如果 hello 金鑰會存放在不同的位置，例如在內部部署。 |
| 軟體即服務 (SaaS) 的開發人員 |「 為我的客戶租用戶金鑰和密碼不希望 hello 責任或潛在的責任。 <br/><br/>我想 hello 客戶 tooown 和管理它們的索引鍵，讓我可以專注於我要怎麼最佳，這提供 hello 核心軟體功能。 」 |√ 客戶可以將他們自己的金鑰匯入 Azure 並加以管理。 SaaS 應用程式需要 tooperform 密碼編譯作業，使用其客戶的金鑰，金鑰保存庫，便會執行這些作業代表 hello 應用程式。 hello 應用程式不會看到 hello 客戶索引鍵。 |
| 資訊安全長 (CSO) |「 我想 tooknow 我們的應用程式符合 FIPS 140-2 層級 2 Hsm 安全的金鑰管理。 <br/><br/>我想 toomake 確定我的組織在 hello 金鑰生命週期的控制權，可以監視金鑰使用方式。 <br/><br/>然後我們使用多個 Azure 服務和資源，但是我想要從 Azure 中的單一位置 toomanage hello 索引鍵。 」 |√ HSM 已通過 FIPS 140-2 Level 2 驗證。<br/><br/>√ 金鑰保存庫經過設計，所以 Microsoft 不會看見或擷取您的金鑰。<br/><br/>√ 近乎即時的金鑰使用情況記錄。<br/><br/>√ hello 保存庫會提供單一介面，不論多少的保存庫中有 Azure 中，哪些區域它們支援，以及哪些應用程式使用它們。 |

只要擁有 Azure 訂用帳戶，任何人都可以建立和使用金鑰保存庫。 雖然金鑰保存庫有益於開發人員和安全性系統管理員，但管理組織其他 Azure 服務的組織系統管理員也可以實作並管理金鑰保存庫。 比方說，此系統管理員會使用 Azure 訂用帳戶登入、 建立 hello 組織保存庫中哪些 toostore 索引鍵，而則是 負責操作工作，例如：

* 建立或匯入金鑰或密碼
* 撤銷或刪除金鑰或密碼
* 授權使用者或應用程式 tooaccess hello 金鑰保存庫，讓他們可以管理或使用其索引鍵和機密資料
* 設定金鑰使用方法 (例如，簽署或加密)
* 監視金鑰使用方法

此系統管理員接著應用程式中，從 Uri toocall 提供開發人員，並提供金鑰的使用情況記錄資訊的安全性系統管理員。 

   ![Azure 金鑰保存庫概觀][1]

開發人員也可以管理 hello 機碼直接使用 Api。 如需詳細資訊，請參閱[hello 金鑰保存庫開發人員手冊 》](key-vault-developers-guide.md)。

## <a name="next-steps"></a>後續步驟
如需適用於系統管理員的開始使用教學課程，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。

如需金鑰保存庫使用方法記錄的詳細資訊，請參閱 [Azure 金鑰保存庫記錄](key-vault-logging.md)。

如需搭配 Azure 金鑰保存庫使用金鑰和密碼的詳細資訊，請參閱[關於金鑰、密碼和憑證](https://msdn.microsoft.com/library/azure/dn903623\(v=azure.1\).aspx)。

<!--Image references-->
[1]: ./media/key-vault-whatis/AzureKeyVault_overview.png
