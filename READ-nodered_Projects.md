## Working with NodeRed Projects AND remote repos

### Introduction

The new feature since NodeRed v0.18.3 Projects has lots of potential, for building NodeRed templates for multiple deploy, such as in the dabar case where many clients industrial water use are displayed in their own web client, but the NodeRed flows are the same.  

Herewith steps to configure it for the following use case:  
- Develop on NodeRed, (on docker on Mac);  
- Commit changes in a NodeRed 'Project' to local git under NodeRed;  
- then to do a remote commit to git on bitbucket (you can have private repo's, unlike on github, but any git repo will work);  
- and lastly to use Ansible to deploy the runtime, and a bash script to unpack the NodeRed code to the folders of each of the clients.  

### Links to useful info on Projects, and Bitbucket

- NodeRed Projects feature - [NodeRed docs](https://nodered.org/docs/user-guide/projects/)
- Setting up bitbucket ssh public key - [Atlasian](https://confluence.atlassian.com/bbkb/permission-denied-publickey-302811860.html)



### Screens (move)

- NodeRed:
  - Project Settings > Settings > add remote :  

    ![add remote](images/nodered_addremote.png)  

  - Settings > Git config > add key :  

    ![add key](images/nodered_addremote.png)
