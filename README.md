# Python

 

# Martian personal assistant

 

import pyttsx3

import speech_recognition as sr

import datetime

import wikipedia

import webbrowser

import os

import microphone

from webbrowser import open

import subprocess as sp

 

engine = pyttsx3.init('sapi5')

voices = engine.getProperty('voices')

# Print(voices [0].id)

engine.setProperty('voice',voices[0].id)

 

def speak(audio):

    engine.say(audio)

    engine.runAndWait()

def wishMe():

    hour = int(datetime.datetime.now().hour)

    if hour>=0 and hour<12:

        speak("Good Morning Sir")

    elif hour>=12 and hour<17:

        speak("Good Afternoon Sir")

    else:

        speak("Good Evening Sir")

    speak("I am Martian Sir. I am from Mars and I am here to help you.")

 

def takeCommand():

    r = sr.Recognizer()

    with sr.Microphone() as source:

        print("Listening...")

        r.pause_threshold = 1

        audio = r.listen(source)

 

    try:

        print("Recognizing...")

        query = r.recognize_google(audio,language = 'en-in')

        print(f"User said: {query}\n")

    except Exception as e:

        speak("Sorry Sir,I could not understand,Could you please say that again?")

        return "None"

    return query    

 

if __name__=="__main__":

    wishMe()

    while True:

        query = takeCommand().lower()

 

        if "how are you" in query:

            speak("I'm fine sir,how can i help you?")

       

 

        elif "who are you" in query:

            speak("Sir I am Martian personal aasistant")

        elif 'wikipedia' in query:

            speak("Searching Wikipedia...Please wait")

            query = query.replace("wikipedia"," ")

            results = wikipedia.summary(query,sentences = 2)

            speak("wikipedia says")

            print(results)

            speak(results)

        elif 'open youtube'in query:

            webbrowser.open("youtube.com")

        elif 'open google' in query:

            webbrowser.open('www.google.co.in')

           

        elif 'open camera' in query:

            sp.run('start microsoft.windows.camera:',shell=True)

           

        elif 'the time' in query:

            strTime = datetime.datetime.now().strftime("%H:%M:%S")

            speak(f"Sir,the time is {strTime}")

        elif 'Martian quit' in query or 'exit' in query or 'close' in query:

            speak("Thanks you for using martian sir")

            exit()

                   

 

 

