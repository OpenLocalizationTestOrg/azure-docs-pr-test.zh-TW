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
# <a name="run-hello-sample-application-for-key-vault"></a><span data-ttu-id="c16fc-103">執行 hello 範例應用程式的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="c16fc-103">Run hello sample application for Key Vault</span></span>

<span data-ttu-id="c16fc-104">在本指南中，您將使用範例應用程式 tooretrieve 密鑰和密碼從金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="c16fc-104">In this guide, you'll use a sample application tooretrieve secrets and passwords from Key Vault.</span></span>

## <a name="download-hello-samples-and-prepare"></a><span data-ttu-id="c16fc-105">下載 hello 範例和準備</span><span class="sxs-lookup"><span data-stu-id="c16fc-105">Download hello samples and prepare</span></span>
<span data-ttu-id="c16fc-106">從 hello 下載 hello Azure 金鑰保存庫用戶端範例[Azure 金鑰保存庫用戶端範例頁面](https://www.microsoft.com/en-us/download/details.aspx?id=45343)。</span><span class="sxs-lookup"><span data-stu-id="c16fc-106">Download hello Azure Key Vault client samples from hello [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span>

<span data-ttu-id="c16fc-107">擷取 hello hello.zip 檔案 tooyour 本機電腦上的內容。</span><span class="sxs-lookup"><span data-stu-id="c16fc-107">Extract hello contents of hello .zip file tooyour local computer.</span></span>

<span data-ttu-id="c16fc-108">讀取 hello **README.md** （這是文字檔案） 的檔案，然後依照 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="c16fc-108">Read hello **README.md** file (this is a text file), and then follow hello instructions.</span></span>

## <a name="run-sample-1--hellokeyvault"></a><span data-ttu-id="c16fc-109">執行範例 #1 部--HelloKeyVault</span><span class="sxs-lookup"><span data-stu-id="c16fc-109">Run Sample #1--HelloKeyVault</span></span>
<span data-ttu-id="c16fc-110">HelloKeyVault 是主控台應用程式的逐步解說 hello 受到金鑰保存庫的重要案例：</span><span class="sxs-lookup"><span data-stu-id="c16fc-110">HelloKeyVault is a console application that walks through hello key scenarios that are supported by Key Vault:</span></span>

1. <span data-ttu-id="c16fc-111">建立/匯入金鑰 （HSM 或軟體）</span><span class="sxs-lookup"><span data-stu-id="c16fc-111">Create/import a key (HSM or software key)</span></span>
2. <span data-ttu-id="c16fc-112">加密使用內容金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="c16fc-112">Encrypt a secret using a content key</span></span>
3. <span data-ttu-id="c16fc-113">包裝 hello 內容金鑰使用金鑰保存庫金鑰</span><span class="sxs-lookup"><span data-stu-id="c16fc-113">Wrap hello content key using a Key Vault key</span></span>
4. <span data-ttu-id="c16fc-114">Unwrap hello 內容金鑰</span><span class="sxs-lookup"><span data-stu-id="c16fc-114">Unwrap hello content key</span></span>
5. <span data-ttu-id="c16fc-115">解密 hello 密碼</span><span class="sxs-lookup"><span data-stu-id="c16fc-115">Decrypt hello secret</span></span>
6. <span data-ttu-id="c16fc-116">設定密碼</span><span class="sxs-lookup"><span data-stu-id="c16fc-116">Set a secret</span></span>

<span data-ttu-id="c16fc-117">該主控台應用程式應該不執行任何變更，不同之處在於會根據 toohello 下列步驟更新 App.Config 中的 hello 適當的組態設定：</span><span class="sxs-lookup"><span data-stu-id="c16fc-117">That console application should run with no changes, except that hello appropriate configuration settings in App.Config will be updated according toohello following steps:</span></span>

1. <span data-ttu-id="c16fc-118">與您的保存庫 URL、 應用程式主體識別碼、 密碼更新 HelloKeyVault\App.config hello 應用程式組態設定。</span><span class="sxs-lookup"><span data-stu-id="c16fc-118">Update hello app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span></span> <span data-ttu-id="c16fc-119">hello 資訊可以選擇性地使用產生**scripts\GetAppConfigSettings.ps1**。</span><span class="sxs-lookup"><span data-stu-id="c16fc-119">hello information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span></span>
2. <span data-ttu-id="c16fc-120">更新 hello hello GetAppConfigSettings.ps1 中的強制變數值。</span><span class="sxs-lookup"><span data-stu-id="c16fc-120">Update hello values of hello mandatory variables in GetAppConfigSettings.ps1.</span></span>
3. <span data-ttu-id="c16fc-121">啟動 hello Windows PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="c16fc-121">Launch hello Windows PowerShell window.</span></span>
4. <span data-ttu-id="c16fc-122">執行 hello PowerShell 視窗中的 hello GetAppConfigSettings.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c16fc-122">Run hello GetAppConfigSettings.ps1 script within hello PowerShell window.</span></span>
5. <span data-ttu-id="c16fc-123">將 hello 結果 hello 指令碼 toohello HelloKeyVault\App.config 檔案複製。</span><span class="sxs-lookup"><span data-stu-id="c16fc-123">Copy hello results of hello script toohello HelloKeyVault\App.config file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c16fc-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c16fc-124">Next steps</span></span>
[<span data-ttu-id="c16fc-125">使用金鑰保存庫密碼部署 VM</span><span class="sxs-lookup"><span data-stu-id="c16fc-125">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="c16fc-126">使用 Key Vault 憑證部署 VM</span><span class="sxs-lookup"><span data-stu-id="c16fc-126">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

