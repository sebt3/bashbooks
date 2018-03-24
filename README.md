# BashBooks
## Overview
BashBooks is a simple shell script that allow you to create "playbooks" in shell script. Each playbook can contain a set of activities.
An activity is a list of bash function that have to be run on a set of target.
You can define your own target lists easyly using a simple configuration file.

```
./bashbooks -B|--book BOOK [-t|--target TARGET] -a|--activity ACT [-l|--list] [-b|--begin MIN] [-e|--end MAX] [-o|--only ONLY] [-h|--help]
./bashbooks BOOK ACT [TARGET]
-B|--book BOOK           : Book to use
-t|--target TARGET       : Run book on target
-a|--activity ACT        : Select the activity to run
-l|--list                : List all available tasks
-b|--begin MIN           : Begin at that task
-e|--end MAX             : End at that task
-o|--only ONLY           : Only run this step
-h|--help                : Show this help text

Available values for BOOK (Book to use):
debian                   : A basic debian book
```

## Your first activity
```
upgrade.update() {
	apt-get -y update
}
upgrade.upgrade() {
	apt-get -y upgrade
}
upgrade() {
	task.add "$TARGET" upgrade.update		"Update apt repository"
	task.add "$TARGET" upgrade.upgrade		"Upgrade the system"
}
act.add.post upgrade "Upgrade the OS"
```
Please note that each `task` function run in a controled environnement where no value are available
