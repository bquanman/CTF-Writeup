### Another

![image](https://user-images.githubusercontent.com/75996090/208592457-5e6bc052-7e31-491b-a076-be7d7971a996.png)

Đây là tất cả các câu hỏi chúng ta nhận được khi netcat

![image](https://user-images.githubusercontent.com/75996090/208592673-59fd1b1f-69fb-45f6-936e-a655b12145dc.png)

#### [1]. What was the malicious process that was run and its SHA-1?

Sau khi rà quét mã độc cả bằng thủ công và bằng công cụ, mình đều ko thấy dấu hiệu của malware trong file bài cho. Vì vậy có thể malware đã bị xóa

Bằng cách xem lịch sử tải xuống, mình thấy người dùng đã tải xuống một file `uwu.exe` từ https://drive.google.com/file/d/1mgGa_t6eWA0jpb7AQdwUW_o_PYJRKs9t/view

![image](https://user-images.githubusercontent.com/75996090/208605261-5226adb3-e1af-4d3c-b7d0-fd2411daae54.png)

Tính sha1sum của uwu.exe

```
$ sha1sum uwu.exec
8c6e53c2ca267bed59da4587c53f1c5ea5a8e9ff  uwu.exec
```

Tuy nhiên khi submit `uwu.exe-8c6e53c2ca267bed59da4587c53f1c5ea5a8e9ff` thì đáp án bị sai. Mình có hỏi thì tác giả nói là mình cần tìm tên của nó lúc nó được thực thi. Nên mình nghĩ sau khi được tải xuống với tên `uwu.exe` thì nó đã bị đổi tên và thực thi sau đó. Vậy `uwu` là tên gốc để submit cho câu hỏi 4

![image](https://user-images.githubusercontent.com/75996090/208622324-224fac9b-44a2-4779-bf4c-9e5de3d41e75.png)

Để tìm tên malware lúc nó được thực thi, mình dùng [PECmd](https://f001.backblazeb2.com/file/EricZimmermanTools/net6/PECmd.zip) để phân tích prefetch file tìm dấu hiệu của các chương trình đã được chạy

![image](https://user-images.githubusercontent.com/75996090/208625474-f115b18c-e8cf-4553-be8d-454a67af4904.png)

Phân tích cho thấy có một file `svchost.exe` được thực thi ở thư mục `Downloads` và `Downloads/CODE-STUDY`. Khi dịch ngược uwu.exe mình thấy đây là 1 file ransomware thực hiện mã hóa tất cả các file có đuôi .txt ở thư mục hiện tại và đổi thành đuôi .uwu, vì vậy lí do svchost.exe xuất hiện ở CODE-STUDY là vì nó đã được di chuyển tới đây để mã hóa các file .txt. Còn lí do nó tên là svchost.exe có thể là vì kẻ tấn công muốn fake tiến trình vs tiến trình hệ thống.

Tới đây có thể kết luận tên malware tại thời điểm được thực thi là svchost.exe

> Answer To Question 1: `svchost.exe-8c6e53c2ca267bed59da4587c53f1c5ea5a8e9ff`

> Answer To Question 4: `uwu`

#### [2]. Where does the malicious process come from?

Đã tìm thấy bên trên, mã độc đc tải xuống từ drive. 

Nhưng để submit câu trả lời thì cẩn thận mấy cái xxxx/xxx/xxx/xxx

> Answer To Question 2: `https://drive.google.com/file/d/1mgGa_t6eWA0jpb7AQdwUW_o_PYJRKs9t/view`

#### [3]. Total running time of malicious process?

Mình có thử tìm thông tin từ prefetch file, event id 4688, 4689 và nhiều cách khác nhau nhưng ko có thông tin cho câu hỏi này. 

Do khi ransomware chạy thì các file bị modify nên ta có thể lấy thời gian file cuối cùng bị modified trừ thời gian file đầu tiên bị modified để tính tổng thời gian ransomware chạy và cách này đã hoạt động.

![image](https://user-images.githubusercontent.com/75996090/208640350-519f22b5-676d-405d-a779-a6fd730e94db.png)

> Answer To Question 3: `2022/12/17-01:23:28`

#### [5]. The secret value in the malicious process's code is?

`uwu.exe` được compile từ python3.7. Mã nguồn sau khi decompile

```python
import winreg
s_box = (99, 124, 119, 123, 242, 107, 111, 197, 48, 1, 103, 43, 254, 215, 171, 118, 202, 130, 201, 125, 250, 89, 71, 240, 173, 212, 162, 175, 156, 164, 114, 192, 183, 253, 147, 38, 54, 63, 247, 204, 52, 165, 229, 241, 113, 216, 49, 21, 4, 199, 35, 195, 24, 150, 5, 154, 7, 18, 128, 226, 235, 39, 178, 117, 9, 131, 44, 26, 27, 110, 90, 160, 82, 59, 214, 179, 41, 227, 47, 132, 83, 209, 0, 237, 32, 252, 177, 91, 106, 203, 190, 57, 74, 76, 88, 207, 208, 239, 170, 251, 67, 77, 51, 133, 69, 249, 2, 127, 80, 60, 159, 168, 81, 163, 64, 143, 146, 157, 56, 245, 188, 182, 218, 33, 16, 255, 243, 210, 205, 12, 19, 236, 95, 151, 68, 23, 196, 167, 126, 61, 100, 93, 25, 115, 96, 129, 79, 220, 34, 42, 144, 136, 70, 238, 184, 20, 222, 94, 11, 219, 224, 50, 58, 10, 73, 6, 36, 92, 194, 211, 172, 98, 145, 149, 228, 121, 231, 200, 55, 109, 141, 213, 78, 169, 108, 86, 244, 234, 101, 122, 174, 8, 186, 120, 37, 46, 28, 166, 180, 198, 232, 221, 116, 31, 75, 189, 139, 138, 112, 62, 181, 102, 72, 3, 246, 14, 97, 53, 87, 185, 134, 193, 29, 158, 225, 248, 152, 17, 105, 217, 142, 148, 155, 30, 135, 233, 206, 85, 40, 223, 140, 161, 137, 13, 191, 230, 66, 104, 65, 153, 45, 15, 176, 84, 187, 22)
inv_s_box = (82, 9, 106, 213, 48, 54, 165, 56, 191, 64, 163, 158, 129, 243, 215, 251, 124, 227, 57, 130, 155, 47, 255, 135, 52, 142, 67, 68, 196, 222, 233, 203, 84, 123, 148, 50, 166, 194, 35, 61, 238, 76, 149, 11, 66, 250, 195, 78, 8, 46, 161, 102, 40, 217, 36, 178, 118, 91, 162, 73, 109, 139, 209, 37, 114, 248, 246, 100, 134, 104, 152, 22, 212, 164, 92, 204, 93, 101, 182, 146, 108, 112, 72, 80, 253, 237, 185, 218, 94, 21, 70, 87, 167, 141, 157, 132, 144, 216, 171, 0, 140, 188, 211, 10, 247, 228, 88, 5, 184, 179, 69, 6, 208, 44, 30, 143, 202, 63, 15, 2, 193, 175, 189, 3, 1, 19, 138, 107, 58, 145, 17, 65, 79, 103, 220, 234, 151, 242, 207, 206, 240, 180, 230, 115, 150, 172, 116, 34, 231, 173, 53, 133, 226, 249, 55, 232, 28, 117, 223, 110, 71, 241, 26, 113, 29, 41, 197, 137, 111, 183, 98, 14, 170, 24, 190, 27, 252, 86, 62, 75, 198, 210, 121, 32, 154, 219, 192, 254, 120, 205, 90, 244, 31, 221, 168, 51, 136, 7, 199, 49, 177, 18, 16, 89, 39, 128, 236, 95, 96, 81, 127, 169, 25, 181, 74, 13, 45, 229, 122, 159, 147, 201, 156, 239, 160, 224, 59, 77, 174, 42, 245, 176, 200, 235, 187, 60, 131, 83, 153, 97, 23, 43, 4, 126, 186, 119, 214, 38, 225, 105, 20, 99, 85, 33, 12, 125)

def sub_bytes(s):
    for i in range(4):
        for j in range(4):
            s[i][j] = s_box[s[i][j]]




def inv_sub_bytes(s):
    for i in range(4):
        for j in range(4):
            s[i][j] = inv_s_box[s[i][j]]




def shift_rows(s):
    (s[0][1], s[1][1], s[2][1], s[3][1]) = (s[1][1], s[2][1], s[3][1], s[0][1])
    (s[0][2], s[1][2], s[2][2], s[3][2]) = (s[2][2], s[3][2], s[0][2], s[1][2])
    (s[0][3], s[1][3], s[2][3], s[3][3]) = (s[3][3], s[0][3], s[1][3], s[2][3])


def inv_shift_rows(s):
    (s[0][1], s[1][1], s[2][1], s[3][1]) = (s[3][1], s[0][1], s[1][1], s[2][1])
    (s[0][2], s[1][2], s[2][2], s[3][2]) = (s[2][2], s[3][2], s[0][2], s[1][2])
    (s[0][3], s[1][3], s[2][3], s[3][3]) = (s[1][3], s[2][3], s[3][3], s[0][3])


def add_round_key(s, k):
    for i in range(4):
        for j in range(4):
            s[i][j] ^= k[i][j]




xtime = lambda a: if a & 128:
(a << 1 ^ 27) & 255None << 1

def mix_single_column(a):
    t = a[0] ^ a[1] ^ a[2] ^ a[3]
    u = a[0]
    a[0] ^= t ^ xtime(a[0] ^ a[1])
    a[1] ^= t ^ xtime(a[1] ^ a[2])
    a[2] ^= t ^ xtime(a[2] ^ a[3])
    a[3] ^= t ^ xtime(a[3] ^ u)


def mix_columns(s):
    for i in range(4):
        mix_single_column(s[i])



def inv_mix_columns(s):
    for i in range(4):
        u = xtime(xtime(s[i][0] ^ s[i][2]))
        v = xtime(xtime(s[i][1] ^ s[i][3]))
        s[i][0] ^= u
        s[i][1] ^= v
        s[i][2] ^= u
        s[i][3] ^= v

    mix_columns(s)

r_con = (0, 1, 2, 4, 8, 16, 32, 64, 128, 27, 54, 108, 216, 171, 77, 154, 47, 94, 188, 99, 198, 151, 53, 106, 212, 179, 125, 250, 239, 197, 145, 57)

def bytes2matrix(text):
    ''' Converts a 16-byte array into a 4x4 matrix.  '''
    return (lambda .0 = None: [ list(text[i:i + 4]) for i in .0 ])(range(0, len(text), 4))


def matrix2bytes(matrix):
    ''' Converts a 4x4 matrix into a 16-byte array.  '''
    return bytes(sum(matrix, []))


def xor_bytes(a, b):
    """ Returns a new byte array with the elements xor'ed. """
    return bytes((lambda .0: pass)(zip(a, b)))


def inc_bytes(a):
    ''' Returns a new byte array with the value increment by 1 '''
    out = list(a)
    for i in reversed(range(len(out))):
        if out[i] == 255:
            out[i] = 0
            continue
        out[i] += 1

    return bytes(out)


def pad(plaintext):
    '''
    Pads the given plaintext with PKCS#7 padding to a multiple of 16 bytes.
    Note that if the plaintext size is a multiple of 16,
    a whole block will be added.
    '''
    padding_len = 16 - len(plaintext) % 16
    padding = bytes([
        padding_len] * padding_len)
    return plaintext + padding


def unpad(plaintext):
    '''
    Removes a PKCS#7 padding, returning the unpadded text and ensuring the
    padding was correct.
    '''
    padding_len = plaintext[-1]
    if not padding_len > 0:
        raise AssertionError
    message = None[:-padding_len]
    padding = plaintext[-padding_len:]
    if not None((lambda .0 = None: pass)(padding)):
        raise AssertionError


def split_blocks(message, block_size, require_padding = (16, True)):
    if len(message) % block_size == 0 and require_padding:
        raise AssertionError
    return (lambda .0 = None: [ message[i:i + 16] for i in .0 ])(range(0, len(message), block_size))


class AES:
    '''
    Class for AES-128 encryption with CBC mode and PKCS#7.
    This is a raw implementation of AES, without key stretching or IV
    management. Unless you need that, please use `encrypt` and `decrypt`.
    '''
    rounds_by_key_size = {
        16: 10,
        24: 12,
        32: 14 }

    def __init__(self, master_key):
        '''
        Initializes the object with a given key.
        '''
        if not len(master_key) in AES.rounds_by_key_size:
            raise AssertionError
        self.n_rounds = None.rounds_by_key_size[len(master_key)]
        self._key_matrices = self._expand_key(master_key)


    def _expand_key(self, master_key):
        '''
        Expands and returns a list of key matrices for the given master_key.
        '''
        key_columns = bytes2matrix(master_key)
        iteration_size = len(master_key) // 4
        i = 1
        while len(key_columns) < (self.n_rounds + 1) * 4:
            word = list(key_columns[-1])
            if len(key_columns) % iteration_size == 0:
                word.append(word.pop(0))
                word = (lambda .0: [ s_box[b] for b in .0 ])(word)
                word[0] ^= r_con[i]
                i += 1
            elif len(master_key) == 32 and len(key_columns) % iteration_size == 4:
                word = (lambda .0: [ s_box[b] for b in .0 ])(word)
            word = xor_bytes(word, key_columns[-iteration_size])
            key_columns.append(word)
        return (lambda .0 = None: [ key_columns[4 * i:4 * (i + 1)] for i in .0 ])(range(len(key_columns) // 4))


    def encrypt_block(self, plaintext):
        '''
        Encrypts a single block of 16 byte long plaintext.
        '''
        if not len(plaintext) == 16:
            raise AssertionError
        plain_state = None(plaintext)
        add_round_key(plain_state, self._key_matrices[0])
        for i in range(1, self.n_rounds):
            sub_bytes(plain_state)
            shift_rows(plain_state)
            mix_columns(plain_state)
            add_round_key(plain_state, self._key_matrices[i])

        sub_bytes(plain_state)
        shift_rows(plain_state)
        add_round_key(plain_state, self._key_matrices[-1])
        return matrix2bytes(plain_state)


    def decrypt_block(self, ciphertext):
        '''
        Decrypts a single block of 16 byte long ciphertext.
        '''
        if not len(ciphertext) == 16:
            raise AssertionError
        cipher_state = None(ciphertext)
        add_round_key(cipher_state, self._key_matrices[-1])
        inv_shift_rows(cipher_state)
        inv_sub_bytes(cipher_state)
        for i in range(self.n_rounds - 1, 0, -1):
            add_round_key(cipher_state, self._key_matrices[i])
            inv_mix_columns(cipher_state)
            inv_shift_rows(cipher_state)
            inv_sub_bytes(cipher_state)

        add_round_key(cipher_state, self._key_matrices[0])
        return matrix2bytes(cipher_state)


    def encrypt_cbc(self, plaintext, iv):
        '''
        Encrypts `plaintext` using CBC mode and PKCS#7 padding, with the given
        initialization vector (iv).
        '''
        if not len(iv) == 16:
            raise AssertionError
        plaintext = None(plaintext)
        blocks = []
        previous = iv
        for plaintext_block in split_blocks(plaintext):
            block = self.encrypt_block(xor_bytes(plaintext_block, previous))
            blocks.append(block)
            previous = block

        return b''.join(blocks)


    def decrypt_cbc(self, ciphertext, iv):
        '''
        Decrypts `ciphertext` using CBC mode and PKCS#7 padding, with the given
        initialization vector (iv).
        '''
        if not len(iv) == 16:
            raise AssertionError
        blocks = None
        previous = iv
        for ciphertext_block in split_blocks(ciphertext):
            blocks.append(xor_bytes(previous, self.decrypt_block(ciphertext_block)))
            previous = ciphertext_block

        return unpad(b''.join(blocks))


import hashlib
from os import listdir, getcwd, rename
from os.path import isfile, join
REG_PATH = 'SYSTEM\\\\ControlSet001\\\\Control\\\\ComputerName\\\\ComputerName'
AES_KEY_SIZE = 16
IV_SIZE = 16

def get_reg(name):
Warning: Stack history is not empty!
Warning: block stack is not empty!

    try:
        registry_key = winreg.OpenKey(winreg.HKEY_LOCAL_MACHINE, REG_PATH, 0, winreg.KEY_READ)
        (value, regtype) = winreg.QueryValueEx(registry_key, name)
        winreg.CloseKey(registry_key)
        return value
        except WindowsError:
            return None
        else:
            return None



def get_key_iv(password, workload = (100000,)):
    '''
    Stretches the password and extracts an AES key, an HMAC key and an AES
    initialization vector.
    '''
    stretched = hashlib.pbkdf2_hmac('sha256', password, b'saltysadlygotkey', workload, AES_KEY_SIZE + IV_SIZE)
    aes_key = stretched[:AES_KEY_SIZE]
    stretched = stretched[AES_KEY_SIZE:]
    iv = stretched[:IV_SIZE]
    return (aes_key, iv)


def encrypt(KEY, plaintext, IV):
    ciphertext = AES(KEY).encrypt_cbc(plaintext, IV)
    return ciphertext

PATH = getcwd()
files = (lambda .0: [ f for f in .0 if isfile(join(PATH, f)) ])(listdir(PATH))
```

Phân tích cho thấy chương trình cơ bản là mã hóa các file trong thư mục hiện tại bằng AES_CBC với key và iv được gen từ hàm get_key_iv. Tuy nhiên ko thấy dấu hiệu hàm `get_key_iv` được sử dụng, vì thế mình nhờ autopsy tìm thêm thông tin và tìm đc full source (cũng ko hiểu tại sao nhưng thôi kệ tập trung làm cho nhanh chứ suy nghĩ làm gì =]]] )

![image](https://user-images.githubusercontent.com/75996090/208643867-4e229666-1d46-4227-a869-5913f7eaff82.png)

get_key_iv lấy tham số truyền vào là ComputerName, giá trị này có thể tìm thấy từ registry hive

![image](https://user-images.githubusercontent.com/75996090/208657793-74f6d33e-617c-4ff0-a4c3-a053aa9f68f2.png)

Đây cũng chính là `secret value` trong câu hỏi

> Answer To Question 5: `IX`

#### [6]. There is a very important file for me but it is encrypted can you help me to recover it?

Có đủ thông tin rồi, giờ là lúc giải mã thôi...

```python
#import winreg
s_box = (99, 124, 119, 123, 242, 107, 111, 197, 48, 1, 103, 43, 254, 215, 171, 118, 202, 130, 201, 125, 250, 89, 71, 240, 173, 212, 162, 175, 156, 164, 114, 192, 183, 253, 147, 38, 54, 63, 247, 204, 52, 165, 229, 241, 113, 216, 49, 21, 4, 199, 35, 195, 24, 150, 5, 154, 7, 18, 128, 226, 235, 39, 178, 117, 9, 131, 44, 26, 27, 110, 90, 160, 82, 59, 214, 179, 41, 227, 47, 132, 83, 209, 0, 237, 32, 252, 177, 91, 106, 203, 190, 57, 74, 76, 88, 207, 208, 239, 170, 251, 67, 77, 51, 133, 69, 249, 2, 127, 80, 60, 159, 168, 81, 163, 64, 143, 146, 157, 56, 245, 188, 182, 218, 33, 16, 255, 243, 210, 205, 12, 19, 236, 95, 151, 68, 23, 196, 167, 126, 61, 100, 93, 25, 115, 96, 129, 79, 220, 34, 42, 144, 136, 70, 238, 184, 20, 222, 94, 11, 219, 224, 50, 58, 10, 73, 6, 36, 92, 194, 211, 172, 98, 145, 149, 228, 121, 231, 200, 55, 109, 141, 213, 78, 169, 108, 86, 244, 234, 101, 122, 174, 8, 186, 120, 37, 46, 28, 166, 180, 198, 232, 221, 116, 31, 75, 189, 139, 138, 112, 62, 181, 102, 72, 3, 246, 14, 97, 53, 87, 185, 134, 193, 29, 158, 225, 248, 152, 17, 105, 217, 142, 148, 155, 30, 135, 233, 206, 85, 40, 223, 140, 161, 137, 13, 191, 230, 66, 104, 65, 153, 45, 15, 176, 84, 187, 22)
inv_s_box = (82, 9, 106, 213, 48, 54, 165, 56, 191, 64, 163, 158, 129, 243, 215, 251, 124, 227, 57, 130, 155, 47, 255, 135, 52, 142, 67, 68, 196, 222, 233, 203, 84, 123, 148, 50, 166, 194, 35, 61, 238, 76, 149, 11, 66, 250, 195, 78, 8, 46, 161, 102, 40, 217, 36, 178, 118, 91, 162, 73, 109, 139, 209, 37, 114, 248, 246, 100, 134, 104, 152, 22, 212, 164, 92, 204, 93, 101, 182, 146, 108, 112, 72, 80, 253, 237, 185, 218, 94, 21, 70, 87, 167, 141, 157, 132, 144, 216, 171, 0, 140, 188, 211, 10, 247, 228, 88, 5, 184, 179, 69, 6, 208, 44, 30, 143, 202, 63, 15, 2, 193, 175, 189, 3, 1, 19, 138, 107, 58, 145, 17, 65, 79, 103, 220, 234, 151, 242, 207, 206, 240, 180, 230, 115, 150, 172, 116, 34, 231, 173, 53, 133, 226, 249, 55, 232, 28, 117, 223, 110, 71, 241, 26, 113, 29, 41, 197, 137, 111, 183, 98, 14, 170, 24, 190, 27, 252, 86, 62, 75, 198, 210, 121, 32, 154, 219, 192, 254, 120, 205, 90, 244, 31, 221, 168, 51, 136, 7, 199, 49, 177, 18, 16, 89, 39, 128, 236, 95, 96, 81, 127, 169, 25, 181, 74, 13, 45, 229, 122, 159, 147, 201, 156, 239, 160, 224, 59, 77, 174, 42, 245, 176, 200, 235, 187, 60, 131, 83, 153, 97, 23, 43, 4, 126, 186, 119, 214, 38, 225, 105, 20, 99, 85, 33, 12, 125)

def sub_bytes(s):
    for i in range(4):
        for j in range(4):
            s[i][j] = s_box[s[i][j]]




def inv_sub_bytes(s):
    for i in range(4):
        for j in range(4):
            s[i][j] = inv_s_box[s[i][j]]




def shift_rows(s):
    (s[0][1], s[1][1], s[2][1], s[3][1]) = (s[1][1], s[2][1], s[3][1], s[0][1])
    (s[0][2], s[1][2], s[2][2], s[3][2]) = (s[2][2], s[3][2], s[0][2], s[1][2])
    (s[0][3], s[1][3], s[2][3], s[3][3]) = (s[3][3], s[0][3], s[1][3], s[2][3])


def inv_shift_rows(s):
    (s[0][1], s[1][1], s[2][1], s[3][1]) = (s[3][1], s[0][1], s[1][1], s[2][1])
    (s[0][2], s[1][2], s[2][2], s[3][2]) = (s[2][2], s[3][2], s[0][2], s[1][2])
    (s[0][3], s[1][3], s[2][3], s[3][3]) = (s[1][3], s[2][3], s[3][3], s[0][3])


def add_round_key(s, k):
    for i in range(4):
        for j in range(4):
            s[i][j] ^= k[i][j]

# learned from https://web.archive.org/web/20100626212235/http://cs.ucsb.edu/~koc/cs178/projects/JT/aes.c
xtime = lambda a: (((a << 1) ^ 0x1B) & 0xFF) if (a & 0x80) else (a << 1)

def mix_single_column(a):
    # see Sec 4.1.2 in The Design of Rijndael
    t = a[0] ^ a[1] ^ a[2] ^ a[3]
    u = a[0]
    a[0] ^= t ^ xtime(a[0] ^ a[1])
    a[1] ^= t ^ xtime(a[1] ^ a[2])
    a[2] ^= t ^ xtime(a[2] ^ a[3])
    a[3] ^= t ^ xtime(a[3] ^ u)


def mix_columns(s):
    for i in range(4):
        mix_single_column(s[i])


def inv_mix_columns(s):
    # see Sec 4.1.3 in The Design of Rijndael
    for i in range(4):
        u = xtime(xtime(s[i][0] ^ s[i][2]))
        v = xtime(xtime(s[i][1] ^ s[i][3]))
        s[i][0] ^= u
        s[i][1] ^= v
        s[i][2] ^= u
        s[i][3] ^= v

    mix_columns(s)


r_con = (0, 1, 2, 4, 8, 16, 32, 64, 128, 27, 54, 108, 216, 171, 77, 154, 47, 94, 188, 99, 198, 151, 53, 106, 212, 179, 125, 250, 239, 197, 145, 57)

def bytes2matrix(text):
    """ Converts a 16-byte array into a 4x4 matrix.  """
    return [list(text[i:i+4]) for i in range(0, len(text), 4)]

def matrix2bytes(matrix):
    """ Converts a 4x4 matrix into a 16-byte array.  """
    return bytes(sum(matrix, []))

def xor_bytes(a, b):
    """ Returns a new byte array with the elements xor'ed. """
    return bytes(i^j for i, j in zip(a, b))

def inc_bytes(a):
    """ Returns a new byte array with the value increment by 1 """
    out = list(a)
    for i in reversed(range(len(out))):
        if out[i] == 0xFF:
            out[i] = 0
        else:
            out[i] += 1
            break
    return bytes(out)

def pad(plaintext):
    """
    Pads the given plaintext with PKCS#7 padding to a multiple of 16 bytes.
    Note that if the plaintext size is a multiple of 16,
    a whole block will be added.
    """
    padding_len = 16 - (len(plaintext) % 16)
    padding = bytes([padding_len] * padding_len)
    return plaintext + padding

def unpad(plaintext):
    """
    Removes a PKCS#7 padding, returning the unpadded text and ensuring the
    padding was correct.
    """
    padding_len = plaintext[-1]
    assert padding_len > 0
    message, padding = plaintext[:-padding_len], plaintext[-padding_len:]
    assert all(p == padding_len for p in padding)
    return message

def split_blocks(message, block_size=16, require_padding=True):
        assert len(message) % block_size == 0 or not require_padding
        return [message[i:i+16] for i in range(0, len(message), block_size)]



class AES:
    """
    Class for AES-128 encryption with CBC mode and PKCS#7.
    This is a raw implementation of AES, without key stretching or IV
    management. Unless you need that, please use `encrypt` and `decrypt`.
    """
    rounds_by_key_size = {16: 10, 24: 12, 32: 14}
    def __init__(self, master_key):
        """
        Initializes the object with a given key.
        """
        assert len(master_key) in AES.rounds_by_key_size
        self.n_rounds = AES.rounds_by_key_size[len(master_key)]
        self._key_matrices = self._expand_key(master_key)

    def _expand_key(self, master_key):
        """
        Expands and returns a list of key matrices for the given master_key.
        """
        # Initialize round keys with raw key material.
        key_columns = bytes2matrix(master_key)
        iteration_size = len(master_key) // 4

        i = 1
        while len(key_columns) < (self.n_rounds + 1) * 4:
            # Copy previous word.
            word = list(key_columns[-1])

            # Perform schedule_core once every "row".
            if len(key_columns) % iteration_size == 0:
                # Circular shift.
                word.append(word.pop(0))
                # Map to S-BOX.
                word = [s_box[b] for b in word]
                # XOR with first byte of R-CON, since the others bytes of R-CON are 0.
                word[0] ^= r_con[i]
                i += 1
            elif len(master_key) == 32 and len(key_columns) % iteration_size == 4:
                # Run word through S-box in the fourth iteration when using a
                # 256-bit key.
                word = [s_box[b] for b in word]

            # XOR with equivalent word from previous iteration.
            word = xor_bytes(word, key_columns[-iteration_size])
            key_columns.append(word)

        # Group key words in 4x4 byte matrices.
        return [key_columns[4*i : 4*(i+1)] for i in range(len(key_columns) // 4)]

    def encrypt_block(self, plaintext):
        """
        Encrypts a single block of 16 byte long plaintext.
        """
        assert len(plaintext) == 16

        plain_state = bytes2matrix(plaintext)

        add_round_key(plain_state, self._key_matrices[0])

        for i in range(1, self.n_rounds):
            sub_bytes(plain_state)
            shift_rows(plain_state)
            mix_columns(plain_state)
            add_round_key(plain_state, self._key_matrices[i])

        sub_bytes(plain_state)
        shift_rows(plain_state)
        add_round_key(plain_state, self._key_matrices[-1])

        return matrix2bytes(plain_state)

    def decrypt_block(self, ciphertext):
        """
        Decrypts a single block of 16 byte long ciphertext.
        """
        assert len(ciphertext) == 16

        cipher_state = bytes2matrix(ciphertext)

        add_round_key(cipher_state, self._key_matrices[-1])
        inv_shift_rows(cipher_state)
        inv_sub_bytes(cipher_state)

        for i in range(self.n_rounds - 1, 0, -1):
            add_round_key(cipher_state, self._key_matrices[i])
            inv_mix_columns(cipher_state)
            inv_shift_rows(cipher_state)
            inv_sub_bytes(cipher_state)

        add_round_key(cipher_state, self._key_matrices[0])

        return matrix2bytes(cipher_state)

    def encrypt_cbc(self, plaintext, iv):
        """
        Encrypts `plaintext` using CBC mode and PKCS#7 padding, with the given
        initialization vector (iv).
        """
        assert len(iv) == 16

        plaintext = pad(plaintext)

        blocks = []
        previous = iv
        for plaintext_block in split_blocks(plaintext):
            # CBC mode encrypt: encrypt(plaintext_block XOR previous)
            block = self.encrypt_block(xor_bytes(plaintext_block, previous))
            blocks.append(block)
            previous = block

        return b''.join(blocks)

    def decrypt_cbc(self, ciphertext, iv):
        """
        Decrypts `ciphertext` using CBC mode and PKCS#7 padding, with the given
        initialization vector (iv).
        """
        assert len(iv) == 16

        blocks = []
        previous = iv
        for ciphertext_block in split_blocks(ciphertext):
            # CBC mode decrypt: previous XOR decrypt(ciphertext)
            blocks.append(xor_bytes(previous, self.decrypt_block(ciphertext_block)))
            previous = ciphertext_block

        return unpad(b''.join(blocks))
        
import base64
import os

import hashlib
from os import listdir, getcwd, rename
from os.path import isfile, join
REG_PATH = 'SYSTEM\\\\ControlSet001\\\\Control\\\\ComputerName\\\\ComputerName'
AES_KEY_SIZE = 16
IV_SIZE = 16

# def get_reg(name):
# Warning: Stack history is not empty!
# Warning: block stack is not empty!

#     try:
#         registry_key = winreg.OpenKey(winreg.HKEY_LOCAL_MACHINE, REG_PATH, 0, winreg.KEY_READ)
#         (value, regtype) = winreg.QueryValueEx(registry_key, name)
#         winreg.CloseKey(registry_key)
#         return value
#         except WindowsError:
#             return None
#         else:
#             return None



def get_key_iv(password, workload = 100000):
    '''
    Stretches the password and extracts an AES key, an HMAC key and an AES
    initialization vector.
    '''
    stretched = hashlib.pbkdf2_hmac('sha256', password, b'saltysadlygotkey', workload, AES_KEY_SIZE + IV_SIZE)
    aes_key = stretched[:AES_KEY_SIZE]
    stretched = stretched[AES_KEY_SIZE:]
    iv = stretched[:IV_SIZE]
    return (aes_key, iv)


def encrypt(KEY, plaintext, IV):
    ciphertext = AES(KEY).encrypt_cbc(plaintext, IV)
    return ciphertext

key, iv = get_key_iv(b'IX')

files = os.listdir()
for file in files:
    with open(file, 'rb') as f:
        ciphertxt = f.read()
    try:
        plaintext = AES(key).decrypt_cbc(ciphertxt,iv)
        dec_b64 = base64.b64decode(plaintext)
        print (dec_b64.decode(),file)
    except Exception as e:
        print(f"Error decrypting file {file}: {e}")
        continue
```

Dựa vào ví dụ đáp án cho thấy câu trả lời cho câu hỏi này là sự kết hợp của tên file và nội dung trong file `KHAI-0303-WAITING_FOR_YOU = KHAI-0303.txt + WAITING_FOR_YOU`

Sử dụng regex như nội dung mẫu để tìm nội dung important file

![image](https://user-images.githubusercontent.com/75996090/208668922-e3ffbb94-5550-450c-bddd-811b69d232e8.png)

Bingo! grep phát ra luôn _:D_

> Answer To Question 6: `SITI-3301-G00D_J0B_Y0U_C4UGHT_M3`

![image](https://user-images.githubusercontent.com/75996090/208670193-e72715db-db5f-4dcd-bf10-4877719929bd.png)

#### Flag: ISITDTU{K4P3_CH0053_Y0U}
