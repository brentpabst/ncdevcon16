Welcome to NCDevCon 2016!!!
===========================
Sample app and other stuff from NCDevCon 2016 talk -  Delivering the Dude: Continuous X.

## Sample App
The sample app is a simple .NET core app with a simple website used to run the samples and demos.

### Running the App
1. Install .NET Core http://dot.NET
1. `git clone https://github.com/brentpabst/ncdevcon16`
1. `cd src`
1. `dotnet restore`
1. `dotnet run`

#### Live Reload
Instead of running `dotnet run` run `dotnet watch run` for live-reload style functionality.

## VMs and Docker
The sample uses three Docker images for Bitbucket Server, Teamcity Server, and a Linux Teamcity Agent.  Four additional Windows VMs are needed to support Octopus, Windows Teamcity agent, and two deployment servers.

### Docker Commands
1. Install a Docker bridge network `docker network create --driver bridge ncdevcon`
1. Install Bitbucket `docker run --name=bitbucket -itd --network=ncdevcon -v /<your data dir>:/var/atlassian/application-data/bitbucket -p 8080:7990 -p 8081:7999 atlassian/bitbucket-server`
1. Install Teamcity Server `docker run --name=teamcity -itd --network=ncdevcon -v /<data dir>:/data/teamcity_server/datadir -v /<log dir>:/opt/teamcity/logs -p 8085:8111 jetbrains/teamcity-server`
1. Install Teamcity Agent `docker run --name=teamcity-agent-2 -itd --network=ncdevcon -v /<data dir>:/data/teamcity_agent/conf -e SERVER_URL="http://teamcity:8111" -e AGENT_NAME="NCDevCon-Agent02" brentpabst/teamcity-agent`
