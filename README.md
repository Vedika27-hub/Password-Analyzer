# Password-Analyzer
def commonpatterns(password):
   
    commonpatterns = ["password", "123456",  "abc123", "iloveyou"]
    for pattern in commonpatterns:
        if pattern in password.lower():
            return True
    return False

def calculatestrength(password):
   
    score = 0
    suggestion = []

    
    if len(password) > 15:
        score += 3
    elif 12 <= len(password) <= 15:
        score += 2
    else:
        score -= 2
        suggestion.append("Increase the length of your password to at least 12 characters.")

   
    if any(char.isupper() for char in password):
        score += 2
    else:
         suggestion.append("Add at least one uppercase letter.")

   
    if any(char.islower() for char in password):
        score += 2
    else:
        suggestion.append("Add at least one lowercase letter.")

   
    if any(char.isdigit() for char in password):
        score += 2
    else:
        suggestion.append("Add at least one number.")

   
    specialcharacters = "!@#$%^&*(),.?\":{}|<>"
    if any(char in specialcharacters for char in password):
        score += 3
    else:
         suggestion.append("Add at least one special character (e.g., !, @, #, etc.).")

    
    if commonpatterns(password):
        score -= 5
        suggestion.append("Avoid using common passwords or patterns like '123456' or 'password'.")

    
    if score >= 8:
        strength = "Strong"
    elif 4 <= score < 8:
        strength = "Moderate"
    else:
        strength = "Weak"

    return score, strength, suggestion



if __name__ == "__main__":
   
    password = input("Enter a password to analyze: ")

    score, strength, suggestion = calculatestrength(password)

    print(f"\nPassword Score: {score}")
    print(f"Password Strength: {strength}")

    if suggestion:
        print("\nSuggestions for improvement:")
        for suggestion in suggestion:
            print(f"- {suggestion}")
