---
layout: post
title: "Intelij increase licesnse evaluation"
comments: true
categories: devops
---

### Intelij increase licesnse evaluation

### Increase Evaluation in Linux

Create file reset_trail.sh with content:
```
 #!/bin/bash
 
 ## declare array of tools
 declare -a tools=(
     "DataGrip"
     "CLion"
     "Rider"
     "PhpStorm"
     )
 
 for tool in "${tools[@]}"
 do
     echo "removing evaluation key for $tool"
     rm -rf ~/.$tool*/config/eval
     rm -rf ~/.java/.userPrefs/jetbrains/${tool,,}
 done
 
 for tool in "${tools[@]}"
 do
     echo "resetting evalsprt in options.xml for $tool"
     sed -i '/evlsprt/d' ~/.$tool*/config/options/options.xml
 done
 
 echo "resetting evalsprt in prefs.xml"
 sed -i '/evlsprt/d' ~/.java/.userPrefs/prefs.xml
 
 for tool in "${tools[@]}"
 do
     echo "change date file for $tool"
     find ~/.$tool* -type d -exec touch -t $(date +"%Y%m%d%H%M") {} +;
     find ~/.$tool* -type f -exec touch -t $(date +"%Y%m%d%H%M") {} +;
 done
```


```
echo "removeing evaluation key"
rm  -rf ~/.IntelliJIdea*/config/eval
rm  -rf ~/.GoLand*/config/eval
rm  -rf ~/.WebStorm*/config/eval

rm -rf ~/.java/.userPrefs/jetbrains/goland
rm -rf ~/.java/.userPrefs/jetbrains/idea
rm -rf ~/.java/.userPrefs/jetbrains/webstorm

echo "resetting evalsprt in options.xml"
sed -i '/evlsprt/d' ~/.IntelliJIdea*/config/options/options.xml
sed -i '/evlsprt/d' ~/.GoLand*/config/options/options.xml
sed -i '/evlsprt/d' ~/.WebStorm*/config/options/options.xml

echo "resetting evalsprt in prefs.xml"
sed -i '/evlsprt/d' ~/.java/.userPrefs/prefs.xml


echo "change date file"
find ~/.IntelliJIdea* -type d -exec touch -t $(date +"%Y%m%d%H%M") {} +;
find ~/.IntelliJIdea* -type f -exec touch -t $(date +"%Y%m%d%H%M") {} +;

find ~/.GoLand* -type d -exec touch -t $(date +"%Y%m%d%H%M") {} +;
find ~/.GoLand* -type f -exec touch -t $(date +"%Y%m%d%H%M") {} +;

find ~/.WebStorm* -type d -exec touch -t $(date +"%Y%m%d%H%M") {} +;
find ~/.WebStorm* -type f -exec touch -t $(date +"%Y%m%d%H%M") {} +;
```
```
rm -rf ~/Library/Preferences/PyCharm2018.1/eval/PyCharm181.evaluation.key
rm -rf ~/Library/Preferences/PyCharm2018.1/options/options.xml
```

# Extends Evaluation in Windows

###### Intellij Evaluation Problem:

If you want to increase evaluation periods to more 30 days you can follow the bellow steps:

- Step 1: Exit intellij software.
- Step 2 : Remove all intellij/pycharn/webstrom home cash folder (like: C:\Users\<Username>/.IntelliJIdea201…..)
- Step3: Windows key + R  type regedit & press enter(open registry)
- Delete evlsprt, evlsprt 1, evlsprt 2 ……. files from jetbrains software.
![Image](../../../../static/img/evaluationProblem.PNG)


![Image](../../../../static/img/intelijCashfolder.PNG)


![Image](../../../../static/img/registry.PNG)


![Image](../../../../static/img/regedit.PNG)


![Image](../../../../static/img/regieditDelete.PNG)


- Open Intelij & evaluate for 30 days & enjoy.







