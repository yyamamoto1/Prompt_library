# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a comprehensive AI prompt library containing 300+ prompts organized by category and use case. The library serves as a curated collection of production-ready prompts for various AI tools (ChatGPT, Claude, Gemini, etc.).

## Architecture & File Structure

The repository uses two distinct prompt formats based on category:

### Format 1: YAML Prompts (Creative/Utility Categories 01-10)

**Location**: `01_image/`, `02_movie/`, `03_comic/`, `04_music/`, `05_writing/`, `06_utility/`, `07_RAG_agent/`, `08_learning_support/`, `09_communication/`, `10__management/`

**Structure**:
```yaml
prompt: |
  Generate a photorealistic portrait...

  **CUSTOMIZABLE PARAMETERS:**
  - **Parameter Name:** [Options: "option1", "option2", "option3"]

  **CORE CHARACTERISTICS:**
  - Detailed specifications...

  **TECHNICAL SPECIFICATIONS:**
  - Camera, lighting, composition details...
```

**Key Patterns**:
- Multi-level nesting with subcategories (e.g., `01_image/01_creation/01_model/`)
- Age-based organization (10s, 20s, 30s, 40s, 50s, 60s_over)
- Gender-specific paths (`female/`, `male/`)
- Common templates in `_common_age/` directories with reusable patterns

### Format 2: Markdown Prompts (Marketing/Business Categories)

**Location**: `Xアフィリエイト/`, `PPCアフィリエイト/`, `ブログアフィリエイト/`, `インスタアフィリエイト/`, `YouTubeアフィリエイト/`, `TikTokマーケティング/`, `メルマガマーケティング/`, `Kindle出版/`, `自動収入構築/`, `LP・セールスページ/`

**Structure**:
- Each category contains exactly 25 numbered prompt files (01-25)
- Filenames are descriptive in Japanese: `01_戦略名.md`
- Self-contained, ready-to-use prompts

## Expanding Existing Prompts

When enhancing prompts (as demonstrated in recent commits), follow these patterns:

### Target Expansion Size
- **Base prompts** (e.g., `female.yml`, `male.yml`): 75-85 lines with comprehensive parameters
- **Category prompts** (personality, style, hobby): 150-200+ lines with 6-14 detailed archetypes/categories
- **Age-specific prompts**: 33+ lines with focused demographic details

### Required Sections for Detailed Prompts

1. **Customizable Parameters** - Multiple selection options for flexibility
2. **Core Characteristics** - Face structure, features, detailed descriptions
3. **Styling Variations** - Hair, makeup/grooming, clothing, accessories
4. **Expression & Pose Options** - Multiple options for different use cases
5. **Technical Specifications**:
   - Camera setup (body, lens, aperture)
   - Lighting design (style-specific options)
   - Composition (framing, background, depth)
   - Image quality (resolution, detail, color, texture)
6. **Output Specifications** - Quality standards and use cases

### Pattern: Multiple Archetypes/Categories

When expanding category files, provide 6-14 distinct options:
- **Personality**: Different character archetypes (confident, creative, intellectual, etc.)
- **Style/Fashion**: Complete style categories (bohemian, professional, street, etc.)
- **Hobby/Role**: Professional roles with authentic context (14+ roles)

Each archetype should include specific guidance for:
- Expression and body language
- Setting and environment
- Clothing and accessories
- Lighting style
- Overall mood/energy

## Development Workflow

### Index Folder Rule

The `index/` folder serves as a temporary inbox for new prompts. When files are found in `index/`:

1. **Review the content** to understand the prompt's purpose
2. **Determine the appropriate category** based on the content:
   - Image generation/editing → `01_image/`
   - Video/movie related → `02_movie/`
   - Code/development → `06_utility/01_code/`
   - AI agent/RAG → `07_RAG_agent/`
   - Text manipulation → `06_utility/02_general_task/`
   - etc.
3. **Convert to YAML format** if the file is in Markdown (for categories 01-10)
4. **Move to the appropriate subfolder** with a descriptive filename
5. **Delete the original file** from `index/`

### Adding New Prompts

1. **For Creative Categories (01-10)**: Add `.yml` files in appropriate subcategory
2. **For Marketing Categories**: Create numbered `.md` files (maintain 25 per category)
3. **Maintain consistency**: Match existing prompt depth and structure within each category

### Expanding Prompts

1. Read existing file first to understand current structure
2. Preserve original intent while adding depth
3. Use English for consistency (avoid Japanese/English mixing in technical specs)
4. Include multiple customization options
5. Add comprehensive technical specifications
6. Ensure 4K+ resolution specs for image prompts

### File Naming Conventions

- **YAML files**: Match directory name (e.g., `10s.yml` in `10s/` directory)
- **Common templates**: Use descriptive names (`01_personality.yml`, `02_style_fashion.yml`)
- **Markdown files**: Numbered with Japanese descriptive names (`01_戦略名.md`)

## Key Principles

1. **Comprehensive over minimal**: Detailed prompts with multiple options are preferred
2. **Structured parameters**: Always use `[Select: "option1", "option2"]` format for choices
3. **Technical precision**: Include specific camera models, lens specs, lighting setups
4. **Use case versatility**: Prompts should work for commercial, editorial, and artistic applications
5. **Avoid stereotypes**: Include guidance on authentic, culturally sensitive representation

## Repository Stats

- **Total prompts**: 300+ files
- **Creative categories**: 10 directories (YAML format)
- **Marketing categories**: 10 directories (Markdown format, 25 prompts each)
- **Recent enhancement**: 6 files expanded (+812 lines, detailed specifications added)
