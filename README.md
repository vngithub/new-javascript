# test-new-javascript
Steps:
The "/node_modules" directory was not uploaded in the repo, we need to install the required packages (dependencies)
npm install
The "\bundle.js" file was not uploaded in the repo, we need to build the project to produce it
npm run build

### from website https://medium.com/@paooolino/a-modern-javascript-project-setup-b7842955d1d3#.1ftkmjcfb:

Preparing you PC
Install NodeJS. See the NodeJS website for details.
Install Git on your machine. I’m using windows, so I installed the Git for Windows that comes with a nice Git Bash in which I can issue Linux commands.
Setup the project
Create a GitHub account and add a new empty repo.
CD into your projects root and clone the online repo. You will have to setup an SSH key, maintaining the private key on your machine and the public key added to your GitHub account.
git clone git@github.com:<your_github_account>/<your_repo>
This will create a new folder in your projects root. CD into that folder.
3. Initialize the project using NPM.
npm init -y
The -y option stands for not asking a confirm everytime. As a result of this action, a package.json file is created. It contains the project configuration. It is useful for two main reasons:
it keeps track of the libraries used by the project.
it allows to define a command to be launched every time we need to build the project and create the bundle.
4. Install Webpack
npm install --save-dev webpack
That’s it! A “node_modules” folder will be created. It will contain a number of subdirectories that will be automatically added by npm when you install new packages. The save-dev option is for adding webpack in the package.json file.
You will notice that package.json has been automatically updated by npm and now contains “webpack” in the “devDependencies” section.
5. Configure Webpack
The webpack configuration is done in the webpack.config.js file:
module.exports = {
  entry: './src/index.js',
  output: {
    path: './build',
    filename: 'bundle.js'
  }
};
This should be quite clear. It tells where to find the project entry-point, and where to place the output.
6. Install Babel
We’ll not launch Babel directly. Since we’re using webpack for bundling, we’ll use Babel with it to automatically translate (transpile) the source files before bundling.
How to use Babel with Webpack? The official site is quite clearer:

Babel for Webpack: installation and usage
npm install --save-dev babel-loader babel-core
Then add a loader in the webpack config:
module.exports = {
  entry: './src/index.js',
  output: {
    path: './build',
    filename: 'bundle.js'
  },
  module: {
    loaders: [{ 
      test: /\.js$/, 
      exclude: /node_modules/, 
      loader: "babel-loader" 
    }]
  }
};
With this, every .js file encountered by Webpack will be processed by Babel first. Babel needs to be configured. We want it to translate ES6 to current JavaScript.
7. Tell Babel what to do
Babel features are packed in separate libraries named presets. To translate ES6 we need to install the following:
npm install --save-dev babel-preset-es2015
The Babel configuration is saved in the .babelrc file. Create it with the following content:
{
  "presets": ["es2015"]
}
Note: if you are on Windows, you won’t be able to create a file whose name begins with a full stop. You can create the file using the Git Bash, sending the “touch .babelrc” command.
8. Install jQuery
No more need to download the jQuery code and manually place in your project folder. Just give
npm install --save jquery
and the jQuery library is available for import.
import $ from 'jquery'
jQuery was saved in the “dependencies” section, because it’s a library used by the runtime code. The other libraries installed so far, instead, need to be used to build the project. Again, query StackOverflow for details.
When you need a library, you should check the corresponding npm page (for jQuery: https://www.npmjs.com/package/jquery). It contains useful information about installation and usage in the Node environment.

The jQuery npm page.


