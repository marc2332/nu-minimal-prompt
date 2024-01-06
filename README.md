```nushell
$env.PROMPT_COMMAND = { ||
    let cwd = $env.PWD | path basename 
    let name = $env.USERNAME
    let branch = do { git name-rev --name-only HEAD } | complete
    let git_status = if $branch.exit_code == 0 and $branch.stdout != "" {
        $"(ansi yellow) | ($branch.stdout)"
    } else {
        " "
    }
    $"(ansi magenta)($name) (ansi yellow)➜ (ansi blue)($cwd)($git_status)"
}

$env.PROMPT_COMMAND_RIGHT = { ||
    ""
}
```