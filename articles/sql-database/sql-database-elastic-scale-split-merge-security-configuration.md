---
title: "aaaSplit 合併安全性設定 |Microsoft 文件"
description: "設定加密的 x409 憑證"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="eb511-103">分割合併安全性設定</span><span class="sxs-lookup"><span data-stu-id="eb511-103">Split-merge security configuration</span></span>
<span data-ttu-id="eb511-104">toouse hello 分割/合併服務，您必須正確設定安全性。</span><span class="sxs-lookup"><span data-stu-id="eb511-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="eb511-105">hello 服務是 Microsoft Azure SQL Database 的 hello 彈性延展功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="eb511-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="eb511-106">如需詳細資訊，請參閱 [Elastic Scale 分割及合併服務教學課程](sql-database-elastic-scale-configure-deploy-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="eb511-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="eb511-107">設定憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-107">Configuring certificates</span></span>
<span data-ttu-id="eb511-108">憑證有兩種設定方式。</span><span class="sxs-lookup"><span data-stu-id="eb511-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="eb511-109">tooConfigure hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="eb511-110">tooConfigure 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="eb511-111">tooobtain 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-111">tooobtain certificates</span></span>
<span data-ttu-id="eb511-112">可以取得憑證，從公用憑證授權單位 (Ca) 或 hello [Windows 憑證服務](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eb511-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="eb511-113">這些是慣用的 hello 方法 tooobtain 憑證。</span><span class="sxs-lookup"><span data-stu-id="eb511-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="eb511-114">如果這些選項都無法使用，您可以產生 **自我簽署憑證**。</span><span class="sxs-lookup"><span data-stu-id="eb511-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="eb511-115">工具 toogenerate 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="eb511-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="eb511-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="eb511-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="eb511-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="eb511-118">toorun hello 工具</span><span class="sxs-lookup"><span data-stu-id="eb511-118">toorun hello tools</span></span>
* <span data-ttu-id="eb511-119">從 Visual Studio 的開發人員命令提示字元，請參閱 [Visual Studio 命令提示字元](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="eb511-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="eb511-120">如果已安裝，請移至：</span><span class="sxs-lookup"><span data-stu-id="eb511-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="eb511-121">取得 hello 從 WDK [Windows 8.1： 下載的套件與工具](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="eb511-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="eb511-122">tooconfigure hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="eb511-123">SSL 憑證是必要的 tooencrypt hello 通訊，並驗證 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="eb511-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="eb511-124">選擇 hello 最適用的 hello 三種案例，並執行所有步驟：</span><span class="sxs-lookup"><span data-stu-id="eb511-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="eb511-125">建立新的自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="eb511-126">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="eb511-127">建立自我簽署 SSL 憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="eb511-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="eb511-128">上傳 SSL 憑證 tooCloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="eb511-129">在服務組態檔中更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="eb511-130">匯入 SSL 憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="eb511-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="eb511-131">toouse hello 憑證從現有的憑證存放區</span><span class="sxs-lookup"><span data-stu-id="eb511-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="eb511-132">從憑證存放區匯出 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="eb511-133">上傳 SSL 憑證 tooCloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="eb511-134">在服務組態檔中更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="eb511-135">toouse PFX 檔案中現有的憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="eb511-136">上傳 SSL 憑證 tooCloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="eb511-137">在服務組態檔中更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="eb511-138">tooconfigure 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-138">tooconfigure client certificates</span></span>
<span data-ttu-id="eb511-139">在訂單 tooauthenticate 要求 toohello 服務會需要用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="eb511-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="eb511-140">選擇 hello 最適用的 hello 三種案例，並執行所有步驟：</span><span class="sxs-lookup"><span data-stu-id="eb511-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="eb511-141">關閉用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="eb511-142">關閉用戶端憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="eb511-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="eb511-143">發行新的自我簽署用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="eb511-144">建立自我簽署憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="eb511-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="eb511-145">上傳的 CA 憑證 tooCloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="eb511-146">在服務組態檔中更新 CA 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="eb511-147">發行用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="eb511-148">建立用戶端憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="eb511-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="eb511-149">匯入用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="eb511-150">複製用戶端憑證指紋</span><span class="sxs-lookup"><span data-stu-id="eb511-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="eb511-151">在 hello 服務組態檔中設定允許用戶端</span><span class="sxs-lookup"><span data-stu-id="eb511-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="eb511-152">使用現有的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="eb511-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="eb511-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="eb511-154">上傳的 CA 憑證 tooCloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="eb511-155">在服務組態檔中更新 CA 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="eb511-156">複製用戶端憑證指紋</span><span class="sxs-lookup"><span data-stu-id="eb511-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="eb511-157">在 hello 服務組態檔中設定允許用戶端</span><span class="sxs-lookup"><span data-stu-id="eb511-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="eb511-158">設定用戶端憑證撤銷檢查</span><span class="sxs-lookup"><span data-stu-id="eb511-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="eb511-159">允許的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="eb511-159">Allowed IP addresses</span></span>
<span data-ttu-id="eb511-160">存取 toohello 服務端點可以是受限制的 toospecific 的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="eb511-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="eb511-161">tooconfigure 加密 hello 存放區</span><span class="sxs-lookup"><span data-stu-id="eb511-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="eb511-162">憑證是儲存在 hello 中繼資料存放區的必要的 tooencrypt hello 認證。</span><span class="sxs-lookup"><span data-stu-id="eb511-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="eb511-163">選擇 hello 最適用的 hello 三種案例，並執行所有步驟：</span><span class="sxs-lookup"><span data-stu-id="eb511-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="eb511-164">使用新的自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="eb511-165">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="eb511-166">建立自我簽署加密憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="eb511-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="eb511-167">上傳加密憑證 tooCloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="eb511-168">在服務組態檔中更新加密憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="eb511-169">使用現有的憑證從 hello 憑證存放區</span><span class="sxs-lookup"><span data-stu-id="eb511-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="eb511-170">從憑證存放區匯出加密憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="eb511-171">上傳加密憑證 tooCloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="eb511-172">在服務組態檔中更新加密憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="eb511-173">使用 PFX 檔案中現有的憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="eb511-174">上傳加密憑證 tooCloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="eb511-175">在服務組態檔中更新加密憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="eb511-176">hello 預設組態</span><span class="sxs-lookup"><span data-stu-id="eb511-176">hello default configuration</span></span>
<span data-ttu-id="eb511-177">hello 預設組態會拒絕所有存取 toohello HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="eb511-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="eb511-178">這是建議的設定，因為 hello 要求 toothese 端點可能會夾帶資料庫認證等機密資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="eb511-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="eb511-179">hello 預設組態可讓所有存取 toohello HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="eb511-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="eb511-180">這項設定可能會進一步限制。</span><span class="sxs-lookup"><span data-stu-id="eb511-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="eb511-181">變更 hello 組態</span><span class="sxs-lookup"><span data-stu-id="eb511-181">Changing hello Configuration</span></span>
<span data-ttu-id="eb511-182">hello 套用 tooand 端點的存取控制規則的群組中設定 hello  **<EndpointAcls>**  > 一節中 hello**服務組態檔**。</span><span class="sxs-lookup"><span data-stu-id="eb511-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="eb511-183">中所設定的存取控制項群組中的 hello 規則<AccessControl name="">hello 服務組態檔區段。</span><span class="sxs-lookup"><span data-stu-id="eb511-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="eb511-184">網路存取控制清單的文件說明 hello 格式。</span><span class="sxs-lookup"><span data-stu-id="eb511-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="eb511-185">例如，tooallow hello 範圍 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS 端點中的唯一 Ip，hello 規則看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="eb511-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="eb511-186">阻絕服務預防</span><span class="sxs-lookup"><span data-stu-id="eb511-186">Denial of service prevention</span></span>
<span data-ttu-id="eb511-187">有兩個不同的機制支援 toodetect 並防止阻絕服務攻擊：</span><span class="sxs-lookup"><span data-stu-id="eb511-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="eb511-188">限制每個遠端主機的並行要求數目 (預設為關閉)</span><span class="sxs-lookup"><span data-stu-id="eb511-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="eb511-189">限制每個遠端主機的存取速率 (預設為開關)</span><span class="sxs-lookup"><span data-stu-id="eb511-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="eb511-190">這些根據 hello 進一步記載於 IIS 中的動態 IP 安全性的功能。</span><span class="sxs-lookup"><span data-stu-id="eb511-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="eb511-191">當變更此設定要小心的 hello 下列因素：</span><span class="sxs-lookup"><span data-stu-id="eb511-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="eb511-192">hello 行為的 proxy 和網路位址轉譯裝置對 hello 遠端主機資訊</span><span class="sxs-lookup"><span data-stu-id="eb511-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="eb511-193">Hello web 角色中的每個要求 tooany 資源會被視為 （例如載入指令碼、 影像和其他內容）</span><span class="sxs-lookup"><span data-stu-id="eb511-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="eb511-194">限制並行存取的數量</span><span class="sxs-lookup"><span data-stu-id="eb511-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="eb511-195">設定此行為的 hello 設定如下：</span><span class="sxs-lookup"><span data-stu-id="eb511-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="eb511-196">變更 DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable 這項保護。</span><span class="sxs-lookup"><span data-stu-id="eb511-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="eb511-197">限制存取的速率</span><span class="sxs-lookup"><span data-stu-id="eb511-197">Restricting rate of access</span></span>
<span data-ttu-id="eb511-198">設定此行為的 hello 設定如下：</span><span class="sxs-lookup"><span data-stu-id="eb511-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="eb511-199">設定 hello 回應 tooa 拒絕要求</span><span class="sxs-lookup"><span data-stu-id="eb511-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="eb511-200">hello 下列設定會設定 hello 回應 tooa 已拒絕要求：</span><span class="sxs-lookup"><span data-stu-id="eb511-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="eb511-201">如需其他支援的值，請參閱在 IIS 中的動態 IP 安全性 toohello 文件。</span><span class="sxs-lookup"><span data-stu-id="eb511-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="eb511-202">設定服務憑證的作業</span><span class="sxs-lookup"><span data-stu-id="eb511-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="eb511-203">本主題僅供參考。</span><span class="sxs-lookup"><span data-stu-id="eb511-203">This topic is for reference only.</span></span> <span data-ttu-id="eb511-204">請遵循 hello 組態步驟中所述：</span><span class="sxs-lookup"><span data-stu-id="eb511-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="eb511-205">設定 hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="eb511-206">設定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="eb511-207">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-207">Create a self-signed certificate</span></span>
<span data-ttu-id="eb511-208">執行：</span><span class="sxs-lookup"><span data-stu-id="eb511-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="eb511-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="eb511-209">toocustomize:</span></span>

* <span data-ttu-id="eb511-210">-n hello 與服務 URL。</span><span class="sxs-lookup"><span data-stu-id="eb511-210">-n with hello service URL.</span></span> <span data-ttu-id="eb511-211">支援萬用字元 ("CN=*.cloudapp.net") 和替代名稱 ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net")。</span><span class="sxs-lookup"><span data-stu-id="eb511-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="eb511-212">-e hello 憑證到期日與建立強式密碼，並指定它出現提示時。</span><span class="sxs-lookup"><span data-stu-id="eb511-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="eb511-213">建立自我簽署 SSL 憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="eb511-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="eb511-214">執行：</span><span class="sxs-lookup"><span data-stu-id="eb511-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="eb511-215">輸入密碼，然後使用這些選項來匯出憑證：</span><span class="sxs-lookup"><span data-stu-id="eb511-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="eb511-216">是，匯出 hello 私密金鑰</span><span class="sxs-lookup"><span data-stu-id="eb511-216">Yes, export hello private key</span></span>
* <span data-ttu-id="eb511-217">匯出所有延伸內容</span><span class="sxs-lookup"><span data-stu-id="eb511-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="eb511-218">從憑證存放區匯出 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="eb511-219">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-219">Find certificate</span></span>
* <span data-ttu-id="eb511-220">按一下 [動作] -> [所有工作] -> [匯出...]</span><span class="sxs-lookup"><span data-stu-id="eb511-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="eb511-221">使用這些選項將憑證匯出至 .PFX 檔案：</span><span class="sxs-lookup"><span data-stu-id="eb511-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="eb511-222">是，匯出 hello 私密金鑰</span><span class="sxs-lookup"><span data-stu-id="eb511-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="eb511-223">如果可能包含 hello 憑證路徑中的所有憑證 * 匯出所有擴充的屬性</span><span class="sxs-lookup"><span data-stu-id="eb511-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="eb511-224">上傳 SSL 憑證 toocloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="eb511-225">上傳以 hello 現有或產生的憑證。以 hello SSL 金鑰組的 PFX 檔案：</span><span class="sxs-lookup"><span data-stu-id="eb511-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="eb511-226">輸入 hello 密碼保護 hello 私密金鑰資訊</span><span class="sxs-lookup"><span data-stu-id="eb511-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="eb511-227">在服務組態檔中更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="eb511-228">更新下列 hello 指紋 hello 上傳憑證 toohello 雲端服務的 hello 服務組態檔中設定的 hello hello 憑證指紋值：</span><span class="sxs-lookup"><span data-stu-id="eb511-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="eb511-229">匯入 SSL 憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="eb511-229">Import SSL certification authority</span></span>
<span data-ttu-id="eb511-230">遵循下列步驟，在所有帳戶/機器將與 hello 服務進行通訊：</span><span class="sxs-lookup"><span data-stu-id="eb511-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="eb511-231">按兩下 hello。在 Windows 檔案總管的 CER 檔案</span><span class="sxs-lookup"><span data-stu-id="eb511-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="eb511-232">在 hello 憑證對話方塊中，按一下 安裝憑證...</span><span class="sxs-lookup"><span data-stu-id="eb511-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="eb511-233">憑證匯入到信任的根憑證授權單位存放區的 hello</span><span class="sxs-lookup"><span data-stu-id="eb511-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="eb511-234">關閉用戶端憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="eb511-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="eb511-235">只有用戶端憑證式驗證支援，並停用允許公用存取 toohello 服務端點，除非其他機制中的位置 （例如 Microsoft Azure 虛擬網路）。</span><span class="sxs-lookup"><span data-stu-id="eb511-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="eb511-236">變更 hello 服務組態檔 tooturn hello 功能中的這些設定 toofalse：</span><span class="sxs-lookup"><span data-stu-id="eb511-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="eb511-237">接著，將相同的憑證指紋與 hello SSL 憑證的 hello 複製在 hello CA 憑證設定：</span><span class="sxs-lookup"><span data-stu-id="eb511-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="eb511-238">建立自我簽署憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="eb511-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="eb511-239">執行下列步驟 toocreate 為憑證授權單位的自我簽署的憑證 tooact hello:</span><span class="sxs-lookup"><span data-stu-id="eb511-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="eb511-240">toocustomize 它</span><span class="sxs-lookup"><span data-stu-id="eb511-240">toocustomize it</span></span>

* <span data-ttu-id="eb511-241">-e 與 hello 憑證到期日</span><span class="sxs-lookup"><span data-stu-id="eb511-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="eb511-242">尋找 CA 公開金鑰</span><span class="sxs-lookup"><span data-stu-id="eb511-242">Find CA public key</span></span>
<span data-ttu-id="eb511-243">所有用戶端憑證必須發出 hello 服務所信任的憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="eb511-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="eb511-244">找到 hello 公用金鑰 toohello 發出 hello 將要 toobe 的用戶端憑證的憑證授權單位使用的驗證順序 tooupload 它 toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="eb511-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="eb511-245">如果找不到 hello hello 公開金鑰檔案，請將它匯出從 hello 憑證存放區：</span><span class="sxs-lookup"><span data-stu-id="eb511-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="eb511-246">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-246">Find certificate</span></span>
  * <span data-ttu-id="eb511-247">用戶端憑證所發出的搜尋 hello 相同的憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="eb511-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="eb511-248">按兩下 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="eb511-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="eb511-249">選取在 hello 憑證 對話方塊中的 hello 憑證路徑索引標籤。</span><span class="sxs-lookup"><span data-stu-id="eb511-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="eb511-250">按兩下 hello 路徑中的 hello CA 項目。</span><span class="sxs-lookup"><span data-stu-id="eb511-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="eb511-251">記下 hello 憑證內容。</span><span class="sxs-lookup"><span data-stu-id="eb511-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="eb511-252">關閉 hello**憑證**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="eb511-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="eb511-253">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-253">Find certificate</span></span>
  * <span data-ttu-id="eb511-254">搜尋 hello 先前所述的 CA。</span><span class="sxs-lookup"><span data-stu-id="eb511-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="eb511-255">按一下 [動作] -> [所有工作] -> [匯出...]</span><span class="sxs-lookup"><span data-stu-id="eb511-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="eb511-256">使用這些選項將憑證匯出至 .CER：</span><span class="sxs-lookup"><span data-stu-id="eb511-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="eb511-257">**否，不要匯出 hello 私密金鑰**</span><span class="sxs-lookup"><span data-stu-id="eb511-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="eb511-258">如果可能的話 hello 憑證路徑中包含的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="eb511-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="eb511-259">匯出所有延伸內容。</span><span class="sxs-lookup"><span data-stu-id="eb511-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="eb511-260">上傳 CA 憑證 toocloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="eb511-261">上傳以 hello 現有或產生的憑證。Hello CA 公開金鑰的 CER 檔案。</span><span class="sxs-lookup"><span data-stu-id="eb511-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="eb511-262">在服務組態檔中更新 CA 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="eb511-263">更新下列 hello 指紋 hello 上傳憑證 toohello 雲端服務的 hello 服務組態檔中設定的 hello hello 憑證指紋值：</span><span class="sxs-lookup"><span data-stu-id="eb511-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="eb511-264">更新下列設定以 hello 相同的 hello hello 值指紋：</span><span class="sxs-lookup"><span data-stu-id="eb511-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="eb511-265">發行用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-265">Issue client certificates</span></span>
<span data-ttu-id="eb511-266">每個個別的授權的 tooaccess hello 服務應該具有用戶端憑證發出 his/hers 獨佔使用，而且應該選擇強式密碼 tooprotect his/hers 擁有其私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="eb511-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="eb511-267">必須的 hello hello 自我簽署 CA 憑證的同一部電腦所產生及儲存中執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb511-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="eb511-268">自訂：</span><span class="sxs-lookup"><span data-stu-id="eb511-268">Customizing:</span></span>

* <span data-ttu-id="eb511-269">-n toohello 將與此憑證驗證的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="eb511-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="eb511-270">-e 與 hello 憑證到期日</span><span class="sxs-lookup"><span data-stu-id="eb511-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="eb511-271">MyID.pvk 和 MyID.cer，使用這個用戶端憑證的唯一檔名</span><span class="sxs-lookup"><span data-stu-id="eb511-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="eb511-272">此命令會提示輸入密碼 toobe 建立，然後用一次。</span><span class="sxs-lookup"><span data-stu-id="eb511-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="eb511-273">請使用強式密碼。</span><span class="sxs-lookup"><span data-stu-id="eb511-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="eb511-274">建立用戶端憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="eb511-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="eb511-275">對於每個產生的用戶端憑證，請執行：</span><span class="sxs-lookup"><span data-stu-id="eb511-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="eb511-276">自訂：</span><span class="sxs-lookup"><span data-stu-id="eb511-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="eb511-277">輸入密碼，然後使用這些選項來匯出憑證：</span><span class="sxs-lookup"><span data-stu-id="eb511-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="eb511-278">是，匯出 hello 私密金鑰</span><span class="sxs-lookup"><span data-stu-id="eb511-278">Yes, export hello private key</span></span>
* <span data-ttu-id="eb511-279">匯出所有延伸內容</span><span class="sxs-lookup"><span data-stu-id="eb511-279">Export all extended properties</span></span>
* <span data-ttu-id="eb511-280">此憑證發給 hello 個別 toowhom 應該選擇 hello 匯出的密碼</span><span class="sxs-lookup"><span data-stu-id="eb511-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="eb511-281">匯入用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-281">Import client certificate</span></span>
<span data-ttu-id="eb511-282">用戶端憑證已發出的每個個別應該匯入 hello 金鑰組在 hello 機器最初將使用 toocommunicate 與 hello 服務：</span><span class="sxs-lookup"><span data-stu-id="eb511-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="eb511-283">按兩下 hello。在 Windows 檔案總管的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="eb511-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="eb511-284">憑證匯入到個人存放區至少這個選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb511-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="eb511-285">核取 [包含所有延伸內容]</span><span class="sxs-lookup"><span data-stu-id="eb511-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="eb511-286">複製用戶端憑證指紋</span><span class="sxs-lookup"><span data-stu-id="eb511-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="eb511-287">用戶端憑證已發出的每個個別必須遵循下列步驟中的 his/hers 順序 tooobtain hello 指紋憑證將會加入 toohello 服務組態檔：</span><span class="sxs-lookup"><span data-stu-id="eb511-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="eb511-288">執行 certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="eb511-288">Run certmgr.exe</span></span>
* <span data-ttu-id="eb511-289">選取 hello 個人 索引標籤</span><span class="sxs-lookup"><span data-stu-id="eb511-289">Select hello Personal tab</span></span>
* <span data-ttu-id="eb511-290">按兩下 hello toobe 用於驗證的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="eb511-291">在開啟的 hello 憑證對話方塊，選取 [hello 詳細資料] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="eb511-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="eb511-292">請確定 [顯示] 是顯示 [全部]</span><span class="sxs-lookup"><span data-stu-id="eb511-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="eb511-293">選取 hello 欄位名為 hello 清單中的憑證指紋</span><span class="sxs-lookup"><span data-stu-id="eb511-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="eb511-294">複製 hello hello 指紋值 * * 刪除不可見的 Unicode 字元前面 hello 第一個數字 * * 刪除全部為空格</span><span class="sxs-lookup"><span data-stu-id="eb511-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="eb511-295">Hello 服務組態檔中設定允許用戶端</span><span class="sxs-lookup"><span data-stu-id="eb511-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="eb511-296">更新下列 hello hello 允許存取 toohello 服務的用戶端憑證指紋的逗號分隔清單的 hello 服務組態檔中設定的 hello hello 值：</span><span class="sxs-lookup"><span data-stu-id="eb511-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="eb511-297">設定用戶端憑證撤銷檢查</span><span class="sxs-lookup"><span data-stu-id="eb511-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="eb511-298">hello 預設設定不會檢查以 hello 憑證授權單位用戶端憑證的撤銷狀態。</span><span class="sxs-lookup"><span data-stu-id="eb511-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="eb511-299">在 hello tooturn 檢查，如果 hello 發行 hello 用戶端憑證的憑證授權單位支援這類檢查，請變更 hello hello 值 hello X509RevocationMode 列舉型別中定義的其中一個具備下列設定：</span><span class="sxs-lookup"><span data-stu-id="eb511-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="eb511-300">建立自我簽署加密憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="eb511-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="eb511-301">如需加密憑證，請執行：</span><span class="sxs-lookup"><span data-stu-id="eb511-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="eb511-302">自訂：</span><span class="sxs-lookup"><span data-stu-id="eb511-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="eb511-303">輸入密碼，然後使用這些選項來匯出憑證：</span><span class="sxs-lookup"><span data-stu-id="eb511-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="eb511-304">是，匯出 hello 私密金鑰</span><span class="sxs-lookup"><span data-stu-id="eb511-304">Yes, export hello private key</span></span>
* <span data-ttu-id="eb511-305">匯出所有延伸內容</span><span class="sxs-lookup"><span data-stu-id="eb511-305">Export all extended properties</span></span>
* <span data-ttu-id="eb511-306">上傳 hello 憑證 toohello 雲端服務時，您將需要 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="eb511-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="eb511-307">從憑證存放區匯出加密憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="eb511-308">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-308">Find certificate</span></span>
* <span data-ttu-id="eb511-309">按一下 [動作] -> [所有工作] -> [匯出...]</span><span class="sxs-lookup"><span data-stu-id="eb511-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="eb511-310">使用這些選項將憑證匯出至 .PFX 檔案：</span><span class="sxs-lookup"><span data-stu-id="eb511-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="eb511-311">是，匯出 hello 私密金鑰</span><span class="sxs-lookup"><span data-stu-id="eb511-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="eb511-312">如果可能包含 hello 憑證路徑中的所有憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="eb511-313">匯出所有延伸內容</span><span class="sxs-lookup"><span data-stu-id="eb511-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="eb511-314">上傳加密憑證 toocloud 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="eb511-315">上傳以 hello 現有或產生的憑證。Hello 加密金鑰組的 PFX 檔案：</span><span class="sxs-lookup"><span data-stu-id="eb511-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="eb511-316">輸入 hello 密碼保護 hello 私密金鑰資訊</span><span class="sxs-lookup"><span data-stu-id="eb511-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="eb511-317">在服務組態檔中更新加密憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="eb511-318">更新下列 hello 指紋 hello 上傳憑證 toohello 雲端服務的 hello 服務組態檔中設定的 hello hello 憑證指紋值：</span><span class="sxs-lookup"><span data-stu-id="eb511-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="eb511-319">常見的憑證作業</span><span class="sxs-lookup"><span data-stu-id="eb511-319">Common certificate operations</span></span>
* <span data-ttu-id="eb511-320">設定 hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="eb511-321">設定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="eb511-322">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-322">Find certificate</span></span>
<span data-ttu-id="eb511-323">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="eb511-323">Follow these steps:</span></span>

1. <span data-ttu-id="eb511-324">執行 mmc.exe。</span><span class="sxs-lookup"><span data-stu-id="eb511-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="eb511-325">[檔案] -> [新增/移除嵌入式管理單元]</span><span class="sxs-lookup"><span data-stu-id="eb511-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="eb511-326">選取 [ **憑證**]。</span><span class="sxs-lookup"><span data-stu-id="eb511-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="eb511-327">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-327">Click **Add**.</span></span>
5. <span data-ttu-id="eb511-328">選擇 hello 憑證存放區位置。</span><span class="sxs-lookup"><span data-stu-id="eb511-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="eb511-329">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-329">Click **Finish**.</span></span>
7. <span data-ttu-id="eb511-330">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-330">Click **OK**.</span></span>
8. <span data-ttu-id="eb511-331">展開 [ **憑證**]。</span><span class="sxs-lookup"><span data-stu-id="eb511-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="eb511-332">展開 hello 憑證存放區節點。</span><span class="sxs-lookup"><span data-stu-id="eb511-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="eb511-333">展開 hello 憑證子節點。</span><span class="sxs-lookup"><span data-stu-id="eb511-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="eb511-334">在 [hello] 清單中選取的憑證。</span><span class="sxs-lookup"><span data-stu-id="eb511-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="eb511-335">匯出憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-335">Export certificate</span></span>
<span data-ttu-id="eb511-336">在 hello**憑證匯出精靈**:</span><span class="sxs-lookup"><span data-stu-id="eb511-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="eb511-337">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-337">Click **Next**.</span></span>
2. <span data-ttu-id="eb511-338">選取**是**，然後**匯出 hello 私密金鑰**。</span><span class="sxs-lookup"><span data-stu-id="eb511-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="eb511-339">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-339">Click **Next**.</span></span>
4. <span data-ttu-id="eb511-340">選取 hello 想要的輸出檔案格式。</span><span class="sxs-lookup"><span data-stu-id="eb511-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="eb511-341">核取 hello 所需的選項。</span><span class="sxs-lookup"><span data-stu-id="eb511-341">Check hello desired options.</span></span>
6. <span data-ttu-id="eb511-342">核取 [ **密碼**]。</span><span class="sxs-lookup"><span data-stu-id="eb511-342">Check **Password**.</span></span>
7. <span data-ttu-id="eb511-343">輸入強式密碼並加以確認。</span><span class="sxs-lookup"><span data-stu-id="eb511-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="eb511-344">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-344">Click **Next**.</span></span>
9. <span data-ttu-id="eb511-345">輸入或瀏覽 toostore hello 憑證的其中一個檔案名稱 (使用。PFX 副檔名）。</span><span class="sxs-lookup"><span data-stu-id="eb511-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="eb511-346">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-346">Click **Next**.</span></span>
11. <span data-ttu-id="eb511-347">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-347">Click **Finish**.</span></span>
12. <span data-ttu-id="eb511-348">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="eb511-349">匯入憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-349">Import certificate</span></span>
<span data-ttu-id="eb511-350">在 hello 憑證匯入精靈：</span><span class="sxs-lookup"><span data-stu-id="eb511-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="eb511-351">選取 hello 存放區位置。</span><span class="sxs-lookup"><span data-stu-id="eb511-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="eb511-352">選取**目前使用者**如果只在目前使用者 下執行的處理序將存取 hello 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="eb511-353">選取**本機**如果其他處理程序，請在此電腦將存取 hello 服務</span><span class="sxs-lookup"><span data-stu-id="eb511-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="eb511-354">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-354">Click **Next**.</span></span>
3. <span data-ttu-id="eb511-355">如果從檔案匯入，確認 hello 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="eb511-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="eb511-356">如果匯入 .PFX 檔案：</span><span class="sxs-lookup"><span data-stu-id="eb511-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="eb511-357">輸入 hello 保護 hello 私密金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="eb511-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="eb511-358">選取匯入選項</span><span class="sxs-lookup"><span data-stu-id="eb511-358">Select import options</span></span>
5. <span data-ttu-id="eb511-359">選取 hello 下列存放區中的 「 位置 」 的憑證</span><span class="sxs-lookup"><span data-stu-id="eb511-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="eb511-360">按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-360">Click **Browse**.</span></span>
7. <span data-ttu-id="eb511-361">選取 hello 所需的存放區。</span><span class="sxs-lookup"><span data-stu-id="eb511-361">Select hello desired store.</span></span>
8. <span data-ttu-id="eb511-362">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="eb511-363">如果選擇 hello 受信任的根憑證授權單位存放區，按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="eb511-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="eb511-364">在所有對話方塊視窗上，按一下 [ **確定** ]。</span><span class="sxs-lookup"><span data-stu-id="eb511-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="eb511-365">Upload certificate</span><span class="sxs-lookup"><span data-stu-id="eb511-365">Upload certificate</span></span>
<span data-ttu-id="eb511-366">在 hello [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="eb511-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="eb511-367">選取 [雲端服務] 。</span><span class="sxs-lookup"><span data-stu-id="eb511-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="eb511-368">選取 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="eb511-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="eb511-369">在 hello 上方功能表中，按一下 **憑證**。</span><span class="sxs-lookup"><span data-stu-id="eb511-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="eb511-370">Hello 下方列上，按一下**上傳**。</span><span class="sxs-lookup"><span data-stu-id="eb511-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="eb511-371">選取 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="eb511-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="eb511-372">如果它是。PFX 檔案中，輸入 hello 私用金鑰 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="eb511-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="eb511-373">完成後，複製 hello hello 清單中的新項目中的 hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="eb511-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="eb511-374">其他安全性考量</span><span class="sxs-lookup"><span data-stu-id="eb511-374">Other security considerations</span></span>
<span data-ttu-id="eb511-375">使用 hello HTTPS 端點時，這份文件中所述的 hello SSL 設定加密 hello 服務及其用戶端之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="eb511-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="eb511-376">這是因為資料庫存取權的認證重要，而且 hello 通訊中所包含的其他可能的敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="eb511-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="eb511-377">不過請注意，hello 服務持續發生內部狀態，包括認證，其內部的資料表中已經提供給中繼資料儲存在 Microsoft Azure 訂用帳戶中的 hello Microsoft Azure SQL 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="eb511-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="eb511-378">該資料庫已定義為 hello 下列服務組態檔中的設定的一部分 (。CSCFG 檔案）：</span><span class="sxs-lookup"><span data-stu-id="eb511-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="eb511-379">這個資料庫中儲存的認證會被加密。</span><span class="sxs-lookup"><span data-stu-id="eb511-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="eb511-380">不過，最佳做法，請向上 toodate 保留 web 和背景工作角色的服務部署中，而且兩者都有存取 toohello 中繼資料資料庫與 hello 憑證用於加密和解密預存認證的安全，您會看到。</span><span class="sxs-lookup"><span data-stu-id="eb511-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

