a
- `run` = `r`
	- can pass args like bash
	- can restart using this
- `file <executable>`
- step into via `step`
- step over via `next` = `n`
	- executes the current command and prints the next command.
- next assembly instruction via `nexti`
- `info registers`
- `x/i $pc` -> current instruction (I think)
- apropos
- `print` = `p`

to expand:
list = l -> surrounding code. Optional line # param
up and down the call stack.
display and undisplay (id). Scoped.
view the entire call stack -> backtrace = bt
watchpoint: watch x
delete <id> 
delete // deletes all of them
info breakpoints = i b
continue = c
reverse-next = rn
reverse-continue
reverse-step
target record-full
set var # change code in runtime.

**Questions**
- what if we try to step into a function which wasn't written by us and was pre-compiled without `-g` flag?
- how do we assign a breakpoint to a line within a function (as opposed to the function's start)?