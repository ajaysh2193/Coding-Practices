# Below are the steps to update node version from 6 to 14

## Installing nvm:

Nvm (node version manager) is a tool that can be used to switch between different versions of node without much hassle, to download it in ubuntu/mac, below are the commands:

- curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
- source ~/.profile
- To list the versions available use; nvm ls-remote
- To install a specific version of node use; nvm install 14 (change the number from 14 to something else for any version)
- To see your installed versions of node use; nvm ls
- To use a specific version; nvm use 14 or nvm use 6
- To run a script without switching the node versions use; nvm exec 14 server.js (use if needed)

## Setting up node version:

Some modules will cause errors while installing, so check for the specific errors and try to update the versions in package.json

- Delete the existing node_modules folder inside the /mean folder.
- Clean up/Verify the cache; npm cache clean / npm cache verify
- Remove asyncawait and grunt-node-inspector from package.json
- Remove relevant code for asyncawait in the project (try to use async library)
- Update the grunt-express-server version to 0.5.4
- Update hummus version to 1.0.110

Optional: If the steps do not work, comment the line 'env: all' from GruntFile.js to make it work!  
