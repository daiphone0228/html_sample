# Webページにおける段組み

## 段組み
- テキストや画像を複数の段に分けてレイアウトすること
- 1段でレイアウトすると読みづらくなるので、2段や3段に分けたりする
- 新聞や雑誌などの様々な媒体で利用されている

## webページにおける段組み
- webページでは複数のボックスを横に並べ、その中にテキストや画像を入れることにより、段組みのようにできる
- ボックスをいかにコントロールして並べるかが重要とされている
※ cssの「Multi-column Layout」の機能を利用することにより、webページでも本来の段組みを実現できるようになっています。

## ボックスを横に並べる
- webページではコントロールせずに追加したものは縦に並んでいくため、横に並べる方法をマスターする必要がある
1. 横に並べたい２個以上のボックスを同じdiv class="boxA"で囲い、それらをfloatさせる
2. さらに下にあるボックスが入り込まないように、boxAをclearfixする
3. その後、横幅をwindowに合わせるため、floatさせた横幅を%でまとめる

## ボックスの横幅の指定
- 基本的には横幅全体を100%として、並べるボックスの割合を%表示で指定する
- 100%を超えた場合は「カラム落ち」といい次の段に移る
- その場合スマートに表示させるために、落ちた分は100%で表示するようにする
- 固定した横幅に対して、左側を固定した場合は下記の用に記述すると、右側が後ろに入り込まず、さらに可変的になる

```css
	sample.css

	.boxA {
	border: solid 8px #00a0e9;
	background-color: #a0e0fe;
	color: #00a0e9;
	}
	.boxA:after {
		content: "";
		display: block;
		clear: both;
	}
	.box2 {
		float: left;
		width: 300px;
	}
	.box3 {
		float: none;
		width: auto;
		margin-left: 300px;
	}
```

```html
	sample.html

	<body>
		<div class="box1">
			BOX1
		</div>
		<div class="boxA">
		<div class="box2">
			BOX2
		</div>
		<div class="box3">
			<p>sample samplesample samplesample samplesample...sample</p>
		</div>
		</div>
		<div class="box4">
			BOX4
		</div>
	</body>
```

## ボックスの反対側を固定（右側）する場合
```css
	sample.css

	.boxB:after {
		content: "";
		display: block;
		clear: both;
	}

	.box6 {
		float: left;
		width: 100%;
		margin-right: -300px;
		padding-right: 300px;
		-moz-box-sizing: border-box;
		-webkit-box-sizing: border-box;
		box-sizing: border-box;
	}

	.box7 {
		float: left;
		width: 300px;
	}
```

```html
	sample.html

	<div class="box5">
		BOX5
	</div>
	<div class="boxB">
		<div class="box6">
			<p>sample samplesample samplesample samplesample...sample</p>
		</div>
		<div class="box7">
			BOX7
		</div>
	</div>
	<div class="box8">
		BOX8
	</div>
```

## レスポンシブデザインに対応させるには
- ブラウザのブレイクポイントを決めるために、`@media (min-width: ***px;) {}`と指定して、そのカッコの中にスタイルを記述する
- 例えば、数値を「768px」とした場合、ブラウザの横幅が768px以上の時にのみ、そのスタイルが適用されるようになる
- この数値をブレイクポイントという

## 自由にボックスを移動させるには
- divダグで囲うboxをうまく工夫することで、好きなボックスを中央に配置したり、することができる。

```css
	sample2.css

	@media (min-width: 768px) {
		.boxA:after {
			content: "";
			display: block;
			clear: both;
		}

		.boxB {
			float: left;
			width: 80%;
		}

		.box4 {
			float: left;
			width: 20%;
		}

		.boxB:after {
			content: "";
			diplay: block;
			clear: both;
		}

		.box2 {
			float: right;
			width: 75%;
		}

		.box3 {
			float: left;
			width: 25%;
		}
	}
```

```html
	sample2.html

	<body>
		<div class="box1">
			BOX1
		</div>
		<div class="boxA">
			<div class="boxB">
				<div class="box2">
					BOX2
				</div>
				<div class="box3">
					BOX3
				</div>
			</div>
			<div class="box4">
				BOX4
			</div>
		</div>
	</body>
```

## レスポンシブデザインに中間のステップを追加する
- cssのブレイクポイントをさらに1つ追加する
- ブレイクポイントの違いはあれど、同じ記述を2つのブレイクポイント間で行う場合は、下記のようにまとめることができる

```css
	sample3.css

	@media (min-width: 768px) {
		.boxA:after {
			content: "";
			display: block;
			clear: both;
		}

		.boxB {
			float: left;
			width: 80%;
		}

		.box4 {
			float: left;
			width: 20%;
		}
	}

	@media (min-width: 600px) {
		.boxB:after {
			content: "";
			diplay: block;
			clear: both;
		}

		.box2 {
			float: right;
			width: 75%;
		}

		.box3 {
			float: left;
			width: 25%;
		}
	}
```

## ボックスを重ねて表示する場合
- cssの`position: absolute`や`position: relative`で調整する











