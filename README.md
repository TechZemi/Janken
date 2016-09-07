じゃんけんゲーム
====================

## ルール

コンピュータと人間が、３回戦のじゃんけんをします。
先に２回勝った方が最終的な勝ちです（あいこは１回には数えず、
勝ち負けが決まって初めて１回です）。

## じゃんけんゲームに必要なものは？

![ブレークダウンツリー](https://github.com/TechZemi/Janken/blob/master/README/Breakdown.png?raw=true)

---
## Step1: グーチョキパーを選べて、画面で表示できるようにする

**ゴール**

![Step1のゴール](https://github.com/TechZemi/Janken/blob/master/README/Step1.png?raw=true)

Step1のゴールをプログラムの視点から見ると、グーチョキパーのボタンを用意して、
そのどれが押されたかが分かる必要があるわけです。

これを実現するまでの手順をもう少し細かくすると、

1. ユーザがグーチョキパーを選ぶボタンを配置する
2. ユーザがボタンを押したら、押されたことを分かるようにする
3. 何を選んだかを分かるようにする

となります。

---

### Step1-1: ユーザがグーチョキパーを選ぶボタンを配置する

<ruby><rb>index</rb><rt>インデックス</rt></ruby>.htmlを開きましょう。
index.htmlは、HTMLでWebサイトを作る時の一般的な名前でした。

![テンプレートの説明](https://github.com/TechZemi/Janken/blob/master/README/html-template.png?raw=true)

ボタン入力には <ruby><rb>input</rb><rt>インプット</rt></ruby> タグを使います。

```
<input type="button" value="グー">
```

上のように書くと、下のように表示されます。

<input type="button" value="グー">

押しても何も起きません。

---

### Step1-2: ユーザがボタンを押したら、押されたことを分かるようにする

まずは「ユーザがボタンを押した時」というイベントをプログラムが扱えるようにしましょう。

方法は２つあります。

1. inputタグに <ruby><rb>onClick</rb><rt>オン クリック</rt></ruby> 属性を追加する
2. JavaScriptでinputタグを見つけ、イベントリスナーを追加する

今年、Techゼミ１年目の皆さんは１で、２年目の皆さんは２で作りましょう。

---

#### 1. inputタグに onClick属性を追加する

先ほど追加したinputタグを以下のように書き換えます。

```
<input type="button" value="グー" onClick="選ぶ()">
```

続いて、<ruby><rb>script</rb><rt>スクリプト</rt></ruby> タグの中に「選ぶ」
<ruby><rb>関数</rb><rt>かんすう</rt></ruby>を用意します。
関数とは、「ある決まった一連の働きをする機械」でした。
関数を作るには<ruby><rb>function</rb><rt>ファンクション</rt></ruby>に続けて
関数の名前を書き、丸括弧、波括弧を用意します。
作る関数名の「選ぶ」以外は半角で書かなくてはいけないので注意して下さい。

```
function 選ぶ() {
    
}
```

グーボタンを押してみましょう。押してもまだ何も起きません。

押したら押されたことが分かるようにしましょう。以下のように、<ruby><rb>alert</rb><rt>アラート</rt></ruby> 関数を使いましょう。

```
function 選ぶ() {
    alert('押された');
}
```

JavaScriptでは、文の最後に「;（セミコロン）」を付けるのがお約束です。
これは、一つの文（＝働き）はここで終わりだよ」とブラウザに教えるためです。



---

#### 2. JavaScriptでinputタグを見つけ、イベントリスナーを追加する

JavaScriptにて、特定のHTMLタグ（ノードと呼びます）を見つけるには、<ruby><rb>querySelector</rb><rt>クエリ セレクタ</rt></ruby>関数を使うのでした。

**例**（新しくtest.htmlを作って、以下を貼り付けて確かめてみよう）
```
<!DOCTYPE html>
<html lang="ja">
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style>
            #red { color: #ff0000; }
            #blue { color: #0000ff; }
            #yellow { color: #ffdd00; }
        </style>
    </head>
    <body>
        <p id="red">赤巻き貝</p>
        <p id="blue">青巻き貝</p>
        <p id="yellow">黃巻き貝</p>
        
        <script type="text/javascript">
            // idがblueのノードを取ってきて、変数blueに入れます
            var blue = document.querySelector('#blue');
            // 取ってきたノードの持つ文字列を「黒巻き貝」に変えます
            blue.textContent = '黒巻き貝';
            // 取ってきたノードに付加されたスタイルの内、color属性を黒に変えます
            blue.style.color = '#000000';
        </script>
    </body>
</html>
```

続いて取ってきたノードに「クリックされた時」のイベントを付けるには、以下のようにします。

**例**（test.htmlを改造して試してみよう）
```
<!DOCTYPE html>
<html lang="ja">
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style>
            #red { color: #ff0000; }
            #blue { color: #0000ff; }
            #yellow { color: #ffdd00; }
        </style>
    </head>
    <body>
        <p id="red">赤巻き貝</p>
        <p id="blue">青巻き貝</p>
        <p id="yellow">黃巻き貝</p>
        
        <script type="text/javascript">
            // idがblueのノードを取ってきて、変数blueに入れます
            var blue = document.querySelector('#blue');
            // 取ってきたノードがクリックされた時に呼ばれる動作を指定
            blue.addEventListener('click', function (e) {
                すり替え();
            });
            
            // 取ってきたノードの色をすり替える関数
            function すり替え() {
                // 取ってきたノードの持つ文字列を「黒巻き貝」に変えます
                blue.textContent = '黒巻き貝';
                // 取ってきたノードに付加されたスタイルの内、color属性を黒に変えます
                blue.style.color = '#000000';
            }
        </script>
    </body>
</html>
```

これらのヒントから、グーチョキパーのボタンがクリックされた時に、

```
function 選ぶ() {

}
```

が呼ばれるようにし、選ぶ関数が動作すると、

```
alert('押された');
```

が表示されるようにしてみましょう。

---

### 今日覚えたい大人のIT用語「インタフェース」

ボンタのようなユーザが入力するための手段や、逆にアラートダイアログのような
コンピュータがユーザに結果などを伝える手段を「__ユーザ・インタフェース__」と呼びます。

インタフェース（interface）とは、元々、物と物との境界面を意味する言葉で、
「__コンピュータと人間との境界面__」という意味からマウスやキーボードの入力装置、
ディスプレイやスピーカなどの出力装置をインタフェースと呼ぶようになりました。

最近では画面を直接タッチしてコンピュータを操作することが普通になったことから、
画面上に配置したボタンや画面上のアラートダイアログなどもインタフェースと呼ぶようになっています。

---

#### Step1-3: 何を選んだかを分かるようにする

ここまでで、グーチョキパーのボタンが押されたことは分かるようになりました。
でもまだ何が押されたかまで、プログラムが分かるようにはなっていません。

何を押されたかを分かるようにするには、「選ぶ」関数に<ruby><rb>引数</rb><rt>ひきすう</rt></ruby>を渡してあげる必要があります。


以下は、引数を取る関数の「宣言」と「呼び出し」の例です。

**例**（index.htmlのscriptタグに以下を貼り付けて試してみよう）
```

// 引数nを取る、「n個の黒丸を追加」関数の宣言
function n個の黒丸を追加(n) {
    var 追加分 = '<br>';
    
    // for文を使って、n回同じ処理をする
    for ( var i=0; i<n; i++ ) {
        追加分 = 追加分 + '● <br>';
    }
    
    // bodyタグの最後に変数「追加分」の中身を追加する処理
    document.body.innerHTML = document.body.innerHTML + 追加分;
}

// 「n個の黒丸を追加」関数を、引数5として呼び出し
n個の黒丸を追加(5);
```


さて、ただアラートで「グー」とか出すだけじゃつまらないし、何より次に進むのに
いちいちOKボタンを押すのは面倒です。選んだ「手」を画像で表示してみましょう。

まずは選ぶ前の空欄を以下の画像（/images/command.png）を使って表示します。

![空欄](https://github.com/TechZemi/Janken/blob/master/images/command.png?raw=true)

以下のHTMLをタグを追加しましょう。
```
<div id="プレーヤー" class="コマンド">
    自分
</div>
```

また、以下のスタイルを追加します。
```
.コマンド {
    background-image: url('./images/command.png');
    width: 200px;
    height: 200px;
    margin: 10px auto;
}
```

divタグを置いて中に「自分」と書きました。普通にdivを置くだけだと、
divは<ruby><rb>block</rb><rt>ブロック</rt></ruby>要素なので、横いっぱいに拡がっています。

![styleなしのdiv](https://github.com/TechZemi/Janken/blob/master/README/div_no_style.png?raw=true)

ここでは、divの大きさを画像の大きさ（横200px、縦200px）に合わせて、 
画面の中央に表示されるように、左右の<ruby><rb>margin</rb><rt>マージン</rt></ruby>
を<ruby><rb>auto</rb><rt>オート</rt></ruby>（自動）にしています。

![styleありのdiv](https://github.com/TechZemi/Janken/blob/master/README/div_with_style.png?raw=true)

これで「手」を選ぶまで、代わりに表示さている空欄ができました。

では「手」を選んだ時、この画像を選んだ「手」で差し替えることにしましょう。
差し替えをJavaScriptで実現するには、

1. （差し替える）元の画像の表示されているタグをノードとして取得する
2. 取得したノードのスタイルを書き換える

という手順で行います。

特定のHTMLタグのノードを取得するので、<ruby><rb>querySelector</rb><rt>クエリ セレクタ</rt></ruby>関数を使いましょう。

```
var プレーヤー = document.querySelector('???');
```

先ほど追加したdivタグのノードを取得し、プレーヤー変数に入れたいです。
どんな風に探すことができるでしょうか。「？？？」に入る文字列を当てて下さい。


次にノードを取得できたら、画像を差し替えます。差し替えるには以下のように
divノードのスタイルを上書きしてあげます。

```
// グーの時はgu.png
// チョキの時はch.png
// パーの時はpa.png
プレーヤー.style.backgroundImage = 'url(./images/gu.png)';
```

選ぶ関数の引数に合わせて自動でグーチョキパーを変えたいですね。
どうすればいいでしょうか？

「もし、◯◯だったら☓☓」を実現するには __if 文__ が使えます。
以下の例の、「手」がグーや「手」がチョキの部分を自分なりに変えてみよう！

**例**
```
if ( 「手」がグー ) {
    プレーヤー.style.backgroundImage = 'url(./images/gu.png)';
} else if （ 「手」がチョキ ）{
    プレーヤー.style.backgroundImage = 'url(./images/ch.png)';
} else {
    プレーヤー.style.backgroundImage = 'url(./images/pa.png)';
}
```

---

### 今日覚えたい大人のIT用語「フィードバック」

ユーザがボタンを押して選んだ結果がアラートダイアログとして、画面に表示されるようになりました。

このような入力に対する結果をフィードバック(feedback)と呼びます。
日本語では「手応え」が一番いい訳だと思います。

「のれんに腕押し」なんてことわざがありますが、押したのに何の手応えもないと
「ホントにこのゲーム動いてるのかな？バグってるんじゃないの？？」とユーザは思います。

よいゲームとは、ユーザの操作に対して、気持ちのいい「手応え、フィードバック」を返すゲームです。

---


