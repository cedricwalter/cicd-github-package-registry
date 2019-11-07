# Example to push to Github package registry

# HOW TO
* Clone this project
* Create a global gradle.properties. The global properties file should be located in your home directory:
    * On Windows: C:\Users\<you>\.gradle\gradle.properties
    * On Mac/Linux: /Users/<you>/.gradle/gradle.properties

    with content
    
        `gpr.user=cedricwalter     # OWNER with the GitHub user or organization name that contains the repository you will be publishing the package to or installing packages from`  
        `gpr.key=xxxxxxxxxxxxxxxxx # access token see below`
        
    see https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line

* Change group and version in build.gradle
```
group = 'com.cedricwalter'
version = '1.0-SNAPSHOT'
```

ATTENTION. as expected, SNAPSHOT version can be publisehed more than once, version not (second run return 403 HTTP)

# Create Releases or Snapshots
## locally 
require a global gradle.properties 
`./gradle publish`
## in travis-ci.org
update the secure variable in .travis.yml to match YOUR project credential
```
travis encrypt "GPR_USER=cedricwalter" --add
travis encrypt "GPR_API_KEY=replace-with-matching-api-key" --add
```
that's all!

# Viewing artifacts
Your artifacts are available at https://github.com/cedricwalter/cicd-github-package-registry/packages

# Using your artifacts in gradle
```
repositories {
        mavenCentral() 
        jcenter()
        maven { url 'https://maven.pkg.github.com/cedricwalter'}
    }
```