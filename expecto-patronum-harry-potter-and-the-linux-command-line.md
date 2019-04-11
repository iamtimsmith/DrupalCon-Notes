# Expecto Patronum: Harry Potter and the Linux Command Line

> ## Professor Charles Jackson
>
> - Headmaster of Kerninghan House of Hogwarts School of Witchcraft, Wizardry, and Linux
> - Senior Web Manager @ Fujifilm
> - https://github.com/nightbeacons/Expecto_Patronum

## Expelliarmus

- Strange sounding, hard-to-pronounce words and phrases
- Amazingly powerful (and dangerous)
- Ancient seldom used texts authored
- No wizard knows it all
- Pretty scary to muggles and mortals

## Safety first

- Practice in a sandbox, scratch directory, or other non-critical directory
- Have a recovery plan
- Backups are your friend
- Anything that can blow up, will

## Where am I??

- It's easy to get lost
- How to get _un_-lost
- `pwd`: print working directory (where am i now?)
- `cd`: return to home directory
- Adding your location to system prompt

## Changing system prompt

- Use a prompt setting to change it.
- Can be found in git repo
- BASH = Born Again Shell
- Making it sticky
  - Add export setting to `.bashrc` file
  - Can be used to set up aliases

## Cat - "Contatenate"

- Display contentes of one or more text files
  ```
  cat settings.php
  cat *.html
  cat on.txt two.txt
  ```
- Concatenate files

```
cat *.log > all_in_one.log
```

## Redirection

- `>`
- `>>` append
- `|`
- Write the output of a command to a file:

## Spells for Linux

- add them to your `.bashrc` file

```
# Safety nets
alias rm='rm -i'
alias mv='mv -i'
alias cp='cp -i'
alias dc='cd' #FatFingers
```

## Bash Aliases

- History

  - Spells for linux, add them to your `.bashrc` file
  - Records and plays back your commands

  ```
  # Tools
  alias h='history'
  ```

- dos2unix: Convert MS-DOS line endings to Unix
- dircmp: Recursively compare two directories and show differences (like git status)
- dircmpdiff: Show differences in files (like git diff)

## Real Time logfile monitors

- First locate log files:
  - `cd /var/log/httpd`
  - `cd /var/log/nginx`
- `tail -f access_log`: Tail shows whats at the bottom and f says make it scrollable.
  - Displays real-time scrolling display of multiple files as they are being written
- `-i` means case insensitive

## Where is athat string?

- "Its either in a file or the database"
- How to search both:
  - `grep` Global search for Regular Expression and Print
    - Searches through one or more files for a string you give it
    - `grep` _string_ _filename_
  - `zgrep` and `bzgrep` files allow you to search compressed files
  - Recursive grep
    - Search for string in any file at or beneath the current directory
    - `grep -rin some_unique_string`
    - r recursive
    - i case insensitive
    - n print line numbers
  - `grep` Your MySQL DB
    - dumpXMLtables.php script
    - `grep drupal *.xml`
  - dumpXML and dircmp
    - Very useful for broken sites
    1. Run dumpXMLtables.php to create before snapshot
    1. In drupal, change _just one thing_
    1. Re-run dump
    1. Use `dircmp before_xml after_xml` to discover all changes

## Images and the CLI

- Manimpulating imgs
  - Using `convert` fro
  - If you can do it with photoship or gimpyou can do it faster with convert
  - Can even create gifs

## Advanced Spells

- Sending email
  - `mail`
  - `echo "This is the body of the email"`
  - can use `cat` command to pull info from file
  - `mail -a /path/to/filename.png` to send with attachment
- Sending a local file to remote system
  - `scp`
  - `scp myfile.txt harryp@hogwards.edu:/var/www`
  - Copy multiple files from remote system to yours
  - `scp ron@hogwards.edu:/tmp/images/*.jpg \/var/www/images`
  - Recursive version
    - Sends all files in a folder
    - `scp -rp spamfolder \ draco@hogwarts.edu:/var/www`

## Automating almost anything

- Using cron and the `crontab` command
  - `crontab -l` - list your cron table
  - `/dev/null` is linux for "go to the trash bin"
  - `crontab -e` - edit your cron table
    - Loads your cron table into your default editor (typically vim). Save file to activate.
- The five cron shceduling fields
  - field - allowed
  - minute - 0-59
  - hour - 0-23
  - day of month - 1-31
  - month - 1-12
- Security for cron
  - Create the file `/etc/cron.allow` (if it doesn't exist) and indicate the non-root users who should be alowed to use cron.
  - All other non-root users will be forbidden from using cron

## Defence against the Dark Arts

- Linux command-line tools provide fast and effective methods to isolate, identify, and analyze maliciousk activity on your site
- They can tell you how they got in, how long they were in, etc
- How did they get in?
  - Check your web server access logs for suspicious POSTs
  - `grep`, `zgrep`, and `gzgrep`
  - Next use the `find`command
  - use grep and variants to search logs
  - Other useful strings to search for:
    - wget
    - curl
    - pastebin.com
    - repo-linux.com
    - base64_decode
    - eval
    - %2fbin%2fsh
    - bin%2f/
- What did they leave behind?
  - From your notes, get timestamps of the first suspicious POST and then get a filesystem backup file that is a little bit older
  - Extract that backup file into a parallel direcotry
  - Use `dircomp` to find the differences between hacked site and backup
  - Note: Avoid using `grep -v` to filter out files that owuld be expected to change. The target could be there!
- No honor among Dementors or Thieves
  - After an intrusion, it is ommon to find a plain HTML Brag page left on the server
  - Hackers circulate links to ther brag pages for fun
  - Brag page often auto downloads copy of virus (often SWF-based) to any unfortunate enough to view the page
  - If you discover a file like this, thoroughly examine the HTML before even _thinking_ about viewing it in your browser

## Just for fun

- `figlet Drupal Rocks` creates ASCII art in CLI
- `fortune` Provides a random quote
- `cowsay` shows an ASCII image with a caption

## Learning more

- Get to know your friendly neighborhood IT team
- `--help` and `-h` and `-usage` flags
- `apropos` (a hidden gem)
- and don't forget google and bing
