# s3sync

1. install aws cli
1. clone this repo to $HOME/.s3sync: `git clone https://github.com/sparrc/s3sync.git $HOME/.s3sync`
1. setup AWS access env vars (AWS_DEFAULT_REGION, AWS_SECRET_ACCESS_KEY, AWS_ACCESS_KEY_ID), this user must have s3 read/write access
1. create s3 bucket if you havent already: `aws s3 mb s3://mybucket`
1. create the local directory that you want to sync: `mkdir -p $HOME/s3`
1. write dir and bucket to config file: `echo "{\"syncdir\":\"$HOME/s3\", \"bucket\":\"mybucket\"}" > $HOME/.s3sync/config.json`
1. run s3sync (`$HOME/.s3sync/s3sync`) or setup a daemon (see below)

### Setup launchd daemon:

1. setup AWS access env vars (AWS_DEFAULT_REGION, AWS_SECRET_ACCESS_KEY, AWS_ACCESS_KEY_ID)
1. `eval "echo \"$(cat com.s3sync.plist)\"" | sudo tee /Library/LaunchAgents/com.s3sync.plist`
1. `sudo chmod 755 /Library/LaunchAgents/com.s3sync.plist`
1. `sudo chown root:wheel /Library/LaunchAgents/com.s3sync.plist`
1. `sudo launchctl load -w /Library/LaunchAgents/com.s3sync.plist`
1. check status with `sudo launchctl list | grep s3sync`

