# 鐵人賽第 3 天: ESlint

本章的目標是提供一些ESLint的簡介與使用建議，當然它只是個檢查工具，而不會自動幫你修正錯誤或警告。在撰寫程式碼的過程中，檢查工具的提示是很重要，它是可以提升開發者撰寫的程式碼的品質的一種工具，所以有的時候你會看到把這種檢查工具稱為程式碼品質工具(Code Quality Tools)。而檢查工具背後的每一項語法檢查，都代表許多資深開發者的想法或經驗累積，這些訊息對初學者來說都是很寶貴的。

JavaScript語言長期以來有許多為人詬病的設計，雖然它一開始的初衷是希望能設計一個簡單易學的程式語言，但是因為自由度高又是弱資料類型，反而造成初學者無所適從，很多時候同一種功能，這樣寫也可以那樣寫好像也可以，就算是對已經熟悉的開發者來說，也有可能會出現不經意的錯誤。

在經過20年來的眾多使用者的努力下，現在有了更多的輔助開發的新方式，創造另一套新的程式語言或超集語言是一條路，例如TypeScript、CoffeeScript或Elm等等。而使用其它的輔助工具是另一條路，例如Lint工具就是其中一個。

## ESLint

Lint工具最早是使用於UNIX系統中C語言的程式碼靜態分析工具，主要是用來標記語法結構上有可疑的、濳在的問題語法或指令。在很早之前就有[JSLint](http://jslint.com/)與[JSHint](http://jshint.com/)兩個為JavaScript設計的檢查工具，其中JSLint是由Douglas Crockford大師所創造，在10多年前(2002)就發佈的一個工具，算得上是很有歷史的工具，不過它十分具有創造者的想法與特色，而且可以彈性自訂的選項很少。而JSHint是從JSLint分支出來的新專案(2011)，更傾向於由社群主導的專案，具有更多的彈性選項，JSHint發展得很好，有許多大公司都採用這個檢查工具，對於延伸的JSX語法，也有分支出來的[JSXHint](https://github.com/STRML/JSXHint)工具。其他還有像[JSCS](http://jscs.info/)工具與[StandardJS](http://standardjs.com/)等等。

[ESLint](http://eslint.org/)是在這個領域的新專案，它在2013年由[Nicholas C. Zakas](https://www.nczonline.net/about/)創造，正如ESLint的名字一樣，它是為ES新標準語法所設計。根據[最近的一份統計](https://ashleynolan.co.uk/blog/frontend-tooling-survey-2016-results#js-linters)也是目前在JavaScript開發中，使用率最高的語法檢查工具。ESLint的功能具有高度設定彈性與擴充性，這是以往的檢查工具中所沒有的，雖然它的檢查速度比像JSHint慢了2x-3x，但它的其他特性的確是更受到開發者的喜好。相較於JSLint與JSHint，ESLint有其他的不同特色如下:

- 高度的設定彈性: 有更多規則選項可以依需求或喜好設定
- 具有擴充功能: 函式庫或框架的開發者可以依需求再開發擴充
- 支援ES6與JSX: 高度支援ES6標準語法(甚至是更高版本標準的語法)，以及React自有的JSX語法
- 警告與錯誤訊息: 更清楚的警告或錯誤訊息

> 註: 上述的JSCS已合併到ESLint專案之中

## Airbnb - JavaScript風格指引

要談到ESLint，就需要進一步談到Airbnb這家公司，這是一家專門在網路上提供民宿(或個人)的住所出租的網站服務業者，有可能你之前有聽過，或是在出國自由行時有去租這個網站上面的房間。那麼Airbnb與ESLint有什麼關係？

Airbnb本身就有在Github上發佈一些自家公司使用的開放原始碼專案，而最有名的開放原始碼專案，就屬這個有4萬多個星的[JavaScript Style Guide (JS風格指引)](https://github.com/airbnb/javascript)。很特別的是，它並不是一個以產出應用程式為目的的專案，而是以社群為導向的方式，制定一份JavaScript應用在開發時的撰寫風格指引，這份指引是讓所有的JavaScript的開發者參考，為了讓開發者能寫出更簡潔、更少錯誤與高度閱讀性的程式碼，而這份的指引是目前是以ES6標準為主。。現在也有延伸這種指引方式到React、CSS-in-JavaScript、CSS / Sass與Ruby的內容。

當然這份JavaScript指引也有許多不同語言的翻譯版本，已經有熱心的朋友翻譯成[繁體中文翻譯的版本](https://github.com/jigsawye/javascript)，應該要多支持鼓勵他(幫他按個星星)。如果在你稍微看到過了這份指引後，可以發現幾乎每個指引規則的後面，都有一個eslint的對應規則，例如:

> 15.1 請使用 === 和 !== ，別使用 == 及 != 。eslint: eqeqeq

後面的`eslint: eqeqeq`對照的就是在ESLint中的[eqeqeq](http://eslint.org/docs/rules/eqeqeq)這個檢查規則，這個規則是在你如果在程式碼中，用值相等比較符號(==)時，會出現警告訊息，內容是有關於要求你要用嚴格相等比較(===)會比較好。

不過，這麼多的JavaScript風格指引，不會有開發者有那個美國時間一一記得，雖然說多也不多，但也都是很零碎的片段。所以Airbnb把所有的風格指引，統統寫成一個ESLint中的預先的規則設定檔案，稱之為[eslint-config-airbnb-base](https://www.npmjs.com/package/eslint-config-airbnb-base)，如果你的開發環境或工具有使用ESLint，直接裝來套用就行了。在"開發工具&環境"的"樣版文件"中，就有直接使用這個設定檔案。

## 如何使用檢查工具

要使用加上Airbnb風格後的ESLint來檢查程式碼，如果你是第一次使用，包準你只有一個感想 - "有夠麻煩"。

你可以把平常寫的JavaScript的一些程式碼，貼到編輯區域看看，例如下面這個用jQuery程式碼:

```js
$('.btn').click(function() {
  $.ajax({
        url: "check.php",
        data: {
            old_password: $("#password").val()
        },
        type: "POST",
        dataType: "json",
        success: function(data,textStatus,jqXHR) {
          console.log("success");
        },
        error: function() {
          console.log("success");
        },
        complete: function() {
          console.log("success");
        }
    });
});
```

經過ESLint檢查後，一共有37個錯誤與7個警告。啥？這不是之前可以用的一個程式碼？因為大部份都是風格部份的錯誤與警告，例如下面這些:

- 語句結尾加了分號(;): 這規則我在`.eslintrc`中另外設定的
- 空格的數量不對: 18.1 將 Tab 設定為兩個空格
- 字串要用單引號(\'\')，不用雙引號(\"\"): 6.1 字串請使用單引號 ''。
- 函式或區塊語句的空格或空行風格: 18.2、18.3、18.4、18.7、18.8、18.9、18.11等等，整個18節內容都有。

上面的程式碼像下面這樣改寫後，雖然看起來和原來的差不多。但現在只剩下4個錯誤3個警告，剩下的錯誤是因為我沒有引入jquery模組，而警告是因為用了三個`console.log`必定會有警告，這樣應該算幾乎符合風格樣式的檢查:

```js
$('.btn').click(() => {
  $.ajax({
    url: 'check.php',
    data: {
      old_password: $('#password').val(),
    },
    type: 'POST',
    dataType: 'json',
    success(data, textStatus, jqXHR) {
      console.log('success')
    },
    error() {
      console.log('success')
    },
    complete() {
      console.log('success')
    },
  })
})
```

所以說這還是需要逐漸地養成習慣的，我建議你開始今天就用吧，用久了自然就會習慣了，事實上大部份的錯誤或警告，只是提醒在撰寫時的一些格式問題。

## 嚴重的錯誤檢查

ESLint會檢查出在程式碼中可能的剖析錯誤，這些錯誤是一旦執行就會產生錯誤而停止執行。基本上當會出現致命錯誤時，其他的所有檢查訊息都會先不出現，而只有這個錯誤的訊息。因為這個錯誤如果不修正，會造成整個程式不能正常運作，例如:

```js
{ a: 1 }.toString() //message: 'Parsing error: Unexpected token'
```

> 註: 這個錯誤的原因是因為前面的物件字面文字，JS會當作是區塊的語句語法來解析。

或是下面這個例子中的錯誤(因為跳脫符號(\\)後面多了一個空格):

```js
const a = 'This is a \
book'

console.log(a)

// message: 'Parsing error: Unterminated string constant'
```

> 註: 這個錯誤的原因是是用用跳脫符號(\\)，跳脫換行符號來作多行字串的定義，但在寫的時候多了一個空格在後面所以造成錯誤。這個錯誤在編輯軟體上是無法直接看到，所以很難被查覺，除非有開啟一些編輯器中的設定值(顯示換行符號之類)。另外，使用跳脫換號符號來定義的字串值，並不是多行字串而是單行字串值。總之，這是個完全不建議的字串定義方式，不過實際上有很少一些人會使用。

或是像ES6中新語法的基本使用錯誤，這個錯誤也會造成程式停止執行。它也可以正確的指出:

```js
const a = [1, 2, 3]
a = [] //message: ''a' is constant. (no-const-assign)'
console.log(a)
```

## 習慣性語法 vs ESLint的錯誤

有些語法幾乎是在其他程式語言中非常習慣的語法，但在ESLint中有可能會出現警告或錯誤訊息，這個時候你可能就要作取捨，看是要遵照ESLint的檢查來修改，還是要改變檢查的規則。

舉個常見例子來說，像下面這個for語句，幾乎每個開發者都會寫成這樣的程式碼:

```js
for (let i = 0; i < 10; i++) {
  // some code
}
```

這時會在ESLint會回報出一個錯誤訊息([no-plusplus](http://eslint.org/docs/rules/no-plusplus))，像下面這樣:

> message: 'Unary operator '++' used. (no-plusplus)'

這個訊息是什麼意思，就是告訴你不能使用像遞增(++)或遞減(--)的運算符。為什麼？因為這兩個運算符它們在JavaScript語言中有一些很古怪的特性，在換行時會出現特殊的結果。不過我個人覺得這除非寫錯或亂寫，不太容易寫成這副德性，例如下面這個來自ESlint中的範例:

```js
// 下面相當於 i++

i ++
j

// 相當於 ++j

i
++
j
```

不過，這兩個運算符會混淆的情況還不少，有的時候會不注意到底是遞增了哪個變數，或是先遞增(減)還是晚遞增(減)。像是下面這樣的合法的程式碼，它到底遞增x還是遞增了y變數:

```js
let x = 1
let y = 2
x+++y
```

正確的答案是像下面這個一樣，這語句是遞增了x變數:

```js
x++ + y
```

> 註: `x+++y`是合法語句，但`x+++++y`就是錯誤的語句。

這個有名的遞增(++)或遞減(--)的運算符問題，在Douglas Crockford大師的大作[JavaScript: The Good Parts](http://shop.oreilly.com/product/9780596517748.do)，中譯本為[JavaScript：優良部分](http://www.books.com.tw/products/0010410726)，就被認為是造成"壞程式碼"的其中一種，所以這個檢查規在JSLint工具就已經有了。

當然，這是因為語法使用時撰寫不清造成的，除非寫錯或亂寫才會出現這種情況。大師雖然建議你使用像`i += 1`的表達式來取代原本的`i++`。但我個人(與眾多的開發者)覺得還是得要看習慣，像有的情況是不能這樣取代，像下面這個就不能取代，要分開寫才行:

```js
array[++i] = foo

//要用下面的語法來取代
i += 1
array[i] = foo
```

ESLint中提供了`allowForLoopAfterthoughts`這個選項，可以讓你在for語句中使用遞增與遞減的運算符，這是很棒的一個設定值。反正社群上一定有人覺得檢查工具就是要像這樣，提供常用的習慣設定就是了。

以上只是ESLint上百個檢查規則的其中一個，這會與你(或整個開發團隊)的使用習慣相關，當衝突發生時你需要作個取捨，看是要調整一下規則，還是理解一下為什麼這樣檢查算是個錯誤，然後依照這個錯誤指示逐步改變習慣。

## ESLint的設定檔

我把ESLint的設定方式放在最後一節，是因為ESLint有個大缺點，就是它不是很容易設定。它在設定檔的格式部份，不知道已經修過或改過多少次，而且可以支援的格式有很多種。先不說規則要如何設定，它的設定檔基本上是使用`.eslintrc`這個檔案，按照官方[Configuring ESLint](http://eslint.org/docs/user-guide/configuring)文件的說法，它可以使用JSON或YAML格式，所以你會看到網路上有兩種設定值的格式。

我在上一章的樣版文件中附的設定檔案的內容如下，這是JSON格式的:

```js
{
  "parser": "babel-eslint",
  "extends": "airbnb-base",
  "rules": {
    "semi": ["error", "never"]
  },
  "ecmaFeatures": {
      "jsx": true,
      "experimentalObjectRestSpread": true
  }
}
```

大概解說一下這裡面的幾個設定區域:

- parser: 指的是剖析器，如果你有用babel編譯器，就是設定"babel-eslint"
- extends: 這可以指定一些已經設定好的規則設定檔，像我這裡是用"airbnb-base"。不過專案裡也要有裝`eslint-config-airbnb-base`套件才能這樣設定。
- rules: 額外的規則，我這裡只有另外定義可以語句結尾不用分號(;)這個規則。
- ecmaFeatures: 這是一些特殊的語法支援，這兩個都是寫React需要的。

這裡沒寫的，但其他常用到的區域如下:

- plugins: 設定外掛。要有安裝才會設定。
- env: 設定是要在browser或node上使用。(實際上可以設定的環境有20多種，大部份都是測試環境)

我會建議初學者先用現成的就好。除了上面的這幾個設定區域外，它的規則有超過一百個以上，而且不一定可用設定值都是相同的，如果你要設定規則，不妨先從別人設定好的來修整或覆蓋，像我上面設定rules區域中這樣，而且規則的部份要參考官方的文件說明。

## 結論

ESLint畢竟只是個檢查工具，光靠工具只能提醒你在撰寫程式碼時的一些可能性的問題，至於程式碼的主要功能是不是能正常運作，或是如何來修正這些程式碼，還是有待於開發者自己的知識。

JavaScript本質上並不是一個嚴謹的程式語言，撰寫風格相當自由而且有許多陷阱與不好的語法。藉由ESLint工具的輔助，的確可以有效的協助開發者，進一步寫出較少bug、較少濳在問題、閱讀性較高的程式碼，好東西不用嗎？建議你現在就開始使用吧。