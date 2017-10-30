# Useful Shell Commands

- `tr -d '\n'` - remove new lines

- [Check existence of input argument in a Bash shell script](https://stackoverflow.com/questions/6482377/check-existence-of-input-argument-in-a-bash-shell-script):
```
if [ $# -eq 0 ]
  then
    echo "No arguments supplied"
fi
```
The $# variable will tell you the number of input arguments the script was passed.
Or you can check if an argument is an empty string or not like:
```
if [ -z "$1" ]
  then
    echo "No argument supplied"
fi
```
The -z switch will test if the expansion of "$1" is a null string or not. If it is a null string then the body is executed.
