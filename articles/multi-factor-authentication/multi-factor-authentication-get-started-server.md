---
title: "aaaGetting 啟動 Azure Multi-factor Authentication Server |Microsoft 文件"
description: "這是描述 tooget 如何開始使用 Azure MFA Server hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
keywords: "驗證伺服器, azure multi factor authentication 應用程式啟動頁面, 驗證伺服器下載"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a><span data-ttu-id="16688-104">Hello Azure Multi-factor Authentication Server 使用者入門</span><span class="sxs-lookup"><span data-stu-id="16688-104">Getting started with hello Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="16688-105"><center>![MFA 內部部署](./media/multi-factor-authentication-get-started-server/server2.png)</center></span><span class="sxs-lookup"><span data-stu-id="16688-105"><center>![MFA on-premises](./media/multi-factor-authentication-get-started-server/server2.png)</center></span></span>

<span data-ttu-id="16688-106">既然我們判定 toouse 內部 Multi-factor Authentication Server，讓我們開始。</span><span class="sxs-lookup"><span data-stu-id="16688-106">Now that we have determined toouse on-premises Multi-Factor Authentication Server, let’s get going.</span></span> <span data-ttu-id="16688-107">此頁面涵蓋 hello 伺服器並設定與內部部署 Active Directory 的新安裝。</span><span class="sxs-lookup"><span data-stu-id="16688-107">This page covers a new installation of hello server and setting it up with on-premises Active Directory.</span></span> <span data-ttu-id="16688-108">如果您已經安裝 hello MFA server，並尋找 tooupgrade，請參閱[升級 toohello 最新的 Azure Multi-factor Authentication Server](multi-factor-authentication-server-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="16688-108">If you already have hello MFA server installed and are looking tooupgrade, see [Upgrade toohello latest Azure Multi-Factor Authentication Server](multi-factor-authentication-server-upgrade.md).</span></span> <span data-ttu-id="16688-109">如果您想要尋求安裝只 hello web 服務的詳細資訊，請參閱[部署 hello Azure Multi-factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="16688-109">If you're looking for information on installing just hello web service, see [Deploying hello Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).</span></span>

## <a name="plan-your-deployment"></a><span data-ttu-id="16688-110">規劃您的部署</span><span class="sxs-lookup"><span data-stu-id="16688-110">Plan your deployment</span></span>

<span data-ttu-id="16688-111">下載 hello Azure Multi-factor Authentication Server 之前，請考慮您的負載和高可用性需求為何。</span><span class="sxs-lookup"><span data-stu-id="16688-111">Before you download hello Azure Multi-Factor Authentication Server, think about what your load and high availability requirements are.</span></span> <span data-ttu-id="16688-112">使用此資訊 toodecide 方式和位置 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="16688-112">Use this information toodecide how and where toodeploy.</span></span>

<span data-ttu-id="16688-113">最好定期 hello 所需的記憶體數量是使用者的 hello 數目預期 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="16688-113">A good guideline for hello amount of memory you need is hello number of users you expect tooauthenticate on a regular basis.</span></span>

| <span data-ttu-id="16688-114">使用者</span><span class="sxs-lookup"><span data-stu-id="16688-114">Users</span></span> | <span data-ttu-id="16688-115">RAM</span><span class="sxs-lookup"><span data-stu-id="16688-115">RAM</span></span> |
| ----- | --- |
| <span data-ttu-id="16688-116">1-10,000</span><span class="sxs-lookup"><span data-stu-id="16688-116">1-10,000</span></span> | <span data-ttu-id="16688-117">4 GB</span><span class="sxs-lookup"><span data-stu-id="16688-117">4 GB</span></span> |
| <span data-ttu-id="16688-118">10,001-50,000</span><span class="sxs-lookup"><span data-stu-id="16688-118">10,001-50,000</span></span> | <span data-ttu-id="16688-119">8 GB</span><span class="sxs-lookup"><span data-stu-id="16688-119">8 GB</span></span> |
| <span data-ttu-id="16688-120">50,001-100,000</span><span class="sxs-lookup"><span data-stu-id="16688-120">50,001-100,000</span></span> | <span data-ttu-id="16688-121">12 GB</span><span class="sxs-lookup"><span data-stu-id="16688-121">12 GB</span></span> |
| <span data-ttu-id="16688-122">100,000-200,001</span><span class="sxs-lookup"><span data-stu-id="16688-122">100,000-200,001</span></span> | <span data-ttu-id="16688-123">16 GB</span><span class="sxs-lookup"><span data-stu-id="16688-123">16 GB</span></span> |
| <span data-ttu-id="16688-124">200,001+</span><span class="sxs-lookup"><span data-stu-id="16688-124">200,001+</span></span> | <span data-ttu-id="16688-125">32 GB</span><span class="sxs-lookup"><span data-stu-id="16688-125">32 GB</span></span> |

<span data-ttu-id="16688-126">需要 tooset 的多部伺服器的高可用性或負載平衡嗎？</span><span class="sxs-lookup"><span data-stu-id="16688-126">Do you need tooset up multiple servers for high availability or load balancing?</span></span> <span data-ttu-id="16688-127">有多種方式 tooset 此組態使用 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="16688-127">There are a number of ways tooset up this configuration with Azure MFA Server.</span></span> <span data-ttu-id="16688-128">當您安裝您的第一個 Azure MFA Server 時，它會變成 hello master。</span><span class="sxs-lookup"><span data-stu-id="16688-128">When you install your first Azure MFA Server, it becomes hello master.</span></span> <span data-ttu-id="16688-129">任何其他伺服器會變成從屬，及自動同步處理使用者和組態 hello 主機。</span><span class="sxs-lookup"><span data-stu-id="16688-129">Any additional servers become subordinate, and automatically synchronize users and configuration with hello master.</span></span> <span data-ttu-id="16688-130">然後，您可以在 設定一部主要伺服器，然後利用 hello rest 做為備份，或者您可以設定負載平衡 hello 的所有伺服器之間。</span><span class="sxs-lookup"><span data-stu-id="16688-130">Then, you can configure one primary server and have hello rest act as backup, or you can set up load balancing among all hello servers.</span></span>

<span data-ttu-id="16688-131">Azure MFA Server 的主機離線時，hello 次級伺服器仍然可以處理兩步驟驗證要求。</span><span class="sxs-lookup"><span data-stu-id="16688-131">When a master Azure MFA Server goes offline, hello subordinate servers can still process two-step verification requests.</span></span> <span data-ttu-id="16688-132">不過，您無法加入新的使用者和現有的使用者之前，無法更新其設定 hello 主機已上線，或取得升級部屬。</span><span class="sxs-lookup"><span data-stu-id="16688-132">However, you can't add new users and existing users can't update their settings until hello master is back online or a subordinate gets promoted.</span></span>

### <a name="prepare-your-environment"></a><span data-ttu-id="16688-133">準備您的環境</span><span class="sxs-lookup"><span data-stu-id="16688-133">Prepare your environment</span></span>

<span data-ttu-id="16688-134">請確定您使用 Azure Multi-factor authentication 的 hello 伺服器符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="16688-134">Make sure hello server  that you're using for Azure Multi-Factor Authentication meets hello following requirements:</span></span>

| <span data-ttu-id="16688-135">Azure Multi-Factor Authentication Server 需求</span><span class="sxs-lookup"><span data-stu-id="16688-135">Azure Multi-Factor Authentication Server Requirements</span></span> | <span data-ttu-id="16688-136">說明</span><span class="sxs-lookup"><span data-stu-id="16688-136">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="16688-137">硬體</span><span class="sxs-lookup"><span data-stu-id="16688-137">Hardware</span></span> |<li><span data-ttu-id="16688-138">200 MB 的硬碟空間</span><span class="sxs-lookup"><span data-stu-id="16688-138">200 MB of hard disk space</span></span></li><li><span data-ttu-id="16688-139">具有 x32 或 x64 功能的處理器</span><span class="sxs-lookup"><span data-stu-id="16688-139">x32 or x64 capable processor</span></span></li><li><span data-ttu-id="16688-140">1 GB 或更高的 RAM</span><span class="sxs-lookup"><span data-stu-id="16688-140">1 GB or greater RAM</span></span></li> |
| <span data-ttu-id="16688-141">軟體</span><span class="sxs-lookup"><span data-stu-id="16688-141">Software</span></span> |<li><span data-ttu-id="16688-142">Windows Server 2008 或更新版本，如果 hello 主機伺服器 OS</span><span class="sxs-lookup"><span data-stu-id="16688-142">Windows Server 2008 or greater if hello host is a server OS</span></span></li><li><span data-ttu-id="16688-143">Windows 7 或更新版本，如果 hello 主機作業系統的用戶端</span><span class="sxs-lookup"><span data-stu-id="16688-143">Windows 7 or greater if hello host is a client OS</span></span></li><li><span data-ttu-id="16688-144">Microsoft .NET 4.0 Framework</span><span class="sxs-lookup"><span data-stu-id="16688-144">Microsoft .NET 4.0 Framework</span></span></li><li><span data-ttu-id="16688-145">IIS 7.0 或更新版本，如果安裝 hello 使用者入口網站或 web 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="16688-145">IIS 7.0 or greater if installing hello user portal or web service SDK</span></span></li> |

### <a name="azure-mfa-server-components"></a><span data-ttu-id="16688-146">Azure MFA Server 元件</span><span class="sxs-lookup"><span data-stu-id="16688-146">Azure MFA Server Components</span></span>

<span data-ttu-id="16688-147">構成 Azure MFA Server 的 Web 元件有三個：</span><span class="sxs-lookup"><span data-stu-id="16688-147">There are three web components that make up Azure MFA Server:</span></span>

* <span data-ttu-id="16688-148">Web 服務 SDK 層啟用與通訊 hello 其他元件和 hello Azure MFA 應用程式伺服器上已安裝</span><span class="sxs-lookup"><span data-stu-id="16688-148">Web Service SDK - Enables communication with hello other components and is installed on hello Azure MFA application server</span></span>
* <span data-ttu-id="16688-149">使用者入口網站的 IIS 網站，允許使用者 tooenroll Azure Multi-factor Authentication (MFA)，並維護自己的帳戶。</span><span class="sxs-lookup"><span data-stu-id="16688-149">User Portal - An IIS web site that allows users tooenroll in Azure Multi-Factor Authentication (MFA) and maintain their accounts.</span></span>
* <span data-ttu-id="16688-150">行動應用程式 Web 服務-可讓您使用行動裝置的應用程式，例如 hello Microsoft 驗證器應用程式進行兩步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="16688-150">Mobile App Web Service - Enables using a mobile app like hello Microsoft Authenticator app for two-step verification.</span></span>

<span data-ttu-id="16688-151">所有的三個元件可以安裝在 hello hello 伺服器是否為網際網路對向的同一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="16688-151">All three components can be installed on hello same server if hello server is internet-facing.</span></span> <span data-ttu-id="16688-152">如果分解成 hello 元件，hello Azure MFA 應用程式伺服器上安裝 hello Web 服務 SDK 和 hello 使用者入口網站和行動裝置應用程式 Web 服務安裝在網際網路對向伺服器。</span><span class="sxs-lookup"><span data-stu-id="16688-152">If breaking up hello components, hello Web Service SDK is installed on hello Azure MFA application server and hello User Portal and Mobile App Web Service are installed on an internet-facing server.</span></span>

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a><span data-ttu-id="16688-153">Azure Multi-Factor Authentication Server 防火牆需求</span><span class="sxs-lookup"><span data-stu-id="16688-153">Azure Multi-Factor Authentication Server firewall requirements</span></span>

<span data-ttu-id="16688-154">每個 MFA 伺服器必須可以在下列位址的連接埠 443 輸出 toohello toocommunicate:</span><span class="sxs-lookup"><span data-stu-id="16688-154">Each MFA server must be able toocommunicate on port 443 outbound toohello following addresses:</span></span>

* <span data-ttu-id="16688-155">https://pfd.phonefactor.net</span><span class="sxs-lookup"><span data-stu-id="16688-155">https://pfd.phonefactor.net</span></span>
* <span data-ttu-id="16688-156">https://pfd2.phonefactor.net</span><span class="sxs-lookup"><span data-stu-id="16688-156">https://pfd2.phonefactor.net</span></span>
* <span data-ttu-id="16688-157">https://css.phonefactor.net</span><span class="sxs-lookup"><span data-stu-id="16688-157">https://css.phonefactor.net</span></span>

<span data-ttu-id="16688-158">如果連外防火牆連接埠 443 上受限，開啟下列的 IP 位址範圍的 hello:</span><span class="sxs-lookup"><span data-stu-id="16688-158">If outbound firewalls are restricted on port 443, open hello following IP address ranges:</span></span>

| <span data-ttu-id="16688-159">IP 子網路</span><span class="sxs-lookup"><span data-stu-id="16688-159">IP Subnet</span></span> | <span data-ttu-id="16688-160">網路遮罩</span><span class="sxs-lookup"><span data-stu-id="16688-160">Netmask</span></span> | <span data-ttu-id="16688-161">IP 範圍</span><span class="sxs-lookup"><span data-stu-id="16688-161">IP Range</span></span> |
|:---: |:---: |:---: |
| <span data-ttu-id="16688-162">134.170.116.0/25</span><span class="sxs-lookup"><span data-stu-id="16688-162">134.170.116.0/25</span></span> |<span data-ttu-id="16688-163">255.255.255.128</span><span class="sxs-lookup"><span data-stu-id="16688-163">255.255.255.128</span></span> |<span data-ttu-id="16688-164">134.170.116.1 – 134.170.116.126</span><span class="sxs-lookup"><span data-stu-id="16688-164">134.170.116.1 – 134.170.116.126</span></span> |
| <span data-ttu-id="16688-165">134.170.165.0/25</span><span class="sxs-lookup"><span data-stu-id="16688-165">134.170.165.0/25</span></span> |<span data-ttu-id="16688-166">255.255.255.128</span><span class="sxs-lookup"><span data-stu-id="16688-166">255.255.255.128</span></span> |<span data-ttu-id="16688-167">134.170.165.1 – 134.170.165.126</span><span class="sxs-lookup"><span data-stu-id="16688-167">134.170.165.1 – 134.170.165.126</span></span> |
| <span data-ttu-id="16688-168">70.37.154.128/25</span><span class="sxs-lookup"><span data-stu-id="16688-168">70.37.154.128/25</span></span> |<span data-ttu-id="16688-169">255.255.255.128</span><span class="sxs-lookup"><span data-stu-id="16688-169">255.255.255.128</span></span> |<span data-ttu-id="16688-170">70.37.154.129 – 70.37.154.254</span><span class="sxs-lookup"><span data-stu-id="16688-170">70.37.154.129 – 70.37.154.254</span></span> |

<span data-ttu-id="16688-171">如果您不使用 hello 事件確認功能，而且您的使用者不使用從裝置的行動裝置應用程式 tooverify hello 公司網路上，您只需要下列範圍的 hello:</span><span class="sxs-lookup"><span data-stu-id="16688-171">If you aren't using hello Event Confirmation feature, and your users aren't using mobile apps tooverify from devices on hello corporate network, you only need hello following ranges:</span></span>

| <span data-ttu-id="16688-172">IP 子網路</span><span class="sxs-lookup"><span data-stu-id="16688-172">IP Subnet</span></span> | <span data-ttu-id="16688-173">網路遮罩</span><span class="sxs-lookup"><span data-stu-id="16688-173">Netmask</span></span> | <span data-ttu-id="16688-174">IP 範圍</span><span class="sxs-lookup"><span data-stu-id="16688-174">IP Range</span></span> |
|:---: |:---: |:---: |
| <span data-ttu-id="16688-175">134.170.116.72/29</span><span class="sxs-lookup"><span data-stu-id="16688-175">134.170.116.72/29</span></span> |<span data-ttu-id="16688-176">255.255.255.248</span><span class="sxs-lookup"><span data-stu-id="16688-176">255.255.255.248</span></span> |<span data-ttu-id="16688-177">134.170.116.72 – 134.170.116.79</span><span class="sxs-lookup"><span data-stu-id="16688-177">134.170.116.72 – 134.170.116.79</span></span> |
| <span data-ttu-id="16688-178">134.170.165.72/29</span><span class="sxs-lookup"><span data-stu-id="16688-178">134.170.165.72/29</span></span> |<span data-ttu-id="16688-179">255.255.255.248</span><span class="sxs-lookup"><span data-stu-id="16688-179">255.255.255.248</span></span> |<span data-ttu-id="16688-180">134.170.165.72 – 134.170.165.79</span><span class="sxs-lookup"><span data-stu-id="16688-180">134.170.165.72 – 134.170.165.79</span></span> |
| <span data-ttu-id="16688-181">70.37.154.200/29</span><span class="sxs-lookup"><span data-stu-id="16688-181">70.37.154.200/29</span></span> |<span data-ttu-id="16688-182">255.255.255.248</span><span class="sxs-lookup"><span data-stu-id="16688-182">255.255.255.248</span></span> |<span data-ttu-id="16688-183">70.37.154.201 – 70.37.154.206</span><span class="sxs-lookup"><span data-stu-id="16688-183">70.37.154.201 – 70.37.154.206</span></span> |

## <a name="download-hello-azure-multi-factor-authentication-server"></a><span data-ttu-id="16688-184">下載 Azure Multi-factor Authentication Server hello</span><span class="sxs-lookup"><span data-stu-id="16688-184">Download hello Azure Multi-Factor Authentication Server</span></span>

1. <span data-ttu-id="16688-185">登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="16688-185">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="16688-186">Hello 左側選取**Active Directory**</span><span class="sxs-lookup"><span data-stu-id="16688-186">On hello left, select **Active Directory**</span></span>
3. <span data-ttu-id="16688-187">按一下 [使用者和群組]</span><span class="sxs-lookup"><span data-stu-id="16688-187">Click **Users and groups**</span></span>
4. <span data-ttu-id="16688-188">按一下 [所有使用者]</span><span class="sxs-lookup"><span data-stu-id="16688-188">Click **All users**</span></span>
5. <span data-ttu-id="16688-189">按一下 [Multi-Factor Authentication]</span><span class="sxs-lookup"><span data-stu-id="16688-189">Click **Multi-Factor Authentication**</span></span>
6. <span data-ttu-id="16688-190">在 [多重要素驗證] 區域之下，選取 [服務設定]</span><span class="sxs-lookup"><span data-stu-id="16688-190">Under **multi-factor authentication** section, select **service settings**</span></span>

   ![服務設定頁面](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. <span data-ttu-id="16688-192">在 hello 服務設定 頁面上，在 hello 囉 」 畫面底部按一下**Go toohello 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="16688-192">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="16688-193">新的頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="16688-193">A new page opens.</span></span>
7. <span data-ttu-id="16688-194">按一下 [下載]。</span><span class="sxs-lookup"><span data-stu-id="16688-194">Click **Downloads**.</span></span>
8. <span data-ttu-id="16688-195">按一下 hello**下載**連結，並儲存 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="16688-195">Click hello **Download** link and save hello installer.</span></span>

   ![下載 MFA Server](./media/multi-factor-authentication-get-started-server/download4.png)

9. <span data-ttu-id="16688-197">保留此頁面開啟，因為我們將 tooit 之後執行 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="16688-197">Keep this page open as we will refer tooit after running hello installer.</span></span>

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a><span data-ttu-id="16688-198">安裝及設定 Azure Multi-factor Authentication Server hello</span><span class="sxs-lookup"><span data-stu-id="16688-198">Install and configure hello Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="16688-199">既然您已經下載 hello 伺服器，您可以安裝並設定它。</span><span class="sxs-lookup"><span data-stu-id="16688-199">Now that you have downloaded hello server you can install and configure it.</span></span> <span data-ttu-id="16688-200">請確定您安裝在該 hello 伺服器符合 hello 規劃 > 一節中所列的需求。</span><span class="sxs-lookup"><span data-stu-id="16688-200">Be sure that hello server you are installing it on meets requirements listed in hello planning section.</span></span>

1. <span data-ttu-id="16688-201">按兩下 hello 可執行檔。</span><span class="sxs-lookup"><span data-stu-id="16688-201">Double-click hello executable.</span></span>
2. <span data-ttu-id="16688-202">在 [hello 選取安裝資料夾] 畫面上，請確定該 hello 資料夾是否正確，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="16688-202">On hello Select Installation Folder screen, make sure that hello folder is correct and click **Next**.</span></span>
3. <span data-ttu-id="16688-203">Hello 安裝完成之後，請按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="16688-203">Once hello installation is complete, click **Finish**.</span></span>  <span data-ttu-id="16688-204">hello 組態精靈 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="16688-204">hello configuration wizard launches.</span></span>
4. <span data-ttu-id="16688-205">在 [hello 組態精靈歡迎畫面中，核取**略過使用 hello 驗證設定精靈**按一下**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="16688-205">On hello configuration wizard welcome screen, check **Skip using hello Authentication Configuration Wizard** and click **Next**.</span></span>  <span data-ttu-id="16688-206">hello 精靈關閉並 hello 伺服器開始。</span><span class="sxs-lookup"><span data-stu-id="16688-206">hello wizard closes and hello server starts.</span></span>

   ![雲端](./media/multi-factor-authentication-get-started-server/skip2.png)

5. <span data-ttu-id="16688-208">回到上我們下載 hello 伺服器 hello 頁面上，按一下 [hello**產生啟用認證**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="16688-208">Back on hello page that we downloaded hello server from, click hello **Generate Activation Credentials** button.</span></span> <span data-ttu-id="16688-209">提供，這項資訊複製到 hello Azure MFA Server hello 方塊中，然後按一下**Activate**。</span><span class="sxs-lookup"><span data-stu-id="16688-209">Copy this information into hello Azure MFA Server in hello boxes provided and click **Activate**.</span></span>

## <a name="send-users-an-email"></a><span data-ttu-id="16688-210">傳送電子郵件給使用者</span><span class="sxs-lookup"><span data-stu-id="16688-210">Send users an email</span></span>

<span data-ttu-id="16688-211">tooease 首度發行、 允許 MFA Server toocommunicate 與您的使用者。</span><span class="sxs-lookup"><span data-stu-id="16688-211">tooease rollout, allow MFA Server toocommunicate with your users.</span></span> <span data-ttu-id="16688-212">MFA Server 可以傳送電子郵件 tooinform 它們，它們已註冊的雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="16688-212">MFA Server can send an email tooinform them that they have been enrolled for two-step verification.</span></span>

<span data-ttu-id="16688-213">您傳送嗨電子郵件應該取決您將進行兩步驟驗證使用者的設定。</span><span class="sxs-lookup"><span data-stu-id="16688-213">hello email you send should be determined by how you configure your users for two-step verification.</span></span> <span data-ttu-id="16688-214">例如，如果您不能 tooimport hello 公司目錄中的電話號碼，hello 電子郵件應該包含 hello 預設電話號碼，讓使用者知道哪些 tooexpect。</span><span class="sxs-lookup"><span data-stu-id="16688-214">For example, if you are able tooimport phone numbers from hello company directory, hello email should include hello default phone numbers so that users know what tooexpect.</span></span> <span data-ttu-id="16688-215">如果您無法匯入電話號碼，或您的使用者將 toouse hello 行動裝置應用程式，將它們傳送電子郵件，其中會將他們導向 toocomplete 帳戶註冊。</span><span class="sxs-lookup"><span data-stu-id="16688-215">If you do not import phone numbers, or your users are going toouse hello mobile app, send them an email that directs them toocomplete their account enrollment.</span></span> <span data-ttu-id="16688-216">Hello 電子郵件中包含超連結 toohello Azure Multi-factor Authentication 使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="16688-216">Include a hyperlink toohello Azure Multi-Factor Authentication User Portal in hello email.</span></span>

<span data-ttu-id="16688-217">hello 電子郵件的 hello 內容也有所不同 hello hello 使用者 （通話、 簡訊或行動裝置應用程式） 已設定的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="16688-217">hello content of hello email also varies depending on hello method of verification that has been set for hello user (phone call, SMS, or mobile app).</span></span>  <span data-ttu-id="16688-218">比方說，如果 hello 使用者需要的 toouse PIN 驗證時，hello 電子郵件通知他們什麼他們初始 PIN 已設定為。</span><span class="sxs-lookup"><span data-stu-id="16688-218">For example, if hello user is required toouse a PIN when they authenticate, hello email tells them what their initial PIN has been set to.</span></span>  <span data-ttu-id="16688-219">使用者在其第一個驗證期間會需要的 toochange 他們的 pin 碼。</span><span class="sxs-lookup"><span data-stu-id="16688-219">Users are required toochange their PIN during their first verification.</span></span>

### <a name="configure-email-and-email-templates"></a><span data-ttu-id="16688-220">設定電子郵件和電子郵件範本</span><span class="sxs-lookup"><span data-stu-id="16688-220">Configure email and email templates</span></span>

<span data-ttu-id="16688-221">針對傳送這些電子郵件中按一下 hello 電子郵件圖示 hello 左 tooset hello 的設定。</span><span class="sxs-lookup"><span data-stu-id="16688-221">Click hello email icon on hello left tooset up hello settings for sending these emails.</span></span> <span data-ttu-id="16688-222">此頁面是您可以在其中輸入藉由檢查 hello hello SMTP 郵件伺服器和傳送電子郵件資訊**傳送電子郵件寄給 toousers**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="16688-222">This page is where you can enter hello SMTP information of your mail server and send email by checking hello **Send emails toousers** check box.</span></span>

![MFA Server 電子郵件組態](./media/multi-factor-authentication-get-started-server/email1.png)

<span data-ttu-id="16688-224">Hello 電子郵件內容索引標籤上，您可以看到從可用 toochoose 的 hello 電子郵件範本。</span><span class="sxs-lookup"><span data-stu-id="16688-224">On hello Email Content tab, you can see hello email templates that are available toochoose from.</span></span> <span data-ttu-id="16688-225">根據您如何設定您的使用者 tooperform 雙步驟驗證，選擇最適合您的 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="16688-225">Depending on how you have configured your users tooperform two-step verification, choose hello template that best suits you.</span></span>

![MFA Server 電子郵件範本](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a><span data-ttu-id="16688-227">從 Active Directory 匯入使用者</span><span class="sxs-lookup"><span data-stu-id="16688-227">Import users from Active Directory</span></span>

<span data-ttu-id="16688-228">現在該 hello 伺服器已安裝，您會想 tooadd 使用者。</span><span class="sxs-lookup"><span data-stu-id="16688-228">Now that hello server is installed you will want tooadd users.</span></span> <span data-ttu-id="16688-229">您可以選擇 toocreate 它們，手動從 Active Directory 中，匯入使用者，或設定自動同步處理與 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="16688-229">You can choose toocreate them manually, import users from Active Directory, or configure automated synchronization with Active Directory.</span></span>

### <a name="manual-import-from-active-directory"></a><span data-ttu-id="16688-230">從 Active Directory 手動匯入</span><span class="sxs-lookup"><span data-stu-id="16688-230">Manual import from Active Directory</span></span>

1. <span data-ttu-id="16688-231">在 hello 左側 hello Azure MFA Server 中，選取 **使用者**。</span><span class="sxs-lookup"><span data-stu-id="16688-231">In hello Azure MFA Server, on hello left, select **Users**.</span></span>
2. <span data-ttu-id="16688-232">在 hello 下方，選取**從 Active Directory 匯入**。</span><span class="sxs-lookup"><span data-stu-id="16688-232">At hello bottom, select **Import from Active Directory**.</span></span>
3. <span data-ttu-id="16688-233">現在您可以搜尋個別使用者或搜尋 hello AD 目錄的 Ou 與它們的使用者。</span><span class="sxs-lookup"><span data-stu-id="16688-233">Now you can either search for individual users or search hello AD directory for OUs with users in them.</span></span>  <span data-ttu-id="16688-234">在此情況下，我們指定 hello 使用者 OU。</span><span class="sxs-lookup"><span data-stu-id="16688-234">In this case, we specify hello users OU.</span></span>
4. <span data-ttu-id="16688-235">反白顯示右 hello 上的所有 hello 使用者，然後按一下 **匯入**。</span><span class="sxs-lookup"><span data-stu-id="16688-235">Highlight all hello users on hello right and click **Import**.</span></span>  <span data-ttu-id="16688-236">您應該會看到指出成功完成作業的快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="16688-236">You should receive a pop-up telling you that you were successful.</span></span>  <span data-ttu-id="16688-237">關閉 hello 匯入 視窗。</span><span class="sxs-lookup"><span data-stu-id="16688-237">Close hello import window.</span></span>

   ![MFA Server 使用者匯入](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a><span data-ttu-id="16688-239">自動與 Active Directory 同步處理</span><span class="sxs-lookup"><span data-stu-id="16688-239">Automated synchronization with Active Directory</span></span>

1. <span data-ttu-id="16688-240">在 hello 左側 hello Azure MFA Server 中，選取 **目錄整合**。</span><span class="sxs-lookup"><span data-stu-id="16688-240">In hello Azure MFA Server, on hello left, select **Directory Integration**.</span></span>
2. <span data-ttu-id="16688-241">瀏覽 toohello**同步** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="16688-241">Navigate toohello **Synchronization** tab.</span></span>
3. <span data-ttu-id="16688-242">Hello 底部，選擇 **新增**</span><span class="sxs-lookup"><span data-stu-id="16688-242">At hello bottom, choose **Add**</span></span>
4. <span data-ttu-id="16688-243">在 hello**加入同步處理項目**出現方塊選擇 hello 網域、 OU**或**安全性群組、 設定、 預設值的方法，以及語言的預設值為這個同步處理工作，並按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="16688-243">In hello **Add Synchronization Item** box that appears choose hello Domain, OU **or** security group, Settings, Method Defaults, and Language Defaults for this synchronization task and click **Add**.</span></span>
5. <span data-ttu-id="16688-244">標示的核取 hello 方塊**啟用與 Active Directory 同步處理**選擇**同步處理間隔**一分鐘到 24 小時之間。</span><span class="sxs-lookup"><span data-stu-id="16688-244">Check hello box labeled **Enable synchronization with Active Directory** and choose a **Synchronization interval** between one minute and 24 hours.</span></span>

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a><span data-ttu-id="16688-245">Hello Azure Multi-factor Authentication Server 如何處理使用者資料</span><span class="sxs-lookup"><span data-stu-id="16688-245">How hello Azure Multi-Factor Authentication Server handles user data</span></span>

<span data-ttu-id="16688-246">當您使用 hello Multi-factor Authentication (MFA) Server 內部部署時，使用者的資料會儲存在 hello 在內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="16688-246">When you use hello Multi-Factor Authentication (MFA) Server on-premises, a user’s data is stored in hello on-premises servers.</span></span> <span data-ttu-id="16688-247">Hello 雲端中不儲存任何持續性的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="16688-247">No persistent user data is stored in hello cloud.</span></span> <span data-ttu-id="16688-248">當 hello 使用者執行雙步驟驗證時，hello MFA Server 會傳送資料 toohello Azure MFA 雲端服務 tooperform hello 驗證。</span><span class="sxs-lookup"><span data-stu-id="16688-248">When hello user performs a two-step verification, hello MFA Server sends data toohello Azure MFA cloud service tooperform hello verification.</span></span> <span data-ttu-id="16688-249">當這些驗證要求傳送 toohello 雲端服務時，hello 下列欄位會傳送 hello 要求及記錄檔中，如此會出現在 hello 客戶的驗證及使用報表。</span><span class="sxs-lookup"><span data-stu-id="16688-249">When these authentication requests are sent toohello cloud service, hello following fields are sent in hello request and logs so that they are available in hello customer's authentication/usage reports.</span></span> <span data-ttu-id="16688-250">有些 hello 欄位是選擇性的因此可以啟用或停用 hello Multi-factor Authentication Server 內。</span><span class="sxs-lookup"><span data-stu-id="16688-250">Some of hello fields are optional so they can be enabled or disabled within hello Multi-Factor Authentication Server.</span></span> <span data-ttu-id="16688-251">來自 hello MFA Server toohello MFA 雲端服務的 hello 通訊會透過連接埠 443 輸出使用 SSL/TLS。</span><span class="sxs-lookup"><span data-stu-id="16688-251">hello communication from hello MFA Server toohello MFA cloud service uses SSL/TLS over port 443 outbound.</span></span> <span data-ttu-id="16688-252">這些欄位包括：</span><span class="sxs-lookup"><span data-stu-id="16688-252">These fields are:</span></span>

* <span data-ttu-id="16688-253">唯一識別碼 - 使用者名稱或內部的 MFA 伺服器識別碼</span><span class="sxs-lookup"><span data-stu-id="16688-253">Unique ID - either username or internal MFA server ID</span></span>
* <span data-ttu-id="16688-254">名字和姓氏 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="16688-254">First and last name (optional)</span></span>
* <span data-ttu-id="16688-255">電子郵件地址 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="16688-255">Email address (optional)</span></span>
* <span data-ttu-id="16688-256">電話號碼 - 進行語音通話或簡訊驗證時</span><span class="sxs-lookup"><span data-stu-id="16688-256">Phone number - when doing a voice call or SMS authentication</span></span>
* <span data-ttu-id="16688-257">安全性權杖 - 執行行動應用程式驗證時</span><span class="sxs-lookup"><span data-stu-id="16688-257">Device token - when doing mobile app authentication</span></span>
* <span data-ttu-id="16688-258">驗證模式</span><span class="sxs-lookup"><span data-stu-id="16688-258">Authentication mode</span></span>
* <span data-ttu-id="16688-259">驗證結果</span><span class="sxs-lookup"><span data-stu-id="16688-259">Authentication result</span></span>
* <span data-ttu-id="16688-260">MFA Server 名稱</span><span class="sxs-lookup"><span data-stu-id="16688-260">MFA Server name</span></span>
* <span data-ttu-id="16688-261">MFA Server IP</span><span class="sxs-lookup"><span data-stu-id="16688-261">MFA Server IP</span></span>
* <span data-ttu-id="16688-262">用戶端 IP – 如果有的話</span><span class="sxs-lookup"><span data-stu-id="16688-262">Client IP – if available</span></span>

<span data-ttu-id="16688-263">此外 toohello 上述欄位，hello 驗證結果 （成功/拒絕） 和任何被拒絕的原因也是儲存與 hello 驗證資料，而且可透過 hello 驗證及使用報表。</span><span class="sxs-lookup"><span data-stu-id="16688-263">In addition toohello fields above, hello verification result (success/denial) and reason for any denials is also stored with hello authentication data and available through hello authentication/usage reports.</span></span>

## <a name="back-up-and-restore-azure-mfa-server"></a><span data-ttu-id="16688-264">備份和還原 Azure MFA Server</span><span class="sxs-lookup"><span data-stu-id="16688-264">Back up and restore Azure MFA Server</span></span>

<span data-ttu-id="16688-265">確定您具有正確的備份是使用任何系統的重要步驟 tootake。</span><span class="sxs-lookup"><span data-stu-id="16688-265">Making sure that you have a good backup is an important step tootake with any system.</span></span>

<span data-ttu-id="16688-266">tooback Azure MFA server，確定您有一份 hello **C:\Program files\multi-factor Authentication 驗證 Server\Data**資料夾包括 hello **PhoneFactor.pfdata**檔案。</span><span class="sxs-lookup"><span data-stu-id="16688-266">tooback up Azure MFA Server, ensure that you have a copy of hello **C:\Program Files\Multi-Factor Authentication Server\Data** folder including hello **PhoneFactor.pfdata** file.</span></span> 

<span data-ttu-id="16688-267">在還原的情況下會需要完整的 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="16688-267">In case a restore is needed complete hello following steps:</span></span>

1. <span data-ttu-id="16688-268">在新的伺服器上重新安裝 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="16688-268">Reinstall Azure MFA Server on a new server.</span></span>
2. <span data-ttu-id="16688-269">啟動 hello 新的 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="16688-269">Activate hello new Azure MFA Server.</span></span>
3. <span data-ttu-id="16688-270">停止 hello **MultiFactorAuth**服務。</span><span class="sxs-lookup"><span data-stu-id="16688-270">Stop hello **MultiFactorAuth** service.</span></span>
4. <span data-ttu-id="16688-271">覆寫 hello **PhoneFactor.pfdata**以 hello 備份複本。</span><span class="sxs-lookup"><span data-stu-id="16688-271">Overwrite hello **PhoneFactor.pfdata** with hello backed up copy.</span></span>
5. <span data-ttu-id="16688-272">啟動 hello **MultiFactorAuth**服務。</span><span class="sxs-lookup"><span data-stu-id="16688-272">Start hello **MultiFactorAuth** service.</span></span>

<span data-ttu-id="16688-273">hello 新的伺服器現在會啟動並執行與 hello 原始備份組態和使用者資料。</span><span class="sxs-lookup"><span data-stu-id="16688-273">hello new server is now up and running with hello original backed-up configuration and user data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16688-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16688-274">Next steps</span></span>

- <span data-ttu-id="16688-275">安裝和設定 hello[使用者入口網站](multi-factor-authentication-get-started-portal.md)自助使用者。</span><span class="sxs-lookup"><span data-stu-id="16688-275">Set up and configure hello [User Portal](multi-factor-authentication-get-started-portal.md) for user self-service.</span></span>
- <span data-ttu-id="16688-276">安裝和設定 hello 與 Azure MFA Server [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md)， [RADIUS 驗證](multi-factor-authentication-get-started-server-radius.md)，或[LDAP 驗證](multi-factor-authentication-get-started-server-ldap.md)。</span><span class="sxs-lookup"><span data-stu-id="16688-276">Set up and configure hello Azure MFA Server with [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md), [RADIUS Authentication](multi-factor-authentication-get-started-server-radius.md), or [LDAP Authentication](multi-factor-authentication-get-started-server-ldap.md).</span></span>
- <span data-ttu-id="16688-277">安裝和設定[使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server-rdg.md)。</span><span class="sxs-lookup"><span data-stu-id="16688-277">Set up and configure [Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS](multi-factor-authentication-get-started-server-rdg.md).</span></span>
- <span data-ttu-id="16688-278">[部署 Azure Multi-factor Authentication 伺服器行動應用程式 Web 服務的 hello](multi-factor-authentication-get-started-server-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="16688-278">[Deploy hello Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).</span></span>
- <span data-ttu-id="16688-279">[使用 Azure Multi-Factor Authentication 與協力廠商 VPN 的進階案例](multi-factor-authentication-advanced-vpn-configurations.md)。</span><span class="sxs-lookup"><span data-stu-id="16688-279">[Advanced scenarios with Azure Multi-Factor Authentication and third-party VPNs](multi-factor-authentication-advanced-vpn-configurations.md).</span></span>
