# Expert System for Help Desk Management

Here's a comprehensive implementation of an expert system for help desk management using Python with NLTK and PyKnow (a Python expert system library).

## Implementation

```python
import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from pyknow import *

nltk.download('punkt')
nltk.download('stopwords')

class HelpDeskSystem(KnowledgeEngine):
    @DefFacts()
    def _initial_action(self):
        yield Fact(action="greet")
        print("\nHelp Desk Expert System initialized...")
        print("Type 'quit' to exit\n")

    # Problem categorization rules
    @Rule(Fact(action='identify_problem'),
          OR(
              Fact(problem_type='login'),
              Fact(symptom='cannot sign in'),
              Fact(symptom='password not working')
          ))
    def login_problem(self):
        self.declare(Fact(problem_category='authentication'))
        self.declare(Fact(solution='reset password'))
        print("Solution: Please use the 'Forgot Password' link or contact IT to reset your password.")

    @Rule(Fact(action='identify_problem'),
          OR(
              Fact(problem_type='email'),
              Fact(symptom='cannot send emails'),
              Fact(symptom='email not working')
          ))
    def email_problem(self):
        self.declare(Fact(problem_category='email_system'))
        self.declare(Fact(solution='check email settings'))
        print("Solution: Verify your email client settings or try accessing webmail.")

    @Rule(Fact(action='identify_problem'),
          OR(
              Fact(problem_type='printer'),
              Fact(symptom='cannot print'),
              Fact(symptom='printer error')
          ))
    def printer_problem(self):
        self.declare(Fact(problem_category='hardware'))
        self.declare(Fact(solution='check printer connection'))
        print("Solution: Check printer connections, restart printer, and verify print queue.")

    # Default rule for unknown problems
    @Rule(Fact(action='identify_problem'),
          NOT(Fact(problem_category=W())))
    def unknown_problem(self):
        print("I couldn't identify your problem. Please contact human support with details.")

    # Solution escalation rules
    @Rule(Fact(problem_category='authentication'),
          Fact(solution='reset password'),
          NOT(Fact(password_reset_attempted=True)))
    def suggest_password_reset(self):
        self.declare(Fact(password_reset_attempted=True))
        print("Have you tried resetting your password using the company portal?")

    @Rule(Fact(problem_category='email_system'),
          Fact(solution='check email settings'),
          NOT(Fact(settings_verified=True))))
    def suggest_settings_check(self):
        self.declare(Fact(settings_verified=True))
        print("Have you verified your incoming/outgoing server settings?")

def preprocess_text(text):
    tokens = word_tokenize(text.lower())
    stop_words = set(stopwords.words('english'))
    filtered_tokens = [word for word in tokens if word not in stop_words]
    return filtered_tokens

def extract_keywords(tokens):
    problem_keywords = {
        'login': ['login', 'sign', 'password', 'authenticate'],
        'email': ['email', 'outlook', 'send', 'receive'],
        'printer': ['print', 'printer', 'scanner', 'hardware']
    }
    
    extracted = {}
    for category, keywords in problem_keywords.items():
        if any(keyword in tokens for keyword in keywords):
            extracted[category] = True
    return extracted

def main():
    engine = HelpDeskSystem()
    engine.reset()
    
    print("Help Desk Expert System: How can I assist you today?")
    
    while True:
        user_input = input("User: ").strip()
        
        if user_input.lower() == 'quit':
            print("Help Desk Expert System: Thank you for using our service. Goodbye!")
            break
            
        # Process user input
        tokens = preprocess_text(user_input)
        keywords = extract_keywords(tokens)
        
        engine.reset()
        engine.declare(Fact(action="identify_problem"))
        
        # Add extracted facts to the engine
        for category in keywords:
            engine.declare(Fact(problem_type=category))
        
        # Add symptoms if no specific problem type identified
        if not keywords:
            engine.declare(Fact(symptom=user_input.lower()))
        
        engine.run()

if __name__ == "__main__":
    main()
```

## Key Components Explained

1. **Knowledge Base**:
   - Contains rules for different problem categories (login, email, printer)
   - Includes symptom patterns that trigger specific rules
   - Has escalation paths for each problem type

2. **Inference Engine**:
   - Uses forward-chaining to process facts and apply rules
   - The PyKnow engine matches facts to rules and executes the appropriate actions

3. **Natural Language Processing**:
   - Tokenization and stopword removal using NLTK
   - Basic keyword extraction to identify problem types
   - Simple pattern matching for symptoms

4. **User Interface**:
   - Text-based interaction system
   - Processes user queries and provides solutions
   - Simple 'quit' command to exit

## How to Use This System

1. Install required packages:
```bash
pip install nltk pyknow
```

2. Run the script and interact with the help desk:
```
Help Desk Expert System: How can I assist you today?
User: I can't login to my account
Solution: Please use the 'Forgot Password' link or contact IT to reset your password.
Have you tried resetting your password using the company portal?

User: my printer isn't working
Solution: Check printer connections, restart printer, and verify print queue.

User: quit
Help Desk Expert System: Thank you for using our service. Goodbye!
```

## Enhancement Options

1. **Add More Problem Domains**:
```python
@Rule(Fact(action='identify_problem'),
      OR(
          Fact(problem_type='network'),
          Fact(symptom='no internet'),
          Fact(symptom='wifi not working')
      ))
def network_problem(self):
    self.declare(Fact(problem_category='connectivity'))
    self.declare(Fact(solution='check network cables'))
    print("Solution: Restart your router and check physical connections.")
```

2. **Integrate with Ticketing System**:
```python
import requests

def create_ticket(problem_description):
    ticket_api_url = "https://yourticketsystem.com/api/tickets"
    payload = {
        "description": problem_description,
        "category": "technical",
        "priority": "medium"
    }
    response = requests.post(ticket_api_url, json=payload)
    return response.json()
```

3. **Add Context Memory**:
```python
class HelpDeskSystem(KnowledgeEngine):
    def __init__(self):
        super().__init__()
        self.context = {}
        
    @Rule(Fact(action='store_context'),
          Fact(user_mention='my computer'))
    def store_device_context(self):
        self.context['device'] = 'computer'
        print("I'll remember you're having computer issues.")
```

This expert system provides a foundation that can be expanded with more rules, integrated with external systems, and enhanced with better NLP capabilities as needed.