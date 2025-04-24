

- For "`ifelse`" condition, in any programming language, the behavior will always be the same, so it does not depend of any programming language
- But, the syntax is different from programming language to programming language

## **Bash "if else" loops** 

- You start with "`if`" 
	- and then provide what is the "expression", or "condition", that is required to be met

```
if [expression]
```

- So "if" the condition is met, then you will say what needs to happen

```
if [expression]
then
	commands
	commands
```

- But, if the condition is not met, then we go to the "`else `" condition
	- and from that condition, execute some other actions
	- finally, close the "if" loop with "`fi`" on your script

```
if [expression]
then
	commands
	commands
else
	commands
	commands
fi
```

### Example
```
a=4
b=10

if [$a > $b ]
then
	echo "a is greater than b"
else
	echo "b is grater than a"
fi
```


## **Bash "for" loops**

- This is you wanting to execute an "action" but "continuously" 
- Like you want to do multiple iterations of an action

- "`for`" will be the "condition" specifically between brackets
- If the condition is met, then do a specific action
- And then increment the condition until the "last value" of the original "condition" is reached 

- And close the condition with the "`done`" statement
	- Everything between `do` and `done` is the "body of the loop"
	- and it runs "once" per item

```
for i in {1..100}; do echo $i; done
```

- A better example
```
for symbol in {1..5}; do
	echo "$symbol"
done
```

Output:
```
1
2
3
4
5
```

### Customizing the Parts
|Part|What You Can Change|
|---|---|
|Loop variable name|`i`, `n`, `count`, `filename`, etc.|
|Sequence/braced list|`{1..100}`, `{a..z}`, `apple banana cherry`, `"$@"`|
|Body command|Any valid Bash command: `echo`, `cp`, `grep`, function calls, etc.|
|Variable expansion|`$i` for loop var, `$1/$2` for script args, `$_` for last arg|
### Real-World Example
Print every `.log` file in a directory:
```
for logfile in /var/log/*.log; do
	echo "Processing $logfile"
	# maybe gzip "$logfile"
done
```

Here:
- `logfile` is the loop variable.    
- The list is all files matching `/var/log/*.log`

### Key Takeaway

- **`for VAR in LIST; do …; done`** loops over each item in LIST.
    
- Use **`$VAR`** to refer to that item inside the loop.
    
- **`$1, $2…`** are only for script/function arguments, not loop variables.

