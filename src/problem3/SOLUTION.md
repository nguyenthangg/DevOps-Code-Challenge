Provide your solution here:

For this challenge, I used the following steps:
1. Accessing the Server

# When the VM is using 99% of its storage, you may find it difficult to SSH into the server, or the VM might not start at all.

# Increase EBS Storage

To resolve this, first increase the EBS volume size of the VM.
# Attach New EBS Volume (if necessary)

If increasing the existing volume isn’t sufficient, you can attach a new EBS volume to the VM.
# Stop the VM

Stop the VM to safely detach the EBS volume.
# Detach and Mount the Volume

Detach the EBS volume from the original VM and attach it to another instance where you can access 

# Resize the EBS Volume

After cleaning up, resize the EBS volume to the desired size.
# Reattach the Volume

Detach the EBS volume from the second instance and reattach it to the original VM.
Start the VM

Finally, start the original VM again.



2. Check Disk Usage

Run df -h to get an overview of disk usage across all mounted filesystems.

Use du -sh /* to identify which directories are consuming the most space.
Investigate Logs

Check the NGINX logs located typically in /var/log/nginx/ (access logs and error logs).

Review other system logs in /var/log/ for any anomalies or excessive logging.

after check logs we could know what is causing the high disk usage from which services or applications are running.

3. NGINX Configuration for Disk Management
# Log Rotation

Use logrotate to manage NGINX log files. This prevents logs from consuming too much disk space.

# Limit Buffer Sizes

Adjust buffer sizes to minimize temporary files on disk.

# Caching Configuration

Implement caching with limits to control disk usage.

# Set Client Body Size Limit

Limit the size of client request bodies to prevent excessive disk usage.


4. Investigating High Traffic on NGINX
Analyze Access Logs

Check the access logs in /var/log/nginx/access.log.
Use tools like awk or grep to filter logs to identify IP addresses with excessive requests.


5. Prevention Strategies

# Monitor Disk Usage

Implement monitoring tools (e.g., CloudWatch, Datadog) to track disk usage in real-time. Set up alerts for when usage approaches critical levels.

# Backup and AMIs
Combine AMIs and Snapshots: Use AMIs for quick recovery and provisioning, and EBS snapshots for ongoing data protection.

Automate Backups: Set up a schedule to automate the creation of snapshots.

Retention Policies: Implement retention policies to manage old AMIs and snapshots, preventing unnecessary storage costs.