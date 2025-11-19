# Voice-to-text-converter
import speech_recognition as sr

def voice_to_text(output_file="output.txt"):
    recognizer = sr.Recognizer()

    with sr.Microphone() as source:
        print("Speak something...")

        recognizer.adjust_for_ambient_noise(source)
        audio = recognizer.listen(source)

    try:
        print("Converting speech to text...")
        text = recognizer.recognize_google(audio)
        print("You said:", text)

        with open(output_file, "w", encoding="utf-8") as f:
            f.write(text)

        print(f"Saved to {output_file}")

    except sr.UnknownValueError:
        print("Could not understand audio")
    except sr.RequestError:
        print("Could not connect to Google Speech API")

voice_to_text() 
