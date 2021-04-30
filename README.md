# speech-to-text-
speech to text lobby project 
import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import 

listener = sr.Recognizer()
engine = pyttsx3.init()


def talk(text):
    engine.say(text)
    engine.runAndWait()


def take_command():
    try:
        with sr.Microphone() as source:
            print('listening....')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'alexa' in command:
                command = command.replace('alexa', '')
                talk(command)
    except:
        pass
    return command


def run_alexa():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play', '')
        talk('playing' + song)
        pywhatkit.playonyt(song)
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        print(time)
        talk('çurrent time is' + time)
    elif 'who is ' in command:
        person = command.replace('who is ', '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)
    elif 'date' in command:
        talk('sorry i have and fever')
    elif 'are you single' in command:
        talk('i am in relationship with wifi')
    elif 'joke' in command:
        talk(pyjokes.get_jokes())
    else:
        talk('please say it once again.')


while True:
    run_alexa()

