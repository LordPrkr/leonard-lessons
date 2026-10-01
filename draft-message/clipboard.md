# Clipboard

Choose an available clipboard tool for the user's interactive machine:

| Environment | Clipboard command |
| --- | --- |
| macOS | `pbcopy` |
| Linux / Wayland | `wl-copy` |
| Linux / X11 | `xclip -selection clipboard` or `xsel --clipboard --input` |
| Windows / PowerShell | `Set-Clipboard` with the complete message passed as a literal string |

Use a clipboard API if the environment provides one. Treat the message as data: pass it through standard input or a literal string, preserving Unicode and line breaks. For a shell command, use a quoted heredoc with a delimiter absent from the message, or a temporary UTF-8 file redirected into the command. Account for any newline added by the transport; remove temporary files afterward.

Confirm the tool reports success before saying “Copied.” If read-back is available, compare it with the approved text; read only the clipboard just written. On failure, or in a remote/headless session without confirmed access to the user's clipboard, explain the limitation and display the approved text for manual copying. Use existing tools rather than installing software or sending text to an external clipboard service.
