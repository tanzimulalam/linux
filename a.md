LINUX QUIZ - grep-friendly notes (Day 1a + Day 1b up to Permissions)
HOW TO USE: every question/command is ONE line with its answer at the end.
  grep -i 'newest at the bottom' a.md
  grep -i 'chmod 600' a.md
  grep -i 'ANSWER' a.md            (all question answers)
  grep -i 'CMD' a.md               (all commands)
  grep -i 'WHY' a.md               (all why/concept answers)
Tip: use -i (ignore case) and search a short, unusual phrase from the question.
Tip: narrow down by piping two greps:  grep -i gz a.md | grep -i wc
Tip: gz / compressed / decompress -> zcat, zless ; combined / total / all -> cat ... | wc -l

==================== Q - EASY ====================
Q01 | Which command prints the directory you are currently in? | ANSWER: pwd - print working directory
Q02 | What does cd with no argument do? | ANSWER: goes to home directory, same as cd ~
Q03 | Which takes you back to the previous directory you were in? | ANSWER: cd - (toggles between two directories)
Q04 | What does .. mean? | ANSWER: parent directory (. is this directory)
Q05 | Which flag makes ls -l show sizes as 4.0K / 12M / 1.3G (human readable)? | ANSWER: -h  ->  ls -lh
Q06 | Which shows hidden dotfiles like .bashrc? | ANSWER: ls -a
Q07 | Create an empty file called notes.md | ANSWER: touch notes.md (also updates timestamp if it exists)
Q08 | Copying a directory with cp requires which flag? | ANSWER: -r  ->  cp -r dir/ dest/
Q09 | mv does which two jobs? | ANSWER: move and rename
Q10 | Which deletes only empty directories? | ANSWER: rmdir
Q11 | Show the first 3 lines of big.csv | ANSWER: head -3 big.csv  (or head -n 3)
Q12 | Which counts the lines in a file? | ANSWER: wc -l  (-c bytes, -w words)
Q13 | Which shows the manual page for ls? | ANSWER: man ls
Q14 | In chmod, the numeric values of r, w, x are | ANSWER: r=4 w=2 x=1
Q15 | chmod 644 notes.md gives which permissions? | ANSWER: rw-r--r--

==================== Q - MEDIUM ====================
Q16 | Which lists files oldest first, newest at the bottom? | ANSWER: ls -ltr  (-t time, -r reverse)
Q17 | mkdir a/b/c fails when a/b does not exist. The fix? | ANSWER: mkdir -p a/b/c  (creates parents, no error if exists)
Q18 | One command to create exp08/raw, processed, figures, logs | ANSWER: mkdir -p exp08/{raw,processed,figures,logs}  (brace expansion)
Q19 | In ls -l, what is the very first character of drwxr-x---? | ANSWER: file type: - file, d directory, l symlink
Q20 | Which lists directories only, without descending into them? | ANSWER: ls -d */
Q21 | What does ? match in a glob? | ANSWER: exactly one character
Q22 | Which pattern matches sample1.txt, sample2.txt, sample3.txt only? | ANSWER: sample[123].txt
Q23 | sample[!0-9]*.txt matches names where the character after sample is | ANSWER: NOT a digit ([!...] negates)
Q24 | Why does ls * not show .bashrc? | ANSWER: * does not match a leading dot (use ls -a)
Q25 | head -c 200 big.bin prints the first 200 | ANSWER: bytes
Q26 | Skip a CSV header and print everything from line 2 onward | ANSWER: tail -n +2 f.csv  (-n 2 = last 2 lines)
Q27 | Watch a log file grow live | ANSWER: tail -f job.log  (Ctrl-c to stop)
Q28 | Which identifies a file's real format regardless of its extension? | ANSWER: file f  (reads magic bytes, ignores extension)
Q29 | A file has Windows line endings. Which command proves it? | ANSWER: cat -A f.csv  (shows ^M$ at line ends)
Q30 | In cat -A output, what does ^I mean? | ANSWER: tab  (^M = carriage return, $ = end of line)
Q31 | Find every .log file under findlab/ | ANSWER: find findlab -name "*.log"
Q32 | Which finds directories only? | ANSWER: find . -type d
Q33 | Find files bigger than 1 MB | ANSWER: find . -size +1M
Q34 | Which sorts 4.0K, 3.1M, 13M correctly? | ANSWER: sort -h  (human-readable sizes)

==================== Q - HARD ====================
Q35 | In what order does the shell process ls -l *.csv? | ANSWER: split -> expand -> find program -> fork/exec -> exit status
Q36 | ls *.zzz errors but echo *.zzz prints *.zzz. Why? | ANSWER: no match -> pattern passed through literally; error comes from ls, not the shell
Q37 | cp sandbox/my results.csv exp09/ gives two cannot stat errors because | ANSWER: word splitting; fix: cp "sandbox/my results.csv" exp09/
Q38 | cp -r template sandbox/t2 where t2 already exists results in | ANSWER: template/ goes INSIDE t2; to copy contents: cp -a template/. dest/
Q39 | Which is the correct tar invocation? | ANSWER: tar -czf  (-f takes a value so it must be last)
Q40 | Why does find . -name *.log (unquoted) misbehave? | ANSWER: shell expands it first; always quote: find . -name "*.log"
Q41 | Run wc -l on every .csv found, in one command | ANSWER: find . -name "*.csv" -exec wc -l {} +
Q42 | ls -l exp07 starts with total 16. That number is | ANSWER: disk blocks (1 KB) used by entries; use du -sh for size
Q43 | du -sh reports more than the sum of visible file sizes because | ANSWER: dirs take ~4 KB, a 7-byte file still uses a 4 KB block
Q44 | wc -l measurements.csv.gz gives a strange number. It is | ANSWER: meaningless; use zcat f.gz | wc -l
Q45 | Directory is drw-------. ls locked works but cat locked/treasure.txt fails. Why and minimum fix? | ANSWER: missing x (enter/traverse); chmod u+x locked
Q46 | Why can you still delete a read-only file? | ANSWER: needs w on the directory; protect with chmod a-w raw/
Q47 | Give group read + enter on shared/ recursively without making CSVs executable | ANSWER: chmod -R g+rX shared/  (capital X = directories only)
Q48 | What does chmod g+s project/ do? | ANSWER: setgid - new files inherit the group

==================== COMMANDS (CMD) ====================
CMD | pwd | show current directory
CMD | cd /path | go to absolute path
CMD | cd dir | go to relative path
CMD | cd .. | up one level
CMD | cd  (or cd ~) | go home
CMD | cd - | back to previous directory
CMD | ls | list names
CMD | ls -l | long listing: permissions, links, owner, group, size, date, name
CMD | ls -lh | long listing with human-readable sizes
CMD | ls -la | include hidden dotfiles
CMD | ls -ltr | sort by time, newest at the bottom
CMD | ls -lt | sort by time, newest at the top
CMD | ls -lS | largest file first
CMD | ls -d */ | directories only
CMD | ls -R | recursive listing
CMD | ls -ld dir | show the directory itself, not its contents
CMD | ls -a dir | wc -l | count entries including hidden (. and .. counted too)
CMD | mkdir dir | make one directory
CMD | mkdir -p a/b/c | make parents too, no error if exists
CMD | mkdir -p exp/{raw,processed,figures,logs} | make several subdirectories at once
CMD | touch f | create empty file or update timestamp
CMD | cp a b | copy file
CMD | cp -r src/ dst/ | copy directory recursively
CMD | cp -a src/ dst/ | copy preserving times, links, modes
CMD | cp -a template/. dest/ | copy CONTENTS of a directory into dest
CMD | cp -i a b | ask before overwrite
CMD | cp "my results.csv" dest/ | quote filenames with spaces
CMD | mv old new | rename
CMD | mv *.png figures/ | move many files into a directory
CMD | mv -n a dest/ | never overwrite
CMD | rm f | delete file (no trash can)
CMD | rm -r dir | delete directory and contents
CMD | rm -f f | force, no prompt, no error if missing
CMD | rm -i *.csv | prompt before each delete
CMD | rmdir dir | delete only an EMPTY directory
CMD | rm -- -weird-file.txt | -- ends options, delete file starting with dash
CMD | rm ./-weird-file.txt | other way to delete file starting with dash
CMD | man ls | manual page (q quit, / search)
CMD | man 5 passwd | manual section 5 (file formats); 1 commands, 3 library, 8 admin
CMD | ls --help | short usage summary
CMD | help cd | help for shell builtins (man cd does not work)
CMD | apropos compress | search manuals by keyword
CMD | type -a cmd | builtin, alias, function or file?
CMD | which -a python3 | which file(s) would run, PATH order
CMD | echo $SHELL | login shell
CMD | echo $0 | shell running right now
CMD | ps -p $$ | current shell process
CMD | cat /etc/shells | installed shells
CMD | echo pattern* | debug a glob before using it
CMD | history | tail -20 | last 20 commands
CMD | history | grep word | search history
CMD | !! | repeat last command
CMD | !$ | last argument of previous command
CMD | !ls | most recent command starting with ls
CMD | source ~/.bashrc | apply bashrc changes without logout
CMD | shopt -s globstar | enable ** recursive glob
CMD | shopt -s nullglob | glob with no match expands to nothing
CMD | file f | real file type from magic bytes
CMD | wc -l f | count lines
CMD | wc -c f | count bytes
CMD | wc -lwc f | lines, words, characters
CMD | stat f | inode, times, permissions, size
CMD | du -h f | disk usage of a file
CMD | head f | first 10 lines
CMD | head -n 3 f | first 3 lines
CMD | head -1 f | first line / column names of CSV
CMD | head -c 200 f | first 200 bytes
CMD | tail -n 20 f | last 20 lines
CMD | tail -1 f | last line
CMD | tail -n +2 f | everything except first line (skip header)
CMD | tail -f log | follow growing file
CMD | less f | page through file (space fwd, b back, /search, n next, g top, G bottom, q quit)
CMD | less -S f | no line wrapping
CMD | less -N f | line numbers
CMD | zless f.gz | page a compressed file
CMD | zcat f.gz | head -3 | first 3 lines of gz without decompressing to disk
CMD | zcat f.gz | wc -l | real line count of gz file
CMD | zcat logs/*.log.gz | wc -l | total lines in ALL .gz files combined, without decompressing to disk
CMD | zcat -f logs/*.log* | wc -l | total lines across .gz AND plain files combined
CMD | zcat f.gz | tail -3 | last 3 lines of gz without decompressing to disk
CMD | zcat f.gz | less | read a gz file without decompressing to disk
CMD | cat logs/*.log | wc -l | total lines in all plain .log files combined
CMD | wc -l logs/*.log | lines per file plus a total line at the bottom
CMD | find logs -name "*.log.gz" -exec zcat {} + | wc -l | total lines of all gz files in a whole tree combined
CMD | ls logs/*.log.gz | wc -l | how many .gz files (count files, not lines)
CMD | cat -A f | show invisible chars: ^M carriage return, ^I tab, $ end of line
CMD | dos2unix f.csv | fix Windows line endings
CMD | sed -i 's/\r$//' f.csv | fix Windows line endings with sed
CMD | cat a.txt b.txt > c.txt | concatenate files
CMD | find . -name "*.log" | find by name recursively
CMD | find . -iname "*.LOG" | case-insensitive name
CMD | find . -type f | files only
CMD | find . -type d | directories only
CMD | find . -size +1M | bigger than 1 MB
CMD | find . -mtime -2 | modified in last 2 days
CMD | find . -newermt 2025-01-01 | modified after date
CMD | find . -name "*.log" ! -newermt 2025-01-01 | modified BEFORE date
CMD | find . -type d -empty | empty directories
CMD | find . -type f -empty | empty files
CMD | find . -name "*.tmp" -delete | delete what you found
CMD | find . -name "*.csv" -exec wc -l {} + | run command on every found file
CMD | find dir -name "*.log" | wc -l | count matching files
CMD | find . -print0 | xargs -0 cmd | handle filenames with spaces
CMD | find . -xtype l | broken links
CMD | du -sh dir | total size of directory
CMD | du -sh * | sort -h | size of each entry, smallest to largest
CMD | du -h --max-depth=1 . | one level down
CMD | df -h | free space on the filesystem
CMD | quota -s | my quota
CMD | chmod u+x s.sh | add execute for owner (fix Permission denied on script)
CMD | chmod go-w f | remove write for group and others
CMD | chmod a+r f | add read for all
CMD | chmod 755 f | rwxr-xr-x
CMD | chmod 644 f | rw-r--r-- normal file
CMD | chmod 600 key | rw------- SSH private key
CMD | chmod 700 dir | rwx------ private
CMD | chmod -R g+rX dir | group read + enter, capital X = x on directories only
CMD | chmod -R g+rwX dir | group read, write, enter
CMD | chmod a-w raw/ | make raw data directory read-only
CMD | chmod -R a-w raw/ | make everything in raw read-only
CMD | chgrp grp dir | change group
CMD | chmod g+s dir | setgid, new files inherit group
CMD | umask 007 | new files get no permissions for others
CMD | id | who am I and my groups
CMD | ./script.sh | run script in current directory
CMD | tar -czf a.tgz d/ | create gzip archive (-f last)
CMD | tar -tzf a.tgz | list archive contents
CMD | tar -xzf a.tgz | extract archive

==================== GLOBS ====================
GLOB | * | any characters including none (not a leading dot, not /)
GLOB | ? | exactly one character
GLOB | [123] | one of 1, 2, 3
GLOB | [0-9] | one digit
GLOB | [!0-9] | NOT a digit
GLOB | {a,b} | brace expansion: a and b (generates text even if files do not exist)
GLOB | {01..12} | sequence 01 to 12
GLOB | ** | recursive (needs shopt -s globstar)
GLOB | sample01[0-9].txt | sample010.txt to sample019.txt
GLOB | sample*7.txt | numbers ending in 7

==================== KEYS ====================
KEY | Tab | complete name (twice = list options)
KEY | Ctrl-r | reverse search history
KEY | Ctrl-a | start of line
KEY | Ctrl-e | end of line
KEY | Ctrl-u | delete to start of line
KEY | Ctrl-k | delete to end of line
KEY | Ctrl-w | delete previous word
KEY | Ctrl-l | clear screen
KEY | Alt-. | insert last argument of previous command
KEY | Ctrl-c | interrupt running command
KEY | Ctrl-d | end of input

==================== WHY / CONCEPTS ====================
WHY | what happens when you press Enter | split words -> expand (braces, ~, $vars, $(cmd), wildcards) -> find program (builtin, function, alias, PATH) -> fork and exec -> collect exit status
WHY | does the program see the wildcard | NO, the shell expands before execution; the program sees the result
WHY | who expands globs | the SHELL, not the command
WHY | glob matches nothing | pattern passed through literally, no error from the shell
WHY | glob in subdirectory | globs match one directory level only, / never matched
WHY | glob vs regex | glob * any chars, ? one char, . literal dot; regex * zero or more of previous, ? zero or one, . any char
WHY | brace expansion in sh | bash feature; sh/dash prints run{01..03}.dat literally; use #!/usr/bin/env bash
WHY | man cd fails | cd is a shell builtin; use help cd; a program could not change your shell's directory
WHY | which -a shows two paths | PATH order decides which runs
WHY | terminal emulator | the window, draws characters
WHY | shell | program that reads, expands, executes (bash, zsh, fish, dash)
WHY | kernel | allocates CPU, memory, files
WHY | short vs long options | -l one dash one letter stackable; --sort=size two dashes readable
WHY | tar -cfz wrong | -f takes a value, must be last in the stack
WHY | absolute path | starts at /
WHY | relative path | starts from current directory
WHY | ~ | home directory, expanded by the shell
WHY | absolute vs relative when | absolute in configuration, relative in code
WHY | /home | small, backed up, quota
WHY | /scratch | huge, fast, NOT backed up, purged 30-90 days
WHY | /project | shared group space
WHY | $TMPDIR | node-local SSD, deleted when job ends
WHY | /etc | system configuration
WHY | /tmp | scratch, wiped on reboot
WHY | /var | logs, spool, caches
WHY | /bin /usr/bin | executables
WHY | /opt | add-on software
WHY | /proc /sys | kernel state as files
WHY | everything is a file | data, terminal /dev/tty, /proc/meminfo
WHY | total 16 in ls -l | disk blocks (1 KB) used by entries, not file count
WHY | mv instant | only the directory entry changes on same filesystem
WHY | cp mv overwrite | both overwrite silently by default
WHY | cp -r trap | if destination exists, source dir goes INSIDE it; use cp -a src/. dst/
WHY | rm safe habit | run ls with the same pattern first, then change ls to rm
WHY | rm -rf $DIR/* danger | if DIR unset becomes rm -rf /*
WHY | rm -rf . * | .* can match .. the parent
WHY | set -u | unset variable aborts script
WHY | filename with space | word splitting; quote it "my results.csv"
WHY | wc -l header | 4001 lines = 4000 data rows
WHY | no trailing newline | wc -l undercounts by one
WHY | cat huge file | dumps to terminal; use less/head/tail
WHY | vim huge file | loads whole file into RAM
WHY | ^M in cat -A | Windows CRLF line ending
WHY | wc -l on gz | meaningless, counts newline bytes in compressed binary
WHY | find quote pattern | unquoted *.log expanded by shell in current dir first
WHY | find paths must precede expression | unquoted glob matched several files
WHY | find output order | filesystem order, not sorted; pipe to sort
WHY | find test order | cheap tests (-type, -name) before expensive (-size)
WHY | du vs df | du walks the tree, df asks the filesystem
WHY | sort -h vs sort -n | -h understands K M G
WHY | du bigger than files | directories take 4 KB, files use whole blocks
WHY | du and quota disagree | file-count quota, or deleted file still open by a process
WHY | ls -l columns | type+permissions, links, owner, group, size, modified date, name
WHY | first char ls -l | - file, d directory, l symlink
WHY | r on file | read contents
WHY | w on file | modify contents
WHY | x on file | run as program
WHY | r on directory | list names
WHY | w on directory | create/delete entries
WHY | x on directory | enter / traverse (cd, access files inside)
WHY | permission classes | user (owner), group, other; first class that applies, not most generous
WHY | ---rw---- | owner cannot read even though group can write
WHY | octal digits | 7 rwx, 6 rw-, 5 r-x, 4 r--, 0 ---
WHY | Permission denied on own script | new script not executable; ls -l then chmod u+x
WHY | directory mode 600 | r lists names, no x so cannot cd or cat; chmod u+x
WHY | share a directory | need r and x on it plus x on every parent
WHY | delete read-only file | needs w on the directory, rm only asks as courtesy
WHY | protect raw data | chmod a-w raw/ on the directory
WHY | capital X | x only on directories (and already-executable files)
WHY | change owner | only root; chgrp only to groups you belong to
WHY | setgid g+s | new files inherit directory group
WHY | umask 007 | no permissions for others on new files
WHY | ls -ltr why | newest file at bottom next to prompt
WHY | cd - why | toggle between two directories
WHY | mkdir -p why | parents + safe to rerun
WHY | rmdir why | refuses non-empty, safety check
WHY | Tab completion | also an error check
WHY | alias in scripts | do not; scripts do not read .bashrc
WHY | history file | ~/.bash_history written when shell exits
