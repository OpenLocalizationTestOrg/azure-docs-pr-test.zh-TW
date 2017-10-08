---
title: "aaaAzure 堆疊金鑰保存庫簡介 |Microsoft 文件"
description: "了解 Azure Stack Key Vault 如何管理金鑰和祕密"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 70f1684a-3fbb-4cd1-bf29-9f9882e98fe9
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/04/2017
ms.author: sngun
ms.openlocfilehash: 12bf9c219c4b2bba37467cafca721a632caa9f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tookey-vault-in-azure-stack"></a>簡介 tooKey Azure 堆疊中的保存庫

## <a name="before-you-start"></a>開始之前
本文章假設 hello 下列：

* Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello 金鑰保存庫服務。  
* 使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。  
* [PowerShell 設定為搭配 Azure Stack 使用](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a>Key Vault 的基本概念
Azure Stack 中的 Key Vault 可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和祕密。 您可以使用 Key Vault 來加密金鑰和祕密 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.pfx 檔案和密碼)。

金鑰保存庫可簡化 hello 金鑰管理程序，並讓您 toomaintain 控制項的索引鍵，以存取並加密資料。 開發人員可以建立開發和測試以分鐘為單位的索引鍵，並再順暢地移轉 tooproduction 索引鍵。 安全性系統管理員可以授與，並撤銷權限 tookeys，視需要。

只要擁有 Azure Stack 訂用帳戶，任何人都可以建立和使用金鑰保存庫。 雖然開發人員和安全性系統管理員，將有益於金鑰保存庫，它可以實作並管理組織的其他 Azure 堆疊服務 hello 雲端系統管理員所管理。 比方說，hello 雲端系統管理員可以使用 Azure 堆疊訂用帳戶登入、 哪些 toostore 機碼中，建立 hello 組織保存庫，就負責處理這些作業的工作：

* 建立或匯入金鑰或密碼
* 撤銷或刪除金鑰或密碼
* 授權使用者或應用程式 tooaccess hello 金鑰保存庫，讓他們可以管理或使用其索引鍵和機密資料
* 設定金鑰使用方法 (例如，簽署或加密)

hello 雲端系統管理員可以從他們的應用程式的 Uri toocall 提供開發人員並提供金鑰的使用情況記錄資訊的安全性系統管理員。

開發人員也可以管理 hello 機碼直接使用 Api。 如需詳細資訊，請參閱 hello 金鑰保存庫開發人員手冊 》。

## <a name="scenarios"></a>案例
hello 下表描述的金鑰保存庫可協助開發人員和安全性系統管理員需求 hello hello 案例：

### <a name="developer-for-an-azure-stack-application"></a>Azure Stack 應用程式的開發人員
**問題**： 我想要用於簽署及加密，會使用金鑰的 Azure 堆疊 toowrite 應用程式，但我想要這些 toobe 外部我的應用程式從如此 hello 方案適合地理位置分散的應用程式。

**說明**：金鑰會儲存在保存庫中，並且視需要由 URI 叫用。

### <a name="developer-for-software-as-a-service-saas"></a>軟體即服務 (SaaS) 的開發人員
**問題：**我不想要顯示 hello 責任或潛在責任我的客戶金鑰和密碼。

**說明**：客戶可以將他們自己的金鑰匯入 Azure Stack 並加以管理。 我想客戶 tooown 並管理其索引鍵，讓我可以專注於我要怎麼最佳，這提供 hello 核心軟體功能。

### <a name="chief-security-officer-cso"></a>資訊安全長 (CSO)
**問題：**我想 toomake 確定我的組織在 hello 金鑰生命週期的控制權，而且可以監視金鑰使用方式。

**說明**：Key Vault 的設計，便是讓 Microsoft 無法看見或擷取您的金鑰。  當應用程式需要 tooperform 密碼編譯作業時使用客戶的金鑰時，金鑰保存庫會代表 hello 應用程式。 hello 應用程式不會看到 hello 客戶索引鍵。  雖然我們會使用多個 Azure 堆疊服務和資源，但我想 toomanage hello 索引鍵，從 Azure 堆疊中的單一位置。 hello 保存庫會提供單一介面，不論多少的保存庫中有 Azure 堆疊，哪些區域它們支援，以及哪些應用程式使用它們。

## <a name="next-steps"></a>後續步驟

* [管理 Azure 堆疊使用 hello 入口網站中的金鑰保存庫](azure-stack-kv-manage-portal.md)  
* [使用 PowerShell 管理 Azure Stack 中的 Key Vault](azure-stack-kv-manage-powershell.md)
