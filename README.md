import re

def check_password_strength(password):
    score = 0
    feedback = []

    # Length check
    if len(password) >= 8:
        score += 1
    else:
        feedback.append("Password should be at least 8 characters long.")

    # Uppercase check
    if re.search(r'[A-Z]', password):
        score += 1
    else:
        feedback.append("Add at least one uppercase letter.")

    # Lowercase check
    if re.search(r'[a-z]', password):
        score += 1
    else:
        feedback.append("Add at least one lowercase letter.")

    # Digit check
    if re.search(r'\d', password):
        score += 1
    else:
        feedback.append("Include at least one number.")

    # Special character check
    if re.search(r'[!@#$%^&*(),.?":{}|<>]', password):
        score += 1
    else:
        feedback.append("Use at least one special character (!@#$ etc.).")

    # Strength level
    if score <= 2:
        strength = "Weak"
    elif score == 3 or score == 4:
        strength = "Moderate"
    else:
        strength = "Strong"

    return score, strength, feedback

def main():
    print("=== Password Strength Checker ===")
    password = input("Enter your password: ")

    score, strength, feedback = check_password_strength(password)

    print(f"\nPassword Strength: {strength} ({score}/5)")
    if feedback:
        print("Suggestions:")
        for f in feedback:
            print(" -", f)

if __name__ == "__main__":
    main()
