# Operators
- | -> Runs a command using the last command as input 
    
    e.g. 
    
    ```
    # This will use the doc.txt content to feed the grep function
    cat doc.txt | grep people
    ```
- && -> The And operator, used to run multiple commands in one line

```
# Installing two python libraries in one line
pip install pandas && pip install numpy
```

- & -> This is the background (daemon) command. makes the preceding commands to the left run in background or daemon mode.

```
# This will run a python script in the background
python3 main.py &
```


# Grep
Used for searching through a string

Useful Flags:

- -i -> This flag will make the search case insensitive.

