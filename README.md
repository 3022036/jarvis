# jarvis
ai
import speech_recognition as sr 
import pyttsx3

# Initialize the recognizer and engine
recognizer = sr.Recognizer()
engine = pyttsx3.init()

# Function to speak
def speak(text):
    engine.say(text)
    engine.runAndWait()

# Function to listen
def listen():
    with sr.Microphone() as source:
        print("Listening...")
        audio = recognizer.listen(source)
        try:
            text = recognizer.recognize_google(audio)
            print("You said:", text)
            return text
        except sr.UnknownValueError:
            print("Could not understand audio")
        except sr.RequestError as e:
            print("Error with audio recognition service; {0}".format(e))

# Main loop for the virtual assistant
speak("Hello, I am your virtual assistant. How can I help you today?")
while True:
    user_input = listen()
    if user_input:
        if "who are you" in user_input:
            speak("I am your virtual assistant")
        elif "goodbye" in user_input:
            speak("Goodbye, have a nice day!")
            break
        else:
            speak("I'm sorry, I didn't understand that. Can you please repeat?")
