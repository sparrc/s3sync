# s3sync

1. Clone this repo to $HOME/.s3sync
1. setup s3 access and create a bucket
1. `mkdir -p /Users/sparrc/my-synced-dir`
1. `echo '{"syncdir":"/Users/sparrc/my-synced-dir", "bucket":"mybucket"}' > $HOME/.s3sync/config.json`
1. run s3sync (`$HOME/.s3sync/s3sync`) or setup a daemon

### Setup launchd daemon:

1. Setup AWS_ environment variables
1. `eval "echo \"$(cat com.s3sync.plist)\"" | sudo tee /Library/LaunchAgents/com.s3sync.plist`
1. `sudo chmod 755 /Library/LaunchDaemons/com.s3sync.plist`
1. `sudo chown root:wheel /Library/LaunchDaemons/com.s3sync.plist`
1. `sudo launchctl load -w /Library/LaunchDaemons/com.s3sync.plist`
1. check status with `sudo launchctl list | grep s3sync`

