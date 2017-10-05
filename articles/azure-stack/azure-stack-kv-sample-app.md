---
title: "允許應用程式取出 Azure Stack Key Vault 密碼 | Microsoft Docs"
description: "使用範例應用程式來處理 Azure Stack Key Vault"
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
ms.openlocfilehash: 4b517526d89e7f6c2649e2f12810b4db705defa3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-the-sample-application-for-key-vault"></a>執行金鑰保存庫的範例應用程式

在本指南中，您將使用範例應用程式從金鑰保存庫擷取密碼和密碼。

## <a name="download-the-samples-and-prepare"></a>下載範例和準備
Azure 金鑰保存庫用戶端範例下載[Azure 金鑰保存庫用戶端範例頁面](https://www.microsoft.com/en-us/download/details.aspx?id=45343)。

內容到本機電腦的.zip 檔解壓縮。

讀取**README.md** （這是文字檔案） 的檔案，然後依照指示進行。

## <a name="run-sample-1--hellokeyvault"></a>執行範例 #1 部--HelloKeyVault
HelloKeyVault 是主控台應用程式的逐步解說也會受到金鑰保存庫的重要案例：

1. 建立/匯入金鑰 （HSM 或軟體）
2. 加密使用內容金鑰的密碼
3. 自動換行內容的金鑰使用金鑰保存庫金鑰
4. Unwrap 內容金鑰
5. 解密密碼
6. 設定密碼

該主控台應用程式應該不執行任何變更，不同之處在於會更新 App.Config 中的適當的組態設定，根據下列步驟：

1. 更新應用程式中的組態設定 HelloKeyVault\App.config 與您的保存庫 URL、 應用程式主體識別碼和密碼。 資訊可以選擇性地使用產生**scripts\GetAppConfigSettings.ps1**。
2. 更新必要 GetAppConfigSettings.ps1 中變數的值。
3. 啟動 Windows PowerShell 視窗。
4. 在 PowerShell 視窗執行 GetAppConfigSettings.ps1 指令碼。
5. 將指令碼的結果複製到 HelloKeyVault\App.config 檔案。

## <a name="next-steps"></a>後續步驟
[使用金鑰保存庫密碼部署 VM](azure-stack-kv-deploy-vm-with-secret.md)

[使用 Key Vault 憑證部署 VM](azure-stack-kv-push-secret-into-vm.md)

