---
title: "Azure 雲端服務角色常見問題集 | Microsoft Docs"
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
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="a0385-104">雲端服務常見問題集</span><span class="sxs-lookup"><span data-stu-id="a0385-104">Cloud Services FAQ</span></span>
<span data-ttu-id="a0385-105">本文提供 Microsoft Azure 雲端服務的一些常見問題解答。</span><span class="sxs-lookup"><span data-stu-id="a0385-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="a0385-106">您也可以造訪 [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083) ，以取得一般的 Azure 價格和支援資訊。</span><span class="sxs-lookup"><span data-stu-id="a0385-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="a0385-107">您也可以參閱 [雲端服務 VM 大小頁面](cloud-services-sizes-specs.md) 以取得大小資訊。</span><span class="sxs-lookup"><span data-stu-id="a0385-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="a0385-108">憑證</span><span class="sxs-lookup"><span data-stu-id="a0385-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="a0385-109">我應該將憑證安裝在何處？</span><span class="sxs-lookup"><span data-stu-id="a0385-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="a0385-110">**My**</span><span class="sxs-lookup"><span data-stu-id="a0385-110">**My**</span></span>  
  <span data-ttu-id="a0385-111">具有私密金鑰的應用程式憑證 (\*.pfx、\*.p12)。</span><span class="sxs-lookup"><span data-stu-id="a0385-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="a0385-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="a0385-112">**CA**</span></span>  
  <span data-ttu-id="a0385-113">所有中繼憑證都會放入此存放區 (原則和子 CA)。</span><span class="sxs-lookup"><span data-stu-id="a0385-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="a0385-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="a0385-114">**ROOT**</span></span>  
  <span data-ttu-id="a0385-115">根 CA 存放區，因此主要的根 CA 憑證應該放在這裡。</span><span class="sxs-lookup"><span data-stu-id="a0385-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="a0385-116">無法移除過期的憑證</span><span class="sxs-lookup"><span data-stu-id="a0385-116">I can't remove expired certificate</span></span>
<span data-ttu-id="a0385-117">Azure 會防止您移除使用中的憑證。</span><span class="sxs-lookup"><span data-stu-id="a0385-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="a0385-118">您必須刪除使用憑證的部署，或使用不同憑證或更新的憑證來更新部署。</span><span class="sxs-lookup"><span data-stu-id="a0385-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="a0385-119">刪除過期的憑證</span><span class="sxs-lookup"><span data-stu-id="a0385-119">Delete an expired certificate</span></span>
<span data-ttu-id="a0385-120">只要憑證不在使用中，您就可以使用 [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell Cmdlet 來移除憑證。</span><span class="sxs-lookup"><span data-stu-id="a0385-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="a0385-121">我有名為 Windows Azure Service Management for Extensions 的已過期憑證</span><span class="sxs-lookup"><span data-stu-id="a0385-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="a0385-122">每當有擴充功能新增至雲端服務 (例如遠端桌面擴充功能)，就會建立這些憑證。</span><span class="sxs-lookup"><span data-stu-id="a0385-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="a0385-123">這些憑證只會用於加密和解密擴充功能的私用組態。</span><span class="sxs-lookup"><span data-stu-id="a0385-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="a0385-124">這些憑證是否過期並不重要。</span><span class="sxs-lookup"><span data-stu-id="a0385-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="a0385-125">系統不會檢查到期日期。</span><span class="sxs-lookup"><span data-stu-id="a0385-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="a0385-126">我已刪除的憑證一直重複出現</span><span class="sxs-lookup"><span data-stu-id="a0385-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="a0385-127">這些憑證會一直重複出現很可能是因為您所使用的工具，例如 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a0385-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="a0385-128">每當您以使用某憑證的工具重新連線，該憑證就會再次上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="a0385-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="a0385-129">我的憑證一直消失</span><span class="sxs-lookup"><span data-stu-id="a0385-129">My certificates keep disappearing</span></span>
<span data-ttu-id="a0385-130">當虛擬機器執行個體回收時，所有本機變更都會遺失。</span><span class="sxs-lookup"><span data-stu-id="a0385-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="a0385-131">請在每次角色啟動時使用 [啟動工作](cloud-services-startup-tasks.md) 將憑證安裝到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a0385-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="a0385-132">我在入口網站中找不到我的管理憑證</span><span class="sxs-lookup"><span data-stu-id="a0385-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="a0385-133">[管理憑證](../azure-api-management-certs.md)只能在 Azure 傳統入口網站中取得。</span><span class="sxs-lookup"><span data-stu-id="a0385-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="a0385-134">目前的 Azure 入口網站沒有使用管理憑證。</span><span class="sxs-lookup"><span data-stu-id="a0385-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="a0385-135">如何停用管理憑證？</span><span class="sxs-lookup"><span data-stu-id="a0385-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="a0385-136">[管理憑證](../azure-api-management-certs.md) 無法停用。</span><span class="sxs-lookup"><span data-stu-id="a0385-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="a0385-137">當您不想再使用它們之後，可以透過 Azure 傳統入口網站將它們刪除。</span><span class="sxs-lookup"><span data-stu-id="a0385-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="a0385-138">如何為特定 IP 位址建立 SSL 憑證？</span><span class="sxs-lookup"><span data-stu-id="a0385-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="a0385-139">請遵照 [建立憑證教學課程](cloud-services-certs-create.md)中的指示執行。</span><span class="sxs-lookup"><span data-stu-id="a0385-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="a0385-140">使用 IP 位址做為 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="a0385-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="a0385-141">安全性</span><span class="sxs-lookup"><span data-stu-id="a0385-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="a0385-142">停用 SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="a0385-142">Disable SSL 3.0</span></span>
<span data-ttu-id="a0385-143">若要停用 SSL 3.0 並使用 TLS 安全性，請建立啟動工作，而其記載於此部落格文章：https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="a0385-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="a0385-144">將 **nosniff** 加入您的網站</span><span class="sxs-lookup"><span data-stu-id="a0385-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="a0385-145">若要防止用戶端探查 MIME 類型，請在您的 *web.config* 檔案中加入一項設定。</span><span class="sxs-lookup"><span data-stu-id="a0385-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="a0385-146">您也可以在 IIS 中將此加入為設定。</span><span class="sxs-lookup"><span data-stu-id="a0385-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="a0385-147">請參考[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)一文來使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="a0385-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="a0385-148">針對 Web 角色自訂 IIS</span><span class="sxs-lookup"><span data-stu-id="a0385-148">Customize IIS for a web role</span></span>
<span data-ttu-id="a0385-149">請從[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)一文使用 IIS 啟動指令碼。</span><span class="sxs-lookup"><span data-stu-id="a0385-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="a0385-150">調整大小</span><span class="sxs-lookup"><span data-stu-id="a0385-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="a0385-151">我不能調整超過 X 個執行個體</span><span class="sxs-lookup"><span data-stu-id="a0385-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="a0385-152">您的 Azure 訂用帳戶對於您可以使用的核心數目有限制。</span><span class="sxs-lookup"><span data-stu-id="a0385-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="a0385-153">如果您已使用所有可用的核心，調整將無法運作。</span><span class="sxs-lookup"><span data-stu-id="a0385-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="a0385-154">例如，如果您有 100 個核心的限制，這表示您的雲端服務可以有 100 個 A1 大小的虛擬機器執行個體，或 50 個 A2 大小的虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="a0385-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="a0385-155">網路</span><span class="sxs-lookup"><span data-stu-id="a0385-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="a0385-156">無法在多 VIP 的雲端服務中保留 IP</span><span class="sxs-lookup"><span data-stu-id="a0385-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="a0385-157">首先，請確定您想要保留其 IP 的虛擬機器執行個體已開啟。</span><span class="sxs-lookup"><span data-stu-id="a0385-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="a0385-158">其次，請確定您會將保留的 IP 同時用於預備與生產部署。</span><span class="sxs-lookup"><span data-stu-id="a0385-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="a0385-159">**勿** 於部署正在升級時變更設定。</span><span class="sxs-lookup"><span data-stu-id="a0385-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="a0385-160">遠端桌面</span><span class="sxs-lookup"><span data-stu-id="a0385-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="a0385-161">當我有 NSG 時，應如何設定遠端桌面？</span><span class="sxs-lookup"><span data-stu-id="a0385-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="a0385-162">將規則加入到 NSG，以允許連接埠 **3389** 和 **20000** 上的流量。</span><span class="sxs-lookup"><span data-stu-id="a0385-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="a0385-163">遠端桌面使用者連接埠 **3389**。</span><span class="sxs-lookup"><span data-stu-id="a0385-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="a0385-164">系統已為雲端服務執行個體進行負載平衡，因此您無法直接控制要連線的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a0385-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="a0385-165">*RemoteForwarder* 與 *RemoteAccess* 代理程式會管理 RDP 流量，並允許用戶端傳送 RDP Cookie 並指定要連線的個別執行個體。</span><span class="sxs-lookup"><span data-stu-id="a0385-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="a0385-166">*RemoteForwarder* 與 *RemoteAccess* 代理程式要求您必須開啟連接埠 **20000***，這在您使用 NSG 的情況下可能是封鎖的。</span><span class="sxs-lookup"><span data-stu-id="a0385-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
