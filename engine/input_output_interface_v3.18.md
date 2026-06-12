# 输入输出接口定义 v3.18

## 1. 用户输入格式（User Input）

### 1.1 新故事初始化输入
```yaml
project_name: string
genre_core: string
core_theme: string
core_plot_idea: string
word_count_target: number
style_preference: list
main_characters: list
```

### 1.2 推进故事输入
```yaml
current_project_id: string
user_instruction: string
custom_constraints: list
```

## 2. 系统输出格式（System Output）

```yaml
content: string
branch_options: list
  - option_id: string
    description: string
    logic_basis: string
    expected_consequences: list
    risks: list
critique_report: object
state_update_summary: object
memory_update: object
next_suggestions: list
```

## 3. 设计原则
- 输入输出尽量结构化，便于后续实现。
- 输出必须包含可解释性（逻辑依据、批判报告）。
- 支持用户随时干预。