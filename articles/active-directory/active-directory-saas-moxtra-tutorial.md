<properties
	pageTitle="チュートリアル: Azure Active Directory と Moxtra の統合 | Microsoft Azure"
	description="Azure Active Directory と Moxtra の間でシングル サインオンを構成する方法について説明します。"
	services="active-directory"
	documentationCenter=""
	authors="jeevansd"
	manager="prasannas"
	editor=""/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="05/16/2016"
	ms.author="jeedes"/>


# チュートリアル: Azure Active Directory と Moxtra の統合

このチュートリアルの目的は、Moxtra と Azure Active Directory (Azure AD) を統合する方法を示すことです。<br>Moxtra と Azure AD の統合には、次の利点があります。

- Moxtra にアクセスする Azure AD ユーザーを制御できます。 
- ユーザーが自分の Azure AD アカウントで自動的に Moxtra にサインオン (シングル サインオン) できるようにします。
- 1 つの中央サイト (Azure クラシック ポータル) でアカウントを管理できます。

SaaS アプリと Azure AD の統合の詳細については、「[Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](active-directory-appssoaccess-whatis.md)」を参照してください。

## 前提条件 

Moxtra と Azure AD の統合を構成するには、次のものが必要です。

- Azure AD サブスクリプション
- Moxtra でのシングル サインオンが有効なサブスクリプション


> [AZURE.NOTE] このチュートリアルの手順をテストする場合、運用環境を使用しないことをお勧めします。


このチュートリアルの手順をテストするには、次の推奨事項に従ってください。

- 必要な場合を除き、運用環境は使用しないでください。
- Azure AD の評価環境がない場合は、[こちら](https://azure.microsoft.com/pricing/free-trial/)から 1 か月の評価版を入手できます。 

 
## シナリオの説明
このチュートリアルの目的は、テスト環境で Azure AD のシングル サインオンをテストできるようにすることです。<br>
このチュートリアルで説明するシナリオは、主に次の 2 つの要素で構成されています。

1. ギャラリーから Moxtra を追加する 
2. Azure AD シングル サインオンの構成とテスト


## ギャラリーから Moxtra を追加する
Azure AD への Moxtra の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に Moxtra を追加する必要があります。

**ギャラリーから Moxtra を追加するには、次の手順を実行します。**

1. **Azure クラシック ポータル**の左側のナビゲーション ウィンドウで、**[Active Directory]** をクリックします。 <br><br> 
![Active Directory][1]<br>

2. **[ディレクトリ]** の一覧から、ディレクトリ統合を有効にするディレクトリを選択します。

3. アプリケーション ビューを開くには、ディレクトリ ビューでトップ メニューの **[アプリケーション]** をクリックします。<br><br> 
![アプリケーション][2]<br>
4. ページの下部にある **[追加]** をクリックします。<br><br> 
![アプリケーション][3]<br>
5. **[実行する内容]** ダイアログで、**[ギャラリーからアプリケーションを追加します]** をクリックします。<br><br> 
![アプリケーション][4]<br>
6. 検索ボックスに、「**Moxtra**」と入力します。<br><br> 
![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_01.png)<br>
7. 結果ウィンドウで **[Moxtra]** を選択し、**[完了]** をクリックしてアプリケーションを追加します。
<br><br>
![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_02.png)<br>

##  Azure AD シングル サインオンの構成とテスト
このセクションの目的は、"Britta Simon" というテスト ユーザーに基づいて、Moxtra で Azure AD のシングル サインオンを構成し、テストする方法について説明することです。

シングル サインオンを機能させるには、Azure AD ユーザーに対応する Moxtra ユーザーが Azure AD で認識されている必要があります。言い換えると、Azure AD ユーザーと Moxtra の関連ユーザーの間で、リンク関係が確立されている必要があります。<br> 
このリンク関係は、Azure AD の **[ユーザー名]** の値を、Moxtra の **[Username]** の値として割り当てることで確立されます。
 
Moxtra で Azure AD のシングル サインオンを構成してテストするには、次の構成要素を完了する必要があります。

1. **[Azure AD シングル サインオンの構成](#configuring-azure-ad-single-single-sign-on)** - ユーザーがこの機能を使用できるようにします。
2. **[Azure AD のテスト ユーザーの作成](#creating-an-azure-ad-test-user)** - Britta Simon で Azure AD のシングル サインオンをテストします。
4. **[Moxtra のテスト ユーザーの作成](#creating-a-moxtra-test-user)** - Moxtra で Britta Simon に対応するユーザーを作成し、Azure AD の Britta Simon にリンクさせます。
5. **[Azure AD テスト ユーザーの割り当て](#assigning-the-azure-ad-test-user)** - Britta Simon が Azure AD のシングル サインオンを使用できるようにします。
5. **[シングル サインオンのテスト](#testing-single-sign-on)** - 構成が機能するかどうかを確認します。

### Azure AD シングル サインオンの構成

このセクションの目的は、Azure クラシック ポータルで Azure AD のシングル サインオンを有効にすることと、Moxtra アプリケーションでシングル サインオンを構成することです。

Moxtra アプリケーションでは、特定の形式の SAML アサーションを使用するため、カスタム属性マッピングを SAML トークン属性の構成に追加する必要があります。次のスクリーンショットはその例です。
<br><br> ![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_09.png)<br>



**Moxtra で Azure AD シングル サインオンを構成するには、次の手順に従います。**

1. Azure クラシック ポータルの **Moxtra** アプリケーション統合ページで **[シングル サインオンの構成]** をクリックし、**[シングル サインオンの構成]** ダイアログを開きます。
<br><br> ![シングル サインオンの構成][6] <br>

2. **[ユーザーの Moxtra へのアクセスを設定してください]** ページで、**[Microsoft Azure AD シングル サインオン]** を選択し、**[次へ]** をクリックします。
<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_03.png)<br>

3. **[アプリケーション設定の構成]** ダイアログ ページで、次の手順に従います。
<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_04.png) <br>

    a.**[サインオン URL]** テキストボックスに、URL **https://www.moxtra.com/service/#login** を入力します。

    b.**[次へ]** をクリックします。
 
 
4. **[Moxtra でのシングル サインオンの構成]** ページで、次の手順を実行します。
<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_05.png)<br>

    a.**[証明書のダウンロード]** をクリックし、コンピューターにファイルを保存します。

    b.**[次へ]** をクリックします。


1. 別の Web ブラウザー ウィンドウで、管理者として Moxtra 企業サイトにサインオンします。

1. 左のツールバーで、**[管理コンソール]、[SAML シングル サインオン]** の順にクリックし、**[新規]** をクリックします。 
<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) <br>


1. **[SAML]** ページで、次の手順を実行します。 
<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)<br>

    a.**[Name]** ボックスに、構成の名前を入力します (例: *SAML*)。

    b.Azure クラシック ポータルで、**[Moxtra でのシングル サインオンの構成]** ダイアログ ページの **[エンティティ ID]** の値をコピーし、**[IdP Entity ID]** ボックスに貼り付けます。

    c.Azure クラシック ポータルで、**[Moxtra でのシングル サインオンの構成]** ダイアログ ページの **[リモート ログイン URL]** の値をコピーし、**[Login URL]** ボックスに貼り付けます。

    d.**[AuthnContextClassRef]** ボックスに、「**urn:oasis:names:tc:SAML:2.0:ac:classes:Password**」と入力します。

    e.Azure クラシック ポータルの **[Moxtra でのシングル サインオンの構成]** ダイアログ ページで、**[名前識別子形式]** の値をコピーし、**[NameID Format]** ボックスに貼り付けます。

    f.ダウンロードした証明書をメモ帳で開き、その内容をコピーして、**[Certificate]** ボックスに貼り付けます。

    g.SAML 電子メール ドメイン テキストボックスに、SAML 電子メール ドメインを入力します。
    > [AZURE.NOTE] ドメインを検証するための手順を確認するには、下の **i** をクリックします。


    h.[**更新**] をクリックします。


6. Azure クラシック ポータルで、シングル サインオンの構成確認を選択し、**[次へ]** をクリックします。 
<br><br>![Azure AD のシングル サインオン][10]<br>

7. **[シングル サインオンの確認]** ページで **[完了]** をクリックします。
<br><br>![Azure AD のシングル サインオン][11]

1. カスタム属性マッピングを SAML トークン属性構成に追加するには、上部のメニューで、**[属性]** をクリックし、**[SAML トークン属性]** ダイアログを開きます。 
<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_general_80.png) <br>



1. 下の表のデータ行ごとに、次の手順を実行します。

    | 属性名 | 属性値 |
    | ---            | ---             |
    | firstname | givenname |
    | lastname | surname |
    | idpid | *<Azure クラシック ポータルの **[Moxtra でのシングル サインオンの構成]** ダイアログの **[エンティティ ID]** 値>* |

 
    a.[ユーザー属性の追加] をクリックします。<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_general_81.png) <br>

    b.**[ユーザー属性の追加]** ダイアログで、テーブルのその行に表示されている属性名と属性値を入力します。 <br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_general_82.png) <br>

    c.**[完了]** をクリックします。



1. **[変更の適用]** をクリックします。
<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_general_84.png)<br>








### Azure AD のテスト ユーザーの作成
このセクションの目的は、Azure クラシック ポータルで Britta Simon というテスト ユーザーを作成することです。<br> 
ユーザーの一覧で **[Britta Simon]** を選択します。<br><br>![Azure AD ユーザーの作成][20]<br>

**Azure AD でテスト ユーザーを作成するには、次の手順に従います。**

1. **Azure クラシック ポータル**の左側のナビゲーション ウィンドウで、**[Active Directory]** をクリックします。 
<br><br>![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-moxtra-tutorial/create_aaduser_09.png) <br> 

2. **[ディレクトリ]** の一覧から、ディレクトリ統合を有効にするディレクトリを選択します。

3. 上部のメニューで **[ユーザー]** をクリックして、ユーザーの一覧を表示します。
<br><br> ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) <br>
 
4. 下部にあるツール バーで **[ユーザーの追加]** をクリックして、**[ユーザーの追加]** ダイアログ ボックスを開きます。
<br><br> ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) <br>

5. **[このユーザーに関する情報の入力]** ダイアログ ページで、次の手順に従います。
<br><br> ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-moxtra-tutorial/create_aaduser_05.png) <br>

    a.[ユーザーの種類] として [組織内の新しいユーザー] を選択します。

    b.**[ユーザー名]** ボックスに「**BrittaSimon**」と入力します。

    c.**[次へ]** をクリックします。

6.  **[ユーザー プロファイル]** ダイアログ ページで、次の手順に従います。
<br><br>![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-moxtra-tutorial/create_aaduser_06.png) <br>
 
    a.**[名]** ボックスに「**Britta**」と入力します。

    b.**[姓]** ボックスに「**Simon**」と入力します。

    c.**[表示名]** ボックスに「**Britta Simon**」と入力します。

    d.**[ロール]** 一覧で **[ユーザー]** を選択します。
    e.**[次へ]** をクリックします。

7. **[一時パスワードの取得]** ダイアログ ページで、**[作成]** をクリックします。
<br><br> ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-moxtra-tutorial/create_aaduser_07.png) <br>
 
8. **[一時パスワードの取得]** ダイアログ ページで、次の手順に従います。
<br><br>![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-moxtra-tutorial/create_aaduser_08.png) <br>
  
    a.**[新しいパスワード]** の値を書き留めます。

    b.**[完了]** をクリックします。

  
 
### Moxtra テスト ユーザーの作成

このセクションの目的は、Moxtra で Britta Simon というユーザーを作成することです。

**Moxtra で Britta Simon というユーザーを作成するには、次の手順を実行します。**

1. Moxtra 企業サイトに管理者としてサインオンします。

1. 左のツールバーで、**[管理コンソール]、[ユーザー管理]** の順にクリックし、**[ユーザーの追加]** をクリックします。 
<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) <br>



1. **[Add User]** ダイアログで、次の手順を実行します。

    a.**[名]** ボックスに「**Britta**」と入力します。

    b.**[Last Name]** ボックスに「**Simon**」と入力します。

    c.**[電子メール]** ボックスに、Britta の Azure クラシックポータルの電子メール アドレスを入力します。

    d.**[事業部]** テキストボックスに、「**Dev**」と入力します。

    e.**[学科]** テキストボックスに、「**IT**」と入力します。

    f.**[管理者]** を選択します。

    g.**[追加]** をクリックします。





### Azure AD テスト ユーザーの割り当て

このセクションの目的は、Britta Simon に Moxtra へのアクセスを許可することで、このユーザーが Azure のシングル サインオンを使用できるようにすることです。
<br><br>![ユーザーの割り当て][200] <br>

**Moxtra に Britta Simon を割り当てるには、次の手順を実行します。**

1. Azure クラシック ポータルでアプリケーション ビューを開くために、ディレクトリ ビューでトップ メニューの **[アプリケーション]** をクリックします。 
<br><br>![ユーザーの割り当て][201] <br>

2. アプリケーションの一覧で **[Moxtra]** を選択します。
<br><br>![シングル サインオンの構成](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_50.png) <br>

1. 上部のメニューで **[ユーザー]** をクリックします。
<br><br>![ユーザーの割り当て][203] <br>

1. ユーザーの一覧で **[Britta Simon]** を選択します。

2. 下部にあるツール バーで **[割り当て]** をクリックします。
<br><br>![ユーザーの割り当て][205]



### シングル サインオンのテスト

このセクションの目的は、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストすることです。<br>
アクセス パネルで Moxtra のタイルをクリックすると、自動的に Moxtra アプリケーションにサインオンします。


## その他のリソース

* [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](active-directory-saas-tutorial-list.md)
* [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_205.png

<!---HONumber=AcomDC_0518_2016-->