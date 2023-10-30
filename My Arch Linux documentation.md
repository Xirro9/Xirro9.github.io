# My Arch Linux documentation
## Mahin Moon

after a quick skim of the arch linux wiki I get a jist of what I have to do.

downloading an iso from the first link in the american iso files

okay so after the iso is installed I need to configure the VM so that the iso will run
I changed the ram size to **2G** and set the hard drive space to **16G**, I also turned on 3D graphics and set the graphics ram to **2G** 

so after loading in the iso and letting it all run I am introduced to an all black screen with text, this resembles what I know as a terminal but is actually the entire operating system as of now.

Side note: 
> the whole OS being a command terminal is kinda awsome, it feels so raw and cool to mess with

so now I have to partition the hard drive myself, I looked over the wiki again but honestly have no idea what I am really doing

I ended up finding a guide on how to partition the disk

side note:
> I also found out about the 'archinstall' command and have used it to have a fully functioning arch linux setup on a seperate vm just to see if it was really that simple. I am not going to use it beacuse there would be no way to document it and im pretty sure it would go against the assigment to use it

first thing I did was run
```
cfdisk /dev/sda
```
and I selected gpt ("l-like ch-ch-CHATGPT?!?!")

I made a New partition and made it 1 megabyte in size and chose the 'boot partition option'
then I made a 'Linux Swap' partition 4**G** in size
the remaining 12**G** I made 'Linux file system' so that my VM can use that space
then I pressed the 'write' button, saving my changes
now to format the partitions

first I ran 
```
mkfs.ext4 /dev/sda3
```

then I partitioned the swap by running
```
mkswap /dev/sda2
swapon -a
```

then we mount our disk
```
mount /dev/sda3 /mnt
```

Now I am going to run pacstrap, installing a few things 
```
pacstrap /mnt base linux linux-firmware nano grub dhcpcd
```
this took a long while but it loaded all of the OS files and some extras

now I am going to run
```
genfstab /mnt
genfstab /mnt >> /mnt/etc/fstab
arch-chroot /mnt
```
 honestly not too sure what did there, just following the guide
 
 now we setup the root password by inputting
```
passwd
```
after typeing and confirming the password, the root user now has a password

and with that we are done with the base installation and ready to reboot by running 
```
reboot
```

Now I have a fully working install of arch-linux

I made my user here and set my password
```
useradd Mahin
passwd Mahin
```

then I installed sudo
```
pacman -S sudo
```

This is still just a large command terminal so its time to install a DE

after a little googleing I decided to install Plasma KDE

first I made sure all packages are up to date:
```
sudo pacman -Syu
```

now to install xorg
```
sudo pacman -S xorg
```

after xorg finishes installing I ran
```
sudo pacman -S plasma-meta kde-applications
```

now to enable a few services 
```
sudo systemctl enable sddm
```

now we reboot into a login screen 
```
reboot
```

I loaded into sddm and logged into my user, bringing me to a fully functioning desktop enviornment

I created a user for codi and set its password, then I expired the password to force the user to change their password as soon as they log in.
```
useradd codi
passwd codi
passwd -e codi
```

now, I could setup a wheel group and set things to make my users sudoers that way, but I got lazy and just edited the /etc/sudoers file, I know its not reccomended but this is my vm and the users are both now sudoers

then I installed zsh
```
sudo pacman -S zsh
```

now if I run 'zsh' in my terminal it will switch from bash to zsh

I installed ssh
```
sudo pacman -S openssh
```

note: 
> The class gateway is not working
> Update: monday: you said you no longer have a class gateway
> The command 'systemctl status sshd' shows that my ssh is active so I think that is enough to prove ssh is on my vm


Now I need to add color to the terminal
I found a tutorial online
I downloaded this guys files on my vm, then ran 'nano DIR_COLORS' to customize the colors to what I wanted.
then I executed the following commands
```
sudo mv bash.bashrc /etc/bash.bashrc
sudo mv DIR_COLORS /etc/
mv .bashrc ~/.bashrc
```
after I restarted my terminal, the terminal had color

My system already boots up to the GUI DE, I did that while partitioning my drives so that part is done.

Finally I ran the following commands to add a few aliases
```
alias brc='.bashrc'
alias BRC='.bashrc'
alias bashrc='.bashrc'
```

With that done I have a fully working arch linux system setup with all the parameters fufilled.

Now time for the video.
