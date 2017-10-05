---
title: "存取防火牆後面的金鑰保存庫 | Microsoft Docs"
description: "了解如何從防火牆後面的應用程式存取 Azure 金鑰保存庫"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: d00c6e0acf437d2bfc3c27e948f4646a6685b08f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a><span data-ttu-id="9b71f-103">在防火牆後存取 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9b71f-103">Access Azure Key Vault behind a firewall</span></span>
### <a name="q-my-key-vault-client-application-needs-to-be-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-to-enable-access-to-a-key-vault"></a><span data-ttu-id="9b71f-104">問︰我的金鑰保存庫用戶端應用程式必須位於防火牆後。</span><span class="sxs-lookup"><span data-stu-id="9b71f-104">Q: My key vault client application needs to be behind a firewall.</span></span> <span data-ttu-id="9b71f-105">我應該開啟哪些連接埠、主機或 IP 位址以啟用金鑰保存庫的存取權？</span><span class="sxs-lookup"><span data-stu-id="9b71f-105">What ports, hosts, or IP addresses should I open to enable access to a key vault?</span></span>
<span data-ttu-id="9b71f-106">若要存取金鑰保存庫，您的金鑰保存庫用戶端應用程式必須存取多個端點才能使用各種功能：</span><span class="sxs-lookup"><span data-stu-id="9b71f-106">To access a key vault, your key vault client application has to access multiple endpoints for various functionalities:</span></span>

* <span data-ttu-id="9b71f-107">透過 Azure Active Directory (Azure AD) 進行的驗證。</span><span class="sxs-lookup"><span data-stu-id="9b71f-107">Authentication via Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="9b71f-108">Azure 金鑰保存庫的管理。</span><span class="sxs-lookup"><span data-stu-id="9b71f-108">Management of Azure Key Vault.</span></span> <span data-ttu-id="9b71f-109">這包括透過 Azure Resource Manager 建立、讀取、更新、刪除和設定存取原則。</span><span class="sxs-lookup"><span data-stu-id="9b71f-109">This includes creating, reading, updating, deleting, and setting access policies through Azure Resource Manager.</span></span>
* <span data-ttu-id="9b71f-110">經由金鑰保存庫專用端點 (例如 [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net))，存取和管理金鑰保存庫本身儲存的物件 (金鑰和密碼)。</span><span class="sxs-lookup"><span data-stu-id="9b71f-110">Accessing and managing objects (keys and secrets) stored in Key Vault itself, going through the Key Vault-specific endpoint (for example, [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).</span></span>  

<span data-ttu-id="9b71f-111">視您的組態和環境而定，會有一些變化。</span><span class="sxs-lookup"><span data-stu-id="9b71f-111">Depending on your configuration and environment, there are some variations.</span></span>   

## <a name="ports"></a><span data-ttu-id="9b71f-112">連接埠</span><span class="sxs-lookup"><span data-stu-id="9b71f-112">Ports</span></span>
<span data-ttu-id="9b71f-113">三項功能 (驗證、管理和資料平面存取) 的所有金鑰保存庫流量都會透過 HTTPS︰連接埠 443 傳送。</span><span class="sxs-lookup"><span data-stu-id="9b71f-113">All traffic to a key vault for all three functions (authentication, management, and data plane access) goes over HTTPS: port 443.</span></span> <span data-ttu-id="9b71f-114">不過，偶爾會有 CRL 的 HTTP (連接埠 80) 流量。</span><span class="sxs-lookup"><span data-stu-id="9b71f-114">However, there will occasionally be HTTP (port 80) traffic for CRL.</span></span> <span data-ttu-id="9b71f-115">支援 OCSP 的用戶端不應該觸達 CRL，但可能偶爾會觸達 [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl)。</span><span class="sxs-lookup"><span data-stu-id="9b71f-115">Clients that support OCSP shouldn't reach CRL, but may occasionally reach [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl).</span></span>  

## <a name="authentication"></a><span data-ttu-id="9b71f-116">驗證</span><span class="sxs-lookup"><span data-stu-id="9b71f-116">Authentication</span></span>
<span data-ttu-id="9b71f-117">金鑰保存庫用戶端應用程式必須存取 Azure Active Directory 端點以便驗證。</span><span class="sxs-lookup"><span data-stu-id="9b71f-117">Key vault client applications will need to access Azure Active Directory endpoints for authentication.</span></span> <span data-ttu-id="9b71f-118">使用的端點取決於 Azure AD 租用戶組態、主體類型 (使用者主體或服務主體) 和帳戶類型 (例如 Microsoft 帳戶，或是公司帳戶或學校帳戶)。</span><span class="sxs-lookup"><span data-stu-id="9b71f-118">The endpoint used depends on the Azure AD tenant configuration, the type of principal (user principal or service principal), and the type of account--for example, a Microsoft account or a work or school account.</span></span>  

| <span data-ttu-id="9b71f-119">主體類型</span><span class="sxs-lookup"><span data-stu-id="9b71f-119">Principal type</span></span> | <span data-ttu-id="9b71f-120">端點:連接埠</span><span class="sxs-lookup"><span data-stu-id="9b71f-120">Endpoint:port</span></span> |
| --- | --- |
| <span data-ttu-id="9b71f-121">使用 Microsoft 帳戶的使用者</span><span class="sxs-lookup"><span data-stu-id="9b71f-121">User using Microsoft account</span></span><br> <span data-ttu-id="9b71f-122">(例如， user@hotmail.com)</span><span class="sxs-lookup"><span data-stu-id="9b71f-122">(for example, user@hotmail.com)</span></span> |<span data-ttu-id="9b71f-123">**全域：**</span><span class="sxs-lookup"><span data-stu-id="9b71f-123">**Global:**</span></span><br> <span data-ttu-id="9b71f-124">login.microsoftonline.com:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-124">login.microsoftonline.com:443</span></span><br><br> <span data-ttu-id="9b71f-125">**Azure 中國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-125">**Azure China:**</span></span><br> <span data-ttu-id="9b71f-126">login.chinacloudapi.cn:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-126">login.chinacloudapi.cn:443</span></span><br><br><span data-ttu-id="9b71f-127">**Azure 美國政府︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-127">**Azure US Government:**</span></span><br> <span data-ttu-id="9b71f-128">login-us.microsoftonline.com:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-128">login-us.microsoftonline.com:443</span></span><br><br><span data-ttu-id="9b71f-129">**Azure 德國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-129">**Azure Germany:**</span></span><br> <span data-ttu-id="9b71f-130">login.microsoftonline.de:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-130">login.microsoftonline.de:443</span></span><br><br> <span data-ttu-id="9b71f-131">和</span><span class="sxs-lookup"><span data-stu-id="9b71f-131">and</span></span> <br><span data-ttu-id="9b71f-132">login.live.com:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-132">login.live.com:443</span></span> |
| <span data-ttu-id="9b71f-133">使用者或服務主體與 Azure AD 中使用工作或學校帳戶 (例如， user@contoso.com)</span><span class="sxs-lookup"><span data-stu-id="9b71f-133">User or service principal using a work or school account with Azure AD (for example, user@contoso.com)</span></span> |<span data-ttu-id="9b71f-134">**全域：**</span><span class="sxs-lookup"><span data-stu-id="9b71f-134">**Global:**</span></span><br> <span data-ttu-id="9b71f-135">login.microsoftonline.com:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-135">login.microsoftonline.com:443</span></span><br><br> <span data-ttu-id="9b71f-136">**Azure 中國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-136">**Azure China:**</span></span><br> <span data-ttu-id="9b71f-137">login.chinacloudapi.cn:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-137">login.chinacloudapi.cn:443</span></span><br><br><span data-ttu-id="9b71f-138">**Azure 美國政府︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-138">**Azure US Government:**</span></span><br> <span data-ttu-id="9b71f-139">login-us.microsoftonline.com:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-139">login-us.microsoftonline.com:443</span></span><br><br><span data-ttu-id="9b71f-140">**Azure 德國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-140">**Azure Germany:**</span></span><br> <span data-ttu-id="9b71f-141">login.microsoftonline.de:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-141">login.microsoftonline.de:443</span></span> |
| <span data-ttu-id="9b71f-142">使用者或服務主體使用工作或學校帳戶，再加上 Active Directory Federation Services (AD FS) 或其他同盟的端點 (例如， user@contoso.com)</span><span class="sxs-lookup"><span data-stu-id="9b71f-142">User or service principal using a work or school account, plus Active Directory Federation Services (AD FS) or other federated endpoint (for example, user@contoso.com)</span></span> |<span data-ttu-id="9b71f-143">公司帳戶或學校帳戶的所有端點，加上 AD FS 或其他同盟端點</span><span class="sxs-lookup"><span data-stu-id="9b71f-143">All endpoints for a work or school account, plus AD FS or other federated endpoints</span></span> |

<span data-ttu-id="9b71f-144">還有其他可能的複雜案例。</span><span class="sxs-lookup"><span data-stu-id="9b71f-144">There are other possible complex scenarios.</span></span> <span data-ttu-id="9b71f-145">如需其他資訊，請參閱 [Azure Active Directory 驗證流程](/documentation/articles/active-directory-authentication-scenarios/)、[整合應用程式與 Azure Active Directory](/documentation/articles/active-directory-integrating-applications/) 及 [Active Directory 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn151124.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9b71f-145">Refer to [Azure Active Directory Authentication Flow](/documentation/articles/active-directory-authentication-scenarios/), [Integrating Applications with Azure Active Directory](/documentation/articles/active-directory-integrating-applications/), and [Active Directory Authentication Protocols](https://msdn.microsoft.com/library/azure/dn151124.aspx) for additional information.</span></span>  

## <a name="key-vault-management"></a><span data-ttu-id="9b71f-146">金鑰保存庫管理</span><span class="sxs-lookup"><span data-stu-id="9b71f-146">Key Vault management</span></span>
<span data-ttu-id="9b71f-147">對於金鑰保存庫管理 (CRUD 和設定存取原則)，金鑰保存庫用戶端應用程式需要存取 Azure Resource Manager 端點。</span><span class="sxs-lookup"><span data-stu-id="9b71f-147">For Key Vault management (CRUD and setting access policy), the key vault client application needs to access an Azure Resource Manager endpoint.</span></span>  

| <span data-ttu-id="9b71f-148">作業類型</span><span class="sxs-lookup"><span data-stu-id="9b71f-148">Type of operation</span></span> | <span data-ttu-id="9b71f-149">端點:連接埠</span><span class="sxs-lookup"><span data-stu-id="9b71f-149">Endpoint:port</span></span> |
| --- | --- |
| <span data-ttu-id="9b71f-150">透過 Azure Resource Manager 的</span><span class="sxs-lookup"><span data-stu-id="9b71f-150">Key Vault control plane operations</span></span><br> <span data-ttu-id="9b71f-151">金鑰保存庫控制項面作業</span><span class="sxs-lookup"><span data-stu-id="9b71f-151">via Azure Resource Manager</span></span> |<span data-ttu-id="9b71f-152">**全域：**</span><span class="sxs-lookup"><span data-stu-id="9b71f-152">**Global:**</span></span><br> <span data-ttu-id="9b71f-153">management.azure.com:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-153">management.azure.com:443</span></span><br><br> <span data-ttu-id="9b71f-154">**Azure 中國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-154">**Azure China:**</span></span><br> <span data-ttu-id="9b71f-155">management.chinacloudapi.cn:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-155">management.chinacloudapi.cn:443</span></span><br><br> <span data-ttu-id="9b71f-156">**Azure 美國政府︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-156">**Azure US Government:**</span></span><br> <span data-ttu-id="9b71f-157">management.usgovcloudapi.net:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-157">management.usgovcloudapi.net:443</span></span><br><br> <span data-ttu-id="9b71f-158">**Azure 德國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-158">**Azure Germany:**</span></span><br> <span data-ttu-id="9b71f-159">management.microsoftazure.de:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-159">management.microsoftazure.de:443</span></span> |
| <span data-ttu-id="9b71f-160">Azure Active Directory 圖形 API</span><span class="sxs-lookup"><span data-stu-id="9b71f-160">Azure Active Directory Graph API</span></span> |<span data-ttu-id="9b71f-161">**全域：**</span><span class="sxs-lookup"><span data-stu-id="9b71f-161">**Global:**</span></span><br> <span data-ttu-id="9b71f-162">graph.windows.net:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-162">graph.windows.net:443</span></span><br><br> <span data-ttu-id="9b71f-163">**Azure 中國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-163">**Azure China:**</span></span><br> <span data-ttu-id="9b71f-164">graph.chinacloudapi.cn:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-164">graph.chinacloudapi.cn:443</span></span><br><br> <span data-ttu-id="9b71f-165">**Azure 美國政府︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-165">**Azure US Government:**</span></span><br> <span data-ttu-id="9b71f-166">graph.windows.net:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-166">graph.windows.net:443</span></span><br><br> <span data-ttu-id="9b71f-167">**Azure 德國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-167">**Azure Germany:**</span></span><br> <span data-ttu-id="9b71f-168">graph.cloudapi.de:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-168">graph.cloudapi.de:443</span></span> |

## <a name="key-vault-operations"></a><span data-ttu-id="9b71f-169">金鑰保存庫作業</span><span class="sxs-lookup"><span data-stu-id="9b71f-169">Key Vault operations</span></span>
<span data-ttu-id="9b71f-170">對於所有金鑰保存庫物件 (金鑰和密碼) 管理和密碼編譯作業，金鑰保存庫用戶端需要存取金鑰保存庫端點。</span><span class="sxs-lookup"><span data-stu-id="9b71f-170">For all key vault object (keys and secrets) management and cryptographic operations, the key vault client needs to access the key vault endpoint.</span></span> <span data-ttu-id="9b71f-171">視金鑰保存庫的位置而定，端點 DNS 尾碼會有所不同。</span><span class="sxs-lookup"><span data-stu-id="9b71f-171">The endpoint DNS suffix varies depending on the location of your key vault.</span></span> <span data-ttu-id="9b71f-172">金鑰保存庫端點的格式為 vault-name.region-specific-dns-suffix，如下表所述。</span><span class="sxs-lookup"><span data-stu-id="9b71f-172">The key vault endpoint is of the format *vault-name*.*region-specific-dns-suffix*, as described in the following table.</span></span>  

| <span data-ttu-id="9b71f-173">作業類型</span><span class="sxs-lookup"><span data-stu-id="9b71f-173">Type of operation</span></span> | <span data-ttu-id="9b71f-174">端點:連接埠</span><span class="sxs-lookup"><span data-stu-id="9b71f-174">Endpoint:port</span></span> |
| --- | --- |
| <span data-ttu-id="9b71f-175">包括金鑰的密碼編譯作業在內的作業；建立、讀取、更新和刪除金鑰與密碼；對金鑰保存庫物件 (金鑰或密碼) 設定或取得標籤和其他屬性</span><span class="sxs-lookup"><span data-stu-id="9b71f-175">Operations including cryptographic operations on keys; creating, reading, updating, and deleting keys and secrets; setting or getting tags and other attributes on key vault objects (keys or secrets)</span></span> |<span data-ttu-id="9b71f-176">**全域：**</span><span class="sxs-lookup"><span data-stu-id="9b71f-176">**Global:**</span></span><br> <span data-ttu-id="9b71f-177">&lt;vault-name&gt;.vault.azure.net:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-177">&lt;vault-name&gt;.vault.azure.net:443</span></span><br><br> <span data-ttu-id="9b71f-178">**Azure 中國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-178">**Azure China:**</span></span><br> <span data-ttu-id="9b71f-179">&lt;vault-name&gt;.vault.azure.cn:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-179">&lt;vault-name&gt;.vault.azure.cn:443</span></span><br><br> <span data-ttu-id="9b71f-180">**Azure 美國政府︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-180">**Azure US Government:**</span></span><br> <span data-ttu-id="9b71f-181">&lt;vault-name&gt;.vault.usgovcloudapi.net:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-181">&lt;vault-name&gt;.vault.usgovcloudapi.net:443</span></span><br><br> <span data-ttu-id="9b71f-182">**Azure 德國︰**</span><span class="sxs-lookup"><span data-stu-id="9b71f-182">**Azure Germany:**</span></span><br> <span data-ttu-id="9b71f-183">&lt;vault-name&gt;.vault.microsoftazure.de:443</span><span class="sxs-lookup"><span data-stu-id="9b71f-183">&lt;vault-name&gt;.vault.microsoftazure.de:443</span></span> |

## <a name="ip-address-ranges"></a><span data-ttu-id="9b71f-184">IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="9b71f-184">IP address ranges</span></span>
<span data-ttu-id="9b71f-185">金鑰保存庫服務會使用其他 Azure 資源，例如 PaaS 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="9b71f-185">The Key Vault service uses other Azure resources like PaaS infrastructure.</span></span> <span data-ttu-id="9b71f-186">因此，不可能提供金鑰保存庫服務端點在任何特定時間會有的特定 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="9b71f-186">So it's not possible to provide a specific range of IP addresses that Key Vault service endpoints will have at any particular time.</span></span> <span data-ttu-id="9b71f-187">如果您的防火牆只支援 IP 位址範圍，請參閱 [Microsoft Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)文件。</span><span class="sxs-lookup"><span data-stu-id="9b71f-187">If your firewall supports only IP address ranges, refer to the [Microsoft Azure Datacenter IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) document.</span></span> <span data-ttu-id="9b71f-188">如需驗證和身分識別 (Azure Active Directory)，您的應用程式必須能夠連接至[驗證和身分識別位址](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)中所述的端點。</span><span class="sxs-lookup"><span data-stu-id="9b71f-188">For authentication and identity (Azure Active Directory), your application must be able to connect to the endpoints described in [Authentication and identity addresses](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b71f-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b71f-189">Next steps</span></span>
<span data-ttu-id="9b71f-190">如果您有關於金鑰保存庫的問題，請造訪 [Azure 金鑰保存庫論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)。</span><span class="sxs-lookup"><span data-stu-id="9b71f-190">If you have questions about Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>
