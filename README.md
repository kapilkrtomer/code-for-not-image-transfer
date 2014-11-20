code-for-not-image-transfer
===========================

import MySQLdb
import glob
import sys
import ast
import shutil
def main(file1):
    
    db = MySQLdb.connect("localhost","root","6Tresxcvbhy")
    cursor = db.cursor()

    sql =""" use zivame """
    cursor.execute(sql)

    f =open(file1)
    l = f.readlines()   
  
   # sys.exit()
    for line in l:
        line= ast.literal_eval(line)
        #print line
        #for info in l:
            
        sku = line[0]
        link = line[1]
        #link= "http://static11.jassets.com/p/Miss-Bennett-Black-Sweatshirts-2812-957766-1-zoom.jpg"
        #print link
        
        sql ="""update  zivame_images set failing_status ='YES' where image_link='%s' """ %(str(link.strip()))
        #print sql
        cursor.execute(sql)

        sql ="""update  zivame_data set upload_to_imgtable ='NO' where image_link='%s' """ %(str(link.strip()))
        cursor.execute(sql)   

        db.commit()

    db.close()
 

def supermain(directory):
    directory ="/home/desktop/anit/zivame/image_not_transfer"
    filelist = "%s/*.txt"%(directory)
    filepattern = glob.glob(filelist)

    
    for file1 in filepattern:
        print file1
        
        main(file1)

    try:
        shutil.rmtree('/home/desktop/anit/zivame/image_not_transfer')
    except:
        pass



if __name__=="__main__":
    directory ="/home/desktop/new_scrap/zobong_new_arivals/image_not_transfer"
    supermain(directory)
