# WB改修による店舗の事務作業の効率化

## 社内向け資料です。

店舗事務の所要時間の低減プロジェクトの一環として、
本年度開発を予定していたWBの改修に合わせて実施することが
可能と予想される改修の一覧を示します。

## 勤怠管理

### 概要
以下の点が効率的な運用を阻害していると判断します。
* シフト組みの際の全スタッフとのコミュニケーション
* スタッフのニーズを考慮しつつシフト組を行うことの難しさ
* 紙運用が前提になっていること
* GUIの操作性の悪さ
* 月末確定時作業の煩雑さ

そこで、これらの問題を解決する改修を実施したいと考えます。

### 全般
#### 画面遷移
##### 改善点
* ページのリロードの発生を抑制し、データだけをやり取りする設計に変更する

##### 効果
* 性能の改善、ユーザビリティの向上

#### 印刷機能
##### 改善点
* 印刷用帳票はすべてPDFとして出力
* サーバから直接プリンタに印刷キューを送信

##### 効果
* 環境依存のレイアウト崩れ等の抑止
* 非Windows端末での印刷を可能にする

### シフト作成
#### 希望シフト収集機能の追加
##### 改善点
* 従業員個人から希望シフトを収集する機能を追加する
  * 希望内容をDWS等に表示する(希望・シフト・実績を並べて表示)
* 確定したシフトを従業員個人に通知する機能を追加する

##### 効果
* 店長・スタッフ間のコミュニケーション効率の向上
* シフト組み作業の効率UP

#### HLGの拡張
##### 改善点
* 売上と直接結びつかない必要人員の定義を可能とする(ex.寸胴移動、両替、買い物)

##### 効果
* HLGの信頼性向上による、シフト組み作業の効率と精度のUP
* 人件費の大枠予測を可能にする(HLGの月合計*平均時給)

### 打刻
##### 改善点
* 顔認証による打刻とする
* 複数回休憩可能とする
* 休憩がn時間以上であれば、自動で複数回出勤と認識させる機能の追加
* 本人による変更申請を可能とする。申請者の１つ上の職位者の承認を持って確定する
* 変更に関するすべての履歴を残す。

##### 効果
* 勤怠実績管理に関わる諸業務の低減
* 印刷済みDWS保管義務からの開放

### 確定処理
#### 確定業務
##### 改善点
* 一日単位の勤怠確定作業の廃止
* 月単位の確定は本部で実施。稼働中の申請がゼロになった時点で可能とする

##### 効果
* 月末作業の軽減

### 人件費管理
##### 改善点
* 人件費の計算に給与システム(SSPR)を使用するように変更する
  * リアルタイムではなく、半日に１回などに変更
* SSPRでの計算結果を受け取って、WB上に人件費として表示

##### 効果
* 計算結果精度の向上および、制度改正時における柔軟性の獲得

## 予算管理

### 売上予算管理
##### 改善点
* 売上予算の粒度を 時間帯あたりから時間あたりに変更する
* 機械学習を用いた売上予測機能を実装し、予算策定を支援する

##### 効果
* 売上予算の精度向上と、HLGへのダイレクトな反映（因果関係がわかりやすくなる）

## 金銭管理
金銭管理については、３分野(売上・入金・小口)の効率化と、現金実査機能の追加により、
ガバナンスレベルを上げつつ、作業工数を大幅に削減可能と考えられます。

### 現金実査機能の追加
##### 改善点
* EXCELを使った従来の方法を廃し、WB上のツール用いた方式に変更する
* スマートフォン・タブレットで使用可能とする

##### 効果
* スマホ使用による、作業の効率向上
* チェック履歴をサーバ上に残すことによる、管理精度の向上

### 小口現金管理の効率化
##### 改善点
* 店舗でのすべての出納情報の登録作業を排除する。
* 代替として、店舗では証跡(領収書)のスキャニングだけを行う
* 外部委託先で仕訳化したデータを表示(R/O)する。

##### 効果
* 業務ボリュームの低減および、責任からの開放
* 入力ミス撲滅による、店舗本部間の調整・連絡業務の軽減

### 入金管理の効率化
##### 効果
* 店舗での登録作業を排除する
* 銀行より定期的に取得したデータを表示(R/O)する

##### 効果
* 業務ボリュームの低減および、責任からの開放
* 入力ミス撲滅による、店舗本部間の調整・連絡業務の軽減

### 売上登録の効率化
##### 改善点
###### 全般
* サマリーではなく、取引履歴を保持する
* Deliousから出る帳票を正として保管するフローの廃止

###### 22インチ寺岡・レジ
* 店舗で発生するすべての取引を券売機・レジを通して計上する
* 券売機からデータを受信した時点で売上を確定する
* WB上での売上高修正機能をオミットする

###### 19インチ寺岡・芝浦券売機
* 券売機外の取引に関しては、従来の総数で登録ではなく、履歴をすべて登録する形に変更する
* 上記の登録タイミングは券売機からの受信タイミングとは独立させる

##### 効果
* 業務ボリュームの低減および、責任からの開放
* 22インチでは、紙のジャーナル保管が不要になる（電子ジャーナル化）
* 券売機からデータを受信した時点で売上が確定するため、券売機締め→確定までの待ち時間が不要になる
* 19インチの場合、業務効率は若干落ちるが、精度が大幅に向上する
  * 将来的に22インチ版以上の機能に収束していくため、次第に全体最適化される
