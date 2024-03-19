# env-watcher

Tired of taking care of your .env files? no more. this script automatically uploads all your files to S3 in the background without you having to lift a finger!


This can be converted into a Go executable and used to run an automatic service in the background:
## steps for Linux:

1. Compile your Go code into a binary executable. Assuming your Go code is in a file named main.go, you can compile it like this:
   ```
  go build -o file_watcher main.go
   ```
2. you'll need to run the executable as a background service. By using systemd to create a service that runs the executable in the background.
3. To configure this service to run on startup: You can add a systemd service for the executable and enable it to start at boot.
   For example, to create a systemd service for your Go executable on Linux:
    1. Create a systemd service file, e.g., 'file_watcher.service', in '/etc/systemd/system/':
    ``` [Unit]
Description=File Watcher Service
After=network.target

[Service]
ExecStart=/path/to/file_watcher
Restart=always

[Install]
WantedBy=multi-user.target
```
