# -*- coding: utf-8 -*-
"""
Created on Sun Apr 15 17:00:57 2018

@author: Shyam
"""

import tensorflow as tf
import keras
import scipy
import sklearn
import matplotlib
import pandas as pd
import cv2
import numpy as np
import os
import pytesseract
import glob
os.chdir('C:\stuff\Studies\Spring 18\Data Mining\Project')
from PIL import Image
import re

#Following for reading words from text and counting it
file_name = '19981212022913.png'
text = pytesseract.image_to_string(Image.open(file_name))

#Counting words in texts
array_text = text.split(' ')
#print(array_text)
array_text_new = []
for x in array_text:
    temp_array = x.split('\n')
    for element in temp_array:     
        if element.strip() != '':
            array_text_new = array_text_new + [element]
    
#array_text_new = [x.split('\n') for x in array_text]
print(array_text_new)
print("Lenght of words is " + str(len(array_text_new)))


#Surbhi's Code for reading files
def getFiles(path):
    """
    - returns  a dictionary of all files 
    having year:[img1,img2,img3....]

    """
    
    imlist = {}
    count = 0
    for each in os.listdir(path):

        print (" #### Reading image category ", each, " ##### ")
        #imlist[each] = []
        path1 = path+'\\'+each
        
        for imagefile in os.listdir(path1):

            print ("Reading file ", imagefile)
            if imagefile[:4] not in imlist.keys():
                imlist[imagefile[:4]] = []

            im = cv2.imread(path1+'\\'+imagefile)
            #im1 = cv2.resize(im,(227, 227), interpolation = cv2.INTER_CUBIC)
            imlist[imagefile[:4]].append(im)
            count +=1

    return [imlist, count]

path = r"D:\Archive"
img_dict,count = getFiles(path)


imlist = {}
count_total = 0
for each in os.listdir(path):

    print (" #### Reading image category ", each, " ##### ")
    imlist[each] = {}
    #imlist[each] = []
    path1 = path+'\\'+each
    
    for imagefile in os.listdir(path1):

        #print ("Reading file ", imagefile)
        try:
            imlist[each][imagefile[:4]]
        except:
            imlist[each][imagefile[:4]] = {}
            imlist[each][imagefile[:4]]['Count_Images'] = 0
            imlist[each][imagefile[:4]]['Words_Images'] = 0

        #im = cv2.imread(path1+'\\'+imagefile)
        imlist[each][imagefile[:4]]['Count_Images'] += 1
        text = pytesseract.image_to_string(Image.open(path1+'\\'+imagefile))
        
        array_text = text.split(' ')
        #print(array_text)
        array_text_new = []
        for x in array_text:
            temp_array = x.split('\n')
            for element in temp_array:     
                if element.strip() != '':
                    array_text_new = array_text_new + [element]
                    
        words_in_image = len(array_text_new)
        imlist[each][imagefile[:4]]['Words_Images'] += words_in_image
        #im1 = cv2.resize(im,(227, 227), interpolation = cv2.INTER_CUBIC)
        count_total +=1
        print("Done No of images is " + str(count_total))


#Count by year
    
#REading from images already stored, manually deleted useless keys

year_dictionary = {}
for key in list(imlist.keys()):
    for year in imlist[key]:
        try:
            year_dictionary[year]
        except:
            year_dictionary[year] = {}
            year_dictionary[year]['Count_of_Words'] = 0
            year_dictionary[year]['Count'] = 0            
        year_dictionary[year]['Count_of_Words'] += imlist[key][year]['Words_Images']
        year_dictionary[year]['Count'] += imlist[key][year]['Count_Images']
        






