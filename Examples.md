# Examples

    alias py='python3'
    alias Rs='Rscript --no-restore'

## Dealing with messy or weird data files

flat text "d.output"
big, >1GB (ls -lh *.output)
no one knows wtf to do with it
excel barely opened it; spss loaded it but barely worked and was slow
needed to analyze in R... good luck

	head d.output

it's pipe separated!

	wc -l

it's huge! (millions of rows)

	firstrow=$(head -n1 d.output | tr '|' ' ')
	for f in $firstrow; do echo $f; done
	echo $firstrow | grep 'id' --color=auto

## Chaining tools

    cat d.output | py script.py | Rs script.R > d.txt
    cat d.output | py pymapper.py | py reducer.py | less

## SSH and Cunix

How to access SSH? Did you know you have a website? www.columbia.edu/~uni

Need to put files in the `public_html` folder... but how to access it?

First, add an alias "cunix" to SSH so you don't have to remember the host name:

    echo -e 'Cunix\n\tHostName cunix.cc.columbia.edu\n\tUser gw2286' >> ~/.ssh/config

Then type: 

    ssh cunix

to access the CUnix server -- another command line shell!

To transfer files, you can use the tools `scp` (for one-off file transfers) or `sftp` (for transferring files while "moving around" inside the server). Like Git and LaTeX, this has GUI alternatives (e.g. WinSCP) but they're all really just a "wrapper" for the command line tool.