---
title: "驗證和 Azure MFA Server aaaIIS |Microsoft 文件"
description: "這是可協助您部署 IIS 驗證與 Azure Multi-factor Authentication Server 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a><span data-ttu-id="b0909-103">針對 IIS Web 應用程式設定 Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="b0909-103">Configure Azure Multi-Factor Authentication Server for IIS web apps</span></span>

<span data-ttu-id="b0909-104">使用 IIS 驗證區段中的 hello Azure Multi-factor Authentication (MFA) Server tooenable hello 和設定 IIS 驗證整合與 Microsoft IIS web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0909-104">Use hello IIS Authentication section of hello Azure Multi-Factor Authentication (MFA) Server tooenable and configure IIS authentication for integration with Microsoft IIS web applications.</span></span> <span data-ttu-id="b0909-105">hello Azure MFA Server 會安裝一個外掛程式，可以篩選 toohello IIS web 伺服器 tooadd Azure Multi-factor Authentication Server 上提出的要求。</span><span class="sxs-lookup"><span data-stu-id="b0909-105">hello Azure MFA Server installs a plug-in that can filter requests being made toohello IIS web server tooadd Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="b0909-106">hello IIS 外掛程式提供表單架構驗證和整合式 Windows HTTP 驗證的支援。</span><span class="sxs-lookup"><span data-stu-id="b0909-106">hello IIS plug-in provides support for Form-Based Authentication and Integrated Windows HTTP Authentication.</span></span> <span data-ttu-id="b0909-107">信任的 Ip 也可以從 雙因素驗證設定的 tooexempt 內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b0909-107">Trusted IPs can also be configured tooexempt internal IP addresses from two-factor authentication.</span></span>

![IIS 驗證](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a><span data-ttu-id="b0909-109">搭配 Azure Multi-Factor Authentication Server 使用表單架構 IIS 驗證</span><span class="sxs-lookup"><span data-stu-id="b0909-109">Using Form-Based IIS Authentication with Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="b0909-110">toosecure IIS web 應用程式使用表單架構驗證、 hello Azure Multi-factor Authentication Server hello IIS web 伺服器上安裝和設定每個程序的 hello hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="b0909-110">toosecure an IIS web application that uses form-based authentication, install hello Azure Multi-Factor Authentication Server on hello IIS web server and configure hello Server per hello following procedure:</span></span>

1. <span data-ttu-id="b0909-111">在 hello Azure Multi-factor Authentication Server，hello 左側功能表中的 hello IIS 驗證 圖示。</span><span class="sxs-lookup"><span data-stu-id="b0909-111">In hello Azure Multi-Factor Authentication Server, click hello IIS Authentication icon in hello left menu.</span></span>
2. <span data-ttu-id="b0909-112">按一下 hello**表單架構** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b0909-112">Click hello **Form-Based** tab.</span></span>
3. <span data-ttu-id="b0909-113">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="b0909-113">Click **Add**.</span></span>
4. <span data-ttu-id="b0909-114">toodetect 使用者名稱、 密碼和網域變數，自動輸入 hello 自動設定表單架構網站 對話方塊中的 hello 登入 URL （例如 https://localhost/contoso/auth/login.aspx)，並按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="b0909-114">toodetect username, password and domain variables automatically, enter hello Login URL (like https://localhost/contoso/auth/login.aspx) within hello Auto-Configure Form-Based Website dialog box and click **OK**.</span></span>
5. <span data-ttu-id="b0909-115">檢查 hello**需要進行 Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入 hello 伺服器與主體 toomulti 雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="b0909-115">Check hello **Require Multi-Factor Authentication user match** box if all users have been or will be imported into hello Server and subject toomulti-factor authentication.</span></span> <span data-ttu-id="b0909-116">如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於多因素驗證，請不要 hello 方塊中選取。</span><span class="sxs-lookup"><span data-stu-id="b0909-116">If a significant number of users have not yet been imported into hello Server and/or will be exempt from multi-factor authentication, leave hello box unchecked.</span></span>
6. <span data-ttu-id="b0909-117">如果無法自動偵測 hello 頁面變數，按一下**手動指定**hello 自動設定表單架構網站 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="b0909-117">If hello page variables cannot be detected automatically, click **Specify Manually** in hello Auto-Configure Form-Based Website dialog box.</span></span>
7. <span data-ttu-id="b0909-118">在 hello 新增表單架構網站 對話方塊中，輸入 hello 提交 URL 欄位中的 hello URL toohello 登入頁面，並輸入應用程式名稱 （選擇性）。</span><span class="sxs-lookup"><span data-stu-id="b0909-118">In hello Add Form-Based Website dialog box, enter hello URL toohello login page in hello Submit URL field and enter an Application name (optional).</span></span> <span data-ttu-id="b0909-119">hello 應用程式名稱會出現在 Azure Multi-factor Authentication 報告，並可能會顯示在簡訊或行動裝置應用程式驗證訊息內。</span><span class="sxs-lookup"><span data-stu-id="b0909-119">hello Application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.</span></span>
8. <span data-ttu-id="b0909-120">選取 hello 正確的要求格式。</span><span class="sxs-lookup"><span data-stu-id="b0909-120">Select hello correct Request format.</span></span> <span data-ttu-id="b0909-121">這設定得**POST 或 GET**大部分 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0909-121">This is set too**POST or GET** for most web applications.</span></span>
9. <span data-ttu-id="b0909-122">輸入 hello 使用者名稱變數、 密碼變數和網域變數 （如果出現在 hello 登入頁面上）。</span><span class="sxs-lookup"><span data-stu-id="b0909-122">Enter hello Username variable, Password variable, and Domain variable (if it appears on hello login page).</span></span> <span data-ttu-id="b0909-123">hello toofind hello 名稱輸入方塊、 瀏覽網頁瀏覽器 toohello 登入頁面、 在 hello 頁面上，以滑鼠右鍵按一下並選取**檢視原始檔**。</span><span class="sxs-lookup"><span data-stu-id="b0909-123">toofind hello names of hello input boxes, navigate toohello login page in a web browser, right-click on hello page, and select **View Source**.</span></span>
10. <span data-ttu-id="b0909-124">檢查 hello**需要 Azure Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入 hello 伺服器與主體 toomulti 雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="b0909-124">Check hello **Require Azure Multi-Factor Authentication user match** box if all users have been or will be imported into hello Server and subject toomulti-factor authentication.</span></span> <span data-ttu-id="b0909-125">如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於多因素驗證，請不要 hello 方塊中選取。</span><span class="sxs-lookup"><span data-stu-id="b0909-125">If a significant number of users have not yet been imported into hello Server and/or will be exempt from multi-factor authentication, leave hello box unchecked.</span></span>
11. <span data-ttu-id="b0909-126">按一下**進階**tooreview 進階設定，包括：</span><span class="sxs-lookup"><span data-stu-id="b0909-126">Click **Advanced** tooreview advanced settings, including:</span></span>

  - <span data-ttu-id="b0909-127">選取自訂拒絕頁面檔案</span><span class="sxs-lookup"><span data-stu-id="b0909-127">Select a custom denial page file</span></span>
  - <span data-ttu-id="b0909-128">針對一段時間使用 cookie 快取成功驗證 toohello 網站</span><span class="sxs-lookup"><span data-stu-id="b0909-128">Cache successful authentications toohello website for a period of time using cookies</span></span>
  - <span data-ttu-id="b0909-129">選擇是否要針對 Windows 網域、 LDAP 目錄的 tooauthenticate hello 主要認證。</span><span class="sxs-lookup"><span data-stu-id="b0909-129">Select whether tooauthenticate hello primary credentials against a Windows Domain, LDAP directory.</span></span> <span data-ttu-id="b0909-130">還是 RADIUS 伺服器來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="b0909-130">or RADIUS server.</span></span>

12. <span data-ttu-id="b0909-131">按一下**確定**tooreturn toohello 新增表單架構網站 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b0909-131">Click **OK** tooreturn toohello Add Form-Based Website dialog box.</span></span>
13. <span data-ttu-id="b0909-132">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b0909-132">Click **OK**.</span></span>
14. <span data-ttu-id="b0909-133">一次 hello URL 且已偵測到或輸入頁面變數時，顯示在 hello 表單架構 面板的 hello 網站資料。</span><span class="sxs-lookup"><span data-stu-id="b0909-133">Once hello URL and page variables have been detected or entered, hello website data displays in hello Form-Based panel.</span></span>

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a><span data-ttu-id="b0909-134">搭配 Azure Multi-Factor Authentication Server 使用整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="b0909-134">Using Integrated Windows Authentication with Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="b0909-135">IIS web 應用程式使用整合式 Windows 驗證，Azure MFA Server hello hello IIS web 伺服器上安裝，然後設定的 toosecure hello 伺服器以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b0909-135">toosecure an IIS web application that uses Integrated Windows HTTP authentication, install hello Azure MFA Server on hello IIS web server, then configure hello Server with hello following steps:</span></span>

1. <span data-ttu-id="b0909-136">在 hello Azure Multi-factor Authentication Server，hello 左側功能表中的 hello IIS 驗證 圖示。</span><span class="sxs-lookup"><span data-stu-id="b0909-136">In hello Azure Multi-Factor Authentication Server, click hello IIS Authentication icon in hello left menu.</span></span>
2. <span data-ttu-id="b0909-137">按一下 hello **HTTP**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b0909-137">Click hello **HTTP** tab.</span></span>
3. <span data-ttu-id="b0909-138">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="b0909-138">Click **Add**.</span></span>
4. <span data-ttu-id="b0909-139">在 hello [新增基底 URL] 對話方塊中，輸入 hello 網站 HTTP 驗證 （例如 http://localhost/owa) 執行 hello URL，並提供應用程式名稱 （選擇性）。</span><span class="sxs-lookup"><span data-stu-id="b0909-139">In hello Add Base URL dialogue box, enter hello URL for hello website where HTTP authentication is performed (like http://localhost/owa) and provide an Application name (optional).</span></span> <span data-ttu-id="b0909-140">hello 應用程式名稱會出現在 Azure Multi-factor Authentication 報告，並可能會顯示在簡訊或行動裝置應用程式驗證訊息內。</span><span class="sxs-lookup"><span data-stu-id="b0909-140">hello Application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.</span></span>
5. <span data-ttu-id="b0909-141">調整 hello 閒置逾時和最大工作階段時間如果 hello 預設值不足。</span><span class="sxs-lookup"><span data-stu-id="b0909-141">Adjust hello Idle timeout and Maximum session times if hello default is not sufficient.</span></span>
6. <span data-ttu-id="b0909-142">檢查 hello**需要進行 Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入 hello 伺服器與主體 toomulti 雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="b0909-142">Check hello **Require Multi-Factor Authentication user match** box if all users have been or will be imported into hello Server and subject toomulti-factor authentication.</span></span> <span data-ttu-id="b0909-143">如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於多因素驗證，請不要 hello 方塊中選取。</span><span class="sxs-lookup"><span data-stu-id="b0909-143">If a significant number of users have not yet been imported into hello Server and/or will be exempt from multi-factor authentication, leave hello box unchecked.</span></span>
7. <span data-ttu-id="b0909-144">檢查 hello **Cookie 快取**視方塊。</span><span class="sxs-lookup"><span data-stu-id="b0909-144">Check hello **Cookie cache** box if desired.</span></span>
8. <span data-ttu-id="b0909-145">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b0909-145">Click **OK**.</span></span>

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a><span data-ttu-id="b0909-146">啟用 Azure Multi-Factor Authentication Server 的 IIS 外掛程式</span><span class="sxs-lookup"><span data-stu-id="b0909-146">Enable IIS Plug-ins for Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="b0909-147">設定之後 hello 表單架構或 HTTP 驗證 Url 和值，請選取 hello 應載入和在 IIS 中啟用 hello Azure Multi-factor Authentication IIS 外掛程式的位置。</span><span class="sxs-lookup"><span data-stu-id="b0909-147">After configuring hello Form-Based or HTTP authentication URLs and settings, select hello locations where hello Azure Multi-Factor Authentication IIS plug-ins should be loaded and enabled in IIS.</span></span> <span data-ttu-id="b0909-148">使用下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="b0909-148">Use hello following procedure:</span></span>

1. <span data-ttu-id="b0909-149">如果在 IIS 6 上執行，請按一下 hello **ISAPI**  索引標籤。選取 hello hello web 應用程式的網站正在執行 （例如預設網站） tooenable hello Azure Multi-factor Authentication ISAPI 篩選外掛程式該站台。</span><span class="sxs-lookup"><span data-stu-id="b0909-149">If running on IIS 6, click hello **ISAPI** tab. Select hello website that hello web application is running under (e.g. Default Web Site) tooenable hello Azure Multi-Factor Authentication ISAPI filter plug-in for that site.</span></span>
2. <span data-ttu-id="b0909-150">如果在 IIS 7 或更新版本執行，請按一下 hello**原生模組** 索引標籤。選取 hello 伺服器、 網站或應用程式 tooenable hello IIS 外掛程式所需的 hello 層級。</span><span class="sxs-lookup"><span data-stu-id="b0909-150">If running on IIS 7 or higher, click hello **Native Module** tab. Select hello server, websites, or applications tooenable hello IIS plug-in at hello desired levels.</span></span>
3. <span data-ttu-id="b0909-151">按一下 hello**啟用 IIS 驗證**在 hello 囉 」 畫面最上方的方塊。</span><span class="sxs-lookup"><span data-stu-id="b0909-151">Click hello **Enable IIS authentication** box at hello top of hello screen.</span></span> <span data-ttu-id="b0909-152">Azure Multi-factor Authentication 現在會保護選取的 hello IIS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0909-152">Azure Multi-Factor Authentication is now securing hello selected IIS application.</span></span> <span data-ttu-id="b0909-153">請確認使用者具有已匯入 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b0909-153">Ensure that users have been imported into hello Server.</span></span>

## <a name="trusted-ips"></a><span data-ttu-id="b0909-154">信任的 IP</span><span class="sxs-lookup"><span data-stu-id="b0909-154">Trusted IPs</span></span>
<span data-ttu-id="b0909-155">hello 信任的 Ip 允許來自特定 IP 位址或子網路的網站要求的使用者 toobypass Azure 多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="b0909-155">hello Trusted IPs allows users toobypass Azure Multi-Factor Authentication for website requests originating from specific IP addresses or subnets.</span></span> <span data-ttu-id="b0909-156">比方說，您可以從 Azure Multi-factor Authentication tooexempt 使用者從 hello 辦公室登入時。</span><span class="sxs-lookup"><span data-stu-id="b0909-156">For example, you may want tooexempt users from Azure Multi-Factor Authentication while logging in from hello office.</span></span> <span data-ttu-id="b0909-157">因此，您可以指定 hello 辦公室子網路作為信任的 Ip 項目。</span><span class="sxs-lookup"><span data-stu-id="b0909-157">For this, you would specify hello office subnet as a Trusted IPs entry.</span></span> <span data-ttu-id="b0909-158">tooconfigure 信任 Ip 時，使用下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="b0909-158">tooconfigure Trusted IPs, use hello following procedure:</span></span>

1. <span data-ttu-id="b0909-159">在 hello IIS 驗證區段中，按一下 hello**信任的 Ip**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b0909-159">In hello IIS Authentication section, click hello **Trusted IPs** tab.</span></span>
2. <span data-ttu-id="b0909-160">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="b0909-160">Click **Add**.</span></span>
3. <span data-ttu-id="b0909-161">Hello 新增信任的 Ip 對話方塊出現時，選取 hello**單一 IP**， **IP 範圍**，或**子網路**選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0909-161">When hello Add Trusted IPs dialog box appears, select hello **Single IP**, **IP range**, or **Subnet** radio button.</span></span>
4. <span data-ttu-id="b0909-162">輸入 hello IP 位址、 IP 位址範圍或子網路應列入白名單。</span><span class="sxs-lookup"><span data-stu-id="b0909-162">Enter hello IP address, range of IP addresses or subnet that should be whitelisted.</span></span> <span data-ttu-id="b0909-163">如果輸入子網路、 選取 hello 適當的網路遮罩，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="b0909-163">If entering a subnet, select hello appropriate Netmask and click **OK**.</span></span> <span data-ttu-id="b0909-164">現在已加入 hello 白名單。</span><span class="sxs-lookup"><span data-stu-id="b0909-164">hello whitelist has now been added.</span></span>