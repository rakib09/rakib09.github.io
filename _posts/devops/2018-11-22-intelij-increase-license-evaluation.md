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

#rm -rf ~/.java/.userPrefs/prefs.xml
#rm -rf ~/.java/.userPrefs/jetbrains/prefs.xml

# Reset PyCharm
rm -rf ~/.config/JetBrains/PyCharm*/eval
# rm -rf ~/.config/JetBrains/PyCharm*/options/other.xml
sed -i -E 's/<property name=\"evl.*\".*\/>//' ~/.config/JetBrains/PyCharm*/options/other.xml
rm -rf ~/.java/.userPrefs/jetbrains/pycharm

# Reset IntelliJ IDEA
rm -rf ~/.config/JetBrains/IntelliJIdea*/eval
# rm -rf ~/.config/JetBrains/IntelliJIdea*/options/other.xml
sed -i -E 's/<property name=\"evl.*\".*\/>//' ~/.config/JetBrains/IntelliJIdea*/options/other.xml
rm -rf ~/.java/.userPrefs/jetbrains/idea

# Reset WebStorm
rm -rf ~/.config/JetBrains/WebStorm*/eval
# rm -rf ~/.config/JetBrains/WebStorm*/options/other.xml
sed -i -E 's/<property name=\"evl.*\".*\/>//' ~/.config/JetBrains/WebStorm*/options/other.xml
rm -rf ~/.java/.userPrefs/jetbrains/webstorm
```

# Extends Evaluation in Windows

###### Intellij Evaluation Problem:

If you want to increase evaluation periods to more 30 days you can follow the bellow steps:

- Step 1: Exit intellij software.
- Step 2 : Remove all intellij/pycharn/webstrom home cash folder (like: C:\Users\<Username>/.IntelliJIdea201…..)
![Image](../../../../static/img/evaluationProblem.PNG)


![Image](../../../../static/img/intelijCashfolder.PNG)

- Step3: Windows key + R  type regedit & press enter(open registry)

![Image](../../../../static/img/regedit.PNG)

- Delete evlsprt, evlsprt 1, evlsprt 2 ……. files from jetbrains software.


![Image](../../../../static/img/registry.PNG)


![Image](../../../../static/img/regieditDelete.PNG)


- Open Intelij & evaluate for 30 days & enjoy.







