import random

def generate_secret():
    secret = random.sample('0123456789', 4)
    return ''.join(secret)

def get_feedback(guess, secret):
    A = sum([1 for i in range(4) if guess[i] == secret[i]])  # 位置和數字都對的數量
    B = sum([1 for i in range(4) if guess[i] != secret[i] and guess[i] in secret])  # 位置錯誤但數字對的數量
    return A, B

def play_game():
    secret = generate_secret()
    print("歡迎來到 1A2B 遊戲！")
    print("我已經選好了四位數字，請開始猜測。")
    
    attempts = 0
    while True:
        guess = input("請輸入您的猜測 (四位數字)：")
  
        if len(guess) != 4 or not guess.isdigit():
            print("請輸入四位數字！")
            continue
        
        attempts += 1
        A, B = get_feedback(guess, secret)
        
        if A == 4:
            print(f"恭喜你！猜對了，秘密數字是 {secret}。你總共猜了 {attempts} 次。")
            break
        else:
            print(f"{A}A{B}B，請繼續猜測。")

if __name__ == '__main__':
    play_game()