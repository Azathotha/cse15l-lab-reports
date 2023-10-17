# Lab Report 1

## 1. cd
a. An example of using the command with no arguments <br />
![Image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/cd_no_arg.png)
> Working Directory: /home/lecture1/messages  ->  /home <br />
> This is not an error message. <br />
> I got this output because cd without an argument means I wanted to change my cuttent working directory to home directory; ~ means home directory.

b. An exmaple of using the command with a path to a directory as an argument <br />
![Image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/cd_direct.png)
> Working Directory: /home  ->  /home/lecture1/messages <br />
> This is not an error message. <br />
> I got this output because I wanted to change current directory to the messages file, and it is now at lecture1/messages.

c. An example of using the command with a path to a file as an argument  <br />
![Image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/cd_file.png)
> Working Directory: /home/lecture1/messages <br />
> This is an error message. <br />
> It outputs an error message because cd is only used to change directories, but not files.

## 2. ls
a. An example of using the command with no arguments <br />
![Image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/ls_no_arg.png)
> Working Directory: /home <br />
> This is not an error message. <br />
> In the home directory, I used ls to list the contents inside; so I got "lecture1" as an output.

b. An exmaple of using the command with a path to a directory as an argument <br />
![Image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/ls_direct.png)
> Working Directory: /home <br />
> This is not an error message. <br />
> I got this output because I asked to list all the contents inside lecture1/messages, so the four file names showed up.

c. An example of using the command with a path to a file as an argument  <br />
![Image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/ls_file.png)
> Working Directory: /home/lecture1/messages <br />
> This is not an error message. <br />
> I got this output because ls is only used for displaying contents of directory; using it on a file results in outputing the file name.

## 3. cat
a. An example of using the command with no arguments <br />
![Image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/cat_no_arg.png)
> Working Directory: /home/lecture1/messages <br />
> This is not an error message. <br />
> There was no output, because the input source was not given.

b. An exmaple of using the command with a path to a directory as an argument <br />
![Image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/cat_direct.png)
> Working Directory: /home <br />
> This is an error message. <br />
> It outputs an error message because cat cannot be used on a directory.

c. An example of using the command with a path to a file as an argument  <br />
![Image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/cat_file.png)
> Working Directory: /home <br />
> This is not an error message. <br />
> I got this output because cat displayed the content in the file.




