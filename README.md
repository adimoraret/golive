# Live stream with AWS MediaLive and MediaStore
GoLive - this is a boilerplate to live stream using AWS MediaLive and MediaStore.
I use serverless framework to create the following AWS resources:
- MediaLive Channel
- MediaLive Input
- MediaLive InputSecurityGroup
- MediaStore Container
- IAM Role

## Setup
1. Make sure you have installed [serverless framework cli](https://www.serverless.com/framework/docs/getting-started/) - Required
1. Configure [AWS credentials](https://www.serverless.com/framework/docs/providers/aws/cli-reference/config-credentials/): - Required
1. Install [AWS cli](https://aws.amazon.com/cli/) - Optional
1. Clone this repo
1. Deploy from bash: `serverless deploy`

## Live Stream software configuration
1. Get input's destination url using aws cli `aws medialive list-inputs` or by logging in to `aws.amazon.com` MediaLive -> Inputs -> Destination A
1. Open a live streaming software(I use [OBS](https://obsproject.com/) in this example)
1. In OBS, add a `Video Capture Device` object from in the `Sources` window
1. Click on `Settings` and navigate to `Stream` section
1. Select `Service` as `Custom`, `Server` as `rtmp://xxxxxxxx:yyyy/golive/`
1. Add the last part of the url (which it should be `now` if you haven't done any changes to the code) as `Stream Key`

## Live Stream
1. Start the GoLive channel using aws cli: `aws medialive list-channels` to get channel's id. Then `aws medialive start-channel --channel-id xxxxxxx`. Or in `aws.amazon.com` navigate to MediaLive -> Channels -> GoLive -> Start channel
2. After channel starts, go to OBS and click `Start Streaming`
3. Done. You should be live at `https://xxxxxx.data.mediastore.{your-region}.amazonaws.com/mystreams/stream.m3u8`. You can get the full link from `aws.amazon.com` navigate to MediaStore -> click on your item -> select the `m3u8` file -> select the object's name.