# ansible



What Is Infrastructure As Code?
IaC means writing code for infrastructure i.e. your systems and devices, which are used to run Softwares, are to be treated as software and defined using code(which can be done using a high level or descriptive language).
For example: version control, testing, small deployments, use of design patterns etc.
Configuration Management tools are used to accomplish IaC.
Why are You Here?
Infrastructure as Code can be achieved using Ansible, which is one of the popular Configuration Management tools. In this course, we will have you explore various capabilities of Ansible.
What is Configuration Management?
Configuration Management is a process of establishing, tracking and controlling the current design and build state of the system (software versions).
It also ensures that past records of system state is easily and accurately accessible which helps in project management, audit purposes, debugging etc.
Before Configuration Management
Consider you are planning for a New Year Special Sale in your e-commerce site. You need to
•	Scale up your servers
•	Then configure them(and all other old servers) for special new year sale
•	This whole process would take lot of effort and time
•	What if new configurations did not work as expected? Then you will have to roll back to previous stable version, which will add more work and subtract the profits and potential customers while in downtime.
Configuration Management Tools
You need some kind of Configuration Management tool that can automate these tasks:
•	Roll back to stable version with zero downtime
•	Provide you with constant computing environment throughout SDLC
•	Automatically scale up or down depending upon traffic
Some of the popular Configuration Management tools are: Ansible, Puppet, Chef and Saltstack.
You will now learn more about Ansible in upcoming cards.
What is Ansible?
Ansible is an open source software, first released by Michael DeHaan in 2012 and owned by Red Hat.
It is used to automate
•	configuration management
•	application deployment
•	software provisioning and other IT needs
Benefits of Ansible
Simple: Very easy to install, setup and learn. Written in YAML file which is pretty much like reading English.
Agentless: Do not need to install any agents on target nodes.
Powerful: It can model any complex IT workflow as it has 1100+ modules
Efficient: You can customize modules, using any programming language
Secure: Uses SSH for connection
Wondering about YAML language?? Read on to discover
What is YAML?
YAML stands for Yet Another Markup Language. It is a data serialization language just like JSON.
Why YAML, when we already have JSON or XML?
•	YAML files are easy to read and write for humans, similar to English
Foundation of YAML
•	YAML files should end as .yaml or .yml
•	Begins with --- and ends with …
•	# defines comment
YAML is Case and Indentation Sensitive
•	Members of a list should be at the same indentation level starting with a dash(-) and space.
•	Each item in the list is a key: value pair (colon must be followed by a space), called as dictionary.
•	At each level, exactly two spaces are used for indentation. Using tabs is not recommended here.
•	Boolean Values
•	Variables can be defined in YAML files as shown:
•	
•	stream: Java
•	
•	allocated: true
•	
•	Variables can be assigned boolean values in different ways as shown:
•	
•	allocated: yes
•	
•	allocated: no
•	
•	allocated: True
•	
•	allocated: TRUE
•	
•	allocated: false
Data Structures
Complicated data structures are possible in YAML.
You can define lists having dictionaries, dictionaries having lists or a mix of both.
In the following example,
•	name and job are dictionaries. Skill is a dictionary with a list.
•	David and Amy are lists having dictionaries

# Employee records

-  David:

    name: David Moore

    job: Developer

    skills:

      - python

      - sql

      - java

-  Amy:

    name: Amy Brown

    job: Developer

    skills:

      - angular

      - redux

      - react
How Ansible Works?
As already discussed, Ansible is a configuration management tool, based on push-based architecture to automate configuration of your hosts to achieve a desired state.
Following are the components of Ansible architecture
•	Inventory - Defines the list of target hosts
•	Playbook (YAML file) - Defines list of tasks
•	Module - A python code invoked from tasks and executed on hosts
•	Control Machine - Takes playbook and executes each task on particular group of hosts
Playbook
A Playbook is a file that defines the desired state of your system.
It contains plays, which has a list of tasks to run in sequence against a list of hosts.
•	A play is set of tasks, grouped together to achieve an objective
•	A task is an instruction you give to Ansible.
•	They are written in YAML format, a data serialization language, that we discussed in previous cards.
Inventory
So Ansible captured the desired state through Playbook, but how would ansible know which machines it should configure through Inventory?
The Inventory file in Ansible contains the list of all hosts (target systems/servers) that need to be configured. You can also group hosts under different names as shown:
[group A]
Host 1
[group B]
Host 2
Host N
More on Inventory
•	Default location of Inventory File: /etc/ansible/hosts
•	You can define an Inventory file statically (.ini file) or dynamically (.json file) to Ansible.
Modules Perform the Action
Modules are a piece of code that gets executed when you run playbook. You use them to describe the state you want the host to be in.
Each task in play is made of module and arguments.
Ad-Hoc Keywords
Before hopping into Ad-Hoc commands, let us first learn Ansible keywords:
•	ansible: This is a tool that allows you to run a single task at a time.
$ ansible <host-pattern> [-m module_name] [-a args] [options]
•	ansible-playbook: This is the tool used to run ansible playbook
$ ansible-playbook <filename.yml> ... [options]
•	ansible-console: This is a REPL using which you can run ad-hoc commands on chosen inventories.
$ ansible-console <host-pattern> [-m module_name] [-a args] [options]
•	ansible-pull: This inverts the default push architecture of Ansible into a pull architecture, which has near-limitless scaling potential.
ansible-pull -U URL [options] [ <filename.yml> ]
•	ansible-doc: Displays data on modules installed in Ansible libraries.
$ ansible-doc [-M module_path] [-l] [-s] [module...]
•	ansible-vault: Using this you can encrypt any structured data file used by Ansible.
$ ansible-vault [create|decrypt|edit|encrypt|rekey] [--help] [options] file_name
•	ansible-galaxy: This is a shared repository for Ansible roles. This ansible-galaxy command can be utilized to manage these roles, or to create a skeleton framework for the roles to be uploaded to Galaxy.
$ ansible-galaxy [delete|import|info|init|install|list|login|remove|search|setup] [--help] [options]
Short Hands in Ansible
•	-a: This tells the arguments to pass to the module
•	-m: Execute the module
•	-b: Use privilege escalation (become)
•	-i: The path to the inventory, which defaults to /etc/ansible/hosts
•	--version: Show program version number
•	--help: Shows help message
Playground for Ansible
Throughout this course, you can use Katacoda Playground to try out Ad-hoc Commands being introduced to you.
Katacoda is an online platform that provides you lab for hands-on, right in your browser, for you to test your Ansible codes and commands.
You are provided with the terminal of Control Machine and one host machine to test your commands.
To practice as you read, you first need to follow the two steps shown in GIF to setup Katacoda environment.
Running Your First Ad-hoc Command
An ad-hoc command is a single statement to complete a particular task. For example: consider you want to check if you could connect to your hosts.
Open Katacoda and enter the following command:
ansible group1 -i myhosts -m ping
The above statement is a single task to ping target host and return pong if the connection is successful.
•	ansible is a keyword you need to write before running any ad-hoc command
•	group1 is the group name of the list of hosts
•	-m means module, this is followed by the module name ping, which will be executed to achieve the task
To know more about each module you can try: ansible-doc ping.
Copy a File to the Servers
You can use copy module to copy a file from your control machine to host as shown:
$ touch test.txt
•	This will create a sample file which could be used to copy
$ ansible host01 -i myhosts -m copy -a "src=test.txt dest=/tmp/"
•	copy the file test.txt from your control machine (where ansible is installed) to all the hosts defined in myhosts inventory group
•	-a means arguments of that module (here copy module)
•	src is attribute of copy module that defines the source path of file or directory on control machine
Similarly, to fetch a file from Host to your Control Machine, you can use fetch module. You may use ansible-doc fetch to know about it.
Encrypting Your File
As you just created a test.txt file, let us now encrypt the same using ansible-vault keyword.
•	$ ansible-vault encrypt test.txt: encrypts the file.
This asks for a password to be set. Give a password and confirm it.
•	ansible-vault edit test.txt: to edit the file and add some content.
This opens vi editor. Type some text, then save it(:wq)
•	cat test.txt: to view the content inside.
Observe the output carefully
•	ansible-vault decrypt test.txt: to decrypt the file, use the password set during encryption
•	cat test.txt: now observe the output
Create Directories and Files
You can use file module to create files and directories, manage their permissions and ownership as shown:
ansible host01 -i myhosts -m file -a "dest=/tmp/test mode=644 state=directory"
•	This will create directory /tmp/test on all the host01 of myhosts group
•	mode defines permission of file/directory
•	state can take value: file, directory, link, absent, etc
You can set the state to absent to delete a file or directory to delete it:
$ ansible host01 -i myhosts -m file -a "dest=/tmp/test state=absent"
Automating with Ansible
Till now you were executing each task (using Ad-hoc command) to create a folder, copy a file, encrypt or decrypt a file, etc.
What if you need to execute, say, **500 tasks** to configure a server?
Do not worry, as Ansible got you.
You just need to define a Playbook that Ansible can play with, and have a popcorn watching Ansible in action.
Read on to find out what Playbook is.
Q.Which command instructs Ansible to execute the playbook on all the hosts except host1? ansible-playbook playbooks/PLAYBOOK_NAME.yml --limit 'all:!host1'
Q.Where is Inventory file located by default? /etc/ansible/hosts
Q.Which one is not a valid value of state argument of "file" module?folder
Q.If you do not need any facts from the host, what command would you use? both gatherfacts: no or gatherfacts: False
Modules
Modules are blocks of Python code that gets executed on remote hosts when you run each task in Playbook.
Each module is built for a particular task and you can use arguments to change the behavior of module.

#Hands-on soln: (https://stackoverflow.com/questions/62467670/ansible-module-to-stop-and-start-ssh-service#:~:text=For%20this%20you%20have%20to,the%20service%20module%20in%20Ansible.)
-
  name: "Stop ssh"
  service:
    name: ssh
    state: stopped


-

  name: "start ssh"
  service:
    name: ssh
    state: started
Things You Should Know About Modules
•	Also referred as task plugins or library plugins
•	Default location for Ansible modules is /usr/share/ansible
•	Take arguments in key=value format (state=stopped)
•	Returns data in JSON format
•	Modules should be idempotent, meaning they should not do any changes if current state of system matches with the desired final state
•	To access list of all installed modules using command line: ansible-doc -l
•	To see the documentation of particular module using command line: ansible-doc yum where yum is the module name
•	You can run modules from the command line or include them in Playbook.
•	Ansible allows you to write your own module (this you will learn later in advanced courses of Ansible).
Let us now go through some standard modules: apt, yum, shell, command, and template.
APT Module
APT (Advanced Package Tool) is a command-line tool used to easily manage (install, remove, search, etc.) packages on Ubuntu/Debian based Linux systems.
Debian Based OS: Ubuntu, Kali Linux, SteamOS and much more.
You can try the following in Katacoda
$ ansible host01 -i myhosts -m apt -a "name=sudo state=latest"

#This is how you write in Playbook

- name: Upgrade sudo to the latest version

  apt:`

    name: sudo

    state: latest
YUM Module
YUM (Yellowdog Updater Modified) is a command-line tool used to easily manage (install, remove, search, etc.) packages on RPM (Red Hat Package Manager) based Linux systems.
Red Hat Based OS: Fedora, Qubes OS, CentOS and much more.

#This is how you write in Playbook

- name: upgrade all packages

  yum:

    name: sudo

    state: latest
shell Module
In shell module, the command name is followed by arguments, which runs on remote hosts through a shell(/bin/sh).
You can use various operations(|,<,> etc) and environment variable(#HOME).
ansible host01 -i myhosts -m shell -a "echo $TERM": This displays the terminal name of host machine

#This is how you write in Playbook

- name: Execute the command in remote shell

  shell: echo $TERM
command Module
In command module, the command name is followed by arguments, which does not run on remote hosts through a shell(/bin/sh).
You cannot use various operations(|,<,> etc) and environment variable(#HOME).
•	To check the list of files or folder in remote host: ansible host01 -i myhosts -m command -a "ls"
•	Make a directory in remote host: ansible host01 -i myhosts -m command -a "mkdir folder1"
•	Check files or folders in remote host: ansible host01 -i myhosts -m command -a "ls"
Now to check files or folders in your terminal use ls and observe the output. As you can see, using command, you can execute tasks on remote host.
command Everytime
Most of the Ansible modules are idempotent.
But command module does not exhibit this property as this runs every time you run playbook. Hence you will always find the changed status on running the same Playbook again and again.
Consider you wrote a task to copy a file to remote hosts using command module.
Ansible command module will copy the same file the number of times you run the Playbook.
Had this been idempotent; Ansible will not copy from the second time, as the file is already present (current state = desired state).
command can be Idempotent
To overcome this, you can use creates or remove parameter, where you define the filename/pattern.
•	creates: if filename exists, task will not run
•	remove: if filename does not exist, task will not run

#This is how you write in Playbook

- name: copy a file, but do not copy if the file already exists

  command: cp /home/dist/file1.txt /usr/someFolder/ creates=file1.txt
template Module
Ansible template is a file having a defined structure with some variables and expressions, which can be replaced with the corresponding values to generate new configuration file.
•	Template files are written in Jinja2 language (.j2) (Read on to know more about Jinja2)
•	Generally, in Ansible, these files are copied to remote hosts in JSON or YAML format
There are basically two files involved to define templates in Ansible:
•	playbook(YAML file): here you substitute variables in template file with values
•	template(Jinja2 file): here you define the template file in Jinja2 format
Let us take the example of the human body as a template. Depending on the various elements (footwear, dress, hair) you could name the template as a man or a woman.
file: sample-playbook.yml
This is where your template and variables are merged.
Let us consider another example of Payslip as a template, where a structure of payslip is pre-defined. Depending on the values being passed new payslip is generated for each name.
#This is how you write in Playbook
- hosts: all
  vars:
    quarter: false,
    salary : 30000,
    extra : 10000,
    names: ["John","David"]
  tasks:
    - name: Ansible Template
      template:
        src: ../templates/sample-template.j2
        dest: /home/sample-template        
•	src: defines path where your template file is kept.
•	dest: path where you want to copy your file (mostly JSON or YAML formatted file).
file: sample-template.j2
This is where you define your template.
{% for name in names %}
Hi {{name}}!
{% if quarter -%}
    Your pay cheque for this month is {{ salary + extra }}.
{% else -%}
    Your pay cheque for this month is {{ salary }}.
{%- endif %}
{% endfor %}
•	variable names are given within double curly braces {{ }}
Hands-on Template
You can test your Jinja2 templates online with the steps as explained.
•	Copy sample-template.j2 file and paste in Template box
•	Copy variables from sample-playbook.yml and paste in Values box
•	Click on Convert

Try It Out - Template
Try to make a template to display Students mark sheet that displays name of student, marks in Physics, Chemistry and Maths.
Provide relevant values via variables.

Q.	You write comments in Jinja2 as __________{# #} _____________.
Q._________ module copies dynamically created file from control machine to target hosts?template
Q.Which Ansible module is utilized for managing docker services and containers?docker service
Q.Which module will you utilize to create a directory?file
Q. Modules are tentatively stored in the nodes and interact with the control machine via a ______ protocol over the standard output. JSON
Environment at a Glance
Control Machine Requirements
•	Linux/Mac OS (Windows not supported)
•	Python (2.6 or later version) should be installed.
•	Install Ansible.
Host Requirements
•	Only Python needs to be installed.
•	Uses SSH to connect to control machine.
•	SFTP is used else scp can be configured.
Step By Step
You need to follow these steps to setup environment on your system:
1.	Install VirtualBox.
2.	Install Vagrant. Vagrant enables virtual software development environment.
3.	Install Ansible.
Install Vagrant
Download and install Vagrant
•	Identify the OS you want to install in your virtual system. Accordingly, you need to find the Vagrant Box (let us consider Ubuntu on both our control and host machines).
•	Create a folder on your local machine, to keep your Vagrant Boxes.
Now, open your terminal and move to the path where you created your folder for Vagrant boxes. Then run the following commands:
•	$ vagrant init ubuntu/trusty64: Initialises vagrant file inside the folder
•	$ vagrant up --provider VirtualBox: will download necessary files of your virtual machine
•	$ vagrant ssh: will make secure connection with virtual machine
Install Ansible
Once you are done with Virtual Box and Vagrant setup, you only need to run one last command in your terminal to install Ansible on the control machine.
On Ubuntu/Debian/Linux Mint
$ sudo apt-get install ansible
On RHEL/CentOS/Fedora
$ sudo yum install epel-release
$ sudo yum install ansible
To verify if Ansible is successfully installed or not: ansible --version
You can follow Ansible Official Docs for detailed instructions.
Writing Playbook
Step By Step
•	Open Katacoda
•	Enter commands given in Step 2 of 6. This makes an SSH connection to your host.
•	Open Playbook using the vi editor (eg: vi demo.yml).
•	Write your playbook (given in next card).
•	Press Escape key on your keyboard.
•	Save and close editor using :wq(w: write, q: quit).
•	Run your playbook: $ ansible-playbook -i myhosts demo.yml.
Sample Playbook 1 - "demo.yml"
---
- name: this play displays "hello world"
  hosts: all
  tasks:
    - name: displaying "hello world"
      shell: echo "hello world"
    - name: displaying wishes for the day
      shell: echo "have a good day"
Playbook Step 1 - Name and Hosts
---
- name: this play displays "hello world"
  hosts: all
•	A Playbook always starts with three dashes ---.
•	name tells the name of the play.
•	hosts tell the list of hosts on which this play will be played.
Playbook Step 2 - Tasks
tasks:
    - name: displaying "hello world"
      shell: echo "hello world"
    - name: displaying wishes for the day
      shell: echo "have a good day"
•	name is optional but is always recommended as it improves readability
•	shell: echo "hello world" is a single task. This executes shell module and calls its echo argument to display the message written
Playbook Step 3 - Run Your Playbook
Type ansible-playbook -i myhosts demo.yml from the terminal to run your Playbook.
•	ansible-playbook is the command to execute your Playbook
•	-i myhosts tell the inventory name is myhosts
•	demo.yml is the playbook that needs to be executed
Output Of "demo.yml"
This is how your Playbook would run
PLAY [this play displays "hello world"] ***************************************
GATHERING FACTS ***************************************************************
ok: [host01]
TASK: [displaying "hello world"] **********************************************
changed: [host01]
TASK: [displaying wishes for the day] *****************************************
changed: [host01]
PLAY RECAP ********************************************************************
host01                     : ok=3    changed=2    unreachable=0    failed=0
Sample Playbook 2 - Install Apache
Let us now take another example to install apache in your hosts.
This is how your Playbook would look:
---
- name: install apache
  hosts: all
  sudo: yes
  tasks:
    - name: install apache2
      apt: name=apache2 update_cache=yes state=latest
Save and run this playbook as apache.yml in Katacoda and check the output.
Please note that for installing in RHEL/CentOS/Fedora,yum module is used instead of apt.
Restructuring Playbook
You can define the same playbook as:
---
- name: install apache
  hosts: all
  sudo: yes
  tasks:
    - name: install apache2
      apt: 
        name: apache2 
        update_cache: yes 
        state: latest
•	observe colon : is used while structuring arguments vertically, whereas equal to sign = is used while structuring arguments horizontally
Both ways of structuring your playbook is fine.
•	This vertical structuring of arguments is not a list, as list starts with dash sign -.
Here name, update_cache and state are arguments of module apt, hence they do not start with -.
Handlers
Handlers are special tasks that run only on certain triggers like notify keyword.
•	Handlers run mostly at the end of the play.
•	Handlers run only once even if you run the playbook multiple times.
This is how a handler would look:
---
- name: install apache
  ...................
  tasks:
    - name: install apache2
      .....................
    notify:
    - start Apache
      ............
  handlers:
    - name: start Apache
      ..........

Q.Using which module can you see the list of all Ansible variables?fetch(wrong)
Q. Which module can you use to install Apache in Ubuntu OS? Apt 
Q. What is the output statement of the following snippet?
tasks:
- name: test
  shell: echo "hello"
  register: a
  debug: msg="the message is {{ a.stdout }}"
Syntax error because of conflicting action statements 
Q. Which command do you use to do a syntax check on your playbook? ansible-playbook <playbook_name> --syntax-check
Conditionals In Ansible
Recollect while reading the section on setting up your environment or while installing an application , you need different modules (apt and yum) to execute task.
What will you do, if you have to configure 50 such servers with different OS and requirements?
This is where conditionals can be used to decide and control the execution flow in Ansible.
Conditionals - When Clause
When clause in Ansible is a raw jinja2 expression that defines the condition which will be evaluated for TRUE or FALSE.
tasks:
  - name: "shutdown Debian flavored systems"
    command: /sbin/shutdown -t now
    when: ansible_os_family == "Debian"
Conditionals - When Clause
•	You can group conditions using parenthesis ()
tasks:
  - name: "shutdown CentOS 6 and Debian 7 systems"
    command: /sbin/shutdown -t now
    when: (ansible_distribution == "CentOS" and ansible_distribution_major_version == "6") or
          (ansible_distribution == "Debian" and ansible_distribution_major_version == "7")+
•	You can define multiple conditions, where all of them should be true to execute the tasks
tasks:
  - name: "shut down CentOS 6 systems"
    command: /sbin/shutdown -t now
    when:
      - ansible_distribution == "CentOS"
      - ansible_distribution_major_version == "6"
Looping in Ansible
If you need to repeat the same task with different items (loop through), you can use with_items clause
For example, consider you want to add several users
- name: add several users
  user:
    name: "{{ item }}"
    state: present
    groups: "developer"
  with_items:
    - raj
	- david
	- john
	- lauren
Looping Through The Inventory
You can loop through the Inventory file to list all hosts or hosts from a play, using with_items with the play_hosts or groups variables,
# show all the hosts in the inventory
- debug:
    msg: "{{ item }}"
  with_items:
    - "{{ groups['all'] }}"

# show all the hosts in the current play
- debug:
    msg: "{{ item }}"
  with_items:
    - "{{ play_hosts }}"
Sample Playbook 3 - Conditions And Loop
This Playbook will add Java Packages to different systems (handling Ubuntu/Debian OS)
- name: debian | ubuntu | add java ppa repo
  apt_repository:
    repo=ppa:webupd8team/java
    state=present
  become: yes
  when: ansible_distribution == 'Ubuntu'
- name: debian | ensure the webupd8 launchpad apt repository is present
    apt_repository:
      repo="{{ item }} http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main"
      update_cache=yes
      state=present
    with_items:
      - deb
      - deb-src
    become: yes
  when: ansible_distribution == 'Debian'
 vars:
  score: 3
tasks:
  - shell: echo "Bang on!! You won."
    when: ??
How do you use a variable to apply condition? 
when : score == 3
Which of these will loop through items randomly?with_random_choice
Hands on 3rd:- ---
- name: install apache2, sqlite3, git pn remote server
  hosts: host01
  sudo: yes
  tasks:
  - name: Install list of packages
    action: apt pkg={{item}} state=installed
    with_items:
      - apache2
      - sqlite3
      - git
ansible.cfg
You told how your hosts should behave (via Playbook). But how do you tell Ansible (your control machine) should behave?
through ansible.cfg
ansible.cfg is a configuration file that defines how Ansible should behave.
It tells
•	how to establish an ssh connection
•	duration of ssh connection with the host
•	how to run the playbook
•	where to log errors that might occur while playing playbook on hosts etc.
Ansible Configuration Settings
Your ansible.cfg file will have the following settings:
•	[defaults]
•	[privilege_escalation]
•	[paramiko_connection]
•	[ssh_connection]
•	[accelerate]
You will now learn the frequently used settings in upcoming cards. For detailed understanding, you may refer to the Ansible Official Docs.
[defaults]
poll_interval
For asynchronous tasks in Ansible, this tells the frequency of checking the status of task completion. The default value is 15 seconds; which implies, for every 15 sec, it will check if the task is completed.
poll_interval = 15
sudo_user
This is the default user to sudo. If --sudo-user is not specified in an Ansible playbook, the default is the most logical: ‘root’:
sudo_user = root
ask_pass
This tells if Ansible Playbook should ask for a password by default. If SSH key is used for authentication, the default behavior is no.
ask_pass = True
ask_sudo_pass
Just like ask_pass, this asks for sudo password by default while sudoing.
ask_sudo_pass = True
remote_port
If your systems did not define an alternate value in Inventory for SSH port, this sets the default value to 22.
remote_port = 22
[privilege_escalation]
*For some tasks to execute in Ansible, you require administrative access to the system.
The settings under [privilege_escalation] will escalate your privileges.*
become
If set to true or yes, you activate privilege escalation.
Default behavior is no.
become=True
become_method
You can define the method for privilege escalation.
Default is sudo, other options are su, pbrun, pfexec, doas, ksu.
become_method=sudo
become_user
This allows you to become the user over privilege escalation.
Default is root.
become_user=root
become_ask_pass
Asks the password for privilege escalation, the default is False.
become_ask_pass=False
Other Settings
accelerate_timeout
This setting will close the socket connection if no data is received from the client for the defined time duration.
default: accelerate_timeout = 30
record_host_keys
If the setting is True(default value), this will record new hosts on the user's host file, provided host key checking is enabled. Setting it to False, the performance will improve and which is recommended when host key checking is disabled.
record_host_keys=False
pipelining
If enabled, the number of SSH connections required for execution of a module on the remote server is reduced, improving the performance significantly.
By default this is disabled: pipelining = False.
Q. ansible.cfg must be present in __________./etc/ansible
Q. How to define the number of parallel processes while communicating to remote hosts?forks
Q. What is the default forks value in the configuration file? 5

--------------------------------------------------------------------------------------

Variables In Ansible
In Ansible, you can define a variable with alphabets, numbers and underscore.
example: foo, foo_bar, foo5
Now let us explore:
•	Playbook Variables
•	Inventory Variables
•	Complex Variables
•	Fact Variables
•	Built-in Variables (explained later)
•	Registered Variables (explained later)

Playbook Variables

Variables In Playbook
Variables may be included inline with the rest of a playbook, using vars:
---
- hosts: all
  vars:
    var: 20
  tasks:    
    - debug: msg="Variable 'var' is set to {{ var }}"
Variables may also be included in a separate file, using the vars_files section
file: playbook.yml

---
- hosts: all
  vars_files:
    - vars.yml
  tasks:
    - debug: msg="Variable 'var' is set to {{ var }}"
file: vars.yml
---
var: 20
You can create the above two files in Katacoda and run it: ansible-playbook -i myhosts playbook.yml
Inventory Variables
Variables In Inventory
You can add variables in your inventory files as:
•	Host Variables - Variables are defined inline for individual host
•	Group Variables - Variables are applied to entire group of hosts
#host variables
[group1]
host1 http_port=80 
host2 http_port=303
#group variables
[group1:vars]
ntp_server= example.com
proxy=proxy.example.com
Organizing Host And Group Variables
What will you do when you need to define multiple variables to multiple hosts? Writing everything inside your inventory file might be cumbersome.
Ansible recommends you to store host and group variables as individual files under /etc/ansible/host_vars/ and /etc/ansible/group_vars/ locations respectively.
•	These variable files are in YAML format with valid file extensions: .yml, .yaml, .json or no file extension
/etc/ansible/host_vars/host1.example.com
/etc/ansible/group_vars/group1.yml
/etc/ansible/group_vars/webservers
Complex Variables
Defining Complex Variables
You can define variables as structured arrays (lists), which you can access as foo[0] as shown:
---
- name: list variables
  hosts: all
  vars:
    foo:
      - one
      - two
      - three
  tasks:
    - name: variable index 1
      debug: msg="{{ foo[0] }}"
    - name: variable index 3
      debug: msg="{{ foo[2] }}"
Accessing Complex Variables
For larger variables, you can easily access part of a variable by using bracket [] or dot . syntax.
For example:
consider you want to retrieve only IPv4 address of the server. But you might first prefer to take a look at the structure of the entire built-in variable (ansible_eth0) as shown:
Go ahead and try this playbook in Katacoda
---
- name: complex variables
  hosts: all
  tasks:
    - debug: var=ansible_eth0
    - debug: msg="{{ ansible_eth0.ipv4.address }}"
    - debug: msg="{{ ansible_eth0['ipv4']['address'] }}"
•	First task will show how the variable ansible_eth0 is structured
•	Second and third tasks displays only the required info
Fact Variables
Facts
You might have observed this output while running the playbook.
GATHERING FACTS *************************
ok: [host01]
Whenever you run Playbook, Ansible by default collects information (facts) about each host like host IP address, CPU type, disk space, operating system information etc.
You can run the following in Katacoda to find the information about host01:
ansible host01 -i myhosts -m setup
Gathering Facts Takes Time
In case you do not need facts of hosts, you can skip the task by setting gather_facts: no in your playbook.
This can save time especially when you are running your Playbook in dozens or hundreds of servers.
Run the following in Katacoda and observe if the task (Gathering Facts) runs or not:
---
- name: testing gather_facts
  hosts: all
  gather_facts: no
  tasks:
    - action: ping
Built-In Variables
Built-In Variables
In Ansible you get some variables by default, even if you do not define them, that helps you to access information about other hosts. Thus you should not define these variables explicitly, as they are reserved.
Let us explore a few of them:
•	hostvars
•	groups
•	inventory_hostname
Hostvars
Occasionally you might be running a task that needs the value of the variable defined in other hosts. By default, variables in Ansible are scoped by hosts.
Ansible provides you with hostvars variable that has all the variables and facts (facts are gathered only if you have talked to the host at least once in any play of your playbook) of all the hosts.
For Example:
Consider you need to run a task in host1 that need IP address of the eth1 interface of the host2
{{ hostvars['host2'].ansible_eth1.ipv4.address }}
Scope Of Host Variables
Wondering the scope of variables defined in group of servers??
#host variables
[group1]
host1 http_port=80 
host2 http_port=303
host3
#group variables
[group1:vars]
ntp_server= example.com
proxy=proxy.example.com
Variables defined in group variables are actually copied to individual hosts of that group, thus making their scope limited to only the host.
Groups
You can find the list of group names defined in your inventory file using groups variable.
For Example: Consider you need the IP address of all the servers in you web group

{% for host in groups.web %}

  server {{ host.inventory_hostname }} {{ host.ansible_default_ipv4.address }}:8080

{% endfor %}

The generated file might look like this:

server chennai.fresco.me 192.0.115.17:8080

server california.fresco.me 192.0.115.78:8080

server singapore.fresco.me 193.0.115.68:8080
Inventory_hostname
You can find the name of the current host using inventory_hostname.

#inventory file

[group1]

server1 ansible_ssh_host=192.169.67.34

inventory_hostname would be server1 instead of 192.169.67.34
Registered Variable
Registered Variable
Ansible allows you to save the output of a task in a variable at run time, through register keyword.
Syntax: register: variable_name
Let us now see how the return value of command module looks like. Go ahead and run the following playbook in Katacoda
file: test.yml

---
- name: show return value of command module
  hosts: all
  tasks:
    - name: creating folder
      command: mkdir folder7
      register: output
    - debug: var=output
•	Run your playbook: ansible-playbook -i myhosts test.yml and observe the output carefully
•	You might observe the output of running a task is returned in JSON format
This playbook will check the contents of the home directory of your host machine (host01) and display a message accordingly
Go ahead and run this in Katacoda

---

- name: check registered variable for emptiness

  hosts: all

  tasks:

    - name: list contents of the directory in the host 

      command: ls /home/ubuntu

      register: contents

    - name: check dir is empty

      debug: msg="Directory is empty"

      when: contents.stdout == ""

    - name: check dir has contents

      debug: msg="Directory is not empty"

      when: contents.stdout != ""

•	register variable stores the output, after executing command module, in contents variable
•	stdout is used to access string content of register variable
Hands on sol2:
- name: copy files
  hosts: all
  tasks: 
    - name: copy file
      copy: src=afile.txt dest=/home/ubuntu/afile_copy.txt
      register:output
    - debug: var=output
Variable Precedence
If you define the same variable in multiple places, it will be overwritten in a certain order as shown:
•	variable you define in Command Line Interface while executing Playbook (Highest Priority)
•	variables that you define inside play of Playbook
•	facts that you discover about other hosts
•	variables defined under the [defaults] category of Roles* (least priority)
Command Line > Playbook > Facts > Roles
________________________________________
You can find the complete details here
*Hold On!! Roles will be discussed in upcoming sections
Workout - - Variable Precedence
•	Fact: The default value of fact variable ansible_bios_version is Bochs
ansible host01 -i myhosts -m setup
•	Play: Write Playbook defining the fact variable ansible_bios_version as fresco

#file: test.yml
---
- hosts: all
  vars:
    ansible_bios_version: Fresco
  tasks:        
    - debug: msg="Variable 'ansible_bios_version' is set to {{ ansible_bios_version }}"
Now run this playbook and notice the value of ansible_bios_version.
ansible-playbook -i myhosts test.yml
•	CLI: While running the playbook in Command Line redefine the variable - ansible-playbook -i myhosts test.yml --extra-vars "ansible_bios_version=Ansible"
Tags
Tags are names pinned on individual tasks, roles or an entire play, that allows you to run or skip parts of your Playbook.
Tags can help you while testing certain parts of your Playbook.
file: tag.yml
---
- name: Play1-install apache
  hosts: all
  sudo: yes
  tasks:
    - name: install apache2
      apt: name=apache2 update_cache=yes state=latest      
    - name: displaying "hello world"
      debug: msg="hello world"
      tags: 
        - tag1
- name: Play2-install nginx
  hosts: all
  sudo: yes
  tags: 
    - tag2
  tasks:
    - name: install nginx
      apt: name=nginx update_cache=yes state=latest      
    - name: debug module displays message in control machine
      debug: msg="have a good day"
      tags: 
        - mymessage
    - name: shell module displays message in host machine.
      shell: echo "yet another task"
      tags: 
        - mymessage
•	
•	

Running Tag.yml
You may save the above Playbook with name tag.yml and run the following commands in Katacoda
•	ansible-playbook -i myhosts tag.yml --list-tasks : displays the list of tasks in the Playbook
•	ansible-playbook -i myhosts tag.yml --list-tags : displays only tags in your Playbook
•	ansible-playbook -i myhosts tag.yml --tags "tag1,mymessage" : executes only certain tasks which are tagged as tag1 and mymessage
Special Tags
Ansible has some special keywords for tags:
•	always: runs the task always
•	tagged: run only those tasks which have some tag
•	untagged: run only those tags which do not have any tags
•	all: run all the tags
You can skip always tag by defining: --skip-tags always
	Include
Till now you were dumping all the tasks and other stuff (handlers, variables) in a single Playbook. This makes it cumbersome to maintain the Playbook as it grows.
Ansible gives you the flexibility of organizing your tasks through include keyword, that introduces more abstraction and make your Playbook more easily maintainable, reusable and powerful.
playbook_include.yml
---
- name: testing includes
  hosts: all
  sudo: yes
  tasks:
    - include: apache.yml    
    - include: content.yml    
    - include: create_folder.yml
    - include: content.yml
- include: nginx.yml
•	You might need root access to install anything in host, that's why sudo: yes
•	First, you will be installing Apache
•	Then you will observe that the host machine is empty at location /home/ubuntu
•	You will create a folder in the same location of the host machine
•	Now you will again check if the location has any content
•	In the end, you will install Nginx as a separate play
Now let us go ahead and add the remaining files in the same test folder.
apache.yml
---
- name: install apache2
  apt: name=apache2 update_cache=yes state=latest      
- name: displaying message
  debug: msg="you are awesome!!"   
create_folder.yml
---
- name: creating folder
  file: path=/home/ubuntu/folder1 state=directory
content.yml
---
- name: list contents of directory in host 
  command: ls /home/ubuntu
  register: contents
- name: check dir is empty
  debug: msg="Directory is empty"
  when: contents.stdout == ""
- name: check dir has contents
  debug: msg="Directory is not empty"
  when: contents.stdout != ""
nginx.yml
---
- name: installing nginx
  hosts: all
  sudo: yes
  tasks:
    - name: install nginx
     apt: name=nginx update_cache=yes state=latest      
    - name: displaying message
      debug: msg="yayy!! nginx installed"
Did you notice something? If you did, you are awesome. And if you don't, you are like 99.9999% others. Cheers!
nginx.yml, unlike apache.yml, is a Playbook which you can run independently. That is why it has tasks and other keywords mentioned explicitly.
 Q.This keyword gives you the flexibility to run a specific part of your playbook.Tags
Which of the following can you include in your Playbook?All
Intro To Roles
Roles are added abstraction of building your Playbook in more modular fashion, where you hide all the technicalities by splitting your tasks into smaller files and grouping them under respective folders of tasks, templates, handlers, vars etc.
•	This is similar to writing Object Oriented Code (for example) in Java
•	Discrete pieces of code can be easily included into larger programs as needed
•	A Role is completely self contained or encapsulated and completely reusable
Role Directory Structure
 
A Role has following folders:
•	Files
•	Handlers
•	Meta
•	Templates
•	Vars
•	Defaults
•	Files
•	1
•	File folder has static files that need to be transferred to host machines. This also stores script file to run.
•	Handlers
•	2
•	All the special tasks that you define in your playbooks, which run only if triggered by notify keyword, are kept in Handlers folder.
•	Meta
•	3
•	You can define a list of roles that should run first before the current role can run properly. In short, Meta folder contains the dependencies of current role.
•	Tasks
•	4
•	You can define each task as YAML file and keep them in Tasks folder.
•	Templates
•	5
•	You can keep all the dynamic files (jinja2), that use variables to be substituted with values during runtime, in Template folder.
•	Vars
•	6
•	The variables of your role are defined in Vars folder.
•	Defaults
•	7
•	Defaults folder works similar to vars folder, only the priority of variables defined in defaults is less than variables in vars.
Creating Structure For Your Role
Before beginning with the Pahase 1, you need to follow these steps to create the folder structure for your Role:
•	Create a folder called roles: mkdir roles and cd roles
•	Create a folder called sample_role inside roles: mkdir sample_role and cd sample_role
•	Create your folder structure for your role: mkdir defaults files handlers tasks templates vars
As your structure is ready, let us now create required files.
Phase 1- nginx.yml
You need to create task for installing Nginx in host under roles/sample_role/tasks/
file: tasks/nginx.yml
---
- name: Installs nginx
  apt: pkg=nginx state=installed update_cache=true   
  notify: 
    - start nginx
Phase 1- Creating Handler
Now you may come out of tasks folder (cd ..) and write your special handler task inside handlers folder
file: handlers/main.yml
---
- name: start nginx
  service: name=nginx state=started
Phase 1-Including Tasks In Main.yml
*Just like nginx.yml, later you will be adding more files in tasks folder.
How will ansible know which task to execute first?*
Tasks, Handlers, and Vars folder always have main.yml file
You need to include those tasks in main.yml file.
file: tasks/main.yml
---
- include: nginx.yml
As you can see, tasks/main.yml is just list of tasks.
Creating Master Playbook
To run all your tasks, you need to create a Playbook in root location (/home/scrapbook/tutorial) location, which will call your role (sample_role).
•	Use cd .. to move up one directory
•	Use pwd to know your present working directory
•	Use ls to check files and folder in your present folder
file: master_playbook.yml
---
- name: my first role in ansible
  hosts: all
  sudo: yes 
  roles:
    - sample_role
Telling Ansible About Your Roles
You called your role in Playbook but how will Ansible know, where your roles are defined?
You need to explicitly tell the path(of roles) in ansible.cfg file
•	Remove the default configuration file: rm ansible.cfg (present in /home/scrapbook/tutorial/ansible.cfg)
•	Add your new configuration settings: vi ansible.cfg, press i and use the settings as shown:
file: ansible.cfg
[defaults]
host_key_checking=False
roles_path = /home/scrapbook/tutorial/roles/
```
What Is Happening?
So, let us have a look at what exactly is happening:
•	You have given the location of your roles by setting roles_path in Ansible configuration file.
•	When you run this playbook, the Role will first check main.yml file in tasks folder and execute tasks.
You can also define multiple roles in master_playbook and they are executed in a sequential manner.
- .....
  roles:
    - sample_role
    - sample_role2
Phase 2 - Copying Static File
Let us now create a task to copy a static file to your host machine.
file: tasks/copy-static.yml

---
- name: Copy a file
  copy: src=some-file.txt dest=/home/ubuntu/file1.txt
But, do we have sample-file.txt ?? No!!
Static files are kept in files folder of a Role.
Let us create a file in files folder: touch some-file.txt
Phase 2 - Including Task in Main Task File
Include the new task in main.yml file
file: tasks/main.yml

---

- include: nginx.yml

- include: copy-static.yml

Run your master_playbook and check the output: ansible-playbook -i myhosts master_playbook.yml
Note: To run your master_playbook, you must be present at /home/scrapbook/tutorial
Phase 3 - Creating Template And Variable File
Templates/Dynamic/Configuration files are kept in templates folder of a role.
file: templates/template-file.j2
this is {{item}}
Variables are kept in vars folder
file: vars/main.yml
var_x:
  - 'variable x'
var_y:
  - 'variable y'
Phase 3 - Creating Task To Send Your Configurations
Let us create a task to send your template/dynamic/configuration file to your host machine.
file: tasks/copy-template.yml
---
- name: sample template - x
  template:
    src: template-file.j2
    dest: /home/ubuntu/copy-template-file.j2
  with_items: var_x
Phase 3 - Including Task in Main Task File
Include the task you just created in your main file:
file: tasks/main.yml
---
- include: nginx.yml
- include: copy-static.yml
- include: copy-template.yml
Run your master_playbook and check the output: ansible-playbook -i myhosts master_playbook.yml
Running Role
Let us run the master_playbook and check the output:
ansible-playbook -i myhosts master_playbook.yml


Note: You can enter yes if prompted while running master_playbook
What Is Ansible Galaxy?
If you are annoyed to build the file structure for a role from scratch in Ansible every time, then this is for you.
Let us enter the Galaxy Of Ansible
•	Ansible Galaxy is a website where people like you can explore, download and rate roles. you can also contribute your role.
•	ansible-galaxy is command line tool for scaffolding the creation of directory structure needed for organizing your code
Try this command in Katacoda: ansible-galaxy init sample_role
Q.Which folder does not require the main.yml file?templates
Q.Which of the following can you use to delete your installed role?remove
Q.This folder stores your dynamic files.templates
Q. You can scaffold your roles using ________ ansible-galaxy
Environment Variables
Managing huge number of hosts can be tedious when the deployment environment is different: development, staging and production
For example, memory requirement for servers in production might be different from servers in the development environment
Ansible recommended way of solving this issue is by maintaining inventory file for each environment, instead of keeping all your hosts in a single inventory.
You can also maintain a separate directory for group_vars.
Multiple Inventories For Each Environment
 This is how a basic directory structure of multistage environment look.
Each environment directory has one inventory file (hosts) and group_vars directory.


