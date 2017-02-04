# Terminal

## Base Shortcuts

`<Ctrl>l` Clear the Terminal.

`<Ctrl>c` Kill the current process.

`<Ctrl>d` (Process Active) Send [End-of-File] to the current process.

`<Ctrl>d` (Prompt) Log out from the current shell.

`<Ctrl>s` Stop the transfer to the terminal.

`<Ctrl>q` Resume the transfer to the terminal. (Try if your terminal stops responding)

`<Ctrl>z` Send the current process to the background.

`<Tab>` Autocomplete the command if there is only one option, or else show all the available options.

`<ArrowUp>` Scroll and edit the command history. Press <Enter> to execute.

## Base Commands

`open` opens a file, directory, URL... just as if you had double-clicked the file's icon.

### Help
`<command> --help |more` Display a brief help on a command (works with most commands).

`man <topic>` Display the contents of the system manual pages (help) on the topic.

`apropos <topic>` Give me the list of the commands that have something to to do with my topic.

### Exit

`exit` Exit from the current shell. Alt `logout` has same effect.

`reset` Restore a screwed-up terminal.

### Where

`uname -a` All info on your machine.

`hostname` Print the name of the local host.

`tty` Print the name of the terminal in which you are typing this command.

`pwd` Print working directory.

### Who

`whoami` Print the current user login name.

`id <username>` Print user id (uid) and his/her group id (gid).

`who` Determine the users logged on the machine.

`finger <username>` System info about a user.

`last` Show listing of users last logged-in on your system.

### When

`date` Print or change the operating system date and time.

`time <command>` Determine the amount of time that it takes for a process to complete and additional info.

`uptime` Show the amount of time since the last reboot.

`cal <m> <y>` Show a calendar for the specified month and year.

### Environment

`set | less` Show the current user environment.

`echo $PATH` Show the content of the environment variable "PATH". This command can be used to show other environment variables as well.

### Jobs

`jobs` list the jobs in the background.

`fg %n` Bring back the nth jobs to the foreground.

### History

`history | less` Show the last commands executed from the command line on the current account.

### Processes

`ps` List the processes currently run by the current user.

`ps axu | less` List all the processes currently running, even those without the controlling terminal, together with the name of the user that owns each process.

`top` Keep listing the currently running processes, sorted by cpu usage (top users first).

`lsof -p <pid>`	List paths that a process id has open.

`lsof <path>`	List processes that have specified path open.

### Disk

`df -h` (=disk free) Print disk info about all the filesystems.

`du / -bh | less` (=disk usage) Print detailed disk usage for each subdirectory starting at the "/" (root) directory.


# Atom

`Cmd+Shift+P` Bring the command prompt

`ctrl-shift-m` Start the markdown preview


## Atom Commands





# Homebrew
### Intall / Uninstall

To install Homebrew, paste the command below in a terminal prompt.
Note that `ruby` must be in your path, formulas are just simple ruby scripts!
```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

To uninstall Homebrew, paste the command below in a terminal prompt ...

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
```

... or download the [uninstall script](https://raw.githubusercontent.com/Homebrew/install/master/uninstall)
and run `./uninstall --help` to view more uninstall options.

Create list of install command based on the current state of your brewery

```bash
brew list | sed -e 's/^/brew install /' > osx-brew-formula-install.sh
```

### Updating
Updating the brew system itself

    brew update

Find out what formulas are out dated

    brew outdated

Upgrade everything ...

    brew upgrade

.. or upgrade a specific formula

    brew upgrade $FORMULA

### Adding / Removing formulas

To add a formula

    brew install $FORMULA

To remove a formula

    brew uninstall $FORMULA

If you do not uninstall all of the versions that Homebrew has installed, Homebrew will continue to attempt to install the newest version it knows about when you do (`brew upgrade --all`).

To remove a formula entirely, you may do

    brew uninstall formula_name --force

### Preventing automatic updates
To stop something from being updated/upgraded

    brew pin $FORMULA

To allow that formulae to update again

    brew unpin $FORMULA

### Clean up the brewery
By default, Homebrew does not uninstall old versions of a formula, so
over time you will accumulate old versions.

Check what would be cleaned up

    brew cleanup -n

Clean up everything at once ...

    brew cleanup

or remove a specific old formula

    brew cleanup $FORMULA
