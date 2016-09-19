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

*Note: I modified the base JetBrains TeamCity agent Docker image to make it compatible with handling .NET Core builds.  I made my own image so others might be able to get past the weird setup stuff I had to do.* 

### Docker Commands
1. Install a Docker bridge network `docker network create --driver bridge ncdevcon`
1. Install Bitbucket `docker run --name=bitbucket -itd --network=ncdevcon -v /<your data dir>:/var/atlassian/application-data/bitbucket -p 8080:7990 -p 8081:7999 atlassian/bitbucket-server`
1. Install Teamcity Server `docker run --name=teamcity -itd --network=ncdevcon -v /<data dir>:/data/teamcity_server/datadir -v /<log dir>:/opt/teamcity/logs -p 8085:8111 jetbrains/teamcity-server`
1. Install Teamcity Agent `docker run --name=teamcity-agent-2 -itd --network=ncdevcon -v /<data dir>:/data/teamcity_agent/conf -e SERVER_URL="http://teamcity:8111" -e AGENT_NAME="NCDevCon-Agent02" brentpabst/teamcity-agent`

### VM Info
Currently Octopus requires a Windows machine to run the server component.  The TeamCity Octopus plugin (which handles deployment communication) requires a Windows build agent as well.  I also used two Windows 2012R2 boxes to demo IIS deployments of the sample app.  On my Mac I run Parallels desktop which allowed for simple 2012R2 VMs to be spun up.  Each VM only got 1-2 CPUs and about 1GB of RAM.  Follow the normal install process for Octopus and IIS/.NET Core, it's a piece of cake.
