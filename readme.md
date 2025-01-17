<h1>Accent_Sandhi_by_EAUT</h1>
情報処理学会の発表で用いた<br>
Accent Sandhi of Compound Nouns of Japanese by Estimating Accent Unit Types <br>
をそこそこに省略したものです。
<h1>【これは何】</h1>
このスクリプト群は日本語の複合名詞のアクセントを<br>
アクセント単位形からアクセントを予測するものです。<br>
<br>
例:<br>

$ python do.py<br>
複合名詞を入力してください。<br>
長野新幹線車両センター<br>
条件を選んでください。kisoku,sur,pho<br>
pho<br>
['長野', '新', '幹線', '車両', 'センター']<br>
input 0(non_strong) or 1(strong) example:0,1,1<br>
<br>
1,0,0,0,0<br>
[[1, 10], ['ナガノ', 'シンカンセンシャリョーセンター'], ['長野', '新幹線車両センター']]
<br>
のように0,1で話者の強調(としているパラメータ)とCRFで予測しているアクセント単位形から、<br>
アクセントの切れ目を予測し、複合名詞全体のアクセントを表示します。<br>
(条件にkisokuを選ぶと、<a href= "http://open-jtalk.sourceforge.net" >OPENJTALK</a>
、
<a href= "https://sites.google.com/site/suzukimasayuki/accent" >TASET</a>
を元にした規則ベースのアクセント(<a href= "https://search.ieice.org/bin/summary.php?id=j66-d_7_849" >匂坂ら(1983)</a>、
<a href= "http://id.nii.ac.jp/1001/00015881/" >宮崎(1983)</a>)合成を行います。)
<br>
<h1>【簡単な動作原理】</h1>
『ＮＨＫ日本語発音アクセント新辞典』の付録に記載の<br>
「アクセント単位形」という考え方をコンピュータで使えないかと作成したものです。
<br>
以下の説明は、本ソースコード群を作成した際に作成したものです。
<br>
語句のにはある単位でアクセントが乖離しないもの、するものが存在する。<br>
ある強調が入ったとき、<br>
その違いをアクセント単位形で示し、単位形が0なら次の単位と結合、<br>
1なら乖離する。<br>
アクセント単位形の予測は、語句の単位(unidicの短単位を想定)レベルのアクセント句による。<br>
アクセント句が0(平板型)なら、アクセント単位形は0<br>
それ以外なら1<br>
<br>
例:長野新幹線車両センター<br>
CRFによるアクセント単位形予測が<br>
1,1,1,0,0<br>
と予測され、<br>
ユーザーから強調入力が<br>
1,0,0,0,0<br>
だった場合。<br>

アクセント結合可否<br>
'長野':乖離<br>
'新':結合<br>
'幹線':結合<br>
'車両':結合<br>
'センター':結合<br>
<br>
結果:[[1, 10], ['ナガノ', 'シンカンセンシャリョーセンター'], ['長野', '新幹線車両センター']]
<br>
※アクセント単位形の予測は<br>
<a href= "https://pj.ninjal.ac.jp/corpus_center/csj/" >『日本語話し言葉コーパス( Corpus of Spontaneous Japanese : CSJ ) 』</a>
で学習しています。
<br>
<br>
<h1>【動作条件】</h1>
<a href= "https://taku910.github.io/mecab/" >Mecab</a>
<a href= "https://taku910.github.io/crfpp/" >CRF++</a>
のpathが通っていることが動作条件です。<br>
(-OverboseできるversionのMecabを使用してください。)<br>
<br>
また、Mecab辞書として
<a href= "https://unidic.ninjal.ac.jp/download#unidic_bccwj" >unidic-cwj-2.3-2.0</a> 
を
使用します。ダウンロードしたディレクトリをこのreadmeと同じディレクトリに(unidic-cwj-2.3-2.0)という名前で置いて下さい。<br>
(システム辞書のデフォルトに設定する必要はありません。)<br>
<br>
Mecabespresso/Mecabespresso.py でMecabのコマンドを、<br>
CRFsyori/CRFsyori.py および CRFsyori2/CRFsyori2.py でCRF++のコマンドを呼び出しています。<br>
コマンドラインの返却値を利用するので、pythonでのコマンドライン結果を取得できるpython環境でご利用ください。<br>
(pyenv等で指定されている場合は該当ディレクトリで設定されているpythonのパスと同じものを使用してください。)<br>
<br>
<h1>【使用方法】</h1>
ターミナルで<br>
do.pyでCUI版を<br>
GUI.pyでGUI版を実行できます。<br>

<h1>【発表予定】</h1>
本研究は、<br>
第83回情報処理学会全国大会<br>
学生セッション［7N会場］（3月20日（土）　13:10〜15:10）<br>
音声言語情報処理（2）<br>
7N-02<br>
<a href= "https://www.gakkai-web.net/gakkai/ipsj/83/program83.html#t4" >アクセント単位形の推測を用いた日本語複合名詞のアクセント句の合成</a>
○青柳詠美，小島正樹（東京薬科大）<br>
で発表します。
<br>
<h2>【連絡先】</h2>
https://github.com/Harunouta/Accent_Sandhi_by_EAUT　より　forkさせていただきます。
