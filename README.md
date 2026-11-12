
syncmac

A Fish shell function wrapping rsync for fast, reliable file transfers from Linux (NTFS/ext4) to macOS-formatted (HFS+) drives. It features an accurate upfront file scan, a pinned 30-second disk usage monitor, automatic RAM cache flushing, and self-cleaning error logging.

Features

• Accurate Progress Tracking (--no-inc-recursive): Scans the full directory tree upfront so the transfer percentage progresses steadily from 0% to 100% without bouncing backward.


• Pinned Disk Space Monitor: Uses terminal cursor positioning (tput) to pin a live timestamp and df -h readout for your destination drive at the top of the terminal, refreshing every 30 seconds without interrupting the rsync progress bar.

• HFS+ Friendly Defaults (-rth --size-only): Preserves timestamps and folder structures while avoiding cross-filesystem UID/permission conflicts between NTFS/Linux and macOS HFS+ volumes.

• Safe RAM Cache Flushing (sync): Forces Linux to finish writing all buffered data from system memory to the external drive before signaling completion—preventing data loss when unmounting non-journaled HFS+ volumes.

• Self-Cleaning Error Log: Captures any skipped files or I/O errors to ~/skipped_mac_files.txt and automatically deletes the log file if zero errors occurred.

• Clean Interrupt Handling: Uses trap to ensure the background monitor loop terminates cleanly if you abort early with Ctrl+C.

Requirements

• Fish Shell (fish)

• rsync (v3.1.0+ for --info=progress2 support)

• ncurses (tput, pre-installed on almost all Linux distributions)
