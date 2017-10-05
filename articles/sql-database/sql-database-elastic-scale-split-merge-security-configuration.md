---
title: "分割合併安全性設定 | Microsoft Docs"
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
ms.openlocfilehash: 7e6ccf51a4b75eef16a7df5c1a1018954af8e5dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="f3310-103">分割合併安全性設定</span><span class="sxs-lookup"><span data-stu-id="f3310-103">Split-merge security configuration</span></span>
<span data-ttu-id="f3310-104">若要使用 Split/Merge 服務，您必須正確地設定安全性。</span><span class="sxs-lookup"><span data-stu-id="f3310-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="f3310-105">此服務是 Microsoft Azure SQL Database 的 Elastic Scale 功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="f3310-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="f3310-106">如需詳細資訊，請參閱 [Elastic Scale 分割及合併服務教學課程](sql-database-elastic-scale-configure-deploy-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="f3310-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="f3310-107">設定憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-107">Configuring certificates</span></span>
<span data-ttu-id="f3310-108">憑證有兩種設定方式。</span><span class="sxs-lookup"><span data-stu-id="f3310-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="f3310-109">設定 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="f3310-110">設定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="f3310-111">取得憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-111">To obtain certificates</span></span>
<span data-ttu-id="f3310-112">您可以從公用憑證授權單位 (CA) 或從 [Windows 憑證服務](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx)取得憑證。</span><span class="sxs-lookup"><span data-stu-id="f3310-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="f3310-113">這些是取得憑證的慣用方法。</span><span class="sxs-lookup"><span data-stu-id="f3310-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="f3310-114">如果這些選項都無法使用，您可以產生 **自我簽署憑證**。</span><span class="sxs-lookup"><span data-stu-id="f3310-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="f3310-115">產生憑證的工具</span><span class="sxs-lookup"><span data-stu-id="f3310-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="f3310-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="f3310-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="f3310-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="f3310-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="f3310-118">執行工具</span><span class="sxs-lookup"><span data-stu-id="f3310-118">To run the tools</span></span>
* <span data-ttu-id="f3310-119">從 Visual Studio 的開發人員命令提示字元，請參閱 [Visual Studio 命令提示字元](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="f3310-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="f3310-120">如果已安裝，請移至：</span><span class="sxs-lookup"><span data-stu-id="f3310-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="f3310-121">從 [Windows 8.1：下載套件與工具](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="f3310-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="f3310-122">設定 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-122">To configure the SSL certificate</span></span>
<span data-ttu-id="f3310-123">需要 SSL 憑證，才能將通訊加密和驗證伺服器。</span><span class="sxs-lookup"><span data-stu-id="f3310-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="f3310-124">從以下三種案例中選擇最適用的案例，然後執行其所有步驟：</span><span class="sxs-lookup"><span data-stu-id="f3310-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="f3310-125">建立新的自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="f3310-126">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="f3310-127">建立自我簽署 SSL 憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="f3310-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="f3310-128">將 SSL 憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="f3310-129">在服務組態檔中更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="f3310-130">匯入 SSL 憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="f3310-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="f3310-131">如何從憑證存放區使用現有的憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="f3310-132">從憑證存放區匯出 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="f3310-133">將 SSL 憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="f3310-134">在服務組態檔中更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="f3310-135">如何使用 PFX 檔案中現有的憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="f3310-136">將 SSL 憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="f3310-137">在服務組態檔中更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="f3310-138">設定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-138">To configure client certificates</span></span>
<span data-ttu-id="f3310-139">需要用戶端憑證，才能驗證服務的要求。</span><span class="sxs-lookup"><span data-stu-id="f3310-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="f3310-140">從以下三種案例中選擇最適用的案例，然後執行其所有步驟：</span><span class="sxs-lookup"><span data-stu-id="f3310-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="f3310-141">關閉用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="f3310-142">關閉用戶端憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="f3310-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="f3310-143">發行新的自我簽署用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="f3310-144">建立自我簽署憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="f3310-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="f3310-145">將 CA 憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="f3310-146">在服務組態檔中更新 CA 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="f3310-147">發行用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="f3310-148">建立用戶端憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="f3310-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="f3310-149">匯入用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="f3310-150">複製用戶端憑證指紋</span><span class="sxs-lookup"><span data-stu-id="f3310-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="f3310-151">在服務組態檔中設定允許的用戶端</span><span class="sxs-lookup"><span data-stu-id="f3310-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="f3310-152">使用現有的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="f3310-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="f3310-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="f3310-154">將 CA 憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="f3310-155">在服務組態檔中更新 CA 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="f3310-156">複製用戶端憑證指紋</span><span class="sxs-lookup"><span data-stu-id="f3310-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="f3310-157">在服務組態檔中設定允許的用戶端</span><span class="sxs-lookup"><span data-stu-id="f3310-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="f3310-158">設定用戶端憑證撤銷檢查</span><span class="sxs-lookup"><span data-stu-id="f3310-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="f3310-159">允許的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f3310-159">Allowed IP addresses</span></span>
<span data-ttu-id="f3310-160">您可將服務端點的存取限制為特定的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="f3310-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="f3310-161">設定存放區加密</span><span class="sxs-lookup"><span data-stu-id="f3310-161">To configure encryption for the store</span></span>
<span data-ttu-id="f3310-162">需要憑證來加密儲存在中繼資料存放區中的認證。</span><span class="sxs-lookup"><span data-stu-id="f3310-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="f3310-163">從以下三種案例中選擇最適用的案例，然後執行其所有步驟：</span><span class="sxs-lookup"><span data-stu-id="f3310-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="f3310-164">使用新的自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="f3310-165">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="f3310-166">建立自我簽署加密憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="f3310-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="f3310-167">將加密憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="f3310-168">在服務組態檔中更新加密憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="f3310-169">從憑證存放區使用現有的憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="f3310-170">從憑證存放區匯出加密憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="f3310-171">將加密憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="f3310-172">在服務組態檔中更新加密憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="f3310-173">使用 PFX 檔案中現有的憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="f3310-174">將加密憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="f3310-175">在服務組態檔中更新加密憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="f3310-176">預設組態</span><span class="sxs-lookup"><span data-stu-id="f3310-176">The default configuration</span></span>
<span data-ttu-id="f3310-177">預設組態會拒絕對 HTTP 端點的所有存取。</span><span class="sxs-lookup"><span data-stu-id="f3310-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="f3310-178">這是建議設定，因為對這些端點的要求可能帶有機密資訊 (如資料庫認證)。</span><span class="sxs-lookup"><span data-stu-id="f3310-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="f3310-179">預設組態會允許對 HTTPS 端點的所有存取。</span><span class="sxs-lookup"><span data-stu-id="f3310-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="f3310-180">這項設定可能會進一步限制。</span><span class="sxs-lookup"><span data-stu-id="f3310-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="f3310-181">變更組態</span><span class="sxs-lookup"><span data-stu-id="f3310-181">Changing the Configuration</span></span>
<span data-ttu-id="f3310-182">套用至端點的存取控制規則群組是在**服務組態檔**的 **<EndpointAcls>** 區段中設定。</span><span class="sxs-lookup"><span data-stu-id="f3310-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="f3310-183">存取控制群組中的規則會設定於服務組態檔的 <AccessControl name=""> 區段中。</span><span class="sxs-lookup"><span data-stu-id="f3310-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="f3310-184">網路存取控制清單文件會說明其格式。</span><span class="sxs-lookup"><span data-stu-id="f3310-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="f3310-185">例如，若只要允許範圍 100.100.0.0 至 100.100.255.255 中的 IP 存取 HTTPS 端點，則規則看起來如下：</span><span class="sxs-lookup"><span data-stu-id="f3310-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="f3310-186">阻絕服務預防</span><span class="sxs-lookup"><span data-stu-id="f3310-186">Denial of service prevention</span></span>
<span data-ttu-id="f3310-187">支援兩個不同的機制來偵測並防止阻斷服務攻擊：</span><span class="sxs-lookup"><span data-stu-id="f3310-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="f3310-188">限制每個遠端主機的並行要求數目 (預設為關閉)</span><span class="sxs-lookup"><span data-stu-id="f3310-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="f3310-189">限制每個遠端主機的存取速率 (預設為開關)</span><span class="sxs-lookup"><span data-stu-id="f3310-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="f3310-190">這些是根據「IIS 中的動態 IP 安全性」所進一步記載的功能。</span><span class="sxs-lookup"><span data-stu-id="f3310-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="f3310-191">變更此設定時，請注意下列因素：</span><span class="sxs-lookup"><span data-stu-id="f3310-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="f3310-192">Proxy 和網路位址轉譯裝置對遠端主機資訊的行為</span><span class="sxs-lookup"><span data-stu-id="f3310-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="f3310-193">考量每個 Web 角色中對任何資源的要求 (例如載入指令碼、影像等)</span><span class="sxs-lookup"><span data-stu-id="f3310-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="f3310-194">限制並行存取的數量</span><span class="sxs-lookup"><span data-stu-id="f3310-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="f3310-195">設定此行為的設定包括：</span><span class="sxs-lookup"><span data-stu-id="f3310-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="f3310-196">將 DynamicIpRestrictionDenyByConcurrentRequests 變更為 true，以啟用這項保護。</span><span class="sxs-lookup"><span data-stu-id="f3310-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="f3310-197">限制存取的速率</span><span class="sxs-lookup"><span data-stu-id="f3310-197">Restricting rate of access</span></span>
<span data-ttu-id="f3310-198">設定此行為的設定包括：</span><span class="sxs-lookup"><span data-stu-id="f3310-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="f3310-199">設定拒絕要求的回應</span><span class="sxs-lookup"><span data-stu-id="f3310-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="f3310-200">下列設定會設定拒絕要求的回應：</span><span class="sxs-lookup"><span data-stu-id="f3310-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="f3310-201">關於其他支援的值，請參閱「IIS 中的動態 IP 安全性」文件。</span><span class="sxs-lookup"><span data-stu-id="f3310-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="f3310-202">設定服務憑證的作業</span><span class="sxs-lookup"><span data-stu-id="f3310-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="f3310-203">本主題僅供參考。</span><span class="sxs-lookup"><span data-stu-id="f3310-203">This topic is for reference only.</span></span> <span data-ttu-id="f3310-204">請遵循以下所述的設定步驟：</span><span class="sxs-lookup"><span data-stu-id="f3310-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="f3310-205">設定 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="f3310-206">設定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="f3310-207">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-207">Create a self-signed certificate</span></span>
<span data-ttu-id="f3310-208">執行：</span><span class="sxs-lookup"><span data-stu-id="f3310-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="f3310-209">自訂：</span><span class="sxs-lookup"><span data-stu-id="f3310-209">To customize:</span></span>

* <span data-ttu-id="f3310-210">-n 與服務 URL。</span><span class="sxs-lookup"><span data-stu-id="f3310-210">-n with the service URL.</span></span> <span data-ttu-id="f3310-211">支援萬用字元 ("CN=*.cloudapp.net") 和替代名稱 ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net")。</span><span class="sxs-lookup"><span data-stu-id="f3310-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="f3310-212">-e 與憑證到期日 建立強式密碼，並於提示時指定它。</span><span class="sxs-lookup"><span data-stu-id="f3310-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="f3310-213">建立自我簽署 SSL 憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="f3310-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="f3310-214">執行：</span><span class="sxs-lookup"><span data-stu-id="f3310-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="f3310-215">輸入密碼，然後使用這些選項來匯出憑證：</span><span class="sxs-lookup"><span data-stu-id="f3310-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="f3310-216">是，匯出私密金鑰</span><span class="sxs-lookup"><span data-stu-id="f3310-216">Yes, export the private key</span></span>
* <span data-ttu-id="f3310-217">匯出所有延伸內容</span><span class="sxs-lookup"><span data-stu-id="f3310-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="f3310-218">從憑證存放區匯出 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="f3310-219">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-219">Find certificate</span></span>
* <span data-ttu-id="f3310-220">按一下 [動作] -> [所有工作] -> [匯出...]</span><span class="sxs-lookup"><span data-stu-id="f3310-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="f3310-221">使用這些選項將憑證匯出至 .PFX 檔案：</span><span class="sxs-lookup"><span data-stu-id="f3310-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="f3310-222">是，匯出私密金鑰</span><span class="sxs-lookup"><span data-stu-id="f3310-222">Yes, export the private key</span></span>
  * <span data-ttu-id="f3310-223">如果可能的話，包含憑證路徑中的所有憑證 *匯出所有延伸內容</span><span class="sxs-lookup"><span data-stu-id="f3310-223">Include all certificates in the certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="f3310-224">將 SSL 憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="f3310-225">連同現有或產生的 .PFX 檔案及 SSL 金鑰組一起上傳憑證：</span><span class="sxs-lookup"><span data-stu-id="f3310-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="f3310-226">輸入密碼以保護私密金鑰資訊</span><span class="sxs-lookup"><span data-stu-id="f3310-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="f3310-227">在服務組態檔中更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="f3310-228">使用上傳至雲端服務的憑證指紋，在服務組態檔中更新下列設定的指紋值：</span><span class="sxs-lookup"><span data-stu-id="f3310-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="f3310-229">匯入 SSL 憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="f3310-229">Import SSL certification authority</span></span>
<span data-ttu-id="f3310-230">在所有會與服務通訊的帳戶/電腦中，遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f3310-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="f3310-231">在 Windows 檔案總管中按兩下 .CER 檔案</span><span class="sxs-lookup"><span data-stu-id="f3310-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="f3310-232">在 [憑證] 對話方塊中，按一下 [安裝憑證...]</span><span class="sxs-lookup"><span data-stu-id="f3310-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="f3310-233">將憑證匯入信任的根憑證授權單位存放區</span><span class="sxs-lookup"><span data-stu-id="f3310-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="f3310-234">關閉用戶端憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="f3310-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="f3310-235">僅支援用戶端憑證式驗證，停用它將允許公開存取服務端點，除非有其他機制存在 (例如 Microsoft Azure 虛擬網路)。</span><span class="sxs-lookup"><span data-stu-id="f3310-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="f3310-236">在服務組態檔中將這些設定變更為 false 以關閉功能：</span><span class="sxs-lookup"><span data-stu-id="f3310-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="f3310-237">接著，在 CA 憑證設定中複製與 SSL 憑證相同的憑證指紋：</span><span class="sxs-lookup"><span data-stu-id="f3310-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="f3310-238">建立自我簽署憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="f3310-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="f3310-239">執行下列步驟來建立自我簽署憑證，以做為憑證授權單位：</span><span class="sxs-lookup"><span data-stu-id="f3310-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="f3310-240">自訂</span><span class="sxs-lookup"><span data-stu-id="f3310-240">To customize it</span></span>

* <span data-ttu-id="f3310-241">-e 與憑證到期日</span><span class="sxs-lookup"><span data-stu-id="f3310-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="f3310-242">尋找 CA 公開金鑰</span><span class="sxs-lookup"><span data-stu-id="f3310-242">Find CA public key</span></span>
<span data-ttu-id="f3310-243">所有用戶端憑證必須已由服務信任的憑證授權單位發出。</span><span class="sxs-lookup"><span data-stu-id="f3310-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="f3310-244">尋找發出用戶端憑證的憑證授權單位的公開金鑰，這些用戶端憑證將用於驗證，以便將公開金鑰上載至雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f3310-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="f3310-245">如果無法取得含有公用金鑰的檔案，請從憑證存放區匯出：</span><span class="sxs-lookup"><span data-stu-id="f3310-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="f3310-246">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-246">Find certificate</span></span>
  * <span data-ttu-id="f3310-247">搜尋相同憑證授權單位所發出的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="f3310-248">按兩下憑證。</span><span class="sxs-lookup"><span data-stu-id="f3310-248">Double-click the certificate.</span></span>
* <span data-ttu-id="f3310-249">在 [憑證] 對話方塊中選取 [憑證路徑] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f3310-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="f3310-250">按兩下路徑中的 CA 項目。</span><span class="sxs-lookup"><span data-stu-id="f3310-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="f3310-251">記下憑證屬性。</span><span class="sxs-lookup"><span data-stu-id="f3310-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="f3310-252">關閉 [ **憑證** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f3310-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="f3310-253">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-253">Find certificate</span></span>
  * <span data-ttu-id="f3310-254">搜尋剛才記下的 CA。</span><span class="sxs-lookup"><span data-stu-id="f3310-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="f3310-255">按一下 [動作] -> [所有工作] -> [匯出...]</span><span class="sxs-lookup"><span data-stu-id="f3310-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="f3310-256">使用這些選項將憑證匯出至 .CER：</span><span class="sxs-lookup"><span data-stu-id="f3310-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="f3310-257">**否，不要匯出私密金鑰**</span><span class="sxs-lookup"><span data-stu-id="f3310-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="f3310-258">如果可能的話，包含憑證路徑中的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="f3310-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="f3310-259">匯出所有延伸內容。</span><span class="sxs-lookup"><span data-stu-id="f3310-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="f3310-260">將 CA 憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="f3310-261">連同現有或產生的 .CER 檔案及 SSL 公開金鑰一起上傳憑證。</span><span class="sxs-lookup"><span data-stu-id="f3310-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="f3310-262">在服務組態檔中更新 CA 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="f3310-263">使用上傳至雲端服務的憑證指紋，在服務組態檔中更新下列設定的指紋值：</span><span class="sxs-lookup"><span data-stu-id="f3310-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="f3310-264">使用相同的憑證指紋更新下列設定的值：</span><span class="sxs-lookup"><span data-stu-id="f3310-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="f3310-265">發行用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-265">Issue client certificates</span></span>
<span data-ttu-id="f3310-266">每個獲授權存取服務的人應該有發行給他專用的用戶端憑證，而且應該選擇他自己的強式密碼來保護私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f3310-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="f3310-267">在產生及儲存自我簽署 CA 憑證的同一部電腦上，必須執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f3310-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="f3310-268">自訂：</span><span class="sxs-lookup"><span data-stu-id="f3310-268">Customizing:</span></span>

* <span data-ttu-id="f3310-269">-n 與將會使用此憑證進行驗證的用戶端的識別碼</span><span class="sxs-lookup"><span data-stu-id="f3310-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="f3310-270">-e 與憑證到期日</span><span class="sxs-lookup"><span data-stu-id="f3310-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="f3310-271">MyID.pvk 和 MyID.cer，使用這個用戶端憑證的唯一檔名</span><span class="sxs-lookup"><span data-stu-id="f3310-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="f3310-272">此命令會提示建立密碼，然後使用一次。</span><span class="sxs-lookup"><span data-stu-id="f3310-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="f3310-273">請使用強式密碼。</span><span class="sxs-lookup"><span data-stu-id="f3310-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="f3310-274">建立用戶端憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="f3310-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="f3310-275">對於每個產生的用戶端憑證，請執行：</span><span class="sxs-lookup"><span data-stu-id="f3310-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="f3310-276">自訂：</span><span class="sxs-lookup"><span data-stu-id="f3310-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="f3310-277">輸入密碼，然後使用這些選項來匯出憑證：</span><span class="sxs-lookup"><span data-stu-id="f3310-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="f3310-278">是，匯出私密金鑰</span><span class="sxs-lookup"><span data-stu-id="f3310-278">Yes, export the private key</span></span>
* <span data-ttu-id="f3310-279">匯出所有延伸內容</span><span class="sxs-lookup"><span data-stu-id="f3310-279">Export all extended properties</span></span>
* <span data-ttu-id="f3310-280">此憑證的發行對象應該選擇匯出密碼</span><span class="sxs-lookup"><span data-stu-id="f3310-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="f3310-281">匯入用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-281">Import client certificate</span></span>
<span data-ttu-id="f3310-282">用戶端憑證已發給的每個人，應該在他要用來與服務通訊的電腦中匯入金鑰組：</span><span class="sxs-lookup"><span data-stu-id="f3310-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="f3310-283">在 Windows 檔案總管中按兩下 .PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="f3310-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="f3310-284">至少使用這個選項，將憑證匯入個人存放區：</span><span class="sxs-lookup"><span data-stu-id="f3310-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="f3310-285">核取 [包含所有延伸內容]</span><span class="sxs-lookup"><span data-stu-id="f3310-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="f3310-286">複製用戶端憑證指紋</span><span class="sxs-lookup"><span data-stu-id="f3310-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="f3310-287">用戶端憑證已發給的每個人必須依照下列步驟，以取得將加入至服務組態檔的憑證指紋：</span><span class="sxs-lookup"><span data-stu-id="f3310-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="f3310-288">執行 certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="f3310-288">Run certmgr.exe</span></span>
* <span data-ttu-id="f3310-289">選取 [個人] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="f3310-289">Select the Personal tab</span></span>
* <span data-ttu-id="f3310-290">按兩下要用於驗證的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="f3310-291">在開啟的 [憑證] 對話方塊中，選取 [詳細資料] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="f3310-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="f3310-292">請確定 [顯示] 是顯示 [全部]</span><span class="sxs-lookup"><span data-stu-id="f3310-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="f3310-293">在清單中選取名為 [憑證指紋] 的欄位</span><span class="sxs-lookup"><span data-stu-id="f3310-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="f3310-294">複製憑證指紋值 ** 刪除第一個數字前面不可見的 Unicode 字元 ** 刪除所有的空格</span><span class="sxs-lookup"><span data-stu-id="f3310-294">Copy the value of the thumbprint ** Delete non-visible Unicode characters in front of the first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="f3310-295">在服務組態檔中設定允許的用戶端</span><span class="sxs-lookup"><span data-stu-id="f3310-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="f3310-296">使用允許存取服務的用戶端憑證指紋的逗號分隔清單，在服務組態檔中更新下列設定的值：</span><span class="sxs-lookup"><span data-stu-id="f3310-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="f3310-297">設定用戶端憑證撤銷檢查</span><span class="sxs-lookup"><span data-stu-id="f3310-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="f3310-298">預設不會向憑證授權單位查詢用戶端憑證的撤銷狀態。</span><span class="sxs-lookup"><span data-stu-id="f3310-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="f3310-299">若要開啟檢查 (如果發行用戶端憑證的憑證授權單位支援此檢查)，請使用 X509RevocationMode 列舉所定義的其中一個值來變更下列設定：</span><span class="sxs-lookup"><span data-stu-id="f3310-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="f3310-300">建立自我簽署加密憑證的 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="f3310-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="f3310-301">如需加密憑證，請執行：</span><span class="sxs-lookup"><span data-stu-id="f3310-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="f3310-302">自訂：</span><span class="sxs-lookup"><span data-stu-id="f3310-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="f3310-303">輸入密碼，然後使用這些選項來匯出憑證：</span><span class="sxs-lookup"><span data-stu-id="f3310-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="f3310-304">是，匯出私密金鑰</span><span class="sxs-lookup"><span data-stu-id="f3310-304">Yes, export the private key</span></span>
* <span data-ttu-id="f3310-305">匯出所有延伸內容</span><span class="sxs-lookup"><span data-stu-id="f3310-305">Export all extended properties</span></span>
* <span data-ttu-id="f3310-306">將憑證上傳至雲端服務時，您將需要密碼。</span><span class="sxs-lookup"><span data-stu-id="f3310-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="f3310-307">從憑證存放區匯出加密憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="f3310-308">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-308">Find certificate</span></span>
* <span data-ttu-id="f3310-309">按一下 [動作] -> [所有工作] -> [匯出...]</span><span class="sxs-lookup"><span data-stu-id="f3310-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="f3310-310">使用這些選項將憑證匯出至 .PFX 檔案：</span><span class="sxs-lookup"><span data-stu-id="f3310-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="f3310-311">是，匯出私密金鑰</span><span class="sxs-lookup"><span data-stu-id="f3310-311">Yes, export the private key</span></span>
  * <span data-ttu-id="f3310-312">如果可能的話，包含憑證路徑中的所有憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="f3310-313">匯出所有延伸內容</span><span class="sxs-lookup"><span data-stu-id="f3310-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="f3310-314">將加密憑證上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="f3310-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="f3310-315">將現有或產生的 .PFX 檔案及加密金鑰組連同憑證一起上傳：</span><span class="sxs-lookup"><span data-stu-id="f3310-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="f3310-316">輸入密碼以保護私密金鑰資訊</span><span class="sxs-lookup"><span data-stu-id="f3310-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="f3310-317">在服務組態檔中更新加密憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="f3310-318">使用上傳至雲端服務的憑證指紋，在服務組態檔中更新下列設定的指紋值：</span><span class="sxs-lookup"><span data-stu-id="f3310-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="f3310-319">常見的憑證作業</span><span class="sxs-lookup"><span data-stu-id="f3310-319">Common certificate operations</span></span>
* <span data-ttu-id="f3310-320">設定 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="f3310-321">設定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="f3310-322">尋找憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-322">Find certificate</span></span>
<span data-ttu-id="f3310-323">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f3310-323">Follow these steps:</span></span>

1. <span data-ttu-id="f3310-324">執行 mmc.exe。</span><span class="sxs-lookup"><span data-stu-id="f3310-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="f3310-325">[檔案] -> [新增/移除嵌入式管理單元]</span><span class="sxs-lookup"><span data-stu-id="f3310-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="f3310-326">選取 [ **憑證**]。</span><span class="sxs-lookup"><span data-stu-id="f3310-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="f3310-327">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-327">Click **Add**.</span></span>
5. <span data-ttu-id="f3310-328">選擇憑證存放區位置。</span><span class="sxs-lookup"><span data-stu-id="f3310-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="f3310-329">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-329">Click **Finish**.</span></span>
7. <span data-ttu-id="f3310-330">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-330">Click **OK**.</span></span>
8. <span data-ttu-id="f3310-331">展開 [ **憑證**]。</span><span class="sxs-lookup"><span data-stu-id="f3310-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="f3310-332">展開憑證存放區節點。</span><span class="sxs-lookup"><span data-stu-id="f3310-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="f3310-333">展開 [憑證] 子節點。</span><span class="sxs-lookup"><span data-stu-id="f3310-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="f3310-334">在清單中選取憑證。</span><span class="sxs-lookup"><span data-stu-id="f3310-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="f3310-335">匯出憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-335">Export certificate</span></span>
<span data-ttu-id="f3310-336">在 [ **憑證匯出精靈**] 中：</span><span class="sxs-lookup"><span data-stu-id="f3310-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="f3310-337">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-337">Click **Next**.</span></span>
2. <span data-ttu-id="f3310-338">選取 [是]，再選取 [匯出私密金鑰]。</span><span class="sxs-lookup"><span data-stu-id="f3310-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="f3310-339">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-339">Click **Next**.</span></span>
4. <span data-ttu-id="f3310-340">選取想要的輸出檔案格式。</span><span class="sxs-lookup"><span data-stu-id="f3310-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="f3310-341">核取所需的選項。</span><span class="sxs-lookup"><span data-stu-id="f3310-341">Check the desired options.</span></span>
6. <span data-ttu-id="f3310-342">核取 [ **密碼**]。</span><span class="sxs-lookup"><span data-stu-id="f3310-342">Check **Password**.</span></span>
7. <span data-ttu-id="f3310-343">輸入強式密碼並加以確認。</span><span class="sxs-lookup"><span data-stu-id="f3310-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="f3310-344">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-344">Click **Next**.</span></span>
9. <span data-ttu-id="f3310-345">輸入或瀏覽至用來儲存憑證的檔案名稱 (使用 .PFX 副檔名)。</span><span class="sxs-lookup"><span data-stu-id="f3310-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="f3310-346">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-346">Click **Next**.</span></span>
11. <span data-ttu-id="f3310-347">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-347">Click **Finish**.</span></span>
12. <span data-ttu-id="f3310-348">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="f3310-349">匯入憑證</span><span class="sxs-lookup"><span data-stu-id="f3310-349">Import certificate</span></span>
<span data-ttu-id="f3310-350">在 [憑證匯入精靈] 中：</span><span class="sxs-lookup"><span data-stu-id="f3310-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="f3310-351">選取存放區位置。</span><span class="sxs-lookup"><span data-stu-id="f3310-351">Select the store location.</span></span>
   
   * <span data-ttu-id="f3310-352">如果只有在目前使用者下執行的處理程序會存取服務，請選取 [ **目前使用者** ]</span><span class="sxs-lookup"><span data-stu-id="f3310-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="f3310-353">如果這台電腦中的其他處理程序會存取服務，請選取 [ **本機電腦** ]</span><span class="sxs-lookup"><span data-stu-id="f3310-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="f3310-354">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-354">Click **Next**.</span></span>
3. <span data-ttu-id="f3310-355">如果從檔案匯入，請確認檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="f3310-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="f3310-356">如果匯入 .PFX 檔案：</span><span class="sxs-lookup"><span data-stu-id="f3310-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="f3310-357">輸入密碼以保護私密金鑰</span><span class="sxs-lookup"><span data-stu-id="f3310-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="f3310-358">選取匯入選項</span><span class="sxs-lookup"><span data-stu-id="f3310-358">Select import options</span></span>
5. <span data-ttu-id="f3310-359">選取將憑證「放入」以下的存放區</span><span class="sxs-lookup"><span data-stu-id="f3310-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="f3310-360">按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-360">Click **Browse**.</span></span>
7. <span data-ttu-id="f3310-361">選取所需的存放區。</span><span class="sxs-lookup"><span data-stu-id="f3310-361">Select the desired store.</span></span>
8. <span data-ttu-id="f3310-362">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="f3310-363">若已選擇 [受信任的根憑證授權單位] 存放區，請按一下 [ **是**]。</span><span class="sxs-lookup"><span data-stu-id="f3310-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="f3310-364">在所有對話方塊視窗上，按一下 [ **確定** ]。</span><span class="sxs-lookup"><span data-stu-id="f3310-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="f3310-365">Upload certificate</span><span class="sxs-lookup"><span data-stu-id="f3310-365">Upload certificate</span></span>
<span data-ttu-id="f3310-366">在 [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="f3310-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="f3310-367">選取 [雲端服務] 。</span><span class="sxs-lookup"><span data-stu-id="f3310-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="f3310-368">選取雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f3310-368">Select the cloud service.</span></span>
3. <span data-ttu-id="f3310-369">按一下頂端功能表的 [ **憑證**]。</span><span class="sxs-lookup"><span data-stu-id="f3310-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="f3310-370">按一下底列的 [ **上傳**]。</span><span class="sxs-lookup"><span data-stu-id="f3310-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="f3310-371">選取憑證檔。</span><span class="sxs-lookup"><span data-stu-id="f3310-371">Select the certificate file.</span></span>
6. <span data-ttu-id="f3310-372">如果是 .PFX 檔案，請輸入私密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="f3310-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="f3310-373">完成後，從清單中的新項目複製憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="f3310-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="f3310-374">其他安全性考量</span><span class="sxs-lookup"><span data-stu-id="f3310-374">Other security considerations</span></span>
<span data-ttu-id="f3310-375">使用 HTTPS 端點時，這份文件中所述的 SSL 設定會加密服務和用戶端之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="f3310-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="f3310-376">這很重要，因為通訊中包含用來存取資料庫和其他可能機密資訊的認證。</span><span class="sxs-lookup"><span data-stu-id="f3310-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="f3310-377">但是請注意，服務會將內部狀態 (包括認證) 保存在 Microsoft Azure SQL 資料庫的內部資料表中 (您在 Microsoft Azure 訂用帳戶中已提供作為中繼資料儲存體)。</span><span class="sxs-lookup"><span data-stu-id="f3310-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="f3310-378">在服務組態檔中 (.CSCFG 檔案)，下列設定中已定義該資料庫：</span><span class="sxs-lookup"><span data-stu-id="f3310-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="f3310-379">這個資料庫中儲存的認證會被加密。</span><span class="sxs-lookup"><span data-stu-id="f3310-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="f3310-380">此外，最佳作法是確定服務部署的 Web 和背景工作角色保持在最新狀態且安全，因為它們都能存取中繼資料資料庫和用來加密和解密已儲存的認證。</span><span class="sxs-lookup"><span data-stu-id="f3310-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

