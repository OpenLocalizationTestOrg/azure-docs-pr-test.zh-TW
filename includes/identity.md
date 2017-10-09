管理身分識別就一樣重要 hello 公用雲端中，所以在內部部署。 與這個 toohelp，Azure 支援數種不同的雲端身分識別技術。 這些選項包括：

* 您可以使用使用 Azure 虛擬機器建立虛擬機器的 hello 雲端中執行 （通常稱為只 AD） 的 Windows Server Active Directory。 這種方法有意義您使用 Azure tooextend 時您的內部部署資料中心到 hello 的雲端。
* 您可以使用 Azure Active Directory toogive 使用者單一登入太[軟體即服務 (SaaS)](https://azure.microsoft.com/overview/what-is-saas/)應用程式。 例如，Microsoft Office 365 會使用這項技術，而且在 Azure 或其他雲端平台中執行的應用程式也可以使用此技術。
* Hello 中執行的應用程式雲端或內部部署可以使用 Azure Active Directory 存取控制 toolet 使用者登入使用從 Facebook、 Google、 Microsoft 和其他識別提供者的身分識別。

本文詳細說明下列三個選項。

## <a name="table-of-contents"></a>目錄
* [在虛擬機器中執行 Windows Server Active Directory](#adinvm)
* [使用 Azure Active Directory](#ad)
* [使用 Azure Active Directory 存取控制](#ac)

## <a name="adinvm"></a>在虛擬機器中執行 Windows Server Active Directory
在 Azure 虛擬機器中執行 Windows Server AD，與在內部部署中執行 Windows Server AD 非常類似。 [圖 1](#fig1) 顯示其外觀的典型範例。

![虛擬機器中的 Azure Active Directory](./media/identity/identity_01_ADinVM.png)

<a name="Fig1"></a>圖 1: Windows Server Active Directory 可以在使用 Azure 虛擬網路連接的 Azure 虛擬機器 tooan 組織的內部部署資料中心內執行。

Hello 範例所示，在 Windows Server AD 正在使用 Azure 虛擬機器，hello 平台的 IaaS 技術所建立的 Vm 中執行。 這些 Vm，以及幾個其他使用 Azure 虛擬網路的虛擬網路連接 tooan 在內部部署資料中心所組成。 hello 虛擬網路 carves 出 hello 透過虛擬私人網路 (VPN) 連線的內部部署網路互動的雲端虛擬機器的群組。 此可讓這些 Azure 虛擬機器看起來只是另一個子網路 toohello 在內部部署資料中心。 如 hello 圖所示，這些 Vm 的兩個正在執行 Windows Server AD 網域控制站。 hello hello 虛擬網路中其他虛擬機器可能在執行應用程式，例如 SharePoint，或以其他方式，例如使用用於開發和測試。 hello 在內部部署資料中心同時執行兩個 Windows Server AD 網域控制站。

有數個選項可以連接 hello 雲端與內部部署上執行中的 hello 網域控制站：

* 讓這些網域控制站全都屬於單一 Active Directory 網域。
* 建立不同 AD 網域內部和屬於 hello hello 雲端中相同的樹系。
* 建立不同的 AD 樹系中 hello 雲端和內部部署，然後連線使用跨樹系信任或 Windows Server Active Directory Federation Services (AD FS)，也可在虛擬機器中執行 Azure 上的 hello 樹系。

進行任何選擇，系統管理員應該確認在內部部署使用者的驗證要求，會因為 hello 連結 toohello 雲端可能 toobe 低於內部網路移 toocloud 網域控制站只在必要時。 連接雲端和內部部署網域控制站中的另一個因素 tooconsider 是複寫所產生的 hello 流量。 Hello 雲端中的網域控制站通常是在自己的 AD 站台，可讓系統管理員 tooschedule 頻率進行複寫。 Azure 流量送出 Azure 資料中心，雖然不位元組傳送中，可能會影響 hello 系統管理員的複寫選項的費用。 此外，值得一提的是，雖然 Azure 會提供自己的網域名稱系統 (DNS) 支援，但此服務是 Active Directory 所需的遺漏功能 (例如 Dynamic DNS 和 SRV 記錄支援)。 因為這個緣故，在 Azure 上執行 Windows Server AD 需要您自己的 DNS 伺服器 hello 雲端中的設定。

在幾個不同的情況下，於 Azure VM 中執行 Windows Server AD 是合理的。 這裡有一些範例：

* 如果您使用 Azure 虛擬機器，來延伸您自己的資料中心，您可能需要本機網域控制站 toohandle 項目，例如 Windows 整合式驗證要求或 LDAP 查詢的 hello 雲端中執行應用程式。 SharePoint，比方說，經常會與互動，Active Directory 中，也因此雖然可能 toorun SharePoint 伺服器陣列在 Azure 中使用內部部署目錄上，設定 hello 雲端中的網域控制站會大幅改善效能。 （它是重要 toorealize，這不一定是必要項目，不過，許多應用程式可以使用僅在內部部署網域控制站的 hello 雲端中順利執行）。
* 假設遠方分公司缺少 hello 資源 toorun 它自己的網域控制站。 現在，使用者必須驗證另一端的 hello world hello toodomain 控制站-登入很慢。 在 Azure 上執行 Active Directory 在接近的 Microsoft 資料中心可以加快這而不需要 hello 分公司中的多個伺服器。
* 使用 Azure 災害復原的組織可能會維護較少的作用中的 Vm 在 hello 雲端中，包括網域控制站。 接著可以準備 tooexpand 此站台為所需的 tootake 透過其他地方失敗。

此外，還有其他可能性。 例如，您不需要 tooconnect hello 雲端 tooan 中的 Windows Server AD 內部部署資料中心。 如果您想 toorun 提供一組特定使用者的 SharePoint 伺服器陣列，比方說，這些使用者會單獨使用以雲端為基礎的身分登入，您可能會在 Azure 上建立獨立樹系。 您使用此技術的方式取決於您的目的。 (如需使用 Windows Server AD 搭配 Azure 的詳細指引， [請參閱這裡](http://msdn.microsoft.com/library/windowsazure/jj156090.aspx))。

## <a name="ad"></a>使用 Azure Active Directory
隨著 SaaS 應用程式日益普及，因而引發一個明顯的問題：這些雲端型應用程式應使用哪種目錄服務？ Microsoft 的回應 toothat 問題是 Azure Active Directory。

有兩個主要選項 hello 雲端中使用這個目錄服務：

* 僅使用 SaaS 應用程式的個人和組織可以依賴 Azure Active Directory 作為其唯一目錄服務。
* 執行 Windows Server Active Directory 的組織可以連接其內部部署目錄 tooAzure Active Directory 中，再使用它 toogive 使用者單一登入 tooSaaS 應用程式。

[圖 2](#fig2)說明 hello 這兩個選項，其中的 Azure Active Directory 是只需要第一個。

![虛擬機器中的 Azure Active Directory](./media/identity/identity_02_AD.png)

<a name="fig2"></a>圖 2: Azure Active Directory 可讓組織的使用者單一登入 tooSaaS 應用程式，包括 Office 365。

如 hello 圖所示，Azure AD 是多租用戶服務。 這表示它可以同時支援許多不同的組織，以及儲存各組織的使用者相關目錄資訊。 在此範例中，組織 A 的使用者正嘗試 tooaccess SaaS 應用程式。 此應用程式可能屬於 Office 365 的一部分 (如 SharePoint Online)，或屬於其他應用程式 - 非 Microsoft 應用程式也可以使用此技術。 因為 Azure AD 支援 hello SAML 2.0 通訊協定，所有的要求從應用程式 hello 能力 toointeract 使用這項產業標準。 (事實上，使用 Azure AD 的應用程式可以在任何資料中心執行，而不限於 Azure 資料中心)。

hello 使用者存取 SaaS 應用程式 （步驟 1） 時，就會開始 hello 程序。 toouse 此應用程式，hello 使用者必須提供 Azure AD 所簽發的權杖。

此權杖會包含用來識別 hello 使用者的資訊和 Azure AD 數位簽章。 tooget hello 語彙基元，hello 使用者驗證自己 tooAzure AD 藉由提供使用者名稱和密碼 （步驟 2）。 然後 azure AD 傳回他只需要 hello 語彙基元 （步驟 3）。

此權杖會接著傳送 toohello SaaS 應用程式 （步驟 4），它會驗證 hello 權杖之簽章，並使用它的內容 （步驟 5）。 Hello 應用程式通常會使用 hello 權杖包含 toodecide 何種資訊 hello 允許使用者 tooaccess hello 身分識別資訊或可能是其他方式。

如果 hello 應用程式需要比 hello 權杖中包含的項目 hello 使用者的詳細資訊，它可以直接從 hello Azure AD Graph API （步驟 6），使用 Azure AD 要求此。 在 hello 初始版本的 Azure AD，hello 目錄結構描述是相當簡單： 它包含只使用者和群組以及它們之間的關聯性。 應用程式可以使用此資訊 toolearn，關於使用者之間的連線。 例如，假設應用程式需要 tooknow 負責這位使用者的管理員 toodecide 他是否允許的存取資料的 toosome 區塊。 它可以透過 Azure AD Graph API hello 透過查詢來了解這設定。

hello Graph API 會使用一般 RESTful 通訊協定，使其大部分的用戶端，包括行動裝置從直接 toouse。 hello API 也支援 hello OData，以更實用的方式加入之類的查詢語言 toolet 用戶端存取資料所定義的擴充功能。 (如需 OData 的詳細資訊，請參閱 [OData 簡介](http://download.microsoft.com/download/E/5/A/E5A59052-EE48-4D64-897B-5F7C608165B8/IntroducingOData.pdf))。Hello Graph API 可以使用的 toolearn 有關使用者之間的關聯性，因為它可讓應用程式了解內嵌 hello Azure AD （這就是為什麼它稱為 hello Graph API） 的特定組織的結構描述中的 hello 社交圖形。 與本身 tooauthenticate tooAzure AD Graph api 要求，應用程式使用 OAuth 2.0。

如果組織不使用 Windows Server Active Directory-它沒有在內部部署伺服器或網域-且僅依賴使用 Azure AD 雲端應用程式，使用剛這個雲端目錄會提供給 hello 公司使用者單一登入 tooall 其中。 雖然此種情況日益普遍，但大多數組織仍使用以 Windows Server Active Directory 建立的內部部署網域。 Azure AD 包含有用的角色 tooplay，為[圖 3](#fig3)顯示。

![虛擬機器中的 azure Active Directory](./media/identity/identity_03_AD.png)
<a id="fig3"></a>圖 3： 組織可以同盟 Windows Server Active Directory 與 Azure Active Directory toogive 及其使用者單一登入 tooSaaS 應用程式。

在此案例中，使用者在組織 B 會希望 tooaccess SaaS 應用程式。 她的做法之前，hello 組織的目錄系統管理員必須與 hello 圖所示，使用 AD FS 的 Azure AD 建立同盟關係。 這些系統管理員也必須設定 hello 組織的內部部署 Windows Server AD 和 Azure AD 之間資料同步處理。 這會自動複製到使用者和群組資訊從 hello 在內部部署目錄 tooAzure AD。 請注意，這可讓： hello 組織作用中，會將其內部部署目錄延伸到 hello 雲端。 結合 Windows Server AD 和 Azure AD 以這種方式可讓 hello 組織可以管理視為單一實體，同時仍能在內部使用量和 hello 雲端中的目錄服務。

toouse Azure AD，hello 使用者第一次登入時 tooher 在內部部署 Active Directory 網域如往常般 （步驟 1）。 當她嘗試 tooaccess hello SaaS 應用程式 （步驟 2） 時，hello 同盟程序會導致 Azure AD 發出她此應用程式 （步驟 3） 的語彙基元。 (如需同盟運作方式的詳細資訊，請參閱 [Windows 的宣告式身分識別：技術和案例](http://www.davidchappell.com/writing/white_papers/Claims-Based_Identity_for_Windows_v3.0--Chappell.docx)。)之前，此權杖會包含用來識別 hello 使用者的資訊和 Azure AD 數位簽章。 此權杖會接著傳送 toohello SaaS 應用程式 （步驟 4），它會驗證 hello 權杖之簽章，並使用它的內容 （步驟 5）。 在 hello 前述案例中，如果，SaaS 應用程式可以使用 hello 更多關於此使用者的 Graph API toolearn hello 和視需要 （步驟 6）。

Azure AD 目前並未完全取代內部部署 Windows Server AD。 如前所述，hello 雲端目錄有更簡單的結構描述，但它也遺失像是群組原則、 hello 能力 toostore 資訊需機器，以及支援的 LDAP。 （事實上，一部 Windows 電腦不能設定的使用者登入使用 Azure AD 但 tooit 的 toolet-這不是支援的案例）。相反地，Azure AD 的 hello 初始目標包括讓企業 hello 雲端中的使用者存取應用程式，而不會維護個別的登入和釋出內部部署目錄系統管理員以手動方式同步處理他們的內部部署目錄與每個 SaaS 應用程式會使用其組織。 經過一段時間，不過，預期這個雲端目錄服務 tooaddress 廣泛的案例。

## <a name="ac"></a>使用 Azure Active Directory 存取控制
以雲端為基礎的身分識別技術可以使用的 toosolve 各種問題。 Azure Active Directory 可以組織為使用者提供單一登入 toomultiple SaaS 應用程式，例如。 但 hello 雲端中的身分識別技術也可以用其他方式。

比方說，假設，應用程式希望其使用者登入使用多個所發行的權杖 toolet*身分識別提供者 (IdPs)*。 現今有為數眾多的身分識別提供者，包括 Facebook、Google、Microsoft 和其他提供者，而應用程式經常讓使用者使用上述其中一個身分識別進行登入。 應該應用程式大費 toomaintain 它自己的使用者和密碼清單時，它會改為依賴已經存在的識別身分？ 接受現有的身分識別可簡化生命週期作業的使用者有較少的使用者名稱和密碼 tooremember，和 hello 人員建立 hello 應用程式，不再需要 toomaintain 他們自己的使用者名稱和密碼的清單。

但是當每一個身分識別提供者簽發某種權杖時，這些權杖並不標準 - 每個 IdP 都有自己的格式。 此外，這些語彙基元中的 hello 資訊也不是標準。 希望 tooaccept 權杖發給，說出的應用程式、 Facebook、 Google、 和 Microsoft 面臨著每一種不同的格式寫入的唯一代碼 toohandle hello 挑戰。

為何要這麼做？ 何不建立一個媒介，以共通的身分識別資訊表示法產生單一權杖格式？ 這種方法會讓生活更簡單的 hello 開發人員建立應用程式，因為他們現在需要 toohandle 只有一種語彙基元。 Azure Active Directory 存取控制會完全，使用不同的語彙基元提供 hello 雲端中的媒介。 [圖 4](#fig4) 顯示其運作方式

![虛擬機器中的 azure Active Directory](./media/identity/identity_04_IdentityProviders.png)
<a id="fig4"></a>圖 4: Azure Active Directory 存取控制可讓不同的身分識別提供者所發行的應用程式 tooaccept 識別權杖。

使用者嘗試從瀏覽器 tooaccess hello 應用程式時，就會開始 hello 程序。 hello 應用程式重新導向自己的 IdP 她 tooan （和也信任該 hello 應用程式）。 她驗證自己 toothis IdP，例如輸入使用者名稱和密碼 （步驟 1），並 hello IdP 傳回包含她 （步驟 2） 的相關資訊的權杖。

如同 hello 圖所示，存取控制會支援各種不同雲端式 IdPs，包括 Google、 Yahoo、 Facebook、 Microsoft （先前稱為 Windows Live ID） 和任何 OpenID 提供者所建立的帳戶。 此外，還支援使用 Azure Active Directory 和 Windows Server Active Directory (透過與 AD FS 同盟) 建立的身分識別。 hello 的目標，是 toocover hello 最常使用的身分識別，是否正在發給 IdPs hello 雲端或內部部署中。

一旦 hello 使用者的瀏覽器具有從 IdP 她所選的 IdP 權杖，它會傳送此語彙基元 tooAccess 控制項 （步驟 3）。 存取控制驗證 hello 語彙基元，並確定它真的核發此 IdP，然後建立新的權杖，根據已針對此應用程式定義的 toohello 規則。 Azure Active Directory 中，例如存取控制是多租用戶的服務，但 hello 租用戶應用程式，而不是客戶組織。 每個應用程式可以如 hello 圖所示，取得自己的命名空間，而且可以定義授權和多個相關的各種規則。

每個應用程式的管理員可利用這些規則來定義應如何將各種 IdP 提供的權杖轉換為存取控制權杖。 例如，如果不同 IdP 以各種類型表示使用者名稱，則存取控制規則可以將這些類型轉換成一般使用者名稱類型。 存取控制，接著將此新語彙基元後 toohello 瀏覽器 （步驟 4），將它提交 toohello 應用程式 （步驟 5）。 一旦有 hello 存取控制權杖，hello 應用程式會驗證此語彙基元實際上由存取控制發出的則會使用其所含 （步驟 6） 的 hello 資訊。

此程序似乎有點複雜，而它實際上是生命簡單得多 hello creator hello 應用程式。 而非處理包含不同的資訊不同的語彙基元 hello 應用程式可接受時還是收到單一語彙基元熟悉的資訊發出多個身分識別提供者的身分識別。 此外，而不需要每個應用程式 toobe 設定 tootrust 各種 IdPs，存取控制會改為維護這些信任關聯性-應用程式只需要信任它。

很值得，沒有關於存取控制是繫結的 tooWindows-它可能也會由已接受唯一 Google 和 Facebook 身分識別的 Linux 應用程式。 而且，即使在存取控制是 hello Azure Active Directory 系列的一部分，您可以將它視為完全不同的服務，從 hello 前一節中所述的內容。 雖然這兩種技術會使用身分識別，但可解決相當不同的問題 （雖然 Microsoft 具有說，它會預期 toointegrate hello 兩個在某個時間點）。

對於幾乎所有應用程式而言，處理身分識別是相當重要的。 hello 目標存取控制是 toomake 它更容易，接受來自各種不同的身分識別提供者的身分識別開發人員 toocreate 應用程式。 將此服務放入 hello 雲端，Microsoft 已做出它可用 tooany 任何平台上執行的應用程式。

## <a name="about-hello-author"></a>關於 hello 作者
David Chappell 是 Chappell & Associates [www.davidchappell.com](http://www.davidchappell.com) (位於美國加州舊金山) 的主席。

