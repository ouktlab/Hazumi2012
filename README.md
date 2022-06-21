﻿# Hazumi2012
Osaka University Multimodal Dialogue Corpus (Hazumi2012)

Hazumi2012では以下のファイル群を公開している（もしくは公開予定）．
```
1. ビデオデータ
2. 閲覧用ELANファイル
3. 実験用ダンプファイル
4. アンケートデータ
```
本サイトでは，2.をelan/以下で，3.をdumpfiles/で，4.をquestionnaire/以下で公開している．

## 1. ビデオデータ
データ利用に関する契約を交わした利用者のみに対して，NII IDR （国立情報学研究所 情報学研究データリポジトリ）から配布される．データの入手方法や概要説明ドキュメントは，NII IDRサイトを参照のこと． https://www.nii.ac.jp/dsc/idr/rdata/Hazumi/

## 2. 閲覧用ELANファイル
アノテーションや書き起こしを全て含んだeaf（ELAN annotation format）ファイ
ルである．
アノテーションツールELANで，実験参加者ビデオを読み込んで使用する．

elan/ 以下に，(実験参加者ID).eaf という名前で置かれている．実験参加者ID
は以下で示すYYMMGAANNの9文字である．  
　YYMM コーパスのバージョン．ここでは2012である．  
　G 実験参加者の性別．M（男性）もしくはF（女性）．  
　AA 実験参加者の年代．20から60まで．  
　NN 上記7文字と合わせてIDとなるように付番．

例えば2012F2001は「Hazumi2012の，20歳代のある女性のデータ」を意味する．

交換と呼ばれる単位ごとに，以下で示されるデータが付与されている．
詳しくは以下の概要説明ドキュメントを参照のこと．
https://www.nii.ac.jp/dsc/idr/rdata/Hazumi/documents/HazumiOverview.pdf

#### 実験参加者の発話の書き起こし
#### システム発話とその対話行為
#### 心象アノテーション
3名の第三者アノテータがが付与した (TS: Third Sentiment) ．

#### 話題継続アノテーション
3名の第三者アノテータがが付与した (TC: Topic Continuance) ．


## 3. 実験用ダンプファイル
対話中のユーザ（実験参加者）の心象を含むラベルデータを予測を対象として， 簡便にマルチモーダル機械学習実験を行えるように作成している．このファイルは， 機械学習の入力として利用できる，ユーザの音声，映像，発話内容（言語）から抽出したマ ルチモーダル特徴量（実数値）とともに，機械学習の出力として利用できる第三者により付与された 心象値・話題継続アノテーションの値（いずれも連続値）を格納している．

### フォルダの構造とファイル：
dumpfiles/      
　├ 2012F2001.csv　  
　├ 2012F2002.csv　  
　:  
　:  

各ファイル（例：2012F2001.csv）は各セッションにおける参加者の発話対ごとのマルチモーダル特徴量とアノテーションの値を含んでいる．計63人分のダンプファイルを格納している．

### 実験用ダンプファイル中のデータ説明：
各列はデータの属性，各行は1発話対で抽出された各特徴量の数値を格納している．  
1行目はデータの属性名を示す．


#### start(exchange), end(exchange):
ユーザの上半身動画（mp4）における発話交換（発話対）の開始，終了時間

#### TC1~TC3:
3名により付与されたtopic continuanceのアノテーション値.

#### TS1~TS3:
3名により付与されたthird sentimentのアノテーション値．

#### Dialogue_act
システム発話の対話行為タイプが格納されている．

#### pcm_RMSenergy_sma_max ~ F0_sma_de_kurtosis:
OpenSmileによって抽出された韻律特徴量．Config fileはIS09_emotion.confである．


#### 17_acceleration_max~AU45_c_mean:
顔表情特徴量．「17」のような数字はOpenFaceのlandmarkを示す. AUはaction unit．
landmark特徴量はOpenFaceから得られる2次元座標データ(30fps)をもとに，目の周り，口の周りなどの12点のフレーム間速度と加速度を交換内で求め，最大値，平均値，標準偏差を特徴量とした. また交換内でのAUの有無の平均を特徴量とした.

#### ADJ～bert767：
ユーザ発話から抽出された言語特徴量が格納されている.
書き起こしデータ内のユーザ発話から特徴量を抽出した合計785次元である．
Stanza NLPを使用して形態素解析を行い，1発話内に含まれる品詞ごとの単語数を計算している（17次元）．
また，Wikipediaに含まれるテキストデータより学習したBERTモデルを利用して，
1発話（単語列）を768次元のベクトルに変換した特徴量も含む．
以下で実装されたBERTモデルを用いている．
https://github.com/yoheikikuta/bert-japanese


### マルチモーダルデータの同期方法：
ユーザの音声データ，映像データはZoomを通じて取得したため，
映像と音声の時刻同期は取れている．
言語特徴量（素性）は発話区間に対応するユーザ発話の書き起こしテキストから抽出した．

詳しくは概要説明ドキュメントを参照のこと．
https://www.nii.ac.jp/dsc/idr/rdata/Hazumi/documents/HazumiOverview.pdf


## 4. アンケートデータ
実験参加者とWizardの双方に対して，実験開始前と実験終了後の両方に実施したアンケートに関するデータである．
questionnaire.xlsxというエクセルファイルとして置いている．
[アンケート項目はHazumi1911と同様
](https://github.com/ouktlab/Hazumi1911/blob/master/questionnaire/1911questionnaire_items.pdf)である．

アンケート結果ファイルには，まず，実験参加者（実験前），実験参加者（実験後），Wizard（実験前），Wizard（実験後）の4つのタブがある．
このそれぞれにおいて，実験参加者は18項目，Wizardは簡略化した3項目に対して，8段階で回答した結果が記録されている．

これに加え，「記述式」「性格特性」という2つのタブに，事後に尋ねた
アンケート結果が記録されている．


# Authors
* 駒谷 和範（大阪大学 産業科学研究所） komatani@sanken.osaka-u.ac.jp
* 岡田 将吾（北陸先端科学技術大学院大学） okada-s@jaist.ac.jp
