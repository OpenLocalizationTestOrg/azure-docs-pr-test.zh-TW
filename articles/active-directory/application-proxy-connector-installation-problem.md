---
title: "安裝 aaaProblem hello 應用程式 Proxy 代理程式連接器 |Microsoft 文件"
description: "如何 tootroubleshoot 問題可能會安裝時的字體 hello 應用程式 Proxy 代理程式連接器"
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
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="93df0-103">安裝應用程式 Proxy 代理程式連接器 hello 的問題</span><span class="sxs-lookup"><span data-stu-id="93df0-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="93df0-104">Microsoft AAD 應用程式 Proxy 連接器是使用輸出連線 tooestablish hello 連線從 hello 雲端可用端點 toohello 內部網域的內部網域元件。</span><span class="sxs-lookup"><span data-stu-id="93df0-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="93df0-105">連接器安裝的一般問題區域</span><span class="sxs-lookup"><span data-stu-id="93df0-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="93df0-106">Hello 連接器安裝失敗時，hello 根本原因通常是一個 hello 下列區域：</span><span class="sxs-lookup"><span data-stu-id="93df0-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="93df0-107">**連線**– hello 新連接器需求 tooregister toocomplete 安裝成功，並建立未來的信任屬性。</span><span class="sxs-lookup"><span data-stu-id="93df0-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="93df0-108">這是藉由連接 toohello AAD 應用程式 Proxy 的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="93df0-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="93df0-109">**建立信任**– hello 新連接器建立自我簽署的憑證，並登錄 toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="93df0-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="93df0-110">**驗證的 hello admin** – 在安裝期間，hello 使用者必須提供系統管理員認證 toocomplete hello 連接器安裝。</span><span class="sxs-lookup"><span data-stu-id="93df0-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="93df0-111">請確認連接 toohello 雲端應用程式 Proxy 服務，且 Microsoft 登入頁面</span><span class="sxs-lookup"><span data-stu-id="93df0-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="93df0-112">**目標：**確認該 hello 連接器電腦可以連線 toohello AAD 應用程式 Proxy 註冊端點，以及 Microsoft 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="93df0-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="93df0-113">開啟下列網頁瀏覽器並前往 toohello: <https://aadap-portcheck.connectorporttest.msappproxy.net> ，確認該 hello 連線 tooCentral 美國和美國東部資料中心與連接埠 9090 和 9091 運作正常。</span><span class="sxs-lookup"><span data-stu-id="93df0-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="93df0-114">如果任何這些連接埠不成功 （沒有綠色的核取記號），請確認該 hello 防火牆或 proxy 後端有\*。 msappproxy.net 9090 和 9091 定義正確的連接埠。</span><span class="sxs-lookup"><span data-stu-id="93df0-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="93df0-115">開啟瀏覽器 （個別索引標籤），並移 toohello 下列網頁： <https://login.microsoftonline.com>，請確定您可以登入 toothat 頁面。</span><span class="sxs-lookup"><span data-stu-id="93df0-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="93df0-116">確認電腦和後端元件支援應用程式 Prxoy 信任憑證</span><span class="sxs-lookup"><span data-stu-id="93df0-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="93df0-117">**目標：**確認 hello 連接器的電腦、 後端 proxy 和防火牆，可以支援 hello 建立 hello 連接器未來的信任的憑證。</span><span class="sxs-lookup"><span data-stu-id="93df0-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="93df0-118">hello 連接器會嘗試 toocreate 受到 TLS1.2 SHA512 憑證。</span><span class="sxs-lookup"><span data-stu-id="93df0-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="93df0-119">如果機器 hello 或 hello 後端防火牆和 proxy 不支援 TLS1.2，hello 安裝失敗。</span><span class="sxs-lookup"><span data-stu-id="93df0-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="93df0-120">**tooresolve hello 問題：**</span><span class="sxs-lookup"><span data-stu-id="93df0-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="93df0-121">請確認 hello 電腦支援 TLS1.2 – 2012 R2 之後的所有 Windows 版本應該支援 TLS 1.2。</span><span class="sxs-lookup"><span data-stu-id="93df0-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="93df0-122">如果您連接器的電腦，從的 2012 R2 版本或之前，請確定該 hello hello 機器已安裝下列 Kb: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="93df0-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="93df0-123">連絡您的網路系統管理員並要求 tooverify 確定 hello 後端 proxy 和防火牆不會封鎖 SHA512 傳出流量。</span><span class="sxs-lookup"><span data-stu-id="93df0-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="93df0-124">確認系統管理員是使用的 tooinstall hello 連接器</span><span class="sxs-lookup"><span data-stu-id="93df0-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="93df0-125">**目標：**確認嘗試 tooinstall hello 連接器該 hello 使用者是系統管理員的正確認證。</span><span class="sxs-lookup"><span data-stu-id="93df0-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="93df0-126">目前，hello 使用者必須是 hello 安裝 toosucceed 的全域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="93df0-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="93df0-127">**tooverify hello 認證正確：**</span><span class="sxs-lookup"><span data-stu-id="93df0-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="93df0-128">連接太<https://login.microsoftonline.com>並用 hello 相同的認證。</span><span class="sxs-lookup"><span data-stu-id="93df0-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="93df0-129">請確定 hello 登入成功。</span><span class="sxs-lookup"><span data-stu-id="93df0-129">Make sure hello login is successful.</span></span> <span data-ttu-id="93df0-130">您可以檢查 hello 使用者角色移過**Azure Active Directory**  - &gt; **使用者和群組** - &gt; **所有使用者**.</span><span class="sxs-lookup"><span data-stu-id="93df0-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="93df0-131">選取您的使用者帳戶，然後 「 目錄角色 」 hello 產生功能表中。</span><span class="sxs-lookup"><span data-stu-id="93df0-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="93df0-132">請確認該 hello 選取的角色是 「 全域系統管理員 」。</span><span class="sxs-lookup"><span data-stu-id="93df0-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="93df0-133">如果您無法 tooaccess hello 的任何頁面沿著這些步驟，您不是全域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="93df0-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93df0-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93df0-134">Next steps</span></span>
[<span data-ttu-id="93df0-135">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="93df0-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
