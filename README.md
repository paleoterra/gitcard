# git card
git card is a command line tool to assist on tracking Kanban card numbers for git commit messages

Currently, two components are included in the project:
git-card  - command line app
prepare-commit-msg - git hook to inject git card number into commit messages

#Installation:

set git-card to be executable
install git-card into a bin directory

set prepare-commit-msg to be executable
install into .git/hooks or into a globel git hooks path

Examples:

//set card number
git card 1

git commit "initial commit"

the first commit will be 
"1 - initial commit"

*******
update your gitingore file (preferably global gitignore) to exclude 
".CARD_NUMBER"

The above file tracks your current card and should not be included in a repo (unless you really want to)


# Install into Powerlevel10k

Powerlevel10k is a theme that allows you to configure your command line.

By editing Powerlevel10k's theme, you can display the current card.

Start by installing Powerlevel10k if you haven't already
https://github.com/romkatv/powerlevel10k

Edit the .p10k.zsh in you home directory:

In the left prompt elements section, add a custom_gitcard line:

    typeset -g POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(
        os_icon                 # os identifier
        custom_gitcard
        dir                     # current directory
        vcs                     # git status
    )

Somewhere below the above section, add the following function:

    function cardcontent() {
    REPOPATH=$(git rev-parse --show-toplevel 2> /dev/null)
    CARDPATH="${REPOPATH}/.CARD_NUMBER"
    if [ -z "${REPOPATH}" ]; then
        echo ""
    elif [ -f ${CARDPATH} ]; then
        CARDNUMBER=$(cat $CARDPATH)
        echo $CARDNUMBER
    else
        echo "NO CARD"
    fi
    }

The above function will read the .CARD_NUMBER file if present and display the card number.

If you are not in a git project, it will set an empty string (and will not show the card on the command line)
If you do not wish to show "NO CARD" if you are in a repo, but don't currently have a card, replace "NO CARD" with ""

After the function, add the following:

  typeset -g POWERLEVEL9K_CUSTOM_GITCARD=cardcontent
  typeset -g POWERLEVEL9K_CUSTOM_GITCARD_BACKGROUND=black
  typeset -g POWERLEVEL9K_CUSTOM_GITCARD_FOREGROUND=green

the first line calls the function above.
The other lines set the apperance of the card number on the command line: customize as needd.


