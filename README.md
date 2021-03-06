# How To Set Up My Dotfiles

# Technique

I spend hours to try create a new bare repository to contains my dotfiles and make it easy to switch to others linux machine: 
- [The flow to create repository avoid "please tell me who you are" - StackOverFlow](https://stackoverflow.com/questions/11656761/git-please-tell-me-who-you-are-error)
- [What do you use to manage dotfiles? - HackerNews](https://news.ycombinator.com/item?id=11070797)
- [What is git --bare repository?](http://gitready.com/advanced/2009/02/01/push-to-only-bare-repositories.html)
- [error: failed to push some refs to 'https://github.com/<your-repo>/dotfiles'
](https://stackoverflow.com/questions/39399804/updates-were-rejected-because-the-tip-of-your-current-branch-is-behind-its-remot)
- Not succesfull with [The best way to store your dotfiles: A bare Git repository](https://www.atlassian.com/git/tutorials/dotfiles)
### Installation

Install the git repository with --bare option .

```sh
cd 
git init --bare $HOME/dotfiles
functions --erase config
git config --global user.email "usr-name-here@gmail.com"
git config --global user.name "git-name-hehre"
alias config='/usr/bin/git --git-dir=$HOME/dotfiles/ --work-tree=$HOME'
config config --local status.showUntrackedFiles no
echo "alias config='/usr/bin/git --git-dir=$HOME/.myconfg/ --work-tree=$HOME'" >> $HOME/.config/fish/config.fish
echo "alias config='/usr/bin/git --git-dir=$HOME/.myconfg/ --work-tree=$HOME'" >> $HOME/.zshrc
echo "alias config='/usr/bin/git --git-dir=$HOME/.myconfg/ --work-tree=$HOME'" >> $HOME/.bashrc

```

Using the alias as git command for add dotfiles to git repository...

```sh
config status
config add .bashrc
config commit -m "Add bashrc"
# move to your dotfiles to execute the following command
cd dotfiles
config fetch
config remote add origin https://github.com/git-user-name-here/dotfiles
config pull https://github.com/nhVietS/dotfiles master
config push --set-upstream origin master
# if  ! [rejected]        master -> master (non-fast-forward)
# error: failed to push some refs to 'https://github.com/usr/dotfiles'
# hint: Updates were rejected because the tip of your current branch is behind
# hint: its remote counterpart. Integrate the remote changes (e.g.
# hint: 'git pull ...') before pushing again.
# hint: See the 'Note about fast-forwards' in 'git push --help' for details.
# then use the -f option as below:
# config push -f --set-upstream origin master

```
