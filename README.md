            password = ''.join(attempt)
            print(f"Trying password: {password}", end='\r')
            try:
                with zipfile.ZipFile(zip_file) as zip_file_ref:
                    zip_file_ref.extractall(pwd=password.encode('utf-8'))
                found = True
                end_time = time.time()
                print(f"\n\033[1m\033[92mPassword found: {password}\033[0m")
                print(f"\033[1m\033[92mTime taken: {end_time - start_time} seconds\033[0m")
                return
            except Exception as e:
                pass
    if not found:
        print("\n\033[1m\033[91mPassword not found\033[0m")
def crack_zip_wordlist(zip_file, wordlist):
    print(f"\nCracking ZIP file: {zip_file}\n")
    print(f"Using wordlist: {wordlist}\n")
    start_time = time.time()
    with open(wordlist, 'r') as f:
        for line in f:
            password = line.strip()
            print(f"Trying password: {password}", end='\r')
            try:
                with zipfile.ZipFile(zip_file) as zip_file_ref:
                    zip_file_ref.extractall(pwd=password.encode())
                end_time = time.time()
                print(f"\n\033[1m\033[92mPassword found: {password}\033[0m")
                print(f"\033[1m\033[92mTime taken: {end_time - start_time} seconds\033[0m")
                return
            except Exception as e:
                pass
    print("\nPassword not found")
def main():
    Saeed_hackers_banner()
    Saeed_zipper_banner()
    print("Choose a method:")
    print("1. Crack ZIP without wordlist")
    print("2. Crack ZIP with wordlist")
    choice = input("Enter your choice (1/2): ")
    zip_file = input("Enter ZIP file path: ")
    if choice == '1':
        max_length = int(input("Enter maximum password length: "))
        crack_zip(zip_file, max_length)
    elif choice == '2':
        wordlist = input("Enter wordlist file path: ")
        crack_zip_wordlist(zip_file, wordlist)
    else:
        print("Invalid choice")
if __name__ == "__main__":
    main()
