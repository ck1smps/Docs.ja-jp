---
title: "ブートス トラップで美しい、応答性の高いサイトの構築"
author: ardalis
description: 
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: bd27832c-2877-4b7b-9337-e009361d845f
ms.technology: aspnet
ms.prod: asp.net-core
uid: client-side/bootstrap
ms.openlocfilehash: f89ad584600c3f12a936599de27f931aff0cd4b5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2017
---
# <a name="building-beautiful-responsive-sites-with-bootstrap"></a><span data-ttu-id="45780-103">ブートス トラップで美しい、応答性の高いサイトの構築</span><span class="sxs-lookup"><span data-stu-id="45780-103">Building beautiful, responsive sites with Bootstrap</span></span>

<a name="bootstrap-index"></a>

<span data-ttu-id="45780-104">によって[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="45780-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="45780-105">ブートス トラップは、現在の応答性の高い web アプリケーションを開発するための最も一般的なの web フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="45780-105">Bootstrap is currently the most popular web framework for developing responsive web applications.</span></span> <span data-ttu-id="45780-106">フロント エンドのデザインおよび開発またはエキスパートの初心者をしているかどうかは、さまざまな機能と、web サイトを持つユーザーのエクスペリエンスを向上できる利点を提供します。</span><span class="sxs-lookup"><span data-stu-id="45780-106">It offers a number of features and benefits that can improve your users' experience with your web site, whether you're a novice at front-end design and development or an expert.</span></span> <span data-ttu-id="45780-107">ブートス トラップは、CSS および JavaScript のファイルのセットとしては展開され、デスクトップにタブレットへ電話から効率的に、web サイトまたはアプリケーションのスケールを支援するよう設計されています。</span><span class="sxs-lookup"><span data-stu-id="45780-107">Bootstrap is deployed as a set of CSS and JavaScript files, and is designed to help your website or application scale efficiently from phones to tablets to desktops.</span></span>

## <a name="getting-started"></a><span data-ttu-id="45780-108">作業の開始</span><span class="sxs-lookup"><span data-stu-id="45780-108">Getting started</span></span>

<span data-ttu-id="45780-109">ブートス トラップで作業を開始するいくつかの方法はあります。</span><span class="sxs-lookup"><span data-stu-id="45780-109">There are several ways to get started with Bootstrap.</span></span> <span data-ttu-id="45780-110">Visual Studio で新しい web アプリケーションを開始する場合、は、事前インストールされているものが大文字のブートス トラップの ASP.NET Core の既定のスタート テンプレートを選択できます。</span><span class="sxs-lookup"><span data-stu-id="45780-110">If you're starting a new web application in Visual Studio, you can choose the default starter template for ASP.NET Core, in which case Bootstrap will come pre-installed:</span></span>

![スターター テンプレート ソリューション ビューでブートス トラップします。](bootstrap/_static/bootstrap-in-starter-template.png)

<span data-ttu-id="45780-112">ASP.NET Core にブートス トラップを追加するプロジェクトに追加することだけ*bower.json*依存関係として。</span><span class="sxs-lookup"><span data-stu-id="45780-112">Adding Bootstrap to an ASP.NET Core project is simply a matter of adding it to *bower.json* as a dependency:</span></span>

[!code-json[Main](../common/samples/WebApplication1/bower.json?highlight=5)]

<span data-ttu-id="45780-113">これは、ブートス トラップを ASP.NET Core プロジェクトに追加することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="45780-113">This is the recommended way to add Bootstrap to an ASP.NET Core project.</span></span>

<span data-ttu-id="45780-114">いくつかのパッケージ マネージャーは、Bower、npm、NuGet のいずれかを使用してブートス トラップをインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="45780-114">You can also install bootstrap using one of several package managers, such as Bower, npm, or NuGet.</span></span> <span data-ttu-id="45780-115">各ケースで、プロセス、基本的に同じです。</span><span class="sxs-lookup"><span data-stu-id="45780-115">In each case, the process is essentially the same:</span></span>

### <a name="bower"></a><span data-ttu-id="45780-116">Bower</span><span class="sxs-lookup"><span data-stu-id="45780-116">Bower</span></span>

```console
bower install bootstrap
```

### <a name="npm"></a><span data-ttu-id="45780-117">npm</span><span class="sxs-lookup"><span data-stu-id="45780-117">npm</span></span>

```console
npm install bootstrap
```

### <a name="nuget"></a><span data-ttu-id="45780-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="45780-118">NuGet</span></span>

```console
Install-Package bootstrap
```

> [!NOTE]
> <span data-ttu-id="45780-119">ASP.NET Core のブートス トラップは Bower を使用すると同じようにクライアント側の依存関係をインストールすることをお勧め (を使用して*bower.json*上記のように、)。</span><span class="sxs-lookup"><span data-stu-id="45780-119">The recommended way to install client-side dependencies like Bootstrap in ASP.NET Core is via Bower (using *bower.json*, as shown above).</span></span> <span data-ttu-id="45780-120">Npm/NuGet の使用は、ブートス トラップを追加して、ASP.NET の以前のバージョンを含む、web アプリケーションの他の種類を簡単にする方法を示すために表示されます。</span><span class="sxs-lookup"><span data-stu-id="45780-120">The use of npm/NuGet are shown to demonstrate how easily Bootstrap can be added to other kinds of web applications, including earlier versions of ASP.NET.</span></span>

<span data-ttu-id="45780-121">ブートス トラップのローカル バージョンを参照している場合は、それを使用する任意のページを参照する必要があります。</span><span class="sxs-lookup"><span data-stu-id="45780-121">If you're referencing your own local versions of Bootstrap, you'll need to reference them in any pages that will use it.</span></span> <span data-ttu-id="45780-122">実稼働環境では、CDN を使用してブートス トラップを参照する必要があります。</span><span class="sxs-lookup"><span data-stu-id="45780-122">In production you should reference bootstrap using a CDN.</span></span> <span data-ttu-id="45780-123">既定の ASP.NET サイト テンプレートで、 *_Layout.cshtml*ファイルはため次のようにします。</span><span class="sxs-lookup"><span data-stu-id="45780-123">In the default ASP.NET site template, the *_Layout.cshtml* file does so like this:</span></span>

[!code-html[Main](../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=9,13,51,59)]

> [!NOTE]
> <span data-ttu-id="45780-124">ブートス トラップの jQuery プラグインのいずれかを使用する場合は、jQuery を参照する必要があります。</span><span class="sxs-lookup"><span data-stu-id="45780-124">If you're going to be using any of Bootstrap's jQuery plugins, you will also need to reference jQuery.</span></span>

## <a name="basic-templates-and-features"></a><span data-ttu-id="45780-125">基本テンプレートと機能</span><span class="sxs-lookup"><span data-stu-id="45780-125">Basic templates and features</span></span>

<span data-ttu-id="45780-126">ブートス トラップの最も基本的なテンプレート似て、 *_Layout.cshtml*に示すファイル以上、かつ簡単にナビゲーションと、ページの残りの部分を表示するために場所用の基本的なメニューが含まれています。</span><span class="sxs-lookup"><span data-stu-id="45780-126">The most basic Bootstrap template looks very much like the *_Layout.cshtml* file shown above, and simply includes a basic menu for navigation and a place to render the rest of the page.</span></span>

### <a name="basic-navigation"></a><span data-ttu-id="45780-127">基本的なナビゲーション</span><span class="sxs-lookup"><span data-stu-id="45780-127">Basic navigation</span></span>

<span data-ttu-id="45780-128">既定のテンプレートのセットを使用する`<div>`上部のナビゲーション バーと、ページの本文を表示する要素。</span><span class="sxs-lookup"><span data-stu-id="45780-128">The default template uses a set of `<div>` elements to render a top navbar and the main body of the page.</span></span> <span data-ttu-id="45780-129">HTML5 を使用している場合は、1 つ目を置き換えることができます`<div>`とタグ付け、`<nav>`同じ効果を取得するタグがより正確なセマンティクス、します。</span><span class="sxs-lookup"><span data-stu-id="45780-129">If you're using HTML5, you can replace the first `<div>` tag with a `<nav>` tag to get the same effect, but with more precise semantics.</span></span>  <span data-ttu-id="45780-130">この最初の`<div>`他のいくつかのユーザーを使用する必要があるを参照してください。</span><span class="sxs-lookup"><span data-stu-id="45780-130">Within this first `<div>` you can see there are several others.</span></span> <span data-ttu-id="45780-131">最初に、 `<div>` "container"し、さらに 2 つのクラスを持つ`<div>`要素:「navbar ヘッダー」と「navbar 折りたたみ」です。</span><span class="sxs-lookup"><span data-stu-id="45780-131">First, a `<div>` with a class of "container", and then within that, two more `<div>` elements: "navbar-header" and "navbar-collapse".</span></span>  <span data-ttu-id="45780-132">ナビゲーション バー ヘッダー div には画面が特定最小の幅を示す 3 つの水平線を下回る場合に表示されるボタンが含まれています (いわゆる「ハンバーガー アイコン」) です。</span><span class="sxs-lookup"><span data-stu-id="45780-132">The navbar-header div includes a button that will appear when the screen is below a certain minimum width, showing 3 horizontal lines (a so-called "hamburger icon").</span></span> <span data-ttu-id="45780-133">純粋な HTML および CSS; を使用して、アイコンが表示されます。イメージは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="45780-133">The icon is rendered using pure HTML and CSS; no image is required.</span></span> <span data-ttu-id="45780-134">これは、それぞれのアイコンを表示するコード、<span>タグが白の横棒の 1 つの表示。</span><span class="sxs-lookup"><span data-stu-id="45780-134">This is the code that displays the icon, with each of the <span> tags rendering one of the white bars:</span></span>

```html
<button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
</button>
```

<span data-ttu-id="45780-135">左上隅に表示されるアプリケーション名も含まれています。</span><span class="sxs-lookup"><span data-stu-id="45780-135">It also includes the application name, which appears in the top left.</span></span>  <span data-ttu-id="45780-136">メイン ナビゲーション メニューは、によって表示される、 `<ul>` 2 番目の div 内の要素と概要や、自宅にお問い合わせくださいへのリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="45780-136">The main navigation menu is rendered by the `<ul>` element within the second div, and includes links to Home, About, and Contact.</span></span> <span data-ttu-id="45780-137">レジスタとログインの他のリンクは、線上の 29 _LoginPartial 行によって追加されます。</span><span class="sxs-lookup"><span data-stu-id="45780-137">Additional links for Register and Login are added by the _LoginPartial line on line 29.</span></span> <span data-ttu-id="45780-138">別の下のナビゲーション、各ページの本文が表示される`<div>`、マークの付いた"container"と「本文のコンテンツ」のクラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="45780-138">Below the navigation, the main body of each page is rendered in another `<div>`, marked with the "container" and "body-content" classes.</span></span> <span data-ttu-id="45780-139">次に示す単純な既定 _Layout ファイルでは、ページの内容は、ページし、単純なに関連付けられている特定のビューによって表示されます`<footer>`の末尾に追加された、`<div>`要素。</span><span class="sxs-lookup"><span data-stu-id="45780-139">In the simple default _Layout file shown here, the contents of the page are rendered by the specific View associated with the page, and then a simple `<footer>` is added to the end of the `<div>` element.</span></span>  <span data-ttu-id="45780-140">ページは、組み込みの表示方法を使用して確認できますこのテンプレート。</span><span class="sxs-lookup"><span data-stu-id="45780-140">You can see how the built-in About page appears using this template:</span></span>

![ページについて](bootstrap/_static/about-page-wide.png)

<span data-ttu-id="45780-142">折りたたまれたナビゲーション バーで、右、上に「ハンバーガー」ボタンでは、ウィンドウが特定の幅を下回った場合に表示されます。</span><span class="sxs-lookup"><span data-stu-id="45780-142">The collapsed navbar, with "hamburger" button in the top right, appears when the window drops below a certain width:</span></span>

![ハンバーガー メニューとページについて](bootstrap/_static/about-page-hamburger.png)

<span data-ttu-id="45780-144">ページの上部から下にスライドを垂直方向の引き出しのメニュー項目を表示するアイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="45780-144">Clicking the icon reveals the menu items in a vertical drawer that slides down from the top of the page:</span></span>

![ハンバーガー メニューとページに関する次のように展開します。](bootstrap/_static/about-page-hamburger-open.png)

### <a name="typography-and-links"></a><span data-ttu-id="45780-146">文字体裁やリンク</span><span class="sxs-lookup"><span data-stu-id="45780-146">Typography and links</span></span>

<span data-ttu-id="45780-147">ブートス トラップは、サイトの基本的な文字体裁、色、およびその CSS ファイルで書式設定のリンクを設定します。</span><span class="sxs-lookup"><span data-stu-id="45780-147">Bootstrap sets up the site's basic typography, colors, and link formatting in its CSS file.</span></span> <span data-ttu-id="45780-148">この CSS ファイルには、テーブル、ボタン、form 要素、イメージ、および複数の既定のスタイルが含まれています ([詳細](http://getbootstrap.com/css/))。</span><span class="sxs-lookup"><span data-stu-id="45780-148">This CSS file includes default styles for tables, buttons, form elements, images, and more ([learn more](http://getbootstrap.com/css/)).</span></span> <span data-ttu-id="45780-149">1 つの機能が特に便利ですが、グリッド レイアウト システムは、次に説明します。</span><span class="sxs-lookup"><span data-stu-id="45780-149">One particularly useful feature is the grid layout system, covered next.</span></span>

### <a name="grids"></a><span data-ttu-id="45780-150">グリッド</span><span class="sxs-lookup"><span data-stu-id="45780-150">Grids</span></span>

<span data-ttu-id="45780-151">ブートス トラップの最も一般的な機能の 1 つは、そのグリッド レイアウト システムです。</span><span class="sxs-lookup"><span data-stu-id="45780-151">One of the most popular features of Bootstrap is its grid layout system.</span></span> <span data-ttu-id="45780-152">最新の web アプリケーションを使用しないように、`<table>`レイアウト、代わりにこの要素の使用を制限する実際の表形式データへのタグ。</span><span class="sxs-lookup"><span data-stu-id="45780-152">Modern web applications should avoid using the `<table>` tag for layout, instead restricting the use of this element to actual tabular data.</span></span> <span data-ttu-id="45780-153">代わりに、列と行を配置できる一連の`<div>`要素および適切な CSS クラス。</span><span class="sxs-lookup"><span data-stu-id="45780-153">Instead, columns and rows can be laid out using a series of `<div>` elements and the appropriate CSS classes.</span></span> <span data-ttu-id="45780-154">これにはグリッドに表示する垂直方向に狭い画面など、携帯電話でのレイアウトを調整する機能など、この方法にいくつかの利点があります。</span><span class="sxs-lookup"><span data-stu-id="45780-154">There are several advantages to this approach, including the ability to adjust the layout of grids to display vertically on narrow screens, such as on phones.</span></span>

<span data-ttu-id="45780-155">[ブートス トラップのグリッド レイアウト システム](http://getbootstrap.com/css/#grid)12 個の列に基づきます。</span><span class="sxs-lookup"><span data-stu-id="45780-155">[Bootstrap's grid layout system](http://getbootstrap.com/css/#grid) is based on twelve columns.</span></span> <span data-ttu-id="45780-156">1、2、3、または 4 つの列に均等に分割できますされ、列の幅を 1 内に変更できるため、この数は選択された画面の垂直方向の幅の 12/です。</span><span class="sxs-lookup"><span data-stu-id="45780-156">This number was chosen because it can be divided evenly into 1, 2, 3, or 4 columns, and column widths can vary to within 1/12th of the vertical width of the screen.</span></span> <span data-ttu-id="45780-157">グリッド レイアウト システムを使用するには、コンテナーで開始する必要があります`<div>`行を追加および`<div>`次に示すように、します。</span><span class="sxs-lookup"><span data-stu-id="45780-157">To start using the grid layout system, you should begin with a container `<div>` and then add a row `<div>`, as shown here:</span></span>

```html
<div class="container">
    <div class="row">
        ...
    </div>
</div>
```

<span data-ttu-id="45780-158">次に、追加`<div>`列ごとに要素列の数を指定する`<div>`"col-md-"で始まる CSS クラスの一部として (12) 外占有する必要があります。</span><span class="sxs-lookup"><span data-stu-id="45780-158">Next, add additional `<div>` elements for each column, and specify the number of columns that `<div>` should occupy (out of 12) as part of a CSS class starting with "col-md-".</span></span> <span data-ttu-id="45780-159">たとえば、単に等しいサイズの 2 つの列がある場合は、それぞれの「col md 6」のクラスを使用するは。</span><span class="sxs-lookup"><span data-stu-id="45780-159">For instance, if you want to simply have two columns of equal size, you would use a class of "col-md-6" for each one.</span></span> <span data-ttu-id="45780-160">ここでは"md"の短縮形「中」は、デスクトップ コンピューターの標準サイズの表示サイズを指します。</span><span class="sxs-lookup"><span data-stu-id="45780-160">In this case "md" is short for "medium" and refers to standard-sized desktop computer display sizes.</span></span> <span data-ttu-id="45780-161">4 つの異なるオプションから選択でき、それぞれに使用する上位の幅 (ため、画面の幅に関係なく修正するレイアウトを設定する場合、xs クラスだけを指定することができます) をオーバーライドしない限り、します。</span><span class="sxs-lookup"><span data-stu-id="45780-161">There are four different options you can choose from, and each will be used for higher widths unless overridden (so if you want the layout to be fixed regardless of screen width, you can just specify xs classes).</span></span>

<span data-ttu-id="45780-162">CSS クラスのプレフィックス</span><span class="sxs-lookup"><span data-stu-id="45780-162">CSS Class Prefix</span></span> | <span data-ttu-id="45780-163">デバイス層</span><span class="sxs-lookup"><span data-stu-id="45780-163">Device Tier</span></span> | <span data-ttu-id="45780-164">幅</span><span class="sxs-lookup"><span data-stu-id="45780-164">Width</span></span>
:---: | :---: | :---:
<span data-ttu-id="45780-165">col-xs-</span><span class="sxs-lookup"><span data-stu-id="45780-165">col-xs-</span></span> | <span data-ttu-id="45780-166">携帯電話</span><span class="sxs-lookup"><span data-stu-id="45780-166">Phones</span></span> | <span data-ttu-id="45780-167">< 768px</span><span class="sxs-lookup"><span data-stu-id="45780-167">< 768px</span></span>
<span data-ttu-id="45780-168">col-sm-</span><span class="sxs-lookup"><span data-stu-id="45780-168">col-sm-</span></span> | <span data-ttu-id="45780-169">タブレット</span><span class="sxs-lookup"><span data-stu-id="45780-169">Tablets</span></span> | <span data-ttu-id="45780-170">> = 768px</span><span class="sxs-lookup"><span data-stu-id="45780-170">>= 768px</span></span>
<span data-ttu-id="45780-171">col-md-</span><span class="sxs-lookup"><span data-stu-id="45780-171">col-md-</span></span> | <span data-ttu-id="45780-172">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="45780-172">Desktops</span></span> | <span data-ttu-id="45780-173">> = 992px</span><span class="sxs-lookup"><span data-stu-id="45780-173">>= 992px</span></span>
<span data-ttu-id="45780-174">col-lg-</span><span class="sxs-lookup"><span data-stu-id="45780-174">col-lg-</span></span> | <span data-ttu-id="45780-175">大規模なデスクトップの表示</span><span class="sxs-lookup"><span data-stu-id="45780-175">Larger Desktop Displays</span></span> | <span data-ttu-id="45780-176">> = 1200px</span><span class="sxs-lookup"><span data-stu-id="45780-176">>= 1200px</span></span>

<span data-ttu-id="45780-177">2 つの列両方「col-md-6」、結果として得られるレイアウトをデスクトップの解像度で 2 つの列となりますが、容量の小さなデバイス (または、デスクトップの幅の狭いブラウザーのウィンドウ) で、ユーザーが簡単に確認できるように表示されるときにこれら 2 つの列が垂直方向に積み重ねを指定する場合水平方向にスクロールする必要がないコンテンツ。</span><span class="sxs-lookup"><span data-stu-id="45780-177">When specifying two columns both with "col-md-6" the resulting layout will be two columns at desktop resolutions, but these two columns will stack vertically when rendered on smaller devices (or a narrower browser window on a desktop), allowing users to easily view content without the need to scroll horizontally.</span></span>

<span data-ttu-id="45780-178">ブートス トラップは常に既定値 1 列のレイアウトでは、のみ 1 つ以上の列を表示するときに列を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="45780-178">Bootstrap will always default to a single-column layout, so you only need to specify columns when you want more than one column.</span></span> <span data-ttu-id="45780-179">明示的に指定するだけの時間、 `<div>` 12 のすべての列をより大きなデバイス層の動作をオーバーライドすることです。</span><span class="sxs-lookup"><span data-stu-id="45780-179">The only time you would want to explicitly specify that a `<div>` take up all 12 columns would be to override the behavior of a larger device tier.</span></span> <span data-ttu-id="45780-180">複数のデバイス層クラスを指定する場合は、特定の時点で列の描画をリセットする必要があります。</span><span class="sxs-lookup"><span data-stu-id="45780-180">When specifying multiple device tier classes, you may need to reset the column rendering at certain points.</span></span> <span data-ttu-id="45780-181">特定のビューポート内に表示される clearfix div を追加することを実現できますこれには、次に示すように。</span><span class="sxs-lookup"><span data-stu-id="45780-181">Adding a clearfix div that is only visible within a certain viewport can achieve this, as shown here:</span></span>

![ナローとワイドのビューポートのグリッド](bootstrap/_static/narrow-and-wide-viewport-grid.png)

<span data-ttu-id="45780-183">上記の例では、1 と 2 行を共有、レイアウトでは、「md」、2 および 3 は"xs"レイアウト内行を共有します。</span><span class="sxs-lookup"><span data-stu-id="45780-183">In the above example, One and Two share a row in the "md" layout, while Two and Three share a row in the "xs" layout.</span></span> <span data-ttu-id="45780-184">なし、clearfix `<div>`2 と 3 では、その"xs"ビュー (1 つだけ、4、および 5 が示されているメモ) では正しく表示されないは。</span><span class="sxs-lookup"><span data-stu-id="45780-184">Without the clearfix `<div>`, Two and Three are not shown correctly in the "xs" view (note that only One, Four, and Five are shown):</span></span>

![clearfix を使用せずグリッド](bootstrap/_static/grid-without-clearfix.png)

<span data-ttu-id="45780-186">この例では、1 つの行のみで`<div>`を使用しているとブートス トラップもほとんどの場合、レイアウトや、列の重なりに関して、正しいこと。</span><span class="sxs-lookup"><span data-stu-id="45780-186">In this example, only a single row `<div>` was used, and Bootstrap still mostly did the right thing with regard to the layout and stacking of the columns.</span></span> <span data-ttu-id="45780-187">通常、行を指定する必要があります`<div>`水平行ごとに、レイアウトを必要として、もちろんブートス トラップのグリッド内で互いを入れ子にすることができます。</span><span class="sxs-lookup"><span data-stu-id="45780-187">Typically, you should specify a row `<div>` for each horizontal row your layout requires, and of course you can nest Bootstrap grids within one another.</span></span> <span data-ttu-id="45780-188">操作を実行すると、入れ子になった各グリッドは、列のクラスを使用して分割することができますし、それが置かれている、要素の幅の 100% を占有します。</span><span class="sxs-lookup"><span data-stu-id="45780-188">When you do, each nested grid will occupy 100% of the width of the element in which it is placed, which can then be subdivided using column classes.</span></span>

### <a name="jumbotron"></a><span data-ttu-id="45780-189">Jumbotron</span><span class="sxs-lookup"><span data-stu-id="45780-189">Jumbotron</span></span>

<span data-ttu-id="45780-190">Visual Studio 2012 または 2013 の既定の ASP.NET MVC テンプレートを使用している場合は、アクションで Jumbotron 可能性があります見てきました。</span><span class="sxs-lookup"><span data-stu-id="45780-190">If you've used the default ASP.NET MVC templates in Visual Studio 2012 or 2013, you've probably seen the Jumbotron in action.</span></span> <span data-ttu-id="45780-191">大規模な背景イメージ、アクション、回転、または類似の要素への呼び出しを表示する使用できるページの大規模な全角セクションを参照します。</span><span class="sxs-lookup"><span data-stu-id="45780-191">It refers to a large full-width section of a page that can be used to display a large background image, a call to action, a rotator, or similar elements.</span></span> <span data-ttu-id="45780-192">Jumbotron をページに追加するには追加、 `<div>` "jumbotron"のクラスを提供し、コンテナーに配置`<div>`内のコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="45780-192">To add a jumbotron to a page, simply add a `<div>` and give it a class of "jumbotron", then place a container `<div>` inside and add your content.</span></span>  <span data-ttu-id="45780-193">標準のバージョンが表示されます、メインの見出しに、jumbotron を使用するページを簡単に調整おできます。</span><span class="sxs-lookup"><span data-stu-id="45780-193">We can easily adjust the standard About page to use a jumbotron for the main headings it displays:</span></span>

![jumbotron 例](bootstrap/_static/jumbotron.png)

### <a name="buttons"></a><span data-ttu-id="45780-195">ボタン</span><span class="sxs-lookup"><span data-stu-id="45780-195">Buttons</span></span>

<span data-ttu-id="45780-196">既定のボタンのクラスとそれぞれの色は、次の図に表示されます。</span><span class="sxs-lookup"><span data-stu-id="45780-196">The default button classes and their colors are shown in the figure below.</span></span>

![テーマが適用されたボタン](bootstrap/_static/theme-buttons.png)

### <a name="badges"></a><span data-ttu-id="45780-198">バッジ</span><span class="sxs-lookup"><span data-stu-id="45780-198">Badges</span></span>

<span data-ttu-id="45780-199">バッジは、ナビゲーション項目の横にある小さな、通常は数値のコールアウトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="45780-199">Badges refer to small, usually numeric callouts next to a navigation item.</span></span> <span data-ttu-id="45780-200">これらは、さまざまなメッセージまたは通知を待機している、または更新プログラムの有無にあります。</span><span class="sxs-lookup"><span data-stu-id="45780-200">They can indicate a number of messages or notifications waiting, or the presence of updates.</span></span> <span data-ttu-id="45780-201">追加するだけでは、このようなバッジを指定する、 <span> 「バッジ」のクラスを使用したテキストを格納します。</span><span class="sxs-lookup"><span data-stu-id="45780-201">Specifying such badges is as simple as adding a <span> containing the text, with a class of "badge":</span></span>

![テーマのバッジ](bootstrap/_static/theme-badges.png)

### <a name="alerts"></a><span data-ttu-id="45780-203">アラート</span><span class="sxs-lookup"><span data-stu-id="45780-203">Alerts</span></span>

<span data-ttu-id="45780-204">アプリケーションのユーザーに何らかの通知、警告またはエラー メッセージを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="45780-204">You may need to display some kind of notification, alert, or error message to your application's users.</span></span> <span data-ttu-id="45780-205">標準のアラートのクラスが便利です。</span><span class="sxs-lookup"><span data-stu-id="45780-205">That's where the standard alert classes are useful.</span></span>  <span data-ttu-id="45780-206">関連付けられている色スキームの 4 つの異なる重要度レベルです。</span><span class="sxs-lookup"><span data-stu-id="45780-206">There are four different severity levels with associated color schemes:</span></span>

![テーマのアラート](bootstrap/_static/theme-alerts.png)

### <a name="navbars-and-menus"></a><span data-ttu-id="45780-208">Navbars およびメニュー</span><span class="sxs-lookup"><span data-stu-id="45780-208">Navbars and menus</span></span>

<span data-ttu-id="45780-209">レイアウトには、標準的なナビゲーション バーでは、既に含まれていますが、ブートス トラップのテーマは、その他のスタイル指定オプションをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="45780-209">Our layout already includes a standard navbar, but the Bootstrap theme supports additional styling options.</span></span> <span data-ttu-id="45780-210">水平方向にな場合はするが、サブ ナビゲーションを追加することもの項目をポップアップ メニューではなく、ナビゲーション バーを垂直に表示することも簡単にできます。</span><span class="sxs-lookup"><span data-stu-id="45780-210">We can also easily opt to display the navbar vertically rather than horizontally if that's preferred, as well as adding sub-navigation items in flyout menus.</span></span> <span data-ttu-id="45780-211">タブ ストリップのように、簡単なナビゲーション メニューは、上に構築されます。</span><span class="sxs-lookup"><span data-stu-id="45780-211">Simple navigation menus, like tab strips, are built on top of</span></span> <ul> <span data-ttu-id="45780-212">要素です。</span><span class="sxs-lookup"><span data-stu-id="45780-212">elements.</span></span> <span data-ttu-id="45780-213">これらは、だけに CSS クラス"nav"、「ナビゲーション タブ」となるため、非常に簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="45780-213">These can be created very simply by just providing them with the CSS classes "nav" and "nav-tabs":</span></span>

![テーマが適用された tabstrips](bootstrap/_static/theme-tabstrips.png)

<span data-ttu-id="45780-215">Navbars は同様に、組み込まれていますが、もう少し複雑です。</span><span class="sxs-lookup"><span data-stu-id="45780-215">Navbars are built similarly, but are a bit more complex.</span></span>  <span data-ttu-id="45780-216">起動時に、`<nav>`または`<div>`要素の残りの部分を保持するコンテナー div を「ナビゲーション バー」のクラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="45780-216">They start with a `<nav>` or `<div>` with a class of "navbar", within which a container div holds the rest of the elements.</span></span> <span data-ttu-id="45780-217">このページが含まれています、ナビゲーション バーには、ヘッダーに既に: 次のように展開されるだけで、このドロップダウン メニューのサポートの追加。</span><span class="sxs-lookup"><span data-stu-id="45780-217">Our page includes a navbar in its header already – the one shown below simply expands on this, adding support for a dropdown menu:</span></span>

![テーマが適用された navbars](bootstrap/_static/theme-navbars.png)

### <a name="additional-elements"></a><span data-ttu-id="45780-219">追加の要素</span><span class="sxs-lookup"><span data-stu-id="45780-219">Additional elements</span></span>

<span data-ttu-id="45780-220">既定のテーマは、ストライプのビューのサポートなど、適切に書式設定されたスタイルの HTML テーブルを表示するも使用できます。</span><span class="sxs-lookup"><span data-stu-id="45780-220">The default theme can also be used to present HTML tables in a nicely formatted style, including support for striped views.</span></span> <span data-ttu-id="45780-221">同じように、ボタンのスタイルを使用してラベルがあります。</span><span class="sxs-lookup"><span data-stu-id="45780-221">There are labels with styles that are similar to those of the buttons.</span></span> <span data-ttu-id="45780-222">標準の HTML を超える追加のスタイル指定オプションをサポートするカスタムのドロップダウン メニューを作成する`<select>`、要素とその要素の既定のスターター サイトが既に使用して 1 つのような Navbars です。</span><span class="sxs-lookup"><span data-stu-id="45780-222">You can create custom Dropdown menus that support additional styling options beyond the standard HTML `<select>` element, along with Navbars like the one our default starter site is already using.</span></span> <span data-ttu-id="45780-223">進行状況バーが必要な場合は、いくつかのスタイルを選択、だけでなくグループの一覧およびパネルにタイトルと内容を組み込むことがあります。</span><span class="sxs-lookup"><span data-stu-id="45780-223">If you need a progress bar, there are several styles to choose from, as well as List Groups and panels that include a title and content.</span></span>  <span data-ttu-id="45780-224">標準のブートス トラップ テーマは、ここで追加オプションを探索します。</span><span class="sxs-lookup"><span data-stu-id="45780-224">Explore additional options within the standard Bootstrap Theme here:</span></span>

[<span data-ttu-id="45780-225">http://getbootstrap.com/examples/theme/</span><span class="sxs-lookup"><span data-stu-id="45780-225">http://getbootstrap.com/examples/theme/</span></span>](http://getbootstrap.com/examples/theme/)

## <a name="more-themes"></a><span data-ttu-id="45780-226">多くのテーマ</span><span class="sxs-lookup"><span data-stu-id="45780-226">More themes</span></span>

<span data-ttu-id="45780-227">色とスタイル アプリケーションのニーズに合わせて調整する、CSS の一部またはすべてをオーバーライドすることで、標準のブートス トラップのテーマを拡張することができます。</span><span class="sxs-lookup"><span data-stu-id="45780-227">You can extend the standard Bootstrap theme by overriding some or all of its CSS, adjusting the colors and styles to suit your own application's needs.</span></span> <span data-ttu-id="45780-228">既製のテーマから開始したい場合は、(をさまざまな商用のテーマを持つ) WrapBootstrap.com Bootswatch.com (を無料のテーマを利用できます) などのブートス トラップのテーマでのオンライン特殊化を使用できるいくつかのテーマ ギャラリーがあります。</span><span class="sxs-lookup"><span data-stu-id="45780-228">If you'd like to start from a ready-made theme, there are several theme galleries available online that specialize in Bootstrap themes, such as WrapBootstrap.com (which has a variety of commercial themes) and Bootswatch.com (which offers free themes).</span></span>  <span data-ttu-id="45780-229">使用可能な有料のテンプレートの一部は、豊富なグラフおよびゲージでの管理用のメニューのおよびダッシュ ボードの豊富なサポートなど、基本的なブートス トラップのテーマの上に機能が大幅に向上を提供します。</span><span class="sxs-lookup"><span data-stu-id="45780-229">Some of the paid templates available provide a great deal of functionality on top of the basic Bootstrap theme, such as rich support for administrative menus, and dashboards with rich charts and gauges.</span></span> <span data-ttu-id="45780-230">人気のある有料テンプレートの一例が、Inspinia、現在の売り上げが 18 ドル、AngularJS および静的な HTML バージョンに加え、ASP.NET MVC5 テンプレートが含まれます。</span><span class="sxs-lookup"><span data-stu-id="45780-230">An example of a popular paid template is Inspinia, currently for sale for $18, which includes an ASP.NET MVC5 template in addition to AngularJS and static HTML versions.</span></span> <span data-ttu-id="45780-231">サンプルのスクリーン ショットを次に示します。</span><span class="sxs-lookup"><span data-stu-id="45780-231">A sample screenshot is shown below.</span></span>

![例のテーマ inspinia](bootstrap/_static/theme-inspinia.png)

<span data-ttu-id="45780-233">ブートス トラップのテーマを変更する場合は、配置、 *bootstrap.css*でテーマのファイル、 **wwwroot/css**フォルダー内の参照を変更および*_Layout.cshtml*指定します。</span><span class="sxs-lookup"><span data-stu-id="45780-233">If you want to change your Bootstrap theme, put the *bootstrap.css* file for the theme you want in the **wwwroot/css** folder and change the references in *_Layout.cshtml* to point it.</span></span>  <span data-ttu-id="45780-234">すべての環境へのリンクを変更します。</span><span class="sxs-lookup"><span data-stu-id="45780-234">Change the links for all environments:</span></span>

```html
<environment names="Development">
    <link rel="stylesheet" href="~/css/bootstrap.css" />
```

```html
<environment names="Staging,Production">
    <link rel="stylesheet" href="~/css/bootstrap.min.css" />
```

<span data-ttu-id="45780-235">空き例では、使用可能なからここで開始できます、独自のダッシュ ボードを作成する場合: [http://getbootstrap.com/examples/dashboard/](http://getbootstrap.com/examples/dashboard/)です。</span><span class="sxs-lookup"><span data-stu-id="45780-235">If you want to build your own dashboard, you can start from the free example available here: [http://getbootstrap.com/examples/dashboard/](http://getbootstrap.com/examples/dashboard/).</span></span>

## <a name="components"></a><span data-ttu-id="45780-236">コンポーネント</span><span class="sxs-lookup"><span data-stu-id="45780-236">Components</span></span>

<span data-ttu-id="45780-237">ブートス トラップにはだけでなく、既に説明したこれらの要素には、さまざまなサポートが含まれています[UI の組み込みコンポーネント](http://getbootstrap.com/components/)です。</span><span class="sxs-lookup"><span data-stu-id="45780-237">In addition to those elements already discussed, Bootstrap includes support for a variety of [built-in UI components](http://getbootstrap.com/components/).</span></span>

### <a name="glyphicons"></a><span data-ttu-id="45780-238">Glyphicons</span><span class="sxs-lookup"><span data-stu-id="45780-238">Glyphicons</span></span>

<span data-ttu-id="45780-239">ブートス トラップには Glyphicons からアイコン セットが含まれています ([http://glyphicons.com](http://glyphicons.com))、200 を超えるアイコン自由に、ブートス トラップが有効な web アプリケーション内で使用可能にします。</span><span class="sxs-lookup"><span data-stu-id="45780-239">Bootstrap includes icon sets from Glyphicons ([http://glyphicons.com](http://glyphicons.com)), with over 200 icons freely available for use within your Bootstrap-enabled web application.</span></span> <span data-ttu-id="45780-240">小さなサンプルだけを次に示します。</span><span class="sxs-lookup"><span data-stu-id="45780-240">Here's just a small sample:</span></span>

![Glyphicons](bootstrap/_static/theme-glyphicons.png)

### <a name="input-groups"></a><span data-ttu-id="45780-242">入力のグループ</span><span class="sxs-lookup"><span data-stu-id="45780-242">Input groups</span></span>

<span data-ttu-id="45780-243">入力グループを使用する追加のテキストの input 要素を持つボタン バンドルより直観的な経験を持つユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="45780-243">Input groups allow bundling of additional text or buttons with an input element, providing the user with a more intuitive experience:</span></span>

![入力のグループ](bootstrap/_static/input-groups.png)

### <a name="breadcrumbs"></a><span data-ttu-id="45780-245">階層リンク</span><span class="sxs-lookup"><span data-stu-id="45780-245">Breadcrumbs</span></span>

<span data-ttu-id="45780-246">パンくずリストは、共通の UI コンポーネントが、最近の履歴や、サイトのナビゲーション階層内の深さが、ユーザーを表示するために使用します。</span><span class="sxs-lookup"><span data-stu-id="45780-246">Breadcrumbs are a common UI component used to show a user their recent history or depth within a site's navigation hierarchy.</span></span> <span data-ttu-id="45780-247">いずれかに「階層リンク バー」クラスを適用することで簡単に追加`<ol>`リスト要素。</span><span class="sxs-lookup"><span data-stu-id="45780-247">Add them easily by applying the "breadcrumb" class to any `<ol>` list element.</span></span> <span data-ttu-id="45780-248">「改ページ調整」クラスを使用して、改ページの組み込みサポートを含める、`<ul>`内の要素、`<nav>`です。</span><span class="sxs-lookup"><span data-stu-id="45780-248">Include built-in support for pagination by using the "pagination" class on a `<ul>` element within a `<nav>`.</span></span> <span data-ttu-id="45780-249">使用して応答埋め込みスライド ショーとビデオの追加`<iframe>`、 `<embed>`、 `<video>`、または`<object>`要素で、ブートス トラップのスタイルが自動的にします。</span><span class="sxs-lookup"><span data-stu-id="45780-249">Add responsive embedded slideshows and video by using `<iframe>`, `<embed>`, `<video>`, or `<object>` elements, which Bootstrap will style automatically.</span></span> <span data-ttu-id="45780-250">特定の縦横比を指定するには、"埋め込む-応答-16by9"などの特定のクラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="45780-250">Specify a particular aspect ratio by using specific classes like "embed-responsive-16by9".</span></span>

## <a name="javascript-support"></a><span data-ttu-id="45780-251">JavaScript のサポート</span><span class="sxs-lookup"><span data-stu-id="45780-251">JavaScript support</span></span>

<span data-ttu-id="45780-252">ブートス トラップの JavaScript ライブラリには、アプリケーション内でプログラムでは、その動作を制御できるため、含まれるコンポーネントの API のサポートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="45780-252">Bootstrap's JavaScript library includes API support for the included components, allowing you to control their behavior programmatically within your application.</span></span> <span data-ttu-id="45780-253">さらに、 *bootstrap.js*十数か所を含むカスタム jQuery プラグイン、遷移、モーダル ダイアログ ボックスのような機能の追加 (ドキュメントで、ユーザーがスクロールされたといったに基づいてスタイルの更新) の検出をスクロールします。折りたたみ動作、手荷物の受け取り場所、およびメニュー画面をオフ スクロールがないため、ウィンドウを付加します。</span><span class="sxs-lookup"><span data-stu-id="45780-253">In addition, *bootstrap.js* includes over a dozen custom jQuery plugins, providing additional features like transitions, modal dialogs, scroll detection (updating styles based on where the user has scrolled in the document), collapse behavior, carousels, and affixing menus to the window so they do not scroll off the screen.</span></span> <span data-ttu-id="45780-254">についての詳細を参照してください: ブートス トラップに組み込まれている JavaScript アドオンのすべてを網羅するための十分なスペースがない[http://getbootstrap.com/javascript/](http://getbootstrap.com/javascript/)です。</span><span class="sxs-lookup"><span data-stu-id="45780-254">There's not sufficient room to cover all of the JavaScript add-ons built into Bootstrap – to learn more please visit [http://getbootstrap.com/javascript/](http://getbootstrap.com/javascript/).</span></span>

## <a name="summary"></a><span data-ttu-id="45780-255">概要</span><span class="sxs-lookup"><span data-stu-id="45780-255">Summary</span></span>

<span data-ttu-id="45780-256">ブートス トラップは、レイアウトし、スタイルの web サイトおよびアプリケーションのさまざまな迅速かつ効率的に使用できる web フレームワークを提供します。</span><span class="sxs-lookup"><span data-stu-id="45780-256">Bootstrap provides a web framework that can be used to quickly and productively lay out and style a wide variety of websites and applications.</span></span> <span data-ttu-id="45780-257">その基本的な文字体裁やスタイルは、カスタム テーマをサポートするいると、手動で作成または製品版を購入できますを簡単に操作できる快適になり、ルック アンド フィールを提供します。</span><span class="sxs-lookup"><span data-stu-id="45780-257">Its basic typography and styles provide a pleasant look and feel that can easily be manipulated through custom theme support, which can be hand-crafted or purchased commercially.</span></span> <span data-ttu-id="45780-258">これは、過去のモダンで開いている web 標準をサポートしながらを実現する高価なサード パーティ製コントロールを必要とする web コンポーネントのホストをサポートします。</span><span class="sxs-lookup"><span data-stu-id="45780-258">It supports a host of web components that in the past would have required expensive third-party controls to accomplish, while supporting modern and open web standards.</span></span>