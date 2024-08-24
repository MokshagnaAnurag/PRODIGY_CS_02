# PRODIGY_CS_02

To develop a simple image encryption tool using pixel manipulation, you can follow these steps. The idea is to perform operations on pixel values to encode and decode the image. Here, I'll guide you through a basic approach using Python with the Pillow library for image handling.

### Prerequisites

Make sure you have Python and the Pillow library installed. You can install Pillow using pip if you don't have it already:

```bash
pip install pillow
```

### Code Implementation

Here's a simple example of how you can create an image encryption and decryption tool. This tool will use a basic XOR operation to manipulate pixel values for encryption and decryption. The XOR operation is simple but effective for this purpose.

#### Step 1: Import Required Libraries

```python
from PIL import Image
import numpy as np
```

#### Step 2: Define Encryption and Decryption Functions

```python
def xor_encrypt_decrypt(pixel, key):
    return pixel ^ key

def process_image(image_path, key, mode='encrypt'):
    image = Image.open(image_path)
    pixels = np.array(image)
    
    if mode == 'encrypt':
        processed_pixels = np.vectorize(lambda pixel: xor_encrypt_decrypt(pixel, key))(pixels)
    elif mode == 'decrypt':
        processed_pixels = np.vectorize(lambda pixel: xor_encrypt_decrypt(pixel, key))(pixels)
    else:
        raise ValueError("Mode must be 'encrypt' or 'decrypt'")
    
    processed_image = Image.fromarray(processed_pixels.astype(np.uint8))
    return processed_image
```

#### Step 3: Save and Load Images

```python
def save_image(image, file_path):
    image.save(file_path)

def load_image(file_path):
    return Image.open(file_path)
```

#### Step 4: Create Main Function to Handle Encryption/Decryption

```python
def main():
    input_image_path = 'input_image.png'  # Path to the image to be encrypted/decrypted
    encrypted_image_path = 'encrypted_image.png'
    decrypted_image_path = 'decrypted_image.png'
    key = 123  # Simple integer key for XOR operation
    
    # Encrypt the image
    encrypted_image = process_image(input_image_path, key, mode='encrypt')
    save_image(encrypted_image, encrypted_image_path)
    print(f'Encrypted image saved to {encrypted_image_path}')
    
    # Decrypt the image
    decrypted_image = process_image(encrypted_image_path, key, mode='decrypt')
    save_image(decrypted_image, decrypted_image_path)
    print(f'Decrypted image saved to {decrypted_image_path}')

if __name__ == '__main__':
    main()
```

### How It Works

1. **Image Loading**: Load the image using Pillow and convert it into a NumPy array for pixel manipulation.
2. **Encryption/Decryption**:
   - For encryption and decryption, apply the XOR operation with a key to each pixel value.
   - The XOR operation is symmetric, meaning the same function is used for both encryption and decryption.
3. **Save and Load**: Save the processed image and load images as needed.

### Testing and Usage

1. Place an image named `input_image.png` in the same directory as your script.
2. Run the script. It will create `encrypted_image.png` and `decrypted_image.png`.
3. Verify the results by viewing the images.


