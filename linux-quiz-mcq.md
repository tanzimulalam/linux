# Linux Quiz — Practice MCQs

48 multiple-choice questions, easy → hard.
Scope: **Day 1a** (shell basics, all) + **Day 1b** up to and including **Permissions** (inspecting files, `find`, `du`/`df`, permissions).
Not covered: archiving (`tar` in depth), links, project organisation.

Click **Answer** under each question to reveal it.

---

## Easy (1–15)

**1.** Which command prints the directory you are currently in?
A) `cwd`  B) `pwd`  C) `dir`  D) `path`
<details><summary>Answer</summary>

**B** — print working directory.
</details>

**2.** What does `cd` with no argument do?
A) Nothing  B) Goes up one level  C) Goes to your home directory  D) Goes to `/`
<details><summary>Answer</summary>

**C** — same as `cd ~`.
</details>

**3.** Which takes you back to the *previous* directory you were in?
A) `cd ..`  B) `cd -`  C) `cd !`  D) `cd prev`
<details><summary>Answer</summary>

**B** — `cd -` toggles between two directories.
</details>

**4.** `..` means:
A) Hidden file  B) This directory  C) The parent directory  D) Home
<details><summary>Answer</summary>

**C** — `.` is this directory, `..` is the parent.
</details>

**5.** Which flag makes `ls -l` show sizes as 4.0K / 12M / 1.3G?
A) `-s`  B) `-H`  C) `-h`  D) `-m`
<details><summary>Answer</summary>

**C** — human-readable.
</details>

**6.** Which shows hidden dotfiles like `.bashrc`?
A) `ls -h`  B) `ls -a`  C) `ls -d`  D) `ls -R`
<details><summary>Answer</summary>

**B**
</details>

**7.** Create an empty file called `notes.md`:
A) `mkdir notes.md`  B) `new notes.md`  C) `touch notes.md`  D) `create notes.md`
<details><summary>Answer</summary>

**C** — `touch` also updates the timestamp if the file exists.
</details>

**8.** Copying a **directory** with `cp` requires which flag?
A) `-d`  B) `-r`  C) `-c`  D) `-a` only
<details><summary>Answer</summary>

**B** — `cp -r` (`-a` also works, but `-r` is the required one).
</details>

**9.** `mv` does which two jobs?
A) Move and copy  B) Move and rename  C) Rename and delete  D) Copy and link
<details><summary>Answer</summary>

**B**
</details>

**10.** Which deletes **only** empty directories?
A) `rm -r`  B) `rm -f`  C) `rmdir`  D) `del`
<details><summary>Answer</summary>

**C** — its refusal on non-empty directories is a useful safety check.
</details>

**11.** Show the first 3 lines of `big.csv`:
A) `head -3 big.csv`  B) `top -3 big.csv`  C) `tail -3 big.csv`  D) `first big.csv`
<details><summary>Answer</summary>

**A** — or `head -n 3 big.csv`.
</details>

**12.** Which counts the lines in a file?
A) `wc -c`  B) `wc -w`  C) `wc -l`  D) `count -l`
<details><summary>Answer</summary>

**C** — `-c` is bytes, `-w` is words.
</details>

**13.** Which shows the manual page for `ls`?
A) `help ls`  B) `man ls`  C) `info -m ls`  D) `ls -man`
<details><summary>Answer</summary>

**B**
</details>

**14.** In `chmod`, the numeric values of r, w, x are:
A) 1, 2, 4  B) 4, 2, 1  C) 2, 4, 1  D) 1, 4, 2
<details><summary>Answer</summary>

**B** — r=4, w=2, x=1.
</details>

**15.** `chmod 644 notes.md` gives:
A) `rwxr--r--`  B) `rw-rw-r--`  C) `rw-r--r--`  D) `rw-r--rw-`
<details><summary>Answer</summary>

**C** — 6=`rw-`, 4=`r--`, 4=`r--`.
</details>

---

## Medium (16–34)

**16.** Which lists files **oldest first, newest at the bottom**?
A) `ls -lt`  B) `ls -ltr`  C) `ls -lS`  D) `ls -lR`
<details><summary>Answer</summary>

**B** — `-t` sorts by time, `-r` reverses so the newest sits next to your prompt.
</details>

**17.** `mkdir a/b/c` fails when `a/b` doesn't exist. The fix:
A) `mkdir -r a/b/c`  B) `mkdir -f a/b/c`  C) `mkdir -p a/b/c`  D) `mkdir -a a/b/c`
<details><summary>Answer</summary>

**C** — `-p` creates parents and doesn't complain if the directory already exists.
</details>

**18.** One command to create `exp08/raw`, `exp08/processed`, `exp08/figures`, `exp08/logs`:
A) `mkdir -p exp08/[raw,processed,figures,logs]`
B) `mkdir -p exp08/{raw,processed,figures,logs}`
C) `mkdir -p exp08/*`
D) `mkdir -p exp08/(raw processed figures logs)`
<details><summary>Answer</summary>

**B** — brace expansion; the shell turns it into four words before `mkdir` runs.
</details>

**19.** In `ls -l`, what is the very **first** character of `drwxr-x---`?
A) A permission bit  B) The file type  C) The owner  D) A link count
<details><summary>Answer</summary>

**B** — `-` file, `d` directory, `l` symlink.
</details>

**20.** Which lists **directories only**, without descending into them?
A) `ls -R`  B) `ls -l`  C) `ls -d */`  D) `ls --dirs`
<details><summary>Answer</summary>

**C** — `-d` is what stops `ls` entering each one.
</details>

**21.** `?` in a glob matches:
A) Zero or more characters  B) Exactly one character  C) A digit  D) A literal `?`
<details><summary>Answer</summary>

**B**
</details>

**22.** Which pattern matches `sample1.txt`, `sample2.txt`, `sample3.txt` only?
A) `sample*.txt`  B) `sample?.txt`  C) `sample[123].txt`  D) `sample{1-3}.txt`
<details><summary>Answer</summary>

**C**
</details>

**23.** `sample[!0-9]*.txt` matches names where the character after "sample" is:
A) A digit  B) Not a digit  C) A letter only  D) Any character
<details><summary>Answer</summary>

**B** — `!` negates the bracket.
</details>

**24.** `ls *` does **not** show `.bashrc` because:
A) It's a system file  B) `*` doesn't match a leading dot  C) It's in another directory  D) It has no extension
<details><summary>Answer</summary>

**B** — use `ls -a` to see it.
</details>

**25.** `head -c 200 big.bin` prints the first 200:
A) Lines  B) Words  C) Bytes  D) Blocks
<details><summary>Answer</summary>

**C**
</details>

**26.** Skip a CSV header and print everything from line 2 onward:
A) `tail -n 2 f.csv`  B) `tail -n +2 f.csv`  C) `head -n +2 f.csv`  D) `tail -2 f.csv`
<details><summary>Answer</summary>

**B** — `-n +2` means "start at line 2"; `-n 2` means "the last 2 lines".
</details>

**27.** Watch a log file grow live:
A) `less -f job.log`  B) `tail -f job.log`  C) `cat -f job.log`  D) `head -f job.log`
<details><summary>Answer</summary>

**B** — `Ctrl-c` to stop.
</details>

**28.** Which identifies a file's real format regardless of its extension?
A) `stat f`  B) `type f`  C) `file f`  D) `wc f`
<details><summary>Answer</summary>

**C** — `file` reads the magic bytes and ignores the name.
</details>

**29.** A file has Windows line endings. Which command proves it?
A) `file f.csv`  B) `cat -A f.csv`  C) `wc -l f.csv`  D) `less f.csv`
<details><summary>Answer</summary>

**B** — shows `^M$` at every line end (`file` doesn't reliably warn you).
</details>

**30.** In `cat -A` output, `^I` means:
A) Carriage return  B) End of line  C) A tab  D) A space
<details><summary>Answer</summary>

**C** — `^M` is a carriage return, `$` is end of line.
</details>

**31.** Find every `.log` file under `findlab/`:
A) `ls -R findlab | grep .log`  B) `find findlab -name "*.log"`  C) `find findlab *.log`  D) `find -name findlab/*.log`
<details><summary>Answer</summary>

**B** — and quote the pattern.
</details>

**32.** Which finds **directories** only?
A) `find . -type f`  B) `find . -type d`  C) `find . -dir`  D) `find . -d`
<details><summary>Answer</summary>

**B**
</details>

**33.** Files bigger than 1 MB:
A) `find . -size 1M`  B) `find . -size +1M`  C) `find . -size >1M`  D) `find . -big 1M`
<details><summary>Answer</summary>

**B** — `+` means "more than".
</details>

**34.** Which sorts `4.0K`, `3.1M`, `13M` correctly?
A) `sort -n`  B) `sort -h`  C) `sort -r`  D) `sort -k`
<details><summary>Answer</summary>

**B** — `-h` understands human-readable suffixes.
</details>

---

## Hard (35–48)

**35.** In what order does the shell process `ls -l *.csv`?
A) Find program → split → expand → execute
B) Split → expand → find program → fork and execute → collect exit status
C) Expand → split → execute → find program
D) Execute → expand → split
<details><summary>Answer</summary>

**B** — the key consequence: the program never sees what you typed, only the expanded result.
</details>

**36.** `ls *.zzz` errors but `echo *.zzz` prints `*.zzz`. Why?
A) `echo` ignores errors
B) The shell expanded it to nothing for `echo`
C) No match, so the pattern is passed through literally; `ls` then failed to find a file with that literal name
D) `echo` does its own globbing
<details><summary>Answer</summary>

**C** — the error came from `ls`, not the shell.
</details>

**37.** `cp sandbox/my results.csv exp09/` fails with two "cannot stat" errors because:
A) The file is read-only
B) The shell split the unquoted space into separate arguments
C) `cp` needs `-r`
D) `exp09/` doesn't exist
<details><summary>Answer</summary>

**B** — word splitting. Fix: `cp "sandbox/my results.csv" exp09/`
</details>

**38.** `cp -r template sandbox/t2`, where `t2` **already exists**, results in:
A) `t2` containing template's contents
B) `t2` being overwritten
C) A `template/` directory created *inside* `t2`
D) An error
<details><summary>Answer</summary>

**C** — the classic cp trap. To copy the contents either way: `cp -a template/. dest/`
</details>

**39.** Which is the correct `tar` invocation?
A) `tar -cfz a.tgz d/`  B) `tar -czf a.tgz d/`  C) `tar -fcz a.tgz d/`  D) `tar -zfc a.tgz d/`
<details><summary>Answer</summary>

**B** — `-f` takes a value, so it must come last in the stack; in A, `-f` swallows `z` as the filename.
</details>

**40.** Why does `find . -name *.log` (unquoted) misbehave?
A) `find` can't read globs
B) The shell expands `*.log` in the current directory first, so `find` receives filenames instead of a pattern
C) It always errors
D) It searches only the current directory
<details><summary>Answer</summary>

**B** — worst case, it "works by accident" when nothing matches locally.
</details>

**41.** Run `wc -l` on every `.csv` found, in one command:
A) `find . -name "*.csv" | wc -l`
B) `find . -name "*.csv" -exec wc -l {} +`
C) `find . -name "*.csv" -wc -l`
D) `wc -l $(find . -type d)`
<details><summary>Answer</summary>

**B** — `{}` is the found path, `+` batches them into one `wc` call. (A only counts how many files matched.)
</details>

**42.** `ls -l exp07` starts with `total 16`. That number is:
A) The file count
B) The total size of the files inside
C) Disk space used by the directory's own entries, in 1 KB blocks
D) The inode number
<details><summary>Answer</summary>

**C** — for real sizes use `du -sh`.
</details>

**43.** `du -sh` reports more than the sum of the visible file sizes because:
A) It counts hidden files twice
B) Every directory occupies space itself and files are allocated in whole blocks
C) It includes the parent directory
D) It measures uncompressed size
<details><summary>Answer</summary>

**B** — a 7-byte file still uses 4 KB.
</details>

**44.** `wc -l measurements.csv.gz` gives a strange number. It is:
A) Wrong — a bug
B) The compressed line count
C) Meaningless — `wc` counted newline bytes in a binary stream; use `zcat f.gz | wc -l`
D) The number of blocks
<details><summary>Answer</summary>

**C** — `wc` answered a different question than the one you meant.
</details>

**45.** A directory has mode `drw-------`. `ls locked` works but `cat locked/treasure.txt` fails. Why, and what is the minimum fix?
A) Missing `r`; `chmod u+r locked`
B) Missing `x`; `chmod u+x locked`
C) Missing `w`; `chmod u+w locked`
D) Wrong owner; `chgrp`
<details><summary>Answer</summary>

**B** — `r` lets you see the names; `x` is needed to enter/traverse and read anything inside.
</details>

**46.** Why can you still delete a file that is read-only?
A) `rm` runs as root
B) Deleting removes an entry from the **directory**, so it needs `w` on the directory, not on the file
C) `rm -f` overrides permissions
D) Read-only only blocks editing by other users
<details><summary>Answer</summary>

**B** — real protection is removing write from the directory: `chmod a-w raw/`
</details>

**47.** Give the group read + enter access to `shared/` recursively **without** making the CSVs executable:
A) `chmod -R g+rx shared/`  B) `chmod -R 775 shared/`  C) `chmod -R g+rX shared/`  D) `chmod -R g+r shared/`
<details><summary>Answer</summary>

**C** — capital `X` adds `x` to directories only.
</details>

**48.** `chmod g+s project/` does what?
A) Makes the directory sticky, so only owners can delete
B) Makes new files inside inherit the directory's **group**
C) Gives the group execute permission
D) Sets the owner to the group
<details><summary>Answer</summary>

**B** — setgid. Without it, files you create in a shared directory belong to your personal group and collaborators can't read them.
</details>
