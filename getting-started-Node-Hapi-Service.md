So you want to build a new micro service using node.js and all the existing deployment infrastructure, eh? AWesome! You came to the right place. The process isn't too arduous but may seem like a lot of steps at first. Don't fret. We'll be done in no time.

### Prepare for It

First things first. We need to install some things locally to make this work. We need `node.js 4.0` and `npm`. You can get this from [NodeJS.org](https://nodejs.org).

We also need the [FSW Hapi Generator](http://gitlab.fsw.com/acme/generator-fsw-hapi/) and [yeoman](http://yeoman.io/). These can be installed from the [FSW NPM Registry](http://proget.fsw.com/npm-feeds/fsw-npm). NOTE: if yeoman cannot find fsw-hapi generator, pull the repo down locally and 'npm link' it from within the directory

```
npm config set registry http://proget.fsw.com/npm/fsw-npm
npm config set always-auth true
npm install -g yo generator-fsw-hapi
```

Now, let's get a workspace set up locally.

```sh
cd dev
mkdir newApp
cd newApp
```

### Generate It

Populating this new folder with our application is our next goal. Yeoman to the rescue!

Running the hapi app generator will prompt you for a few answers to questions and then create all the files you need.

```sh
$ yo fsw-hapi:app
##############
? What's the base name of your API? newApp
? What's the name of the mongo database this API will use? newAppDb
/Users/jgaylor/dev/acme/testapp/app
   create app/index.js
   create app/package.json
   create app/manifest.js
   create app/config.json
   create app/.gitignore
...
```

Once the app is created we can generate the build scripts as well.

```
$ yo fsw-hapi:build
##############
? What's the name of your team? acme
? What's the name of your app? newApp
? Where is the Git repo located? http://gitlab.fsw.com/acme/newApp.git
identical .gitignore
   create Dockerfile
   create scripts/build.sh
   create scripts/package.sh
   create scripts/publish.sh
   create scripts/deploy_k8s.sh
   create scripts/make_k8s_config.sh
   create scripts/gator_promote.sh
   create scripts/vars.sh
```

At this point you have a new app and the scripts jenkins needs to build it. Now, we need to make a git repo to keep a track of the source code. To do this, go to [GitLab](http://gitlab.fsw.com) and click the green "New Project" button. Create the project as "public" and using the name that matches the Git repo url set in a previous step.

After creating a repo, let's put the code we have in it.

Back in the workspace created earlier, let's run some git commands.

```
# make this folder into a git repo
git init

# track all the files except those ignored by the generatoed .gitignore
git add --all

# make an initial commit
git commit -m "initialize the new app"

# tell the local repo where the origin remote is. use the URL from above
git remote add origin http://gitlab.fsw.com/TEAM/APP.git

# put the code online
git push -u origin master
```

After getting the code onto gitlab, it is time to generate the build jobs on Jenkins.

Navigate to [MaxPower Jenkins](http://k8sminion01.fsw.io:31427/) and go to the [Generate Node.js Janky Jobs](http://minion01.tools.k8s.acme:32303/job/Generate%20Node.js%20Janky%20Jobs/). Then click [Build with Parameters](http://minion01.tools.k8s.acme:32303/job/Generate%20Node.js%20Janky%20Jobs/build?delay=0sec). The values should match those used in the generator before. After the job has finished, you'll need to go to [Manage Jenkins](http://minion01.tools.k8s.acme:32303/manage) and click "Reload Configuration from Disk".

### Build It

[[Explain Release and Snapshot Jobs]]

[[Explain Promotions & Gator]]


### Deploy It

[[ Explain Deploying a gator version to a cluster ]]
