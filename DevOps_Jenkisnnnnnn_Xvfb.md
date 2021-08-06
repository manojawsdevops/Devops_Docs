In jenkins job

export DISPLAY=:1
/root/data/ace-11.0.0.7/tools/mqsicreatebar -data $WORKSPACE -b $Application#$BUILD_NUMBER.bar -a $Application


Install XVfb in terminal

yum install Xvfb -y

su jenkins
Run below commmands

export DISPLAY=:1
Xvfb $DISPLAY -screen 0 1024x768x16
