---
ID: 360
post_title: How to Run a Local Copy of Sonar
author: Luc
post_date: 2013-05-02 16:27:39
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/how-to-run-a-local-copy-of-sonar/
published: true
---
(env = cygwin)
1. Download Sonar server
2. Download sonar-runner
3. Edit sonar-runner.bat so it doesn't throw "java.lang.OutOfMemoryError: Java heap space"

These settings work for me:
<code>set SONAR_RUNNER_OPTS=-Xmx512m -XX:MaxPermSize=512m
set SONAR_RUNNER_HOME=C:\\Dev\\Frameworks\\sonar-runner-2.2</code>

Also remove the lines at the end of the file which kill the terminal.

Leave the Sonar server process running in the background and run the Sonar runner periodically to analyse the project. I like to do this with bash functions e.g.
 
<pre class="lang:sh decode:true " >
#start the server
sonar_start(){
  cd /cygdrive/c/sonar-3.5.1/bin/windows-x86-32
  ./StartSonar.bat
}
#run the analysis
sonar_analyse(){
  cd $PROJECT_HOME
  exec /cygdrive/c/Dev/Frameworks/sonar-runner-2.2/bin/sonar-runner.bat
}</pre> 

The functions are sourced in my profile so I can access them with "so" and hit TAB + ENTER.