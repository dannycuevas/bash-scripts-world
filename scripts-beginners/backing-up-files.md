### **1. Backing Up Configuration Files**

Imagine you want to back up all `.conf` files from `/etc` into your home directory’s `backup` folder. A beginner-friendly loop looks like this:

```
#!/bin/bash
mkdir -p ~/backup

for conf in /etc/*.conf; do
	echo "Backing up $conf..."
	cp "$conf" ~/backup/
done

echo "All .conf files have been backed up to ~/backup."
```

- **`for conf in /etc/*.conf; do …; done`**  
    Loops over each file ending in `.conf` in `/etc`.
    
- **`conf`**  
    Is the loop variable—you could name it anything (e.g. `file`, `config`).
    
- **`cp "$conf" ~/backup/`**  
    Copies the current file into your `~/backup` directory.
    
- **`echo`**  
    Gives you feedback on what’s happening.
