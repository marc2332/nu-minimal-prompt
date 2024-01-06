past this in your `config.nu`:

```nushell
$env.PROMPT_COMMAND = { ||
    let cwd = $env.PWD | path basename 
    let name = $env.USERNAME
    let branch = do { git name-rev --name-only HEAD } | complete
    let git_status = if $branch.exit_code == 0 and $branch.stdout != "" {
        $"(ansi white) ➜(ansi yellow) \u{eafe} ($branch.stdout)"
    } else {
        "\n"
    }
    $"(ansi magenta)($name) (ansi white)➜ (ansi blue)($cwd)($git_status)\n"
}

$env.PROMPT_COMMAND_RIGHT = { ||
    ""
}
```