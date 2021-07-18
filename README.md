# FRIDAY_Artificial-Intelligence
FRIDAY_Artificial-Intelligence using PYTHON


import datetime
import pyttsx3
import speech_recognition as sr
import wikipedia
import webbrowser
import os
import smtplib

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour >= 0 and hour <= 12:
        speak("Good Morning Sir..!")
        speak("Have a good start with ur morning...")
    elif hour > 12 and hour <= 18:
        speak("a Very Good AfterNoon to you Sir!!")
        speak("GReat to have you here...")
    else:
        speak("Good Evening to you Sir..")
        speak("Glad you are bacK here..")

    speak("This is Friday...speed 3.7 Geega hertz......memory 1 terrabyte....I am your assistant here.")
    speak("Please tell me Sir, How may I help you?")


def takeCommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening....")
        r.pause_threshold = 0.8
        audio = r.listen(source)

    try:
        print("Recognizing....")
        query = r.recognize_google(audio, language="en-in")
        print(f"User said : {query}\n")
    except Exception as e:
        # print(e)
        print("Say that again please..")
        return "None"
    return query

def sendEmail(to, content):
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('youremail-id', 'yourpassword')   #Your Email-id and Password, needed here.
    server.sendmail('youremail-id', to,content)    #Your EMail-id, needed.
    server.close()

if __name__ == "__main__":
    # speak("Madhur is an Astrophile and Mechanical Engineer and a Data Scientist.")
    wishMe()
    while True:
    # if 1:
        query = takeCommand().lower()
    
    # logic for excuting tasks based on Query.
        if 'wikipedia' in query:
            speak('Searching Wikipedia...')
            query = query.replace('wikipedia', "")
            results = wikipedia.summary(query, sentences=2)
            speak("According to wikipedia")
            print(results)
            speak(results)

    
        elif 'open youtube' in query :
            webbrowser.open("youtube.com")

        elif 'open google' in query:
            webbrowser.open("google.com")

        elif 'open gmail' in query:
            webbrowser.open("gmail.com")

        elif 'open linkedin' in query:
            webbrowser.open("linkedin.com")

        elif 'open my browser' in query:
            speak("opening mozzila...")
            print(speak)
            browserPath = "C:\\Program Files\\Mozilla Firefox\\firefox.exe"
            os.startfile(browserPath)
        
        elif 'open pycharm' in query:
            speak("opening pycharm IDE for you sir...")
            print(speak)
            pycharmPath = "C:\\Program Files\\JetBrains\\PyCharm Community Edition 2021.1.1\\bin\\pycharm64.exe"
            os.startfile(pycharmPath)
        
        elif 'skype' in query:
            speak("opening skype for you sir...")
            print(speak)
            skypePath = "C:\\Program Files (x86)\\Microsoft\\Skype for Desktop\\Skype.exe"
            os.startfile(skypePath)
            

        elif 'play music' and 'play some music' in query:
            music_dir =  'E:\\NewFolder\\nEw sOngs\\eng'   #Your folder source for music, needed.
            songs = os.listdir(music_dir)
            print(songs)
            os.startfile(os.path.join(music_dir, songs[0]))
        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"Sir, the time is {strTime}")
        elif 'vs code' in query:
            codePath = "C:\\Users\\mmadh\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(codePath)
        elif 'email to myfriend' in query:
            try:
                speak("What should I say?")
                content = takeCommand()
                to = "reciever's_email-id"    #Reciever's Email id needed
                sendEmail(to,content)
                speak("Your Email has been sent,Sir")
            except Exception as e:
                print(e)
                print("Sorry Sir, I am not able to send this mail.")
                speak("Sorry Sir, I am not able to send this mail.")

        elif 'goodbye' in query:
            speak('have a good day sir....It was my honour to help you...')
            print(speak)
            exit()
