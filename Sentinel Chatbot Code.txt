##
# First we import all the important libraries #


import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
print(voices[0].id)
engine.setProperty('voice',voices[0].id)

def sentinelvoice(audioinput):
    engine.say(audioinput)
    engine.runAndWait()

def wish():
    hour = int(datetime.datetime.now().hour)
    print("----->",hour)
    if hour>=0 and hour<12:
        sentinelvoice("Good Morning User, I am Sentinel , What can i do for you")
    elif hour>=12 and hour<=18:
        sentinelvoice("Good Afternoon User, I am Sentinel,What can i do for you")
    else:
        sentinelvoice("Good Evening User, I am Sentinel,What can i do for you")

def takecommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("listening...")
        r.pause_thresold=1
        audio = r.listen(source)
    try:
        print("Recognizing...")
        query = r.recognize_google(audio,language='en-in')
        print("Query: ",query)
    except Exception as e:
        print(e)
        print("sorry, I didn't get you. Say that again please")
        print("contact  Yash Jadhav at yashj3291@gmail.com")
        return "None"
    return query

wish()

status = True
while status:
    query = takecommand().lower()
    
    if "What is" in query or "who is" in query:
        sentinelvoice("searching in wikipedia")
        query = query.replace("wikipedia","")
        result = wikipedia.summary
        print(result)
        sentinelvoice("According to wikipedia...")
        sentinelvoice(result)
        
    elif "spotify" in query:
        webbrowser.open("spotify.com")
    elif "youtube" in query:
        webbrowser.open("youtube.com")
    elif "today's weather" in query:
        webbrowser.open("windy.com")
    elif "feeling hungry" in query:
        webbrowser.open("zomato.com")
    elif "amazon" in query:
        webbrowser.open("amazon.in")
    elif "movie ticket" in query:
        webbrowser.open("bookmyshow.com")
    elif "todays update" in query:
        webbrowser.open("news.google.com")
    elif "vaccination" in query:
        webbrowser.open("cowin.gov.in")
    elif "get me a doctor" in query:
        webbrowser.open("practo.com")
    elif "google meet" in query:
        webbrowser.open("meet.google.com")
    elif "instagram" in query:
        webbrowser.open("instagram.com")
    else:
        webbrowser.open("google.com")