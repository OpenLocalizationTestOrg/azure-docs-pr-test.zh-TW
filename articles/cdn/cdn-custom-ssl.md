---
title: "aaa\"啟用 HTTPS，在 Azure 的 CDN 自訂網域 |Microsoft 文件 」"
description: "深入了解如何在您的 Azure CDN 端點的自訂網域上 tooenable HTTPS。"
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
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="20504-103">在 Azure CDN 自訂網域上啟用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="20504-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="20504-104">Azure CDN 自訂網域的 HTTPS 支援可讓您透過 SSL 使用的資料在傳輸過程中您的網域名稱 tooimprove hello 安全性 toodeliver 安全內容。</span><span class="sxs-lookup"><span data-stu-id="20504-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="20504-105">您的自訂網域的 hello 端對端工作流程 tooenable HTTPS 已經過簡化，透過一種單鍵啟用，完成憑證管理，以及所有的任何額外的成本。</span><span class="sxs-lookup"><span data-stu-id="20504-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="20504-106">它是關鍵 tooensure hello 隱私性及您 web 應用程式的機密資料在傳輸過程中的所有資料完整性。</span><span class="sxs-lookup"><span data-stu-id="20504-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="20504-107">使用 HTTPS 通訊協定可確保您的機密資料已加密時透過傳送的嗨 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="20504-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="20504-108">它提供信任與認證，並保護您的 Web 免於攻擊。</span><span class="sxs-lookup"><span data-stu-id="20504-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="20504-109">目前，Azure CDN 支援 CDN 端點上的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="20504-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="20504-110">舉例來說，當您從 Azure CDN (https://contoso.azureedge.net) 建立端點時，預設會啟用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="20504-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="20504-111">現在透過自訂網域 HTTPS，您也可以針對自訂網域 (如 https://www.contoso.com) 啟用安全傳遞。</span><span class="sxs-lookup"><span data-stu-id="20504-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="20504-112">Hello 的 HTTPS 功能的索引鍵屬性的部分包括：</span><span class="sxs-lookup"><span data-stu-id="20504-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="20504-113">不須額外付費：取得或續約憑證不須付費，且 HTTPS 流量不另外收費。</span><span class="sxs-lookup"><span data-stu-id="20504-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="20504-114">您只需支付從 hello CDN GB 輸出。</span><span class="sxs-lookup"><span data-stu-id="20504-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="20504-115">簡單的啟用： 一個按一下佈建是可從 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="20504-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="20504-116">您也可以使用 REST API 或其他開發人員工具 tooenable hello 功能。</span><span class="sxs-lookup"><span data-stu-id="20504-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="20504-117">完整憑證管理：為您處理所有憑證採購及管理。</span><span class="sxs-lookup"><span data-stu-id="20504-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="20504-118">憑證會自動佈建及更新先前 tooexpiration。</span><span class="sxs-lookup"><span data-stu-id="20504-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="20504-119">這完全移除服務中斷，因為憑證即將到期的 hello 的風險。</span><span class="sxs-lookup"><span data-stu-id="20504-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="20504-120">先前 tooenabling HTTPS 支援，您必須已經建立[Azure CDN 自訂網域](./cdn-map-content-to-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="20504-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="20504-121">步驟 1： 啟用 hello 功能</span><span class="sxs-lookup"><span data-stu-id="20504-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="20504-122">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour Verizon 標準或進階的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="20504-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="20504-123">在 [hello] 清單中的端點，hello 端點包含您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="20504-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="20504-124">按一下您想要的 tooenable HTTPS hello 自訂網域。</span><span class="sxs-lookup"><span data-stu-id="20504-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![端點刀鋒視窗](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="20504-126">按一下**上**tooenable HTTPS 並儲存 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="20504-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![自訂 HTTPS 對話方塊](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="20504-128">步驟 2︰網域驗證</span><span class="sxs-lookup"><span data-stu-id="20504-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="20504-129">必須先完成網域驗證才能在您的自訂網域上啟用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="20504-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="20504-130">您有 6 商務天 tooapprove hello 網域。</span><span class="sxs-lookup"><span data-stu-id="20504-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="20504-131">6 個工作天內沒有核准將會取消要求。</span><span class="sxs-lookup"><span data-stu-id="20504-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="20504-132">啟用 HTTPS，在您的自訂網域之後，我們的 HTTPS 憑證提供者 DigiCert 會為您的網域，根據 WHOIS registrant 資訊，請透過 （依預設） 的電子郵件或電話連絡 hello registrant 驗證您的網域擁有權。</span><span class="sxs-lookup"><span data-stu-id="20504-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="20504-133">DigiCert 也會傳送 hello 驗證電子郵件 toohello 下方位址。</span><span class="sxs-lookup"><span data-stu-id="20504-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="20504-134">如果 WHOIS 註冊者資訊為私用，請確定您可以直接從下列其中一個地址做出核准。</span><span class="sxs-lookup"><span data-stu-id="20504-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="20504-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="20504-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="20504-136">webmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="20504-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="20504-137">hostmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="20504-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="20504-138">postmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="20504-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="20504-139">在收到 hello 電子郵件時，您有兩個驗證選項：</span><span class="sxs-lookup"><span data-stu-id="20504-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="20504-140">您可以為核准所有未來的訂單 hello 透過使用相同帳戶執行 hello 相同的根網域，例如 consoto.com。這是建議的方法，如果您計劃 tooadd 中的其他自訂網域 hello 未來 hello 相同的根網域。</span><span class="sxs-lookup"><span data-stu-id="20504-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="20504-141">您只可以核准此要求中所使用的 hello 特定主機名稱。</span><span class="sxs-lookup"><span data-stu-id="20504-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="20504-142">後續的要求將需要另外核准。</span><span class="sxs-lookup"><span data-stu-id="20504-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="20504-143">範例電子郵件：</span><span class="sxs-lookup"><span data-stu-id="20504-143">Example email:</span></span>
    
    ![自訂 HTTPS 對話方塊](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="20504-145">核准之後，DigiCert 會加入您的自訂網域名稱 toohello 的 SAN 憑證。</span><span class="sxs-lookup"><span data-stu-id="20504-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="20504-146">hello 憑證一年才有效，並會自動更新已過期。</span><span class="sxs-lookup"><span data-stu-id="20504-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="20504-147">步驟 3： 等候 hello 傳播，然後開始使用您的功能</span><span class="sxs-lookup"><span data-stu-id="20504-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="20504-148">Hello 網域名稱驗證完成後就會在 hello 自訂網域 HTTPS 功能 toobe active too6 8 小時。</span><span class="sxs-lookup"><span data-stu-id="20504-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="20504-149">Hello 程序完成之後，hello Azure 入口網站中的 hello"自訂 HTTPS"狀態會設定太 「 已啟用 」。</span><span class="sxs-lookup"><span data-stu-id="20504-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="20504-150">您現在即可使用訂網域的 HTTPS 功能。</span><span class="sxs-lookup"><span data-stu-id="20504-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="20504-151">常見問題集</span><span class="sxs-lookup"><span data-stu-id="20504-151">Frequently asked questions</span></span>

1. <span data-ttu-id="20504-152">*Hello 憑證提供者，以及使用何種類型是憑證的誰？*</span><span class="sxs-lookup"><span data-stu-id="20504-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="20504-153">我們使用 DigiCert 提供的主題別名 (SAN) 憑證。</span><span class="sxs-lookup"><span data-stu-id="20504-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="20504-154">SAN 憑證可以使用一個憑證來保護多個完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="20504-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="20504-155">*是否可以使用自己的憑證？*</span><span class="sxs-lookup"><span data-stu-id="20504-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="20504-156">目前不可以，但其在 hello 藍圖。</span><span class="sxs-lookup"><span data-stu-id="20504-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="20504-157">*如果沒有收到 hello 網域驗證電子郵件從 DigiCert 嗎？*</span><span class="sxs-lookup"><span data-stu-id="20504-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="20504-158">如果您沒有在 24 小時內收到驗證電子郵件，請連絡 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="20504-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="20504-159">*SAN 憑證的安全性是否比專用憑證來得低？*</span><span class="sxs-lookup"><span data-stu-id="20504-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="20504-160">SAN 憑證，如下所示 hello 做為專用的憑證相同的加密及安全性標準。所有核發的 SSL 憑證都使用 SHA-256 來加強伺服器安全性。</span><span class="sxs-lookup"><span data-stu-id="20504-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="20504-161">*是否可以搭配 Akamai 的 Azure CDN 使用自訂網域 HTTPS？*</span><span class="sxs-lookup"><span data-stu-id="20504-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="20504-162">此功能目前只提供給 Verizon 的 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="20504-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="20504-163">我們正在 hello 未來幾個月中支援 Azure cdn Akamai 從這項功能。</span><span class="sxs-lookup"><span data-stu-id="20504-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="20504-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20504-164">Next steps</span></span>

- <span data-ttu-id="20504-165">深入了解如何註冊 tooset[上您的 Azure CDN 端點的自訂網域](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="20504-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


