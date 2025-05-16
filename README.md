# s3sync

1. install awscli (optional: install xz)
2. setup AWS access using `aws configure`, this user must have s3 read/write access
3. clone and setup s3sync on machine: 
```bash
# clone this repo to ~/.s3sync
git clone https://github.com/sparrc/s3sync.git $HOME/.s3sync
# write config file. syncdir is the local synced directory. bucket is the s3 bucket.
cat << EOF > $HOME/.s3sync/config
BUCKET="myBucket"
AWS_PROFILE="default"
ARCHIVE_INTERVAL="120"
SYNC_DIR="/Users/sparrc/s3"
EOF
```
4. create s3 bucket if you havent already: `aws s3 mb s3://mybucket`
5. setup a daemon (see below)

### Setup systemd daemon (linux):

```bash
cd $HOME/.s3sync
eval "echo \"$(cat s3sync.service)\"" | sudo tee /etc/systemd/system/s3sync.service
sudo systemctl daemon-reload
sudo systemctl enable s3sync
sudo systemctl start s3sync
```

### Setup launchd daemon (macOS):

```bash
cd $HOME/.s3sync
eval "echo \"$(cat s3sync.plist)\"" | sudo tee /Library/LaunchAgents/s3sync.plist
sudo chmod 755 /Library/LaunchAgents/s3sync.plist
sudo chown root:wheel /Library/LaunchAgents/s3sync.plist
sudo launchctl load -w /Library/LaunchAgents/s3sync.plist
```

