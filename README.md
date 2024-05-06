import speech_recognition as sr
import pyttsx3

# Initialize speech recognition
recognizer = sr.Recognizer()

# Initialize text-to-speech engine
engine = pyttsx3.init()

def process_command(command):
    # Here you can define different actions based on the command
    if "hello" in command:
        return "Hello! How can I assist you today?"
    elif "what's the time" in command:
        # Code to get the current time
        return "The current time is 10:00 AM"
    else:
        return "Sorry, I didn't understand that command."

def listen_for_command():
    with sr.Microphone() as source:
        print("Listening for command...")
        recognizer.adjust_for_ambient_noise(source)
        audio = recognizer.listen(source)

    try:
        print("Recognizing command...")
        command = recognizer.recognize_google(audio)
        print("You said:", command)
        return command.lower()
    except sr.UnknownValueError:
        print("Sorry, I couldn't understand what you said.")
        return ""
    except sr.RequestError:
        print("Sorry, there was an error with the speech recognition service.")
        return ""

def speak(response):
    engine.say(response)
    engine.runAndWait()

if __name__ == "__main__":
    speak("Hello! I'm your Python voice assistant.")
    while True:
        command = listen_for_command()
        if command == "exit":
            break
        response = process_command(command)
        speak(response)
