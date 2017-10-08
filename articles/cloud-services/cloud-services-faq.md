---
title: "aaaAzure 雲端服務角色常見問題集 |Microsoft 文件"
description: "關於 Azure 雲端服務的常見問題集。 關於憑證、Web 角色和背景工作角色的一些常見問題解答。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="775e1-104">雲端服務常見問題集</span><span class="sxs-lookup"><span data-stu-id="775e1-104">Cloud Services FAQ</span></span>
<span data-ttu-id="775e1-105">本文提供 Microsoft Azure 雲端服務的一些常見問題解答。</span><span class="sxs-lookup"><span data-stu-id="775e1-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="775e1-106">您也可以造訪 hello [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)一般 Azure 定價和支援資訊。</span><span class="sxs-lookup"><span data-stu-id="775e1-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="775e1-107">此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。</span><span class="sxs-lookup"><span data-stu-id="775e1-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="775e1-108">憑證</span><span class="sxs-lookup"><span data-stu-id="775e1-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="775e1-109">我應該將憑證安裝在何處？</span><span class="sxs-lookup"><span data-stu-id="775e1-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="775e1-110">**My**</span><span class="sxs-lookup"><span data-stu-id="775e1-110">**My**</span></span>  
  <span data-ttu-id="775e1-111">具有私密金鑰的應用程式憑證 (\*.pfx、\*.p12)。</span><span class="sxs-lookup"><span data-stu-id="775e1-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="775e1-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="775e1-112">**CA**</span></span>  
  <span data-ttu-id="775e1-113">所有中繼憑證都會放入此存放區 (原則和子 CA)。</span><span class="sxs-lookup"><span data-stu-id="775e1-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="775e1-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="775e1-114">**ROOT**</span></span>  
  <span data-ttu-id="775e1-115">hello 根 CA 存放區，讓您的主要根 CA 憑證應該在這裡。</span><span class="sxs-lookup"><span data-stu-id="775e1-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="775e1-116">無法移除過期的憑證</span><span class="sxs-lookup"><span data-stu-id="775e1-116">I can't remove expired certificate</span></span>
<span data-ttu-id="775e1-117">Azure 會防止您移除使用中的憑證。</span><span class="sxs-lookup"><span data-stu-id="775e1-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="775e1-118">您需要使用 hello 憑證 tooeither 刪除 hello 部署或更新 hello 部署具有不同或更新憑證。</span><span class="sxs-lookup"><span data-stu-id="775e1-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="775e1-119">刪除過期的憑證</span><span class="sxs-lookup"><span data-stu-id="775e1-119">Delete an expired certificate</span></span>
<span data-ttu-id="775e1-120">只要 hello 憑證不在使用中，您可以使用 hello[移除 AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove 憑證。</span><span class="sxs-lookup"><span data-stu-id="775e1-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="775e1-121">我有名為 Windows Azure Service Management for Extensions 的已過期憑證</span><span class="sxs-lookup"><span data-stu-id="775e1-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="775e1-122">擴充功能加入 toohello 雲端服務，例如 hello 遠端桌面延伸模組時，會建立這些憑證。</span><span class="sxs-lookup"><span data-stu-id="775e1-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="775e1-123">這些憑證只用於加密和解密 hello 擴充的 hello 私用組態。</span><span class="sxs-lookup"><span data-stu-id="775e1-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="775e1-124">這些憑證是否過期並不重要。</span><span class="sxs-lookup"><span data-stu-id="775e1-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="775e1-125">不會檢查 hello 到期日。</span><span class="sxs-lookup"><span data-stu-id="775e1-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="775e1-126">我已刪除的憑證一直重複出現</span><span class="sxs-lookup"><span data-stu-id="775e1-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="775e1-127">這些憑證會一直重複出現很可能是因為您所使用的工具，例如 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="775e1-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="775e1-128">每當您重新連線使用的憑證的工具，將重新予以上傳的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="775e1-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="775e1-129">我的憑證一直消失</span><span class="sxs-lookup"><span data-stu-id="775e1-129">My certificates keep disappearing</span></span>
<span data-ttu-id="775e1-130">當 hello 虛擬機器執行個體回收時，所有本機變更都會遺失。</span><span class="sxs-lookup"><span data-stu-id="775e1-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="775e1-131">使用[啟動工作](cloud-services-startup-tasks.md)tooinstall 憑證 toohello 虛擬機器的每個時間 hello 角色啟動。</span><span class="sxs-lookup"><span data-stu-id="775e1-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="775e1-132">我找不到我的管理憑證在 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="775e1-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="775e1-133">[管理憑證](../azure-api-management-certs.md)hello Azure 傳統入口網站中才有。</span><span class="sxs-lookup"><span data-stu-id="775e1-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="775e1-134">hello 目前的 Azure 入口網站並不會使用管理憑證。</span><span class="sxs-lookup"><span data-stu-id="775e1-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="775e1-135">如何停用管理憑證？</span><span class="sxs-lookup"><span data-stu-id="775e1-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="775e1-136">[管理憑證](../azure-api-management-certs.md) 無法停用。</span><span class="sxs-lookup"><span data-stu-id="775e1-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="775e1-137">您刪除它們透過 hello Azure 傳統入口網站時您不希望 toobe 不再使用。</span><span class="sxs-lookup"><span data-stu-id="775e1-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="775e1-138">如何為特定 IP 位址建立 SSL 憑證？</span><span class="sxs-lookup"><span data-stu-id="775e1-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="775e1-139">依照指示進行 hello hello[建立憑證的教學課程](cloud-services-certs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="775e1-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="775e1-140">Hello DNS 名稱作為 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="775e1-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="775e1-141">安全性</span><span class="sxs-lookup"><span data-stu-id="775e1-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="775e1-142">停用 SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="775e1-142">Disable SSL 3.0</span></span>
<span data-ttu-id="775e1-143">toodisable SSL 3.0 和使用 TLS 安全性，建立啟動工作，而其已記錄在此部落格文章： https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="775e1-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="775e1-144">新增**nosniff** tooyour 網站</span><span class="sxs-lookup"><span data-stu-id="775e1-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="775e1-145">tooprevent 用戶端從探測 hello MIME 類型，新增設定，在您*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="775e1-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="775e1-146">您也可以在 IIS 中將此加入為設定。</span><span class="sxs-lookup"><span data-stu-id="775e1-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="775e1-147">使用 hello 下列命令以 hello[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)發行項。</span><span class="sxs-lookup"><span data-stu-id="775e1-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="775e1-148">針對 Web 角色自訂 IIS</span><span class="sxs-lookup"><span data-stu-id="775e1-148">Customize IIS for a web role</span></span>
<span data-ttu-id="775e1-149">使用 hello IIS 啟動指令碼從 hello[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)發行項。</span><span class="sxs-lookup"><span data-stu-id="775e1-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="775e1-150">調整大小</span><span class="sxs-lookup"><span data-stu-id="775e1-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="775e1-151">我不能調整超過 X 個執行個體</span><span class="sxs-lookup"><span data-stu-id="775e1-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="775e1-152">您的 Azure 訂閱 hello 您可以使用的核心數目的上限。</span><span class="sxs-lookup"><span data-stu-id="775e1-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="775e1-153">調整將無法運作如果您已使用所有可用的 hello 核心。</span><span class="sxs-lookup"><span data-stu-id="775e1-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="775e1-154">例如，如果您有 100 個核心的限制，這表示您的雲端服務可以有 100 個 A1 大小的虛擬機器執行個體，或 50 個 A2 大小的虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="775e1-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="775e1-155">網路</span><span class="sxs-lookup"><span data-stu-id="775e1-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="775e1-156">無法在多 VIP 的雲端服務中保留 IP</span><span class="sxs-lookup"><span data-stu-id="775e1-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="775e1-157">首先，請確定您正嘗試 tooreserve hello IP 用於該 hello 虛擬機器執行個體已開啟。</span><span class="sxs-lookup"><span data-stu-id="775e1-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="775e1-158">第二，請確定您麻煩 hello 預備和生產環境部署使用保留 Ip。</span><span class="sxs-lookup"><span data-stu-id="775e1-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="775e1-159">**不這麼做**hello 部署正在升級時，變更 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="775e1-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="775e1-160">遠端桌面</span><span class="sxs-lookup"><span data-stu-id="775e1-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="775e1-161">當我有 NSG 時，應如何設定遠端桌面？</span><span class="sxs-lookup"><span data-stu-id="775e1-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="775e1-162">新增規則 toohello 允許連接埠上的流量的 NSG **3389**和**20000**。</span><span class="sxs-lookup"><span data-stu-id="775e1-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="775e1-163">遠端桌面使用者連接埠 **3389**。</span><span class="sxs-lookup"><span data-stu-id="775e1-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="775e1-164">雲端服務執行個體是負載平衡，因此您無法直接控制至哪一個執行個體 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="775e1-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="775e1-165">hello *RemoteForwarder*和*RemoteAccess*代理程式管理 RDP 流量，並允許 hello 用戶端 toosend RDP cookie，並指定要個別執行個體 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="775e1-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="775e1-166">hello *RemoteForwarder*和*RemoteAccess*代理程式需要該連接埠**20000*** 開啟，如果您有 NSG 可能會封鎖連接。</span><span class="sxs-lookup"><span data-stu-id="775e1-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
