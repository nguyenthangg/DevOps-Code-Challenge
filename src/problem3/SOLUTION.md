Provide your solution here:

For this challenge, I used the following steps:
# Accessing the Server

1. When the VM is using 99% of its storage, you may find it difficult to SSH into the server, or the VM might not start at all.

2. Increase EBS Storage

To resolve this, first increase the EBS volume size of the VM.

3. Attach New EBS Volume (if necessary)

If increasing the existing volume isn’t sufficient, you can attach a new EBS volume to the VM.

4. Stop the VM

Stop the VM to safely detach the EBS volume.

5. Detach and Mount the Volume

Detach the EBS volume from the original VM and attach it to another instance where you can access 

6. Resize the EBS Volume

After cleaning up, resize the EBS volume to the desired size.

7.  Reattach the Volume

Detach the EBS volume from the second instance and reattach it to the original VM.

Start the VM

Finally, start the original VM again.



# Check Disk Usage

Run df -h to get an overview of disk usage across all mounted filesystems.

Use du -sh /* to identify which directories are consuming the most space.
Investigate Logs

Check the NGINX logs located typically in /var/log/nginx/ (access logs and error logs).

Review other system logs in /var/log/ for any anomalies or excessive logging.

after check logs we could know what is causing the high disk usage from which services or applications are running.

# NGINX Configuration for Disk Management
1. Log Rotation

Use logrotate to manage NGINX log files. This prevents logs from consuming too much disk space.

2. Limit Buffer Sizes

Adjust buffer sizes to minimize temporary files on disk.

3. Caching Configuration

Implement caching with limits to control disk usage.

4. Set Client Body Size Limit

Limit the size of client request bodies to prevent excessive disk usage.


5. Investigating High Traffic on NGINX
Analyze Access Logs

Check the access logs in /var/log/nginx/access.log.
Use tools like awk or grep to filter logs to identify IP addresses with excessive requests.


# Prevention Strategies

1. Monitor Disk Usage

Implement monitoring tools (e.g., CloudWatch, Datadog) to track disk usage in real-time. Set up alerts for when usage approaches critical levels.

2. Backup and AMIs

Combine AMIs and Snapshots: Use AMIs for quick recovery and provisioning, and EBS snapshots for ongoing data protection.

Automate Backups: Set up a schedule to automate the creation of snapshots.

Retention Policies: Implement retention policies to manage old AMIs and snapshots, preventing unnecessary storage costs.