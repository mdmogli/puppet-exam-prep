# Analyzing Puppet Runs

[INDEX](../../README.md)

### Life cycle of a puppet run:

-  Agent -> Master: Request handshake (SSL verification)
-  Master -> Agent: Accept handshake (SSL verification)
-  Agent -> Master: Request node object (A node object consists of the node's facts, environment, node parameters and classes.)
-  Master         : Node object prepared by node terminus (ussualy is plain, that is blank values)
-  Master -> Agent: Sends node object.
-  Agent          : Makes changes based on node object (if any)
-  Agent -> Master: Request catalog and send facts to the master
-  Master         : evaluates -> variables, main manifest, modules and associated modules, node objects values.
-  Master -> Agent: Sends catalog to agent.
-  Agent          : Makes changes based on catalog (if any)
-  Agent -> Master: Returns reports

### event types on console:

1. Failure: A property was out of sync; Puppet tried to make changes, but was unsuccessful.
1. Corrective change: setting on a system that does not match the setting you defined for it in your Puppet code (enforce).
1. Intentional change: are any changes that you make yourself, in your Puppet code.
1. Corrective no-op: same as 2 but without changes (noop).
1. Intentional no-op: same as 3 but without changes (noop).
1. Skip: A prerequisite for this resource was not met and puppet skip the resource.
