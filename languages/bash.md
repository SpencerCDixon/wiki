## Bash Tips/Quirks


### Variable Assignment
Never use spaces

```bash
VARIABLE=2   # yes
VARIABLE =2  # NO
```

Quoting variables
```bash
mv $VAR $VAR_new   # WRONG
mv $VAR ${VAR}_new # Right
```

### For Loops
Iterates over output of thing in backtics.  Alternatively, could use `{1..10}`
instead of using the seq program.
```bash
for i in `seq 1 10`
do
  echo "$1"
done
```

One liner: 
```bash
for i in `seq 1 10`; do echo "$1"; done
```

You can interpolate command out with either backticks or `$()`
```bash
OUTPUT=`command`
# or
OUTPUT=$(command)
```

### If Statements
Just always use [[ even though [ is valid.  

You can use `-e` to check for if file/dir exists.  To test before hand you can
use the `test` command.

```bash
if [[ -e /tmp/awesome.txt ]]; then
  echo "awesome"
fi

test -e /tmp/awesome.txt # wsee what it will do first
```

### Background Processes

You can put commands into backgounrd with `&`

```bash
long_running_command &
```

Then run `fg` to bring it to the foreground.  Fg takes a job id.  To get the job
id (and not PID for some odd reason) you run: `jobs`

### Random Tips

* use `set -e` at top of bash scripts and it will explode properly when a program returns a non 0 code.  Otherwise failures are silently ignored...  
* use `set -u` at top of files to make bash yell at you when using unset variables.  
* use `set -x` for debugging.  Will print every command before running.  
* ^ you can combine the above at top of files with: `set -eux` Safety first!  
* use a [shell linter to check your programs before running](https://www.shellcheck.net/)  
*



# Useful MACOS configuration:
```
# ==================================================================
# MACOS# ============================================================

======# KEYBOARDecho "Configuring key repeat"defaults write NSGlob




alDomain KeyRepeat -int 1defaults write NSGlobalDomain InitialKeyRepea
t -int 10# HIDDEN FILESecho "Configuring hidden files to show"defa




ults write com.apple.finder AppleShowAllFiles YESkillall Finder# MEN


U BARecho "Configuring menu bar to autohide"defaults write NSGlobalD


omain _HIHideMenuBar -bool truekillall Finder# DOCKecho "Configuri




ng dock to autohide"osascript <<EOD  tell application "System Events"

    if (get autohide of dock preferences) is false then      tell doc

    k preferences to set autohide to not autohide    end if  end tellEOD


# SCREENSHOTSecho "Configuring screenshots to save in Downloads"de




faults write com.apple.screencapture location ~/Downloadskillall Syste
mUIServer# CHROMEecho "Configuring incognito mode"defaults write c




om.google.chrome IncognitoModeAvailability -integer 1# =============


=====================================================echo "Done"

```
