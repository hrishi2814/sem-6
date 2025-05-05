# Elementary Chatbot for Customer Interaction

Here's a simple chatbot implementation using Python with either ChatterBot or NLTK. I'll provide both versions so you can choose which one works best for your needs.

## Option 1: Using ChatterBot (Simpler Implementation)

```python
from chatterbot import ChatBot
from chatterbot.trainers import ChatterBotCorpusTrainer

# Create a new chatbot
customer_bot = ChatBot(
    'Customer Support Bot',
    storage_adapter='chatterbot.storage.SQLStorageAdapter',
    logic_adapters=[
        {
            'import_path': 'chatterbot.logic.BestMatch',
            'default_response': 'I apologize, but I don\'t understand. Could you please rephrase that?',
            'maximum_similarity_threshold': 0.90
        }
    ]
)

# Train the chatbot
trainer = ChatterBotCorpusTrainer(customer_bot)
trainer.train(
    "chatterbot.corpus.english.greetings",
    "chatterbot.corpus.english.conversations"
)

# Basic interaction loop
print("Customer Support Bot: Hello! How can I help you today? (Type 'quit' to exit)")
while True:
    try:
        user_input = input("You: ")
        if user_input.lower() == 'quit':
            print("Customer Support Bot: Thank you for chatting with us!")
            break
            
        response = customer_bot.get_response(user_input)
        print(f"Customer Support Bot: {response}")
        
    except (KeyboardInterrupt, EOFError):
        print("\nCustomer Support Bot: Session ended. Have a great day!")
        break
```

## Option 2: Using NLTK (More Customizable)

```python
import random
import nltk
from nltk.chat.util import Chat, reflections

# Define conversation pairs
pairs = [
    [
        r"hi|hello|hey",
        ["Hello! How can I assist you today?", "Hi there! What can I do for you?"]
    ],
    [
        r"what is your name?",
        ["I'm a customer support chatbot. You can call me HelperBot!",]
    ],
    [
        r"how are you?",
        ["I'm functioning well, thank you! How can I help you?",]
    ],
    [
        r"(.*) help (.*)",
        ["I'd be happy to help with %2. Could you provide more details?",]
    ],
    [
        r"(.*) problem (.*)",
        ["I'm sorry to hear you're having a problem with %2. Let me assist you.",]
    ],
    [
        r"quit|bye|exit",
        ["Thank you for contacting us. Have a great day!", "Goodbye! Come back if you have more questions."]
    ],
    [
        r"(.*)",
        ["I'm not sure I understand. Could you rephrase that?", 
         "I want to help, but I didn't get that. Can you explain differently?"]
    ]
]

# Create the chatbot
def customer_chatbot():
    print("Customer Support Bot: Hello! How can I help you today? (Type 'quit' to exit)")
    chat = Chat(pairs, reflections)
    chat.converse()

if __name__ == "__main__":
    nltk.download('punkt')
    customer_chatbot()
```

## How to Run These Chatbots

1. **For ChatterBot version**:
   - Install requirements: `pip install chatterbot chatterbot_corpus`
   - Run the script

2. **For NLTK version**:
   - Install requirements: `pip install nltk`
   - Run the script (it will download required NLTK data first time)

## Key Features of These Chatbots

1. **Basic Conversation Handling**:
   - Greetings and farewells
   - Simple question answering
   - Default responses for unrecognized input

2. **Customization Options**:
   - Easily add more conversation patterns (in NLTK version)
   - Train with more data (in ChatterBot version)
   - Connect to a database for persistent storage

3. **Simple Interface**:
   - Text-based interaction
   - Clear exit command ('quit')

## Enhancing Your Chatbot

To make this more useful for customer service, you could:

1. Add domain-specific knowledge:
```python
# Add to NLTK pairs or train ChatterBot with:
pairs.append([
    r"(.*) return policy (.*)",
    ["Our return policy allows returns within 30 days with receipt. Would you like more details?"]
])
```

2. Connect to a knowledge base:
```python
import json

# Load FAQ from JSON file
with open('faq.json') as f:
    faq_data = json.load(f)
    
# Add to your response logic
for question, answer in faq_data.items():
    pairs.append([question, [answer]])
```

3. Add simple memory:
```python
context = {}

def remember_info(user_input):
    # Extract and store important information
    if "my name is" in user_input.lower():
        name = user_input.split("my name is")[1].strip()
        context['name'] = name
        return f"Nice to meet you, {name}!"
    return None
```

This provides a foundation you can build upon for more sophisticated customer interactions!