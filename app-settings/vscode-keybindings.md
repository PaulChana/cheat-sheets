# VScode keybindings

```json

// Place your key bindings in this file to override the defaultsauto[]
[
    {
        "key": "alt",
        "command": "workbench.action.toggleMultiCursorModifier"
    },
    {
        "key": "f7",
        "command": "workbench.action.debug.stepInto",
        "when": "debugState != 'inactive'"
    },
    {
        "key": "f11",
        "command": "-workbench.action.debug.stepInto",
        "when": "debugState != 'inactive'"
    },
    {
        "key": "f6",
        "command": "workbench.action.debug.stepOver",
        "when": "debugState == 'stopped'"
    },
    {
        "key": "f10",
        "command": "-workbench.action.debug.stepOver",
        "when": "debugState == 'stopped'"
    },
    {
        "key": "f8",
        "command": "workbench.action.debug.stepOut",
        "when": "debugState == 'stopped'"
    },
    {
        "key": "shift+f11",
        "command": "-workbench.action.debug.stepOut",
        "when": "debugState == 'stopped'"
    },
    {
        "key": "ctrl+cmd+j",
        "command": "editor.action.revealDefinition",
        "when": "editorHasDefinitionProvider && editorTextFocus && !isInEmbeddedEditor"
    },
    {
        "key": "f12",
        "command": "-editor.action.revealDefinition",
        "when": "editorHasDefinitionProvider && editorTextFocus && !isInEmbeddedEditor"
    },
    {
        "key": "ctrl+cmd+left",
        "command": "-workbench.action.terminal.resizePaneLeft",
        "when": "terminalFocus && terminalHasBeenCreated || terminalFocus && terminalProcessSupported"
    },
    {
        "key": "ctrl+cmd+left",
        "command": "-workbench.action.moveEditorToPreviousGroup"
    },
    {
        "key": "ctrl+cmd+left",
        "command": "workbench.action.navigateBack",
        "when": "canNavigateBack"
    },
    {
        "key": "ctrl+-",
        "command": "-workbench.action.navigateBack",
        "when": "canNavigateBack"
    },
    {
        "key": "ctrl+shift+cmd+right",
        "command": "-editor.action.smartSelect.expand",
        "when": "editorTextFocus"
    },
    {
        "key": "ctrl+cmd+right",
        "command": "-workbench.action.terminal.resizePaneRight",
        "when": "terminalFocus && terminalHasBeenCreated || terminalFocus && terminalProcessSupported"
    },
    {
        "key": "ctrl+shift+cmd+right",
        "command": "workbench.action.moveEditorToNextGroup"
    },
    {
        "key": "ctrl+cmd+right",
        "command": "-workbench.action.moveEditorToNextGroup"
    },
    {
        "key": "ctrl+cmd+right",
        "command": "workbench.action.navigateForward",
        "when": "canNavigateForward"
    },
    {
        "key": "ctrl+shift+-",
        "command": "-workbench.action.navigateForward",
        "when": "canNavigateForward"
    }
]



```

#vscode