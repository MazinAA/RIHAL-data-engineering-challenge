from PIL import Image
import re
import datefinder
from pytesseract import image_to_string, pytesseract

pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"#optical character recognition (OCR) tool
image_path = r"C:\Users\hp\Desktop\cv\job teste\RIHAL\image.png"#where image saved
image = Image.open(image_path)#open image
text = image_to_string(image, lang='deu')#convert image to the text

# print(text[:-1])#shows full email as text

pattern1 = r'(<[a-zA-Z0-9-\.]+@[a-zA-Z-\.]*[com|om]>)'#for find emails from text
match1 = re.findall(pattern1, text)#to find the matching results in text
print(match1)#print email result as output

pattern2 = datefinder.find_dates(text)#use datefider tool to find dates
for match2 in pattern2:#to get the matching results from the text
    print(match2)#ptint the reselt

pattern3 = r'Rate: ([$a-zA-Z0-9]+)'#to find the rates
match3 = re.findall(pattern3, text)#to get the matching results from the text
print(match3)#print rates result as output

pattern4 = r'Room: ([a-zA-Z]+)'#to find room names
match4 = re.findall(pattern4, text)#to get matching result
print(match4)#print the room names result as output

pattern5 = r'[\w][a-zA-Z][\s]*[A-Za-z]+, [A-Z][a-z-]+'#to find the first and last names
match5 = re.findall(pattern5, text)#to get the matching result
for i in match5:#Definition of each section in match5
    i = i.split(",")#divide it after (,)
    i = i[::-1]#to invert it
    fullname = ",".join(i)#ro join it agin
    divider = ","
    fullname = divider.join(i)#save finall rasult in fullname
    print(fullname)#print the fullname result as output
