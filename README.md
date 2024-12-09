# CheckMyPass

CheckMyPass is a Python script that uses the [Have I Been Pwned API](https://haveibeenpwned.com/API/v3) to check if your passwords have been compromised in a data breach. The script ensures user privacy by implementing the k-Anonymity model.

## Features
- Uses SHA-1 hashing to secure passwords during the check.
- Leverages k-Anonymity to query the API without exposing the full password hash.
- Provides a count of how many times a password has been compromised.
- Simple command-line interface.

## Prerequisites
- Python 3.6 or higher
- `requests` library

Install the `requests` library if not already installed:
```bash
pip install requests
```

## Usage

1. Clone the repository:
```bash
git clone <repository-url>
```

2. Navigate to the project directory:
```bash
cd CheckMyPass
```

3. Run the script with passwords as arguments:
```bash
python checkmypass.py <password1> <password2> ...
```

### Example
```bash
python checkmypass.py password123 qwerty
```
Output:
```
password123 was found 12345 times.... you should change your password
qwerty was found 98765 times.... you should change your password
```

## How It Works
1. The password is hashed using SHA-1.
2. The first 5 characters of the hash (the "head") are sent to the Have I Been Pwned API.
3. The API returns all hashes that share the same 5-character prefix.
4. The script compares the "tail" of the hashed password with the API response to find matches.
5. If a match is found, the script displays how many times the password has been breached.

## Privacy
The script uses k-Anonymity, which means only the first 5 characters of the hash are sent to the API. The full hash or the plaintext password is never exposed to the API, ensuring user privacy.

## API Reference
- **URL:** `https://api.pwnedpasswords.com/range/<first5characters>`
- **Response:** A list of SHA-1 hashes sharing the same prefix and their breach counts.

## Contributing
Feel free to open issues or submit pull requests to improve this project.

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.
