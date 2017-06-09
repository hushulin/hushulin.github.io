##### install nodejs on windows
1. links to https://nodejs.org/en/
2. download the v6.11.0 LTS (long term support)
3. wait a minute...
4. install it `D:\Program Files\nodejs\`
5. finished
##### install git bash on windows
1. https://git-scm.com/download/win
2. download the git-2.13.0-64-bit.exe in auto mode (do not manual operation)(fast download rate to use thunder)
3. install git bash only (use cli mode only)
4. `D:\Program Files\Git`
5. finished
##### install npm
npm is built-in nodejs by this version
##### init git repository sunny
1. git init
2. git remote add origin ssh://git@192.168.1.101:8822/wuyi/sunny.git
3. git add .
4. git commit
5. git push -u origin master
6. windows ssh key gen (do it first)
	1. ssh-keygen.exe -t rsa -C "hushulin@jiuchunjiaoyu.com"
	2. copy the pub to webserver. (add ssh keys)
	3. redo up lists
##### install webpack2.0 + vue2.0
1. npm init
2. npm install --save vue (2.3.4) (install vue2.0)
3. npm install --save-dev webpack@^2.1.0-beta.25 webpack-dev-server@^2.1.0-beta.9 (install webpack2.0 contains web server)
4. npm install --save-dev babel-core babel-loader babel-preset-es2015 (install babel)(to translater es6)
5. npm install --save-dev vue-loader vue-template-compiler (resolver .vue templates)
6. npm install --save-dev css-loader file-loader (resolver .css styles)
7. npm install -g webpack@^2.1.0-beta.25 (global install to use `webpack` command)
8. npm install -g webpack-dev-server@^2.1.0-beta.9 (`webpack-dev-server`)
##### wait for me to code the app framework
### todo:
1. mult index
2. base application object
3. easy router
4. easy object-relation-model
5. standard modules
6. etc...