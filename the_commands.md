```
pwd

echo ~

ls

ls /

cd ..

# cd hotdog2
# cd hotdog2/
cd ~

ls -l
ls -a
ls -la

man ls

man bash

mkdir shell-tutorial
ls
ls shell-tutorial

touch shell-tutorial/stuff1
ls shell-tutorial
cd shell-tutorial
pwd
ls

mkdir my-files my-backups
ls

mv stuff1 mv-files/stuff1

mv my-files/file1 my-files/stuff1.txt

cd my-files
mv stuff-1.txt regression_model_diagnostics.log
ls

ls ../my-backups
echo $PATH

cp regression_model_diagnostics.log ../my-backups/regression_model_diagnostics

ls ../my-backups

rm regression_model_diagnostics.log

cd ~/shell-tutorial
# cd ..

rmdir my-files
# rm -d my-files

# head
# cat
ls /bin | head -n2
ls /bin | echo

touch hello_world
echo hello world > hello_world
cat hello_world
echo goodbye world > hello_world
cat hello_world

echo just kidding >> hello_world
cat hello_world

echo "hello world" >> hello_world
echo \"hello world\" >> hello_world
echo 'hello world' >> hello_world
echo '"hello world"' >> hello_world
echo '\"hello world\"' >> hello_world
cat hello_world

nano
emacs
vim

ls -a ~
touch ~/.bash_profile

# ~/bin/my_script --option input1
echo 'export PATH="~/bin:$PATH"' >> ~/.bash_profile
# my_script --option input1

ls /bin
echo $PATH
echo "$PATH"
echo '$PATH'
```
