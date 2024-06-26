# env-watcher

Tired of taking care of your .env files? no more. this script automatically uploads all your files to S3 in the background without you having to lift a finger!

This can be converted into a Go executable and used to run an automatic service in the background:


## steps for Linux:

1. set up the list of env vars required to connect with AWS
   
   ```
   DIRECTORY_TO_WATCH
   AWS_ACCESS_KEY_ID 
   AWS_SECRET_KEY    
   AWS_REGION        
   AWS_BUCKET_NAME   
   ```


2. Compile your Go code into a binary executable. Assuming your Go code is in a file named main.go, you can compile it like this:



```
go build -o file_watcher main.go
```

3. you'll need to run the executable as a background service. By using systemd to create a service that runs the executable in the background.

4. To configure this service to run on startup: You can add a systemd service for the executable and enable it to start at boot.
   For example, to create a systemd service for your Go executable on Linux:
   
   1. Create a systemd service file, e.g., 'file_watcher.service', in '/etc/systemd/system/':
      
      ```
      [Unit]
      Description=File Watcher Service
      After=network.target
      
      [Service]
      ExecStart=/path/to/file_watcher
      Restart=always
      
      [Install]
      WantedBy=multi-user.target
      ```
      
      Replace /path/to/file_watcher with the actual path to your compiled Go executable.
   
   2. Enable the service to start at boot:
      
      ```
      sudo systemctl enable file_watcher.service
      ```
   
   3. Start the service:
      
      ```
      sudo systemctl start file_watcher.service
      ```

This will start your Go executable as a background service and ensure it starts automatically on system boot.

For Windows, you would follow similar steps, but you'll need to create a Windows service instead of a systemd service. You can use tools like NSSM (Non-Sucking Service Manager) to create and manage Windows services.

---

You can try restarting the service again when making some changes using the following command:

```
sudo systemctl restart file_watcher.service
```

If the service still fails to start, check the systemd journal for more detailed error messages that can help pinpoint the issue:

```
sudo journalctl -xe
```
