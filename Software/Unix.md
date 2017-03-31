# Tips and tricks on using Unix systems

## Shortcuts in the terminal

Suppose you want a quick shortcut to get to your workspace and source it. Create an alias command and add it to your `.bashrc` file. For example suppose I want a new command `goAndre` we will add a line to `~/.bashrc` such as

    alias goAndre="cd ~/andre_ws; source devel/setup.bash"

## Terminal multiplexing

If you're on a remote system through ssh and you want multiple terminals or if you want multiple terminals in the same window on a local system, you can use `tmux` to create splits and windows. Install by running

    sudo apt install tmux

A good [cheatsheet](https://gist.github.com/MohamedAlaa/2961058) is available. However here are the basic shortcuts you need to know:

* Before running any commands below you must first hit the prefix command `ctrl + b`.
* `%` Split window vertically
* `"` Split window horizontally
* `arrowkey` Move to a split in that direction
* `x` Kill a pane
* `c` Create a window
* `n` Go to next window
* `&` Kill window (**and all the panes in it**)

If you lost connection to a robot but it stayed on (e.g. you had to reboot your local machine), you can regain control of your tmux session by attaching to it. e.g.

    ssh asctec@firefly_green
    tmux
    # do stuff and the lose connection
    ssh asctec@firefly_green
    tmux a
    # regain the previous session

If you temporarily lost connection to a robot (e.g. had to unplug and replug and ethernet cable) you'll notice that your tmux session will simply be regained (this is the main advantage of `tmux` over `screen`).

## Saving tmux configurations

Suppose you have a multi-terminal setup with multiple commands to execute in each terminal and you want to setup everything and run all your commands using a single command. Use [tmuxp](https://github.com/tony/tmuxp).

TODO add example config used in the Husky for Activeslam.
