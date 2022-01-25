# Bash Shell Basics
- #! /bin/bash → bash로 실행되는 스크립트임을 알려준다.
    - 써주지 않아도 default가 bash 실행이므로 제대로 실행되긴 하지만 스크립트가 여러 종류(python, java ...)가 있으므로 명시해주는 것이 좋다.

## If on Strings

- if statements must have a space at the end of `[`, `]`

```bash
#/ bin/bash

echo -e "\n The program continue"

read -p "say something to greet me!" d  # user input을 d에 저장
echo "============================="

if [ "$d" == "helllo" ]; then
	echo "hello to you!"
elif [ "$d" == "good morning" ]; then
	echo "morning to you"
elif [ "$d" == "bye" ]; then
	echo "bye to you"
else
	echo "have a nice day anyway..."
fi

## Empty String
if [ -z "$d" ]; then
	echo "Empty String"
fi

## NON Empty String
if [ -n "$d" ]; then
	echo "NON Empty String"
fi

if [ ! -z "$d" ]; then
	echo "NOT Empty String"
fi
```

## If on Numbers

```bash
#! /bin/bash

read -p "give me a number" numb
echo "===================="

# Number Equal to 18
if [ $numb -eq 18 ]; then
	echo "It is 18"
else 
	echo "not 18"
fi

# Number Not Equal to 18
if [ $numb -ne 18 ]; then
	echo "Not 18"
fi

# Number Lower Than 18
if [ $numb -lt 18 ]; then
	echo "lower than 18"
fi

# Number Greater Than 18
if [ $numb -gt 18 ]; then
	echo "lower than 18"
fi

# Lower Or Eqaul to
if [ $numb -le 18 ]; then
	echo "Lower of Equal to 18"
fi

# Greater Or Equal to
if [ $numb -ge 18 ]; then
	echo "Greater or Equal to 18"
fi

```

## If on Files

```bash
#! /bin/bash

read -p "give me a filename" myfile
echo "===================="

if [ -e "$myfile" ]; then
	echo "the file exists"
else
	"Doesn't exist"
fi

# If Directory
if [ -d "$myfile" ]; then
	echo "file exists and is a Directory"
fi

# Regular file(not directory, not link...)
if [ -f "$myfile" ]; then
	echo "file exists and it is a regular file"
fi

# Not Empty
if [ -s "$myfile" ]; then
	echo "file exists and has length > 0"
fi

# Empty
if [ ! -s "$myfile" ]; then
	echo "file exists and has length = 0"
fi

# ========================================== #

# Readable
if [ -r "$myfile" ]; then
	echo "file exists and readable"
else
	echo "NOT readable"
fi

# Writable
if [ -w "$myfile" ]; then
	echo "file exists and writable"
else
	echo "Not Writable"
fi

# Executable
if [ -x "$myfile" ]; then
	echo "file exists and exectuable"
else
	echo "NOT Executable"
fi
```

## Logic Conditions

```bash
## AND
if [ $numb -gt 2 -a $numb -lt 10 ]; then
	echo "3<numb<10"
fi

## OR
if [ $numb -lt 3 -o $numb -gt 10 ]; then
	echo "num<3 OR num>10"
fi

## Example - file executable AND also NON Empty
myfile="Frank.sh"
if [ -s "$myfile" -a -x "$myfile" ]; then
	echo "$myfile NON Empty AND Executable"
fi
```

## Modern way to use IF Conditions...

```bash
if [[ $numb lt 10 ]]; then
	echo "numb < 10"
fi

if [[ -s "$myfile" ]]; then
	echo "$myfile NON Empty"
fi

### Difference are the symbol for
# AND --> &&
# OR --> ||

if [ $numb -gt 2 && $numb -lt 10 ]; then
	echo "3<numb<10"
fi

## OR
if [ $numb -lt 3 || $numb -gt 10 ]; then
	echo "num<3 OR num>10"
fi
```

## For Loop

```bash
for i in {1,2,3,4}; do
	echo -e "hi there \n"
	echo "the value of i is: $i"
done

for i in {a, b, c, d}; do
	echo "the value of i is: $i"
done

echo "------------------------"

for i in {21, "my cat", 1, 2, "hello", "END"}; do
	echo "the value of i is: $i"
	touch "%{i}.xls"
done

echo "------------------------"

#### BRACE EXPANSION
for i in {b..f}_file ; do
	echo "the value of i is: $i"
done
# b_file, c_file, ..., f_file

#### FILE
for i in ./*.txt; do
	echo "the file is: $i"
done

############# MODOERN WAY FOR LOOP FOR NUMBERS

for (( i = 0; i <25l i=i+1 )); do
	echo "$i"
done
# 0, 3, 6, ..., 24
```
