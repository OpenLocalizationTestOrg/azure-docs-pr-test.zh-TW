組織使用更多的 [軟體即服務 (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) 應用程式來提高產能，因為雲端技術和工具變得更容易使用。 當 hello SaaS 應用程式的數目增加時，它會成為一項挑戰 hello 管理員 toomanage 帳戶和存取權限，並如 hello 使用者 tooremember 不同的密碼。 個別管理這些應用程式會建立額外的工作且安全性變低。

* Tookeep 追蹤的許多密碼通常 toouse 的員工較不安全，請寫下密碼，或是使用 hello 方法 tooremember 相同密碼跨多個帳戶。
* 當新員工報到或舊員工離職時，他們的所有帳戶都必須個別佈建或取消佈建。
* 此外，員工可能使用 SaaS 應用程式進行啟動他們的工作而不需要透過 IT，也就是說他們所建立自己的帳戶在 hello IT 系統管理員的系統上您尚未核准，且不監視。  

所有這些挑戰的解決方案就是單一登入 (SSO)。 它具有 hello 最簡單的方式 toomanage 多個應用程式，並提供使用者一致的登入體驗。 Azure Active Directory (Azure AD) 提供強固的 SSO 解決方案，且具有許多可用的預先整合應用程式，具有系統管理員的教學課程，tooquickly 設定新的應用程式並開始佈建使用者。

## <a name="how-does-azure-active-directory-integrate-apps"></a>Azure Active Directory 如何整合 App？
Azure AD 可讓您 toointegrate 您的應用程式和佈建的帳戶。 這可透過下列兩種方法之一來完成。

* 若 hello 應用程式已預先整合 hello 應用程式組件庫中，您可以瀏覽該入口網站 tooset 註冊應用程式，並設定 hello 設定 tooallow SSO。 任何組件庫應用程式中，您可以開始後續 hello 簡單逐步解說提供在 hello 應用程式庫和 hello Azure 入口網站 tooenable 單一登入。
* 如果 hello 應用程式不在 hello 組件庫中，您可以仍然設定大部分的應用程式做為自訂應用程式的 Azure AD 中。 這需要更多的位元技術專業知識 tooconfigure。 您可以加入支援 SAML 2.0 的任何應用程式做為同盟應用程式，或者加入具有 HTML 登入頁面的任何應用程式做為密碼 SSO 應用程式。

在 hello 案例，其中使用者已建立其自己帳戶 SaaS 應用程式不是由管理 IT 消費化、 hello [Cloud App Discovery](../articles/active-directory/active-directory-cloudappdiscovery-whatis.md)工具提供解決方案。 此工具會監視 hello web 流量 tooidentify 哪些應用程式正在使用整個 hello 組織，以及使用每個人員的 hello 數目。 IT 可以使用此資訊 toolearn 哪些應用程式 hello 使用者偏好，並決定哪些 toointegrate 至 Azure AD，sso。  

當您將應用程式整合到 Azure AD 時，您可以對應 hello 使用者建立的應用程式識別 tootheir 各自的 Azure AD 身分識別。  

