# explore-bash-scripting
  * know version of your bash - echo $SHELL
  * change the shell to bash (mac) - chsh -s /bin/bash
  * print env vars - env
  * view contents of file - cat <filePath> eg : cat /etc/profile
  * see aliases set in current shell - alias
  * see all internal commands - help
  * see bash version - echo $BASH_VERSION
  * echo -e "a\tb" - -e enables the formating with bash
  * printf "%s\n" hello world - hello <newline> world
  * printf "%s\n" "hello world" - hello world
  * printf "%04d\t" 1 - 0001
  * printf "%.2f\t" 1 - 1.00
  * printf "%d\t" 255 0xff 0377 - 255  255  255
  * shopt +s extglob - enables more regex pattrens in current shell like *(pattren), +(pattren) along with regular commands like ls eg: ls *.txt
  * ls -a *.txt - all files ending with .txt
  * ls -a ?(e).txt - all files having name <singleLetter e/NoLetter>.txt
  * ls -a @(e).txt - file with name e.txt
  * grep <textInSingleQuotes> <fileNameOrPattren> - grep 'hello' *.txt
  * command | grep <textOrPattren> - ls | grep 'abc'
  * grep means generic regular expression parser
  * exclude errors in output - ex: grep 'root' * 2>dev/null  
  * see file names which containing text - grep -l 'root' *
  * See non occurance of that text - grep -v 'root' *
  * see n lines after or before that match - grep -A n -B n 'root' *
