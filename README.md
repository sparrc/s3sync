# s3sync

1. Clone this repo to $HOME/.s3sync
1. setup s3 access and create a bucket
1. mkdir -p /Users/sparrc/my-synced-dir
1. echo '{"syncdir":"/Users/sparrc/my-synced-dir", "bucket":"mybucket"}' > $HOME/.s3sync/config.json
1. $HOME/.s3sync/s3sync

