# File Parsing and Access Control Automation in Python

## Project Overview
An essential component of cybersecurity operations is managing and enforcing access control lists. In this project, I developed an automated Python algorithm to parse an organization's access file (`allow_list.txt`) and dynamically update it by removing IP addresses that no longer hold authorization to restricted network resources.

---

## Technical Objectives
* **File Operations:** Read and write external text files securely using Python's `with` statement and file handling modes (`"r"` and `"w"`).
* **Data Transformation:** Convert raw string data from text files into Python lists using `.split()` for itemized processing, and rejoin lists into formatted strings using `.join()`.
* **Conditional Logic & Iteration:** Iterate through dataset collections using `for` loops and evaluate removal criteria via `if` statements and `.remove()` methods.
* **Function Modularization:** Encapsulate the file-parsing and updating algorithm into a reusable Python function to streamline future access control administrative tasks.

---

## Step-by-Step Implementation

### 1. Opening and Reading the Access File
The initial phase opens the targeted access file (`allow_list.txt`) in read mode (`"r"`) using a `with` statement to ensure proper resource handling. The `.read()` method imports the file contents as a continuous string.

```python
import_file = "allow_list.txt"

# Open allow list file and read contents
with open(import_file, "r") as file:
    ip_addresses = file.read()
```

---

### 2. Converting String Data into a List
To analyze and evaluate individual IP addresses, the raw string dataset is converted into a list using the .split() method. By default, .split() separates elements based on whitespace characters.

```python
# Convert IP address string into an iterable list
ip_addresses = ip_addresses.split()
```

---

### 3. Iterating and Removing Revoked IP Addresses
A for loop iterates through every entry in the ip_addresses list. Inside the loop, a conditional if statement checks whether the current IP exists within the predefined remove_list. If matched, the address is removed from the ip_addresses list using .remove().

```python
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

# Evaluate each IP and remove unauthorized entries
for element in ip_addresses:
    if element in remove_list:
        ip_addresses.remove(element)
```

---

### 4. Rejoining Data and Rewriting the Allow List File
To update the original text file, the modified list is converted back into a space-delimited string using the .join() method. The file is then re-opened in write mode ("w"), completely overwriting the old content with the updated access list.

```python
# Reconstruct list back into a space-separated string
ip_addresses = " ".join(ip_addresses)

# Overwrite original allow_list.txt file with updated entries
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

---

### Modular Implementation (Reusable Function)
To operationalize this algorithm for ongoing administrative tasks, all parsing and file-handling logic was encapsulated into a single Python function named update_file().

```python
def update_file(import_file, remove_list):
    """
    Parses an access file, removes specified IP addresses,
    and updates the destination text file.
    """
    # Read file
    with open(import_file, "r") as file:
        ip_addresses = file.read()

    # Convert string to list
    ip_addresses = ip_addresses.split()

    # Iterate and remove unauthorized IPs
    for element in ip_addresses:
        if element in remove_list:
            ip_addresses.remove(element)

    # Convert back to string format
    ip_addresses = " ".join(ip_addresses)

    # Overwrite file with updated allow list
    with open(import_file, "w") as file:
        file.write(ip_addresses)


# Example Execution:
revoke_ips = ["192.168.25.60", "192.168.140.81", "192.168.203.198"]
update_file("allow_list.txt", revoke_ips)

# Verification Read:
with open("allow_list.txt", "r") as file:
    updated_text = file.read()

print("Updated Allow List Contents:")
print(updated_text)
```

---

### Summary & Security Impact
* **Automated Privilege Management:** Replaced manual text editing with an automated Python script, reducing human error when modifying critical security boundary files.

* **Code Reusability:** Modularizing the solution into update_file() allows security operations teams to integrate this logic into larger security orchestration pipelines or run scheduled access review workflows effortlessly.

* **Data Processing Efficiency:** Leveraging Python string manipulation (.split(), .join()) and file management methods provides a scalable foundation for handling larger network access logs and security intelligence lists.

*[To view the full documentation]*(./python-access-control-automation/python_access_contol_automation_full_documentation.pdf)
