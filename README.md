Totally fair 😄 .zshrc becomes a junk drawer fast. Let’s wipe it clean and set up a fresh, minimal, working setup with exactly what you want:

✅ Powerlevel10k
✅ Autosuggestions (inline)
✅ Ctrl+R fuzzy searchable + scrollable history (fzf)
✅ Syntax highlighting
✅ Fast startup (instant prompt)

No extra noise.

⸻

0) Backup your current config (safety)

cp ~/.zshrc ~/.zshrc.backup.$(date +%Y%m%d-%H%M%S)
cp ~/.p10k.zsh ~/.p10k.zsh.backup.$(date +%Y%m%d-%H%M%S) 2>/dev/null


⸻

1) Install required packages (macOS)

brew install git fzf zsh-autosuggestions zsh-syntax-highlighting

Install Nerd Font (for icons in p10k):

brew install --cask font-meslo-lg-nerd-font

Set font in iTerm2:
iTerm2 → Settings → Profiles → Text → Font → MesloLGS Nerd Font
Restart iTerm2.

⸻

2) Install Oh My Zsh (fresh)

If already installed, skip this.

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"


⸻

3) Install Powerlevel10k (Oh My Zsh theme way)

git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k


⸻

4) Replace your .zshrc with a clean minimal one

This will remove all that “nonsense” and keep only what you need.

cat > ~/.zshrc <<'EOF'
# ---- Powerlevel10k Instant Prompt (keep at very top) ----
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

# ---- Oh My Zsh ----
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="powerlevel10k/powerlevel10k"
plugins=(git)

source $ZSH/oh-my-zsh.sh

# ---- History settings (better Ctrl+R experience) ----
HISTSIZE=100000
SAVEHIST=100000
setopt share_history
setopt hist_ignore_dups
setopt hist_reduce_blanks
setopt inc_append_history

# ---- Autosuggestions (inline from history) ----
source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh

# ---- Ctrl+R fuzzy searchable (scrollable) history via fzf ----
source <(fzf --zsh)

# ---- Syntax highlighting (must be last) ----
source $(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
EOF

Reload:

source ~/.zshrc


⸻

5) Configure Powerlevel10k (the nice prompt)

Run:

p10k configure

Recommended choices:
	•	Prompt style: Lean (fast + clean)
	•	Icons: Yes
	•	Transient prompt: Yes
	•	Instant prompt: Yes

⸻

6) Test your 3 main features

✅ Autosuggestions

Type:

git st

You should see gray suggestion → press → to accept.

✅ Ctrl+R scrollable search

Press:
	•	Ctrl + R
Type any keyword and you should see a scrollable list (use arrow keys).

✅ Powerlevel10k

You should see:
	•	path with ~
	•	git branch when inside a repo
	•	nice symbols/icons

⸻

If you still see “plugin not found”

That happens only if you added zsh-autosuggestions inside plugins=(...).
In our clean setup we did NOT do that — we load it via source ... from Homebrew, so you won’t get that error.

⸻

Want it EXACTLY like mac Terminal (but with p10k)?

Tell me which look you want:
	1.	Minimal (only path + git)
	2.	Full (time, status, node/python, execution time, etc.)

Reply: 1 or 2 and I’ll give you the best p10k choices + a tuned .p10k.zsh.
