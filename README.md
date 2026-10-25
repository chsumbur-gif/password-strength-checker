# password-strength-checker


import string


def check_password_strength(password):
    score = 0
    suggestions = []

    # 1. Check password length
    if len(password) >= 12:
        score += 1
    else:
        suggestions.append("Use at least 12 characters.")

    # 2. Check uppercase letters
    if any(char.isupper() for char in password):
        score += 1
    else:
        suggestions.append("Add an uppercase letter (A-Z).")

    # 3. Check lowercase letters
    if any(char.islower() for char in password):
        score += 1
    else:
        suggestions.append("Add a lowercase letter (a-z).")

    # 4. Check numbers
    if any(char.isdigit() for char in password):
        score += 1
    else:
        suggestions.append("Add a number (0-9).")

    # 5. Check special characters
    if any(char in string.punctuation for char in password):
        score += 1
    else:
        suggestions.append("Add a special character (!, @, #, etc.).")

    # 6. Determine password strength
    if score <= 2:
        strength = "WEAK"
    elif score <= 4:
        strength = "MODERATE"
    else:
        strength = "STRONG"

    return strength, score, suggestions


def main():
    print("=" * 40)
    print("     PASSWORD STRENGTH CHECKER")
    print("=" * 40)

    password = input("Enter your password: ")

    if not password:
        print("Error: Password cannot be empty.")
        return

    strength, score, suggestions = check_password_strength(password)

    print("\n--- PASSWORD REPORT ---")
    print("Strength:", strength)
    print(f"Criteria passed: {score}/5")

    if suggestions:
        print("\nSuggestions for improvement:")
        for suggestion in suggestions:
            print("-", suggestion)
    else:
        print("\nAll five basic checks passed!")

    print("\nNote: This is a basic strength estimate,")
    print("not a guarantee that your password is secure.")


if __name__ == "__main__":
    main()
