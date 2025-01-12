# Math Test
## Challenge Description
![Screenshot 2025-01-12 180634](https://github.com/user-attachments/assets/6dedcb4d-d6a4-4430-8944-7116a9e0e0d0)  
![Screenshot 2025-01-12 180536](https://github.com/user-attachments/assets/77c55e3d-901b-4d2f-8d29-d6d61d2da2c7)  
When connecting to the server, you will need to finish 1000 of math calculation in order to get the flag.  

## Solution
```c
import socket

# Server details
HOST = "34.66.235.106"
PORT = 5000

def solve_math_challenge():
    try:
        # Connect to the server
        with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
            s.connect((HOST, PORT))
            print("Connected to the server.")

            # Receive and interact with the server
            while True:
                data = s.recv(4096).decode()
                print(data)

                # Look for a math question
                if "Question:" in data:
                    # Extract the equation
                    eqn_start = data.find("Question:") + len("Question:")
                    eqn_end = data.find("\n", eqn_start)
                    equation = data[eqn_start:eqn_end].strip()

                    # Evaluate the equation safely
                    try:
                        answer = eval(equation)
                    except ZeroDivisionError:
                        answer = 0

                    # Send the answer back
                    s.sendall(f"{answer}\n".encode())
                elif "Congratz!" in data or "Wrong!!" in data:
                    # If we win or fail, exit
                    break

    except Exception as e:
        print(f"An error occurred: {e}")

if __name__ == "__main__":
    solve_math_challenge()
```
I have created a script to connect to the server, calculate and submit the answer automatically. After all 1000 questions are answered, the flag will be printed out.  

## Challenge Flag  
uoftctf{7h15_15_b451c_10_7357_d16u153d_45_4_m47h_7357}
