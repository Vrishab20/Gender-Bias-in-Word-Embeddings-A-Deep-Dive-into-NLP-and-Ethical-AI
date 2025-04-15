<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8"/><title>Gender Bias in Word Embeddings: A Deep Dive into NLP and Ethical AI</title><style>
/* cspell:disable-file */
/* webkit printing magic: print all background colors */
html {
	-webkit-print-color-adjust: exact;
}
* {
	box-sizing: border-box;
	-webkit-print-color-adjust: exact;
}

html,
body {
	margin: 0;
	padding: 0;
}
@media only screen {
	body {
		margin: 2em auto;
		max-width: 900px;
		color: rgb(55, 53, 47);
	}
}

body {
	line-height: 1.5;
	white-space: pre-wrap;
}

a,
a.visited {
	color: inherit;
	text-decoration: underline;
}

.pdf-relative-link-path {
	font-size: 80%;
	color: #444;
}

h1,
h2,
h3 {
	letter-spacing: -0.01em;
	line-height: 1.2;
	font-weight: 600;
	margin-bottom: 0;
}

.page-title {
	font-size: 2.5rem;
	font-weight: 700;
	margin-top: 0;
	margin-bottom: 0.75em;
}

h1 {
	font-size: 1.875rem;
	margin-top: 1.875rem;
}

h2 {
	font-size: 1.5rem;
	margin-top: 1.5rem;
}

h3 {
	font-size: 1.25rem;
	margin-top: 1.25rem;
}

.source {
	border: 1px solid #ddd;
	border-radius: 3px;
	padding: 1.5em;
	word-break: break-all;
}

.callout {
	border-radius: 3px;
	padding: 1rem;
}

figure {
	margin: 1.25em 0;
	page-break-inside: avoid;
}

figcaption {
	opacity: 0.5;
	font-size: 85%;
	margin-top: 0.5em;
}

mark {
	background-color: transparent;
}

.indented {
	padding-left: 1.5em;
}

hr {
	background: transparent;
	display: block;
	width: 100%;
	height: 1px;
	visibility: visible;
	border: none;
	border-bottom: 1px solid rgba(55, 53, 47, 0.09);
}

img {
	max-width: 100%;
}

@media only print {
	img {
		max-height: 100vh;
		object-fit: contain;
	}
}

@page {
	margin: 1in;
}

.collection-content {
	font-size: 0.875rem;
}

.column-list {
	display: flex;
	justify-content: space-between;
}

.column {
	padding: 0 1em;
}

.column:first-child {
	padding-left: 0;
}

.column:last-child {
	padding-right: 0;
}

.table_of_contents-item {
	display: block;
	font-size: 0.875rem;
	line-height: 1.3;
	padding: 0.125rem;
}

.table_of_contents-indent-1 {
	margin-left: 1.5rem;
}

.table_of_contents-indent-2 {
	margin-left: 3rem;
}

.table_of_contents-indent-3 {
	margin-left: 4.5rem;
}

.table_of_contents-link {
	text-decoration: none;
	opacity: 0.7;
	border-bottom: 1px solid rgba(55, 53, 47, 0.18);
}

table,
th,
td {
	border: 1px solid rgba(55, 53, 47, 0.09);
	border-collapse: collapse;
}

table {
	border-left: none;
	border-right: none;
}

th,
td {
	font-weight: normal;
	padding: 0.25em 0.5em;
	line-height: 1.5;
	min-height: 1.5em;
	text-align: left;
}

th {
	color: rgba(55, 53, 47, 0.6);
}

ol,
ul {
	margin: 0;
	margin-block-start: 0.6em;
	margin-block-end: 0.6em;
}

li > ol:first-child,
li > ul:first-child {
	margin-block-start: 0.6em;
}

ul > li {
	list-style: disc;
}

ul.to-do-list {
	padding-inline-start: 0;
}

ul.to-do-list > li {
	list-style: none;
}

.to-do-children-checked {
	text-decoration: line-through;
	opacity: 0.375;
}

ul.toggle > li {
	list-style: none;
}

ul {
	padding-inline-start: 1.7em;
}

ul > li {
	padding-left: 0.1em;
}

ol {
	padding-inline-start: 1.6em;
}

ol > li {
	padding-left: 0.2em;
}

.mono ol {
	padding-inline-start: 2em;
}

.mono ol > li {
	text-indent: -0.4em;
}

.toggle {
	padding-inline-start: 0em;
	list-style-type: none;
}

/* Indent toggle children */
.toggle > li > details {
	padding-left: 1.7em;
}

.toggle > li > details > summary {
	margin-left: -1.1em;
}

.selected-value {
	display: inline-block;
	padding: 0 0.5em;
	background: rgba(206, 205, 202, 0.5);
	border-radius: 3px;
	margin-right: 0.5em;
	margin-top: 0.3em;
	margin-bottom: 0.3em;
	white-space: nowrap;
}

.collection-title {
	display: inline-block;
	margin-right: 1em;
}

.page-description {
	margin-bottom: 2em;
}

.simple-table {
	margin-top: 1em;
	font-size: 0.875rem;
	empty-cells: show;
}
.simple-table td {
	height: 29px;
	min-width: 120px;
}

.simple-table th {
	height: 29px;
	min-width: 120px;
}

.simple-table-header-color {
	background: rgb(247, 246, 243);
	color: black;
}
.simple-table-header {
	font-weight: 500;
}

time {
	opacity: 0.5;
}

.icon {
	display: inline-block;
	max-width: 1.2em;
	max-height: 1.2em;
	text-decoration: none;
	vertical-align: text-bottom;
	margin-right: 0.5em;
}

img.icon {
	border-radius: 3px;
}

.user-icon {
	width: 1.5em;
	height: 1.5em;
	border-radius: 100%;
	margin-right: 0.5rem;
}

.user-icon-inner {
	font-size: 0.8em;
}

.text-icon {
	border: 1px solid #000;
	text-align: center;
}

.page-cover-image {
	display: block;
	object-fit: cover;
	width: 100%;
	max-height: 30vh;
}

.page-header-icon {
	font-size: 3rem;
	margin-bottom: 1rem;
}

.page-header-icon-with-cover {
	margin-top: -0.72em;
	margin-left: 0.07em;
}

.page-header-icon img {
	border-radius: 3px;
}

.link-to-page {
	margin: 1em 0;
	padding: 0;
	border: none;
	font-weight: 500;
}

p > .user {
	opacity: 0.5;
}

td > .user,
td > time {
	white-space: nowrap;
}

input[type="checkbox"] {
	transform: scale(1.5);
	margin-right: 0.6em;
	vertical-align: middle;
}

p {
	margin-top: 0.5em;
	margin-bottom: 0.5em;
}

.image {
	border: none;
	margin: 1.5em 0;
	padding: 0;
	border-radius: 0;
	text-align: center;
}

.code,
code {
	background: rgba(135, 131, 120, 0.15);
	border-radius: 3px;
	padding: 0.2em 0.4em;
	border-radius: 3px;
	font-size: 85%;
	tab-size: 2;
}

code {
	color: #eb5757;
}

.code {
	padding: 1.5em 1em;
}

.code-wrap {
	white-space: pre-wrap;
	word-break: break-all;
}

.code > code {
	background: none;
	padding: 0;
	font-size: 100%;
	color: inherit;
}

blockquote {
	font-size: 1.25em;
	margin: 1em 0;
	padding-left: 1em;
	border-left: 3px solid rgb(55, 53, 47);
}

.bookmark {
	text-decoration: none;
	max-height: 8em;
	padding: 0;
	display: flex;
	width: 100%;
	align-items: stretch;
}

.bookmark-title {
	font-size: 0.85em;
	overflow: hidden;
	text-overflow: ellipsis;
	height: 1.75em;
	white-space: nowrap;
}

.bookmark-text {
	display: flex;
	flex-direction: column;
}

.bookmark-info {
	flex: 4 1 180px;
	padding: 12px 14px 14px;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}

.bookmark-image {
	width: 33%;
	flex: 1 1 180px;
	display: block;
	position: relative;
	object-fit: cover;
	border-radius: 1px;
}

.bookmark-description {
	color: rgba(55, 53, 47, 0.6);
	font-size: 0.75em;
	overflow: hidden;
	max-height: 4.5em;
	word-break: break-word;
}

.bookmark-href {
	font-size: 0.75em;
	margin-top: 0.25em;
}

.sans { font-family: ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol"; }
.code { font-family: "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace; }
.serif { font-family: Lyon-Text, Georgia, ui-serif, serif; }
.mono { font-family: iawriter-mono, Nitti, Menlo, Courier, monospace; }
.pdf .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK JP'; }
.pdf:lang(zh-CN) .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK SC'; }
.pdf:lang(zh-TW) .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK TC'; }
.pdf:lang(ko-KR) .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK KR'; }
.pdf .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK JP'; }
.pdf:lang(zh-CN) .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK SC'; }
.pdf:lang(zh-TW) .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK TC'; }
.pdf:lang(ko-KR) .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK KR'; }
.pdf .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK JP'; }
.pdf:lang(zh-CN) .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK SC'; }
.pdf:lang(zh-TW) .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK TC'; }
.pdf:lang(ko-KR) .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK KR'; }
.pdf .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK JP'; }
.pdf:lang(zh-CN) .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK SC'; }
.pdf:lang(zh-TW) .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK TC'; }
.pdf:lang(ko-KR) .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK KR'; }
.highlight-default {
	color: rgba(55, 53, 47, 1);
}
.highlight-gray {
	color: rgba(120, 119, 116, 1);
	fill: rgba(120, 119, 116, 1);
}
.highlight-brown {
	color: rgba(159, 107, 83, 1);
	fill: rgba(159, 107, 83, 1);
}
.highlight-orange {
	color: rgba(217, 115, 13, 1);
	fill: rgba(217, 115, 13, 1);
}
.highlight-yellow {
	color: rgba(203, 145, 47, 1);
	fill: rgba(203, 145, 47, 1);
}
.highlight-teal {
	color: rgba(68, 131, 97, 1);
	fill: rgba(68, 131, 97, 1);
}
.highlight-blue {
	color: rgba(51, 126, 169, 1);
	fill: rgba(51, 126, 169, 1);
}
.highlight-purple {
	color: rgba(144, 101, 176, 1);
	fill: rgba(144, 101, 176, 1);
}
.highlight-pink {
	color: rgba(193, 76, 138, 1);
	fill: rgba(193, 76, 138, 1);
}
.highlight-red {
	color: rgba(212, 76, 71, 1);
	fill: rgba(212, 76, 71, 1);
}
.highlight-default_background {
	color: rgba(55, 53, 47, 1);
}
.highlight-gray_background {
	background: rgba(248, 248, 247, 1);
}
.highlight-brown_background {
	background: rgba(244, 238, 238, 1);
}
.highlight-orange_background {
	background: rgba(251, 236, 221, 1);
}
.highlight-yellow_background {
	background: rgba(251, 243, 219, 1);
}
.highlight-teal_background {
	background: rgba(237, 243, 236, 1);
}
.highlight-blue_background {
	background: rgba(231, 243, 248, 1);
}
.highlight-purple_background {
	background: rgba(248, 243, 252, 1);
}
.highlight-pink_background {
	background: rgba(252, 241, 246, 1);
}
.highlight-red_background {
	background: rgba(253, 235, 236, 1);
}
.block-color-default {
	color: inherit;
	fill: inherit;
}
.block-color-gray {
	color: rgba(120, 119, 116, 1);
	fill: rgba(120, 119, 116, 1);
}
.block-color-brown {
	color: rgba(159, 107, 83, 1);
	fill: rgba(159, 107, 83, 1);
}
.block-color-orange {
	color: rgba(217, 115, 13, 1);
	fill: rgba(217, 115, 13, 1);
}
.block-color-yellow {
	color: rgba(203, 145, 47, 1);
	fill: rgba(203, 145, 47, 1);
}
.block-color-teal {
	color: rgba(68, 131, 97, 1);
	fill: rgba(68, 131, 97, 1);
}
.block-color-blue {
	color: rgba(51, 126, 169, 1);
	fill: rgba(51, 126, 169, 1);
}
.block-color-purple {
	color: rgba(144, 101, 176, 1);
	fill: rgba(144, 101, 176, 1);
}
.block-color-pink {
	color: rgba(193, 76, 138, 1);
	fill: rgba(193, 76, 138, 1);
}
.block-color-red {
	color: rgba(212, 76, 71, 1);
	fill: rgba(212, 76, 71, 1);
}
.block-color-default_background {
	color: inherit;
	fill: inherit;
}
.block-color-gray_background {
	background: rgba(248, 248, 247, 1);
}
.block-color-brown_background {
	background: rgba(244, 238, 238, 1);
}
.block-color-orange_background {
	background: rgba(251, 236, 221, 1);
}
.block-color-yellow_background {
	background: rgba(251, 243, 219, 1);
}
.block-color-teal_background {
	background: rgba(237, 243, 236, 1);
}
.block-color-blue_background {
	background: rgba(231, 243, 248, 1);
}
.block-color-purple_background {
	background: rgba(248, 243, 252, 1);
}
.block-color-pink_background {
	background: rgba(252, 241, 246, 1);
}
.block-color-red_background {
	background: rgba(253, 235, 236, 1);
}
.select-value-color-uiBlue { background-color: undefined; }
.select-value-color-pink { background-color: rgba(225, 136, 179, 0.27); }
.select-value-color-purple { background-color: rgba(168, 129, 197, 0.27); }
.select-value-color-green { background-color: rgba(123, 183, 129, 0.27); }
.select-value-color-gray { background-color: rgba(84, 72, 49, 0.15); }
.select-value-color-transparentGray { background-color: undefined; }
.select-value-color-translucentGray { background-color: undefined; }
.select-value-color-orange { background-color: rgba(224, 124, 57, 0.27); }
.select-value-color-brown { background-color: rgba(210, 162, 141, 0.35); }
.select-value-color-red { background-color: rgba(244, 171, 159, 0.4); }
.select-value-color-yellow { background-color: rgba(236, 191, 66, 0.39); }
.select-value-color-blue { background-color: rgba(93, 165, 206, 0.27); }
.select-value-color-pageGlass { background-color: undefined; }
.select-value-color-washGlass { background-color: undefined; }

.checkbox {
	display: inline-flex;
	vertical-align: text-bottom;
	width: 16;
	height: 16;
	background-size: 16px;
	margin-left: 2px;
	margin-right: 5px;
}

.checkbox-on {
	background-image: url("data:image/svg+xml;charset=UTF-8,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20viewBox%3D%220%200%2016%2016%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%0A%3Crect%20width%3D%2216%22%20height%3D%2216%22%20fill%3D%22%2358A9D7%22%2F%3E%0A%3Cpath%20d%3D%22M6.71429%2012.2852L14%204.9995L12.7143%203.71436L6.71429%209.71378L3.28571%206.2831L2%207.57092L6.71429%2012.2852Z%22%20fill%3D%22white%22%2F%3E%0A%3C%2Fsvg%3E");
}

.checkbox-off {
	background-image: url("data:image/svg+xml;charset=UTF-8,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20viewBox%3D%220%200%2016%2016%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%0A%3Crect%20x%3D%220.75%22%20y%3D%220.75%22%20width%3D%2214.5%22%20height%3D%2214.5%22%20fill%3D%22white%22%20stroke%3D%22%2336352F%22%20stroke-width%3D%221.5%22%2F%3E%0A%3C%2Fsvg%3E");
}
	
</style></head><body><article id="1a950465-ff70-802e-8119-ef1fb5d956d2" class="page serif"><header><img class="page-cover-image" src="https://www.notion.so/images/page-cover/gradients_11.jpg" style="object-position:center 40%"/><div class="page-header-icon page-header-icon-with-cover"><span class="icon">👥</span></div><h1 class="page-title"><strong>Gender Bias in Word Embeddings: A Deep Dive into NLP and Ethical AI</strong></h1><p class="page-description"></p></header><div class="page-body"><p id="1a950465-ff70-81b9-adfd-d27d9bfb07ee" class="block-color-gray">FEBRUARY 28, 2025</p><p id="1a950465-ff70-81c7-980e-f5f5bc971c81" class="block-color-gray">VRISHAB PRSANTH DAVEY<br/>vdave048@uottawa.ca<br/></p><p id="1a950465-ff70-80e6-8237-ff9ec3da9858" class="">#UO - 300438343</p><figure class="block-color-gray_background callout" style="white-space:pre-wrap;display:flex" id="1a950465-ff70-81df-841f-f1ed15ae088d"><div style="font-size:1.5em"><span class="icon">📌</span></div><div style="width:100%">Abstract</div></figure><p id="1aa50465-ff70-80b9-95b4-f3ed6d624041" class="">Word embeddings are numeric representations of meaning derived from word co-occurrence statistics in human-produced texts. These embeddings, foundational to many Natural Language Processing (NLP) applications, have been found to encode and perpetuate social biases, including gender bias. This blog explores gender bias in widely used static English word embeddings trained on internet corpora (GloVe 2014, fastText 2017) [58]. While prior research has focused on specific gender associations, this analysis broadens the scope to include word frequency disparities, parts-of-speech tendencies, semantic clustering, and sentiment dimensions. Findings indicate that 77% of the 1,000 most frequent words in these embeddings are more associated with men [58], reinforcing a masculine default in online language. Male-associated words are predominantly verbs, aligning with perceptions of agency and action, while female-associated words are often adjectives and adverbs, reinforcing descriptive stereotypes. Semantic clustering reveals that men are linked with professions, technology, and power, whereas women are frequently associated with appearance, relationships, and even explicit content. These findings underscore the necessity of mitigating biases in NLP models to create fairer AI applications.</p><h1 id="1a950465-ff70-81e5-94d3-c961db0381c9" class="">Introduction &amp; Background</h1><p id="1a950465-ff70-802c-af3c-d731055b7f59" class="">All credits for this research go to <strong>Aylin Caliskan et al. (2022)</strong> for their hard work in conducting this study. I have tried my best to reference and summarize the key insights from their paper. This blog aims to provide an accessible understanding of their findings and the implications of how gender bias in word embeddings, foundational to many <strong>Natural Language Processing (NLP) applications</strong>, encode and perpetuate gender biases [58].</p><p id="1aa50465-ff70-809d-a83c-e4cce0d90fa8" class="">The role of Natural Language Processing (NLP) in daily life has grown exponentially, powering applications from machine translation to automated resume screening [7].  A key component of these applications is word embeddings—compressed, numeric representations of word meanings based on large-scale language data. However, research has shown that these embeddings inherit biases present in human-generated text, subtly reinforcing societal stereotypes[9-12].</p><p id="1a950465-ff70-8069-ab22-c5a65eb56a31" class="">Among the most pervasive biases is gender bias, which affects a wide range of NLP applications. Prior studies have revealed that word embeddings associate men with career-related terms and women with family-oriented words, perpetuating traditional gender role [12, 17, 26]. This blog takes a comprehensive approach to gender bias in word embeddings by analyzing not just direct word associations but also syntactic structures, semantic clusters, and psychological dimensions such as valence, arousal, and dominance.</p><figure id="1a950465-ff70-807e-a0f4-ff5de1baedad" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image.png"><img style="width:709.9874877929688px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image.png"/></a></figure><p id="1a950465-ff70-806a-bab1-ca5c9a984abd" class=""><strong>                          </strong><em><strong>Figure 1: Visualization of Gender Associations in Word Embeddings</strong></em></p><p id="1a950465-ff70-8087-bb1e-f4ed9afa9f64" class="">As demonstrated in <strong>Figure 1</strong>, the gender associations of the 1,000 most frequently occurring words in GloVe embeddings exhibit a clear imbalance, with a stronger association toward male-related words. This pattern persists even at broader scales, affecting NLP systems at a foundational level. The implications of these biases are far-reaching—from hiring algorithms that favor male candidates to AI-driven content moderation systems that reinforce gendered language disparities.</p><p id="1a950465-ff70-80f5-adef-ed7f9ad366d9" class="">In this blog, I will dissect these findings, explain their implications, and discuss potential mitigation strategies for reducing gender bias in NLP models.</p><h1 id="1a950465-ff70-81e3-8254-f54ea7ee12c7" class=""><strong>Understanding Gender Bias in Word Embeddings</strong></h1><p id="1aa50465-ff70-802c-b266-c4263699b3e6" class="">Examining past work in the subject helps one to understand the level of gender bias in NLP. Previous research has found bias in many different spheres, from more general language structures to direct word associations. Based on their co-occurrence patterns in text corpora, <strong>word embeddings</strong> including those employed in <strong>GloVe and fastText</strong> offer continuous-valued vector representations of words [58]. These embeddings reflect cultural norms and prejudices present in training data, hence promoting <strong>gender stereotypes in NLP applications</strong> even if they efficiently capture links between words.</p><p id="1aa50465-ff70-80aa-bef5-d2cd3389c85f" class="">The <strong>Word Embedding Association Test</strong> and its variation, <strong>Single- Category WEAT </strong>[58] are among the most often used techniques for spotting bias in embeddings. These assessments assess the relative association of words with various attribute categories (e.g., male vs. female terms), and past studies have shown that such prejudices <strong>fit</strong> real-world occupational gender inequalities. Comparisons with <strong>human psychological judgments</strong> have confirmed that male-associated terms are typically related with <strong>dominance and arousal</strong> while female-associated words tend to score higher on <strong>valence (pleasantness</strong>). This has important ramifications for <strong>AI models that process and interpret human language</strong> since these prejudices affect automated decision-making in content creation, recommendations, and hiring as well as in content development.</p><p id="1aa50465-ff70-802d-828a-ce7631fa0659" class="">Research has also repeatedly shown that <strong>gender stereotypes</strong> endure in word embeddings, so supporting conventional relationships between <strong>men and leadership roles</strong> and <strong>women with domestic and appearance-related terms</strong>. Although several approaches have been suggested to reduce these prejudices, most debiassing strategies fall short in <strong>completely eliminating the underlying gender associations</strong>. Moreover, <strong>word frequency</strong> is quite important for bias transmission; male-associated terms show <strong>more often</strong> in embeddings. This overrepresentation of male-linked words can lead to decreased visibility of underrepresented groups in AI-driven applications, hence adding to <strong>systemic bias in NLP models</strong>. Establishing <strong>fairer language models</strong> that more precisely reflect linguistic variation depends on addressing these discrepancies.</p><p id="1aa50465-ff70-80e1-a428-d20811bf3834" class="">By means of this investigation of related work, it is evident that <strong>gender bias in word embeddings is a well-documented problem with far-reaching consequences</strong>. These prejudices will be further broken out in the next parts, together with possible remedies to lessen them.</p><h1 id="1a950465-ff70-80d7-a11b-d07b46111f11" class=""><strong>Data Collection and Experimental Approach</strong></h1><p id="1aa50465-ff70-806d-b49f-df99138d7ae7" class="">We need datasets measuring human qualities, gender associations, and emotional aspects of language if we are to examine gender bias in NLP models. Our investigation centers on a few fundamental components. Trained on the <strong>Common Crawl corpus</strong>, more especially <strong>GloVe (trained on 840 billion tokens) and fastText (trained on 600 billion tokens),</strong> we employ <strong>300-dimensional word embeddings</strong>. Standard in artificial intelligence research, these extensively utilized embeddings also reflect prejudices in human language. We use <strong>SC-WEAT</strong>, a technique that measures the relative association of words with male and female identities, to evaluate gender correlations. Whereas a <strong>negative value</strong> denotes masculine prejudice, a <strong>positive effect size</strong> implies a closer link to female-associated phrases.</p><p id="1aa50465-ff70-8087-b8ff-fee57eed1848" class="">We investigate <strong>emotional dimensions</strong> by using the <strong>NRC-VAD Lexicon</strong>, a psycholinguistic dataset including human-rated ratings for <strong>valence (positivity), arousal (intensity), and dominance (control)</strong> beyond direct word connections. Previous studies indicate that <strong>female-associated words</strong> show <strong>higher valence</strong> whereas <strong>male-associated words</strong> usually show <strong>higher dominance and arousal scores</strong>. Furthermore, greatly affects how bias spreads in artificial intelligence systems is word frequency. We examine the frequency of gendered terms using third-party estimation tools since embeddings store words based on frequency but lack clear count values. Studies indicate that commonly occurring words effect AI behavior: if male-associated words predominate embeddings, <strong>AI-driven decision-making could be disproportionately influenced by male-centric language</strong>.</p><p id="1aa50465-ff70-8044-b8c9-c01df7ce581b" class="">We curate a <strong>Big Tech lexicon</strong> including businesses like <strong>Google, Microsoft, Amazon, and Facebook</strong> [58] to investigate gender bias in professional environments. Our results show that <strong>62% of Big Tech-related words</strong> are more firmly connected with men, so supporting male dominance in conversations on technology and invention. The next part will investigate to evaluate gender bias in several linguistic structures.</p><h1 id="1a950465-ff70-80df-9b4c-dd368e6141ae" class="">Experimental Methodology</h1><p id="1a950465-ff70-8067-ad79-c19fe3f06f9e" class="">We conduct multiple analyses to assess gender bias across different linguistic structures:</p><ul id="1a950465-ff70-8003-860e-eadbd2541206" class="bulleted-list"><li style="list-style-type:disc"><strong>SC-WEAT for gender bias effect sizes</strong> across different frequency ranges (top 100, 1,000, and 10,000 most frequent words).</li></ul><ul id="1a950465-ff70-8038-b95f-d7629ead1b66" class="bulleted-list"><li style="list-style-type:disc"><strong>Parts-of-speech analysis</strong>, categorizing gendered words as nouns, adjectives, or verbs.</li></ul><ul id="1a950465-ff70-8069-8c78-e20bbb13a876" class="bulleted-list"><li style="list-style-type:disc"><strong>Clustering algorithms</strong>, grouping gender-associated words into conceptual domains (e.g., leadership, appearance, technology).</li></ul><ul id="1a950465-ff70-80a3-a33c-fe8967e7ca98" class="bulleted-list"><li style="list-style-type:disc"><strong>Correlation analysis</strong>, measuring how gender bias aligns with valence, arousal, and dominance scores.</li></ul><p id="1a950465-ff70-80d2-a438-f8d1e2e7d04c" class="">These analyses provide a multidimensional view of gender bias in NLP, helping us identify patterns that affect AI applications. The next section will dive deeper into Understanding how Gender Bias Manifests and discuss their implications for AI fairness.</p><h1 id="1a950465-ff70-80a8-9d66-f0ad1663216f" class="">Understanding How Gender Bias Manifests?</h1><p id="1a950465-ff70-80fd-8966-fc48a31e057a" class="">Word frequency distributions are one of the main forms in which gender bias shows in word embeddings. As shown in Figure 2, pretrained GloVe and fastText embeddings show a high male connection for most often occurring terms. This suggests that words connected to men show more often in big size text corpora, so supporting a masculine default in NLP models. </p><figure id="1a950465-ff70-807d-9026-caa1bab8b1c6" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%201.png"><img style="width:444px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%201.png"/></a></figure><p id="1a950465-ff70-80b0-a120-facfb8652de7" class=""><strong>           Figure 2: Most Frequent Words in Pretrained GloVe and fastText Word Embeddings </strong>[58].</p><p id="1a950465-ff70-8069-bb4d-d29275ec18e3" class="">Table 1 and Table 2, measure the distribution of male, and female associated words over several frequency ranges, give a thorough description of these frequency-based gender correlations. Though fastText is somewhat less biassed in terms of frequency percentage, the trends across both GloVe and fastText are constant.</p><figure id="1a950465-ff70-80c5-9c32-ea003cb875ac" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%202.png"><img style="width:709.9500122070312px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%202.png"/></a></figure><p id="1a950465-ff70-80c7-bf73-c3d741b2d14e" class=""><strong>               Table 1: The Most Frequent Words in the GloVe Embedding Vocabulary </strong>[58].</p><figure id="1a950465-ff70-8063-834f-dc70764e7774" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%203.png"><img style="width:709.9874877929688px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%203.png"/></a></figure><p id="1a950465-ff70-807d-9c4a-ea830d2a85af" class=""><strong>                   Table 2: The Most Frequent Words in the fastText Embedding Vocabulary </strong>[58].</p><h2 id="1aa50465-ff70-802d-9aba-cd7e56cc82a5" class=""><strong>Concept Clustering and Gendered Associations</strong></h2><p id="1aa50465-ff70-803c-a233-da75f8b55056" class="">Beyond frequency distributions, gender bias in word embeddings affects conceptual grouping of words. We classed the 1,000 most often occurring male- and female-associated terms using unsupervised clustering methods. Table 3 illustrates the outcomes, which reveal that whilst male-associated words are more likely to be clustered under engineering, leadership, money, and Big Tech-related concepts, female-associated words commonly cluster around themes such as beauty, fashion, relationships, and domestic responsibilities.</p><figure id="1a950465-ff70-806f-8ded-d2d9f5265653" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%204.png"><img style="width:709.9874877929688px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%204.png"/></a></figure><p id="1a950465-ff70-80ed-96b0-fa8afebe90b1" class=""><strong>                    Table 3: Concept Clusters for Male- and Female-Associated Words </strong>[58].</p><p id="1a950465-ff70-808d-9c1d-d6d12e37376e" class="">To further illustrate these findings, Figure <strong>3</strong> provides concrete examples of words within each gender-associated cluster. Notably, two of the most prominent female-associated clusters are related to <strong>sexual profanities and explicit adult content</strong>, reinforcing concerns about how NLP systems may inadvertently perpetuate harmful stereotypes.</p><figure id="1a950465-ff70-809b-b9a3-dee0a6bb3cbd" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%205.png"><img style="width:393px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%205.png"/></a></figure><p id="1a950465-ff70-80e4-ad19-ecac5b902065" class=""><strong>                           Figure 3: Examples of Concept Clusters for Male and Female Words </strong>[58].</p><h2 id="1aa50465-ff70-80d5-95fa-f783f32d9955" class=""><strong>Parts-of-Speech and Gender Disparities</strong></h2><p id="1a950465-ff70-802e-acd5-d01d303178b1" class="">The analysis of <strong>parts-of-speech (POS) distributions</strong> within word embeddings reveals notable gender disparities. As depicted in <strong>Figure 4</strong>, words associated with male attributes (d ≥ 0.50) in the GloVe vocabulary tend to cluster into conceptual groups such as <strong>adventure, engineering, science, sports, violence, and war </strong>[58]. These findings suggest that male-associated words are more likely to be linked with active, high-status, and traditionally male-dominated domains.</p><figure id="1a950465-ff70-8069-b1b1-e1cb261ec263" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%206.png"><img style="width:387px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%206.png"/></a></figure><p id="1a950465-ff70-8094-b0f0-f45c02173063" class=""><strong>                                               Figure 4: Concept Clusters for Male-Associated Words </strong>[58].</p><p id="1a950465-ff70-8097-96da-eba1cf1f290e" class="">A further breakdown of POS associations in GloVe and fastText embeddings, provided in <strong>Tables 4 and 5</strong>, confirms that <strong>female-associated words are predominantly adjectives and adverbs</strong>, while <strong>male-associated words are more likely to be verbs and nouns</strong>. This pattern reinforces traditional gender roles, where men are depicted as active agents performing actions, while women are often described through their attributes.</p><figure id="1a950465-ff70-80d5-9497-ec5ba4113fa2" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%207.png"><img style="width:485px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%207.png"/></a></figure><p id="1a950465-ff70-8008-8f17-fa26ceeadb04" class=""><strong>                                     Table 4: Gender and Parts-of-Speech Associations in GloVe </strong>[58].</p><figure id="1a950465-ff70-80a4-8b3d-e0ca4623d4d6" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%208.png"><img style="width:497px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%208.png"/></a></figure><p id="1a950465-ff70-800f-b733-f7abc0c3d9e6" class=""><strong>                                      Table 5: Gender and Parts-of-Speech Associations in fastText </strong>[58].</p><p id="1a950465-ff70-8064-8d4a-d61bbfc98489" class="">For instance, in the <strong>GloVe embeddings</strong>, <strong>113 of the 1,000 most frequent female-associated words are adjectives</strong>, compared to <strong>66 male-associated adjectives</strong>[58]. Similarly, the <strong>fastText embeddings</strong> show this same pattern, with <strong>female-associated words being more descriptive than their male counterparts</strong>.</p><p id="1aa50465-ff70-80be-8fb2-f9ac806ea26f" class="">Additionally, <strong>adverbs</strong> follow this trend—<strong>133 of the 10,000 most frequent female-associated words in the GloVe embeddings are adverbs</strong>, compared to just <strong>45 adverbs among male-associated words</strong>[58].</p><h2 id="1a950465-ff70-80b6-856c-f7346248e9f1" class="">The &quot;Other&quot; Category and Historical Significance</h2><p id="1aa50465-ff70-80f7-a5ee-d3bfbda85020" class="">The <strong>&quot;Other&quot; POS category</strong> shows another important difference with regard to pronouns, interjections, and number words. Male-associated words abound in this category, as seen in <strong>Tables 4 and 5</strong> particularly in historical, scientific, and numerical settings.</p><p id="1aa50465-ff70-80d4-bbd1-f6c774dcc17a" class=""><strong>677 of the 1,252 &quot;Other&quot; male-associated words</strong> at N = 10,000 are related in the <strong>GloVe embeddings</strong> to numerical, measurement, and historical issues [58].<br/>Comparatively to merely <br/><strong>482 verbs among female-associated words</strong>, <strong>613 of the 10,000 male-associated words</strong> are verbs in the <strong>fastText embeddings</strong>.</p><p id="1aa50465-ff70-8084-918e-e8effe0cbf8d" class="">This trend points to a <strong>systematic gender bias</strong> whereby female-associated words mostly stress <strong>traits, feelings, and descriptions</strong> while male-associated words fit intellectual, technical, and action-oriented areas.</p><h2 id="1a950465-ff70-8072-b25b-e84793e98793" class="">Singular vs. Plural Noun Bias</h2><p id="1aa50465-ff70-80a1-ac63-e4db1afae878" class="">One last issue of thought is the variation in <strong>singular and plural noun use</strong> in gendered nouns. As noted in the study:</p><p id="1aa50465-ff70-8099-b1ca-f773e484740b" class="">Comparatively to <strong>92 plural male-associated nouns</strong>, 166 of the 1,000 most frequent terms linked with women in GloVe embeddings are plural common nouns [58].<br/>This trend points to a <br/><strong>linguistic tendency</strong> whereby women are more commonly described in collective terms while men are referred as individuals, hence strengthening gendered language positioning.</p><p id="1aa50465-ff70-80f8-8c74-ef315ca92585" class="">Applications of NLP, like text production, sentiment analysis, and AI-driven content suggestions, depend much on these prejudices. Unconsciously, the over-representation of men in action-oriented roles and women in descriptive, communal, and emotional settings shapes how artificial intelligence models understand and create text. Development of fair and balanced AI-driven communication systems depends on addressing these prejudices.</p><p id="1aa50465-ff70-80a8-8534-c48dcdaee1a4" class="">We investigated the psychological aspects of gender bias in word embeddings by means of correlations with <strong>valence (Pleasantness), arousal (intensity), and dominance (power/control)</strong> employing the <strong>NRC-VAD lexicon</strong>. Whereas male-related terms connect negatively with valence but positively with <strong>dominance and arousal</strong>, female-associated words tend to correlate positively with <strong>valence</strong>, suggesting they are associated with pleasantness.</p><figure id="1a950465-ff70-80ec-a790-e733e22d6f36" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%209.png"><img style="width:394px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%209.png"/></a></figure><p id="1a950465-ff70-8078-b707-f6e54a488ecb" class=""><strong>Table 6: Female-Associated Words Correlate More Strongly with Valence, While              Male-Associated Words Correlate with Arousal and Dominance </strong>[58].</p><p id="1a950465-ff70-80c5-9ea5-cb1d188eb94f" class="">This suggests that <strong>words related to men in word embeddings are more likely to evoke feelings of power and intensity</strong>, whereas words related to women tend to be linked with positive emotions but lower dominance. The same pattern persists when broken-down by-<strong>word frequency ranges</strong>, as observed in <strong>Table 7</strong>, which examines correlations by gender-association effect size.</p><figure id="1a950465-ff70-804f-b3cc-c34a0103c6f5" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%2010.png"><img style="width:389px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%2010.png"/></a></figure><p id="1a950465-ff70-8054-b9bc-d901db492f7c" class=""><strong>                                Table 7: Gender Association Effect Size and NRC-VAD Ratings </strong>[58].</p><h2 id="1a950465-ff70-8012-b3c4-f30606991771" class="">Gender Bias in Big Tech Terminology</h2><p id="1a950465-ff70-80ad-b69b-c9810557eebf" class="">One especially startling example of gender bias is seen in <strong>Big Tech terminology</strong>. Words connected with <strong>technology-related professions, leadership, and innovation</strong> most definitely correlate with male-associated words in both GloVe and fastText embeddings, as seen in <strong>Figure 5</strong>.</p><figure id="1a950465-ff70-80de-b91c-f0ded7b81c00" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%2011.png"><img style="width:372px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%2011.png"/></a></figure><p id="1a950465-ff70-8049-aaf5-f15df5e4bbc2" class=""><strong>                                               Figure 5: Big Tech Gender Association by Effect Size </strong>[58].</p><p id="1aa50465-ff70-80ac-95b4-f91cb9eb11cc" class="">This finding is crucial, as <strong>AI-driven hiring platforms, search algorithms, and recommendation systems trained on these embeddings could inadvertently reinforce existing gender disparities in STEM fields</strong>. Addressing such biases is critical for ensuring <strong>fair representation of women in technology-related discussions and AI applications</strong>.</p><p id="1aa50465-ff70-8093-9629-e8d129407bf1" class="">GloVe and fastText static word embeddings, across all levels of analysis, demonstrate a higher association with male-related words than female-related words. Of the <strong>10,000 most frequent words</strong> in the GloVe vocabulary, <strong>1,187</strong> exhibit a large effect size association with men, compared to only <strong>611</strong> with a strong association with women [58]. <strong>fastText embeddings</strong> follow a similar pattern but show a <strong>lower bias</strong>, suggesting that representation of women in corpora has improved over time, particularly from pre-2014 GloVe training data to post-2017 models. However, despite this incremental change, <strong>implicit gender bias remains prevalent</strong> (Figure 6).</p><figure id="1a950465-ff70-80c1-9beb-d1fa772f4812" class="image"><a href="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%2012.png"><img style="width:399px" src="Gender%20Bias%20in%20Word%20Embeddings%20A%20Deep%20Dive%20into%20NL%201a950465ff70802e8119ef1fb5d956d2/image%2012.png"/></a></figure><p id="1a950465-ff70-80d5-87ac-c5a75b8cab2f" class=""><strong>Figure 6: Gender Bias Correlation with Valence, Arousal, and Dominance in GloVe Embeddings </strong>[58].</p><h1 id="1aa50465-ff70-8033-90ac-f6f36a8a0a5a" class="">The Role of Bias in AI Applications</h1><p id="1aa50465-ff70-8055-b419-f356951f1bdd" class="">The propagation of these <strong>gender representations</strong> in word embeddings significantly impacts downstream AI applications, particularly in <strong>visual-linguistic models</strong> such as OpenAI&#x27;s <strong>CLIP</strong>. Systems trained on these biased embeddings may associate <strong>non-sexual female-related terms</strong> with explicit content, reinforcing <strong>harmful biases in image classification, content moderation, and hiring algorithms</strong>.</p><p id="1aa50465-ff70-802d-9bff-e27515043c06" class="">Similarly, an examination of <strong>Big Tech-related words</strong> (Figure 5) reveals that more than <strong>60% of technology-related words in embeddings are associated with men</strong>. This suggests that AI models used in <strong>recruitment, professional networking, and career counseling</strong> may perpetuate existing gender gaps in STEM fields.</p><h1 id="1aa50465-ff70-8049-8ab8-db3cfc57251c" class="">Future Directions</h1><p id="1aa50465-ff70-80f1-a35e-dfc756af2dea" class="">Dealing with gender bias in NLP calls for a multimodal strategy combining:</p><ul id="1aa50465-ff70-80a9-ac6d-cc0833748c60" class="bulleted-list"><li style="list-style-type:disc"><strong>Debiasing embeddings</strong> without sacrificing language integrity, hence mitigating bias.</li></ul><ul id="1aa50465-ff70-80f0-b02e-f92635b08217" class="bulleted-list"><li style="list-style-type:disc"><strong>Diverse and representative</strong> training data with <strong>gender-balanced word distributions</strong>.<br/>Intervention techniques include <br/><strong>ethical artificial intelligence frameworks</strong> and <strong>policy changes</strong> help to stop AI systems from extending gender language prejudices.</li></ul><ul id="1aa50465-ff70-804e-9055-df6aeb475a93" class="bulleted-list"><li style="list-style-type:disc">Resolving these problems at both the <strong>algorithmic</strong> and <strong>data</strong> levels will enable researchers and developers to produce <strong>fairer, more inclusive NLP models</strong> reflecting a <strong>balanced representation of gender in AI-driven communications</strong>.</li></ul><h1 id="1aa50465-ff70-80e5-ac4d-c306bfd75b43" class="">References</h1><p id="1aa50465-ff70-806b-82e9-daed8616f7e9" class="">[1] Mohamed Abdalla and Moustafa Abdalla. 2021. The Grey Hoodie Project: Big<br/>tobacco, big tech, and the threat on academic integrity. In Proceedings of the 2021<br/>AAAI/ACM Conference on AI, Ethics, and Society. 287–297.<br/>[2] Alan Akbik, Duncan Blythe, and Roland Vollgraf. 2018. Contextual String Embeddings<br/>for Sequence Labeling. In COLING 2018, 27th International Conference<br/>on Computational Linguistics. 1638–1649.<br/>[3] Mahzarin R Banaji and Anthony G Greenwald. 1995. Implicit gender stereotyping<br/>in judgments of fame. Journal of personality and social psychology 68, 2 (1995),<br/>181.<br/>[4] Christine Basta, Marta R Costa-Jussà, and Noe Casas. 2019. Evaluating the<br/>underlying gender bias in contextualized word embeddings. arXiv preprint<br/>arXiv:1904.08783 (2019).<br/>[5] Emily M Bender and Batya Friedman. 2018. Data statements for natural language<br/>processing: Toward mitigating system bias and enabling better science.<br/>Transactions of the Association for Computational Linguistics 6 (2018), 587–604.<br/>[6] Abeba Birhane, Vinay Uday Prabhu, and Emmanuel Kahembwe. 2021. Multimodal<br/>datasets: misogyny, pornography, and malignant stereotypes. arXiv preprint<br/>arXiv:2110.01963 (2021).<br/>[7] J Stewart Black and Patrick van Esch. 2020. AI-enabled recruiting: What is it and<br/>how should a manager use it? Business Horizons 63, 2 (2020), 215–226.<br/>[8] Piotr Bojanowski, Edouard Grave, Armand Joulin, and Tomas Mikolov. 2017.<br/>Enriching word vectors with subword information. Transactions of the Association<br/>for Computational Linguistics 5 (2017), 135–146.<br/>[9] Tolga Bolukbasi, Kai-Wei Chang, James Y Zou, Venkatesh Saligrama, and Adam T<br/>Kalai. 2016. Man is to computer programmer as woman is to homemaker?<br/>debiasing word embeddings. Advances in neural information processing systems<br/>29 (2016), 4349–4357.<br/>[10] Marc-Etienne Brunet, Colleen Alkalay-Houlihan, Ashton Anderson, and Richard<br/>Zemel. 2019. Understanding the origins of bias in word embeddings. In International<br/>Conference on Machine Learning. PMLR, 803–811.<br/>[11] Aylin Caliskan. 2021. Detecting and mitigating bias in natural language processing.<br/>Brookings Institution (2021).<br/>[12] Aylin Caliskan, Joanna J Bryson, and Arvind Narayanan. 2017. Semantics derived<br/>automatically from language corpora contain human-like biases. Science 356,<br/>6334 (2017), 183–186.<br/>[13] Aylin Caliskan and Molly Lewis. [n. d.]. Social biases in word embeddings and<br/>their relation to human cognition. PsyArXiv.<br/>[14] Kaytlin Chaloner and Alfredo Maldonado. 2019. Measuring gender bias in word<br/>embeddings across domains and discovering new gender bias word categories. In<br/>Proceedings of the First Workshop on Gender Bias in Natural Language Processing.<br/>25–32.<br/>[15] Tessa Charlesworth, Aylin Caliskan, and Mahzarin R. Banaji. 2022. Historical<br/>Representations of Social Groups Across 200 Years of Word Embeddings from<br/>Google Books. Proceedings of the National Academy of Sciences (2022).<br/>[16] Tessa ES Charlesworth and Mahzarin R Banaji. 2021. Patterns of Implicit and<br/>Explicit Stereotypes III: Long-Term Change in Gender Stereotypes. Social Psychological<br/>and Personality Science (2021), 1948550620988425.<br/>[17] Tessa ES Charlesworth, Victor Yang, Thomas C Mann, Benedek Kurdi, and<br/>Mahzarin R Banaji. 2021. Gender stereotypes in natural language: Word embeddings<br/>show robust consistency across child and adult language corpora of more<br/>than 65 million words. Psychological Science 32, 2 (2021), 218–240.<br/>[18] Sapna Cheryan and Hazel Rose Markus. 2020. Masculine defaults: Identifying<br/>and mitigating hidden cultural biases. Psychological Review 127, 6 (2020), 1022.<br/>[19] Jacob Cohen. 2013. Statistical power analysis for the behavioral sciences. Academic<br/>press.<br/>[20] Ronan Collobert, JasonWeston, Léon Bottou, Michael Karlen, Koray Kavukcuoglu,<br/>and Pavel Kuksa. 2011. Natural language processing (almost) from scratch.<br/>Journal of machine learning research 12, ARTICLE (2011), 2493–2537.<br/>[21] Maria De-Arteaga, Alexey Romanov, Hanna Wallach, Jennifer Chayes, Christian<br/>Borgs, Alexandra Chouldechova, Sahin Geyik, Krishnaram Kenthapadi, and<br/>Adam Tauman Kalai. 2019. Bias in bios: A case study of semantic representation<br/>bias in a high-stakes setting. In proceedings of the Conference on Fairness,<br/>Accountability, and Transparency. 120–128.<br/>[22] Sunipa Dev, Masoud Monajatipoor, Anaelia Ovalle, Arjun Subramonian, Jeff<br/>Phillips, and Kai-Wei Chang. 2021. Harms of Gender Exclusivity and Challenges<br/>in Non-Binary Representation in Language Technologies. In Proceedings of the<br/>2021 Conference on Empirical Methods in Natural Language Processing. 1968–1994.<br/>[23] Alice H Eagly and Antonio Mladinic. 1989. Gender stereotypes and attitudes<br/>toward women and men. Personality and social psychology bulletin 15, 4 (1989),<br/>543–558.<br/>[24] Alice H Eagly and Antonio Mladinic. 1994. Are people prejudiced against women?<br/>Some answers from research on attitudes, gender stereotypes, and judgments of<br/>competence. European review of social psychology 5, 1 (1994), 1–35.<br/>[25] Charles Elkan. 2003. Using the triangle inequality to accelerate k-means. In<br/>Proceedings of the 20th international conference on Machine Learning (ICML-03).<br/>147–153.<br/>[26] Nikhil Garg, Londa Schiebinger, Dan Jurafsky, and James Zou. 2018. Word<br/>embeddings quantify 100 years of gender and ethnic stereotypes. Proceedings of<br/>the National Academy of Sciences 115, 16 (2018), E3635–E3644.<br/>[27] Hila Gonen and Yoav Goldberg. 2019. Lipstick on a pig: Debiasing methods cover<br/>up systematic gender biases in word embeddings but do not remove them. arXiv<br/>preprint arXiv:1903.03862 (2019).<br/>[28] Anthony G Greenwald, Debbie E McGhee, and Jordan LK Schwartz. 1998. Measuring<br/>individual differences in implicit cognition: the implicit association test.<br/>Journal of personality and social psychology 74, 6 (1998), 1464.<br/>[29] Wei Guo and Aylin Caliskan. 2021. Detecting emergent intersectional biases:<br/>Contextualized word embeddings contain a distribution of human-like biases. In<br/>Proceedings of the 2021 AAAI/ACM Conference on AI, Ethics, and Society. 122–133.<br/>[30] N. Hsu, K. L. Badura, D. A. Newman, and M. E. P. Speach. 2021. Gender,<br/>“masculinity,” and “femininity”: A meta-analytic review of gender differences<br/>in agency and communion. Psychological Bulletin (2021), 987–1011. https:<br/><br/><a href="https://doi.org/10.1037/bul0000343">//doi.org/10.1037/bul0000343</a><br/>[31] Larry L Jacoby, Colleen Kelley, Judith Brown, and Jennifer Jasechko. 1989. Becoming<br/>famous overnight: Limits on the ability to avoid unconscious influences<br/>of the past. Journal of personality and social psychology 56, 3 (1989), 326.<br/>[32] Andrew Karpinski and Ross B Steinman. 2006. The single category implicit<br/>association test as a measure of implicit social cognition. Journal of personality<br/>and social psychology 91, 1 (2006), 16.<br/>[33] Hadas Kotek, Rikker Dockum, Sarah Babinski, and Christopher Geissler. 2021.<br/>Gender bias and stereotypes in linguistic example sentences. Language (2021).<br/>[34] Tomas Mikolov, Edouard Grave, Piotr Bojanowski, Christian Puhrsch, and Armand<br/>Joulin. 2018. Advances in Pre-Training Distributed Word Representations.<br/>In Proceedings of the International Conference on Language Resources and Evaluation<br/>(LREC 2018).<br/>[35] Tomáš Mikolov, Wen-tau Yih, and Geoffrey Zweig. 2013. Linguistic regularities<br/>in continuous space word representations. In Proceedings of the 2013 conference of<br/>the north american chapter of the association for computational linguistics: Human<br/>language technologies. 746–751.<br/>[36] Saif M. Mohammad. 2018. Obtaining Reliable Human Ratings of Valence, Arousal,<br/>and Dominance for 20,000 EnglishWords. In Proceedings of The Annual Conference<br/>of the Association for Computational Linguistics (ACL). Melbourne, Australia.<br/>[37] Brian A Nosek, Frederick L Smyth, Natarajan Sriram, Nicole M Lindner, Thierry<br/>Devos, Alfonso Ayala, Yoav Bar-Anan, Robin Bergh, Huajian Cai, Karen Gonsalkorale,<br/>et al. 2009. National differences in gender–science stereotypes predict<br/>national sex differences in science and math achievement. Proceedings of the<br/>National Academy of Sciences 106, 26 (2009), 10593–10597.<br/>[38] Charles E Osgood. 1964. Semantic differential technique in the comparative study<br/>of cultures 1. American Anthropologist 66, 3 (1964), 171–200.<br/>[39] Charles Egerton Osgood, George J Suci, and Percy H Tannenbaum. 1957. The<br/>measurement of meaning. Number 47. University of Illinois press.<br/>[40] Amandalynne Paullada, Inioluwa Deborah Raji, Emily M Bender, Emily Denton,<br/>and Alex Hanna. 2021. Data and its (dis) contents: A survey of dataset<br/>development and use in machine learning research. Patterns 2, 11 (2021), 100336.<br/>[41] Jeffrey Pennington, Richard Socher, and Christopher D. Manning. 2014. GloVe:<br/>Global Vectors for Word Representation. In Empirical Methods in Natural Language<br/>Processing (EMNLP). 1532–1543. <br/><a href="http://www.aclweb.org/anthology/D14-">http://www.aclweb.org/anthology/D14-</a><br/>1162<br/>[42] Alec Radford, Jong Wook Kim, Chris Hallacy, Aditya Ramesh, Gabriel Goh,<br/>Sandhini Agarwal, Girish Sastry, Amanda Askell, Pamela Mishkin, Jack Clark,<br/>et al. 2021. Learning transferable visual models from natural language supervision.<br/>arXiv preprint arXiv:2103.00020 (2021).<br/>[43] Dominik Schlechtweg, Barbara McGillivray, Simon Hengchen, Haim Dubossarsky,<br/>and Nina Tahmasebi. 2020. Semeval-2020 task 1: Unsupervised lexical<br/>semantic change detection. arXiv preprint arXiv:2007.11464 (2020).<br/>[44] Robyn Speer, Joshua Chin, Andrew Lin, Sara Jewett, and Lance Nathan. 2018.<br/>LuminosoInsight/wordfreq: v2.2. <br/><a href="https://doi.org/10.5281/zenodo.1443582">https://doi.org/10.5281/zenodo.1443582</a><br/>[45] Ryan Steed and Aylin Caliskan. 2021. Image representations learned with unsupervised<br/>pre-training contain human-like biases. In Proceedings of the 2021 ACM<br/>Conference on Fairness, Accountability, and Transparency. 701–713.<br/>[46] Autumn Toney-Wails and Aylin Caliskan. 2021. ValNorm Quantifies Semantics<br/>to Reveal Consistent Valence Biases Across Languages and Over Centuries.<br/>Empirical Methods in Natural Language Processing (EMNLP) (2021).<br/>[47] Laurens Van der Maaten and Geoffrey Hinton. 2008. Visualizing data using t-SNE.<br/>Journal of machine learning research 9, 11 (2008).<br/>[48] Tianlu Wang, Xi Victoria Lin, Nazneen Fatema Rajani, Bryan McCann, Vicente<br/>Ordonez, and Caiming Xiong. 2020. Double-Hard Debias: Tailoring Word Embeddings<br/>for Gender Bias Mitigation. In Association for Computational Linguistics<br/>(ACL).<br/>[49] Amy Beth Warriner, Victor Kuperman, and Marc Brysbaert. 2013. Norms of<br/>valence, arousal, and dominance for 13,915 English lemmas. Behavior research<br/>methods 45, 4 (2013), 1191–1207.<br/>[50] Laura Wendlandt, Jonathan K. Kummerfeld, and Rada Mihalcea. 2018. Factors<br/>Influencing the Surprising Instability of Word Embeddings. In Proceedings of<br/>the 2018 Conference of the North American Chapter of the Association for Computational<br/>Linguistics: Human Language Technologies, Volume 1 (Long Papers).<br/>Association for Computational Linguistics, New Orleans, Louisiana, 2092–2102.<br/><br/><a href="https://doi.org/10.18653/v1/N18-1190">https://doi.org/10.18653/v1/N18-1190</a><br/>[51] Robert Wolfe, Mahzarin R. Banaji, and Aylin Caliskan. 2022. Evidence for Hypodescent<br/>in Visual Semantic AI. In Proceedings of the 2022 ACM Conference on<br/>Fairness, Accountability, and Transparency (ACM FAccT).<br/>[52] Robert Wolfe, Mahzarin R Banaji, and Aylin Caliskan. 2022. Evidence for Hypodescent<br/>in Visual Semantic AI. arXiv preprint arXiv:2205.10764 (2022).<br/>[53] Robert Wolfe and Aylin Caliskan. 2021. Low Frequency Names Exhibit Bias<br/>and Overfitting in Contextualizing Language Models. Proceedings of the 2021<br/>conference on empirical methods in natural language processing (EMNLP) (2021).<br/>[54] RobertWolfe and Aylin Caliskan. 2022. Markedness in Visual Semantic AI. In Proceedings<br/>of the 2022 ACM Conference on Fairness, Accountability, and Transparency<br/>(ACM FAccT).<br/>[55] Robert Wolfe and Aylin Caliskan. 2022. VAST: The Valence-Assessing Semantics<br/>Test for Contextualizing Language Models. In Proceedings of the 36th AAAI<br/>Conference on Artificial Intelligence (AAAI).<br/>[56] Robert B Zajonc. 2001. Mere exposure: A gateway to the subliminal. Current<br/>directions in psychological science 10, 6 (2001), 224–228.<br/>[57] Jieyu Zhao, Tianlu Wang, Mark Yatskar, Ryan Cotterell, Vicente Ordonez, and<br/>Kai-Wei Chang. 2019. Gender bias in contextualized word embeddings. arXiv<br/>preprint arXiv:1904.03310 (2019).<br/></p><p id="1aa50465-ff70-800c-a22f-eed824172c23" class="">[58]Aylin Caliskan, Pimparkar Parth Ajay, Tessa Charlesworth, Robert Wolfe, and Mahzarin R. Banaji. 2022. Gender Bias in Word Embeddings: A Comprehensive Analysis of Frequency, Syntax, and Semantics. In Proceedings of the 2022 AAAI/ACM Conference on AI, Ethics, and Society (AIES &#x27;22). Association for Computing Machinery, New York, NY, USA, 156–170. <a href="https://doi.org/10.1145/3514094.3534162">https://doi.org/10.1145/3514094.3534162</a></p><figure id="1aa50465-ff70-80e3-b9c7-f2300c963552"><a href="https://arxiv.org/abs/2206.03390" class="bookmark source"><div class="bookmark-info"><div class="bookmark-text"><div class="bookmark-title">Gender Bias in Word Embeddings: A Comprehensive Analysis of...</div><div class="bookmark-description">The statistical regularities in language corpora encode well-known social biases into word embeddings. Here, we focus on gender to provide a comprehensive analysis of group-based biases in...</div></div><div class="bookmark-href"><img src="https://arxiv.org/static/browse/0.3.4/images/icons/apple-touch-icon.png" class="icon bookmark-icon"/>https://arxiv.org/abs/2206.03390</div></div><img src="https://arxiv.org/static/browse/0.3.4/images/arxiv-logo-fb.png" class="bookmark-image"/></a></figure><h1 id="1aa50465-ff70-80d5-9680-c445cee9aec7" class="">Appendix </h1><p id="1aa50465-ff70-80d6-8b56-c934d6a90c70" class=""><br/>ContentWarning: The authors of the paper have mentioned the following clusters contain the most frequent 1,000 female-associated and male-associated words in the lexicon with effect sizes 𝑑 ≥ 0.50. The results might be triggering [58].<br/>A.1 Female Associated Clusters<br/>Advertising Words: ABOUT, BEST, CLICK, CONTACT, FIRST,<br/>FREE, HERE,HOT, LOVE,MAC, MORE, NEXT,NOTE,NOW, OPEN,<br/>OR, OTHER, PLUS, SAVE, SEE, SPECIAL, STAR, TODAY, TWO,<br/>VERY, WITH, WOW<br/>Beauty and Appearance: accessories, adorable, adore, attractive,<br/>beads, beautiful, beauty, boutique, bracelet, bridal, bride, butterfly,<br/>candles, ceramic, charming, chic, clothes, clothing, coats, cocktail,<br/>colorful, colors, colours, coral, costume, costumes, crafts, crystal,<br/>crystals, cute, dancers, decor, decorating, decorations, delicate, delightful,<br/>designer, designs, doll, dolls, dress, dresses, earrings, elegance,<br/>elegant, ensemble, exotic, exquisite, fabric, fabrics, fabulous,<br/>fairy, fashion, fashionable, feminine, floral, flower, flowers,<br/>footwear, fragrance, gorgeous, gown, hair, handbags, handmade,<br/>heels, invitations, jewellery, jewelry, knit, knitting, lace,<br/>ladies, lip, lovely, makeup, metallic, necklace, nylon, outfit, outfits,<br/>paired, pale, pattern, pearl, pendant, perfume, pillow, pink,<br/>platinum, polish, princess, prom, purple, purse, quilt, ribbon, romantic,<br/>roses, satin, scent, sewing, sheer, silk, skirt, sleek, stitch,<br/>stunning, styling, stylish, sweater, themed, tiny, trendy, vibrant,<br/>Vuitton, waist, wardrobe, wear, wedding, weddings, wonderful,<br/>yarn<br/>Celebrities and Modeling: AMI, authors, availability, bio, blogger,<br/>bloggers, blogs, bookmark, browse, cell, checkout, class, classes,<br/>clicks, cluster, collections, contacting, coordinates, cosmetic, coupon,<br/>curves, date, designers, dot, engagement, giveaway, goodies, inexpensive,<br/>info, invites, layout, libraries, litter, magazine, magazines,<br/>markers, matching, measurements, membrane, model, modeling,<br/>models, ms, newest, null, on-line, patterns, peek, photograph, photos,<br/>photostream, pictures, pumps, registry, reserved, royalty, sample,<br/>samples, scans, separated, shipping, shopping, shops, spanish,<br/>stamps, stores, strips, supermarket, swap, temp, template, templates,<br/>trends, triangle, updated, websites, widget<br/>Cooking and Kitchen: bake, Bake, baked, baking, cake, cakes,<br/>chocolate, Chocolate, cinnamon, coconut, Cookies, Cooking, cream,<br/>creamy, crust, cups, dairy, delicious, Delicious, dessert, dressing,<br/>egg, eggs, foods, Ginger, homemade, honey, Ingredients, lemon,<br/>milk, Milk, nutrition, organic, pumpkin, recipe, Recipe, recipes,<br/>Recipes, Salad, spice, spicy, sugar, sweet, tea, teaspoon, tsp, vanilla,<br/>vegan, vegetables, vegetarian, veggies, yogurt, yummy<br/>Fashion and Lifestyle: Autumn, Bag, Bags, Ballet, Barbie, Basket,<br/>Bathroom, Beads, Beautiful, Beauty, Bed, Bedroom, Bee, Bottom,<br/>Boutique, Bracelet, Bridal, Bride, Butterfly, Cake, Candle, Candy,<br/>Carnival, Carpet, Ceramic, Charm, Cherry, Clearance, Clothes, Colors,<br/>Compact, Contemporary, Cookie, Coral, Costume, Cottage,<br/>Covers, Crafts, Cream, Crystal, Daisy, Dance, Dancing, Decor, Designer,<br/>Designs, Desk, Diamonds, Dining, DIY, Doll, Dolls, Dreams,<br/>Dress, Dresses, Earrings, Egg, Emerald, Evening, Fabric, Fairy, Fancy,<br/>Fashion, Favorites, Fiber, Floor, Floral, Flower, Flowers, Giveaway,<br/>Gorgeous, Hair, Halloween, Heart, Heated, Honey, Inspired, Jeans,<br/>Jewelry, Kiss, Kitty, Lace, Ladies, Laundry, Layer, Lovely, Loving,<br/>Luxury, Makeup, Mesh, Metallic, Mint, Mirror, Mirrors, Nail, Natural,<br/>Necklace, Nylon, Passion, Pattern, Patterns, Pearl, Perfect, Picture,<br/>Pillow, Pink, Platinum, Plus, Powder, Pretty, Princess, Printed,<br/>Pump, Queen, Rack, Ribbon, Romance, Romantic, Rose, Roses, Ruby,<br/>Salon, Satin, Shades, Shape, Shipping, Shoes, Shoulder, Shower,<br/>Silk, Simply, Skin, Sleeping, Smile, Soap, Soft, Spice, Split, Style,<br/>Sugar, Summer, Sunny, Swan, Sweet, Swim, Tea, Tops, Tote, Trend,<br/>Trim, Tropical, Twilight, Unique, Valentine, Vampire, Vanity, Venus,<br/>Victorian, Vintage, Wear, Wedding, Weddings, Witch, Womens,<br/>Wonderful, Wrap, ∼, r<br/>Female Names: Abbey, actress, Actress, Alice, Allison, Amanda,<br/>Amber, Amy, Ana, Andrea, Angela, Angie, Ann, Anna, Anne, Annie,<br/>Ashley, Barbara, Bella, Belle, Beth, Betty, Beverly, Bonnie, Britney,<br/>Brooke, Buffy, Carol, Caroline, Carrie, Catherine, Charlotte, Cheryl,<br/>Christina, Christine, Cindy, Claire, Clara, Clare, Courtney, Dana,<br/>Dawn, Debbie, Deborah, Denise, Diana, Diane, Donna, Dorothy,<br/>Elizabeth, Ellen, Emily, Emma, Erin, Eva, Eve, Gaga, Grace, Heather,<br/>Helen, Hilton, Holly, Ivy, Jackie, Jane, Janet, Jen, Jennifer, Jenny,<br/>Jessica, Jill, Jo, Joan, Joy, Judy, Julia, Julie, Karen, Kate, Katherine,<br/>Kathleen, Kathy, Katie, Katrina, Katy, Kay, Kelly, Kim, Kristen,<br/>Lady, Laura, Lauren, Lily, Linda, Lindsay, Lisa, Liz, Louise, Loved,<br/>Lucy, Lynn, Madison, Madonna, Mae, Maggie, Mai, Mama, Margaret,<br/>Maria, Marie, Marilyn, Marina, Married, Mary, Maya, Megan,<br/>Melissa, Mercedes, Met, Michelle, Miss, Molly, Mommy, Monica,<br/>Ms, Ms., Nancy, Natalie, Nicole, Nikki, Nina, Olivia, Pam, Patricia,<br/>Paula, Penny, Rachel, Rebecca, Rihanna, Rosa, Sally, Samantha, Sandra,<br/>Sara, Sarah, Savannah, Sharon, Shirley, singer, Sister, Sisters,<br/>Sophie, Spears, Stephanie, Sue, Susan, Tara, Tiffany, Tina, Vanessa,<br/>Victoria, Wendy, Whitney, Willow, xx, Yay<br/>Health and Relationships: abortion, acne, addicted, addiction,<br/>allergic, allergy, arthritis, aunt, babies, belly, breast, cancer, caring,<br/>celebrities, celebrity, chatting, cheating, clinic, complications, counseling,<br/>couple, couples, dancer, DD, depressed, depression, diabetes,<br/>disabilities, disorder, distress, donor, emotionally, experiencing, girlfriend,<br/>grandmother, healthier, her, hers, herself, hips, hormones,<br/>inspirational, lady, literacy, lover, loving, marriage, messy, mom,<br/>moms, mother, mothers, mum, nurse, nurses, nursing, obsessed, obsession,<br/>oral, parent, parenting, passionate, poems, pose, poses, pregnancy,<br/>pregnant, protective, relationship, relationships, romance,<br/>seniors, sensitive, sexuality, she, She, sister, sisters, skin, stories,<br/>stressful, supportive, survivors, syndrome, therapist, therapy, toes,<br/>toxic, tumor, vampire, witch, wives, woman, women<br/>Luxury and Lifestyle: accommodations, Apartment, balcony, bath,<br/>bathroom, bathrooms, beaches, bedroom, carpet, catering, closet,<br/>cottage, cozy, cruise, Enjoy, enjoys, flats, gardening, holidays, intimate,<br/>kitchen, laundry, luxurious, luxury, massage, mattress, outdoors,<br/>pets, queen, relaxing, rooms, Rooms, salon, sandy, shower,<br/>showers, soap, Spa, spa, sunny, swim, swimming, tile, tub, vacations,<br/>wellness, yoga<br/>Obscene Adult Material: anal, babe, babes, bikini, bitch, blonde,<br/>blowjob, boob, boobs, bra, breasts, brunette, busty, chick, chicks,<br/>cum, cunt, dildo, ebony, erotic, escort, facial, flashing, fucked, gal,<br/>galleries, gallery, girl, girls, hentai, horny, hot, hottest, juicy, kissing,<br/>latex, lesbian, lesbians, lick, licking, lingerie, mature, milf, movies,<br/>naked, naughty, nipples, nude, orgasm, panties, penetration, pics,<br/>posing, pussy, sexy, shemale, slut, stockings, sucking, teen, teens,<br/>tit, tits, webcam, wet, whore, xxx<br/>Sexual Profanities: 00, Amateur, Anal, Asian, Ass, Babe, Blonde,<br/>Busty, Cum, Cute, Ebony, Facial, Fucked, Galleries, Girl, Girls, Her,<br/>Horny, Hot, Huge, Lesbian, Mature, Mom, Moms, Movies, Naked,<br/>Nude, Pics, Pictures, Porn, Pussy, Sex, Sexy, Teen, Teens, Tight, Tits,<br/>Wet, Wife, XXX<br/>Web Article Titles: Absolutely, Acne, Across, Addiction, Adelaide,<br/>Advertise, Affordable, Alberta, Apply, Aurora, Awareness, Bachelor,<br/>Benefit, Biggest, Blogger, Bollywood, Breast, Calendar, Cancel,<br/>Cancer, Caribbean, Celebrity, Changing, Choice, Choosing, Classes,<br/>Closed, Collections, Compliance, Consumer, Consumers, Contest,<br/>Coordinator, Counseling, Created, Cruise, Cure, Czech, Dakota,<br/>Dates, Denmark, Designers, Destination, Diabetes, Diet, Disclaimer,<br/>Eating, eBook, Editorial, Engagement, ER, Everyday, Exclusive, Explore,<br/>Factor, Fiction, Finding, Fitness, Food, Foods, Gallery, Getting,<br/>Health, Healthy, Holidays, Inspiration, Languages, Libraries,<br/>Lifestyle, Lots, Magazine, Massage, Model, Models, Month, MS,<br/>MSN, Multiple, Naturally, Newsletter, non-profit, nonprofit, Novel,<br/>Nurse, Nursing, Nutrition, Oral, Parties, Patent, Patient, Platform,<br/>Pregnancy, Privacy, Purchase, Readers, Reality, Recently, Reception,<br/>Registry, Relationship, Relationships, Reserved, Rica, Runtime, Sample,<br/>Scenes, Secret, Secrets, Seller, Shared, Shares, Sharing, Shows,<br/>Sierra, Sites, Spotlight, Statement, Student, Target, Teacher, Teachers,<br/>Templates, Therapy, Totally, Treat, Trends, Updates, VIP, Virgin,<br/>Virtual, Vitamin, Voices, Wellness, Whole, Winners, Women, Write,<br/>Yoga<br/>A.2 Male Associated Clusters<br/>Adventure and Music: &quot;, ’, 1972, Against, Answer, Arms, Articles,<br/>Back, Band, Bass, Batman, Battle, Bear, Beat, Beer, Blues, Brain,<br/>Brother, Brothers, Bull, Camp, Champion, Cold, Comedy, Cool,<br/>Count, Crew, Da, Dead, Death, Devil, Die, DJ, Dog, Dragon, Eagle,<br/>Empire, End, EP, Essential, Evil, Evolution, Fans, feat, Fight, Fish,<br/>Flying, Force, Four, Future, Game, Ghost, Giant, Great, Green, Guitar,<br/>Gun, Guys, Hat, Head, Hero, Hood, II, III, Iron, IV, Jazz, Jump, King,<br/>Kingdom, Kings, Knight, Late, Leader, Legend, Lincoln, Lion, LP,<br/>Major, Man, Mario, Marvel, Master, Max, Military, Motion, Nation,<br/>Navy, Numbers, Of, Official, Orchestra, Original, Oxford, Pack, Part,<br/>Pass, Points, Prime, Prince, Quote, Rank, Raw, Records, Remix,<br/>remix, Reserve, Retrieved, Return, Revolution, Rise, Rock, Rocky,<br/>Roll, Rule, Running, Rush, Score, Scottish, Shirt, Shot, Six, Sound,<br/>Stand, Strong, Super, Ten, Tiger, Trail, Trial, Ultimate, views, Vol,<br/>Volume, Wall, War, Wars, Way, Will, Wolf<br/>Big Tech: .0, 1.1, 2.0, 3.0, Android, Answers, API, App, Applications,<br/>Audio, Build, Canon, Cisco, Cloud, Command, Computer, contribs,<br/>CPU, demo, developer, Developer, developers, Documents, Error,<br/>Firefox, Flash, Forums, Galaxy, Gaming, GMT, Google, GPS, HP,<br/>IBM, Install, Intel, Intelligence, Internet, Introduction, iOS, iPhone,<br/>Java, JavaScript, Linux, Message, Microsoft, MP3, NET, Nintendo,<br/>Notes, OS, PC, Player, plugin, Problem, Programming, PS3, Questions,<br/>Re, RE, Remote, replies, RSS, Samsung, Security, SEO, Server,<br/>SMS, Software, SQL, Statistics, Test, User, Users, Wii, Windows,<br/>Wireless, Xbox, XML, XP, YouTube<br/>Engineering and Automotive: AC, Advance, Audi, Auto, Automotive,<br/>Bar, Battery, BMW, Built, Button, Cap, Charger, Chevrolet,<br/>Chrome, Circuit, Construction, Contractors, Custom, Dodge,<br/>Doors, Driver, Driving, Duty, Economy, Electric, Engine, Engineer,<br/>Engineering, Equipment, Extra, Fishing, Fuel, Garage, Gas, Gear,<br/>General, GM, Golf, Guard, Hardware, Heating, Heavy, Honda, Industrial,<br/>Laser, Logo, Machine, Maintenance, Manual, Manufacturing,<br/>Metal, Motor, Nissan, Oil, Pocket, Portable, Power, Premium, Pressure,<br/>Printing, Pro, Quick, Racing, RC, Repair, Rod, Signs, Solar,<br/>Solid, Speed, Sport, Standard, Steel, System, Tech, Technical, Tool,<br/>Tools, Toyota, Trade, Trading, Training, Transfer, Transport, Truck,<br/>Universal, Upper, Wood, Yamaha<br/>Engineering and Electronics: assembly, audio, auto, automotive,<br/>backup, batteries, blade, brass, build, built, capable, charge, charging,<br/>chip, circuit, command, commands, computing, conditioning,<br/>console, construction, contractor, contractors, controller, conversion,<br/>convert, converted, custom, dealer, dealers, driver, durable,<br/>duty, electronics, enabled, engine, engineer, engineering, engineers,<br/>engines, enterprise, execution, formation, gate, gear, general, generation,<br/>header, install, legacy, lightweight, logic, manual, master,<br/>motor, operation, physics, pipe, power, printer, printing, proven,<br/>receiver, reference, remote, repair, replace, replacement, restoration,<br/>rod, root, scheme, seal, security, setup, software, solution, superior,<br/>suspension, tire, transfer, trucks, upgrade<br/>God and Religion: Abraham, according, According, Allah, appointed,<br/>authority, bear, bears, believed, Bible, blind, brothers, century,<br/>Christ, Christianity, Christians, commentary, composed, creator,<br/>evil, evolution, Father, favor, followers, fool, genius, glory, God,<br/>god, Gospel, he, He, himself, His, Holy, holy, hundred, Islam, Israel,<br/>Jerusalem, Jesus, Jews, king, kingdom, land, Lord, man, mere, Muslims,<br/>nations, passage, philosophy, poor, Pope, possession, praise,<br/>principle, quote, referred, refers, regard, regarded, respect, reward,<br/>Roman, Rome, rule, sacrifice, sheep, sin, sir, Son, sword, temple,<br/>theory, tho, thou, Thus, tradition, translation, united, unto, verse,<br/>wise, worthy, ye<br/>Male Names: Aaron, actor, Adam, Al, Alan, Albert, Alex, Allen,<br/>Andrew, Andy, Anthony, Arthur, Barry, Ben, Bill, Billy, Bishop, Bob,<br/>Bobby, Brad, Brandon, Brian, Brown, Bruce, Bryan, Captain, Carl,<br/>Carlos, CEO, Chairman, chairman, Charles, Chief, Chris, Christopher,<br/>Chuck, Clay, Craig, Dan, Daniel, Danny, Dave, David, Dennis,<br/></p><p id="1aa50465-ff70-805f-8bf1-dda58e87adcb" class="">Dick, Don, Donald, Doug, Duke, Ed, Eddie, Eric, Francis, Frank,<br/>Franklin, Fred, Gary, Gates, George, Glenn, Gordon, Governor, Greg,<br/>Guy, Harrison, Harry, Henry, Howard, Ian, Jack, Jackson, Jacob, Jake,<br/>James, Jason, Jay, Jeff, Jefferson, Jeremy, Jerry, Jim, Jimmy, Joe, Joel,<br/>John, Johnny, Johnson, Jon, Jonathan, Joseph, Josh, Jr., Juan, Justin,<br/>Keith, Ken, Kevin, Kyle, Larry, Luke, Marc, Mark, Marshall, Martin,<br/>Matt, Matthew, Mayor, Michael, Mike, Miles, Morris, Mr, Mr., Murray,<br/>Nathan, Neil, Nelson, Nick, Norman, Oliver, Patrick, Paul, Pete,<br/>Peter, Phil, Philip, Ralph, Randy, Rich, Richard, Rick, Rob, Robert,<br/>Robinson, Roger, Ron, Roy, Russell, Ryan, Sam, Samuel, Scott, Sean,<br/>Simon, Sir, Stanley, Stephen, Steve, Steven, Ted, Terry, Thomas,<br/>Tim, Tom, Tommy, Tony, Troy, Victor, Vincent, W., Walter, Wayne,<br/>William<br/>Non-English Tokens: al, Barcelona, con, da, DE, del, der, des, di,<br/>du, e, ed, El, el, et, le, Madrid, o, par, que, se, un, van<br/>Numbers, Dates, and Metrics: -1, 103, 111, 113, 1500, 160, 2.4, 200,<br/>220, 240, 250, 2d, 300, 3000, 320, 360, 400, 450, 500, 51, 600, 700, 73,<br/>77, 900, [, acres, BC, C, c., D, d, ft, ft., G, Given, k, MP, No., O, OF, P,<br/>p, p., Per, pp., R, SS, St, U., v, v., W, £<br/>Sports: backs, ball, band, baseball, basketball, bass, bat, beat, beaten,<br/>beating, beer, bench, betting, blues, boss, buddy, camp, captain,<br/>champion, championship, cheat, coach, coaches, coin, crew, decent,<br/>defensive, don, draft, drum, drums, dude, elite, epic, era, fans,<br/>fellow, finest, fishing, football, franchise, gambling, game, games,<br/>gaming, golf, grand, great, greatest, guard, guitar, guy, guys, heads,<br/>hero, hockey, hunting, idiot, injuries, injury, jazz, jersey, jokes,<br/>kick, league, legend, legendary, lineup, manager, mark, mate, minor,<br/>musicians, offense, offensive, pass, passes, passing, penalty, pit,<br/>pitch, player, players, points, pound, premier, prime, pro, prospect,<br/>prospects, racing, rally, rank, recruiting, retired, rotation, rush,<br/>saves, score, scored, scoring, serving, solid, sport, sports, squad,<br/>stadium, starter, stats, suspended, tackle, team, teams, thread, ton,<br/>tournament, trade, trading, tribute, tricks, ultimate, versus, veteran,<br/>victory, wing, yard, yards, zone<br/>Sports and Cities: 2014, AL, Antonio, Arena, Athletic, Baltimore,<br/>Baseball, Basketball, Bay, Bears, Boston, Bowl, Buffalo, Champions,<br/>Championship, Chicago, Cincinnati, Cleveland, Columbus, Dallas,<br/>Detroit, Diego, Draft, Eagles, England, ESPN, FC, Football, Giants,<br/>Highlights, Hockey, Indians, Jersey, Jose, Junior, League, Lions, Liverpool,<br/>Louis, Louisville, Manchester, Milwaukee, Minnesota, MLB,<br/>MLS, Montreal, NBA, NCAA, NFL, NHL, Nike, Oakland, Orlando,<br/>Penn, Philadelphia, Pittsburgh, Players, Premier, Rangers, Saints,<br/>San, SEC, Soccer, Sox, Sports, St., Stadium, Tampa, Team, Ticket,<br/>Tickets, Tigers, Tournament, United, vs, vs., Yankees<br/>War and Violence: against, Army, army, arrest, arrested, attack,<br/>ban, battle, bin, Bush, charges, chief, cited, combat, commit, committed,<br/>corruption, crimes, criminal, dead, defeat, defeated, defense,<br/>Defense, destruction, enemies, enemy, executed, fight, fighter, fighting,<br/>fights, fought, fraud, governor, gun, guns, heroes, illegal, injured,<br/>intelligence, Iraq, Iraqi, kill, killed, killing, leader, leaders,<br/>leadership, led, march, military, minister, officers, opponents, opposition,<br/>personnel, prison, province, racist, regime, revolution, ruled,<br/>soldier, soldiers, spokesman, supporters, tactics, terror, terrorist,<br/>troops, veterans, violent, war, wars, weapons<br/>A.3 Big TechWords<br/>965 Big Tech Words: 23andMe, 3Com, 3COM, 3Par, 3PAR, 7digital,<br/>9to5Google, 9to5mac, 9to5Mac, AAPL, ABBYY, Accenture,<br/>Acer, Acronis, Activision, Acxiom, AdAge, Adaptec, Adidas, Ad-<br/>Mob, Admob, Adobe, AdSense, Adsense, AdWords, Adwords, Agilent,<br/>Airbnb, Airbus, Airtel, Akamai, Albanesius, Alcatel, Alcatel-<br/>Lucent, Alibaba, <br/><a href="http://alibaba.com/">Alibaba.com</a>, Alienware, AllFacebook, AllThingsD,<br/>AltaVista, Altera, Amazon, <br/><a href="http://amazon.com/">Amazon.com</a>, AMD, Amdocs, AmEx,<br/>AMZN, Anandtech, AnandTech, Andoid, Andreessen, Andriod, Android,<br/>ANDROID, android, Android-based, Android-powered, AndroidPIT,<br/>anti-competitive, anti-trust, anticompetitive, Antitrust,<br/>antitrust, AOL, AOpen, API, APIs, Appcelerator, AppEngine, Apple,<br/>APPLE, <br/><a href="http://apple.com/">Apple.com</a>, AppleInsider, AppleTV, Appstore, appstore,<br/>AppStore, AppUp, Archos, Ariba, ARM-based, <br/><a href="http://ask.com/">Ask.com</a>, ASRock,<br/>AstraZeneca, Asus, ASUS, asus, ASUSTeK, Asustek, ATandT,<br/>Atari, Atheros, ATi, ATI, Atlassian, Atmel, Atom-based, Atos, Atrix,<br/>AuthenTec, Autodesk, automaker, Automattic, Avanade, Avaya,<br/>Avira, Avnet, AWS, Baidu, baidu, <br/><a href="http://baidu.com/">Baidu.com</a>, Ballmer, Barclays,<br/>Bazaarvoice, BBRY, BenQ, BestBuy, Bestbuy, BetaNews, Betriebssystem,<br/>Bezos, BIDU, Bing, Biogen, Bitcoin, Bitdefender, BitTorrent,<br/>BlackBerry, Blekko, Blinkx, bloatware, BloggingStocks, Bloomberg,<br/>BlueStacks, Boeing, BofA, <br/><a href="http://box.net/">Box.net</a>, Boxee, Brightcove, Broadcom,<br/>Brocade, BSkyB, Bungie, BusinessWeek, <br/><a href="http://buy.com/">Buy.com</a>, BuzzFeed, BYD,<br/>Canalys, Canonical, Capgemini, carmaker, Carphone, CCleaner,<br/>CentOS, ChannelWeb, Chegg, China, China-based, Chinavasion,<br/>chip-maker, Chipmaker, chipmaker, chipmakers, chipset, chipsets,<br/>Chipzilla, Chitika, Chromebook, ChromeBook, Chromebooks,<br/>ChromeOS, CinemaNow, <br/><a href="http://cio.com/">CIO.com</a>, Cisco, CISCO, CISPA, Citi,<br/>Citibank, Citigroup, Citrix, Cleantech, Clearwire, closed-source,<br/>cloud-computing, Cloudera, CNET, CNet, Cnet, cnet, Coca-Cola,<br/>Cognizant, Comcast, Compal, companies, company, Compaq, Comp-<br/>TIA, ComputerWorld, Computerworld, Computex, ComScore, Comscore,<br/>comScore, Conexant, Cooliris, Corp, Costolo, Coursera, Cr-48,<br/>crapware, Cringely, CrunchBase, CSCO, CUDA, Cupertino, Cupertinobased,<br/>CyanogenMod, Cyanogenmod, CyberLink, Cyberlink, Cybersecurity,<br/>cybersecurity, D-Link, DailyTech, Daimler, Danone,<br/>DARPA, Datacenter, Deezer, Dell, DELL, Deloitte, DeNA, Dhingana,<br/>DigiTimes, Digitimes, DisplayLink, DisplayPort, DivX, Do-<br/>CoMo, Docomo, DOCOMO, DoJ, DOJ, DoubleClick, Doubleclick,<br/>DreamHost, Dropbox, DropBox, E-Commerce, E-Readers, EBay,<br/>eBay, Ebay, Ebuyer, eCommerce, Ecosystem, ecosystem,<br/><br/><a href="http://electricpig.co.uk/">Electricpig.co.uk</a>, Electronista, Elop, Eloqua, eMachines, Emachines,<br/>eMarketer, EMC, Emulex, Endeca, Engadget, engadget, Epson, Ericsson,<br/>Erictric, ESET, Esri, Etisalat, Everex, Evernote, EVGA, eWeek,<br/>Experian, ExtremeTech, Exxon, ExxonMobil, Exynos, F-Secure, Facebook,<br/>FaceBook, Facebooks, FedEx, Feedly, Firefox, Flextronics, Flipboard,<br/>Flipkart, Fortinet, FOSS, Foxconn, foxconn, Foxit, FreeBSD,<br/>Freescale, Frito-Lay, FTC, Fudzilla, Fujifilm, Fujitsu, Fusion-io, GadgeTell,<br/>Gaikai, Gameloft, GameStop, Gartner, Gawker, GE, <br/><a href="http://geek.com/">Geek.com</a>,<br/>GeekWire, GeForce, Geforce, Gemalto, Genentech, Geohot, Get-<br/>Jar, Gigabyte, GIGABYTE, GigaOm, GigaOM, GitHub, Github, Gizmodo,<br/>Glassdoor, GlaxoSmithKline, Gmail, GMail, GMAIL, go-tomarket,<br/>GoDaddy, Godaddy, GoGrid, GOOG, Google, GOOGLE,<br/>Google-owned, <br/><a href="http://google.com/">Google.com</a>, Googler, Googlers, Googles, GoogleTV,<br/>Googleâ, Goolge, GoPro, gOS, <br/><a href="http://gottabemobile.com/">GottaBeMobile.com</a>, Gowalla, Gphone,<br/>GPU, GPUs, Groupon, GSK, GSMA, GSMArena, H-P, Hackathon,<br/>Hackintosh, hackintosh, Hadoop, Haier, Hanvon, HD-DVD, Heroku,<br/>Hewlett-Packard, Hisense, Hitachi, Honeywell, Hootsuite, Hortonworks,<br/><br/><a href="http://hothardware.com/">HotHardware.com</a>, Hotmail, HP, HPQ, HSBC, HTC, htc,<br/>HTML5, Huawei, huawei, HUAWEI, HubSpot, Hulu, Hynix, I.B.M.,<br/>i7500, IaaS, iAd, iAds, IBM, ibm, IBMs, Icahn, iClarified, iCloud,<br/>Ideapad, IDEOS, IDG, IE10, IE8, IE9, iFixit, iMessage, Informatica,<br/>InformationWeek, Infosys, InfoWorld, Inktomi, INTC, Intel,<br/>INTEL, Intel-based, Intels, InterDigital, <br/><a href="http://internetnews.com/">internetnews.com</a>, Internet-<br/><br/><a href="http://news.com/">News.com</a>, InterVideo, Intuit, Inventec, Iomega, iOS, iPad3, iPhone,<br/>iPhone5, iPhones, IPO, iRobot, iTablet, ITProPortal, iTWire, ITworld.<br/>com, iWatch, iWork, JBoss, JetBlue, Jolicloud, Joyent, JPMorgan,<br/><br/><a href="http://jr.com/">JR.com</a>, Kaltura, Kaspersky, KDDI, Kinect, Klout, Kobo,<br/>KPMG, LastPass, Lenovo, lenovo, LENOVO, LePhone, Lexmark,<br/>LG, Liliputing, LiMo, Lindows, LinkedIn, Linkedin, Linksys, Linspire,<br/>Linux, Lite-On, Livescribe, <br/><a href="http://liveside.net/">LiveSide.net</a>, Lodsys, Logitech,<br/>LogMeIn, Lucasfilm, Lucent, Lufthansa, Lumia, Lytro, MacDailyNews,<br/>MacMall, MacOS, MacRumors, Magento, MakerBot, Malware,<br/>Malwarebytes, Marketshare, marketshare, Marvell, Mashable,<br/>MasterCard, Mastercard, Mattel, McAfee, McKesson, McKinsey,<br/>McNealy, MediaTek, Mediatek, Medion, Meebo, MeeGo, Meego,<br/>Meizu, Mellanox, Mendeley, Merck, MetroPCS, Microchip, Microelectronics,<br/>Micron, Microsft, Microsoft, MicroSoft, MIcrosoft, microsoft,<br/>MICROSOFT, Microsofts, MicroStrategy, Micrsoft, Mircosoft,<br/>MIT, Mitel, mobile-device, MobileCrunch, MobiTV, mocoNews,<br/>Monoprice, Monsanto, Motherboard, Moto, Motorola, motorola,<br/>Motorolla, Mozilla, Mozy, MSFT, multinationals, Multitouch,<br/>multitouch, MVNO, MySQL, Napster, NASA, Nasdaq, NASDAQ,<br/>Navteq, Neowin, <br/><a href="http://neowin.net/">Neowin.net</a>, Nestle, Nestlé, NetApp, Netbook,<br/>Netezza, Netflix, NetFlix, Netgear, NetGear, NETGEAR, Netscape,<br/>NetSuite, Newegg, NewEgg, newegg, <br/><a href="http://newegg.com/">Newegg.com</a>, <a href="http://newegg.com/">NewEgg.com</a>,<br/><br/><a href="http://news.cnet.com/">news.cnet.com</a>, NewsFactor, Nextag, Nexus, Nike, Nimbuzz, Nintendo,<br/>Nokia, nokia, NOKIA, non-Apple, Nortel, Novartis, Novell,<br/>NSA, NSDQ, Nuance, NVDA, Nvidia, NVIDIA, NVidia, nVidia,<br/>nVIDIA, nvidia, NXP, OCZ, OEM, OEMs, OLED, OLPC, Omniture,<br/>OmniVision, Onkyo, OnLive, Onlive, Open-Source, open-source,<br/>open-sourced, OpenCL, OpenDNS, OpenFeint, OpenSocial, Open-<br/>Solaris, opensource, OpenStack, Optus, Oracle, ORCL, Orkut, OSes,<br/>OSX, Otellini, <br/><a href="http://outlook.com/">Outlook.com</a>, Ouya, OUYA, <a href="http://overstock.com/">Overstock.com</a>, PaaS,<br/>paidContent, PalmOne, Panasonic, PandoDaily, Pantech, Papermaster,<br/>patent-infringement, PayPal, Paypal, PCMag, <br/><a href="http://pcmag.com/">PCMag.com</a>,<br/>PCWorld, Pegatron, Pepsi, PepsiCo, Pepsico, Pfizer, Phablet, phablet,<br/>PhoneArena, Phoronix, Pichai, Pixar, Pixel, Plantronics, Plaxo,<br/><br/><a href="http://play.com/">Play.com</a>, Playdom, Pogoplug, Polycom, PopCap, post-PC, Postini,<br/>PowerDVD, Powerset, PowerVR, pre-IPO, PS4, Psystar, Publicis,<br/>PwC, QCOM, Qihoo, QLogic, QNAP, Quad-Core, Qualcomm, qualcomm,<br/>QUALCOMM, Quantcast, Quickoffice, QuickOffice, Quora,<br/>Rackspace, RackSpace, Radeon, Rakuten, Ralink, Rambus, Raytheon,<br/>Razer, Rdio, ReadWriteWeb, RealNetworks, Realtek, Redbox, Reddit,<br/>RedHat, Redhat, Redmond-based, Renesas, Renren, RHEL, RightScale,<br/>RIM, RIMM, Roku, Rovio, SaaS, Safaricom, Salesforce, SalesForce,<br/>salesforce, <br/><a href="http://salesforce.com/">Salesforce.com</a>, <a href="http://salesforce.com/">SalesForce.com</a>, <a href="http://salesforce.com/">salesforce.com</a>, Samsung,<br/>samsung, SAMSUNG, Samsungs, SanDisk, Sandisk, Sanofi,<br/>SAP, Scoble, Scobleizer, SDK, SDKs, Seagate, search-engine, Seesmic,<br/>Semiconductor, Set-Top, SGX, Shopify, Silicon, SiliconANGLE, SiliconBeat,<br/>Singtel, SingTel, Sinofsky, SkyDrive, Skype, Slashdot,<br/>Smartphone, smartphone, smartphones, Smartphones, smartwatch,<br/>SoftBank, Softbank, Softpedia, software, SolarCity, SonicWall, Sonos,<br/>Sony, sony, SONY, Sophos, SoundCloud, SourceForge, SpaceX, Spansion,<br/>Splashtop, Splunk, Spotify, Spreadtrum, Sprint-Nextel, Starbucks,<br/>Stardock, startups, Startups, STMicroelectronics, Success-<br/>Factors, SugarCRM, SugarSync, Sumsung, Sunnyvale, SunPower,<br/>Supermicro, superphone, SUSE, SuSE, SwiftKey, Swisscom, Swype,<br/>Sybase, Symantec, Synaptics, Synnex, Synopsys, T-Mobile, T-mobile,<br/>TalkTalk, Taobao, tech, TechCrunch, Techcrunch, techcrunch,<br/><br/><a href="http://techcrunch.com/">techcrunch.com</a>, Techdirt, TechEye, TechFlash, TechHive, Techmeme,<br/>TechNewsWorld, TechnoBuffalo, TechRadar, TechSpot, Tech-<br/>Web, Tegra, telco, Telco, telcos, Telcos, Telefonica, Telefónica, Telenor,<br/>TeliaSonera, Telstra, Tencent, Teradata, Tesco, Tesla,<br/>ThinkGeek, Thinkpad, ThinkPad, TIBCO, Tibco, Ticketmaster,<br/>TigerDirect, TiVo, Tizen, TMobile, TomTom, Torvalds, Toshiba,<br/>toshiba, TouchPad, Touchpad, Toyota, Transmeta, TRENDnet, TSMC,<br/>Tudou, Turkcell, Twilio, Twitter, Uber, Ubergizmo, Ubisoft, Ubuntu,<br/>Udacity, UEFI, Ultrabook, ultrabook, Ultrabooks, ultrabooks, Unilever,<br/>Unisys, uTorrent, UX, <br/><a href="http://v3.co.uk/">V3.co.uk</a>, Valleywag, VatorNews, Venture-<br/>Beat, VeriFone, Verisign, VeriSign, Verizon, Vertica, Vevo, Viacom,<br/>Viadeo, Viber, Vidyo, ViewSonic, Viewsonic, VirnetX, VirtualBox,<br/>Visa, Vizio, VIZIO, Vlingo, VMware, VMWare, Vmware, Vodafone,<br/>Vodaphone, Volusion, VP8, VPN, vPro, VR-Zone, Vringo, Vuze, Vyatta,<br/>VZW, W3C, Wacom, Wal-Mart, Walmart, <br/><a href="http://walmart.com/">Walmart.com</a>, Waze,<br/>WebEx, Webkit, WebKit, WebM, WebOS, webOS, Webroot, Websense,<br/>Weibo, WhatsApp, Whatsapp, WiDi, WikiLeaks, Wikileaks,<br/>WildTangent, WiMax, WiMAX, Win7, Win8, WinBeta, Windows,<br/>WIndows, Windows7, Windows8, WinRumors, Wintel, Wipro,<br/>Wistron, WMPoweruser, Woz, WP7, WP8, WSJ, WWDC, x86, X86,<br/>Xbox, XBox, XCode, XDA, Xerox, Xiaomi, Xilinx, Xobni, Xoom,<br/>XOOM, Xperia, Yahoo, Yammer, Yandex, Yarow, Yelp, YHOO, Youku,<br/>YouTube, Zappos, ZDNet, ZDnet, Zenbook, Zendesk, Zillow, Zimbra,<br/>Zoho, Zotac, ZTE, Zuckerberg, Zynga<br/></p></div></article><span class="sans" style="font-size:14px;padding-top:2em"></span></body></html>
