---
Created: "2026-01-27"
Type: Zettle
Aliases:
References:
Links:
- [[Multiplexer]]
- [[Learning]]
- [[WezTerm]]
- [[Terminal]]
tags: [blog]
published: 2026-05-11 14:35
modified: 2026-05-11 14:35
---

Need to think about the practical usage of features mentioned.
	"platform independence"
	"session handling: detaching helps context switching and remote working"
# Possible term emulator:
- [x]  WezTerm
- [ ] ~~Cygwin + Tmux~~

### WezTerm
[[WezTerm]]

# Tmux
[Tmux by Ham](https://hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/)
I might give up using Tmux on Windows as the combination of `Cygwin + Tmux` has several dealbreaker: can't use `C-l cmd` to quickly perform open terminal here.
The file management in cygwin is also inconsistent with Windows, you have to go to places like `/cygdrive/c/ ..` to actually visiting Microsoft OS file system which makes fuzzy finder in nvim unpractical to use. 
	Using C-b as prefix key

## WezTerm + Tmux
	after wezterm ssh, using tmux new -s <NAME> to maintain multiplex
	setw -g mode-keys vi: Ctrl+B then [
	Shift + <mouse> : leave mouse operation to outer term.
### tmux.conf
	```
	set -g mouse on
	setw -g mode-keys vi
	set -g history-limit 100000
	# 告诉 tmux 使用 256 色
	set -g default-terminal "tmux-256color"

	# 开启 truecolor 支持（关键！）
	set -ga terminal-overrides ",xterm-256color:Tc"
	set -ga terminal-overrides ",wezterm:Tc"
	```
## Panes

	C-b %: split into left and right pane
	C-b <arrow key>: Switching pane 
	Ctrl-d : Closing pane <esc>
## Window
	C-b c: creating new window
	C-b p: previous window
	C-b n: next window
	C-b <number>: switch to <number> window

## Session Handling

###### if you done with your session, can either git rid of it by simply exiting all the panes inside or keep the session in the background for later use
	C-b d: detach current session
	C-b D: let tmux give you a choice which to detach
	$tmux ls: list current running session	
	$tmux attach  -t 0: connect to that session
	$tmux new -s database: give session name	
	$tmux rename-session -t 0 databse: rename session

## Moving on
###### some notes by author Ham vocke
	C-b z: make pane go full screen
    C-b C-<arrow key>: Resize pane in direction of 
	C-b ,: rename the current window
	C-b ?: see a list of available commands 