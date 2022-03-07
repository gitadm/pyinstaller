# Building python2 executable in CentOS7


## Install pyinstaller 

*  Get PyInstaller for python2.  https://pypi.org/project/pyinstaller/2.0/#files

*  Check PyInstaller for python2 packages. https://pypi.org/project/pyinstaller/2.0/#files

* Download Pyinstaller2.0 package wget https://files.pythonhosted.org/packages/ec/a3/dc7bc8c48a873c3156866df709a23078a6dda86db88328df5cf639385527/pyinstaller-2.0.tar.bz2
 
* Unzip the bz2 :  bunzip2 pyinstaller-2.0.tar.bz2
 
* Extract the tar file : tar xvf pyinstaller-2.0.tar
 
* Check files in extracted path
###
       cd pyinstaller-2.0/
       [root@buildserver pyinstaller-2.0]# ll
       total 48
       drwxr-xr-x. 8 admin admin 4096 Aug  8  2012 buildtests
       drwxr-xr-x. 5 admin admin 4096 Aug  8  2012 doc
       drwxr-xr-x. 4 admin admin   31 Aug  8  2012 e2etests
       drwxr-xr-x. 2 admin admin 4096 Aug  8  2012 examples
       -rw-r--r--. 1 root  root    45 May  7 02:48 howto.txt
       -rw-r--r--. 1 admin admin   18 Aug  8  2012 MANIFEST.in
       drwxr-xr-x. 8 admin admin 4096 Aug  8  2012 PyInstaller
       -rwxr-xr-x. 1 admin admin 3244 Aug  8  2012 pyinstaller-gui.py
       -rwxr-xr-x. 1 admin admin 2718 Aug  8  2012 pyinstaller.py
       -rw-r--r--. 1 admin admin 1741 Aug  8  2012 README.rst
       -rw-r--r--. 1 admin admin 3778 Aug  8  2012 setup.py
       drwxr-xr-x. 8 admin admin 4096 Aug  8  2012 source
       drwxr-xr-x. 4 admin admin  101 Aug  8  2012 support
       drwxr-xr-x. 2 admin admin 4096 Aug  8  2012 utils
       [root@buildserver pyinstaller-2.0]#
 
## Example Command to build: 03/06/2022
python pyinstaller.py /path/to/yourscript.py
 
 
## Verify pyinstaller working
### Create a test python source script to build into binary : 

 
    [root@k8s-master python]# cat > example1.py  << "#EOF"
    import sys
    import os

    def mainProgram():
       print("This is a test")


    if __name__ == "__main__":
      mainProgram()

    #EOF


### Run pyinstaller to build a binary : 

     [root@buildserver pyinstaller-2.0]# ./pyinstaller.py -D -F -n  example1 -c example1.py
     INFO: wrote /root/pyinstaller-2.0/example1/example1.spec
     INFO: UPX is not available.
     INFO: checking Analysis
     INFO: building Analysis because out00-Analysis.toc non existent
     INFO: running Analysis out00-Analysis.toc
     INFO: Analyzing /root/pyinstaller-2.0/support/_pyi_bootstrap.py
     INFO: Analyzing /root/pyinstaller-2.0/PyInstaller/loader/archive.py
     INFO: Analyzing /root/pyinstaller-2.0/PyInstaller/loader/carchive.py
     INFO: Analyzing /root/pyinstaller-2.0/PyInstaller/loader/iu.py
     INFO: Analyzing example1.py
     INFO: Hidden import 'encodings' has been found otherwise
     INFO: Looking for run-time hooks
     INFO: Analyzing rthook /root/pyinstaller-2.0/support/rthooks/pyi_rth_encodings.py
     INFO: Warnings written to /root/pyinstaller-2.0/example1/build/pyi.linux2/example1/warnexample1.txt
     INFO: checking PYZ
     INFO: rebuilding out00-PYZ.toc because out00-PYZ.pyz is missing
     INFO: building PYZ out00-PYZ.toc
     INFO: checking PKG
     INFO: rebuilding out00-PKG.toc because out00-PKG.pkg is missing
     INFO: building PKG out00-PKG.pkg
     INFO: checking EXE
     INFO: rebuilding out00-EXE.toc because example1 missing
     INFO: building EXE from out00-EXE.toc
     INFO: Appending archive to EXE /root/pyinstaller-2.0/example1/dist/example1
     [root@buildserver pyinstaller-2.0]#

### Test the binary : 

     [root@buildserver dist]# /root/pyinstaller-2.0/example1/dist/example1
     This is a test
     [root@buildserver dist]#

### Further 

Create a build script to ensure a unique version.

keep build release in a relese path

### *** END ***
