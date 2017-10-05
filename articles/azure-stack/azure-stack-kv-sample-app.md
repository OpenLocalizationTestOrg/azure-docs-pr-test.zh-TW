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
# <a name="run-the-sample-application-for-key-vault"></a><span data-ttu-id="9ad7e-103">執行金鑰保存庫的範例應用程式</span><span class="sxs-lookup"><span data-stu-id="9ad7e-103">Run the sample application for Key Vault</span></span>

<span data-ttu-id="9ad7e-104">在本指南中，您將使用範例應用程式從金鑰保存庫擷取密碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-104">In this guide, you'll use a sample application to retrieve secrets and passwords from Key Vault.</span></span>

## <a name="download-the-samples-and-prepare"></a><span data-ttu-id="9ad7e-105">下載範例和準備</span><span class="sxs-lookup"><span data-stu-id="9ad7e-105">Download the samples and prepare</span></span>
<span data-ttu-id="9ad7e-106">Azure 金鑰保存庫用戶端範例下載[Azure 金鑰保存庫用戶端範例頁面](https://www.microsoft.com/en-us/download/details.aspx?id=45343)。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-106">Download the Azure Key Vault client samples from the [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span>

<span data-ttu-id="9ad7e-107">內容到本機電腦的.zip 檔解壓縮。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-107">Extract the contents of the .zip file to your local computer.</span></span>

<span data-ttu-id="9ad7e-108">讀取**README.md** （這是文字檔案） 的檔案，然後依照指示進行。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-108">Read the **README.md** file (this is a text file), and then follow the instructions.</span></span>

## <a name="run-sample-1--hellokeyvault"></a><span data-ttu-id="9ad7e-109">執行範例 #1 部--HelloKeyVault</span><span class="sxs-lookup"><span data-stu-id="9ad7e-109">Run Sample #1--HelloKeyVault</span></span>
<span data-ttu-id="9ad7e-110">HelloKeyVault 是主控台應用程式的逐步解說也會受到金鑰保存庫的重要案例：</span><span class="sxs-lookup"><span data-stu-id="9ad7e-110">HelloKeyVault is a console application that walks through the key scenarios that are supported by Key Vault:</span></span>

1. <span data-ttu-id="9ad7e-111">建立/匯入金鑰 （HSM 或軟體）</span><span class="sxs-lookup"><span data-stu-id="9ad7e-111">Create/import a key (HSM or software key)</span></span>
2. <span data-ttu-id="9ad7e-112">加密使用內容金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="9ad7e-112">Encrypt a secret using a content key</span></span>
3. <span data-ttu-id="9ad7e-113">自動換行內容的金鑰使用金鑰保存庫金鑰</span><span class="sxs-lookup"><span data-stu-id="9ad7e-113">Wrap the content key using a Key Vault key</span></span>
4. <span data-ttu-id="9ad7e-114">Unwrap 內容金鑰</span><span class="sxs-lookup"><span data-stu-id="9ad7e-114">Unwrap the content key</span></span>
5. <span data-ttu-id="9ad7e-115">解密密碼</span><span class="sxs-lookup"><span data-stu-id="9ad7e-115">Decrypt the secret</span></span>
6. <span data-ttu-id="9ad7e-116">設定密碼</span><span class="sxs-lookup"><span data-stu-id="9ad7e-116">Set a secret</span></span>

<span data-ttu-id="9ad7e-117">該主控台應用程式應該不執行任何變更，不同之處在於會更新 App.Config 中的適當的組態設定，根據下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9ad7e-117">That console application should run with no changes, except that the appropriate configuration settings in App.Config will be updated according to the following steps:</span></span>

1. <span data-ttu-id="9ad7e-118">更新應用程式中的組態設定 HelloKeyVault\App.config 與您的保存庫 URL、 應用程式主體識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-118">Update the app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span></span> <span data-ttu-id="9ad7e-119">資訊可以選擇性地使用產生**scripts\GetAppConfigSettings.ps1**。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-119">The information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span></span>
2. <span data-ttu-id="9ad7e-120">更新必要 GetAppConfigSettings.ps1 中變數的值。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-120">Update the values of the mandatory variables in GetAppConfigSettings.ps1.</span></span>
3. <span data-ttu-id="9ad7e-121">啟動 Windows PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-121">Launch the Windows PowerShell window.</span></span>
4. <span data-ttu-id="9ad7e-122">在 PowerShell 視窗執行 GetAppConfigSettings.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-122">Run the GetAppConfigSettings.ps1 script within the PowerShell window.</span></span>
5. <span data-ttu-id="9ad7e-123">將指令碼的結果複製到 HelloKeyVault\App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="9ad7e-123">Copy the results of the script to the HelloKeyVault\App.config file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ad7e-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ad7e-124">Next steps</span></span>
[<span data-ttu-id="9ad7e-125">使用金鑰保存庫密碼部署 VM</span><span class="sxs-lookup"><span data-stu-id="9ad7e-125">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="9ad7e-126">使用 Key Vault 憑證部署 VM</span><span class="sxs-lookup"><span data-stu-id="9ad7e-126">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

