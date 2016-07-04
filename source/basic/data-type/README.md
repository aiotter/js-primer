# データ型とリテラル

## データ型

JavaScriptは動的型付け言語に分類される言語であるため、
静的型付け言語のように変数に型の指定をすることはなく、実行時に型が決定されます。

JavaScriptでは次の6つのプリミティブなデータ型とオブジェクトによって成り立っています。

- プリミティブ型のデータ
    - 真偽値（Boolean）: `true` or `false`
    - 数値（Number）: `42` や `3.14159` など
    - 文字列（String）: `"JavaScript"` など
    - undefined: 値が未定義であるデータ型
    - null: 値が存在しないnull値を意味するデータ型
    - シンボル（Symbol）: `Symbol()`で作られたインスタンスは一意で不変な値となる
- オブジェクト（Object)
    - オブジェクト、配列、関数などプリミティブ以外のものはオブジェクトの一種

JavaScriptでは`typeof`演算子を使うことで、次のように値のデータ型を調べることができます。

[import, typeof-example.js](src/typeof-example.js)

`typeof null; // => "object"`となるのは[The history of “typeof null”][歴史的経緯のある仕様バグ]ですが、
他のプリミティブ値についてはそれぞれのデータ型を調べることができます。

オブジェクトと一言にいってもJavaScriptではすべてがオブジェクトであると言われるほど、多くの種類が存在します。
`typeof`演算子では複合型と言われるオブジェクトの細かい種類を知ることはできません。

つまり、`typeof`演算子は、プリミティブ型またはオブジェクトかを判別するもので、
オブジェクトの詳細な型については別の方法を判定するようになっています。
詳しくは各オブジェクトの中で見ていきます。

## リテラル

プリミティブ値やオブジェクトは**リテラル**を使うことでプログラムに表現することができます。

TODO: リテラルとはプログラム上で数値や文字列など、直接記述した内容がそのデータ型の値を書ける記法を定義したものです。
たとえば、`"`と`"`で囲んだ文字列と扱えるため、繰り返し扱うデータ型は簡単に書けるようになっています。
リテラル表現がない場合は、その値を作る関数に引数を渡して作成する形になります。
そのような冗長な表現を避ける方法として主要な値にはリテラルが用意されています。

次の3つのプリミティブデータ型にはそれぞれリテラル表現を持っています。

- 真偽値
- 数値
- 文字列

### 真偽値（Boolean）

真偽値は`true`と`false`のリテラルがあります。
それぞれは`true`と`false`の値を返すリテラルとなります。

```js
true; // => true
false; // => false
```

### 数値（Number）

数値は大きく分けて`42`のような整数リテラルと`3.14159`のような浮動小数点リテラルがあります。

#### 整数リテラル

整数リテラルは次の4種類があります。

- 10進数: 先頭が`0`ではない数値 - `10`
- 2進数: `0b` または `0B` - `0b1`
    - `0b` の後ろには`0`または`1` の数値
- 8進数: `0o` または `0O` - `0o7` [^1]
    - `0o` の後ろには `0`から`7` までの数値
- 16進数: `0x` または `0X` - `0x15`
    - `0x` の後ろには `0`から`15`までの数値

JavaScriptでは、0から9の数字のみで書かれた数値は10進数として扱われます。

`0b`から始まる2進数リテラルは、ビットを表現するのによく利用されています。

[import, binary-example.js](src/binary-example.js)

`0o`から始まる8進数リテラルは、ファイルのパーミッションを表現するのによく利用されています。

[import, octal-example.js](src/octal-example.js)

`0x`から始まる16進数リテラルは、文字のコードポイントやRGB値の表現などに利用されています。

[import, hex-example.js](src/hex-example.js)

TODO: もっと具体的なイメージの話をしたい。

|        	| 表記例 	| 用途                       |
|--------	|--------	|----------------------------|
| 10進数 	| 42     	| 数値                        |
| 2進数  	| 0b0001 	| ビット演算など               |
| 8進数  	| 0o777  	| ファイルのパーミッションなど     |
| 16進数 	| 0xEEFF 	| 文字コード、RGB値など         |

#### 浮動小数点数リテラル

JavaScriptではIEEE 浮動小数点数形式を採用しています。
浮動小数点数をリテラルと書く場合には次の2種類の表記が利用できます。

- `3.14159` のような `.`（ドット）を含んだ数値
- `2e8` のような `e` または `E` を含んだ数値

`0`から始まる浮動小数点数は、`0`を省略し書くことができます。

```js
.123; // => 0.123
```

しかし、JavaScriptでは`.`をオブジェクトにおいて利用する機会が多いため、
`0`から始まる場合でも省略せずに書いたほうが意図しない挙動を減らせるでしょう。

> **Note** 変数名が数字から始めることができないのは、数値リテラルと衝突してしまうことが理由としてあげられます。

### 文字列（String）

文字列リテラル共通のルールとして、同じ記号で囲んだ範囲を文字列として扱います。
文字列リテラルとして次の3種類のリテラルがありますが、すべて評価した結果は同じ"文字列"です。

<!-- textlint-disable eslint -->

```js
"文字列";
'文字列';
`文字列`;
```

<!-- textlint-enable eslint -->

#### ダブルクオートとシングルクオート

`"`（ダブルクオート）と`'`（シングルクオート）は全く同じ意味となります。
PHPやRubyなどとは違い、どちらのリテラルでも評価結果は全く同じとなります。

文字列リテラルは同じ記号で囲む必要があるため、次のように文字列の中に同じ記号が出現した場合は、
`\'`という形で`\`を使いエスケープしなければなりません。

<!-- textlint-disable eslint -->

```js
'8 o\'clock'; // => "8 o'clock"
```

<!-- textlint-enable eslint -->

そのため、文字列内部に出現しないリテラル記号を使うことで、エスケープをせずに書くことができます。

```js
"8 o'clock"; // => "8 o'clock"
```

ダブルクオートとシングルクオートどちらも改行をそのまま入力することはできません。
次のように改行を含んだ文字列を定義使用すると `Syntax Error` となります。

<!-- textlint-disable eslint -->

```js
"複数行の
文字列を
入れたい"; // Syntax Error
```

<!-- textlint-enable eslint -->

改行の代わりに改行記号のエスケープシーケンス（`\n`）を使うことで複数行の文字列を書くことができます。


```js
"複数行の\n文字列を\n入れたい";
```

複数行の文字列は次のTemplate literalを使うことでもっと直感的に書くことができます。


#### [ES2015] Template literal

Template literalは `\``（バックティック）で囲んだ範囲を文字列とするリテラルです。
Template literalでは、複数行の文字列を改行記号なしに書くことができます。

複数行の文字列も`\``で囲めば、そのまま書くことができます。


```js
`複数行の
文字列を
入れたい`; // => "複数行の\n文字列を\n入れたい"
```

また、名前のとおりテンプレートのような機能を持っています。
Template literal内で`${変数名}`と書いた場合に、その変数の値を埋め込むことができます。

```js
var string = "文字列";
console.log(`これは${string}です`); // => "これは文字列です"
```

Tagged Templatesも他の文字列リテラルと同様に同じリテラル記号を内包したい場合は、`\`を使いエスケープする必要があります。

<!-- textlint-disable eslint -->

```js
`This is \`code\``;// => "This is `code`"
```

<!-- textlint-enable eslint -->

### nullリテラル

nullリテラルは`null`値を返すリテラルです。
`null`は「値がない」ということを表現する値です。

次のように、未定義の変数を参照した場合は、
参照できないため`ReferenceError`の例外が投げられます。

```js
foo;// "ReferenceError: foo is not defined"
```

`foo`は値がないということを表現したい場合は、
`null`値を代入することで、`null`値をもつ`foo`という変数を定義することができます。
これにより、`foo`を値がない変数として定義し、参照できるようになります。

```js
var foo = null;
foo; // => null
```

### オブジェクトリテラル

JavaScriptにおいてあらゆるものの基礎となるのがオブジェクトです。
そのオブジェクトを作成する方法のひとつとしてオブジェクトリテラルがあります。
オブジェクトリテラルは`{}`（中括弧）を書くことで、新しいオブジェクトを作成できます。

```js
var object = {}; // 中身が空のオブジェクトを作成
console.log(object); // => {}
```

オブジェクトリテラルはオブジェクトの作成と同時に中身を定義することができます。
オブジェクトのキーと値を`:`で区切ったものを `{}` の中に書くことで作成と初期化が同時に行えます。

次のコードで作成したオブジェクトは `key` というキー名と `value` という値をもつオブジェクトを作成しています。

```js
var object = {
    key: "value"
};
```

このとき、オブジェクトがもつキーのことをプロパティ名と呼びます。
この場合、 `object` は `key` というプロパティを持っていると言います。
`object` は `key` を参照するには、`.`（ドット）で繋ぎ参照することができます。

```js
var object = {
    key: "value"
};
console.log(object.key); // => "value"
```

オブジェクトのプロパティ名には変数名と同じものが利用でき、
値にはプリミティブ値からオブジェクトまで何でも入れることができます。

オブジェクトは多くの機能や仕組みを持っていますが、詳細については第n章で紹介します。
そのため、`{}`という記号が出てきたら新しいオブジェクトを作成しているんだなと見てください。

- [ ] TODO: 第n章を埋める。

### 配列リテラル

最後にもうひとつ重要なリテラルとして配列リテラルがあります。
配列リテラルは`[`と`]`で値をカンマ区切りで囲みます。

```js
var emptyArray = []; // 空の配列を作成
var array = [1, 2, 3]; // 値をもった配列を作成
```

配列もオブジェクトの一種ですが、プログラミングにおいてとても重要な機能を持っています。
配列についての詳細は第n章で紹介します。

- [ ] TODO: 第n章を埋める。


### 正規表現リテラル

最後にJavaScriptは正規表現をリテラルで書くことができます。
正規表現は`/`と`/`で正規表現のパターン文字列囲みます。

次のコードでは、1文字以上の数字にマッチする正規表現をリテラルで表現することができます。

```js
var numberRegExp = /\d+/; // 1文字以上の数字にマッチする正規表現
// 123が正規表現にマッチするかをテストする
numberRegExp.test(123); // => true
```

文字列から正規表現オブジェクトを作成することもできますが、
その際、特殊文字の二重エスケープが必要になり直感的に書くことが難しくなります。

正規表現オブジェクトについて詳しくは、第n章で紹介します。

## まとめ

この章では、データ型とリテラルについて学びました。

- 6つのプリミティブなデータ型とオブジェクトがある
- 真偽値、数値、文字列についてリテラル表現がある
- オブジェクトではオブジェクトと配列リテラルがある

## [コラム] undefinedはリテラルではない

プリミティブ型として紹介した`undefined`はリテラルではないのかという疑問があるかもしれません。
`undefined`はただのグローバル変数で、`undefined`という値を持っているだけとなっています。

そのため、`undefined`という名前のローカル変数を定義することができます。

```js
var undefined; // undefinedというローカル変数を定義できる
```

一方、リテラルである`null`は変数ではなくリテラルであるため再定義することができません。

[import, var-null-invalid.js](./src/var-null-invalid.js)

[変数と宣言](../variables/README.md)で解説したように、
`let`や`const`で定義した変数は再定義することができません。
一方、`var`やグローバル変数は同じ変数名で再定義することができます。

また、変数名としてリテラルは利用できない予約語として定義されているため、このような違いが生じています。

## 参考

- [11.6.2 Reserved Words](http://www.ecma-international.org/ecma-262/7.0/#prod-ReservedWord "Reserved Words")
- [11.8.3.1Static Semantics: MV](http://www.ecma-international.org/ecma-262/7.0/#sec-static-semantics-mv "11.8.3.1Static Semantics: MV")

[^1]: `0o` は数字のゼロと小文字アルファベットの`o`
[The history of “typeof null”]: http://www.2ality.com/2013/10/typeof-null.html  "The history of “typeof null”"