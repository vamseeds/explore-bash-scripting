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
  * search text in sub folders as well - grep -r 'root' *
  * use -E along with grep in order to use extended regex . eg :  grep -E 'bo+t' somefile
  * spliting content inf file using cut - cut -d<charToSplit> -f <nTh Column After cutting> <fileName> . Eg: cut -d: -f 1 /etc/passwd
  * sorting the data using sort - sort <option> . eg sort -n (numeric sorting order) , sort -d (dictionary order) . Eg : cut -d: -f 3 /etc/passwd | sort -n
  * print last n lines of file or input - tail -n /etc/passwd . eg: print last 5 lines of a file tail -5 /etc/passwd
  * print first n lines of file or input - head -n /etc/passwd . eg: print first 5 lines of a file head -5 /etc/passwd
  * print 4th line of a file  - head -4 /etc/passwd | tail -1 
  * old syntax for both head and tail is <command> -n <no.of lines> <fileName> , default line count is 10
  * retrive nth line using sed : sed -n <n>p <fileName> . eg: sed -n 5p /etc/passwd
  * replace text using sed (done once per line) : sed -i (interactive) '/s/<toBeReplaced>/<replacement>' <fileName> . eg: sed -i '/s/abc/xyz' somefile
  * ldd $(which <cmd>) to see the libraries being used... lesser libs more performance ... eg : ldd $(which awk)
  * replace all text occurences using sed : sed -i (interactive) '/s/<toBeReplaced>/<replacement>/g' <fileName> . eg: sed -i '/s/abc/xyz/g' somefile
  * delete nTh line using sed :  sed -i -e '<n>d' <fileName> . eg : sed -i -e '2d' sometext
  * awk can be used as filter (can do similar work of cut) print 1st column after separtion using : . awk -F : '{print $1}' /etc/passwd , 4th col : awk -F : '{print $4}' /etc/passwd
  * Searching and filtering with awk (can't be done with cut) : awk -F : '/student/ {print $1}' /etc/passwd 
  * advanced filtering based on different columns : awk -F : '$3(column 3) < 999 {print $1} /etc/password'
  * How do you tell your shell script interpreter that current file has followed bash format ? Ans : use Shebang at starting (#!bin/bash or #!usr/bin/env bash)
  * Single Quotes are Strong any variable reference inside single quotes is not interpreted
  * Double Quotes are referred as Weak Quotes as variable references can be interpreted
  * To avoid interpretation while using double quotes just add a backslash before variable . eg : echo "Hello \$USER" will be Hello $USER ... USER will not get interpreted 
  * declare is used to set special type of variable
      **eg :  read only variable declare -r x=1000 
      ** array variable declare -a my_array or declare -A my_array
  * Use declare -p to see which kind of variable it is . Eg : declare -p PATH 
  * Scripts which needs to be sourced should not start with shebang ... having shebang will create a new subshell for execution 
  * Site Specific data need to be decoupled from script and should be sourced in script .
  * source files can have variables and functions but to make it clean prefer having variables only
  * sourcing can be done in 2 ways viz., source <file> , . <file>
  * variables can be viewed in 2 ways . set , compgen -v
  * positional arguments of a script can be referred using $<position> . $0 is always script name . Eg: ./deploy.sh hello vamsi , $0 = ./deploy.sh , $1 = hello , $2 =vamsi 
  * /$* will treat all args as single string , /$@ will be helpful to iterate over all args
  * "shift <n>" command is useful to skip n arguments inside script.   ./deploy.sh hello vamsi how are you . $1 = hello . if we use shift 2 $1 will be how
  * Command Substitution : When we want to use the result of a command we use command substitution . Eg : today = $(date +%d-%m-%y) - $() is mostly is used and readable other way is to use backtick notation Eg: today = `date +%d-%m-%y` . Issue is some screens show backtick like single quote and it can be confusing
  * How to see the exit code of previous command? : use echo $?
  * here document : Its a I/O redirection to feed command list to an interactive program  .  Eg:
   ```
   cat >./kustomization.yaml <<EOF 
configMapGenerator:
- name: example-configmap-1
  files:
  - application.properties
EOF
   ```
   In above example we are trying to cat something and saving that to kustomization.yaml ... the command will consume data until it finds the keyword EOF. <<KEYWORD will help in redirection of data until it finds that text
   
   * Parameter Substitution: When Parameter is not available we can do 3 things display some value to stdout or assign some value or throw error message. Eg: 
   ```
   echo ${user:-$(whoami)}  - This just displays whoami result when user var is not available . Future references of user will still be empty
   echo ${user:=$(whoami)}  - This will assign whoami result to user when user var data is unavailable/not initialized. Future references of user will still be result of whoami
   echo ${user:?"Error"} - When user is not available Error will be displayed
   ```
   
   * Pattren Matching :
   ```
   ${var#} - length of the string
   ${var#<regex>} - removes the matched regex portion from right
   ${var##<regex>} - removes the long/last matched regex portion from right
   ${var%<regex>} - removes the matched regex portion from left
   ${var%%<regex>} - removes the long/last matched regex portion from right
   ```
   Replacement:
   ```
   ${var/pattren/replacement} -single replacement
   ${var//pattren/replacement} -global replacement
   ${var/#pattren/replacement} -replacement when var starts with pattren
   ${var/%pattren/replacement} -replacement when var ends with a pattren
   ```
   * In order to use all regex features we need to enable extended globbing . To enable it we should add below line in script :
     ```shopt -s extglob```
   
  

 
