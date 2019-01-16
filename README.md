# aws-autoscaling
A micro-framework that handles the autoscaling life cycle hook calls to init.d type scripts inside to instance and responds to scale-out and scale-in events

# General

The original idea was from official amazon's repo and project [aws-samples/aws-lambda-lifecycle-hooks-function](https://github.com/aws-samples/aws-lambda-lifecycle-hooks-function)

The hole system used autoscaling life cicle hooks to trigger a lambda function that calls the System Manager to execute a script inside to instance. Instance must already have installed the ssm-agent (new instances of amzn-linux and amzn-linux-2 already had this package).
The image must have inside a folder stracture and a script that called from ssm agent.
The stracture has 2 folders:
* ec2-scalein.d
* ec2-scaleout.d

Any runnable script in these folders run in the corresponding event of the instance (if the instance is member of Autoscaling Group). 

The framework has internal system to heartbeat the hook event or to abandon or continue the scale. 
The scripts must return 0 if the execution was success else any other code will cause abandon to the scale event. 

Instance must has installed the aws-cli and correct permitions to call:
* autoscaling:RecordLifecycleActionHeartbeat
* autoscaling:CompleteLifecycleAction

Suggested way is to put a role on instance and role propagate the permitions

# Autoscale life cicle event

# CloudWatch rule

# Lambdas
Lambda need permition to allow ssm:SendCommand 
