## Shell scripting concepts

---

A shell script is a script written for the command line shell of an operating system. It consists of a series of commands that are executed in order by the shell interpreter. Shell scripts are commonly used to automate repetitive tasks, perform system maintenance, and configure system environments.

There are several different shells available for Unix-like systems, such as Bash, sh, csh, and tcsh. Bash (Bourne-Again shell) is the most commonly used shell and it is the default shell on most Linux distributions and macOS.

In a shell script, you can use variables to store and manipulate data. Variables are declared with the = operator, and can be accessed by prefixing the variable name with a $ sign. For example, the following script declares a variable name and assigns it the value "John Doe", and then uses the echo command to print out a greeting:

```bash
name="John Doe"
echo "Hello, $name"
```

Shells also provides several built-in control structures that allow you to control the flow of execution in your script. These include if statements for conditional execution, for and while loops for iterating over a sequence of values or until a condition is met, and case statements for conditional branching. Here is an example of a for loop that counts from 1 to 10 in bash script:

```bash
for i in {1..10}; do
  echo $i
done
```

and here is an example of a for loop that counts from 1 to 10 in sh script:

```bash
for i in $(seq 1 10); do
  echo $i
done
```

Shells also include many built-in commands, such as echo, cd, and pwd, which can be used to perform common tasks like printing text to the screen, changing the current working directory, and determining the current working directory. Additionally, you can call other programs and utilities from within a shell script, allowing you to integrate a wide range of functionality into your script. For example, the following command uses the ls command to list the files in the current directory:

```bash
ls -l
```

Shells also provide several features to make scripting more powerful, such as command line arguments, standard input, and output, exit status, and functions.

Command line arguments can be passed to the script and accessed using the special variables `$1, $2, $3`, etc, where `$1` is the first argument, `$2` is the second argument, and so on.

```bash
echo "first argument is: $1"
```

Standard input, output and error can be redirected to and from files or to other commands using the >, < and | operators, respectively.

```bash
command1 | command2
```

Exit status is the value returned by the last executed command and can be accessed using `$?` variable.

```bash
command1
echo "exit status: $?"
```

Functions can be defined in the script and called when needed, it allows the separation of the script logic into smaller and reusable blocks.

```bash
function greet {
  echo "Hello, $1"
}
greet "John Doe"
```

---

## Real example of a shell script for devops daily tasks

Let's say you need to regularly check the disk usage on your servers to ensure that there is enough free space. One way to do this is to SSH into each server, run the df command, and manually check the output. However, this can be time-consuming and error-prone, especially if you have many servers to check.

Instead, you could write a shell script that automates this task. The script could use SSH to connect to each server, run the df command, and parse the output to check the disk usage. If the usage exceeds a certain threshold, the script could send an email alert or send a notification to a chat or messaging service.

Here's an example of a simple shell script that does this using Bash:

```bash
#!/bin/bash

# List of servers to check
servers=( "server1.example.com" "server2.example.com" "server3.example.com" )

# Threshold for disk usage in percent
threshold=90

# Loop through the servers
for server in "${servers[@]}"
do
    # Get the disk usage information
    usage=$(ssh $server "df -h / | tail -1" | awk '{print $5}' | sed 's/%//')

    # Check if the usage is above the threshold
    if [ $usage -gt $threshold ]; then
        # Send an email alert
        echo "Disk usage on $server is at $usage%, which is above the threshold of $threshold%" | mail -s "High disk usage on $server" admin@example.com
    fi
done

```

---

#### And here's a breakdown of this shell script example:

```bash
#!/bin/bash
```

- This line is called a shebang, it specifies the interpreter to be used for running the script. In this case it's /bin/bash.

```bash
# List of servers to check
servers=( "server1.example.com" "server2.example.com" "server3.example.com" )
```

- This line declares an array named servers that contains the list of servers that we want to check the disk usage on.

```bash
# Threshold for disk usage in percent
threshold=90
```

- This line declares a variable threshold that stores the disk usage threshold value in percentage beyond which the script sends an alert.

```bash
# Loop through the servers
for server in "${servers[@]}"
do
```

- This line uses a for loop to iterate over the list of servers in the servers array. The "${servers[@]}" syntax is used to loop over all the elements of the array.

```bash
    # Get the disk usage information
    usage=$(ssh $server "df -h / | tail -1" | awk '{print $5}' | sed 's/%//')
```

- This line uses the ssh command to connect to the current server in the loop and runs the df -h / | tail -1 command. This command shows the disk usage of the root partition, tail -1 command takes the last line in the output (which is the root partition information) and awk '{print $5}' command prints the fifth column of the output which is the disk usage percentage. sed 's/%//' removes the % sign from the percentage. Then the result of the command is stored in the usage variable

```bash
    # Check if the usage is above the threshold
    if [ $usage -gt $threshold ]; then
```

- This line uses an if statement to check if the disk usage value stored in the usage variable is greater than the threshold value stored in the threshold variable. If the usage is above the threshold, the script proceeds to the next step, otherwise it continues with the next iteration of the loop.

```bash
        # Send an email alert
        echo "Disk usage on $server is at $usage%, which is above the threshold of $threshold%" | mail -s "High disk usage on $server" admin@example.com
```

- This line uses the echo command to construct an alert message, the message contains the server name and its current disk usage percentage and how it exceeded the threshold. Then, the message is piped to the mail command which is used to send the email to the admin, the -s option is used to specify the subject of the email.

```bash
    fi
done
```

- The fi indicates the end of the if statement, the done indicates the end of the for loop.

---

To finish, you can schedule this script to run at regular intervals by using tools such as cron on Linux systems. cron is a built-in scheduling utility that allows you to schedule commands or scripts to run automatically at specified intervals.

You can edit the crontab by running crontab -e and add a new entry that specifies when you want the script to run and the path to the script file:

```bash
*/30 * * * * /path/to/script.sh
```

This line runs the script every 30 minutes.

you can also use the at command to run the script just once on a specific date and time.

By scheduling the script to run automatically, you can ensure that you are notified of any potential issues with disk usage on your servers in a timely manner, allowing you to take action before they become critical.

It's worth noting that this script is a simple example and should be adjusted to suit your specific requirements and environment. Additionally, you can also use other Linux utilities such as `nagios` and `zabbix` to monitor the disk usage and many other parameters, those tools are more powerful and provide more flexibility and features than using just shell script.

---

This is just one example of how shell script can be used to automate a devops task. Other examples include:

- Automating software deployment
- Creating and managing backups
- Automating monitoring and alerting
- Automating scaling and load balancing
- Automating container orchestration
- Automating database management tasks
