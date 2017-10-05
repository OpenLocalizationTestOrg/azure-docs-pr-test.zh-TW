---
title: "在 Azure CDN 自訂網域上啟用 HTTPS | Microsoft Docs"
description: "了解如何在具有自訂網域的 Azure CDN 端點上啟用 HTTPS。"
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="7078a-103">在 Azure CDN 自訂網域上啟用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="7078a-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="7078a-104">Azure CDN 自訂網域的 HTTPS 支援，可讓您使用自訂的網域名稱透過 SSL 傳遞安全內容，以改善資料傳送的安全性。</span><span class="sxs-lookup"><span data-stu-id="7078a-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="7078a-105">啟用自訂網域 HTTPS 的端對端工作流程已簡化為一步啟用和完整憑證管理，而且不須額外費用。</span><span class="sxs-lookup"><span data-stu-id="7078a-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="7078a-106">確保您所有 Web 應用程式在傳輸資料時的隱私和資料完整性非常重要。</span><span class="sxs-lookup"><span data-stu-id="7078a-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="7078a-107">使用 HTTPS 通訊協定可確保您的機密資料在網際網路上傳遞時已經過加密。</span><span class="sxs-lookup"><span data-stu-id="7078a-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="7078a-108">它提供信任與認證，並保護您的 Web 免於攻擊。</span><span class="sxs-lookup"><span data-stu-id="7078a-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="7078a-109">目前，Azure CDN 支援 CDN 端點上的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="7078a-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="7078a-110">舉例來說，當您從 Azure CDN (https://contoso.azureedge.net) 建立端點時，預設會啟用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="7078a-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="7078a-111">現在透過自訂網域 HTTPS，您也可以針對自訂網域 (如 https://www.contoso.com) 啟用安全傳遞。</span><span class="sxs-lookup"><span data-stu-id="7078a-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="7078a-112">HTTPS 功能的一些重要特色如下：</span><span class="sxs-lookup"><span data-stu-id="7078a-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="7078a-113">不須額外付費：取得或續約憑證不須付費，且 HTTPS 流量不另外收費。</span><span class="sxs-lookup"><span data-stu-id="7078a-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="7078a-114">您只需支付 CDN 的 GB 輸出。</span><span class="sxs-lookup"><span data-stu-id="7078a-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="7078a-115">容易啟用：從 [Azure 入口網站](https://portal.azure.com)按一下就能佈建。</span><span class="sxs-lookup"><span data-stu-id="7078a-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7078a-116">您也可以使用 REST API 或其他開發工具來啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="7078a-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="7078a-117">完整憑證管理：為您處理所有憑證採購及管理。</span><span class="sxs-lookup"><span data-stu-id="7078a-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="7078a-118">系統會自動佈建憑證並在到期前自動更新。</span><span class="sxs-lookup"><span data-stu-id="7078a-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="7078a-119">這樣可以完全避免因為憑證到期而導致的服務中斷風險。</span><span class="sxs-lookup"><span data-stu-id="7078a-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="7078a-120">啟用 HTTPS 支援之前，您必須先建立 [Azure CDN 自訂網域](./cdn-map-content-to-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="7078a-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="7078a-121">步驟 1︰啟用功能</span><span class="sxs-lookup"><span data-stu-id="7078a-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="7078a-122">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽到您的 Verizon 標準或進階 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="7078a-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="7078a-123">在端點清單中，按一下包含自訂網域的端點。</span><span class="sxs-lookup"><span data-stu-id="7078a-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="7078a-124">按一下您要啟用 HTTPS 的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="7078a-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![端點刀鋒視窗](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="7078a-126">按一下 [開啟]來啟用 HTTPS 並儲存變更。</span><span class="sxs-lookup"><span data-stu-id="7078a-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![自訂 HTTPS 對話方塊](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="7078a-128">步驟 2︰網域驗證</span><span class="sxs-lookup"><span data-stu-id="7078a-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="7078a-129">必須先完成網域驗證才能在您的自訂網域上啟用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="7078a-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="7078a-130">您有 6 個工作天可以核准網域。</span><span class="sxs-lookup"><span data-stu-id="7078a-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="7078a-131">6 個工作天內沒有核准將會取消要求。</span><span class="sxs-lookup"><span data-stu-id="7078a-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="7078a-132">在您的自訂網域上啟用 HTTPS 之後，我們的憑證提供者 DigiCert 會根據 WHOIS 註冊資訊，透過電子郵件 (預設) 或電話連絡您網域的註冊人，以驗證網域的所有權。</span><span class="sxs-lookup"><span data-stu-id="7078a-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="7078a-133">DigiCert 也會將驗證電子郵件傳送到下列地址。</span><span class="sxs-lookup"><span data-stu-id="7078a-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="7078a-134">如果 WHOIS 註冊者資訊為私用，請確定您可以直接從下列其中一個地址做出核准。</span><span class="sxs-lookup"><span data-stu-id="7078a-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="7078a-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="7078a-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="7078a-136">webmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="7078a-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="7078a-137">hostmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="7078a-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="7078a-138">postmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="7078a-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="7078a-139">收到電子郵件之後，您有兩種驗證方式選項：</span><span class="sxs-lookup"><span data-stu-id="7078a-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="7078a-140">您可以核准未來所有經相同帳戶針對同一個根網域 (如 consoto.com) 的所有訂購。</span><span class="sxs-lookup"><span data-stu-id="7078a-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="7078a-141">如果您計畫未來要針對同一個跟網域新增其他自訂網域，則建議您選擇此方法。</span><span class="sxs-lookup"><span data-stu-id="7078a-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="7078a-142">您可以只核准這次要求使用的特定主機名稱。</span><span class="sxs-lookup"><span data-stu-id="7078a-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="7078a-143">後續的要求將需要另外核准。</span><span class="sxs-lookup"><span data-stu-id="7078a-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="7078a-144">範例電子郵件：</span><span class="sxs-lookup"><span data-stu-id="7078a-144">Example email:</span></span>
    
    ![自訂 HTTPS 對話方塊](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="7078a-146">核准之後，DigiCert 會將您的自訂網域名稱加入 SAN 憑證。</span><span class="sxs-lookup"><span data-stu-id="7078a-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="7078a-147">憑證有效期限為一年，並且會在到期之前自動更新。</span><span class="sxs-lookup"><span data-stu-id="7078a-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="7078a-148">步驟 3︰ 等待傳播，然後開始使用您的功能</span><span class="sxs-lookup"><span data-stu-id="7078a-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="7078a-149">自訂網域名稱的 HTTPS功能要在網域名稱通過驗證之後 6-8 小時才會啟用。</span><span class="sxs-lookup"><span data-stu-id="7078a-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="7078a-150">程序完成之後，Azure 入口網站中的 [自訂 HTTPS] 狀態將會設為 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="7078a-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="7078a-151">您現在即可使用訂網域的 HTTPS 功能。</span><span class="sxs-lookup"><span data-stu-id="7078a-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="7078a-152">常見問題集</span><span class="sxs-lookup"><span data-stu-id="7078a-152">Frequently asked questions</span></span>

1. <span data-ttu-id="7078a-153">*憑證提供者是誰？使用的是哪一種憑證？*</span><span class="sxs-lookup"><span data-stu-id="7078a-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="7078a-154">我們使用 DigiCert 提供的主題別名 (SAN) 憑證。</span><span class="sxs-lookup"><span data-stu-id="7078a-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="7078a-155">SAN 憑證可以使用一個憑證來保護多個完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="7078a-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="7078a-156">*是否可以使用自己的憑證？*</span><span class="sxs-lookup"><span data-stu-id="7078a-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="7078a-157">目前不行，但此功能已列在藍圖中。</span><span class="sxs-lookup"><span data-stu-id="7078a-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="7078a-158">*如果沒有收到 DigiCert 的驗證電子郵件該怎麼辦？*</span><span class="sxs-lookup"><span data-stu-id="7078a-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="7078a-159">如果您沒有在 24 小時內收到驗證電子郵件，請連絡 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="7078a-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="7078a-160">*SAN 憑證的安全性是否比專用憑證來得低？*</span><span class="sxs-lookup"><span data-stu-id="7078a-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="7078a-161">SAN 憑證遵循和專用憑證相同的加密與安全性標準。</span><span class="sxs-lookup"><span data-stu-id="7078a-161">A SAN cert follows the same encryption and security standards as a dedicated cert.</span></span> <span data-ttu-id="7078a-162">所有核發的 SSL 憑證都使用 SHA-256 來加強伺服器安全性。</span><span class="sxs-lookup"><span data-stu-id="7078a-162">All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="7078a-163">*是否可以搭配 Akamai 的 Azure CDN 使用自訂網域 HTTPS？*</span><span class="sxs-lookup"><span data-stu-id="7078a-163">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="7078a-164">此功能目前只提供給 Verizon 的 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="7078a-164">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="7078a-165">我們正在進行相關工作，讓此功能在未來的幾個月內支援 Akamai 的 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="7078a-165">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7078a-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7078a-166">Next steps</span></span>

- <span data-ttu-id="7078a-167">了解如何[在 Azure CDN 端點上設定自訂網域](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="7078a-167">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


