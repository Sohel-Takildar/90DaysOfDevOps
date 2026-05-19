# kernel --
  Kernel is the Brain of the Opreating System.

# user --
 user is a person who uses a computer or system.

# space --
 space in an area or place available for use.

# init/systemd --
  init/systemd is the first process that start when Linux boots and manges system services.

# How processes are created and managed --
  Processes are created when a program starts and managed by the operating system using commands like ps,top,and kill.

# What systemd does and why it matters --
  Systemd manages system service and control the Linux boot process.
  It matter because it keeps the system running properly and manages services easily.

# Explain **process states** (running, sleeping, zombie, etc.)
--
# "process states "
   When a program run in Linux , it goes through different process states.

   1 - Running (R) 
       The process is currently using the CPU or ready to learn.

   2 - Sleeping (S)
       The process is waiting for an event or user input.

   3 - Zombie (Z) 
       The process has finished its work but the parent process has not yet collected its exit status.

    
 ##  These commands show process states in Linux. ##

    ps aux 
     
  or
      
     top

# 5 Important Commands ---
    1 - ps  
    ps aux

    2 - top
    top

    3 - systemctl
    systemctl statues nginx

    4 - kill
    kill PID

    5 - journalctl
    journalctl -xe
