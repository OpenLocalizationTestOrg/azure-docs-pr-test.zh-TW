---
title: "Azure 雲端服務與 Azure CDN aaaIntegrate |Microsoft 文件"
description: "了解如何 toodeploy 雲端服務提供整合的 Azure CDN 端點的內容"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a> 整合雲端服務與 Azure CDN
雲端服務可以整合 Azure cdn，提供任何內容來自 hello 雲端服務的位置。 這個方法提供下列您 hello 下列優點：

* 輕鬆地在雲端服務的專案目錄中部署和更新影像、指令碼和樣式表
* 輕鬆升級您的雲端服務，例如 jQuery 或啟動程序的版本中的 hello NuGet 封裝
* 管理您的 Web 應用程式和您 CDN 服務內容所有從 hello 相同 Visual Studio 介面
* Web 應用程式和 CDN 提供的內容採用統一的部署工作流程
* 整合 ASP.NET 統合和縮製與 Azure CDN

## <a name="what-you-will-learn"></a>學習目標
在本教學課程中，您將了解如何：

* [整合 Azure CDN 端點與雲端服務，並從 Azure CDN 提供網頁的靜態內容](#deploy)
* [在雲端服務中為靜態內容設定快取設定](#caching)
* [透過 Azure CDN 使用控制器動作提供內容](#controller)
* [Serve 結合在一起，並縮短透過 Azure CDN 的內容，同時保留 hello 指令碼偵錯 Visual Studio 體驗](#bundling)
* [設定 Azure CDN 離線時的後援指令碼和 CSS](#fallback)

## <a name="what-you-will-build"></a>將建置的項目
您將部署雲端服務 Web 角色將 hello 預設的 ASP.NET MVC 範本、 從整合式的 Azure CDN，例如影像、 控制器動作的結果及 hello 預設 JavaScript 和 CSS 檔案，加入程式碼 tooserve 內容和也可以撰寫程式碼 tooconfigure hello組合服務 hello 事件中的 hello CDN 的遞補機制已離線。

## <a name="what-you-will-need"></a>必要元件
本教學課程有 hello 下列必要條件：

* 使用中的 [Microsoft Azure 帳戶](/account/)
* Visual Studio 2015 (含 [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> 您需要 Azure 帳戶 toocomplete 本教學課程：
> 
> * 您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)-取得信用額度您可以使用 tootry 出支付 Azure 服務，而且即使他們用於之後您可以在最多保留 hello 帳戶，並使用免費的 Azure 服務，例如網站。
> * 您可以 [啟用 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - 您的 MSDN 訂閱每月會提供您額度，您可以用在 Azure 付費服務。
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>部署雲端服務
在本節中，您會部署 hello 預設 Visual Studio 2015 tooa 雲端服務 Web 角色，在 ASP.NET MVC 應用程式範本，然後將它整合到新的 CDN 端點。 請遵循下列的 hello 指示：

1. 在 Visual Studio 2015 中，建立新的 Azure 雲端服務從功能表列中 hello 太移**檔案 > 新增 > 專案 > 雲端 > Azure 雲端服務**。 命名並按一下 [確定] 。
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. 選取**ASP.NET Web 角色**按一下 hello  **>**   按鈕。 按一下 [確定]。
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. 選取 [MVC]，按一下 [確定]。
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. 現在，將發佈此 Web 角色 tooan Azure 雲端服務。 Hello 雲端服務專案上按一下滑鼠右鍵，然後選取**發行**。
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. 如果您不尚未登入 Microsoft Azure，請按一下 hello**新增帳戶...**下拉式清單中，然後按一下 hello**將帳戶加入**功能表項目。
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. 在 hello 登入頁面中，使用登入 hello tooactivate 您使用您的 Azure 帳戶的 Microsoft 帳戶。
7. 登入後，按一下 [ **下一步**]。
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. 如果您未建立雲端服務或儲存體帳戶，Visual Studio 會協助您建立兩者。 在 hello**建立雲端服務和帳戶**對話方塊、 型別 hello 所需的服務名稱和選取 hello 所需的區域。 然後按一下 [ **建立**]。
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. 在 hello 發佈設定 頁面上，確認 hello 組態，按一下 **發行**。
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > 雲端服務的 hello 發行程序需要較長時間。 hello 啟用 Web Deploy 的所有角色 選項可以進行偵錯雲端服務更快，藉由提供快速 （但暫存） 更新 tooyour Web 角色。 如需有關這個選項的詳細資訊，請參閱[發行雲端服務使用 hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx)。
   > 
   > 
   
    當 hello **Microsoft Azure 活動記錄檔**顯示發行狀態為**已完成**，您將建立 CDN 端點與此雲端服務整合。
   
   > [!WARNING]
   > 如果之後發佈，部署的 hello 雲端服務會顯示錯誤畫面，它可能是因為您已部署的 hello 雲端服務正在使用[客體 OS 不包含.NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates)。  您可 [將 .NET 4.5.2 部署為啟動工作](../cloud-services/cloud-services-dotnet-install-dotnet.md)，以解決此問題。
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>建立新的 CDN 設定檔
CDN 設定檔就是 CDN 端點的集合。  每個設定檔皆包含一或多個 CDN 端點。  您可能希望 toouse 多個設定檔 tooorganize 您的 CDN 端點的網際網路網域、 web 應用程式，或其他一些準則。

> [!TIP]
> 如果您已經有您想 toouse，本教學課程中的 CDN 設定檔時，繼續太[建立新的 CDN 端點](#create-a-new-cdn-endpoint)。
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>建立新的 CDN 端點
**toocreate 新儲存體帳戶的 CDN 端點**

1. 在 hello [Azure 管理入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。  您可能已釘選它 toohello 儀表板 hello 上一個步驟中。  如果您不是，您可以找到它，即可**瀏覽**，然後**CDN 設定檔**，而且 hello 設定檔上按一下您想 tooadd 至您的端點。
   
    hello CDN 設定檔 刀鋒視窗隨即出現。
   
    ![CDN 設定檔][cdn-profile-settings]
2. 按一下 hello**加入端點** 按鈕。
   
    ![[加入端點] 按鈕][cdn-new-endpoint-button]
   
    hello**將端點加入**刀鋒視窗隨即出現。
   
    ![[加入端點] 刀鋒視窗][cdn-add-endpoint]
3. 輸入這個 CDN 端點的 [名稱]  。  此名稱將會使用的 tooaccess hello 網域您快取的資源`<EndpointName>.azureedge.net`。
4. 在 hello**來源類型**下拉式清單中，選取*雲端服務*。  
5. 在 hello**來源主機名稱**下拉式清單中，選取您的雲端服務。
6. 保留 hello 的預設值**原始路徑**，**原始主機標頭**，和**原始通訊協定/連接埠**。  您至少必須指定一個通訊協定 (HTTP 或 HTTPS)。
7. 按一下 hello**新增**按鈕 toocreate hello 新端點。
8. 一旦建立 hello 端點時，它會出現在 hello 設定檔的端點清單。 hello 清單檢視會顯示 hello URL toouse tooaccess 快取內容，以及 hello 原始網域。
   
    ![CDN 端點][cdn-endpoint-success]
   
   > [!NOTE]
   > hello 端點將無法立即可供使用。  就可以在透過 hello CDN 網路 hello 註冊 toopropagate too90 分鐘。 可透過 hello CDN hello 內容之前，立即嘗試 toouse hello CDN 網域名稱的使用者可能會收到狀態碼 404。
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>測試 hello CDN 端點
發行狀態的 hello 時**已完成**、 開啟瀏覽器視窗，並瀏覽過**http://<cdnName>*.azureedge.net/Content/bootstrap.css**。 在我的設定中，此 URL 為：

    http://camservice.azureedge.net/Content/bootstrap.css

對應 toohello 遵循在 hello CDN 端點的原始 URL:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

當您巡覽太**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**，根據您的瀏覽器中，您將會是提示的 toodownload 或開啟 hello bootstrap.css，來自已發行的 Web 應用程式。

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

同樣地，您可以從 CDN 端點，以 http://&lt;serviceName>.cloudapp.net/ 存取任何可公開存取的 URL。 例如：

* 從 hello /Script 路徑.js 檔案
* Hello /Content 從任何內容的檔案路徑
* 任何控制器/動作
* 如果已在您的 CDN 端點，任何 URL 查詢字串以啟用 hello 查詢字串

事實上，以 hello 上述組態，您可以主控 hello 整個雲端服務從 **http://*&lt;cdnName >*.azureedge.net/**。如果太瀏覽**http://camservice.azureedge.net/ * * 將 hello 動作結果中的 Home/Index。

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

不過，這不表示永遠是個不錯的主意 tooserve 透過 Azure CDN 的整個雲端服務。 

CDN 與靜態傳遞最佳化不會不一定被加速並非 toobe 快取，或因為 hello CDN 必須 hello 資產的新版本從提取 hello 原始伺服器通常很頻繁地更新動態資產的傳遞。 針對此案例中，您可以啟用[動態網站加速](cdn-dynamic-site-acceleration.md)最佳化 (DSA)，您會使用各種技術 toospeed 向上傳遞非快取的動態資產的 CDN 端點。 

如果您有混合的靜態及動態內容的站台，您可以選擇 tooserve 靜態內容從 CDN 與靜態最佳化型別 （例如一般 web 傳遞） 和 tooserve 動態內容直接從 hello 原始伺服器，或是透過 CDNDSA 最佳化端點開啟個別的情況。 toothat 結束時，您已經看過如何 tooaccess 個別的內容檔案從 hello CDN 端點。 我將示範如何 tooserve 特定控制器動作，透過特定的 CDN 端點在服務控制器的動作，透過 Azure CDN 的內容。

hello 的替代方式是 toodetermine 的雲端服務中的案例為基礎的 tooserve 從 Azure CDN 的內容。 toothat 結束時，您已經看過如何 tooaccess 個別的內容檔案從 hello CDN 端點。 我將示範如何 tooserve 特定控制器動作，透過 hello 中的 CDN 端點[提供從控制器動作，透過 Azure CDN 的內容](#controller)。

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>在雲端服務中設定靜態檔案的快取選項
與雲端服務中的 Azure CDN 整合，您可以指定您想在 hello CDN 端點中快取靜態內容 toobe 的方式。 toodo，開啟*Web.config*從您的 Web 角色專案 (例如 WebRole1)，並加入`<staticContent>`項目太`<system.webServer>`。 hello 以下的 XML 設定 hello 快取 tooexpire 3 天內。  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

一旦您這樣做，您的雲端服務中的所有靜態檔案將會觀察的 hello 相同規則在您的 CDN 快取。 若要更精確控制快取設定，請將 *Web.config* 檔案加入至資料夾，並在檔案中新增您的設定。 例如，加入*Web.config*檔案 toohello *\Content*資料夾和取代 hello 內容以下列 XML 的 hello:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

這項設定會導致所有靜態檔案從 hello *\Content*資料夾 toobe 快取 15 天。

如需有關如何 tooconfigure hello`<clientCache>`項目，請參閱[用戶端快取&lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache)。

在[提供從控制器動作，透過 Azure CDN 的內容](#controller)，我也會顯示您如何設定控制器的動作結果的快取設定，以及在 hello CDN 快取中。

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>透過 Azure CDN 使用控制器動作提供內容
當您使用 Azure CDN 整合的雲端服務 Web 角色時，是相當容易 tooserve 從控制器動作，透過 hello Azure CDN 的內容。 以外處理您的雲端服務直接透過 Azure CDN （示範上面），[馬頓 Balliauw](https://twitter.com/maartenballiauw)為您示範如何 toodo 它與有趣 MemeGenerator 控制器中的[減少以 hello Azure CDN 的 hello 網站上的延遲時間](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). 我在這裡簡單地重述一次。

假設您想要在您的雲端服務中的年輕 Chuck Norris 映像為基礎的 toogenerate memes (由相片[Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) 如下所示：

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

您有簡單`Index`動作，可 hello 客戶 toospecify hello superlatives hello 影像中，然後產生 hello 卡通人物，一旦他們後 toohello 動作。 因為這是 Chuck Norris，您希望此頁面 toobecome 末來而多半極受歡迎全域。 這就是利用 Azure CDN 來提供半動態內容的一個最佳例子。

請遵循上述 toosetup hello 步驟，此控制器的動作：

1. 在 hello *\Controllers*資料夾中，建立新的.cs 檔案呼叫*MemeGeneratorController.cs*並取代 hello 內容以 hello 遵循程式碼。 確定 tooreplace hello 反白顯示的部分是您 CDN 的名稱。  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. 以滑鼠右鍵按一下 hello 預設`Index()`動作，並選取**加入檢視**。
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. 接受下列 hello 設定值，然後按一下**新增**。
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. 開啟新的 hello *Views\MemeGenerator\Index.cshtml*和 hello 內容取代為下列簡單的 HTML 送出 hello superlatives hello:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. 重新發行 hello 雲端服務，並瀏覽過**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** 瀏覽器中的。

當您送出 hello 表單值太`/MemeGenerator/Index`，hello`Index_Post`動作方法會傳回連結 toohello`Show`動作方法，以個別的輸入識別碼 hello。 當您按一下 hello 連結時，您會到達 hello 下列程式碼：  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

如果您的本機偵錯工具已附加，將會取得本機的重新導向的 hello 一般偵錯經驗。 如果它 hello 雲端服務中執行，它會重新導向至：

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

對應 toohello 之後在您的 CDN 端點的原始 URL:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


然後，您可以使用 hello`OutputCacheAttribute`屬性 hello`Generate`方法 toospecify 方式應該快取 hello 動作結果，這將會採用 Azure CDN。 下列程式碼 hello 指定快取的到期日 1 小時 （3600 秒）。

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

同樣地，您可從任何控制器動作的內容在您的雲端服務中透過您的 Azure CDN，預期的 hello 快取選項。

Hello 下一節，我將說明如何配套 tooserve hello，及縮短指令碼並透過 Azure CDN 的 CSS。

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>整合 ASP.NET 統合和縮製與 Azure CDN
指令碼和 CSS 樣式表不常變更，而是主要的 hello Azure CDN 快取。 處理 hello 整個 Web 角色透過 Azure CDN 是最簡單方式 toointegrate hello 統合及縮製的 Azure CDN。 不過，因為您可能不想 toodo 此，我將說明如何 toodo 它同時保留 hello 預期 develper 經驗的 ASP.NET 統合及縮製，例如：

* 絕佳的偵錯模式體驗
* 流暢的部署
* 立即更新 tooclients 指令碼/CSS 版本升級
* CDN 端點失敗時的後援機制
* 儘可能不修改程式碼

在 hello **WebRole1**您建立專案時[整合您的 Azure 網站的 Azure CDN 端點，並提供靜態內容在網頁中，從 Azure CDN](#deploy)，開啟*App_Start\BundleConfig.cs* ，看看 hello`bundles.Add()`方法呼叫。

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

第一次 hello`bundles.Add()`陳述式會將指令碼組合在 hello 虛擬目錄`~/bundles/jquery`。 然後，開啟*_layout.cshtml\_Layout.cshtml* toosee hello 指令碼組合標記的呈現方式。 您應該能夠 toofind hello 遵循的 Razor 程式碼行：

    @Scripts.Render("~/bundles/jquery")

Hello Azure Web 角色中執行此 Razor 程式碼時，它會呈現`<script>`標記 hello 指令碼類似 toohello 下列組合：

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

不過，當它執行 Visual Studio 中輸入`F5`，它會分別轉譯 hello 配套中的每個指令碼檔案 （在上述的 hello 情況下，只有一個指令碼檔案是 hello 配套中）：

    <script src="/Scripts/jquery-1.10.2.js"></script>

這可讓您在開發環境中的 toodebug hello JavaScript 程式碼時降低並行的用戶端連線 （結合在一起） 並改進檔案下載效能 （縮小） 在生產環境中。 Azure CDN 整合功能很不錯 toopreserve 它。 此外，由於 hello 轉譯組合已經包含自動產生的版本字串，您需要 tooreplicate 的功能，因此 hello 每當您更新您的 jQuery 版本透過 NuGet，它可以在 hello 用戶端更新儘速可能的。

請遵循以下 toointegration ASP.NET 統合及縮製與您的 CDN 端點的 hello 步驟。

1. 回到*App_Start\BundleConfig.cs*，修改 hello`bundles.Add()`方法 toouse 不同[配套建構函式](http://msdn.microsoft.com/library/jj646464.aspx)，其中指定 CDN 位址。 toodo，取代 hello`RegisterBundles`方法定義，以下列程式碼的 hello:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    要確定 tooreplace `<yourCDNName>` hello 的 Azure CDN 的名稱。
   
    純文字的方式，在您要設定`bundles.UseCdn = true`並加入精心製作的 CDN URL tooeach 組合。 例如，hello 第一個建構函式在 hello 程式碼中：
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    是 hello 與相同：
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    這個建構函式會告知 ASP.NET 統合及縮製 toorender 個別的指令碼檔案偵錯時在本機，但使用 hello 指定有問題的 CDN 位址 tooaccess hello 指令碼。 不過，對於此謹慎建構的 CDN URL，請注意兩項重要特性：
   
   * 此 CDN url hello 原點`http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`，這是實際 hello 虛擬目錄的雲端服務中的 hello 指令碼組合。
   * 因為您使用 CDN 建構函式，hello hello 組合的 CDN 指令碼標記不再包含自動產生的 hello hello 轉譯 URL 中的版本字串。 每次 hello 指令碼組合會在您的 Azure CDN 的快取遺漏的已修改的 tooforce，您必須以手動方式產生唯一的版本字串。 在 hello 相同時間，此唯一的版本字串必須保持不變透過 hello 部署 toomaximize 在 Azure CDN 的快取點擊 hello 生命 hello 組合部署之後。
   * hello 查詢字串 v = < W.X.Y.Z > 提取從*Properties\AssemblyInfo.cs* Web 角色專案中。 您可以部署工作流程，其中包含每次發行 tooAzure 遞增 hello 組件版本。 或者，您可以修改*Properties\AssemblyInfo.cs*專案 tooautomatically 遞增 hello 版本字串中，每次建置時，使用 hello 萬用字元 ' *'。 例如：
     
        [assembly: AssemblyVersion("1.0.0.*")]
     
     產生的唯一字串 hello 存留期間部署的任何其他策略 toostreamline 運作此處所示。
2. 重新發佈 hello 雲端服務和存取 hello 首頁。
3. 檢視 hello hello 網頁的 HTML 程式碼。 您應該能夠 toosee hello CDN URL 轉譯，每次您重新發行變更 tooyour 雲端服務是唯一的版本字串。 例如：  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. 在 Visual Studio 中偵錯 Visual Studio 中的 hello 雲端服務輸入`F5`。，
5. 檢視 hello hello 網頁的 HTML 程式碼。 您仍然會看到每一個指令檔以個別方式轉譯，讓您在 Visual Studio 中享有一致的偵錯體驗。  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>CDN URL 的後援機制
當您的 Azure CDN 端點因任何原因失敗時，您會想網頁 toobe 智慧足夠 tooaccess 您的原始 Web 伺服器作為 hello 載入 JavaScript 或啟動程序的後援選項。 它是在您的網站，因為 tooCDN 無法使用，但提供的指令碼和樣式表更嚴重 toolose 重要頁面功能的嚴重 toolose 映像。

hello[配套](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx)類別包含內容呼叫[CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) ，可讓您的 CDN 失敗 tooconfigure hello 後援機制。 toouse 這個屬性，請遵循下列 hello 步驟：

1. 在 Web 角色專案中，開啟*App_Start\BundleConfig.cs*，其中每個新增 CDN URL[配套建構函式](http://msdn.microsoft.com/library/jj646464.aspx)，並讓 hello 下列反白顯示變更 tooadd 後援機制 toohello預設組合：  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    當`CdnFallbackExpression`是不是 null，指令碼會插入 hello HTML tootest 是否 hello 配套已順利載入，否則，請存取 hello 配套直接從 hello 原始 Web 伺服器。 這個屬性需要 toobe 集合 tooa JavaScript 運算式會測試是否會正確載入 hello 個別 CDN 組合。 hello 運算式需要 tootest 每個組合不同相應 toohello 內容。 如 hello 預設組合上述：
   
   * `window.jquery` 定義於 jquery-{version}.js 中
   * `$.validator` 定義於 jquery.validate.js 中
   * `window.Modernizr` 定義於 modernizer-{version}.js 中
   * `$.fn.modal` 定義於 bootstrap.js 中
     
     您可能已注意到我未設定 CdnFallbackExpression hello`~/Cointent/css`組合。 這是因為目前沒有[System.Web.Optimization 中的 bug](https://aspnetoptimization.codeplex.com/workitem/104) ，插入`<script>`標記而不是 hello 後援 CSS 預期的 hello`<link>`標記。
     
     不過，[Ember 顧問團](https://github.com/EmberConsultingGroup) (英文) 提供一套良好的[樣式套件組合後援](https://github.com/EmberConsultingGroup/StyleBundleFallback) (英文)。
2. CSS toouse hello 因應措施建立新的.cs 檔案在您 Web 角色專案*App_Start*資料夾稱為*StyleBundleExtensions.cs*，並將其內容取代 hello[從程式碼GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs)。
3. 在*App_Start\StyleFundleExtensions.cs*，重新命名 hello 命名空間 tooyour Web 角色的名稱 (例如**WebRole1**)。
4. 請返回太`App_Start\BundleConfig.cs`和上次修改 hello`bundles.Add`陳述式搭配下列反白顯示的程式碼的 hello:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    這個新的擴充方法會使用 hello tooinject 編寫指令碼 hello HTML toocheck hello DOM 中，符合類別名稱、 規則名稱和 hello CSS 組合和便在 2008 年後 toohello 原始 Web 伺服器時 toofind hello 相符項目中定義的規則值相同的概念。
5. 發佈一次 hello 雲端服務和存取 hello 首頁。
6. 檢視 hello hello 網頁的 HTML 程式碼。 您應該尋找類似 toohello 下列插入指令碼：    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    請注意，hello CSS 組合插入指令碼仍會包含從 hello hello 郵政編碼的地方剩餘`CdnFallbackExpression`hello 列中的屬性：

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    但由於 hello 第一部分 hello | |運算式一律會傳回 （在正上方的 hello 行），則為 true，hello document.write() 函式永遠不會執行。

## <a name="more-information"></a>相關資訊
* [Hello Azure 內容傳遞網路 (CDN) 的概觀](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [使用 Azure CDN](cdn-create-new-endpoint.md)
* [ASP.NET 統合和縮製](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
