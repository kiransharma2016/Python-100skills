#### this script split an yaml file into different yaml file based on --- the yaml starter. 

import time
import os, shutil, fnmatch

with open("dashboard.yaml", "r") as file: # Use file to refer to the file object
  #data = file.readlines()

  a = 1
  kindw = ""
  namew =""
#print (data)

  for line in file:

    filefr = str(a)+ ".yml"
    #print ("filename  :"+filefr)

    #print("I  am here :"+ filefr)

    if ( os.path.exists(filefr) ):
       #print( "File exists")

       if ( line.strip().split(":")[0] == "kind"):
             kindw = (line.strip().split(":")[1]).strip()
       elif( line.strip().split(":")[0] == "name"  and len(namew) == 0 ):
             namew = (line.strip().split(":")[1]).strip()

       if ( (line.strip()) == "---"):
          #print (" check mistake")
          fw.close()

          print ("kind:" + kindw)
          print ("name: " + namew)

          dst=kindw.strip() + ".yml"
          if ( os.path.exists(dst) ):
              dst = kindw+str(1)+".yml"

          shutil.move(filefr,dst.strip())

          kindw = ""
          namew = ""

          a = a + 1
          continue
       elif ( len(line.strip() ) != 0 ):
          fw.write(line)
    else:
         fw = open(filefr,"w")
         fw.write("---\n")


  dst=kindw.strip() + ".yml"
  shutil.move(filefr,dst)
  print (filefr)
  print ("kind:" + kindw)
  print ("name: " + namew)
