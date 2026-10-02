# World Model × Ontology × JEV

## 基本思想

世界を理解するためには、データを集めるだけでは足りない。世界に何が存在するか、それらをどう分類するか、目の前の具体物が何なのか、その判断をどう構造化するか、そして意味をもとに何をするかを分離する。

World → World Model → Ontology → JEV → Semantic AST → Agent → Action

## World Model

World Model は「世界には何が存在し、どのような関係を持っているか」を表す。Repository、Directory、File、Workflow、Issue、Commit、Document、Paragraph、Sentence、Person、Agent、Action など、観測対象と関係をモデル化する。

ここではまだ「この文章は依頼である」と判断しない。「これは GitHub Issue に含まれる文章である」という世界の事実を扱う。

## Ontology

Ontology は「世界に存在するものを、どのような種類として扱うのか」を定義する Semantic Dictionary である。

例: repository / file / directory / issue / idea / insight / memo / prompt / script / request / complaint / command / question / assertion / proposal / instruction / narration

Ontology は自由なタグの集合ではなく、できるだけ controlled vocabulary として管理する。

## Type と Instance

型と実体を混同しない。issue は型であり、GitHub Issue #123 はそのインスタンスである。request は型であり、「READMEを整理してください」という具体的な発話がそのインスタンスになる。

Ontology → type、World → instance という関係である。

## JEV

JEV は「この具体的なものは、実際には何なのか？」を判断する意味層である。World Model と Ontology を参照し、観測した具体物について judgment を行う。

例:

- 「README整理して」→ request
- 「READMEぐちゃぐちゃで困る」→ complaint
- 「READMEを整理しろ」→ command
- 「READMEどう整理する？」→ question

JEV は単なる classifier ではなく、Judgement + Evidence を返す。

## Content Type と Speech Act

「何というコンテンツなのか」と「何をしようとして発話されたのか」は分ける。

Content Type: issue / idea / insight / memo / prompt / script

Speech Act: request / complaint / command / question / assertion / proposal / instruction / narration

したがって、Issue の中に request が書かれている、という構造を表現できる。

## 一文単位まで降りる

JEV は repository 単位だけでなく、Organization → Repository → Directory → File → Document → Paragraph → Sentence → Phrase と解像度を下げられる。

README 全体についても、一文ごとに assertion、description、complaint、proposal、request などを判断できる。

## Semantic AST

JEV の判断結果は Semantic AST として保存する。

例:

entity: sentence
content_type: idea
speech_act: proposal
subject: repository/readme.yaml
action: create/metadata-type-definition
judgment: confidence 0.91
evidence: sentence 12

ここで type と judgment は別物である。type は Ontology に存在する正式な型、judgment は JEV が今回のインスタンスについて行った判断である。

これにより confidence、evidence、判断履歴、再判定を扱える。

## Evidence

JEV は判断だけを出さず、可能な限り根拠を残す。

Repository なら README.md、RUBRIC.md、SERIES.md、seed/、STAGE/ など。Sentence なら sentence index、該当語、target など。

つまり JEV の出力は Judgement + Evidence である。

## 不確実なら質問する

JEV は分からないものを無理に分類しない。

例えば「これ、READMEどうにかして」は request、complaint、proposal の区別が曖昧である。その場合は judgment: unknown とし、「READMEを修正してほしい、という依頼ですか？」のように質問する。

判断できる → 判断する。判断できない → 質問する。

これは単純な classifier ではなく、uncertainty を扱う semantic agent になる。

## Repository も同じ方法で読む

Repository についても README、Issues、Directory、Files、Workflows、Commits、Config、Tests などを観測し、JEV で意味づけできる。

Repository → evidence → JEV → type + purpose + inputs + outputs + workflow + evidence

つまり Repository 自体を一つの「意味を持った存在」として読む。

## readme.yaml の役割

この考え方では readme.yaml は README の補助ファイルにとどまらず、Semantic Dictionary / Ontology の入口になる。

想定する型定義には repository、file、document、sentence、content、speech-act、status、relation、workflow、evidence などがある。

## readme.yaml と ast-jev の分離

readme.yaml は「世界をどういう言葉で記述するか」を定義する。ast-jev は「目の前の世界を、その言葉でどう解釈するか」を実行する。

readme.yaml → Ontology / Semantic Dictionary / Type Definition
ast-jev → Observation / Judgment / Evidence / Question → Semantic AST

## bons.ai Agent

Agent は JEV の判断を利用する。

World → World Model → Ontology → JEV → Semantic AST → Agent → Action

例えば「README整理して」は、sentence → JEV → speech_act=request / target=README / action=organize → Agent → 調査 → 変更案 → 実行、という流れになる。

## 最終的な責務分離

World は repo / file / issue / text。World Model は entities / relations / state。Ontology は types / vocabulary / rules。JEV は judgment / evidence / ask。Semantic AST は structured meaning。Agent は reasoning / planning。Action は edit / create / search / run。

## まとめ

これは単なる README metadata でも text classifier でもない。

世界を観測し、Ontology によって意味を定義し、JEV によって具体的な存在を判定し、Semantic AST として保持し、その意味を Agent の行動につなげるための基盤である。

対応関係:

JSON = Data Dictionary
Ontology = Semantic Dictionary
World Model = 世界の状態・関係
JEV = Semantic Judgment
AST = Judgment の構造表現
Agent = Judgment を使って行動する存在

最終的には bons.ai の各 Agent が個別に世界を解釈するのではなく、共通の意味層を持つ。

World → World Model → Ontology → JEV → Semantic AST → Agent → Action

「1 repo 1 agent」であっても、Agent ごとに世界の意味がバラバラにならない。

readme.yaml が Semantic Dictionary、ast-jev が Semantic Judgment Engine、各 bons.ai Agent がその上で動く実行主体、という三層構造になる。

---

# 世界を分類する機械

男は、一台の機械を作った。

「この機械は、世界を理解します」

友人が眉をひそめた。

「ずいぶん大きなことを言うね」

「簡単ですよ。まず世界モデルを作る」

機械の画面に、木が表示された。

「木」

「それだけ？」

「次にオントロジーです。木には種類があります。植物、家具、材料、象徴……」

「なるほど」

「そしてJEVが判断します」

男が木を指さした。

「これは？」

機械が答えた。

> 植物。

「正解だ」

次に男は、机の上の書類を指した。

「これは？」

> Issue。

「正解」

「これは？」

男は一枚のメモを見せた。

> README整理して。

機械は少し考えた。

> request。

「すばらしい」

男は嬉しくなった。

「これで機械は、人間の言葉まで理解できる」

ところが、機械は突然、

> 質問があります。

と表示した。

「なんだ？」

> 「README整理して」は、依頼ですか？

「そうだ」

> 命令ではありませんか？

「まあ、命令といえば命令だが……」

> ぐちではありませんか？

「違う」

> 提案では？

「違う」

> 冗談では？

男は黙った。

機械は続けた。

> 判断できません。

「では、質問すればいい」

> 何を？

「本人に聞け」

機械は男を見た。

> あなたは、READMEを整理してほしいのですか？

「そうだ」

> 本当に？

「本当だ」

> なぜ？

男は困った。

「……きれいにしたいからだ」

> なぜきれいにしたいのですか？

「機械が読みやすいように」

> なぜ機械が読みやすい必要があるのですか？

「機械が世界を理解するためだ」

機械はしばらく沈黙した。

そして、新しい分類を追加した。

> **人間：世界を理解したい存在**

男は満足した。

「とうとう人間まで分類できたな」

機械は答えなかった。

そのころ機械の内部では、

World
↓
World Model
↓
Ontology
↓
JEV
↓
Semantic AST
↓
Agent

という処理が、静かに繰り返されていた。

そして最後に、まだOntologyに存在しないものが一つだけ残っていた。

> **世界そのもの。**
