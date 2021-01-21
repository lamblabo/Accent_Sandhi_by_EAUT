#【これは何】<br>
このスクリプト群は日本語の複合名詞のアクセントを
アクセント単位形からアクセントを予測するものです。
<br>
例:
$ python do.py
複合名詞を入力してください。
長野新幹線車両センター
条件を選んでください。kisoku,sur,pho
pho
['長野', '新', '幹線', '車両', 'センター']
input 0(non_strong) or 1(strong) example:0,1,1
<br>
1,0,0,0,0
[[1, 10], ['ナガノ', 'シンカンセンシャリョーセンター'], ['長野', '新幹線車両センター']]
<br>
のように0,1で話者の強調(としているパラメータ)とCRFで予測しているアクセント単位形から、
アクセントの切れ目を予測し、複合名詞全体のアクセントを表示します。
(条件にkisokuを選ぶと、OPENJTALK、TASETを元にした規則ベースのアクセント合成を行います。)
<br>
#【簡単な動作原理】<br>
『ＮＨＫ日本語発音アクセント新辞典』の付録に記載の
「アクセント単位形」という考え方をコンピュータで使えないかと作成したものです。

以下の説明は、本ソースコード群を作成した際に作成したものです。

語句のにはある単位でアクセントが乖離しないもの、するものが存在する。
その違いをアクセント単位形で示し、単位形が0なら次の単位と結合、
1なら乖離する。
アクセント単位形の予測は、語句の単位(unidicの短単位を想定)レベルのアクセント句による。
アクセント句が0(平板型)なら、アクセント単位形は0
それ以外なら1

例:長野新幹線車両センター
CRFによるアクセント単位形予測が
1,1,1,0,0
と予測され、
ユーザーから強調入力が
1,0,0,0,0
だった場合。

アクセント結合可否
'長野':乖離
'新':結合
'幹線':結合
'車両':結合
'センター':結合

結果:[[1, 10], ['ナガノ', 'シンカンセンシャリョーセンター'], ['長野', '新幹線車両センター']]

※アクセント単位形の予測は
『日本語話し言葉コーパス( Corpus of Spontaneous Japanese : CSJ ) 』で学習しています。

#【動作条件】
Mecab(-Overboseできるもの)(https://taku910.github.io/mecab/)、
CRF++(https://taku910.github.io/crfpp/)のpathが通っていることが動作条件です。

また、Mecab辞書としてunidic-cwj-2.3-2.0(https://unidic.ninjal.ac.jp/download#unidic_bccwj)を
使用します。ダウンロードしたディレクトリをこのreadmeと同じディレクトリに(unidic-cwj-2.3-2.0)という名前で置いて下さい。
(システム辞書のデフォルトに設定する必要はありません。)

Mecabespresso/Mecabespresso.py でMecabのコマンドを、
CRFsyori/CRFsyori.py および CRFsyori2/CRFsyori2.py でCRF++のコマンドを呼び出しています。
コマンドラインの返却値を利用するので、pythonでのコマンドライン結果を取得できるpython環境でご利用ください。
(pyenv等で指定されている場合は該当ディレクトリで設定されているpythonのパスと同じものを使用してください。)

#【使用方法】
ターミナルで
do.pyでCUI版を
GUI.pyでGUI版を実行できます。

#【発表予定】
本研究は、
第83回情報処理学会全国大会(https://www.gakkai-web.net/gakkai/ipsj/83/program83.html#t4)
学生セッション［7N会場］（3月20日（土）　13:10〜15:10）
音声言語情報処理（2）
7N-02
アクセント単位形の推測を用いた日本語複合名詞のアクセント句の合成
○青柳詠美，小島正樹（東京薬科大）
で発表いたします。

#【連絡先】
東京薬科大学　生命科学研究科　生物情報科学研究室<br>
青柳　詠美
s168002@icloud.com
utaharunomar17@gmail.com
