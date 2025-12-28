# 🧠 Prompt Engineering Techniques

プロンプトエンジニアリング手法の体系的な解説と実務例集

## 📚 カテゴリ構成

### 01_essential/ - 必須手法 ⭐
実務で必ず使用する基本的かつ重要な手法

- **01_role_playing.md** - ロールプレイングプロンプト（役割定義）
- **02_chain_of_thought.md** - CoT（思考の連鎖）
- **03_zero_shot_cot.md** - Zero-shot CoT（step by step）
- **04_output_format.md** - 出力形式の指定方法（Markdownコードブロック）
- **05_a_to_z.md** - A to Z（包括的な指示）

### 02_standard/ - 標準手法
基本を理解した上で活用する実用的な手法

- **01_few_shot_learning.md** - Few-shot Learning（例示学習）
- **02_both.md** - Both（両方の視点）
- **03_mock.md** - Mock（模擬・シミュレーション）

### 03_advanced/ - 高度な手法
複雑なタスクや特殊なケースで活用する専門的手法

- **01_react.md** - ReAct（推論と行動）
- **02_tree_of_thoughts.md** - ToT（思考の木）
- **03_metacognitive.md** - Metacognitive Prompting（メタ認知）
- **04_step_back.md** - Step Back（一歩引いた視点）
- **05_iep.md** - IEP（推論的除外）
- **06_self_consistency.md** - Self-Consistency（自己無撞着性）
- **07_generated_knowledge.md** - Generated Knowledge Prompting
- **08_emotion_prompt.md** - EmotionPrompt（感情プロンプト）
- **09_instruction_tuning.md** - Instruction Tuning
- **10_self_correction.md** - Chain of Thought with Self-Correction
- **11_recursive.md** - Recursive Prompting（再帰的プロンプト）
- **12_summarization.md** - Summarization with Constraints

## 🎯 使用方法

1. **初心者**: まず `01_essential/` の5つの必須手法を習得
2. **中級者**: `02_standard/` の標準手法で実務の幅を広げる
3. **上級者**: `03_advanced/` の高度な手法で複雑な課題に対応

## 📖 各ファイルの構成

各Markdownファイルには以下が含まれます：

- **概要** - 手法の簡潔な説明
- **重要度** - 必須/推奨/応用の分類
- **使用場面** - どんな時に使うか
- **基本パターン** - プロンプトテンプレート
- **実務例** - 実際に使えるプロンプト例と期待される出力
- **組み合わせ** - 他の手法との相乗効果
- **注意点** - 使用時の注意事項

## 🔄 推奨される組み合わせ

### 必須の組み合わせ
```
Role-playing + CoT + Zero-shot CoT + 出力形式指定
```

### 高度な組み合わせ
```
Role-playing + ToT + Self-Consistency + 出力形式指定
```

## 📊 対応AIツール

- ChatGPT (GPT-4, GPT-3.5)
- Claude (Opus, Sonnet, Haiku)
- Gemini
- その他LLMツール
