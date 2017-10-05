---
title: "安裝應用程式 Proxy 代理程式連接器時遇到問題 | Microsoft Docs"
description: "如何針對在安裝應用程式 Proxy 代理程式連接器時可能遇到的問題進行疑難排解"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 91b3f6f3c8339647f568a509e9efd8e1fffb13dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a><span data-ttu-id="15c75-103">安裝應用程式 Proxy 代理程式連接器時遇到問題</span><span class="sxs-lookup"><span data-stu-id="15c75-103">Problem installing the Application Proxy Agent Connector</span></span>

<span data-ttu-id="15c75-104">Microsoft AAD 應用程式 Proxy 連接器是內部網域元件，它會使用輸出連線來建立雲端可用端點至內部網域的連線。</span><span class="sxs-lookup"><span data-stu-id="15c75-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="15c75-105">連接器安裝的一般問題區域</span><span class="sxs-lookup"><span data-stu-id="15c75-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="15c75-106">連接器安裝失敗時，根本原因通常是下列其中一個區域：</span><span class="sxs-lookup"><span data-stu-id="15c75-106">When the installation of a connector fails, the root cause is usually one of the following areas:</span></span>

1.  <span data-ttu-id="15c75-107">**連線**：若要成功完成安裝，新的連接器必須註冊並建立未來信任內容。</span><span class="sxs-lookup"><span data-stu-id="15c75-107">**Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties.</span></span> <span data-ttu-id="15c75-108">這是透過連線至 AAD 應用程式 Proxy 雲端服務來完成。</span><span class="sxs-lookup"><span data-stu-id="15c75-108">This is done by connecting to the AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="15c75-109">**信任建立**：新的連接器會建立自我簽署憑證，並向雲端服務註冊。</span><span class="sxs-lookup"><span data-stu-id="15c75-109">**Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.</span></span>

3.  <span data-ttu-id="15c75-110">**系統管理員的驗證**：在安裝期間，使用者必須提供系統管理員認證才能完成連接器安裝。</span><span class="sxs-lookup"><span data-stu-id="15c75-110">**Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.</span></span>

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="15c75-111">確認與雲端應用程式 Proxy 服務和 Microsoft 登入頁面之間連線</span><span class="sxs-lookup"><span data-stu-id="15c75-111">Verify connectivity to the Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="15c75-112">**目標：**確認連接器電腦可以連線到 AAD 應用程式 Proxy 註冊端點以及 Microsoft 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="15c75-112">**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="15c75-113">開啟瀏覽器並移至下列網頁： <https://aadap-portcheck.connectorporttest.msappproxy.net> (英文)，確認透過連接埠 9090 和 9091 與美國中部 (Central US) 與美國東部 (East US) 資料中心的連線是正常的。</span><span class="sxs-lookup"><span data-stu-id="15c75-113">Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="15c75-114">如果有任何連接埠未成功 (沒有綠色勾選記號)，請確認防火牆或後端 Proxy 是否已正確定義 \*.msappproxy.net 與連接埠 9090 和 9091。</span><span class="sxs-lookup"><span data-stu-id="15c75-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="15c75-115">開啟瀏覽器 (其他索引標籤)，並移至下列網頁：<https://login.microsoftonline.com>，確定您可以登入該頁面。</span><span class="sxs-lookup"><span data-stu-id="15c75-115">Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="15c75-116">確認電腦和後端元件支援應用程式 Prxoy 信任憑證</span><span class="sxs-lookup"><span data-stu-id="15c75-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="15c75-117">**目標︰**確認連接器電腦、後端 Proxy 和防火牆可支援由連接器針對未來信任所建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="15c75-117">**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="15c75-118">連接器會嘗試建立由 TLS1.2 所支援的 SHA512 憑證。</span><span class="sxs-lookup"><span data-stu-id="15c75-118">The connector tries to create a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="15c75-119">如果電腦或後端防火牆及 Proxy 不支援 TLS1.2，則安裝會失敗。</span><span class="sxs-lookup"><span data-stu-id="15c75-119">If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.</span></span>
>
>

<span data-ttu-id="15c75-120">**解決此問題：**</span><span class="sxs-lookup"><span data-stu-id="15c75-120">**To resolve the issue:**</span></span>

1.  <span data-ttu-id="15c75-121">確認電腦支援 TLS1.2：2012 R2 之後的所有 Windows 版本都應該支援 TLS 1.2。</span><span class="sxs-lookup"><span data-stu-id="15c75-121">Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="15c75-122">如果您的連接器電腦是 2012 R2 或更舊版本，請確定電腦已安裝下列 KB：<https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="15c75-122">If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="15c75-123">連絡您的網路系統管理員，並要求確認後端 Proxy 和防火牆不會針對連出流量封鎖 SHA512。</span><span class="sxs-lookup"><span data-stu-id="15c75-123">Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-to-install-the-connector"></a><span data-ttu-id="15c75-124">確認是以系統管理員身分安裝連接器</span><span class="sxs-lookup"><span data-stu-id="15c75-124">Verify admin is used to install the connector</span></span>

<span data-ttu-id="15c75-125">**目標︰**確認嘗試安裝連接器的使用者是具有正確認證的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="15c75-125">**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials.</span></span> <span data-ttu-id="15c75-126">目前使用者必須是全域管理員，安裝才會成功。</span><span class="sxs-lookup"><span data-stu-id="15c75-126">Currently, the user must be a global administrator for the installation to succeed.</span></span>

<span data-ttu-id="15c75-127">**確認認證是否正確：**</span><span class="sxs-lookup"><span data-stu-id="15c75-127">**To verify the credentials are correct:**</span></span>

<span data-ttu-id="15c75-128">連線到 <https://login.microsoftonline.com> 並使用相同的認證。</span><span class="sxs-lookup"><span data-stu-id="15c75-128">Connect to <https://login.microsoftonline.com> and use the same credentials.</span></span> <span data-ttu-id="15c75-129">確定登入成功。</span><span class="sxs-lookup"><span data-stu-id="15c75-129">Make sure the login is successful.</span></span> <span data-ttu-id="15c75-130">您可以檢查使用者角色，方法是移至 [Azure Active Directory] -&gt; [使用者和群組] -&gt; [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="15c75-130">You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="15c75-131">選取您的使用者帳戶，然後在產生的功能表中選取 [目錄角色]。</span><span class="sxs-lookup"><span data-stu-id="15c75-131">Select your user account, then “Directory Role” in the resulting menu.</span></span> <span data-ttu-id="15c75-132">確認所選取的角色為 [全域管理員]。</span><span class="sxs-lookup"><span data-stu-id="15c75-132">Verify that the selected role is “Global administrator”.</span></span> <span data-ttu-id="15c75-133">如果您無法存取這些步驟上的任何頁面，您就不是全域管理員。</span><span class="sxs-lookup"><span data-stu-id="15c75-133">If you are unable to access any of the pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15c75-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15c75-134">Next steps</span></span>
[<span data-ttu-id="15c75-135">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="15c75-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
