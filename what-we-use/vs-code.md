# Visual Studio Code <!-- omit in toc -->

Table of Contents

- [Tutorial](#tutorial)
- [Extensions](#extensions)
  - [Code Spell Checker](#code-spell-checker)
  - [Batch Rename](#batch-rename)
  - [Error Lens](#error-lens)
  - [Pretty TypeScript Errors](#pretty-typescript-errors)
  - [SonarLint](#sonarlint)
  - [jwt-decode](#jwt-decode)
  - [Duplicate Action](#duplicate-action)
  - [GitLens](#gitlens)
  - [Unix Time Converter](#unix-time-converter)
  - [Better Comments](#better-comments)
  - [Live Share](#live-share)
  - [Polacode 2022](#polacode-2022)
  - [Markdown All in One](#markdown-all-in-one)
  - [Paste JSON as Code](#paste-json-as-code)
  - [Sort JSON Objects](#sort-json-objects)
- [Shortcuts](#shortcuts)
- [Settings](#settings)
- [Markdown](#markdown)
- [GitHub Copilot](#github-copilot)
  - [The Inspiration](#the-inspiration)
  - [Autocompletion](#autocompletion)
  - [Chat](#chat)
    - [Inline Chat](#inline-chat)
    - [Sidebar Chat](#sidebar-chat)
    - [Voice Chat](#voice-chat)
  - [Three Ss](#three-ss)
- [Recommended set up on repositories](#recommended-set-up-on-repositories)
- [Reference](#reference)

## Tutorial

> Open the Welcome page from the Help > Editor Playground menu or use the Help: Interactive Editor Playground command from the Command Palette (⇧⌘P).

## Extensions

- Most of the images are from the original plugin page

### [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker "https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker")

![Code Spell Checker](https://raw.githubusercontent.com/streetsidesoftware/vscode-spell-checker/main/images/suggestions.gif)

- find spelling mistakes

---

### [Batch Rename](https://marketplace.visualstudio.com/items?itemName=JannisX11.batch-rename-extension "https://marketplace.visualstudio.com/items?itemName=JannisX11.batch-rename-extension")

![Batch Rename](https://raw.githubusercontent.com/JannisX11/batch-rename/main/media/demo.gif)

- Rename multiple files easily

---

### [Error Lens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens "https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens")

![Error Lens](https://raw.githubusercontent.com/usernamehw/vscode-error-lens/master/img/demo.png)

- Display error at the end of the line

---

### [Pretty TypeScript Errors](https://marketplace.visualstudio.com/items?itemName=yoavbls.pretty-ts-errors "https://marketplace.visualstudio.com/items?itemName=yoavbls.pretty-ts-errors")

![Pretty TypeScript Errors](https://raw.githubusercontent.com/yoavbls/pretty-ts-errors/b358fed5b4437be9fe109a836b77c6ca88a273a6/assets/this.png)

- Wrap the error in a more readable way

---

### [SonarLint](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarlint-vscode "https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarlint-vscode")

![SonarLint](https://raw.githubusercontent.com/SonarSource/sonarlint-vscode/b446efa174ad1bf03a3c98a2fe68c7fe6c74b45c/images/sonarlint-vscode.gif)

- Provide additional recommendations other than eslint
- Further set up please refer to [here](./sonarqube.md "./sonarqube.md")

---

### [jwt-decode](https://marketplace.visualstudio.com/items?itemName=jflbr.jwt-decoder "https://marketplace.visualstudio.com/items?itemName=jflbr.jwt-decoder")

![jwt-decode](https://raw.githubusercontent.com/jflbr/jwt-decoder/master/images/demo-from-untitled-document.gif)

- Decode JWT Token in VSCode

---

### [Duplicate Action](https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-duplicate "https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-duplicate")

![Duplicate Action](./duplicate-action.png "./duplicate-action.png")

- Click `Duplicate File or Directory` to duplicate the whole target group

---

### [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens "https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens")

![GitLens](https://raw.githubusercontent.com/gitkraken/vscode-gitlens/main/images/docs/current-line-blame.png)

- Show who has edited the code before

---

### [Unix Time Converter](https://marketplace.visualstudio.com/items?itemName=espresso3389.unixtime-converter "https://marketplace.visualstudio.com/items?itemName=espresso3389.unixtime-converter")

![Unix Time Converter](https://raw.githubusercontent.com/espresso3389/unixtime-converter/master/images/intro.gif)

- Convert unix timestamp to readable time

---

### [Better Comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments "https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments")

![Better Comments](https://raw.githubusercontent.com/aaron-bond/better-comments/084a906e73a3ca96d5319441714be8e3a2a8c385/images/better-comments.PNG)

- Highlight common TODO phrases

---

### [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare "https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare")

![Live Share](https://user-images.githubusercontent.com/116461/47793782-4d253500-dcdc-11e8-9c76-3d9d5b474d9d.png)

- Live sharing and collaboration tool on VScode

---

### [Polacode 2022](https://marketplace.visualstudio.com/items?itemName=jeff-hykin.polacode-2019 "https://marketplace.visualstudio.com/items?itemName=jeff-hykin.polacode-2019")

- Extract code segments as beautiful images

![Polacode 2022](https://github.com/octref/polacode/raw/master/demo/usage.gif)

---

### [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one "https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one")

- Extra support on markdown

---

### [Paste JSON as Code](https://marketplace.visualstudio.com/items?itemName=quicktype.quicktype "https://marketplace.visualstudio.com/items?itemName=quicktype.quicktype")

- JSON with interfaces in typescript

![Paste JSON as Code](https://raw.githubusercontent.com/quicktype/quicktype-vscode/master/media/demo-interactive.gif)

---

### [Sort JSON Objects](https://marketplace.visualstudio.com/items?itemName=richie5um2.vscode-sort-json "https://marketplace.visualstudio.com/items?itemName=richie5um2.vscode-sort-json")

- Sort JSON Objects

![Sort JSON Objects](https://raw.githubusercontent.com/richie5um/vscode-sort-json/6a2930b71ef8418b1bde43b554c5ef85b8ddba1f/resources/usage.gif "https://raw.githubusercontent.com/richie5um/vscode-sort-json/6a2930b71ef8418b1bde43b554c5ef85b8ddba1f/resources/usage.gif")

## Shortcuts

- Extract Variables & Functions
- Rename Symbols
- Text Selection
  - After selected the text and do a right-click, the menu on the selected text and number bar is completely different
- Dart Refactoring, check [here](https://dartcode.org/docs/refactorings-and-code-fixes "https://dartcode.org/docs/refactorings-and-code-fixes")

- [Refactoring Tips](https://code.visualstudio.com/docs/editor/refactoring "https://code.visualstudio.com/docs/editor/refactoring")
- open `Settings` - `cmd` + `,`
- Split editor: `cmd` + `\`
- Move across editor: `cmd` + `option` + `<` / `>`

- Change Cases with `cmd + p` + `>`, e.g. smart boy
  - `Transform to Kebab Case` - smart-boy
  - `Transform to Lowercase` - smartboy
  - `Transform to Uppercase` - SMARTBOY
  - `Transform to Snake Case` - smart_boy
  - `Transform to Camel Case` - smartBoy
  - `Transform to Pascal Case` - SmartBoy
  - `Transform to Title Case` - Smartboy

- `cmd` + `p` AND
  - `>` - Command mode
  - `@` - local symbol search
  - `#` - global symbol search

## Settings

```json
{
  // * TypeScript Inlay Hints
  // Show inference arguments & types in ghost text

  "typescript.inlayHints.parameterNames.enabled": "all",
  "typescript.inlayHints.variableTypes.enabled": true, // highly recommended
  "typescript.inlayHints.propertyDeclarationTypes.enabled": true,
  "typescript.inlayHints.parameterTypes.enabled": true, // highly recommended
  "typescript.inlayHints.functionLikeReturnTypes.enabled": true, // highly recommended

  // Update import paths when moved
  "javascript.updateImportsOnFileMove.enabled": "always",
  "typescript.updateImportsOnFileMove.enabled": "always",

  // * TypeScript Reference Code Lens
  "typescript.referencesCodeLens.enabled": true,

  // * TypeScript Implementation Code Lens
  // Useful on OOP Style
  "typescript.implementationsCodeLens.showOnInterfaceMethods": true,

  // * Typescript Path
  "typescript.preferences.importModuleSpecifier": "non-relative",

  // * Dart Inlay Hints
  // Show inference arguments & types in ghost text
  // Shortcut - `ctrl` + `opt`
  "[dart]": {
    // 'off' - never show
    // 'on' - always show
    // 'offUnlessPressed' - show only while shortcut keys are held down (default)
    // 'onUnlessPressed' - show, but hide while shortcut keys are held down
    "editor.inlayHints.enabled": "offUnlessPressed"
  },

  // * TSX / XML / HTML
  // Auto rename the closing tag when the open tag has updated
  "editor.linkedEditing": true,

  // Brackets with color lines
  "editor.guides.bracketPairs": true

  // * Ruler
  "editor.rulers": [100, 150], // can have multiple rulers

  // * Sticky Scroll
  "editor.stickyScroll.scrollWithEditor": true, // on editor
  "workbench.tree.enableStickyScroll": true, // on document ree

  // * Auto-hide on Mini-map
  "editor.minimap.autohide": true, // might not be very useful to everyone; need to set folding markers
  "editor.minimap.size": "fill",

  // * Auto newline
  "files.insertFinalNewline": true, // respect lint settings
  "files.trimTrailingWhitespace": true, // respect lint settings

  // * Auto Save
  "files.autoSaveWhenNoErrors": true,
  "files.autoSave": "onFocusChange",  // Save if lose focus

  // save space
  "workbench.tree.indent": 4,
}
```

- Inlay Hints

  ![Settings](./inlay-hinting-settings.png)
  ![Example](./inlay-hinting-example.png)

- Reference Code Lens

  ![Reference Code Lens](ts-references-code-lens.png)

- Ruler
- Word Wrap
- Autosave

- [Typescript Editing](https://code.visualstudio.com/docs/typescript/typescript-editing "https://code.visualstudio.com/docs/typescript/typescript-editing")

## Markdown

1. Shortcuts

    ```markdown
    // bang bang will show all the headers in workspace to be selected
    [here](##)
    ```

2. Drag the image / video to the editor AND hold `shift` to link it

## GitHub Copilot

### The Inspiration

- It is a tool to help engineers to focus on `ideas` and `testing`
- Less focus on syntax
- Copilot does not know something it does not know (Hallucination)

![Hallucination](./hallucination.png "./hallucination.png")

### Autocompletion

1. ghost text
   - type the function name
   - type the comment
     - purpose
     - input
     - output

| Usage                 | Windows            | Mac                   |
| --------------------- | ------------------ | --------------------- |
| Accept suggestion     | `tab`              | `tab`                 |
| Accept partially      | `ctrl` + `>`       | `cmd` + `>`           |
| Alternate suggestions | `alt` + `[` or `]` | `option` + `[` or `]` |
| All suggestions       | `ctrl` + `enter`   | `ctrl` + `enter`      |

### Chat

- use `@terminal`, `@vscode` and `@workspace`
- point to files by `#file:someFileName`, `#editor` and `#selection`

#### Inline Chat

- `ctrl` / `cmd` + `I`

```typescript
// q: what is software engineering?
```

#### Sidebar Chat

![sidebar chat](https://github.com/adamwan-nexplore/guidebook-nxp-hk/assets/124669872/dd9325eb-6988-4a78-94cf-140c36df84f2)

- Code copilot in the terminal

```bash
/fix
/tests
/explain
/git
```

#### Voice Chat

![voice chat](https://github.com/adamwan-nexplore/guidebook-nxp-hk/assets/124669872/d652878d-ea82-4e35-9042-bd4065cb78a4)

- `ctrl` / `cmd` + `I` AND `ctrl` / `cmd` + `I`

### Three Ss

- Simple
  - keep the intention simple
- Specific
  - keep the expected code generated to produce a few lines
- Short
  - only one to two sentences each time and words in each sentence should be minimal

- copilot will give more score to files you open
- highlight the code

## Recommended set up on repositories

- File Path: `.vscode/settings.json`

API

```json
{
  "recommendations": [
    "aaron-bond.better-comments",
    "dbaeumer.vscode-eslint",
    "eamodio.gitlens",
    "firsttris.vscode-jest-runner",
    "GitHub.copilot-chat",
    "GitHub.copilot",
    "JannisX11.batch-rename-extension",
    "jeff-hykin.polacode-2019",
    "mrmlnc.vscode-duplicate",
    "MS-vsliveshare.vsliveshare",
    "orta.vscode-jest",
    "quicktype.quicktype",
    "richie5um2.vscode-sort-json",
    "SonarSource.sonarlint-vscode",
    "streetsidesoftware.code-spell-checker",
    "usernamehw.errorlens",
    "yoavbls.pretty-ts-errors",
    "yzhang.markdown-all-in-one",
  ]
}
```

Web

```json
{
  "recommendations": [
    "aaron-bond.better-comments",
    "dbaeumer.vscode-eslint",
    "eamodio.gitlens",
    "firsttris.vscode-jest-runner",
    "GitHub.copilot-chat",
    "GitHub.copilot",
    "JannisX11.batch-rename-extension",
    "jeff-hykin.polacode-2019",
    "meganrogge.template-string-converter",
    "mrmlnc.vscode-duplicate",
    "MS-vsliveshare.vsliveshare",
    "orta.vscode-jest",
    "quicktype.quicktype",
    "richie5um2.vscode-sort-json",
    "SonarSource.sonarlint-vscode",
    "streetsidesoftware.code-spell-checker",
    "usernamehw.errorlens",
    "yoavbls.pretty-ts-errors",
    "yzhang.markdown-all-in-one",
  ]
}
```

Mobile

```json
{
  "recommendations": [
    "aaron-bond.better-comments",
    "dart-code.dart-code",
    "dart-code.flutter",
    "eamodio.gitlens",
    "GitHub.copilot-chat",
    "GitHub.copilot",
    "JannisX11.batch-rename-extension",
    "jeff-hykin.polacode-2019",
    "mrmlnc.vscode-duplicate",
    "MS-vsliveshare.vsliveshare",
    "quicktype.quicktype",
    "richie5um2.vscode-sort-json",
    "SonarSource.sonarlint-vscode",
    "streetsidesoftware.code-spell-checker",
    "usernamehw.errorlens",
    "vscjava.vscode-gradle",
    "yzhang.markdown-all-in-one",
  ]
}
```

## Reference

- [GitHub Copilot in VS Code](https://code.visualstudio.com/docs/copilot/overview "https://code.visualstudio.com/docs/copilot/overview")
- [Getting started with GitHub Copilot](https://github.com/features/copilot/getting-started "https://github.com/features/copilot/getting-started")
- [Top 5 Serious Time Savers in VS Code](https://www.youtube.com/watch?v=MLvLiWueESY "https://www.youtube.com/watch?v=MLvLiWueESY*")
- [How I Set Up VS Code](https://www.youtube.com/watch?v=85q9FTdVyJs "https://www.youtube.com/watch?v=85q9FTdVyJs")
