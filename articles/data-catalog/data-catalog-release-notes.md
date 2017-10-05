---
title: "Azure 資料目錄版本資訊 | Microsoft Docs"
description: "Azure 資料目錄的版本資訊。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: d3db9bee0558cac5fb4f5b8fb4ab67a35ce0f141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="0538f-103">Azure 資料目錄版本資訊</span><span class="sxs-lookup"><span data-stu-id="0538f-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-the-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="0538f-104">Azure 資料目錄 2015 年 11 月 20 日版本的注意事項</span><span class="sxs-lookup"><span data-stu-id="0538f-104">Notes for the November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="0538f-105">在 Power BI Desktop 中開啟資料來源</span><span class="sxs-lookup"><span data-stu-id="0538f-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="0538f-106">使用 **Azure 資料目錄** 入口網站的 [在 Power BI Desktop 中開啟資料來源] 選項時，使用者可能會在 Power BI Desktop 應用程式中遇到下列兩個問題之一：</span><span class="sxs-lookup"><span data-stu-id="0538f-106">When using the "Open in Power BI Desktop" option from the **Azure Data Catalog** portal, users may encounter one of two problems in the Power BI Desktop application:</span></span>

* <span data-ttu-id="0538f-107">會顯示標題為「無法開啟文件」的對話方塊</span><span class="sxs-lookup"><span data-stu-id="0538f-107">A dialog box with the title "Unable to Open Document" is displayed</span></span>
* <span data-ttu-id="0538f-108">Power BI Desktop 應用程式可開啟，但檔案是空的</span><span class="sxs-lookup"><span data-stu-id="0538f-108">The Power BI Desktop application opens, but the file appears to be empty</span></span>

<span data-ttu-id="0538f-109">針對上述每個狀況，只要從 [PowerBI.com](https://powerbi.com)下載並安裝最新版的 Power BI Desktop 即可解決問題。</span><span class="sxs-lookup"><span data-stu-id="0538f-109">For each situation, the problem can be resolved by downloading and installing the latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-the-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="0538f-110">Azure 資料目錄 2015 年 11 月 13 日版本的注意事項</span><span class="sxs-lookup"><span data-stu-id="0538f-110">Notes for the November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-teradata"></a><span data-ttu-id="0538f-111">註冊並連接至 Teradata</span><span class="sxs-lookup"><span data-stu-id="0538f-111">Registering and connecting to Teradata</span></span>
<span data-ttu-id="0538f-112">連接到 Teradata 資料來源時，使用者必須已安裝正確的 Teradata ODBC 驅動程式，符合所使用軟體的位元 (32 位元或 64 位元)。</span><span class="sxs-lookup"><span data-stu-id="0538f-112">When connecting to Teradata data sources users must have installed the correct Teradata ODBC driver that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

<span data-ttu-id="0538f-113">截至本 ADC 發行日為止，最新 [適用於 Windows 的 Teradata ODBC 驅動程式 (15.10 版)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) 相容於 Office 2013，但不相容於 Office 2016。</span><span class="sxs-lookup"><span data-stu-id="0538f-113">As of this ADC release date, the most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-the-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="0538f-114">Azure 資料目錄 2015 年 7 月 13 日版本的注意事項</span><span class="sxs-lookup"><span data-stu-id="0538f-114">Notes for the July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-oracle-database"></a><span data-ttu-id="0538f-115">註冊並連接至 Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="0538f-115">Registering and connecting to Oracle Database</span></span>
<span data-ttu-id="0538f-116">連接到 Oracle 資料庫資料來源時，使用者必須已安裝正確的 Oracle 驅動程式，符合所使用軟體的位元 (32 位元或 64 位元)。</span><span class="sxs-lookup"><span data-stu-id="0538f-116">When connecting to Oracle Database data sources users must have installed the correct Oracle drivers that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

* <span data-ttu-id="0538f-117">在執行 32 位元 Windows 的電腦上註冊 Oracle 資料來源時，將使用 32 位元 Oracle 驅動程式</span><span class="sxs-lookup"><span data-stu-id="0538f-117">When registering Oracle data sources on a computer running 32-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="0538f-118">在執行 64 位元 Windows 的電腦上註冊 Oracle 資料來源時，將使用 64 位元 Oracle 驅動程式</span><span class="sxs-lookup"><span data-stu-id="0538f-118">When registering Oracle data sources on a computer running 64-bit Windows, the 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="0538f-119">在執行 32 位元版本 Microsoft Office 的電腦上使用 Excel 連接到 Oracle 資料來源時 (包括在 64 位元 Windows 上)，將使用 32 位元 Oracle 驅動程式</span><span class="sxs-lookup"><span data-stu-id="0538f-119">When connecting to Oracle data sources using Excel on a computer running the 32-bit version of Microsoft Office, including on 64-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="0538f-120">在執行 64 位元版本 Microsoft Office 的電腦上使用 Excel 連接到 Oracle 資料來源時，將使用 64 位元 Oracle 驅動程式</span><span class="sxs-lookup"><span data-stu-id="0538f-120">When connecting to Oracle data sources using Excel on a computer running the 64-bit version of Microsoft Office, the 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-to-sql-server-reporting-services"></a><span data-ttu-id="0538f-121">註冊及連接到 SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="0538f-121">Registering and connecting to SQL Server Reporting Services</span></span>
<span data-ttu-id="0538f-122">對於 SQL Server Reporting Services (SSRS) 資料來源的支援，僅限於原生模式伺服器。</span><span class="sxs-lookup"><span data-stu-id="0538f-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited to Native Mode servers only.</span></span> <span data-ttu-id="0538f-123">未來版本將加入在 SharePoint 模式中支援 SSRS。</span><span class="sxs-lookup"><span data-stu-id="0538f-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="0538f-124">在 Excel 中開啟資料資產</span><span class="sxs-lookup"><span data-stu-id="0538f-124">Opening data assets in Excel</span></span>
<span data-ttu-id="0538f-125">在 Microsoft Excel 中從 **Azure 資料目錄**入口網站開啟資料資產時，使用者可能會看到 [Microsoft Excel 安全性注意事項] 對話方塊的提示。</span><span class="sxs-lookup"><span data-stu-id="0538f-125">When opening data assets in Microsoft Excel from the **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="0538f-126">這是標準的預期行為，使用者可以選取 [啟用]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="0538f-126">This is standard, expected behavior, and users can select **Enable** to continue.</span></span>

<span data-ttu-id="0538f-127">如需詳細資訊，請參閱 [啟用或停用可疑網站之連結和檔案的安全性警告](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE)。</span><span class="sxs-lookup"><span data-stu-id="0538f-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="0538f-128">Proxy 與原則設定及資料來源註冊</span><span class="sxs-lookup"><span data-stu-id="0538f-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="0538f-129">使用者可能會遇到一種情況，他們可以登入 Azure 資料目錄入口網站，但在嘗試登入資料來源註冊工具時，卻遇到錯誤訊息，導致無法登入。</span><span class="sxs-lookup"><span data-stu-id="0538f-129">Users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="0538f-130">此問題行為有兩個可能的原因：</span><span class="sxs-lookup"><span data-stu-id="0538f-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="0538f-131">**原因 1：Active Directory Federation Services 設定**。資料來源註冊工具使用「表單驗證」，根據 Active Directory 驗證使用者登入。</span><span class="sxs-lookup"><span data-stu-id="0538f-131">**Cause 1: Active Directory Federation Services configuration** The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span></span> <span data-ttu-id="0538f-132">Active Directory 系統管理員必須在全域驗證原則中啟用表單驗證，登入才會成功。</span><span class="sxs-lookup"><span data-stu-id="0538f-132">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="0538f-133">在某些情況下，只有當使用者是在公司網路上，或只有當使用者從公司網路外部連接時，才會發生此錯誤行為。</span><span class="sxs-lookup"><span data-stu-id="0538f-133">In some situations, this error behavior may occur only when the user is on the company network, or only when the user is connecting from outside the company network.</span></span> <span data-ttu-id="0538f-134">全域驗證原則允許分別為內部網路和外部網路連線啟用驗證方法。</span><span class="sxs-lookup"><span data-stu-id="0538f-134">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="0538f-135">如果使用者連線的網路未啟用表單驗證，可能會發生登入錯誤。</span><span class="sxs-lookup"><span data-stu-id="0538f-135">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span></span>

<span data-ttu-id="0538f-136">如需詳細資訊，請參閱 [設定驗證原則](https://technet.microsoft.com/library/dn486781.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0538f-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="0538f-137">**原因 2：網路 Proxy 設定**。如果公司網路使用 Proxy 伺服器，註冊工具可能無法透過 Proxy 連線到 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="0538f-137">**Cause 2: Network proxy configuration** If the corporate network uses a proxy server, the registration tool may not be able to connect to Azure Active Directory through the proxy.</span></span> <span data-ttu-id="0538f-138">使用者可以編輯註冊工具的組態檔，將此區段加入至檔案，以確保註冊工具能夠連線：</span><span class="sxs-lookup"><span data-stu-id="0538f-138">Users can ensure that the registration tool by editing the tool’s configuration file, adding this section to the file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="0538f-139">若要找出 RegistrationTool.exe.config 檔案，請啟動註冊工具，然後開啟 Windows 工作管理員公用程式。</span><span class="sxs-lookup"><span data-stu-id="0538f-139">To locate the RegistrationTool.exe.config file, launch the registration tool, and then open the Windows Task Manager utility.</span></span> <span data-ttu-id="0538f-140">在工作管理員的 [詳細資料] 索引標籤，以滑鼠右鍵按一下 RegistrationTool.exe，再從快顯功能表中選擇 [開啟檔案位置]。</span><span class="sxs-lookup"><span data-stu-id="0538f-140">On the Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from the pop-up menu.</span></span>
