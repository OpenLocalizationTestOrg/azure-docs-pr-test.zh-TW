---
title: "<span data-ttu-id=\"dd91b-101\">使用憑證搭配企業整合套件 | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"dd91b-101\">Using certificates with Enterprise Integration Pack | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"dd91b-102\">了解如何使用憑證搭配企業整合套件 | Azure Logic Apps</span><span class=\"sxs-lookup\"><span data-stu-id=\"dd91b-102\">Learn how to use certificates with the Enterprise Integration Pack | Azure Logic Apps</span></span>"
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
ms.openlocfilehash: 0570aab14283b38f9efcc50636f0c0c1c8e3ed13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="dd91b-103">了解憑證與企業整合套件</span><span class="sxs-lookup"><span data-stu-id="dd91b-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="dd91b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="dd91b-104">Overview</span></span>
<span data-ttu-id="dd91b-105">企業整合使用憑證來保護 B2B 通訊的安全。</span><span class="sxs-lookup"><span data-stu-id="dd91b-105">Enterprise integration uses certificates to secure B2B communications.</span></span> <span data-ttu-id="dd91b-106">您可以在企業整合應用程式中使用兩種憑證類型：</span><span class="sxs-lookup"><span data-stu-id="dd91b-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="dd91b-107">公開憑證，必須先向憑證授權單位 (CA) 購買。</span><span class="sxs-lookup"><span data-stu-id="dd91b-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="dd91b-108">私人憑證，您可以自行核發。</span><span class="sxs-lookup"><span data-stu-id="dd91b-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="dd91b-109">這些憑證有時也稱為自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="dd91b-109">These certificates are sometimes referred to as self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="dd91b-110">什麼是憑證？</span><span class="sxs-lookup"><span data-stu-id="dd91b-110">What are certificates?</span></span>
<span data-ttu-id="dd91b-111">憑證是數位文件，可驗證電子通訊參與者的身分識別，同時還能保護電子通訊的安全。</span><span class="sxs-lookup"><span data-stu-id="dd91b-111">Certificates are digital documents that verify the identity of the participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="dd91b-112">為什麼要使用憑證？</span><span class="sxs-lookup"><span data-stu-id="dd91b-112">Why use certificates?</span></span>
<span data-ttu-id="dd91b-113">B2B 通訊有時必須確保機密。</span><span class="sxs-lookup"><span data-stu-id="dd91b-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="dd91b-114">企業整合透過下列兩種方式，使用憑證來保護這些通訊的安全：</span><span class="sxs-lookup"><span data-stu-id="dd91b-114">Enterprise integration uses certificates to secure these communications in two ways:</span></span>

* <span data-ttu-id="dd91b-115">將訊息的內容加密</span><span class="sxs-lookup"><span data-stu-id="dd91b-115">By encrypting the contents of messages</span></span>
* <span data-ttu-id="dd91b-116">以數位方式簽署訊息</span><span class="sxs-lookup"><span data-stu-id="dd91b-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="dd91b-117">上傳公開憑證</span><span class="sxs-lookup"><span data-stu-id="dd91b-117">Upload a public certificate</span></span>

<span data-ttu-id="dd91b-118">若要在具備 B2B 功能的 Logic Apps 中使用「公開憑證」  ，您必須先將憑證上傳到整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd91b-118">To use a *public certificate* in your logic apps with B2B capabilities, you first need to upload the certificate into your integration account.</span></span>  

<span data-ttu-id="dd91b-119">上傳憑證之後，當您在自己建立的 [合約](logic-apps-enterprise-integration-agreements.md) 中定義 B2B 訊息的屬性時，就能使用它來保護這些訊息的安全。</span><span class="sxs-lookup"><span data-stu-id="dd91b-119">After you upload a certificate, it's available to help you secure your B2B messages when you define their properties in the [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="dd91b-120">以下是您登入 Azure 入口網站後，將公開憑證上傳到整合帳戶的詳細步驟：</span><span class="sxs-lookup"><span data-stu-id="dd91b-120">Here are the detailed steps for uploading your public certificates into your integration account after you sign in to the Azure portal:</span></span>

1. <span data-ttu-id="dd91b-121">選取 [更多服務]，然後在篩選搜尋方塊中輸入**整合**。</span><span class="sxs-lookup"><span data-stu-id="dd91b-121">Select **More services** and enter **integration** in the filter search box.</span></span> <span data-ttu-id="dd91b-122">從結果清單中選取 [整合帳戶]</span><span class="sxs-lookup"><span data-stu-id="dd91b-122">Select **Integration Accounts** from the results list</span></span>     
<span data-ttu-id="dd91b-123">![選取瀏覽](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="dd91b-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="dd91b-124">選取要將憑證新增到的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd91b-124">Select the integration account to which you want to add the certificate.</span></span>  
![選取要將憑證新增到的整合帳戶](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="dd91b-126">選取 [憑證]  圖格。</span><span class="sxs-lookup"><span data-stu-id="dd91b-126">Select the **Certificates** tile.</span></span>  
<span data-ttu-id="dd91b-127">![選取憑證圖格](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="dd91b-127">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="dd91b-128">在開啟的 [憑證] 刀鋒視窗中選取 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd91b-128">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="dd91b-129">![選取新增按鈕](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="dd91b-129">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="dd91b-130">輸入憑證的**名稱**，然後從下拉式清單中選取 [公用] 憑證類型。</span><span class="sxs-lookup"><span data-stu-id="dd91b-130">Enter a **Name** for your certificate, and then select the certificate type as **public** from the dropdown.</span></span>  
6. <span data-ttu-id="dd91b-131">選取 [憑證] 文字方塊右邊的資料夾圖示。</span><span class="sxs-lookup"><span data-stu-id="dd91b-131">Select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="dd91b-132">當檔案選擇器開啟時，尋找並選取您要上傳到整合帳戶的憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="dd91b-132">When the file picker opens, find and select the certificate file that you want to upload to your integration account.</span></span>
7. <span data-ttu-id="dd91b-133">選取憑證，然後在檔案選擇器中選取 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="dd91b-133">Select the certificate, and then select **OK** in the file picker.</span></span> <span data-ttu-id="dd91b-134">這會驗證憑證並上傳到您的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd91b-134">This validates and uploads the certificate to your integration account.</span></span>
8. <span data-ttu-id="dd91b-135">最後，返回 [新增憑證] 刀鋒視窗，然後選取 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd91b-135">Finally, back on the **Add certificate** blade, select the **OK** button.</span></span>  
<span data-ttu-id="dd91b-136">![選取確定按鈕](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="dd91b-136">![Select the OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="dd91b-137">選取 [憑證]  圖格。</span><span class="sxs-lookup"><span data-stu-id="dd91b-137">Select the **Certificates** tile.</span></span> <span data-ttu-id="dd91b-138">您應該會看到新增的憑證。</span><span class="sxs-lookup"><span data-stu-id="dd91b-138">You should see the newly added certificate.</span></span>  
<span data-ttu-id="dd91b-139">![查看新憑證](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="dd91b-139">![See the new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="dd91b-140">上傳私人憑證</span><span class="sxs-lookup"><span data-stu-id="dd91b-140">Upload a private certificate</span></span>

<span data-ttu-id="dd91b-141">若要在具有 B2B 功能的邏輯應用程式中使用「私人憑證」，您可以執行下列步驟以將私人憑證上傳到您的整合帳戶</span><span class="sxs-lookup"><span data-stu-id="dd91b-141">To use a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate to your integration account by taking the following steps</span></span>

1. <span data-ttu-id="dd91b-142">[將您的私人金鑰上傳到 Key Vault](../key-vault/key-vault-get-started.md "了解 Key Vault") 並提供**金鑰名稱**</span><span class="sxs-lookup"><span data-stu-id="dd91b-142">[Upload your private key to Key Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="dd91b-143">您必須授權 Logic Apps 以便對 Key Vault 執行作業。</span><span class="sxs-lookup"><span data-stu-id="dd91b-143">You must authorize Logic Apps to perform operations on Key Vault.</span></span> <span data-ttu-id="dd91b-144">您可以使用下列 PowerShell 命令授與 Logic Apps 服務主體的存取權︰ `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="dd91b-144">You can grant access to the Logic Apps service principal by using the following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="dd91b-145">在您執行上一個步驟之後，請將私人憑證新增到整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd91b-145">After you've taken the previous step, add a private certificate to integration account.</span></span>

<span data-ttu-id="dd91b-146">以下是您登入 Azure 入口網站後，將私人憑證上傳到整合帳戶的詳細步驟：</span><span class="sxs-lookup"><span data-stu-id="dd91b-146">Following are the detailed steps for uploading your private certificates into your integration account after you sign in to the Azure portal:</span></span>  
 
1. <span data-ttu-id="dd91b-147">選取要將憑證新增到其中的整合帳戶，然後選取 [憑證] 圖格。</span><span class="sxs-lookup"><span data-stu-id="dd91b-147">Select the integration account to which you want to add the certificate and select the **Certificates** tile.</span></span>  
<span data-ttu-id="dd91b-148">![選取憑證圖格](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="dd91b-148">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="dd91b-149">在開啟的 [憑證] 刀鋒視窗中選取 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd91b-149">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="dd91b-150">![選取新增按鈕](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="dd91b-150">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="dd91b-151">輸入憑證的**名稱**，然後從下拉式清單中選取 [私人] 憑證類型。</span><span class="sxs-lookup"><span data-stu-id="dd91b-151">Enter a **Name** for your certificate, and select the certificate type as **private** from the dropdown.</span></span>   
4. <span data-ttu-id="dd91b-152">選取 [憑證] 文字方塊右邊的資料夾圖示。</span><span class="sxs-lookup"><span data-stu-id="dd91b-152">select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="dd91b-153">當檔案選擇器開啟時，尋找您要上傳到整合帳戶的對應公開憑證。</span><span class="sxs-lookup"><span data-stu-id="dd91b-153">When the file picker opens, find the corresponding public certificate that you want to upload to your integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="dd91b-154">新增私人憑證時，請務必新增要在 [AS2 合約](logic-apps-enterprise-integration-as2.md)接收和傳送設定中顯示的對應公開憑證，以用來簽署與加密訊息。</span><span class="sxs-lookup"><span data-stu-id="dd91b-154">While adding a private certificate it is important to add corresponding public certificate to show in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting the messages.</span></span>
   > 
   >   

5. <span data-ttu-id="dd91b-155">選取 [資源群組]、[Key Vault]、[金鑰名稱]，然後選取 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd91b-155">Select the **Resource Group**, **Key Vault**, **Key Name** and select the **OK** button.</span></span>  
<span data-ttu-id="dd91b-156">![新增憑證](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="dd91b-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="dd91b-157">選取 [憑證]  圖格。</span><span class="sxs-lookup"><span data-stu-id="dd91b-157">Select the **Certificates** tile.</span></span> <span data-ttu-id="dd91b-158">您應該會看到新增的憑證。</span><span class="sxs-lookup"><span data-stu-id="dd91b-158">You should see the newly added certificate.</span></span>
<span data-ttu-id="dd91b-159">![查看新憑證](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="dd91b-159">![See the new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="dd91b-160">建立 B2B 合約</span><span class="sxs-lookup"><span data-stu-id="dd91b-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="dd91b-161">深入了解金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="dd91b-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "了解金鑰保存庫")  

