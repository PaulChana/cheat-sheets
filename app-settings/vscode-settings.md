# VScode settings

```json

{
    "workbench.colorTheme": "Default Dark+",
    "window.openFoldersInNewWindow": "on",
    "files.associations": {
        "CMakeLists.txt": "cmake",
        "*.cmake": "cmake",
        ".clang-format": "yaml"
    },
    "[cmake]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "cheshirekow.cmake-format"
    },
    "[markdown]": {
        "editor.formatOnSave": true,
        "editor.formatOnPaste": true,
        "editor.defaultFormatter": "DavidAnson.vscode-markdownlint"
    },
    "editor.codeActionsOnSave": {
        "source.fixAll.markdownlint": "explicit"
    },
    "jupyter.runStartupCommands": [
        "%load_ext autoreload", "%autoreload 2"
    ],
    "editor.fontSize": 16,
    "cSpell.language": "en-GB",
    "cSpell.userWords": [
        "Allman",
        "Ampify",
        "cibuildwheel",
        "CLANGFORMAT",
        "codesign",
        "constexpr",
        "Dylib",
        "endfunction",
        "fastly",
        "Focusrite",
        "focusritegroup",
        "gitmodules",
        "juce",
        "lldb",
        "MSVC",
        "noexcept",
        "notarization",
        "notorization",
        "Novation",
        "nullopt",
        "nullptr",
        "objc",
        "powf",
        "sccache",
        "SDKROOT",
        "SRCROOT",
        "struct",
        "swiftformat",
        "swiftlint",
        "vocaster",
        "xcodebuild",
        "xcodeproj"
    ],
    "editor.minimap.enabled": false,
    "cmakeFormat.exePath": "/Users/paulchana/Library/Python/3.9/bin/cmake-format",
    "[javascript]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "editor.multiCursorModifier": "ctrlCmd",
    "editor.accessibilitySupport": "off",
    "[typescript]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[json]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "files.insertFinalNewline": true,
    "[typescriptreact]": {
        "editor.tabSize": 2,
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[html]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "terminal.integrated.env.osx": {
        "FIG_NEW_SESSION": "1"
    },
    "[python]": {
        "editor.formatOnType": true,
        "editor.defaultFormatter": "ms-python.black-formatter"
    },
    "shellformat.effectLanguages": [
        "shellscript",
        "dockerfile",
        "dotenv",
        "hosts",
        "jvmoptions",
        "ignore",
        "gitignore",
        "properties",
        "spring-boot-properties",
        "azcli",
        "bats"
    ],
    "shellformat.flag": "-i=4 -ci",
    "[shellscript]": {
        "editor.formatOnSave": true,
        "files.eol": "\n"
    },
    "circleci.hostUrl": "",
    "python.formatting.provider": "none",
    "jupyter.askForKernelRestart": false,
    "jupyter.widgetScriptSources": [
        "jsdelivr.com",
        "unpkg.com"
    ],
    "circleci.notifications.areActive": "no",
    "notebook.output.scrolling": true,
    "github.copilot.advanced": {},
    "telemetry.telemetryLevel": "off",
}


```