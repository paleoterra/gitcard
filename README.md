# git card
git card is a command line tool to assist on tracking Kanban card numbers for git commit messages

Currently, two components are included in the project:
git-card  - command line app
prepare-commit-msg - git hook to inject git card number into commit messages

Instalation

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