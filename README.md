# unique-name-generatory
import random

# Predefined lists of adjectives and nouns
adjectives = ["Cool", "Happy", "Swift", "Brave", "Bright"]
nouns = ["Tiger", "Dragon", "Eagle", "Phoenix", "Lion"]

# Function to generate a random username
def generate_username(include_numbers=False, include_special_chars=False, length=None):
    # Combine random adjective and noun
    adjective = random.choice(adjectives)
    noun = random.choice(nouns)
    username = adjective + noun
    
    # Optionally include numbers
    if include_numbers:
        username += str(random.randint(0, 999))
    
    # Optionally include special characters
    if include_special_chars:
        special_chars = "!@#$%^&*"
        username += random.choice(special_chars)
    
    # Optionally set username length
    if length and len(username) > length:
        username = username[:length]
    
    return username

# Function to save usernames to a file
def save_usernames_to_file(usernames, filename="usernames.txt"):
    try:
        with open(filename, "w") as file:
            for username in usernames:
                file.write(username + "\n")
        print(f"Usernames saved to {filename}")
    except Exception as e:
        print(f"Error saving usernames to file: {e}")

# Main function to interact with the user
def main():
    print("Welcome to the Random Username Generator!")
    usernames = []
    
    # Ask user for preferences
    num_usernames = int(input("How many usernames would you like to generate? "))
    include_numbers = input("Include numbers in usernames? (yes/no): ").lower() == "yes"
    include_special_chars = input("Include special characters? (yes/no): ").lower() == "yes"
    length = input("Specify a maximum length for the usernames (press Enter to skip): ")
    length = int(length) if length.isdigit() else None
    
    # Generate usernames based on preferences
    for _ in range(num_usernames):
        username = generate_username(include_numbers, include_special_chars, length)
        usernames.append(username)
        print(username)
    
    # Save to file
    save_option = input("Would you like to save these usernames to a file? (yes/no): ").lower()
    if save_option == "yes":
        save_usernames_to_file(usernames)

if __name__ == "__main__":
    main()
