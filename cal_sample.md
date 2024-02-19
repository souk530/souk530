CLI（コマンドラインインターフェイス）を使用した簡単な電卓アプリをPythonで作成します。このアプリは2桁以下の数値の入力を受け付け、結果の最大桁数を4桁に制限します。四則演算（加算、減算、乗算、除算）をサポートします。

```python
def get_input(prompt):
    while True:
        try:
            # 入力を受け取る
            user_input = input(prompt)
            # 入力を整数に変換
            number = int(user_input)
            # 2桁以下の数値かどうかをチェック
            if len(user_input) > 2:
                raise ValueError
            return number
        except ValueError:
            print("2桁以下の数値を入力してください。")

def calculate(a, b, operation):
    # 演算を実行
    if operation == '+':
        return a + b
    elif operation == '-':
        return a - b
    elif operation == '*':
        return a * b
    elif operation == '/':
        if b != 0:
            return a / b
        else:
            print("0で割ることはできません。")
            return None
    else:
        print("無効な演算です。")
        return None

def main():
    print("簡易電卓アプリへようこそ。終了するにはCtrl+Cを押してください。")

    while True:
        # 数値の入力を受け取る
        a = get_input("数値1 (2桁以下): ")
        b = get_input("数値2 (2桁以下): ")

        # 演算子の入力を受け取る
        operation = input("演算を選択してください (+, -, *, /): ")

        # 計算を実行
        result = calculate(a, b, operation)

        # 結果を表示
        if result is not None:
            # 結果の桁数が4桁を超える場合は調整
            result_str = str(result)
            if len(result_str) > 4:
                if '.' in result_str:
                    # 小数点が含まれている場合は、小数点以下を調整
                    result_str = result_str[:4]
                else:
                    # 整数の場合は単純に4桁に切り詰め
                    result_str = result_str[:4]
            print("結果: ", result_str)
        print("")

if __name__ == "__main__":
    main()
```

このプログラムは、ユーザーから2つの2桁以下の数値と演算子を入力として受け取り、選択した演算を行います。結果は最大で4桁まで表示されます。0での除算や無効な演算を入力した場合はエラーメッセージを表示します。プログラムを終了するには、Ctrl+Cを押します。
