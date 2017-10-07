---
title: "aaaAllow 應用程式 tooretrieve Azure 堆疊金鑰保存庫密碼 |Microsoft 文件"
description: "使用 Azure 堆疊金鑰保存庫中的範例應用程式 toowork"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/04/2017
ms.author: sngun
ms.openlocfilehash: 2ff3f0bab86d9d1934b463f72124863d29dbe696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-for-key-vault"></a>執行 hello 範例應用程式的金鑰保存庫

在本指南中，您將使用範例應用程式 tooretrieve 密鑰和密碼從金鑰保存庫。

## <a name="download-hello-samples-and-prepare"></a>下載 hello 範例和準備
從 hello 下載 hello Azure 金鑰保存庫用戶端範例[Azure 金鑰保存庫用戶端範例頁面](https://www.microsoft.com/en-us/download/details.aspx?id=45343)。

擷取 hello hello.zip 檔案 tooyour 本機電腦上的內容。

讀取 hello **README.md** （這是文字檔案） 的檔案，然後依照 hello 指示。

## <a name="run-sample-1--hellokeyvault"></a>執行範例 #1 部--HelloKeyVault
HelloKeyVault 是主控台應用程式的逐步解說 hello 受到金鑰保存庫的重要案例：

1. 建立/匯入金鑰 （HSM 或軟體）
2. 加密使用內容金鑰的密碼
3. 包裝 hello 內容金鑰使用金鑰保存庫金鑰
4. Unwrap hello 內容金鑰
5. 解密 hello 密碼
6. 設定密碼

該主控台應用程式應該不執行任何變更，不同之處在於會根據 toohello 下列步驟更新 App.Config 中的 hello 適當的組態設定：

1. 與您的保存庫 URL、 應用程式主體識別碼、 密碼更新 HelloKeyVault\App.config hello 應用程式組態設定。 hello 資訊可以選擇性地使用產生**scripts\GetAppConfigSettings.ps1**。
2. 更新 hello hello GetAppConfigSettings.ps1 中的強制變數值。
3. 啟動 hello Windows PowerShell 視窗。
4. 執行 hello PowerShell 視窗中的 hello GetAppConfigSettings.ps1 指令碼。
5. 將 hello 結果 hello 指令碼 toohello HelloKeyVault\App.config 檔案複製。

## <a name="next-steps"></a>後續步驟
[使用金鑰保存庫密碼部署 VM](azure-stack-kv-deploy-vm-with-secret.md)

[使用 Key Vault 憑證部署 VM](azure-stack-kv-push-secret-into-vm.md)

