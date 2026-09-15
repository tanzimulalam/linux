LINUX QUIZ Q&A - one line per question:   Q: question | A: answer | K: keywords
USE:  cat a.md | grep -i 'word'          e.g.  cat a.md | grep -i 'gz'
MORE: cat a.md | grep -i 'word1' | grep -i 'word2'     (lines with BOTH words)
TIP:  search ONE short word from the question (gz, empty, newest, hidden, execute, size, header, space...), always use -i

===== SHELL: WHAT HAPPENS WHEN YOU PRESS ENTER =====
Q: What happens when you press Enter on a command line (order of steps)? | A: 1 split into words on whitespace, 2 expand (braces, ~, $variables, $(commands), wildcards), 3 find program (builtin, function, alias, else PATH), 4 fork and execute, 5 wait and collect exit status | K: enter steps order shell process split expand execute
Q: In what order does the shell expand things? | A: braces {} -> tilde ~ -> $variables -> $(commands) -> wildcards/globs | K: expansion order brace tilde variable command substitution glob
Q: Does the program (ls, cp) see the wildcard you typed? | A: No. The shell expands it first; the program only sees the expanded result (list of filenames) | K: program sees expanded glob wildcard shell expands
Q: Who expands wildcards/globs, the shell or the command? | A: The SHELL, before the command runs | K: glob wildcard expanded by shell not program
Q: What is a terminal emulator? | A: The window (GNOME Terminal, iTerm2, Windows Terminal); it only draws characters, knows nothing about Linux | K: terminal emulator window
Q: What is the shell? | A: The program that reads your line, expands it and executes it (bash, zsh, fish, dash); a program that launches other programs | K: shell bash zsh fish dash definition
Q: What are utilities? | A: The actual programs like ls, grep, python - ordinary executables in ordinary directories | K: utilities programs executables
Q: What is the kernel? | A: Allocates CPU, memory and files; you never talk to it directly | K: kernel cpu memory
Q: Why is the shell useful for research / a PhD student? | A: remote machines have no GUI, reproducibility (command is a record), scale (1 or 100000 files), composability (pipelines), speed on large text, every tool has a CLI | K: why shell reasons reproducibility scale remote

===== WHICH SHELL =====
Q: Show your login shell | A: echo $SHELL | K: login shell which shell
Q: Show the shell interpreting this line right now | A: echo $0 | K: current shell running now
Q: Show the actual shell process | A: ps -p $$ | K: shell process pid
Q: Show bash version | A: bash --version | K: bash version
Q: List shells installed on the machine | A: cat /etc/shells | K: installed shells list
Q: Which shell is default on HPC clusters? On macOS? | A: bash on HPC; zsh on macOS | K: default shell hpc cluster mac
Q: What is sh? | A: The POSIX subset - portable but missing arrays and [[ ]] (often dash on Debian/Ubuntu) | K: sh posix dash
Q: bash -c 'echo run{01..03}.dat' vs sh -c 'echo run{01..03}.dat' output? | A: bash: run01.dat run02.dat run03.dat ; sh: run{01..03}.dat (literal, no error - brace expansion is a bash feature) | K: brace expansion bash sh difference run01
Q: Why use #!/usr/bin/env bash instead of #!/bin/sh? | A: sh/dash lacks bash features like brace expansion and silently does the wrong thing | K: shebang env bash bin sh

===== COMMAND SHAPE AND OPTIONS =====
Q: Name the parts of: ls -l -h --sort=size /scratch/project/raw | A: ls = command name; -l, -h = short options; --sort=size = long option with a value; /scratch/project/raw = argument (operand) | K: anatomy parts command option argument operand
Q: Short option vs long option? | A: short: one dash one letter, stackable (-lh = -l -h); long: two dashes, readable (--sort=size) | K: short long option dash
Q: Are ls -lh, ls -l -h, ls -hl the same? | A: Yes - short options stack and order does not matter | K: stacking options combine
Q: Is tar -czf a.tgz d/ or tar -cfz a.tgz d/ correct? | A: tar -czf is correct. In -cfz, -f takes the value "z" as the filename. An option that takes a value must come LAST in a stack | K: tar option value last f wrong mistake
Q: Delete a file named -weird-file.txt (starts with a dash) | A: rm -- -weird-file.txt   OR   rm ./-weird-file.txt | K: dash filename starts with hyphen double dash end of options
Q: What does -- mean in a command? | A: End of options; everything after is a filename/argument | K: double dash end options
Q: Short or long options in scripts? | A: Long options in scripts (readable), short options interactively | K: scripts long options readable
Q: Does the order of options matter? Order of operands? | A: Options usually no; operands yes (cp SOURCE DEST, not reverse) | K: order operands source destination
Q: Why do filenames with spaces cause trouble? | A: Everything is separated by whitespace, so a space splits one name into two arguments | K: spaces filename whitespace splitting

===== HELP =====
Q: Open the manual page for ls | A: man ls   (q quit, / search) | K: manual man page help
Q: Open section 5 of the manual for passwd | A: man 5 passwd | K: man section 5 file format
Q: What are the manual sections that matter? | A: 1 commands, 3 library calls, 5 file formats, 8 admin commands | K: man sections 1 3 5 8
Q: Show short usage summary for ls | A: ls --help | K: help flag usage summary
Q: Get help for a shell builtin like cd | A: help cd | K: builtin help cd
Q: Why does man cd fail but help cd works? | A: cd is a shell builtin, not a program (a separate program could not change your shell's directory) | K: man cd fails builtin
Q: Search manual descriptions by keyword (e.g. compress) | A: apropos compress | K: apropos search keyword manual
Q: Is python3 a builtin, alias, function or file? | A: type -a python3 | K: type builtin alias function
Q: Which file(s) would run for python3? | A: which -a python3 | K: which path location executable
Q: which -a python3 shows two paths. What decides which one runs? | A: PATH order (first one in PATH runs) | K: which two paths PATH order wrong python
Q: What does type -a cd print? | A: cd is a shell builtin | K: type cd builtin
Q: What part of a man page should you read first? | A: EXAMPLES section at the bottom | K: man examples tutorial
Q: Tools that give examples instead of specifications? | A: tldr and cheat | K: tldr cheat examples

===== FILESYSTEM =====
Q: What is / ? | A: The root of everything (one tree, no drive letters) | K: root slash
Q: What is in /home? | A: User home directories | K: home directory
Q: What is in /bin and /usr/bin? | A: Executables | K: bin executables
Q: What is in /etc? | A: System configuration | K: etc config configuration
Q: What is /tmp? | A: Scratch space, wiped on reboot | K: tmp temporary
Q: What is in /var? | A: Logs, spool, caches | K: var logs
Q: What is /opt? | A: Add-on software | K: opt software
Q: What are /proc and /sys? | A: Kernel state shown as files | K: proc sys kernel
Q: Where does a USB stick or second disk appear? | A: As a directory inside the single tree (not D: or E:) | K: usb disk mount drive letter
Q: What does "everything is a file" mean? | A: Data, your terminal (/dev/tty), kernel memory info (/proc/meminfo) are all files, so same tools work on everything | K: everything is a file dev tty meminfo
Q: /home on a cluster? | A: Small, backed up, quota'd - code and configuration | K: home cluster backed up quota
Q: /scratch or /lustre on a cluster? | A: Huge, fast, NOT backed up, purged after 30-90 days - working data | K: scratch lustre purge not backed up
Q: /project on a cluster? | A: Shared group space, medium size, usually backed up | K: project shared group
Q: $TMPDIR on a cluster? | A: Node-local SSD, fastest, deleted when your job ends | K: tmpdir node local ssd
Q: Check disk space of your filesystems | A: df -h | K: df disk free space filesystem

===== PATHS =====
Q: What is an absolute path? | A: Starts at / e.g. /scratch/mgc/exp07/raw/run01.dat | K: absolute path
Q: What is a relative path? | A: Starts where you are e.g. raw/run01.dat | K: relative path
Q: What does . mean? | A: This (current) directory | K: dot current directory
Q: What does .. mean? | A: The parent directory (one level up) | K: dotdot parent up
Q: What does ./configure mean? | A: Run configure explicitly from this directory | K: dot slash current
Q: What does ~ mean? | A: Your home directory (expanded by the shell) | K: tilde home
Q: What does ~alice mean? | A: alice's home directory | K: tilde user home other
Q: Which command shows . and .. entries? | A: ls -a | K: show dot dotdot hidden
Q: When to use absolute vs relative paths? | A: Absolute paths in configuration; relative paths in code (portable) | K: absolute relative when rule of thumb
Q: Why never hard-code /home/yourname in published code? | A: It breaks on anyone else's machine (reviewer) - use relative paths | K: hard code home path portable

===== NAVIGATION =====
Q: Where am I? / print current directory | A: pwd | K: current directory where print working
Q: Go to /scratch/mgc | A: cd /scratch/mgc | K: change directory absolute
Q: Go into exp07/raw from here | A: cd exp07/raw | K: change directory relative
Q: Go up one directory | A: cd .. | K: up one level parent
Q: Go up two directories | A: cd ../.. | K: up two levels
Q: Go to home directory | A: cd   (or cd ~) | K: home go back home lost
Q: Go back to the previous directory | A: cd - | K: previous directory back toggle
Q: Get from ~/linux-lab into exp07/logs and back using two commands total | A: cd exp07/logs   then   cd - | K: two commands back and forth logs
Q: Without cd, list exp07/processed/ while standing in exp07/logs/ | A: ls ../processed | K: without cd list other directory relative
Q: Why prefer cd - over cd ../.. to go back? | A: cd - still works if you ended up somewhere unexpected | K: cd dash vs dotdot

===== LS =====
Q: List names in the current directory | A: ls | K: list files
Q: Long listing (permissions, owner, size, date) | A: ls -l | K: long listing details
Q: Long listing with human-readable sizes (4.0K, 12M, 1.3G) | A: ls -lh | K: human readable size
Q: Show hidden files / dotfiles (.bashrc, .git) | A: ls -la   (or ls -a) | K: hidden dotfiles all
Q: List by time, newest at the bottom | A: ls -ltr | K: newest bottom time reverse
Q: List by time, newest at the top | A: ls -lt | K: newest top time
Q: Which file in exp07/raw/instrument_a/ was modified most recently? One command | A: ls -ltr exp07/raw/instrument_a   (newest is the LAST line) | K: most recently modified newest latest file
Q: List largest files first | A: ls -lS | K: largest biggest size sort
Q: List directories only (not their contents) | A: ls -d */ | K: directories only
Q: List recursively into subdirectories | A: ls -R | K: recursive subdirectories
Q: Show a directory's own permissions (not its contents) | A: ls -ld dirname | K: directory itself permissions ld
Q: How many files and directories are in exp07/, including hidden ones? | A: ls -a exp07 | wc -l   (. and .. are counted too) | K: count files including hidden how many entries
Q: Count files (not hidden) in a directory | A: ls dir | wc -l | K: count files number
Q: ls -l exp07 starts with "total 16". What is it? | A: Disk space used by the directory's entries in 1 KB blocks - NOT a file count, NOT size of files inside (use du -sh for size) | K: total 16 ls blocks
Q: Why ls -ltr instead of ls -lt? | A: -r puts newest at the bottom next to your prompt, no scrolling in a directory with 400 files | K: why ltr reverse
Q: Why doesn't alphabetical ls show which run finished last? | A: Names don't reflect time; sort by time with ls -ltr | K: alphabetical name order time
Q: What does -d do in ls? | A: Stops ls from descending into directories it is given | K: ls d flag
Q: Useful alias for ls | A: alias ll='ls -lhtr' | K: alias ll

===== MKDIR / TOUCH =====
Q: Create one directory called results | A: mkdir results | K: make directory create folder
Q: Create exp08/raw when exp08 does not exist | A: mkdir -p exp08/raw | K: parents nested create p
Q: Create 4 subdirectories raw processed figures logs in exp08 with one command | A: mkdir -p exp08/{raw,processed,figures,logs} | K: several subdirectories braces at once
Q: Create sandbox/exp09/ with subdirectories raw, processed, figures, logs using one command | A: mkdir -p sandbox/exp09/{raw,processed,figures,logs} | K: exp09 subdirectories one command
Q: What does mkdir -p do besides making parents? | A: No error if the directory already exists - safe in scripts that are rerun | K: p exists no error rerun
Q: What happens to mkdir a/b/c without -p if a/b doesn't exist? | A: It fails | K: mkdir fails without p
Q: Does mkdir see the braces in {raw,processed}? | A: No - the shell expands them into separate words before mkdir runs | K: braces expanded shell mkdir
Q: Create an empty file notes.md / update its timestamp | A: touch notes.md | K: empty file create timestamp touch
Q: Create 12 files run01.dat to run12.dat | A: touch run{01..12}.dat | K: many files sequence create

===== CP / MV =====
Q: Copy a file params.yaml to a backup | A: cp params.yaml params.yaml.bak | K: copy file backup
Q: Copy a directory template/ to exp08/ | A: cp -r template/ exp08/ | K: copy directory recursive r
Q: Copy a directory preserving times, links, permissions | A: cp -a source/ backup/ | K: copy preserve archive a
Q: Copy and ask before overwriting | A: cp -i a.txt b.txt | K: prompt overwrite interactive
Q: Copy the CONTENTS of template/ into sandbox/exp09/ (so exp09/README.md exists, not exp09/template/README.md) | A: cp -a template/. sandbox/exp09/ | K: copy contents into directory slash dot
Q: cp -r template sandbox/t1 where t1 does NOT exist - result? | A: t1 is created with template's contents inside (README.md config src) | K: cp trap not exist
Q: cp -r template sandbox/t2 where t2 ALREADY exists - result? | A: template/ directory itself goes inside t2 (sandbox/t2/template) | K: cp trap exists inside
Q: Copy "my results.csv" (space in name) into exp09/ | A: cp "sandbox/my results.csv" sandbox/exp09/ | K: space filename quotes copy
Q: What does cp sandbox/my results.csv exp09/ (unquoted) do? | A: Shell splits on the space -> 3 arguments sandbox/my, results.csv, exp09/ -> "cp: cannot stat 'sandbox/my': No such file" and same for results.csv (word splitting) | K: cannot stat unquoted space word splitting error
Q: Rename draft.tex to manuscript.tex | A: mv draft.tex manuscript.tex | K: rename file
Q: Rename sandbox/exp09/README.md to sandbox/exp09/NOTES.md | A: mv sandbox/exp09/README.md sandbox/exp09/NOTES.md | K: rename readme notes
Q: Move all png files into figures/ | A: mv *.png figures/ | K: move many files png
Q: Move without ever overwriting | A: mv -n a.txt dest/ | K: no overwrite never n
Q: Why is mv instant even for a huge file? | A: On the same filesystem only the directory entry changes, data isn't copied | K: mv fast instant large
Q: Do cp and mv overwrite by default? | A: Yes, silently | K: overwrite silently default
Q: Two jobs of mv? | A: Rename and move | K: mv rename move

===== RM =====
Q: Delete a file | A: rm scratch.txt | K: delete remove file
Q: Delete a directory and everything in it | A: rm -r old_run/ | K: delete directory recursive
Q: Force delete, no prompt, no error if missing | A: rm -f stubborn.txt | K: force delete f
Q: Delete csv files asking for each one | A: rm -i *.csv | K: prompt each delete interactive
Q: Delete an empty directory only | A: rmdir empty_dir | K: remove empty directory rmdir
Q: Why use rmdir instead of rm -r? | A: rmdir refuses non-empty directories - tells you if you were wrong | K: rmdir safety non empty
Q: Delete sandbox/exp09/logs/ safely | A: ls sandbox/exp09/logs   then   rm -r sandbox/exp09/logs | K: safe delete check first logs
Q: Is there a trash can for rm? | A: No - rm unlinks immediately; /scratch usually has no backup | K: trash undo recover
Q: Safest habit before rm with a pattern? | A: Run ls with the same pattern first, check output, then change ls to rm | K: safe habit ls first
Q: Danger of rm -rf $DIR/* | A: If DIR is unset it becomes rm -rf /* | K: danger unset variable dir
Q: Danger of rm -rf ~/data /old (with a space) | A: The space makes it delete ~/data entirely AND /old | K: danger space typo
Q: Danger of rm -rf .* | A: .* can match .. (the parent directory) | K: danger dot star parent
Q: How to make a script abort on an unset variable? | A: set -u | K: set u unset variable script
Q: Alias to be asked before every rm | A: alias rm='rm -i' (while learning; scripts must not rely on it) | K: alias rm i
Q: Best protection against deleting raw data? | A: Make it read-only: chmod -R a-w data/raw/ (you can't delete what you can't write) | K: protect raw data read only

===== GLOBBING / WILDCARDS =====
Q: What does * match? | A: Any characters including none (but not a leading dot, and never /) | K: star asterisk any characters
Q: What does ? match? | A: Exactly one character | K: question mark one character
Q: Match any name ending in .csv | A: *.csv | K: ending csv extension
Q: Match run followed by exactly two characters then .dat | A: run??.dat | K: two characters question marks
Q: Match sample1.txt sample2.txt sample3.txt | A: sample[123].txt | K: brackets set one of
Q: Match a digit right after sample, then anything | A: sample[0-9]*.txt | K: digit range bracket
Q: Match NOT a digit after sample | A: sample[!0-9]*.txt | K: not digit negate exclamation
Q: Brace expansion for two directories alpha and beta logs | A: {alpha,beta}/*.log | K: brace two directories
Q: Generate run01.dat to run12.dat | A: run{01..12}.dat | K: sequence expansion range numbers
Q: Recursive glob for all .py files in subdirectories | A: **/*.py   after   shopt -s globstar | K: recursive double star globstar
Q: Why doesn't ls * show .bashrc? | A: * does not match a leading dot | K: hidden dot star not shown
Q: How to test/debug a glob before running a dangerous command? | A: Put echo in front: echo sample00[1-3].txt | K: debug glob echo test
Q: echo sample00[1-3].txt output? | A: sample001.txt sample002.txt sample003.txt (echo got 3 arguments, never saw brackets) | K: echo bracket output
Q: ls *.zzz when nothing matches - what happens? | A: ls: cannot access '*.zzz': No such file or directory (pattern passed literally; the error comes from ls, not the shell) | K: no match cannot access zzz
Q: echo *.qqq (or *.zzz) when nothing matches prints? | A: *.qqq (the pattern itself, unchanged) | K: no match echo literal qqq
Q: Why does echo *.qqq differ from ls *.qqq? | A: Both receive literal *.qqq; echo just prints it, ls looks for a file with that name and errors | K: echo vs ls no match difference
Q: for f in *.csv in an empty directory runs how? | A: Once, with f = literal "*.csv". Guard with [[ -e "$f" ]] or shopt -s nullglob | K: loop empty nullglob
Q: How many files match sample*.txt in globlab? | A: ls sample*.txt | wc -l   -> 120 | K: count sample txt how many match
Q: How many sample files have a number ending in 7? | A: ls sample*7.txt | wc -l   -> 12 | K: ending in 7 count
Q: List only sample010.txt through sample019.txt | A: ls sample01[0-9].txt | K: range 010 019
Q: Pattern for every .txt except notes.md and sample999.txt.bak | A: echo sample*.txt (.bak doesn't end in .txt; notes.md isn't .txt) | K: except exclude txt bak
Q: What does ls sample*.txt.bak print? | A: sample999.txt.bak (* matched "999.txt", so it DID match) | K: bak pattern matched
Q: Why does ls sample*.txt not show subdir/sample050.txt? | A: A glob matches one directory level only; * never matches /. Use sample*/*.txt, ** with globstar, or find | K: subdirectory not shown one level
Q: Glob vs regex: * ? . | A: glob * = any chars, ? = one char, . = literal dot; regex * = zero or more of previous, ? = zero or one, . = any char | K: glob regex difference regular expression
Q: Are globs anchored? | A: Yes, always match the whole name; regex only with ^ and $ | K: anchored whole name
Q: Is {a,b} globbing? | A: No, brace expansion - generates text even if no files exist | K: brace not glob

===== HISTORY / KEYS / BASHRC =====
Q: Show your last 20 commands | A: history | tail -20 | K: history last commands
Q: Find how you ran sbatch before | A: history | grep sbatch | K: search history grep
Q: Repeat the last command | A: !! | K: repeat last command bang bang
Q: Use last argument of previous command | A: !$   (e.g. mkdir -p a/b/c then cd !$) | K: last argument bang dollar
Q: Rerun the most recent command starting with ls | A: !ls | K: bang command starting
Q: Where is bash history stored? | A: ~/.bash_history, written when shell exits | K: history file bash_history
Q: Complete a filename | A: Tab (twice to list options) | K: tab completion
Q: Reverse search history | A: Ctrl-r | K: reverse search ctrl r
Q: Jump to start / end of line | A: Ctrl-a / Ctrl-e | K: start end line ctrl a e
Q: Delete to start / to end of line | A: Ctrl-u / Ctrl-k | K: delete line ctrl u k
Q: Delete previous word | A: Ctrl-w | K: delete word ctrl w
Q: Clear the screen | A: Ctrl-l | K: clear screen ctrl l
Q: Insert last argument of previous command (key) | A: Alt-. | K: alt dot last argument
Q: Stop / interrupt a running command | A: Ctrl-c | K: interrupt stop kill ctrl c
Q: End of input / logout | A: Ctrl-d | K: end input ctrl d
Q: Why is Tab completion an error check? | A: If it doesn't complete, you're not where you think or the file isn't named what you think | K: tab error check
Q: Apply .bashrc changes without logging out | A: source ~/.bashrc | K: source bashrc reload
Q: Keep lots of history / no duplicates | A: export HISTSIZE=100000 ; export HISTCONTROL=ignoredups:erasedups | K: histsize histcontrol
Q: Keep history across sessions | A: shopt -s histappend | K: histappend
Q: Enable ** | A: shopt -s globstar | K: globstar enable
Q: Should you put aliases in scripts? | A: No - scripts run where .bashrc doesn't; be explicit | K: alias scripts
Q: Alias to cd to scratch | A: alias scratch='cd /scratch/$USER' | K: alias scratch

===== INSPECTING FILES =====
Q: What kind of file is this / format regardless of extension? | A: file data.bin | K: file type format detect magic
Q: unknown_blob has no extension. What kind of file is it? | A: file unknown_blob  -> PDF document, version 1.4 | K: unknown blob no extension pdf
Q: file mystery.dat says "data". Meaning? | A: file recognized nothing - raw binary, encrypted, or unknown format | K: data unrecognized binary
Q: How does file decide the type? | A: Reads magic bytes at the start of the file; ignores the extension | K: magic bytes extension
Q: Count lines in a file | A: wc -l big.csv | K: count lines number of lines
Q: Count bytes in a file | A: wc -c big.csv | K: count bytes
Q: Count lines, words, characters | A: wc -lwc notes.md | K: words characters count
Q: Disk usage of one file | A: du -h big.csv | K: disk usage file size
Q: Show everything about a file (inode, times, permissions, size) | A: stat big.csv | K: stat inode metadata
Q: How many data rows (not lines) does measurements.csv have? | A: wc -l measurements.csv -> 4001 lines, so 4000 data rows (minus header) | K: data rows header minus one
Q: Count data rows without header | A: tail -n +2 f.csv | wc -l | K: rows without header count
Q: A file with no trailing newline - wc -l? | A: Undercounts by one | K: trailing newline undercount
Q: Show first 10 lines | A: head big.csv | K: first lines beginning
Q: Show first 3 lines | A: head -n 3 big.csv   (or head -3) | K: first 3 lines
Q: Show column names / header of a CSV | A: head -1 measurements.csv | K: column names header first line
Q: Show the very last row | A: tail -1 measurements.csv | K: last row last line
Q: Show first 200 bytes | A: head -c 200 big.bin | K: first bytes
Q: Show last 20 lines of a log | A: tail -n 20 job.log | K: last lines end
Q: Everything except the first line (skip header) | A: tail -n +2 big.csv | K: skip header except first line
Q: Difference between tail -n +2 and tail -n 2? | A: +2 = start at line 2 to the end; 2 = the last 2 lines | K: plus two difference
Q: Follow a growing log live | A: tail -f job.log  (Ctrl-c to stop) | K: follow live growing log
Q: Why are head and tail fast on a 40 GB file? | A: They read only what they need | K: fast large file head tail
Q: Why check tail of a data file? | A: Files are often truncated at the end by a job that ran out of time/disk | K: truncated end check
Q: What does head -3 of a CSV confirm? | A: Delimiter, column order, date format before writing parsing code | K: delimiter columns check
Q: Page through a big file | A: less big.csv | K: page scroll view less
Q: Page without wrapping long lines (wide table) | A: less -S big.csv | K: no wrap wide chop
Q: Page with line numbers | A: less -N job.log | K: line numbers less
Q: Page a compressed file | A: zless archive.gz | K: page compressed gz zless
Q: less keys | A: space forward, b back, /pattern search, n next, ? search backward, g first line, G last line, -S toggle wrap, q quit | K: less keys navigation quit search
Q: What pager does man use? | A: less (same keys) | K: man pager less
Q: Show first three lines of measurements.csv.gz without decompressing to disk | A: zcat measurements.csv.gz | head -3   (or zless) | K: gz first lines without decompressing zcat head
Q: How many lines in a .gz file (without decompressing to disk)? | A: zcat file.gz | wc -l | K: gz lines count compressed zcat wc
Q: How many lines are in all of logs/*.log.gz combined, without decompressing anything to disk? | A: zcat logs/*.log.gz | wc -l | K: all gz combined total lines logs zcat wc
Q: Total lines across .gz AND plain log files combined | A: zcat -f logs/*.log* | wc -l | K: gz and plain combined mixed
Q: Last 3 lines of a .gz file | A: zcat f.gz | tail -3 | K: gz last lines tail
Q: Search inside a .gz file for a word | A: zcat f.gz | grep word   (or zgrep word f.gz) | K: grep inside gz zgrep search compressed
Q: Total lines in all plain .log files combined | A: cat logs/*.log | wc -l | K: all logs combined total plain
Q: Lines per file with a total at the bottom | A: wc -l logs/*.log | K: per file total wc multiple
Q: How many .gz files are there (count files, not lines)? | A: ls logs/*.log.gz | wc -l | K: number of gz files count files
Q: wc -l measurements.csv vs wc -l measurements.csv.gz differ wildly. Why? | A: The .gz is binary; wc counts newline bytes that happen to appear - meaningless (not wrong). Decompress first: zcat f.gz | wc -l | K: wc gz different meaningless
Q: windows_export.csv looks fine but breaks a parser. Prove what's wrong with one command | A: cat -A windows_export.csv | head -2   -> ^M at every line end (Windows CRLF) | K: windows line endings crlf parser cat A
Q: Show invisible characters | A: cat -A file | K: invisible hidden characters
Q: In cat -A: ^M, $, ^I mean? | A: ^M = carriage return (Windows), $ = end of line, ^I = tab | K: caret M dollar I meaning
Q: Why do ^M line endings break numbers? | A: Last column becomes 1.5\r instead of 1.5, numeric comparisons fail | K: carriage return numeric fail
Q: Does file warn about CRLF in CSV? | A: Not always - don't rely on it alone | K: file crlf warning
Q: Fix Windows line endings | A: dos2unix f.csv   OR   sed -i 's/\r$//' f.csv | K: fix crlf dos2unix sed
Q: Why not cat huge.csv or vim huge.csv? | A: cat dumps 40 GB to terminal; vim loads it all into RAM - can freeze a shared login node. Use less/head/tail | K: cat vim huge file bad
Q: What is cat actually for? | A: Concatenating small files: cat a.txt b.txt > c.txt | K: cat concatenate join files
Q: Accidentally catted a huge file - what now? | A: Ctrl-c to interrupt, Ctrl-l to clear | K: oops stop output

===== FIND =====
Q: Find all .log files recursively from here | A: find . -name "*.log" | K: find name log recursive
Q: How many .log files are anywhere under findlab/? | A: find findlab -name "*.log" | wc -l   -> 9 | K: count log files findlab how many
Q: Find case-insensitive name | A: find . -iname "*.LOG" | K: case insensitive iname
Q: Find files only | A: find . -type f | K: type f files only
Q: Find directories only | A: find . -type d | K: type d directories only
Q: Find files larger than 1 MB | A: find . -type f -size +1M | K: larger bigger than size 1M
Q: Which files under findlab are larger than 1 MB? | A: find findlab -type f -size +1M | K: findlab large files bin
Q: Find files smaller than 1 KB | A: find . -type f -size -1k | K: smaller size
Q: Find files modified in the last 2 days | A: find . -mtime -2 | K: modified recent days mtime
Q: Find files modified more than 30 days ago | A: find . -mtime +30 | K: older than days old
Q: Find files modified after 2025-01-01 | A: find . -newermt 2025-01-01 | K: after date newermt
Q: Find every .log file last modified BEFORE 2025 | A: find findlab -name "*.log" ! -newermt 2025-01-01 | K: before date older not newer
Q: Find empty directories | A: find . -type d -empty | K: empty directories
Q: Find empty files | A: find . -type f -empty | K: empty files
Q: Find all empty directories AND all empty files (two tests) | A: find findlab -type d -empty ; find findlab -type f -empty | K: empty both
Q: Delete all .tmp files found | A: find . -name "*.tmp" -delete   (list first without -delete!) | K: find delete tmp
Q: Count lines in every .csv under findlab/ with one command | A: find findlab -name "*.csv" -exec wc -l {} + | K: exec wc every csv lines
Q: What do {} and + mean in -exec? | A: {} = each found path; + = pass many paths to one command (\; runs once per file) | K: exec braces plus semicolon
Q: Run a command on found files with spaces in names | A: find . -print0 | xargs -0 cmd | K: print0 xargs spaces
Q: Find broken symbolic links | A: find . -xtype l | K: broken links xtype
Q: Total lines of all .gz files in a whole tree | A: find logs -name "*.log.gz" -exec zcat {} + | wc -l | K: find gz tree total
Q: Find .bin files larger than 1M in findlab | A: find findlab -type f -size +1M -name "*.bin" | K: bin large combined tests
Q: How are multiple find tests combined? | A: ANDed together, left to right; first argument is the starting directory | K: tests and order find
Q: Which find tests should come first? | A: Cheap ones (-type, -name) before expensive ones (-size) | K: test order cheap expensive
Q: Why must you quote the pattern in find -name "*.log"? | A: Unquoted, the shell expands *.log in the current directory first, so find gets filenames not a pattern | K: quote pattern find why
Q: What happens with find findlab -name *.log (no quotes)? | A: No .log here -> works by accident; exactly one -> searches that one name; several -> error "paths must precede expression" | K: unquoted find error paths must precede expression
Q: Is find output sorted? | A: No, filesystem order - pipe to sort if needed | K: find order sort
Q: find vs ls? | A: ls lists one directory; find walks an entire tree | K: find vs ls difference
Q: Sort find output | A: find . -name "*.log" | sort | K: sort find output

===== DISK SPACE: DU / DF =====
Q: Total size of a directory | A: du -sh findlab | K: directory size total du
Q: Size of each entry here, smallest to largest | A: du -sh * | sort -h | K: sizes sorted biggest smallest
Q: Which single directory in findlab holds the most data? | A: du -sh findlab/* | sort -h   (biggest is last) | K: most data biggest directory
Q: Sizes one level down only | A: du -h --max-depth=1 . | K: max depth one level
Q: Is the whole filesystem full? | A: df -h /scratch | K: filesystem full df
Q: Show my quota | A: quota -s | K: quota
Q: du vs df? | A: du walks the tree adding file usage; df asks the filesystem - they disagree and both are right | K: du df difference
Q: sort -h vs sort -n? | A: sort -h understands 4.0K 3.1M 13M; sort -n does not | K: sort h human n numeric
Q: Why does du -sh findlab report more than the sum of file sizes? | A: Directories take space (~4 KB each) and files use whole blocks (7-byte file uses 4 KB) | K: du more than sum blocks
Q: du and your quota disagree - why? | A: Over file-count quota not byte quota, or a deleted file is still held open by a running process | K: quota disagree
Q: Strategy to find where space went | A: du -h --max-depth=1, cd into the biggest, repeat 3-4 times | K: find space strategy
Q: What does -s mean in du -sh? | A: Summarize - one total, don't show subdirectories | K: du s summarize

===== PERMISSIONS: READING LS -L =====
Q: Explain -rw-r--r-- 1 mgc csds 4.2M Mar 14 09:31 counts.tsv | A: - = file; rw- owner; r-- group; r-- others; 1 = links; mgc = owner; csds = group; 4.2M size; Mar 14 09:31 modified; counts.tsv name | K: ls l columns explain fields
Q: Columns of ls -l in order | A: type+permissions, number of links, owner, group, size, last modified date, name | K: columns order ls l
Q: First character of ls -l: - d l? | A: - regular file, d directory, l symbolic link | K: first character type file directory link
Q: What is the second column (number) in ls -l? | A: Number of links (and subdirectories for a directory) | K: link count second column
Q: Third and fourth columns of ls -l? | A: Owner and group | K: owner group column
Q: Explain drwxr-x--- | A: directory; owner rwx; group r-x (read + enter); others nothing | K: drwxr-x explain
Q: Explain lrwxrwxrwx ... latest -> run_2026_03_14 | A: symbolic link named latest pointing to run_2026_03_14 | K: symlink arrow
Q: The three permission classes | A: user (owner), group, other | K: classes user group other ugo
Q: r w x values | A: r=4, w=2, x=1 | K: values numbers 4 2 1
Q: r on a file / on a directory | A: file: read contents; directory: list the names inside | K: read permission meaning
Q: w on a file / on a directory | A: file: modify contents; directory: create/delete entries inside | K: write permission meaning
Q: x on a file / on a directory | A: file: run it as a program; directory: enter it / traverse through it (cd) | K: execute permission meaning directory enter
Q: Which class's permissions apply to you? | A: The FIRST class that applies (owner, then group, then other) - not the most generous | K: first class applies
Q: File is ---rw----. Can the owner read it? | A: No - owner class has no permissions even though group can write | K: owner cannot read group
Q: Octal digits 7 6 5 4 0? | A: 7=rwx, 6=rw-, 5=r-x, 4=r--, 0=--- | K: octal digits meaning
Q: What is 755? | A: rwxr-xr-x (owner all, others read+execute) - scripts/programs/directories | K: 755
Q: What is 644? | A: rw-r--r-- - normal default for a file | K: 644
Q: What is 600? | A: rw------- - required for SSH private keys | K: 600 ssh key
Q: What is 700? | A: rwx------ - private to owner | K: 700 private
Q: What is 750? | A: rwxr-x--- - group can read and enter, others nothing | K: 750
Q: What is 775? | A: rwxrwxr-x - group can write too | K: 775
Q: What is 444? | A: r--r--r-- - read-only for everyone | K: 444 read only
Q: What is 777? | A: rwxrwxrwx - everyone everything (avoid) | K: 777
Q: Convert rwxr-x--- to octal | A: 750 | K: convert symbolic to octal
Q: Convert rw-rw-r-- to octal | A: 664 | K: 664

===== PERMISSIONS: CHMOD =====
Q: Add execute permission for the owner | A: chmod u+x analyse.sh | K: add execute owner u+x
Q: Remove write for group and others | A: chmod go-w shared.csv | K: remove write group others
Q: Add read for everyone | A: chmod a+r notes.md | K: add read all everyone
Q: Set rwxr-xr-x | A: chmod 755 analyse.sh | K: set 755
Q: Set rw-r--r-- | A: chmod 644 notes.md | K: set 644
Q: Set permissions for an SSH private key | A: chmod 600 ~/.ssh/id_ed25519 | K: ssh key chmod 600
Q: id_demo is a pretend private key. Set it to what SSH demands and give octal | A: chmod 600 id_demo   (rw-------, octal 600) | K: id_demo private key
Q: Give group read and enter access recursively without making files executable | A: chmod -R g+rX project/   (capital X = x only on directories) | K: capital X recursive group read enter
Q: Give the group read and enter access to shared/ recursively, without making the CSVs executable | A: chmod -R g+rX shared/ | K: shared group csv not executable
Q: Let group read, write and enter a project recursively | A: chmod -R g+rwX project/ | K: group read write enter
Q: What does capital X do in chmod? | A: Adds execute only to directories (and files already executable by someone) | K: capital X meaning
Q: Protect raw data from being changed/deleted | A: chmod a-w raw/   (and chmod -R a-w raw/ for contents) | K: protect raw read only a-w
Q: Make everything in raw/ read-only for everyone including you | A: chmod -R a-w raw/ | K: read only everyone including me recursive
Q: What do u g o a mean? | A: u = user/owner, g = group, o = others, a = all | K: ugoa meaning
Q: What do + - = mean in chmod? | A: + add, - remove, = set exactly | K: plus minus equals chmod
Q: Make a script runnable by everyone | A: chmod a+x script.sh   (or chmod 755) | K: executable everyone
Q: Run a script in the current directory | A: ./analyse.sh | K: run script dot slash

===== PERMISSIONS: PROBLEMS =====
Q: ./analyse.sh says Permission denied. Diagnose and fix with minimum change | A: ls -l analyse.sh (shows -rw-r--r--, no x) ; chmod u+x analyse.sh ; ./analyse.sh | K: permission denied script run fix
Q: Most common reason a new script won't run? | A: New files are not executable - needs chmod u+x | K: script not executable new
Q: locked/ is mode 600 (drw-------). Why does ls locked work but cat locked/treasure.txt not? | A: r lets you list names; without x you cannot enter/traverse to read files inside | K: locked 600 ls works cat fails
Q: Fix locked/ so you can read files inside, one command | A: chmod u+x locked | K: fix locked directory
Q: Directory has r but no x - what can you do? | A: See names only - no cd, no reading files, not even sizes | K: r without x directory
Q: Why does cd permlab/locked say Permission denied? | A: Directory lacks x (execute = enter) | K: cd permission denied directory
Q: What do you need to share a directory with others? | A: r and x on it, plus x on every parent directory leading to it | K: share directory parents x
Q: Why can you delete a read-only file? | A: Deleting removes an entry from the DIRECTORY, so it needs w on the directory, not the file. rm only asks for confirmation as a courtesy | K: delete read only file why directory write
Q: How to really prevent deleting files in raw/? | A: Remove write from the directory: chmod a-w raw/ | K: prevent delete directory write
Q: rm asks "remove write-protected regular file?" - why? | A: File is read-only; rm asks as a courtesy but can still delete if directory is writable | K: write protected rm asks

===== OWNERSHIP / GROUPS =====
Q: Who am I and which groups am I in? | A: id | K: id user groups whoami
Q: Change group of project/ to csds | A: chgrp csds project/ | K: change group chgrp
Q: Change group recursively | A: chgrp -R csds project/ | K: chgrp recursive
Q: Who can change a file's owner? | A: Only root | K: change owner root chown
Q: Which groups can you give a file to? | A: Only groups you belong to | K: chgrp only my groups
Q: Make new files in a shared directory inherit its group | A: chmod g+s project/   (setgid) | K: setgid inherit group g+s
Q: Why is chmod g+s needed on shared lab directories? | A: Without it, files you create belong to your personal group and collaborators can't read them | K: setgid why shared
Q: Make new files have no permissions for others | A: umask 007 | K: umask 007 others default

===== LAB SETUP (from slides) =====
Q: Build the lab environment | A: bash setup-day1.sh   then   cd ~/linux-lab | K: setup lab environment
Q: Lost during the lab? | A: cd ~/linux-lab and start again (rerun script to rebuild) | K: lost lab reset
