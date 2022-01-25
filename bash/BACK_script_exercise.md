# The BACK Script
### Back script intro

- pwd: `/a/b/c/d/e`
    - back 4 → pwd: `/a`

## Subshells

- 터미널을 띄운 뒤 `bash`를 실행하면 새로운 bash 터미널이 실행되며 `exit`하면 다시 현재의 터미널로 돌아온다.
- 스크립트 첫째줄에 쓰는 `#! /bin/bash`도 스크립트 실행시 subshell을 실행 후 종료하는 것이다.

```bash
#! /bin/bash

echo "hello"

exit   ## exit the subshell

echo "last line" ## Will it be executed in the current shell? -- NO. exit 이전까지만 실행되며 current shell로 빠져나온다.
```

## The Source Command

- `source script.sh` == `. script.sh`
    - 스크립트가 current shell에서 (not subshell) 실행되도록 함
    - 스크립트에서 지정한 변수가 현재 터미널에서도 저장됨

## The Type Command

1. executable program
    - `type cat` → cat is /bin/cat
    - `type [script.sh](http://script.sh)` → script.sh is /file_path/script.sh
2. shell builtins
    - `type cd` → cd is a shell builtin
3. alias
    - `type lf` → lf is an alias for `ls -Flha`

## Alias in Bash

- `alias ll='ls -l'`
- check alias
    - `type ll`
    - `alias ll`
- alias list
    - `alias`
- remove alias
    - `unalias ll`
- set alias permanently → add to `.profile`

## Command Substitution - `$()`

- `which cd` → `/usr/bin/cd`
- `ls -l /usr/bin/cd`

  ⇒ `ls -l $(which cd)`

---

## Parameter in bash

- Access `N`th parameter: `$N`
    - 12th parameter →  `${12}`
    - `$12` = `$1` + `2`
- How many parameters you have? → `$#`
- All parameters
    - `$@`: 모든 파라미터를 iterable하게 넘김
    - `$*`: 모든 파라미터를 묶어서 하나로 넘김(non-iterable)
