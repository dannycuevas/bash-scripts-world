2. Checking Status of Common Services**

Say you have a few services you always check after a reboot. You can automate it:

```
#!/bin/bash
services=("nginx" "mysql" "docker")

for svc in "${services[@]}"; do
	echo "Checking $svc status..."
	systemctl is-active --quiet "$svc" && \
		echo "$svc is running" || \
		echo "$svc is NOT running"
done
```

- **`services=("…")`**  
    Defines an array of service names.
    
- **`"${services[@]}"`**  
    Expands to each service in turn.
    
- **`systemctl is-active --quiet`**  
    Tests if the service is running (exit code `0` means “yes”).
    
- **`&& … || …`**  
    Runs the first `echo` if the check succeeds, otherwise the second.
