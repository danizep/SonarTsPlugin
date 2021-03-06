#Basic setup example
This sample project can be analysed by SonarQube to demonstrate:

* Linting information from ```tslint```, configured via a ```tslint.json``` file
* Code coverage metrics from an LCOV file

You can see a live example of the results of analysing this project at [https://sonar.pablissimo.com](https://sonar.pablissimo.com/dashboard?id=com.pablissimo.sonar%3Abasic-setup).

##Building and analysing

* Run ```npm install``` from the cloned repo folder
* Run ```npm test``` to regenerate code coverage information
  * You don't *need* to perform this step, a coverage file is already checked into the repository

To analyse with SonarQube just run ```sonar-scanner -X``` from the cloned repo folder.

* The -X flag will give us diagnostic information during the run, so you can see what the plugin is up to

##Breaking down the sonar-project.properties file

The sample has a ```sonar-project.properties``` file that controls how the analysis gets run. We haven't specified anything here that isn't its default or automatically detected - these are explained under the table.

<table>
<thead><tr><th>Line</th><th>Description</th></tr></thead>
<tbody>
<tr><td>sonar.projectKey=com.pablissimo.sonar:basic-setup</td><td>Unique string that identifies this project to SonarQube, differentiating it from any other project that's being analysed by the same server</td></tr>
<tr><td>sonar.projectName=Basic project setup example</td><td>Name of the project, which will show in the SonarQube admin interface</td></tr>
<tr><td>sonar.projectVersion=1.0</td><td>Version of the project</td></tr>
<tr><td>sonar.sources=./src</td><td>The path to the source code for your project - essentially describing the files to be analysed. Specified relative to the sonar-project.properties file.</td></tr>
<tr><td>sonar.sourceEncoding=UTF-8</td><td>The encoding of your source files - typically UTF-8 is fine, unless you know you're using a different encoding</td></tr>
<tr><td>sonar.exclusions=node_modules/**</td><td>The files that should be excluded from analysis - here, we don't want to include anything in the node_modules folder as it's full of TypeScript and JavaScript that's got nothing to do with us and would muddy the analysis</td></tr>
<tr><td>sonar.tests=./test</td><td>The path to any test code you have for your project, which will be excluded when calculating code coverage metrics - but these files are still analysed by the plugin for linting issues</td></tr>
<tr><td>sonar.ts.coverage.lcovReportPath=coverage/lcov.info</td><td>The path to an LCOV-format file describing code coverage for your project. Typically generated by tools like Karma, Istanbul (with Istanbul-remap), Chutzpah etc</td></tr>
</tbody>
</table>

Several settings are automatically detected (and you'll see these listed in the LCOV output):

* The path to ```tslint``` is automatically detected as within the node_modules folder
* The location to the ```tslint.json``` file that configures tslint is automatically assumed to be the same folder as the ```sonar-project.properties``` file
