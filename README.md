

# ec2-spot-jenkins-plugin
The EC2 Spot Jenkins plugin launches EC2 Spot instances as worker nodes for Jenkins CI server, 
automatically scaling the capacity with the load. 

# SpotFleet
This plugin uses Spot Fleet to launch instances instead of directly launching them by itself. 
Amazon EC2 attempts to maintain your Spot fleet's target capacity as Spot prices change to maintain
the fleet within the specified price range. For more information, see 
[How Spot Fleet Works](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-fleet.html).

# Usage
You'll need an AWS account to use this plugin, you can get one at [AWS]( http://aws.amazon.com/ec2/ "AWS"). 
Once you have an account, create an IAM user with sufficient permissions to launch Spot Fleets ( 
[Spot Fleet Prerequisites](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-fleet-requests.html#spot-fleet-prerequisites 
"Spot Fleet Prerequisites") ) and get its AWS credentials.

Then you need to set up a fleet that will serve as the build fleet for Jenkins. You can use the 
[AWS console]( http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-fleet-requests.html#create-spot-fleet )
to launch it or AWS CLI tools. Make sure that you specify an SSH key that will be used later by Jenkins.

Once the fleet is launched, you can set it up by adding a new **EC2 Fleet** cloud in the 
"Manage Jenkins" > "Configure System" menu of Jenkins.

# Scaling
You can specify the scaling limits in your cloud settings. By default, Jenkins will try to scale fleet up
if there are enough tasks waiting in the build queue and scale down idle nodes after a specified idleness period.

You can use the History tab in the AWS console to view the scaling history. 
