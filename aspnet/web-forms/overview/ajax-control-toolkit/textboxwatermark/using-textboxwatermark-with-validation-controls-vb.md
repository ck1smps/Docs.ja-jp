---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: 検証コントロール (VB) で TextBoxWatermark の使用 |Microsoft ドキュメント
author: wenz
description: AJAX コントロールのツールキットで TextBoxWatermark コントロールは、ボックス内でテキストが表示されないようにテキスト ボックスを拡張します。 ボックスに、ユーザーがクリックしたときに.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ca1a4af62af1d65525e59d0b7bc47245dd01476
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2018
---
<a name="using-textboxwatermark-with-validation-controls-vb"></a>検証コントロール (VB) で TextBoxWatermark を使用します。
====================
によって[Christian Wenz](https://github.com/wenz)

[コードをダウンロードする](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> AJAX コントロールのツールキットで TextBoxWatermark コントロールは、ボックス内でテキストが表示されないようにテキスト ボックスを拡張します。 ボックスに、ユーザーがクリックするは空になります。 ユーザーがテキストを入力することがなく、ボックスのまま、指定済みのテキストが表示されます。 これは同じページで、ASP.NET の検証コントロールと競合する可能性がありますが、これらの問題を解決する可能性があります。


## <a name="overview"></a>概要

`TextBoxWatermark`ボックス内でテキストが表示されるように、AJAX コントロール Toolkit でコントロールがテキスト ボックスを拡張します。 ボックスに、ユーザーがクリックするは空になります。 ユーザーがテキストを入力することがなく、ボックスのまま、指定済みのテキストが表示されます。 これは同じページで、ASP.NET の検証コントロールと競合する可能性がありますが、これらの問題を解決する可能性があります。

## <a name="steps"></a>手順

このサンプルの基本的なセットアップは、次:`TextBox`を使用してコントロールを透かし、`TextBoxWatermarkExtender`コントロール。 ボタンを使用して、ポストバックのトリガー、ページ上の検証コントロールのトリガーを後で使用されます。 また、`ScriptManager`コントロールは ASP.NET AJAX を初期化するために必要があります。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

ここで追加、`RequiredFieldValidator`コントロールかどうかがテキスト フィールドに、フォームが送信されるときに確認します。 `InitialValue`検証コントロールのプロパティで使用されるものと同じ値に設定する必要があります、`TextBoxWatermarkExtender`コントロール: 変更なしのテキスト ボックスの値は、その中レベルのウォーターマーク値でフォームが送信されるときに。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

このアプローチの 1 つの問題: 場合は、クライアントには、JavaScript が無効化、テキスト フィールドされません事前入力透かしのテキストをそのため、`RequiredFieldValidator`エラー メッセージは発生しません。 そのため、1 秒あたり`RequiredFieldValidator`制御が必要なを空のテキスト ボックスのチェック (を省略すると、`InitialValue`属性)。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

両方の検証コントロールを使用するので`Display` =`"Dynamic"`エンドユーザーとを区別できない、視覚的な外観が 2 つの検証コントロールが発生しました。 代わりに、ようそれらの 1 つだけを使用する必要がありました。

最後に、検証コントロールにエラー メッセージが発行されたない場合は、フィールド内のテキストを出力するには、いくつかサーバー側コードを追加します。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]


[![検証コントロールがないテキスト フィールドにエラーが発生します。](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

検証エラーが発生 フィールドにテキストがないこと ([フルサイズのイメージを表示するをクリックして](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))

> [!div class="step-by-step"]
> [前へ](using-textboxwatermark-in-a-formview-vb.md)
