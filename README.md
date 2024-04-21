# python-voice-assistance
import speech_recognition as sr
import webbrowser

#Initialize speech recognition engine
recognizer = sr.Recognizer()

#Function to recognize speech
def listen():
    with sr.Microphone() as source:
        print("Adjusting for ambient noise...")
        recognizer.adjust_for_ambient_noise(source, duration=1)
        print("Listening...")
        audio = recognizer.listen(source)

    try:
        print("Recognizing...")
        command = recognizer.recognize_google(audio)
        print("You said:", command)
        return command.lower()
    except sr.UnknownValueError:
        print("Sorry, I couldn't understand what you said.")
        return ""
    except sr.RequestError as e:
        print("Could not request results from Google Speech Recognition service; {0}".format(e))
        return ""

#Function to open websites
def open_website(website_name):
    websites = {
        "google": "https://www.google.com",
        "youtube": "https://www.youtube.com",
        
        
    }

    if website_name in websites:
        webbrowser.open(websites[website_name])
        print(f"Opening {website_name}...")
    else:
        print(f"Sorry, I don't know how to open {website_name}.")

    # Acknowledge the command to open a website
    print("Opening website...")

# Main function
def main():
    print("Hello! How can I assist you today?")
    while True:
        command = listen()
        if "hello" in command:
            print("Hello there!")
        elif "how are you" in command:
            print("I'm doing well, thank you!")
        elif "what is your name" in command:
            print("My name is Python Voice Assistant.")
        elif "who is the Prime Minister of India" in command:
            print("The Prime Minister of India is Narendra Modi.")
        elif "open" in command:
            words = command.split()
            if "website" in words:
                website_index = words.index("website")
                website_name = words[website_index + 1]
                open_website(website_name)
            else:
                print("Sorry, I couldn't understand which website to open.")
        elif "exit" in command:
            print("Goodbye!")
            break
        else:
            print("I'm not sure how to help with that.")

if __name__ == "__main__":
    main()

