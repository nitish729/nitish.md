import speech_recognition as sr
import pyttsx3
import os

# Voice Setup
engine = pyttsx3.init()
def speak(text):
    print(f"AI: {text}")
    engine.say(text)
    engine.runAndWait()

def listen():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("\nListening...")
        r.pause_threshold = 1
        audio = r.listen(source)
    try:
        query = r.recognize_google(audio, language='en-in')
        print(f"User: {query}\n")
    except Exception:
        return "None"
    return query.lower()

def ai_utility():
    speak("Hello Nitish, I am your System Assistant. How can I help you today?")
    
    while True:
        command = listen()

        if 'clean' in command or 'boost' in command:
            speak("Cleaning temporary files for you.")
            # Yahan purana clear_temp function call karein
            os.system('del /s /f /q %temp%\\*.*')
            speak("System cleaned successfully.")

        elif 'status' in command or 'activation' in command:
            speak("Checking system activation status.")
            os.system('cscript //nologo %systemroot%\\system32\\slmgr.vbs /xpr')

        elif 'install' in command:
            speak("Which app should I install? Chrome or VLC?")
            app = listen()
            if 'chrome' in app:
                os.system('winget install Google.Chrome')
                speak("Installing Chrome.")

        elif 'exit' in command or 'stop' in command:
            speak("Goodbye! Have a great day.")
            break

if __name__ == "__main__":
    ai_utility()
