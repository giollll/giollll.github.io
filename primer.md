*Some notes I took while reading throught the picoctf primer section.

ls list of directory contents

cat output the contents of <file> 

cd changes directory to <directory> 

file brings up files

egrep outputs patterns/words you search for. 

find . -type f -exec grep "picoCTF" '{}' \; -print   finds the file based on content 

unzip unzips the zip files 

wget https://jupiter.challenges.picoctf.org/static/495d43ee4a2b9f345a4307d053b4d88d/file
downloads the link adress 

egrep 'picoCTF' file  (searching for the flag picoCTF)  

cd ~/files (to put into the file directory) 

find . -name uber-secret.txt (to find the file) 

egrep 'picoCTF' file (to find content in a file) 

mmls on it to find the size of the Linux partition

nc This, of course, is the name of the program we are running. Netcat, or 'nc' as this system calls it. Sometimes the program name will be the full 'netcat' variety, but on the webshell, it is 'nc'.

saturn.picoctf.net This is the name of the computer we’re connecting to. This is a challenge server that picoCTF runs.
52279 This is the number of the port we’re connecting to for the challenge. This will probably be different for your challenge.

Block: the block layer is the second lowest level of the four layers considered here. Block layer tools are prepended with 'blk' in the Sleuthkit. blkcat is a block layer tool that 

outputs the contents of a single block. The block layer is the numbers of the disk image broken into equal-sized chunks. A single file is likely to contain multiple blocks

Inode: the inode layer is the bookkeeping layer of a disk image. It’s like the table of contents, with the chapter numbers being like the inodes, and the pages like the blocks of a 

file. Inode layer tools are prepended with 'i'. icat is an inode layer tool that outputs a single file based on its inode number.

Filename: the filename layer is one layer that most any user of a computer actually sees and interacts with. This is the layer with which we will start our exploration of the Sleuthkit in the current challenge. Interacting with the filename layer will look a lot like using the shell normally. Filename layer tools are prepended by 'f'. fls lists the files on an image starting at the root. This is what we will use for our exploration of the disk image.
decompress the challenge file:
gunzip disk.flag.img.gz 
mv my_name.txt my_info/ mv my_lastname.txt my_info/ moves both files to this directory 

echo "samuel" > my_name.txt(creating file with a name inside) 

echo "pardo" > my_lastname.txt (creating another file with last name) 

mkdir my_info (creating a directory called my_info) 

mv my_name.txt my_info/ mv my_lastname.txt my_info/ (moving files into my_info) 

zip -r my_info.zip my_info/(compressing the folder) 

Note that my_info.zip is the name we chose for our compressed file, and '-r' means recursively, which in this case means that we want to compress everything inside the folder.
rm -r my_info(removing the folder) 
unzip my_info.zip(to uncompress the folder) 
zip --encrypt -r my_protected_info.zip my_info/ (encrypting and zipping) 
gdb ./vuln1 (GDB can generate assembly from the machine code in memory while we are debugging the program so we can easily see what the machine code is doing.)
