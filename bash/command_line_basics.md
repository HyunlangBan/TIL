## cp

Copy multiple files to dir

- `cp -v bla bla_2 info.txt dir-9`
- `-v`: verbose option
  - output: bla, bla_2, info.txt → dir-9

## cat

- `cat -n` → 출력에 줄번호 추가
- concat file outputs → `cat text_1.txt text_2.txt`

## more

- output을 화면에 맞게 출력, arrow로 이동

## less

- output 출력시 새 창으로 띄워 기존 터미널에 흔적을 남기지 않는다.

## echo

- `-e`: new line이 필요할때 (이 옵션을 안쓰면 \를 그냥 스트링으로 알아들음)
- `echo -e “hello \nthere”`
- `\c`: 출력시 마지막 라인의 줄바꿈을 삭제
- `\v`: vertical tab (\t \n \t)

## touch

- `-c`: 동일한 이름의 파일이 있을때에만 덮어쓰는 옵션

## wildcards

- `*` → any characters and any numbers
- `?` → any character or number
- `[abc]` → a or b or c
- `[abc][ab].text` → ab.txt
- `!` → exclude
- `[!abc]` → any char that is not a, b or c
- `[[:alpha:]]` → only letters
- `[[:lower:]]` → lower case letter
- `[[:upper:]]` → upper case letter
- `[[:digit:]]` → only digits

## Variable

```bash
bob=130
echo ${bob}
echo "this is my value: ${bob}"
unset bob

a=123456789
echo ${#a}   # how many characters it contains -> 9

echo ${a:4}  # start with 4th character -> 56789
echo ${a:4:2} # 56
echo ${a: -3} # there should be a space! -> 789
```

## Variables Manipulation

```bash
b="hello there"
echo ${b#h}  # remove first h
echo ${b#t}  # nothing happend -> b doesnt start with t
echo ${b#*t} # remove everything upto t -> here

a=123456789
echo ${a%p}  # remove from the end -> 12345678
echo ${a%3*} # 12

```

## Permanet variables

- 임시 변수 → 변수를 할당하고 터미널을 끄고 새로 켜면 사라져있다.
- 로그인 스크립트에 설정해주어야 한다(ex - `.bashrc`, `.profile`, ...)

```bash
## .profile

s="my variable"
```

## read

```bash
read a
something123
echo ${a} # something123

read -p "give me a value of the variable: " q
give me the value of the variable: albert123
echo ${q} # albert123

read   # nothing to store the string
PAPA
echo $REPLY
PAPA
```

## Redirect output

- COMMAND -output→ STDOUT FILE → SCREEN
- COMMAND -output→ STDOUT FILE -redirect→ SOME FILE (redirect sign: `1>` or `>`)

`ls -l 1> a_file.txt`   
`ls -l > a_file.txt`   

- if the a_file.txt doesn’t exist, they create the file.

  `echo “add a line here ... “ >> a_file.txt`
  
  

- concat 2 files and redirect

  `cat bob.txt text1.txt > text_a.txt`   
  
 
- 입력으로 쓴 모든 값이 b_file.txt에 저장

  `cat > b_file.txt`
  

## Redirect the error

- COMMAND -status(error)→ STDERR FILE → SCREEN
- COMMAND -status(error)→ STDERR FILE -redirect→ SOME FILE (sign: `2>`)

`ls -l weraer 2> b_file.txt`

`&>` : redirect both stdoutput and stderror

- redirect to different files
  - `ls -l text1.txt text2.txt werawear 1> output.txt 2> error.txt`   


- 필요하지 않은 에러 메시지를 무시할 수 있음  
  - `/dev/null` → 항상 비어있으며 전송된 데이터는 삭제됨       
  - `ls -l text1.txt text2.txt anotherfile.txt 2> /dev/null`

## Pipe

put the previous command output as an input of next command

`ls A-folder/ | tail -3`

`ls A-folder/ | tail -3 | sort > myfile.txt`

## grep

: search

```bash
grep so b.txt  # search ‘so’ in b.txt
something

grep So b.txt # case sensitive
Son

grep -i so b.txt # ignore case
something
Son

ls | grep txt

ls | grep -v t # get everything except the file has t
```

## Brace expansion

```bash
echo {1,2,3}
1 2 3

echo {1,2,3,7}_file
1_file 2_file 3_file 7_file

echo example{1..7}
example1 example2 example3 example4 example5 example**6** example7

touch file{1..8} # create many files at once

echo {a,b,c}_{1,2,3}
a_1 a_2 a_3 b_1 b_2 b_3 c_1 c_2 c_3
```

## Permission in the terminal

- different user can different things
- every file is assigned to an ‘OWNER’ and to a ‘GROUP’

- `rwxr-xr-x 16 hyunlang(OWNER) staff(GROUP) 512 4 12 2021 text_1.txt`

- every file can be: readable, writable, executable (r, w, x)
  - `-rw -r - - r - -` → `rw-` (ONWER), `r - -` (GROUP), `r - -`(OTHER USERS)

## Change permission on files

`chmod u=r info.txt`

`chmod g=rx info.txt`

`chmod o=x info.txt`

`chmod +x info.txt` → executable to everybody(user, group, others)

`chmod -x info.txt` → nobody has permission to execute

---
### Reference
- https://www.udemy.com/course/bash-shell-scripting-learn-by-creating-6-real-world-scripts/
