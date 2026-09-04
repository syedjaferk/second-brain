---
layout: post
title: 'Tool: Serial Activity - Remote SSH Manager'
date: 2024-08-20 02:16:20+00:00
render_with_liquid: false
category: SSH Management
tags:
- Remote SSH
- Automation
- Python Scripting
- Machine Learning
- Network Configuration
---



<h3 class="wp-block-heading">Why this tool was created ?</h3><p class="wp-block-paragraph">During our college times, we had a crash course on Machine Learning. Our coordinators has arranged an ML Engineer to take class for 3 days. He insisted to install packages to have hands-on experience. But unfortunately many of our people were not sure about the installations of the packages. So we need to find a solution to install all necessary packages in all machines.</p><p class="wp-block-paragraph">We had a scenario like, all the machines had <strong>one specific same user account</strong> <strong>with same password</strong> for all the machines. So we were like; if we are able to automate it in one machine then it would be easy for rest of the machines ( Just a for-loop iterating the x.0.0.1 to x.0.0.255 ). This is the birthplace of this tool.</p><h3 class="wp-block-heading">Code=-</h3><pre class="wp-block-syntaxhighlighter-code">#!/usr/bin/env pythonimport sysimport os.pathfrom multiprocessing.pool import ThreadPoolimport paramikoBASE_ADDRESS = "192.168.7."USERNAME = "t1"PASSWORD = "uni1"def create_client(hostname):    """Create a SSH connection to a given hostname."""    ssh_client = paramiko.SSHClient()    ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())    ssh_client.connect(hostname=hostname, username=USERNAME, password=PASSWORD)    ssh_client.invoke_shell()    return ssh_clientdef kill_computer(ssh_client):    """Power off a computer."""    ssh_client.exec_command("poweroff")def install_python_modules(ssh_client):    """Install the programs specified in requirements.txt"""    ftp_client = ssh_client.open_sftp()    # Move over get-pip.py    local_getpip = os.path.expanduser("~/lab_freak/get-pip.py")    remote_getpip = "/home/%s/Documents/get-pip.py" % USERNAME    ftp_client.put(local_getpip, remote_getpip)    # Move over requirements.txt    local_requirements = os.path.expanduser("~/lab_freak/requirements.txt")    remote_requirements = "/home/%s/Documents/requirements.txt" % USERNAME    ftp_client.put(local_requirements, remote_requirements)    ftp_client.close()    # Install pip and the desired modules.    ssh_client.exec_command("python %s --user" % remote_getpip)    ssh_client.exec_command("python -m pip install --user -r %s" % remote_requirements)def worker(action, hostname):    try:        ssh_client = create_client(hostname)        if action == "kill":            kill_computer(ssh_client)        elif action == "install":            install_python_modules(ssh_client)        else:            raise ValueError("Unknown action %r" % action)    except BaseException as e:        print("Running the payload on %r failed with %r" % (hostname, action))def main():    if len(sys.argv) &lt; 2:        print("USAGE: python kill.py ACTION")        sys.exit(1)    hostnames = [str(BASE_ADDRESS) + str(i) for i in range(30, 60)]    with ThreadPool() as pool:        pool.map(lambda hostname: worker(sys.argv[1], hostname), hostnames)if __name__ == "__main__":    main()</pre><p class="wp-block-paragraph"></p>


## Related Posts
- [[ACESS YOUR LOCAL APPLICATION VIA INTERNET]]
- [[Locust EP 3: Simulating Multiple User Types in Locust]]
- [[Can UV Transform Python Scripts into Standalone Executables ?]]
- [[🚀 #FOSS: Mastering Superfile: The Ultimate Terminal-Based File Manager for Power Users]]
- [[Docker Ep 8: Tomcat: Exploring Docker Port Mapping and Logs]]

