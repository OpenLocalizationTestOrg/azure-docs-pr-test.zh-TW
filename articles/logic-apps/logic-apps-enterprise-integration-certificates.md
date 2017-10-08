---
title: "Enterprise Integration Pack aaaUsing 憑證 |Microsoft 文件"
description: "了解 toouse 以 hello 企業版整合套件的憑證 |Azure 邏輯應用程式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="9ad76-103">了解憑證與企業整合套件</span><span class="sxs-lookup"><span data-stu-id="9ad76-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="9ad76-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9ad76-104">Overview</span></span>
<span data-ttu-id="9ad76-105">企業的整合會使用憑證 toosecure B2B 通訊。</span><span class="sxs-lookup"><span data-stu-id="9ad76-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="9ad76-106">您可以在企業整合應用程式中使用兩種憑證類型：</span><span class="sxs-lookup"><span data-stu-id="9ad76-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="9ad76-107">公開憑證，必須先向憑證授權單位 (CA) 購買。</span><span class="sxs-lookup"><span data-stu-id="9ad76-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="9ad76-108">私人憑證，您可以自行核發。</span><span class="sxs-lookup"><span data-stu-id="9ad76-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="9ad76-109">這些憑證有時會參照的 tooas 自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="9ad76-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="9ad76-110">什麼是憑證？</span><span class="sxs-lookup"><span data-stu-id="9ad76-110">What are certificates?</span></span>
<span data-ttu-id="9ad76-111">憑證是數位文件，以便驗證 hello 電子通訊中的 hello 參與者的身分識別，也可以保護電子通訊。</span><span class="sxs-lookup"><span data-stu-id="9ad76-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="9ad76-112">為什麼要使用憑證？</span><span class="sxs-lookup"><span data-stu-id="9ad76-112">Why use certificates?</span></span>
<span data-ttu-id="9ad76-113">B2B 通訊有時必須確保機密。</span><span class="sxs-lookup"><span data-stu-id="9ad76-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="9ad76-114">企業的整合會使用憑證 toosecure 這些通訊有兩種：</span><span class="sxs-lookup"><span data-stu-id="9ad76-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="9ad76-115">藉由加密 hello 訊息的內容</span><span class="sxs-lookup"><span data-stu-id="9ad76-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="9ad76-116">以數位方式簽署訊息</span><span class="sxs-lookup"><span data-stu-id="9ad76-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="9ad76-117">上傳公開憑證</span><span class="sxs-lookup"><span data-stu-id="9ad76-117">Upload a public certificate</span></span>

<span data-ttu-id="9ad76-118">toouse*公開憑證*B2B 功能與應用程式邏輯，您必須先 tooupload hello 憑證到整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ad76-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="9ad76-119">上傳憑證之後，就可以使用 toohelp hello 中定義其屬性時，安全 B2B 訊息[協議](logic-apps-enterprise-integration-agreements.md)您所建立。</span><span class="sxs-lookup"><span data-stu-id="9ad76-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="9ad76-120">以下是 hello 您 toohello Azure 入口網站中登入後，將您的公開憑證上傳至整合帳戶的詳細的步驟：</span><span class="sxs-lookup"><span data-stu-id="9ad76-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="9ad76-121">選取**更多服務**輸入**整合**hello 篩選搜尋 方塊中。</span><span class="sxs-lookup"><span data-stu-id="9ad76-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="9ad76-122">選取**整合帳戶**hello 結果清單中</span><span class="sxs-lookup"><span data-stu-id="9ad76-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="9ad76-123">![選取瀏覽](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="9ad76-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="9ad76-124">選取您想要 tooadd hello 憑證 hello 整合帳戶 toowhich。</span><span class="sxs-lookup"><span data-stu-id="9ad76-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![選取您想要 tooadd hello 憑證 hello 整合帳戶 toowhich](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="9ad76-126">選取 hello**憑證**磚。</span><span class="sxs-lookup"><span data-stu-id="9ad76-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="9ad76-127">![選取 hello 憑證磚](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="9ad76-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="9ad76-128">在 [hello**憑證**刀鋒視窗，開啟時，請選取 hello**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ad76-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="9ad76-129">![選取 hello [新增] 按鈕](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="9ad76-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="9ad76-130">輸入**名稱**您的憑證，以及選取 hello 憑證類型為**公用**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="9ad76-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="9ad76-131">選取 hello 資料夾圖示右邊 hello hello**憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9ad76-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="9ad76-132">當 hello 檔案選擇器開啟時，尋找並選取您想 tooupload tooyour 整合帳戶 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="9ad76-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="9ad76-133">選取 hello 憑證，然後選取**確定**hello 檔案選擇器中。</span><span class="sxs-lookup"><span data-stu-id="9ad76-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="9ad76-134">這會驗證，並上傳 hello 憑證 tooyour 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ad76-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="9ad76-135">最後上, 一步 hello**加入憑證**刀鋒視窗中，選取 hello**確定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ad76-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="9ad76-136">![選取 [確定] 按鈕，hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="9ad76-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="9ad76-137">選取 hello**憑證**磚。</span><span class="sxs-lookup"><span data-stu-id="9ad76-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="9ad76-138">您應該會看到 hello 新加入的憑證。</span><span class="sxs-lookup"><span data-stu-id="9ad76-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="9ad76-139">![請參閱 hello 新憑證](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="9ad76-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="9ad76-140">上傳私人憑證</span><span class="sxs-lookup"><span data-stu-id="9ad76-140">Upload a private certificate</span></span>

<span data-ttu-id="9ad76-141">toouse*私用憑證*B2B 功能與應用程式邏輯，您可以上傳的私用憑證 tooyour 整合帳戶採取下列步驟 hello</span><span class="sxs-lookup"><span data-stu-id="9ad76-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="9ad76-142">[上傳您私用金鑰 tooKey 保存庫](../key-vault/key-vault-get-started.md "深入了解金鑰保存庫")並提供**機碼名稱**</span><span class="sxs-lookup"><span data-stu-id="9ad76-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="9ad76-143">您必須授權金鑰保存庫的 Logic Apps tooperform 作業。</span><span class="sxs-lookup"><span data-stu-id="9ad76-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="9ad76-144">您可以使用下列 PowerShell 命令的 hello，授與存取 toohello Logic Apps 服務主體：`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="9ad76-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="9ad76-145">您已取得 hello 上一個步驟之後，請加入私人憑證 toointegration 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ad76-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="9ad76-146">下列是 hello 登入 toohello Azure 入口網站之後，將您的私用憑證上傳至整合帳戶的詳細的步驟：</span><span class="sxs-lookup"><span data-stu-id="9ad76-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="9ad76-147">選取您想 tooadd hello 憑證，並選取 hello hello 整合帳戶 toowhich**憑證**磚。</span><span class="sxs-lookup"><span data-stu-id="9ad76-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="9ad76-148">![選取 hello 憑證磚](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="9ad76-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="9ad76-149">在 [hello**憑證**刀鋒視窗，開啟時，請選取 hello**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ad76-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="9ad76-150">![選取 hello [新增] 按鈕](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="9ad76-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="9ad76-151">輸入**名稱**您的憑證，以及選取 hello 憑證類型為**私人**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="9ad76-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="9ad76-152">選取右邊 hello hello hello 資料夾圖示**憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9ad76-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="9ad76-153">當 hello 檔案選擇器開啟時，找出 hello 對應的公開憑證的 tooupload tooyour 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ad76-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="9ad76-154">加入私用憑證時務必 tooadd 對應公用憑證中的 tooshow [AS2 協議](logic-apps-enterprise-integration-as2.md)接收和傳送設定，來簽署與加密 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="9ad76-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="9ad76-155">選取 hello**資源群組**，**金鑰保存庫**，**機碼名稱**和選取 hello**確定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ad76-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="9ad76-156">![新增憑證](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="9ad76-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="9ad76-157">選取 hello**憑證**磚。</span><span class="sxs-lookup"><span data-stu-id="9ad76-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="9ad76-158">您應該會看到 hello 新加入的憑證。</span><span class="sxs-lookup"><span data-stu-id="9ad76-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="9ad76-159">![請參閱 hello 新憑證](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="9ad76-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="9ad76-160">建立 B2B 合約</span><span class="sxs-lookup"><span data-stu-id="9ad76-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="9ad76-161">深入了解金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9ad76-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "了解金鑰保存庫")  

