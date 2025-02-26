---
title: 文字クラス
slug: Web/JavaScript/Guide/Regular_Expressions/Character_Classes
---

{{JSSidebar("JavaScript Guide")}}

文字クラスは、文字や数字の区別など、文字の種類を区別します。

## 種類

<table class="standard-table">
  <thead>
    <tr>
      <th scope="col">文字</th>
      <th scope="col">意味</th>
    </tr>
  </thead>
  <tbody></tbody>
  <tbody>
    <tr>
      <td><code>.</code></td>
      <td>
        <p>次のいずれかの意味を持ちます。</p>
        <ul>
          <li>
            行末文字 (
            <code>\n</code>、<code>\r</code>、<code>\u2028</code>、<code
              >\u2029</code
            >
            ) を除くあらゆる 1 文字とマッチします。例えば、<code>/.y/</code> は
            "my" と "ay" にマッチし、"yes make my day" の "yes"
            にはマッチしません。
          </li>
          <li>
            文字セット内では <code>.</code> はその特別な意味を失い、文字通りの
            "."と一致します。
          </li>
        </ul>
        <p>
          複数行フラグ (<code>m</code>) は "."
          の意味を変えないことに注意してください。そのため、複数行にわたるパターンに一致させるには、（IEの古いバージョン以外なら）文字集合
          <code>[^]</code> を使うことで、改行を含む任意の文字に一致します。
        </p>
        <p>
          <strong>ES2018</strong> では <code>s</code> "dotAll"
          フラグが追加されました。これは行末文字と一致することを可能にします。
        </p>
      </td>
    </tr>
    <tr>
      <td><code>\d</code></td>
      <td>
        <p>
          あらゆる（アラビア）数字にマッチします。<code>[0-9]</code>
          に相当します。例えば <code>/\d/</code> や <code>/[0-9]/</code> は "B2
          is the suite number" の "2" にマッチします。
        </p>
      </td>
    </tr>
    <tr>
      <td><code>\D</code></td>
      <td>
        <p>
          あらゆる（アラビア）数字以外の文字にマッチします。<code>[^0-9]</code>
          に相当します。例えば <code>/\D/</code> や <code>/[^0-9]/</code> は "B2
          is the suite number" の "B" にマッチします。
        </p>
      </td>
    </tr>
    <tr>
      <td><code>\w</code></td>
      <td>
        <p>
          アンダースコアを含むあらゆる半角英数字（基本ラテンアルファベット）にマッチします。<code
            >[A-Za-z0-9_]</code
          >
          に相当します。例えば <code>/\w/</code> は、"apple," の 'a' や "$5.28,"
          の "5" や "3D" の "3" にマッチします。
        </p>
      </td>
    </tr>
    <tr>
      <td><code>\W</code></td>
      <td>
        <p>
          前述以外の文字にマッチします。<code>[^A-Za-z0-9_]</code>
          に相当します。例えば <code>/\W/</code> や
          <code>/[^A-Za-z0-9_]/</code> は、"50%" の "%" にマッチします。
        </p>
      </td>
    </tr>
    <tr>
      <td><code>\s</code></td>
      <td>
        <p>
          スペース、タブ、改ページ、改行を含むホワイトスペース文字にマッチします。<code
            >[
            \f\n\r\t\v​\u00a0\u1680​\u180e\u2000​-\u200a​\u2028\u2029\u202f\u205f​\u3000\ufeff]</code
          >
          に相当します。例えば <code>/\s\w*/</code> は <code>"foo bar"</code> の
          <code>" bar"</code> にマッチします。
        </p>
      </td>
    </tr>
    <tr>
      <td><code>\S</code></td>
      <td>
        <p>
          ホワイトスペース以外の文字にマッチします。<code
            >[^
            \f\n\r\t\v\u00a0\u1680\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]</code
          >
          に相当します。例えば <code>/\S\w*/</code> は "foo bar" の "foo"
          にマッチします。
        </p>
      </td>
    </tr>
    <tr>
      <td><code>\t</code></td>
      <td>タブ (U+0009) にマッチします。</td>
    </tr>
    <tr>
      <td><code>\r</code></td>
      <td>復帰文字 (U+000D) にマッチします。</td>
    </tr>
    <tr>
      <td><code>\n</code></td>
      <td>改行文字 (U+000A) にマッチします。</td>
    </tr>
    <tr>
      <td><code>\v</code></td>
      <td>垂直タブ (U+000B) にマッチします。</td>
    </tr>
    <tr>
      <td><code>\f</code></td>
      <td>改ページ (U+000C) にマッチします。</td>
    </tr>
    <tr>
      <td><code>[\b]</code></td>
      <td>
        後退文字（バックスペース、U+0008）にマッチします。単語境界文字
        (<code>\b</code>) については<a
          href="/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Boundaries"
          >境界</a
        >を見てください。
      </td>
    </tr>
    <tr>
      <td><code>\0</code></td>
      <td>
        NULL 文字 (U+0000)
        にマッチします。この後ろに他の数字を続けてはいけません。<code>\0</code>
        の後に（0 から 7 までの）数字が続くと 8 進数の<a
          href="/ja/docs/Web/JavaScript/Reference/Lexical_grammar#Octal"
          >エスケープシーケンス</a
        >となるからです。
      </td>
    </tr>
    <tr>
      <td>
        <code>\c<em>X</em></code>
      </td>
      <td>
        <p>
          <code><em>X</em></code> には A から Z のうち 1
          文字が入ります。文字列中の制御文字にマッチします。例えば
          <code>/\cM/</code> は文字列中の control-M (U+000D) にマッチします。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>\x<em>hh</em></code>
      </td>
      <td>
        <code>hh</code>（2 桁の 16 進数）コードからなる文字にマッチします。
      </td>
    </tr>
    <tr>
      <td>
        <code>\u<em>hhhh</em></code>
      </td>
      <td>
        <code>hhhh</code>（4 桁の 16 進数）の値からなる UTF-16
        コードユニットにマッチします。
      </td>
    </tr>
    <tr>
      <td>
        <code>\u<em>{hhhh}</em></code> または <code><em>\u{hhhhh}</em></code>
      </td>
      <td>
        <p>
          (<code>u</code> フラグがセットされた時のみ)<strong> </strong
          ><code>U+<em>hhhh</em></code> または <code>U+<em>hhhhh</em></code> (16
          進数) Unicode 値からなる文字にマッチします。
        </p>
      </td>
    </tr>
    <tr>
      <td><code>\</code></td>
      <td>
        <p>
          次の文字を特別に扱うこと、「エスケープ」することを示します。
          その振る舞いは、2 通りのうちのどちらか 1 つです。
        </p>
        <ul>
          <li>
            通常文字の前に付けられた場合、次の文字が特別なもので、文字通りには評価されないことを示します。例えば
            <code>b</code> は文字 <code>"b"</code> にマッチします。しかし "b"
            の前にバックスラッシュを置いて <code>\b</code> とすると、<a
              href="/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Boundaries"
              >単語区切り</a
            >を意味するようになります。
          </li>
          <li>
            特殊文字の前に付けられた場合、次の文字が特別なものでなく、文字通りに評価されることを表します。例えば、<code
              >"*"</code
            >
            は、先行文字の 0
            回以上の出現が一致する必要があることを意味する特殊文字です。例えば、<code
              >/a*/</code
            >
            は 0 回以上の <code>"a"</code> とマッチします。文字通りの
            <code>*</code>
            にマッチさせるには、その直前にバックスラッシュを入れます。例えば、<code
              >/a\*/</code
            >
            は <code>"a*"</code> とマッチします。
          </li>
        </ul>
        <div class="blockIndicator note">
          <p>
            この文字を文字通りにマッチさせるには、それ自身をエスケープします。つまり、
            <code>/\\/</code> を使って <code>\</code> を検索します。
          </p>
        </div>
      </td>
    </tr>
  </tbody>
</table>

## 例

### 一連の数字を探す

```js
var randomData = "015 354 8787 687351 3512 8735";
var regexpFourDigits = /\b\d{4}\b/g;
// \b は境界を示します（つまり、単語の真ん中からマッチを開始しません）
// \d{4} は 4 つの数字を示します
// \b は別の境界を示します（つまり、単語の真ん中でマッチが終わりません）


console.table(randomData.match(regexpFourDigits));
// ['8787', '3512', '8735']
```

### A から始まる（ラテンアルファベットの）単語を探す

```js
var aliceExcerpt = "I’m sure I’m not Ada,’ she said, ‘for her hair goes in such long ringlets, and mine doesn’t go in ringlets at all.";
var regexpWordStartingWithA = /\b[aA]\w+/g;
// \b は境界を示します（つまり、単語の真ん中からマッチを開始しません）
// [aA] は a または A の文字を示します
// \w+ は複数回の *ラテンアルファベットからなる* 任意の文字を示します

console.table(aliceExcerpt.match(regexpWordStartingWithA));
// ['Ada', 'and', 'at', 'all']
```

### （ユニコード文字の）単語を探す

単語を表すために、ラテンアルファベットではなく、 Unicode 文字の範囲が使えます。（つまり、ロシア語やアラビア語のような他の言語のテキストを扱えます。） Unicode の 「基本多言語面」には、世界中で使われているほとんどの文字が含まれており、それらの文字で書かれた単語にマッチするための文字クラスと範囲を利用できます。

```js
var nonEnglishText = "Приключения Алисы в Стране чудес";
var regexpBMPWord = /([\u0000-\u0019\u0021-\uFFFF])+/gu;
// U+0000 から U+FFFF までの BMP、ただし、U+0020 は空白

console.table(nonEnglishText.match(regexpBMPWord));
[ 'Приключения', 'Алисы', 'в', 'Стране', 'чудес' ]
```

## 仕様

| 仕様書                                                                                               | 策定状況                     | コメント |
| ---------------------------------------------------------------------------------------------------- | ---------------------------- | -------- |
|                                                                                                      |                              |          |
| {{SpecName('ESDraft', '#sec-characterclass', 'RegExp: Character classes')}} | {{Spec2('ESDraft')}} |          |

## ブラウザサポート

{{Compat("javascript.builtins.RegExp.character_classes")}}

## 関連情報

- [正規表現](/ja/docs/Web/JavaScript/Guide/Regular_Expressions)
- [`RegExp()` コンストラクタ](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
