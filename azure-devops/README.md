
# Running self hosted Agent on Linux and use the agent in our azure devops pipeline



Install and create the agent

mkdir azure-agent && cd azure-agent
Wget https://vstsagentpackage.azureedge.net/agent/3.243.1/vsts-agent-linux-x64-3.243.1.tar.gz

~/azure-agnet$ tar zxvf ~/Downloads/vsts-agent-linux-x64-3.243.1.tar.gz

Configure the agentDetailed instructions
~/azure-agnet$ ./config.sh


run agent:
~/myagent$ ./run.sh





To run agent in backend:
sudo ./svc.sh install

sudo ./svc.sh start

sudo ./svc.sh status
