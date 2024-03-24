# Task-3-Python
import secrets
import string

def generate_password(length, lowercase=True, uppercase=True, digits=True, symbols=True):
  """
  Generates a random password based on user-specified criteria.

  Args:
      length: The desired length of the password.
      lowercase: Include lowercase letters (True by default).
      uppercase: Include uppercase letters (True by default).
      digits: Include digits (True by default).
      symbols: Include symbols (True by default).

  Returns:
      A randomly generated password that meets the specified criteria.
  """

  # Define character sets based on user preferences
  char_set = ""
  if lowercase:
    char_set += string.ascii_lowercase
  if uppercase:
    char_set += string.ascii_uppercase
  if digits:
    char_set += string.digits
  if symbols:
    char_set += string.punctuation

  # Validate character set availability
  if not char_set:
    raise ValueError("Please select at least one character type (lowercase, uppercase, digits, or symbols).")

  # Generate password using secrets.choice for randomness
  password = ''.join(secrets.choice(char_set) for _ in range(length))
  return password

while True:
  try:
    # Get user input for password length
    length = int(input("Enter desired password length (minimum 8 characters): "))
    if length < 8:
      raise ValueError("Password length must be at least 8 characters.")

    # Get user input for complexity preferences (default True for all)
    lowercase = input("Include lowercase letters (y/n)? ").lower() == 'y'
    uppercase = input("Include uppercase letters (y/n)? ").lower() == 'y'
    digits = input("Include digits (y/n)? ").lower() == 'y'
    symbols = input("Include symbols (y/n)? ").lower() == 'y'

    # Generate password
    password = generate_password(length, lowercase, uppercase, digits, symbols)

    # Display the password
    print("Your generated password is:", password)

    # Ask user if they want to generate another password
    choice = input("Do you want to generate another password? (y/n): ")
    if choice.lower() != 'y':
      break
  except ValueError as e:
    print("Invalid input:", e)

print("Thank you for using the password generator!")
