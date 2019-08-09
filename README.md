# speech-recognization
it was a small project powered by Google web search API as the recogniser class used to recognise the speech whether you speak in the microphone at the perticular time or give it a input of recording voice notes.
#!/usr/bin/env python
# coding: utf-8

# In[1]:


import pip


# In[2]:


#importing the speech recognition package from pip
import speech_recognition as sr


# In[3]:


sr.__version__


# In[4]:


#creating a recognizer class (instance)
s = sr.Recognizer()


# In[5]:


#setting the path from where we are uploading the voice
import os
os.getcwd()


# In[6]:


os.chdir("F:\datasets")


# In[7]:


first = sr.AudioFile('Recording (4).WAV')


# In[8]:


#capturing the data from the file
#it reads the data and put it in the source file which is the intence of the audiofile
#then he record method records the data in to an audiodata intence
with first as source:
    audio =s.record(source)
#we can add duretion by this code audio = s.record(source , duretion = 4)
'''The record() method, when used inside a with block, always moves ahead in the file stream. This means that
if you record once for four seconds and then record again for four seconds, the second time returns the four seconds
of audio after the first four seconds.'''
'''audio = s.record(source , duretion = 4)
   audio2 = s.record(source , duretion = 4)
   s.recognize_google(audio)
   s.recognize_google(audio2)'''


# In[9]:


#confirming the record method
type(audio)


# In[10]:


s.recognize_google(audio)


# In[11]:


#while playing anoumnimous duretion of the clip, it might possible that the clip might stop mid-phase or nmid-word , for that 
#we will use following algorithm.
with first as source:
    audio = s.record(source , offset=4 , duration=3)
    
s.recognize_google(audio)


# In[12]:


#for noise cancellation
with first as source:
    s.adjust_for_ambient_noise(source)
    #s.adjust_for_ambient_noise(source)
    audio = s.record(source)
    
s.recognize_google(audio , show_all = True)


# In[13]:


mic = sr.Microphone()


# In[14]:


sr.Microphone.list_microphone_names()


# In[24]:


#mic = sr.Microphone(device_index = 3)
#to customize the microphone if not working on default.

#to capture microphone input
with mic as source:
    s.adjust_for_ambient_noise(source) #to reduce noise in the running microphone
    audio = s.listen(source)


# In[25]:


s.recognize_google(audio) #transform the audio in to the text 
