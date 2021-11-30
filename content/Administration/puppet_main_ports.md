# Puppet Main ports

[INDEX](../../README.md)

1. **22**: Code manager to fetch code from git server (outbound).
1. **443**: 
   1. Code manager to fetch code from git server (outbound).
   1. Provides access to the console (inbound).
1. **4433** (inbound):
   1. Classifier / Console API endpoint.
   1. Primary server communicates to console over this port.  
1. **5432** (inbound): PE-Database main port.
1. **8080/8081(SSL)** (inbound): PuppetDB service main port: status checks, requests, etc.
1. **8140** (inbound): Puppet Server main port that communicates with Console services, certificate requests, compilers status checks, installation scripts, etc.
1. **8142** (inbound): Orchestator and "Run Puppet" button use this port to accept responses/traffict via PXP agent.
1. **8143** (inbound): Orchestator use this port to accept connections from PCP brokers. 
2. **8170** (inbound): used by Code manager services to deploy environments, receive webhooks and API calls.