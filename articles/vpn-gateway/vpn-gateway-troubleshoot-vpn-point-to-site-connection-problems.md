---
title: "aaaTroubleshoot Azure 點對站連線問題 |Microsoft 文件"
description: "深入了解如何 tootroubleshoot 點對站連線問題。"
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="fe890-103">疑難排解：Azure 點對站連線問題</span><span class="sxs-lookup"><span data-stu-id="fe890-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="fe890-104">本文列出您可能遇到的常見點對站連線問題。</span><span class="sxs-lookup"><span data-stu-id="fe890-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="fe890-105">文中也會探討這些問題的可能原因和解決方案。</span><span class="sxs-lookup"><span data-stu-id="fe890-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="fe890-106">VPN 用戶端錯誤：找不到憑證</span><span class="sxs-lookup"><span data-stu-id="fe890-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="fe890-107">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-107">Symptom</span></span>

<span data-ttu-id="fe890-108">當您使用 hello VPN 用戶端嘗試 tooconnect tooan Azure 虛擬網路時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe890-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="fe890-109">**找不到可以使用這個可延伸的驗證通訊協定的憑證。(錯誤 798)**</span><span class="sxs-lookup"><span data-stu-id="fe890-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="fe890-110">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-110">Cause</span></span>

<span data-ttu-id="fe890-111">如果遺漏 hello 用戶端憑證，就會發生這個問題**憑證-目前的憑證**。</span><span class="sxs-lookup"><span data-stu-id="fe890-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="fe890-112">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-112">Solution</span></span>

<span data-ttu-id="fe890-113">請確定該 hello 用戶端憑證已安裝在 hello 遵循 hello 憑證存放區 (Certmgr.msc) 的位置：</span><span class="sxs-lookup"><span data-stu-id="fe890-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="fe890-114">**憑證 - 目前的使用者\個人\憑證**</span><span class="sxs-lookup"><span data-stu-id="fe890-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="fe890-115">如需如何 tooinstall hello 用戶端憑證的詳細資訊，請參閱[產生及匯出憑證，為點對站連線](vpn-gateway-certificates-point-to-site.md)。</span><span class="sxs-lookup"><span data-stu-id="fe890-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fe890-116">當您匯入 hello 用戶端憑證時，請勿選取 hello**啟用加強私密金鑰保護**選項。</span><span class="sxs-lookup"><span data-stu-id="fe890-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="fe890-117">VPN 用戶端錯誤： 收到 hello 訊息發現非預期或格式不正確</span><span class="sxs-lookup"><span data-stu-id="fe890-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="fe890-118">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-118">Symptom</span></span>

<span data-ttu-id="fe890-119">當您使用 hello VPN 用戶端嘗試 tooconnect tooan Azure 虛擬網路時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe890-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="fe890-120">**收到 hello 訊息發現非預期或格式不正確。(錯誤 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="fe890-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="fe890-121">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-121">Cause</span></span>

<span data-ttu-id="fe890-122">如果 hello 根憑證公開金鑰不會上傳到 hello Azure VPN 閘道，就會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="fe890-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="fe890-123">如果 hello 金鑰已毀損或過期時，它也會發生。</span><span class="sxs-lookup"><span data-stu-id="fe890-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="fe890-124">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-124">Solution</span></span>

<span data-ttu-id="fe890-125">tooresolve 這個問題，請檢查 hello 狀態的 hello 根的憑證在 Azure 入口網站 toosee hello 是否已被撤銷。</span><span class="sxs-lookup"><span data-stu-id="fe890-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="fe890-126">如果未被撤銷，請嘗試 toodelete hello 根憑證和 reupload。</span><span class="sxs-lookup"><span data-stu-id="fe890-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="fe890-127">如需詳細資訊，請參閱 [建立憑證](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts)。</span><span class="sxs-lookup"><span data-stu-id="fe890-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="fe890-128">VPN 用戶端錯誤：憑證鏈結已處理但被終止</span><span class="sxs-lookup"><span data-stu-id="fe890-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="fe890-129">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-129">Symptom</span></span> 

<span data-ttu-id="fe890-130">當您使用 hello VPN 用戶端嘗試 tooconnect tooan Azure 虛擬網路時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe890-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="fe890-131">**憑證鏈結已處理，但在 hello 信任提供者所未信任的根憑證終止。**</span><span class="sxs-lookup"><span data-stu-id="fe890-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="fe890-132">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-132">Solution</span></span>

1. <span data-ttu-id="fe890-133">請確定該 hello 遵循憑證位於 hello 正確的位置：</span><span class="sxs-lookup"><span data-stu-id="fe890-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="fe890-134">憑證</span><span class="sxs-lookup"><span data-stu-id="fe890-134">Certificate</span></span> | <span data-ttu-id="fe890-135">位置</span><span class="sxs-lookup"><span data-stu-id="fe890-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="fe890-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="fe890-136">AzureClient.pfx</span></span>  | <span data-ttu-id="fe890-137">目前的使用者\個人\憑證</span><span class="sxs-lookup"><span data-stu-id="fe890-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="fe890-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="fe890-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="fe890-139">目前的使用者\受信任的根憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="fe890-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="fe890-140">AzureGateway-*GUID*.cloudapp.net、AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="fe890-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="fe890-141">本機電腦\受信任的根憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="fe890-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="fe890-142">如果 hello 憑證已經在 hello 位置，請嘗試 toodelete hello 憑證，並將它們重新安裝。</span><span class="sxs-lookup"><span data-stu-id="fe890-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="fe890-143">hello  **azuregateway-*GUID*。 cloudapp.net** 憑證位於 hello VPN 用戶端組態封裝從 hello Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="fe890-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="fe890-144">您可以使用從 hello 封裝檔案封存 tooextract hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="fe890-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="fe890-145">檔案下載錯誤：未指定目標 URI</span><span class="sxs-lookup"><span data-stu-id="fe890-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="fe890-146">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-146">Symptom</span></span>

<span data-ttu-id="fe890-147">您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe890-147">You receive hello following error message:</span></span>

<span data-ttu-id="fe890-148">**檔案下載錯誤。未指定目標 URI。**</span><span class="sxs-lookup"><span data-stu-id="fe890-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="fe890-149">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-149">Cause</span></span> 

<span data-ttu-id="fe890-150">此問題的發生原因是閘道類型不正確。</span><span class="sxs-lookup"><span data-stu-id="fe890-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="fe890-151">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-151">Solution</span></span>

<span data-ttu-id="fe890-152">hello VPN 閘道類型必須是**VPN**，而且 hello VPN 類型必須是**RouteBased**。</span><span class="sxs-lookup"><span data-stu-id="fe890-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="fe890-153">VPN 用戶端錯誤：Azure VPN 自訂指令碼失敗</span><span class="sxs-lookup"><span data-stu-id="fe890-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="fe890-154">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-154">Symptom</span></span>

<span data-ttu-id="fe890-155">當您使用 hello VPN 用戶端嘗試 tooconnect tooan Azure 虛擬網路時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe890-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="fe890-156">**自訂指令碼 （您的路由表 tooupdate） 失敗。(錯誤 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="fe890-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="fe890-157">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-157">Cause</span></span>

<span data-ttu-id="fe890-158">如果您正在使用快速鍵 tooopen hello 站對點 VPN 連線，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="fe890-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="fe890-159">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-159">Solution</span></span> 

<span data-ttu-id="fe890-160">開啟 hello VPN 封裝直接而不是從 hello 捷徑開啟它。</span><span class="sxs-lookup"><span data-stu-id="fe890-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="fe890-161">無法安裝 hello VPN 用戶端</span><span class="sxs-lookup"><span data-stu-id="fe890-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="fe890-162">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-162">Cause</span></span> 

<span data-ttu-id="fe890-163">額外的憑證是必要的 tootrust hello VPN 閘道，您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fe890-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="fe890-164">hello 憑證包含在 hello VPN 用戶端組態封裝產生自 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="fe890-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="fe890-165">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-165">Solution</span></span>

<span data-ttu-id="fe890-166">擷取 hello VPN 用戶端組態封裝，並尋找 hello.cer 檔案中。</span><span class="sxs-lookup"><span data-stu-id="fe890-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="fe890-167">tooinstall hello 憑證，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fe890-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="fe890-168">開啟 mmc.exe。</span><span class="sxs-lookup"><span data-stu-id="fe890-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="fe890-169">新增 hello**憑證**嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="fe890-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="fe890-170">選取 hello**電腦**hello 本機電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="fe890-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="fe890-171">以滑鼠右鍵按一下 hello**受信任的根憑證授權單位**節點。</span><span class="sxs-lookup"><span data-stu-id="fe890-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="fe890-172">按一下**全部工作** > **匯入**，和您從 hello VPN 用戶端組態封裝擷取瀏覽 toohello.cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="fe890-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="fe890-173">Hello 電腦重新啟動。</span><span class="sxs-lookup"><span data-stu-id="fe890-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="fe890-174">嘗試使用 tooinstall hello VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="fe890-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="fe890-175">Azure 入口網站的錯誤： 無法 toosave hello VPN 閘道和 hello 資料無效</span><span class="sxs-lookup"><span data-stu-id="fe890-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="fe890-176">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-176">Symptom</span></span>

<span data-ttu-id="fe890-177">當您嘗試在 hello Azure 入口網站中的 hello VPN 閘道的 toosave hello 變更時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe890-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="fe890-178">**失敗的 toosave 虛擬網路閘道&lt;*閘道名稱*&gt;。</span><span class="sxs-lookup"><span data-stu-id="fe890-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="fe890-179">憑證 &lt;*憑證識別碼*&gt; 的資料無效。**</span><span class="sxs-lookup"><span data-stu-id="fe890-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="fe890-180">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-180">Cause</span></span> 

<span data-ttu-id="fe890-181">如果 hello 根憑證公開金鑰您上傳包含無效的字元，例如空格，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="fe890-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="fe890-182">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-182">Solution</span></span>

<span data-ttu-id="fe890-183">請確定 hello 憑證中的 hello 資料不包含無效的字元，例如分行符號 （換行）。</span><span class="sxs-lookup"><span data-stu-id="fe890-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="fe890-184">hello 整個值應該是一行很長。</span><span class="sxs-lookup"><span data-stu-id="fe890-184">hello entire value should be one long line.</span></span> <span data-ttu-id="fe890-185">下列文字的 hello 是 hello 憑證的範例：</span><span class="sxs-lookup"><span data-stu-id="fe890-185">hello following text is a sample of hello certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="fe890-186">Azure 入口網站的錯誤： 無法 toosave hello VPN 閘道，而且 hello 資源名稱無效</span><span class="sxs-lookup"><span data-stu-id="fe890-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="fe890-187">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-187">Symptom</span></span>

<span data-ttu-id="fe890-188">當您嘗試在 hello Azure 入口網站中的 hello VPN 閘道的 toosave hello 變更時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe890-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="fe890-189">**失敗的 toosave 虛擬網路閘道&lt;*閘道名稱*&gt;。</span><span class="sxs-lookup"><span data-stu-id="fe890-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="fe890-190">資源名稱&lt; *tooupload 再試一次的憑證名稱*&gt;是無效的 * *。</span><span class="sxs-lookup"><span data-stu-id="fe890-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="fe890-191">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-191">Cause</span></span>

<span data-ttu-id="fe890-192">因為 hello hello 憑證名稱包含無效的字元，例如空格，就會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="fe890-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="fe890-193">Azure 入口網站錯誤：VPN 套件檔案下載錯誤 503</span><span class="sxs-lookup"><span data-stu-id="fe890-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="fe890-194">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-194">Symptom</span></span>

<span data-ttu-id="fe890-195">當您嘗試 toodownload hello VPN 用戶端組態封裝時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe890-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="fe890-196">**無法 toodownload hello 檔案。錯誤詳細資料： 503 錯誤。hello 伺服器太忙碌。**</span><span class="sxs-lookup"><span data-stu-id="fe890-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="fe890-197">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-197">Solution</span></span>

<span data-ttu-id="fe890-198">此錯誤可能是由暫時性的網路問題所造成。</span><span class="sxs-lookup"><span data-stu-id="fe890-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="fe890-199">幾分鐘的時間之後，重試 toodownload hello VPN 封裝。</span><span class="sxs-lookup"><span data-stu-id="fe890-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="fe890-200">Azure VPN 閘道升級： 所有 P2S 用戶端將無法 tooconnect</span><span class="sxs-lookup"><span data-stu-id="fe890-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="fe890-201">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-201">Cause</span></span>

<span data-ttu-id="fe890-202">Hello 憑證是否超過 50%到它的存留期 hello 憑證變換。</span><span class="sxs-lookup"><span data-stu-id="fe890-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="fe890-203">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-203">Solution</span></span>

<span data-ttu-id="fe890-204">tooresolve 這個問題，請建立並轉散發新憑證 toohello VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="fe890-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="fe890-205">一次有太多 VPN 用戶端連線</span><span class="sxs-lookup"><span data-stu-id="fe890-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="fe890-206">每個 VPN 閘道，hello 允許的連線數目上限為 128。</span><span class="sxs-lookup"><span data-stu-id="fe890-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="fe890-207">您可以看到連接的用戶端 hello Azure 入口網站中的 hello 總數。</span><span class="sxs-lookup"><span data-stu-id="fe890-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="fe890-208">點對站 VPN 不正確地將 10.0.0.0/8 toohello 路由表的路由</span><span class="sxs-lookup"><span data-stu-id="fe890-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="fe890-209">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-209">Symptom</span></span>

<span data-ttu-id="fe890-210">當您撥 hello hello 點對站台的用戶端上的 VPN 連線時，hello VPN 用戶端應該加入朝 hello Azure 虛擬網路的路由。</span><span class="sxs-lookup"><span data-stu-id="fe890-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="fe890-211">hello IP 協助程式服務應該加入的 hello VPN 用戶端 hello 子網路的路由。</span><span class="sxs-lookup"><span data-stu-id="fe890-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="fe890-212">hello VPN 用戶端範圍所屬 10.0.0.0/8，例如 10.0.12.0/24 tooa 較小的子的網路。</span><span class="sxs-lookup"><span data-stu-id="fe890-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="fe890-213">系統會新增較高優先順序的 10.0.0.0/8 路由，而不是 10.0.12.0/24 的路由。</span><span class="sxs-lookup"><span data-stu-id="fe890-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="fe890-214">這個不正確的路由會中斷與其他內部部署網路可能屬於 tooanother 10.50.0.0/24，例如 hello 10.0.0.0/8 範圍內的子網路上沒有定義的特定路由的連線。</span><span class="sxs-lookup"><span data-stu-id="fe890-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="fe890-215">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-215">Cause</span></span>

<span data-ttu-id="fe890-216">這是針對 Windows 用戶端設計的行為。</span><span class="sxs-lookup"><span data-stu-id="fe890-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="fe890-217">當 hello 用戶端會使用 hello PPP IPCP 通訊協定時，它會從 hello 伺服器 （在此情況下 hello VPN 閘道） 取得 hello hello 通道介面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fe890-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="fe890-218">不過，由於 hello 通訊協定的限制，hello 用戶端並沒有 hello 子網路遮罩。</span><span class="sxs-lookup"><span data-stu-id="fe890-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="fe890-219">因為沒有任何其他方式 tooget hello 用戶端，它會嘗試根據 hello hello 通道介面 IP 位址類別 tooguess hello 子網路遮罩。</span><span class="sxs-lookup"><span data-stu-id="fe890-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="fe890-220">因此，您已加入根據 hello 下列靜態對應的路由：</span><span class="sxs-lookup"><span data-stu-id="fe890-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="fe890-221">如果位址所屬 tooclass A--> 套用/8</span><span class="sxs-lookup"><span data-stu-id="fe890-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="fe890-222">如果位址所屬的 tooclass B--> 套用為/16</span><span class="sxs-lookup"><span data-stu-id="fe890-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="fe890-223">如果位址所屬的 tooclass C--> 套用/24</span><span class="sxs-lookup"><span data-stu-id="fe890-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="fe890-224">VPN 用戶端無法存取網路檔案共用</span><span class="sxs-lookup"><span data-stu-id="fe890-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="fe890-225">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-225">Symptom</span></span>

<span data-ttu-id="fe890-226">hello VPN 用戶端已連線 toohello Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fe890-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="fe890-227">不過，hello 用戶端無法存取網路共用。</span><span class="sxs-lookup"><span data-stu-id="fe890-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="fe890-228">原因</span><span class="sxs-lookup"><span data-stu-id="fe890-228">Cause</span></span>

<span data-ttu-id="fe890-229">hello SMB 通訊協定用於存取檔案共用。</span><span class="sxs-lookup"><span data-stu-id="fe890-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="fe890-230">起始 hello 連線時，hello VPN 用戶端新增 hello 工作階段的認證，並發生 hello 失敗。</span><span class="sxs-lookup"><span data-stu-id="fe890-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="fe890-231">建立 hello 連接之後，hello 用戶端會強制 toouse hello 快取認證，Kerberos 驗證。</span><span class="sxs-lookup"><span data-stu-id="fe890-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="fe890-232">此程序隨即起始查詢 toohello 金鑰發佈中心 （網域控制站） tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="fe890-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="fe890-233">Hello 用戶端會從 hello 網際網路連線，因為它可能不能 tooreach hello 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="fe890-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="fe890-234">因此，hello 用戶端無法從 Kerberos tooNTLM 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="fe890-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="fe890-235">只有時間的認證是包含有效的憑證時，系統會提示該 hello 用戶端 hello （使用 SAN = UPN） 它所聯結的 hello 網域 toowhich 所發出。</span><span class="sxs-lookup"><span data-stu-id="fe890-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="fe890-236">hello 用戶端也必須是實體連線的 toohello 網域網路。</span><span class="sxs-lookup"><span data-stu-id="fe890-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="fe890-237">在此情況下，hello 用戶端會嘗試 toouse hello 憑證，並向外連 toohello 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="fe890-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="fe890-238">然後 hello 金鑰發佈中心會傳回"KDC_ERR_C_PRINCIPAL_UNKNOWN 」 錯誤。</span><span class="sxs-lookup"><span data-stu-id="fe890-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="fe890-239">hello 用戶端是強制的 toofail tooNTLM。</span><span class="sxs-lookup"><span data-stu-id="fe890-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="fe890-240">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-240">Solution</span></span>

<span data-ttu-id="fe890-241">toowork hello 問題，停用 hello 快取的網域認證，從下列登錄子機碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe890-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="fe890-242">找不到 hello 點對站 VPN 連線中 Windows hello VPN 用戶端重新安裝之後</span><span class="sxs-lookup"><span data-stu-id="fe890-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="fe890-243">徵狀</span><span class="sxs-lookup"><span data-stu-id="fe890-243">Symptom</span></span>

<span data-ttu-id="fe890-244">您移除 hello 點對站 VPN 連線，然後再重新安裝 hello VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="fe890-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="fe890-245">在此情況下，hello VPN 連線設定不成功。</span><span class="sxs-lookup"><span data-stu-id="fe890-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="fe890-246">看不到在 hello hello VPN 連線**網路連線**Windows 中的設定。</span><span class="sxs-lookup"><span data-stu-id="fe890-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="fe890-247">方案</span><span class="sxs-lookup"><span data-stu-id="fe890-247">Solution</span></span>

<span data-ttu-id="fe890-248">tooresolve hello 問題，請刪除 hello 舊 VPN 用戶端組態檔從**C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**，然後再次執行 hello VPN 用戶端安裝程式。</span><span class="sxs-lookup"><span data-stu-id="fe890-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
